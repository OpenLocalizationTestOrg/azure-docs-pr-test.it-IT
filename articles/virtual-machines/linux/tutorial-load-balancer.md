---
title: aaaHow tooload bilanciare macchine virtuali Linux in Azure | Documenti Microsoft
description: "Informazioni su come il carico bilanciamento toocreate un'applicazione a elevata disponibilità e sicura tra tre macchine virtuali Linux toouse hello Azure"
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
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="03625-103">Come tooload bilanciare macchine virtuali Linux in Azure toocreate applicazioni a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="03625-103">How tooload balance Linux virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="03625-104">Il bilanciamento del carico offre un livello più elevato di disponibilità distribuendo le richieste in ingresso tra più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="03625-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="03625-105">In questa esercitazione apprendere hello diversi componenti del servizio di bilanciamento del carico di Azure hello che distribuisce il traffico e garantire disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="03625-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="03625-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="03625-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="03625-107">Creare un servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="03625-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="03625-108">Creare un probe di integrità per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="03625-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="03625-109">Creare regole del traffico di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="03625-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="03625-110">Utilizzare cloud init toocreate un'app Node.js di base</span><span class="sxs-lookup"><span data-stu-id="03625-110">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="03625-111">Creare macchine virtuali e collegare bilanciamento del carico tooa</span><span class="sxs-lookup"><span data-stu-id="03625-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="03625-112">Visualizzare un bilanciamento del carico in azione</span><span class="sxs-lookup"><span data-stu-id="03625-112">View a load balancer in action</span></span>
> * <span data-ttu-id="03625-113">Aggiungere e rimuovere macchine virtuali da un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="03625-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="03625-114">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="03625-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="03625-115">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="03625-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="03625-116">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="03625-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="03625-117">Panoramica di Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="03625-117">Azure load balancer overview</span></span>
<span data-ttu-id="03625-118">Azure Load Balancer è un bilanciamento del carico di livello 4 (TCP, UDP) che offre disponibilità elevata mediante la distribuzione del traffico in ingresso nelle macchine virtuali integre.</span><span class="sxs-lookup"><span data-stu-id="03625-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="03625-119">Un probe di integrità di bilanciamento del carico consente di monitorare una determinata porta in ogni macchina virtuale e vengono distribuiti solo il traffico tooan operativo VM.</span><span class="sxs-lookup"><span data-stu-id="03625-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="03625-120">Definire una configurazione IP front-end che contenga uno o più indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="03625-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="03625-121">Questa configurazione IP front-end consente il toobe di applicazioni e del servizio di bilanciamento del carico accessibile tramite Internet hello.</span><span class="sxs-lookup"><span data-stu-id="03625-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="03625-122">Le macchine virtuali connesse tooa bilanciamento del carico utilizzando la scheda di interfaccia di rete virtuale (NIC).</span><span class="sxs-lookup"><span data-stu-id="03625-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="03625-123">toodistribute traffico toohello macchine virtuali, un pool di indirizzi back-end contiene indirizzi IP hello di hello virtuale (NIC) connesse toohello bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="03625-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="03625-124">flusso di hello toocontrol del traffico, definire regole di bilanciamento del carico per porte specifiche e protocolli che eseguono il mapping delle macchine virtuali tooyour.</span><span class="sxs-lookup"><span data-stu-id="03625-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>

<span data-ttu-id="03625-125">Se è stato eseguito troppo esercitazione precedente hello[creare un set di scalabilità della macchina virtuale](tutorial-create-vmss.md), è stato creato un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="03625-125">If you followed hello previous tutorial too[create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="03625-126">Tutti questi componenti sono stati configurati per l'utente come parte del set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="03625-126">All these components were configured for you as part of hello scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="03625-127">Creare un Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="03625-127">Create Azure load balancer</span></span>
<span data-ttu-id="03625-128">Questa sezione descrive come è possibile creare e configurare ciascun componente del servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="03625-128">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="03625-129">Per poter creare un servizio di bilanciamento del carico, è prima necessario creare un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="03625-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="03625-130">esempio Hello crea un gruppo di risorse denominato *myResourceGroupLoadBalancer* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="03625-130">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="03625-131">Creare un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="03625-131">Create a public IP address</span></span>
<span data-ttu-id="03625-132">tooaccess l'app in hello Internet, è necessario un indirizzo IP pubblico di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="03625-132">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="03625-133">Creare un indirizzo IP pubblico con [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="03625-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="03625-134">esempio Hello crea un indirizzo IP pubblico denominato *myPublicIP* in hello *myResourceGroupLoadBalancer* gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="03625-134">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="03625-135">Creare un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="03625-135">Create a load balancer</span></span>
<span data-ttu-id="03625-136">Creare un servizio di bilanciamento del carico con [az network lb create](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="03625-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="03625-137">esempio Hello crea un bilanciamento del carico denominato *myLoadBalancer* e assegna hello *myPublicIP* configurazione IP front-end dell'indirizzo toohello:</span><span class="sxs-lookup"><span data-stu-id="03625-137">hello following example creates a load balancer named *myLoadBalancer* and assigns hello *myPublicIP* address toohello front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="03625-138">Creare un probe di integrità</span><span class="sxs-lookup"><span data-stu-id="03625-138">Create a health probe</span></span>
<span data-ttu-id="03625-139">tooallow hello bilanciamento toomonitor hello stato di caricamento dell'app, utilizzare un probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="03625-139">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="03625-140">probe di integrità Hello dinamicamente aggiunge o rimuove le macchine virtuali dalla rotazione di bilanciamento del carico hello in base alle loro controlli toohealth di risposta.</span><span class="sxs-lookup"><span data-stu-id="03625-140">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="03625-141">Per impostazione predefinita, una macchina virtuale viene rimosso dalla distribuzione del servizio di bilanciamento del carico hello dopo due tentativi consecutivi non riusciti a intervalli di 15 secondi.</span><span class="sxs-lookup"><span data-stu-id="03625-141">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="03625-142">Un probe di integrità viene creato in base a un protocollo o una specifica pagina di controllo integrità per l'app.</span><span class="sxs-lookup"><span data-stu-id="03625-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="03625-143">Hello di esempio seguente crea un probe TCP.</span><span class="sxs-lookup"><span data-stu-id="03625-143">hello following example creates a TCP probe.</span></span> <span data-ttu-id="03625-144">È anche possibile creare probe HTTP personalizzati per i controlli di integrità con granularità fine.</span><span class="sxs-lookup"><span data-stu-id="03625-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="03625-145">Quando si utilizza un probe HTTP personalizzato, è necessario creare pagina di controllo di integrità hello, ad esempio *healthcheck.js*.</span><span class="sxs-lookup"><span data-stu-id="03625-145">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="03625-146">probe Hello deve restituire un **HTTP 200 OK** risposta per l'host hello carico bilanciamento tookeep hello nella rotazione.</span><span class="sxs-lookup"><span data-stu-id="03625-146">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="03625-147">toocreate un probe di integrità TCP, utilizzare [az di rete lb probe creare](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="03625-147">toocreate a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="03625-148">esempio Hello crea un probe di integrità denominato *myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="03625-148">hello following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="03625-149">Creare una regola di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="03625-149">Create a load balancer rule</span></span>
<span data-ttu-id="03625-150">Una regola di bilanciamento del carico è toodefine utilizzato come il traffico è toohello distribuita le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="03625-150">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="03625-151">Definire una configurazione IP front-end di hello per il traffico in ingresso hello e hello back-end pool tooreceive hello traffico IP, con origine necessari hello e porta di destinazione.</span><span class="sxs-lookup"><span data-stu-id="03625-151">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="03625-152">toomake che solo le macchine virtuali integro ricevano il traffico, è inoltre definire toouse probe di integrità hello.</span><span class="sxs-lookup"><span data-stu-id="03625-152">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="03625-153">Creare una regola di bilanciamento del carico con [az network lb rule create](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="03625-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="03625-154">esempio Hello crea una regola denominata *myLoadBalancerRule*, hello utilizza *myHealthProbe* probe di integrità e bilancia il traffico sulla porta *80*:</span><span class="sxs-lookup"><span data-stu-id="03625-154">hello following example creates a rule named *myLoadBalancerRule*, uses hello *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

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


## <a name="configure-virtual-network"></a><span data-ttu-id="03625-155">Configurare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="03625-155">Configure virtual network</span></span>
<span data-ttu-id="03625-156">Prima di distribuire alcune macchine virtuali e possibile eseguire il servizio di bilanciamento del test, creare hello che supporta le risorse di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="03625-156">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="03625-157">Per ulteriori informazioni sulle reti virtuali, vedere hello [gestire reti virtuali di Azure](tutorial-virtual-network.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="03625-157">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="03625-158">Creare risorse di rete</span><span class="sxs-lookup"><span data-stu-id="03625-158">Create network resources</span></span>
<span data-ttu-id="03625-159">Creare una rete virtuale con [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="03625-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="03625-160">esempio Hello crea una rete virtuale denominata *myVnet* con una subnet denominata *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="03625-160">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="03625-161">tooadd un gruppo di sicurezza di rete, utilizzare [rete az creare](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="03625-161">tooadd a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="03625-162">esempio Hello crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="03625-162">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="03625-163">Creare una regola del gruppo di sicurezza di rete con [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="03625-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="03625-164">esempio Hello crea una regola di gruppo di sicurezza di rete denominata *myNetworkSecurityGroupRule*:</span><span class="sxs-lookup"><span data-stu-id="03625-164">hello following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="03625-165">Le schede di interfaccia di rete virtuale vengono create con [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="03625-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="03625-166">Hello esempio crea tre schede di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="03625-166">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="03625-167">(Una scheda di rete virtuale per ogni macchina virtuale viene creato per l'app in hello seguendo i passaggi).</span><span class="sxs-lookup"><span data-stu-id="03625-167">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="03625-168">È possibile creare macchine virtuali e schede di rete virtuali aggiuntive in qualsiasi momento e aggiungerli toohello servizio di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="03625-168">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="03625-169">Creare macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="03625-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="03625-170">Creare una configurazione cloud-init</span><span class="sxs-lookup"><span data-stu-id="03625-170">Create cloud-init config</span></span>
<span data-ttu-id="03625-171">Nell'esercitazione precedente su [come toocustomize una macchina virtuale Linux al primo avvio](tutorial-automate-vm-deployment.md), si è appreso tooautomate personalizzazione con cloud init.</span><span class="sxs-lookup"><span data-stu-id="03625-171">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="03625-172">È possibile utilizzare hello stesso tooinstall file di configurazione cloud init NGINX ed eseguire una semplice app Node.js 'Hello World'.</span><span class="sxs-lookup"><span data-stu-id="03625-172">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="03625-173">Nella shell corrente, creare un file denominato *cloud init.txt* e Incolla hello seguente configurazione.</span><span class="sxs-lookup"><span data-stu-id="03625-173">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="03625-174">Ad esempio, creare file hello in hello Shell Cloud non presenti nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="03625-174">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="03625-175">Immettere `sensible-editor cloud-init.txt` toocreate hello file e visualizzare un elenco degli editor disponibili.</span><span class="sxs-lookup"><span data-stu-id="03625-175">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="03625-176">Assicurarsi che tale file intero cloud-init hello viene copiato correttamente, soprattutto hello prima riga:</span><span class="sxs-lookup"><span data-stu-id="03625-176">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

### <a name="create-virtual-machines"></a><span data-ttu-id="03625-177">Creare macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="03625-177">Create virtual machines</span></span>
<span data-ttu-id="03625-178">disponibilità elevata di hello tooimprove dell'app, posizionare le macchine virtuali in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="03625-178">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="03625-179">Per ulteriori informazioni sui set di disponibilità, vedere hello precedente [come macchine virtuali a disponibilità elevata toocreate](tutorial-availability-sets.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="03625-179">For more information about availability sets, see hello previous [How toocreate highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="03625-180">Creare un set di disponibilità con [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="03625-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="03625-181">esempio Hello crea un set denominato di disponibilità *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="03625-181">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="03625-182">Ora è possibile creare le macchine virtuali hello con [creare vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="03625-182">Now you can create hello VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="03625-183">Hello esempio crea tre macchine virtuali e genera le chiavi SSH se non esiste già:</span><span class="sxs-lookup"><span data-stu-id="03625-183">hello following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

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

<span data-ttu-id="03625-184">Sono presenti attività in background che continuare toorun dopo hello CLI di Azure restituisce toohello prompt.</span><span class="sxs-lookup"><span data-stu-id="03625-184">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="03625-185">Hello `--no-wait` parametro non attendere tutti hello toocomplete di attività.</span><span class="sxs-lookup"><span data-stu-id="03625-185">hello `--no-wait` parameter does not wait for all hello tasks toocomplete.</span></span> <span data-ttu-id="03625-186">Potrebbe essere un altro paio di minuti prima di poter accedere app hello.</span><span class="sxs-lookup"><span data-stu-id="03625-186">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="03625-187">Hello probe di integrità di bilanciamento del carico rileva automaticamente quando l'applicazione hello è in esecuzione in ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="03625-187">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="03625-188">Dopo l'applicazione hello è in esecuzione, regola di bilanciamento del carico hello avvia toodistribute traffico.</span><span class="sxs-lookup"><span data-stu-id="03625-188">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="03625-189">Testare il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="03625-189">Test load balancer</span></span>
<span data-ttu-id="03625-190">Ottenere l'indirizzo IP pubblico di hello del servizio di bilanciamento del carico con [Mostra public-ip di rete az](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="03625-190">Obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="03625-191">esempio Hello Ottiene hello di indirizzo IP per *myPublicIP* creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="03625-191">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="03625-192">È quindi possibile immettere l'indirizzo IP pubblico hello nel browser web tooa.</span><span class="sxs-lookup"><span data-stu-id="03625-192">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="03625-193">Nota: impiegato pochi minuti hello hello macchine virtuali toobe pronto prima dell'avvio di servizio di bilanciamento del carico hello toodistribute traffico toothem.</span><span class="sxs-lookup"><span data-stu-id="03625-193">Remember - it takes a few minutes hello hello VMs toobe ready before hello load balancer starts toodistribute traffic toothem.</span></span> <span data-ttu-id="03625-194">Hello app viene visualizzata, inclusi hello nome host della macchina virtuale hello tale bilanciamento del carico hello distribuite tooas traffico nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="03625-194">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Esecuzione dell'app Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="03625-196">servizio di bilanciamento del carico hello toosee distribuire il traffico tra tutte le tre macchine virtuali in esecuzione l'app, è possibile forza aggiornamento web browser.</span><span class="sxs-lookup"><span data-stu-id="03625-196">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="03625-197">aggiunta e rimozione di VM</span><span class="sxs-lookup"><span data-stu-id="03625-197">Add and remove VMs</span></span>
<span data-ttu-id="03625-198">È possibile la manutenzione tooperform hello macchine virtuali in esecuzione l'app, ad esempio l'installazione di aggiornamenti del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="03625-198">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="03625-199">toodeal con un aumento del traffico tooyour app, potrebbe essere necessario tooadd altre macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="03625-199">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="03625-200">In questa sezione illustra come tooremove o aggiungere una macchina virtuale dal servizio di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="03625-200">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="03625-201">Rimuovere una macchina virtuale dal servizio di bilanciamento del carico hello</span><span class="sxs-lookup"><span data-stu-id="03625-201">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="03625-202">È possibile rimuovere una macchina virtuale dal pool di indirizzi back-end hello con [az nic ip-config-pool di indirizzi rete rimuovere](/cli/azure/network/nic/ip-config/address-pool#remove).</span><span class="sxs-lookup"><span data-stu-id="03625-202">You can remove a VM from hello backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="03625-203">Hello seguente rimuove esempio hello schede di rete virtuale per **myVM2** da *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="03625-203">hello following example removes hello virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="03625-204">servizio di bilanciamento del carico hello toosee distribuire il traffico tra hello altre due macchine virtuali in esecuzione l'app è possibile forza aggiornamento web browser.</span><span class="sxs-lookup"><span data-stu-id="03625-204">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="03625-205">È ora possibile eseguire la manutenzione in hello macchina virtuale, ad esempio l'installazione degli aggiornamenti del sistema operativo o l'esecuzione di un riavvio della VM.</span><span class="sxs-lookup"><span data-stu-id="03625-205">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="03625-206">Aggiungere un bilanciamento del carico VM toohello</span><span class="sxs-lookup"><span data-stu-id="03625-206">Add a VM toohello load balancer</span></span>
<span data-ttu-id="03625-207">Dopo l'esecuzione della manutenzione di macchina virtuale, o se è necessario tooexpand capacità, è possibile aggiungere un pool di indirizzi back-end VM toohello con [az rete nic ip-config-pool di indirizzi di Aggiungi](/cli/azure/network/nic/ip-config/address-pool#add).</span><span class="sxs-lookup"><span data-stu-id="03625-207">After performing VM maintenance, or if you need tooexpand capacity, you can add a VM toohello backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="03625-208">esempio Hello aggiunge hello schede di rete virtuale per **myVM2** troppo*myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="03625-208">hello following example adds hello virtual NIC for **myVM2** too*myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="03625-209">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="03625-209">Next steps</span></span>
<span data-ttu-id="03625-210">In questa esercitazione è creato un servizio di bilanciamento del carico e collegato tooit macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="03625-210">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="03625-211">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="03625-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="03625-212">Creare un servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="03625-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="03625-213">Creare un probe di integrità per il servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="03625-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="03625-214">Creare regole del traffico di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="03625-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="03625-215">Utilizzare cloud init toocreate un'app Node.js di base</span><span class="sxs-lookup"><span data-stu-id="03625-215">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="03625-216">Creare macchine virtuali e collegare bilanciamento del carico tooa</span><span class="sxs-lookup"><span data-stu-id="03625-216">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="03625-217">Visualizzare un bilanciamento del carico in azione</span><span class="sxs-lookup"><span data-stu-id="03625-217">View a load balancer in action</span></span>
> * <span data-ttu-id="03625-218">Aggiungere e rimuovere macchine virtuali da un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="03625-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="03625-219">Spostare toolearn esercitazione successiva toohello ulteriori dettagli sui componenti di rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="03625-219">Advance toohello next tutorial toolearn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="03625-220">Gestire le VM e le reti virtuali</span><span class="sxs-lookup"><span data-stu-id="03625-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
