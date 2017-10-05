---
title: Come bilanciare il carico delle macchine virtuali di Linux in Azure | Microsoft Docs
description: "Informazioni su come usare Azure Load Balancer per creare un'applicazione sicura e a disponibilità elevata in tre macchine virtuali di Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 7b3a089d2f6386afcc46cbc4377594be0d758fc6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-load-balance-linux-virtual-machines-in-azure-to-create-a-highly-available-application"></a><span data-ttu-id="6c4dd-103">Come bilanciare il carico per le macchine virtuali di Linux in Azure per creare un'applicazione a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="6c4dd-103">How to load balance Linux virtual machines in Azure to create a highly available application</span></span>
<span data-ttu-id="6c4dd-104">Il bilanciamento del carico offre un livello più elevato di disponibilità distribuendo le richieste in ingresso tra più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="6c4dd-105">In questa esercitazione vengono illustrati i diversi componenti di Azure Load Balancer che distribuiscono il traffico e garantiscono una disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-105">In this tutorial, you learn about the different components of the Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="6c4dd-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6c4dd-107">Creare un servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="6c4dd-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="6c4dd-108">Creare un probe di integrità per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="6c4dd-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="6c4dd-109">Creare regole del traffico di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="6c4dd-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="6c4dd-110">Usare cloud-init per creare un'applicazione di base Node.js</span><span class="sxs-lookup"><span data-stu-id="6c4dd-110">Use cloud-init to create a basic Node.js app</span></span>
> * <span data-ttu-id="6c4dd-111">Creare macchine virtuali e collegarsi a un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="6c4dd-111">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="6c4dd-112">Visualizzare un bilanciamento del carico in azione</span><span class="sxs-lookup"><span data-stu-id="6c4dd-112">View a load balancer in action</span></span>
> * <span data-ttu-id="6c4dd-113">Aggiungere e rimuovere macchine virtuali da un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="6c4dd-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6c4dd-114">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa esercitazione è necessario eseguire l'interfaccia della riga di comando di Azure versione 2.0.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6c4dd-115">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="6c4dd-116">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="6c4dd-117">Panoramica di Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="6c4dd-117">Azure load balancer overview</span></span>
<span data-ttu-id="6c4dd-118">Azure Load Balancer è un bilanciamento del carico di livello 4 (TCP, UDP) che offre disponibilità elevata mediante la distribuzione del traffico in ingresso nelle macchine virtuali integre.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="6c4dd-119">Un probe di integrità del bilanciamento del carico monitora una determinata porta in ogni VM e distribuisce il traffico solo a una VM operativa.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-119">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

<span data-ttu-id="6c4dd-120">Definire una configurazione IP front-end che contenga uno o più indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="6c4dd-121">Questa configurazione IP front-end garantisce l'accessibilità al bilanciamento del carico e alle applicazioni tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-121">This front-end IP configuration allows your load balancer and applications to be accessible over the Internet.</span></span> 

<span data-ttu-id="6c4dd-122">Le macchine virtuali si connettono a un bilanciamento del carico tramite la scheda di interfaccia di rete virtuale (NIC).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-122">Virtual machines connect to a load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="6c4dd-123">Per distribuire il traffico alle macchine virtuali, è necessario che un pool di indirizzi back-end contenga gli indirizzi IP delle schede di interfaccia di rete virtuale connesse al bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-123">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

<span data-ttu-id="6c4dd-124">Per controllare il flusso del traffico, è necessario definire le regole di bilanciamento del carico per porte e protocolli specifici che eseguono il mapping delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-124">To control the flow of traffic, you define load balancer rules for specific ports and protocols that map to your VMs.</span></span>

<span data-ttu-id="6c4dd-125">Se è stata eseguita l'esercitazione precedente per [creare un set di scalabilità della macchina virtuale](tutorial-create-vmss.md), è stato creato un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-125">If you followed the previous tutorial to [create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="6c4dd-126">Tutti questi componenti sono stati configurati come parte del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-126">All these components were configured for you as part of the scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="6c4dd-127">Creare un Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="6c4dd-127">Create Azure load balancer</span></span>
<span data-ttu-id="6c4dd-128">Questa sezione descrive dettagliatamente come creare e configurare ogni componente del bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-128">This section details how you can create and configure each component of the load balancer.</span></span> <span data-ttu-id="6c4dd-129">Per poter creare un servizio di bilanciamento del carico, è prima necessario creare un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="6c4dd-130">Nell'esempio seguente viene creato un gruppo di risorse denominato *myResourceGroupLoadBalancer* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-130">The following example creates a resource group named *myResourceGroupLoadBalancer* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="6c4dd-131">Creare un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="6c4dd-131">Create a public IP address</span></span>
<span data-ttu-id="6c4dd-132">Per accedere all'app in Internet, assegnare un indirizzo IP pubblico al servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-132">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="6c4dd-133">Creare un indirizzo IP pubblico con [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="6c4dd-134">Nell'esempio seguente viene creato un indirizzo IP pubblico denominato *myPublicIP* nel gruppo di risorse *myResourceGroupLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-134">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="6c4dd-135">Creare un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="6c4dd-135">Create a load balancer</span></span>
<span data-ttu-id="6c4dd-136">Creare un servizio di bilanciamento del carico con [az network lb create](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="6c4dd-137">L'esempio seguente crea un servizio di bilanciamento del carico denominato *myLoadBalancer* e assegna l'indirizzo *myPublicIP* alla configurazione IP front-end:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-137">The following example creates a load balancer named *myLoadBalancer* and assigns the *myPublicIP* address to the front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="6c4dd-138">Creare un probe di integrità</span><span class="sxs-lookup"><span data-stu-id="6c4dd-138">Create a health probe</span></span>
<span data-ttu-id="6c4dd-139">Per consentire al servizio di bilanciamento del carico di monitorare lo stato dell'app, si usa un probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-139">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="6c4dd-140">Il probe di integrità aggiunge o rimuove in modo dinamico le VM nella rotazione del servizio di bilanciamento del carico in base alla rispettiva risposta ai controlli di integrità.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-140">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="6c4dd-141">Per impostazione predefinita, una VM viene rimossa dalla distribuzione del servizio di bilanciamento del carico dopo due errori consecutivi a intervalli di 15 secondi.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-141">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="6c4dd-142">Un probe di integrità viene creato in base a un protocollo o una specifica pagina di controllo integrità per l'app.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="6c4dd-143">Nell'esempio seguente viene creato un probe TCP.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-143">The following example creates a TCP probe.</span></span> <span data-ttu-id="6c4dd-144">È anche possibile creare probe HTTP personalizzati per i controlli di integrità con granularità fine.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="6c4dd-145">Quando si usa un probe HTTP personalizzato, è necessario creare la pagina di controllo integrità, ad esempio *healthcheck.js*.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-145">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="6c4dd-146">Il probe deve restituire la risposta **HTTP 200 OK** affinché il servizio di bilanciamento del carico mantenga l'host nella rotazione.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-146">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="6c4dd-147">Per creare un probe di integrità TCP, usare con [az network lb probe create](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-147">To create a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="6c4dd-148">L'esempio seguente crea un probe di integrità denominato *myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-148">The following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="6c4dd-149">Creare una regola di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="6c4dd-149">Create a load balancer rule</span></span>
<span data-ttu-id="6c4dd-150">Una regola di bilanciamento del carico consente di definire come il traffico verrà distribuito alle VM.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-150">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="6c4dd-151">Definire la configurazione IP front-end per il traffico in ingresso e il pool IP di back-end affinché riceva il traffico, insieme alla porta di origine e di destinazione necessaria.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-151">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="6c4dd-152">Per assicurarsi che solo le macchine virtuali integre ricevano il traffico, è necessario anche definire il probe di integrità da usare.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-152">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="6c4dd-153">Creare una regola di bilanciamento del carico con [az network lb rule create](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="6c4dd-154">L'esempio seguente crea una regola denominata *myLoadBalancerRule*, usa il probe di integrità *myHealthProbe* e bilancia il traffico sulla porta *80*:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-154">The following example creates a rule named *myLoadBalancerRule*, uses the *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a><span data-ttu-id="6c4dd-155">Configurare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="6c4dd-155">Configure virtual network</span></span>
<span data-ttu-id="6c4dd-156">Prima di distribuire alcune macchine virtuali e testare il servizio di bilanciamento, creare le risorse di rete virtuale di supporto.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-156">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="6c4dd-157">Per altre informazioni sulle reti virtuali, vedere l'esercitazione [Gestire le reti virtuali di Azure](tutorial-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-157">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="6c4dd-158">Creare risorse di rete</span><span class="sxs-lookup"><span data-stu-id="6c4dd-158">Create network resources</span></span>
<span data-ttu-id="6c4dd-159">Creare una rete virtuale con [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="6c4dd-160">L'esempio seguente crea una rete virtuale denominata *myVnet* con una subnet denominata *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-160">The following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="6c4dd-161">Per aggiungere un gruppo di sicurezza di rete usare [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-161">To add a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="6c4dd-162">L'esempio seguente crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-162">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="6c4dd-163">Creare una regola del gruppo di sicurezza di rete con [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="6c4dd-164">L'esempio seguente crea una regola del gruppo di sicurezza di rete denominata *myNetworkSecurityGroupRule*:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-164">The following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="6c4dd-165">Le schede di interfaccia di rete virtuale vengono create con [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="6c4dd-166">L'esempio seguente crea tre schede di interfaccia di rete virtuali,</span><span class="sxs-lookup"><span data-stu-id="6c4dd-166">The following example creates three virtual NICs.</span></span> <span data-ttu-id="6c4dd-167">Una scheda di interfaccia di rete virtuale per ogni VM creata per l'app nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-167">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="6c4dd-168">È possibile creare altre schede di interfaccia di rete virtuale e macchine virtuali in qualsiasi momento e aggiungerle al bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-168">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a><span data-ttu-id="6c4dd-169">Creare macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="6c4dd-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="6c4dd-170">Creare una configurazione cloud-init</span><span class="sxs-lookup"><span data-stu-id="6c4dd-170">Create cloud-init config</span></span>
<span data-ttu-id="6c4dd-171">In un'esercitazione precedente, [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) (Come personalizzare una macchina virtuale Linux al primo avvio), è stato descritto come personalizzare una macchina virtuale al primo avvio con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-171">In a previous tutorial on [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with cloud-init.</span></span> <span data-ttu-id="6c4dd-172">È possibile usare lo stesso file di configurazione cloud-init per installare NGINX ed eseguire una semplice app Node.js "Hello World".</span><span class="sxs-lookup"><span data-stu-id="6c4dd-172">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="6c4dd-173">Nella shell corrente creare un file denominato *cloud-init.txt* e incollare la configurazione seguente.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-173">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="6c4dd-174">Ad esempio, creare il file in Cloud Shell anziché nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-174">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="6c4dd-175">Immettere `sensible-editor cloud-init.txt` per creare il file e visualizzare un elenco degli editor disponibili.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-175">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="6c4dd-176">Assicurarsi che l'intero file cloud-init venga copiato correttamente, in particolare la prima riga:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-176">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a><span data-ttu-id="6c4dd-177">Creare macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="6c4dd-177">Create virtual machines</span></span>
<span data-ttu-id="6c4dd-178">Per aumentare la disponibilità elevata dell'app, posizionare le macchine virtuali in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-178">To improve the high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="6c4dd-179">Per altre informazioni sui set di disponibilità, vedere l'esercitazione precedente [Come creare macchine virtuali a disponibilità elevata](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-179">For more information about availability sets, see the previous [How to create highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="6c4dd-180">Creare un set di disponibilità con [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="6c4dd-181">L'esempio seguente crea un set di disponibilità denominato *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-181">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="6c4dd-182">Ora è possibile creare le VM con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-182">Now you can create the VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="6c4dd-183">L'esempio seguente crea tre VM e genera le chiavi SSH, se non sono già presenti:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-183">The following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

<span data-ttu-id="6c4dd-184">Sono presenti attività in background la cui esecuzione continua dopo che l'interfaccia della riga di comando di Azure è tornata al prompt.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-184">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="6c4dd-185">Il parametro `--no-wait` non attende il completamento di tutte le attività.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-185">The `--no-wait` parameter does not wait for all the tasks to complete.</span></span> <span data-ttu-id="6c4dd-186">Potrebbe trascorrere ancora qualche minuto prima che sia possibile accedere all'app.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-186">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="6c4dd-187">Il probe di integrità del servizio di bilanciamento del carico rileva quando l'app è in esecuzione in ogni VM.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-187">The load balancer health probe automatically detects when the app is running on each VM.</span></span> <span data-ttu-id="6c4dd-188">Quando l'app è in esecuzione, la regola di bilanciamento del carico inizia a distribuire il traffico.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-188">Once the app is running, the load balancer rule starts to distribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="6c4dd-189">Testare il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="6c4dd-189">Test load balancer</span></span>
<span data-ttu-id="6c4dd-190">Ottenere l'indirizzo IP pubblico del servizio di bilanciamento del carico con [az network public-ip show](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-190">Obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="6c4dd-191">L'esempio seguente ottiene l'indirizzo IP per *myPublicIP* creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-191">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="6c4dd-192">Sarà quindi possibile immettere l'indirizzo IP pubblico in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-192">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="6c4dd-193">Si ricordi che sono necessari alcuni minuti perché le macchine virtuali siano pronte e che il bilanciamento del carico inizi a distribuire traffico a queste.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-193">Remember - it takes a few minutes the the VMs to be ready before the load balancer starts to distribute traffic to them.</span></span> <span data-ttu-id="6c4dd-194">Verrà visualizzata l'app, con il nome host della macchina virtuale a cui il servizio di bilanciamento del carico ha distribuito il traffico, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-194">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Esecuzione dell'app Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="6c4dd-196">Per verificare la distribuzione del traffico tra tutte e tre le VM che eseguono l'app da parte del servizio di bilanciamento del carico, forzare l'aggiornamento del Web browser.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-196">To see the load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="6c4dd-197">aggiunta e rimozione di VM</span><span class="sxs-lookup"><span data-stu-id="6c4dd-197">Add and remove VMs</span></span>
<span data-ttu-id="6c4dd-198">Potrebbe essere necessario eseguire attività di manutenzione sulle VM che eseguono l'app, ad esempio per installare aggiornamenti del sistema operativo,</span><span class="sxs-lookup"><span data-stu-id="6c4dd-198">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="6c4dd-199">oppure aggiungere altre VM per gestire un aumento del traffico verso l'app.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-199">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="6c4dd-200">Questa sezione illustra come rimuovere o aggiungere una VM nel servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-200">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="6c4dd-201">Rimuovere una VM dal servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="6c4dd-201">Remove a VM from the load balancer</span></span>
<span data-ttu-id="6c4dd-202">È possibile rimuovere una VM dal pool di indirizzi back-end con [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-202">You can remove a VM from the backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="6c4dd-203">L'esempio seguente rimuove la scheda di interfaccia di rete virtuale per **myVM2** da *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-203">The following example removes the virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="6c4dd-204">Per verificare la distribuzione del traffico nelle due VM restanti che eseguono l'app da parte del servizio di bilanciamento del carico, forzare l'aggiornamento del Web browser.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-204">To see the load balancer distribute traffic across the remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="6c4dd-205">È ora possibile eseguire attività di manutenzione sulla VM, ad esempio installare aggiornamenti del sistema operativo o eseguire un riavvio della VM.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-205">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="6c4dd-206">Aggiungere una VM al servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="6c4dd-206">Add a VM to the load balancer</span></span>
<span data-ttu-id="6c4dd-207">Al termine della manutenzione di una VM o se è necessario espandere la capacità, è possibile aggiungere una VM al pool di indirizzi back-end con [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span><span class="sxs-lookup"><span data-stu-id="6c4dd-207">After performing VM maintenance, or if you need to expand capacity, you can add a VM to the backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="6c4dd-208">L'esempio seguente aggiunge la scheda di interfaccia di rete virtuale per **myVM2** a *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-208">The following example adds the virtual NIC for **myVM2** to *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="6c4dd-209">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c4dd-209">Next steps</span></span>
<span data-ttu-id="6c4dd-210">In questa esercitazione viene creato un bilanciamento del carico e vengono collegate le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-210">In this tutorial, you created a load balancer and attached VMs to it.</span></span> <span data-ttu-id="6c4dd-211">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="6c4dd-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6c4dd-212">Creare un servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="6c4dd-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="6c4dd-213">Creare un probe di integrità per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="6c4dd-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="6c4dd-214">Creare regole del traffico di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="6c4dd-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="6c4dd-215">Usare cloud-init per creare un'applicazione di base Node.js</span><span class="sxs-lookup"><span data-stu-id="6c4dd-215">Use cloud-init to create a basic Node.js app</span></span>
> * <span data-ttu-id="6c4dd-216">Creare macchine virtuali e collegarsi a un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="6c4dd-216">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="6c4dd-217">Visualizzare un bilanciamento del carico in azione</span><span class="sxs-lookup"><span data-stu-id="6c4dd-217">View a load balancer in action</span></span>
> * <span data-ttu-id="6c4dd-218">Aggiungere e rimuovere macchine virtuali da un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="6c4dd-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="6c4dd-219">Passare all'esercitazione successiva per altre informazioni sui componenti della rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c4dd-219">Advance to the next tutorial to learn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6c4dd-220">Gestire le VM e le reti virtuali</span><span class="sxs-lookup"><span data-stu-id="6c4dd-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
