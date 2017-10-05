---
title: Usare il DNS interno per la risoluzione dei nomi di VM con l'interfaccia della riga di comando di Azure 2.0 | Documentazione Microsoft
description: Come creare schede di interfaccia di rete virtuale e usare DNS interni per la risoluzione dei nomi di VM in Azure con l'interfaccia della riga di comando di Azure 2.0
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: 992920adb1ae3736d43cc5f0bbb2081a20a1674d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="3d936-103">Creare schede di interfaccia di rete virtuale e usare DNS interni per la risoluzione dei nomi di VM in Azure</span><span class="sxs-lookup"><span data-stu-id="3d936-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="3d936-104">Questo articolo illustra come impostare nomi DNS interni statici per VM Linux usando schede di interfaccia di rete virtuale (vNic) e nomi di etichette DNS con l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="3d936-104">This article shows you how to set static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with the Azure CLI 2.0.</span></span> <span data-ttu-id="3d936-105">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d936-105">You can also perform these steps with the [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="3d936-106">Si ricorre ai nomi DNS statici per i servizi di infrastruttura permanenti, ad esempio per un server di compilazione Jenkins, usato per questo documento, o un server Git.</span><span class="sxs-lookup"><span data-stu-id="3d936-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="3d936-107">I requisiti sono:</span><span class="sxs-lookup"><span data-stu-id="3d936-107">The requirements are:</span></span>

* [<span data-ttu-id="3d936-108">Un account di Azure</span><span class="sxs-lookup"><span data-stu-id="3d936-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="3d936-109">File di chiavi SSH pubbliche e private</span><span class="sxs-lookup"><span data-stu-id="3d936-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="3d936-110">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="3d936-110">Quick commands</span></span>
<span data-ttu-id="3d936-111">Se si vuole eseguire rapidamente l'attività, la sezione seguente indica dettagliatamente i comandi necessari.</span><span class="sxs-lookup"><span data-stu-id="3d936-111">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="3d936-112">Altre informazioni dettagliate e il contesto per ogni passaggio sono disponibili nelle sezioni successive del documento, a partire da [qui](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="3d936-112">More detailed information and context for each step can be found in the rest of the document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="3d936-113">Per eseguire questi passaggi è necessario aver installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e aver effettuato l'accesso a un account Azure con il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="3d936-113">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="3d936-114">Pre-requisiti: gruppo di risorse, rete virtuale e subnet, gruppo di sicurezza di rete con SSH in ingresso.</span><span class="sxs-lookup"><span data-stu-id="3d936-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="3d936-115">Creare una scheda di interfaccia di rete virtuale con un nome DNS interno statico</span><span class="sxs-lookup"><span data-stu-id="3d936-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="3d936-116">Creare la vNic con il comando [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="3d936-116">Create the vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="3d936-117">Il flag `--internal-dns-name` dell'interfaccia della riga di comando consente di impostare l'etichetta DNS, che indica il nome DNS statico per la scheda di interfaccia di rete virtuale (vNic).</span><span class="sxs-lookup"><span data-stu-id="3d936-117">The `--internal-dns-name` CLI flag is for setting the DNS label, which provides the static DNS name for the virtual network interface card (vNic).</span></span> <span data-ttu-id="3d936-118">L'esempio seguente crea una scheda di rete virtuale denominata `myNic`, la connette alla rete virtuale `myVnet` e crea un record di nome DNS interno denominato `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="3d936-118">The following example creates a vNic named `myNic`, connects it to the `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-the-vnic"></a><span data-ttu-id="3d936-119">Distribuire una VM e connettere la scheda di interfaccia di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="3d936-119">Deploy a VM and connect the vNic</span></span>
<span data-ttu-id="3d936-120">Creare una VM con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="3d936-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="3d936-121">Il flag `--nics` consente di connette la scheda di interfaccia di rete virtuale alla VM durante la distribuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="3d936-121">The `--nics` flag connects the vNic to the VM during the deployment to Azure.</span></span> <span data-ttu-id="3d936-122">L'esempio seguente crea una VM `myVM` con Managed Disks di Azure e collega la scheda di interfaccia di rete virtuale denominata `myNic` ottenuta dal passaggio precedente:</span><span class="sxs-lookup"><span data-stu-id="3d936-122">The following example creates a VM named `myVM` with Azure Managed Disks and attaches the vNic named `myNic` from the preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="3d936-123">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="3d936-123">Detailed walkthrough</span></span>

<span data-ttu-id="3d936-124">In Azure, un'infrastruttura interamente basata sul modello CiCd (Continuous Integration and Continuous Deployment) richiede la disponibilità di server statici o di lunga durata.</span><span class="sxs-lookup"><span data-stu-id="3d936-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers to be static or long-lived servers.</span></span> <span data-ttu-id="3d936-125">È consigliabile che gli asset di Azure, come le reti virtuali e i gruppi di sicurezza di rete, siano risorse statiche, ovvero di lunga durata e distribuite raramente.</span><span class="sxs-lookup"><span data-stu-id="3d936-125">It is recommended that Azure assets like the virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="3d936-126">Dopo essere stata distribuita, una rete virtuale può essere usata in nuove distribuzioni senza alcun effetto negativo sull'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="3d936-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="3d936-127">È possibile aggiungere in seguito un server repository Git e un server di automazione Jenkins, è possibile distribuire un modello CiCd in questa rete virtuale per un ambiente di test o di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="3d936-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd to this virtual network for your development or test environments.</span></span>  

<span data-ttu-id="3d936-128">I nomi DNS interni sono risolvibili solo all'interno di una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3d936-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="3d936-129">Trattandosi di nomi interni, non sono risolvibili esternamente in Internet e garantiscono quindi una sicurezza aggiuntiva per l'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="3d936-129">Because the DNS names are internal, they are not resolvable to the outside internet, providing additional security to the infrastructure.</span></span>

<span data-ttu-id="3d936-130">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="3d936-130">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="3d936-131">I nomi dei parametri di esempio includono `myResourceGroup`, `myNic` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="3d936-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="3d936-132">Creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="3d936-132">Create the resource group</span></span>
<span data-ttu-id="3d936-133">Creare prima il gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="3d936-133">First, create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="3d936-134">Nell'esempio seguente viene creato un gruppo di risorse denominato `myResourceGroup` nella località `westus`:</span><span class="sxs-lookup"><span data-stu-id="3d936-134">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-the-virtual-network"></a><span data-ttu-id="3d936-135">Creare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="3d936-135">Create the virtual network</span></span>

<span data-ttu-id="3d936-136">Il passaggio successivo è creare una rete virtuale in cui avviare le VM.</span><span class="sxs-lookup"><span data-stu-id="3d936-136">The next step is to build a virtual network to launch the VMs into.</span></span> <span data-ttu-id="3d936-137">Ai fini di questa procedura, la rete virtuale contiene una subnet.</span><span class="sxs-lookup"><span data-stu-id="3d936-137">The virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="3d936-138">Per altre informazioni sulle reti virtuali in Azure, vedere [Creare una rete virtuale usando l'interfaccia della riga di comando di Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d936-138">For more information on Azure virtual networks, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="3d936-139">Creare la rete virtuale con [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="3d936-139">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="3d936-140">L'esempio seguente creata una rete virtuale denominata `myVnet` e una sottorete denominata `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="3d936-140">The following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="3d936-141">Creare il gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="3d936-141">Create the Network Security Group</span></span>
<span data-ttu-id="3d936-142">I gruppi di sicurezza di rete di Azure sono analoghi a un firewall a livello di rete.</span><span class="sxs-lookup"><span data-stu-id="3d936-142">Azure Network Security Groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="3d936-143">Per altre informazioni sui gruppi di sicurezza di rete, vedere [Come creare gruppi di sicurezza di rete nell'interfaccia della riga di comando di Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d936-143">For more information about Network Security Groups, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="3d936-144">Creare il gruppo di sicurezza di rete con [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="3d936-144">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="3d936-145">Nell'esempio seguente viene creato un gruppo di sicurezza di rete denominato `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="3d936-145">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-to-allow-ssh"></a><span data-ttu-id="3d936-146">Aggiungere una regola in entrata per consentire SSH</span><span class="sxs-lookup"><span data-stu-id="3d936-146">Add an inbound rule to allow SSH</span></span>
<span data-ttu-id="3d936-147">Aggiungere una regole in ingresso per il gruppo di sicurezza di rete con [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="3d936-147">Add an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="3d936-148">Nell'esempio seguente viene creata una regola denominata `myRuleAllowSSH`:</span><span class="sxs-lookup"><span data-stu-id="3d936-148">The following example creates a rule named `myRuleAllowSSH`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-the-subnet-with-the-network-security-group"></a><span data-ttu-id="3d936-149">Associare la subnet con il gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="3d936-149">Associate the subnet with the Network Security Group</span></span>
<span data-ttu-id="3d936-150">Per associare la subnet con il gruppo di sicurezza di rete usare [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="3d936-150">To associate the subnet with the Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="3d936-151">L'esempio seguente associa il nome di subnet `mySubnet` al gruppo di sicurezza di rete `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="3d936-151">The following example associates the subnet name `mySubnet` with the Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-the-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="3d936-152">Creare la scheda di interfaccia di rete virtuale e i nomi DNS statici</span><span class="sxs-lookup"><span data-stu-id="3d936-152">Create the virtual network interface card and static DNS names</span></span>
<span data-ttu-id="3d936-153">Sebbene Azure sia molto flessibile, per poter usare nomi DNS per la risoluzione dei nomi di VM è necessario creare schede di interfaccia di rete virtuale (vNic) che includano un'etichetta DNS.</span><span class="sxs-lookup"><span data-stu-id="3d936-153">Azure is very flexible, but to use DNS names for VM name resolution, you need to create virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="3d936-154">Le schede di interfaccia di rete virtuale sono importanti in quanto è possibile riutilizzarle connettendole a VM differenti nel ciclo di vita dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="3d936-154">vNics are important as you can reuse them by connecting them to different VMs over the infrastructure lifecycle.</span></span> <span data-ttu-id="3d936-155">In questo modo la scheda di interfaccia di rete virtuale diventa una risorsa statica, mentre le VM possono essere temporanee.</span><span class="sxs-lookup"><span data-stu-id="3d936-155">This approach keeps the vNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="3d936-156">Applicando l'etichettatura DNS a una scheda di interfaccia di rete virtuale, è possibile abilitare nella rete virtuale la risoluzione di nomi semplici provenienti da altre VM.</span><span class="sxs-lookup"><span data-stu-id="3d936-156">By using DNS labeling on the vNic, we are able to enable simple name resolution from other VMs in the VNet.</span></span> <span data-ttu-id="3d936-157">L'uso di nomi risolvibili consente anche ad altre macchine virtuali di accedere al server di automazione in base al nome DNS `Jenkins` o al server Git come `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="3d936-157">Using resolvable names enables other VMs to access the automation server by the DNS name `Jenkins` or the Git server as `gitrepo`.</span></span>  

<span data-ttu-id="3d936-158">Creare la vNic con il comando [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="3d936-158">Create the vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="3d936-159">L'esempio seguente crea una scheda di rete virtuale denominata `myNic`, la connette alla rete virtuale `myVnet` denominata `myVnet` e crea un record di nome DNS interno denominato `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="3d936-159">The following example creates a vNic named `myNic`, connects it to the `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="3d936-160">Distribuire la macchina virtuale nell'infrastruttura di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="3d936-160">Deploy the VM into the virtual network infrastructure</span></span>
<span data-ttu-id="3d936-161">A questo punto sono disponibili una rete virtuale e subnet, un gruppo di sicurezza di rete che funge da firewall per proteggere la subnet bloccando tutto il traffico in ingresso tranne quello verso la porta 22 per SSH e una scheda di interfaccia di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d936-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="3d936-162">Ora è possibile distribuire una VM all'interno di questa infrastruttura di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="3d936-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="3d936-163">Creare una VM con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="3d936-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="3d936-164">L'esempio seguente crea una VM `myVM` con Managed Disks di Azure e collega la scheda di interfaccia di rete virtuale denominata `myNic` ottenuta dal passaggio precedente:</span><span class="sxs-lookup"><span data-stu-id="3d936-164">The following example creates a VM named `myVM` with Azure Managed Disks and attaches the vNic named `myNic` from the preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="3d936-165">Usando i flag dell'interfaccia della riga di comando per chiamare le risorse esistenti, si indica ad Azure di distribuire la macchina virtuale all'interno della rete esistente.</span><span class="sxs-lookup"><span data-stu-id="3d936-165">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="3d936-166">Come già detto, dopo essere state distribuite la rete virtuale e la subnet possono essere usate come risorse statiche o permanenti nell'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="3d936-166">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="3d936-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3d936-167">Next steps</span></span>
* [<span data-ttu-id="3d936-168">Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="3d936-168">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="3d936-169">Creare una VM Linux in Azure usando i modelli</span><span class="sxs-lookup"><span data-stu-id="3d936-169">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
