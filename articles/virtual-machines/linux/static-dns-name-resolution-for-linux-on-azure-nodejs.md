---
title: Uso del DNS interno per la risoluzione dei nomi di macchine virtuali in Azure | Documentazione Microsoft
description: Uso del DNS interno per la risoluzione dei nomi di macchine virtuali in Azure.
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
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: bfba2cf38a0624e8480a32bf153f391d820da5a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="1199d-103">Uso del DNS interno per la risoluzione dei nomi di macchine virtuali in Azure</span><span class="sxs-lookup"><span data-stu-id="1199d-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="1199d-104">Questo articolo illustra come impostare nomi DNS interni statici per macchine virtuali Linux usando schede di interfaccia di rete virtuale (VNic) e nomi di etichette DNS.</span><span class="sxs-lookup"><span data-stu-id="1199d-104">This article shows how to set static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="1199d-105">Si ricorre ai nomi DNS statici per i servizi di infrastruttura permanenti, ad esempio per un server di compilazione Jenkins, usato per questo documento, o un server Git.</span><span class="sxs-lookup"><span data-stu-id="1199d-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="1199d-106">I requisiti sono:</span><span class="sxs-lookup"><span data-stu-id="1199d-106">The requirements are:</span></span>

* [<span data-ttu-id="1199d-107">Un account di Azure</span><span class="sxs-lookup"><span data-stu-id="1199d-107">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="1199d-108">File di chiavi SSH pubbliche e private</span><span class="sxs-lookup"><span data-stu-id="1199d-108">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="1199d-109">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="1199d-109">CLI versions to complete the task</span></span>
<span data-ttu-id="1199d-110">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="1199d-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="1199d-111">[Interfaccia della riga di comando di Azure 1.0](#quick-commands): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="1199d-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="1199d-112">[Interfaccia della riga di comando di Azure 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="1199d-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="1199d-113">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="1199d-113">Quick commands</span></span>

<span data-ttu-id="1199d-114">Se si vuole eseguire rapidamente l'attività, la sezione seguente indica dettagliatamente i comandi necessari.</span><span class="sxs-lookup"><span data-stu-id="1199d-114">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="1199d-115">Altre informazioni dettagliate e il contesto per ogni passaggio sono disponibili nelle sezioni successive del documento, [a partire da qui](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="1199d-115">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="1199d-116">Prerequisiti: gruppo di risorse, rete virtuale, gruppo di sicurezza di rete con SSH in ingresso, subnet.</span><span class="sxs-lookup"><span data-stu-id="1199d-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="1199d-117">Creare una scheda di interfaccia di rete virtuale con un nome DNS interno statico</span><span class="sxs-lookup"><span data-stu-id="1199d-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="1199d-118">Il flag dell'interfaccia della riga di comando `-r` consente di impostare l'etichetta DNS, che indica il nome DNS statico per la scheda di interfaccia di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1199d-118">The `-r` cli flag is for setting the DNS label, which provides the static DNS name for the VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-the-vm-into-the-vnet-nsg-and-connect-the-vnic"></a><span data-ttu-id="1199d-119">Distribuire la macchina virtuale nella rete virtuale, associare il gruppo di sicurezza di rete e connettere la scheda di interfaccia di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="1199d-119">Deploy the VM into the VNet, NSG and, connect the VNic</span></span>

<span data-ttu-id="1199d-120">Il flag `-N` consente di connette la scheda di interfaccia virtuale alla macchina virtuale durante la distribuzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1199d-120">The `-N` connects the VNic to the new VM during the deployment to Azure.</span></span>

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="1199d-121">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="1199d-121">Detailed walkthrough</span></span>

<span data-ttu-id="1199d-122">In Azure, un'infrastruttura interamente basata sul modello CiCd (Continuous Integration and Continuous Deployment) richiede la disponibilità di server statici o di lunga durata.</span><span class="sxs-lookup"><span data-stu-id="1199d-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers to be static or long-lived servers.</span></span>  <span data-ttu-id="1199d-123">È consigliabile che gli asset di Azure, come le reti virtuali e i gruppi di sicurezza di rete, siano risorse statiche, ovvero di lunga durata e distribuite raramente.</span><span class="sxs-lookup"><span data-stu-id="1199d-123">It is recommended that Azure assets like the Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="1199d-124">Dopo essere stata distribuita, una rete virtuale può essere usata in nuove distribuzioni senza alcun effetto negativo sull'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="1199d-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span>  <span data-ttu-id="1199d-125">Aggiungendo a questa rete statica un server repository Git e un server di automazione Jenkins, è possibile distribuire un modello CiCd in un ambiente di test o di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="1199d-125">Adding to this static network a Git repository server and a Jenkins automation server delivers CiCd to your development or test environments.</span></span>  

<span data-ttu-id="1199d-126">I nomi DNS interni sono risolvibili solo all'interno di una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1199d-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="1199d-127">Trattandosi di nomi interni, non sono risolvibili esternamente in Internet e garantiscono quindi una sicurezza aggiuntiva per l'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="1199d-127">Because the DNS names are internal, they are not resolvable to the outside internet, providing additional security to the infrastructure.</span></span>

<span data-ttu-id="1199d-128">_Sostituire i nomi nell'esempio con nomi personalizzati._</span><span class="sxs-lookup"><span data-stu-id="1199d-128">_Replace any examples with your own naming._</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="1199d-129">Creare il gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="1199d-129">Create the Resource group</span></span>

<span data-ttu-id="1199d-130">Per organizzare tutti gli elementi creati in questa procedura dettagliata è necessario un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1199d-130">A Resource Group is needed to organize everything we create in this walkthrough.</span></span>  <span data-ttu-id="1199d-131">Per altre informazioni sui gruppi di risorse di Azure, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1199d-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-the-vnet"></a><span data-ttu-id="1199d-132">Creare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="1199d-132">Create the VNet</span></span>

<span data-ttu-id="1199d-133">Il primo passaggio consiste nella compilazione di una rete virtuale nella quale eseguire le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1199d-133">The first step is to build a VNet to launch the VMs into.</span></span>  <span data-ttu-id="1199d-134">Ai fini di questa procedura, la rete virtuale contiene una subnet.</span><span class="sxs-lookup"><span data-stu-id="1199d-134">The VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="1199d-135">Per altre informazioni sulle reti virtuali di Azure, vedere [Creare una rete virtuale (classica) usando l'interfaccia della riga di comando di Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1199d-135">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-the-nsg"></a><span data-ttu-id="1199d-136">Creare il gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="1199d-136">Create the NSG</span></span>

<span data-ttu-id="1199d-137">La subnet è protetta da un gruppo di sicurezza di rete esistente che viene creato prima della subnet.</span><span class="sxs-lookup"><span data-stu-id="1199d-137">The Subnet is built behind an existing Network Security Group so we build the NSG before the Subnet.</span></span>  <span data-ttu-id="1199d-138">I gruppi di sicurezza di rete di Azure sono analoghi ai firewall a livello di rete.</span><span class="sxs-lookup"><span data-stu-id="1199d-138">Azure NSGs are equivalent to a firewall at the network layer.</span></span>  <span data-ttu-id="1199d-139">Per altre informazioni sui gruppi di sicurezza di Azure, vedere [Come creare gruppi di sicurezza di rete nell'interfaccia della riga di comando di Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1199d-139">For more information on Azure NSGs, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="1199d-140">Aggiungere una regola di assenso SSH in ingresso</span><span class="sxs-lookup"><span data-stu-id="1199d-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="1199d-141">La VM Linux deve accedere da Internet, pertanto è necessaria una regola che consenta di lasciare entrare il traffico in ingresso verso la porta 22 della VM Linux.</span><span class="sxs-lookup"><span data-stu-id="1199d-141">The Linux VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the Linux VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="1199d-142">Aggiungere una subnet alla rete virtuale</span><span class="sxs-lookup"><span data-stu-id="1199d-142">Add a subnet to the VNet</span></span>

<span data-ttu-id="1199d-143">Le macchine virtuali all'interno della rete virtuale devono trovarsi in una subnet.</span><span class="sxs-lookup"><span data-stu-id="1199d-143">VMs within the VNet must be located in a subnet.</span></span>  <span data-ttu-id="1199d-144">Ogni rete virtuale può avere più subnet.</span><span class="sxs-lookup"><span data-stu-id="1199d-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="1199d-145">Creare la subnet e associarla al gruppo di sicurezza di rete per aggiungere un firewall alla subnet.</span><span class="sxs-lookup"><span data-stu-id="1199d-145">Create the subnet and associate the subnet with the NSG to add a firewall to the subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="1199d-146">La subnet è ora aggiunta all'interno della rete virtuale e associata a un gruppo di sicurezza di rete e alla relativa regola.</span><span class="sxs-lookup"><span data-stu-id="1199d-146">The Subnet is now added inside the VNet and associated with the NSG and the NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="1199d-147">Creazione di nomi DNS statici</span><span class="sxs-lookup"><span data-stu-id="1199d-147">Creating static DNS names</span></span>

<span data-ttu-id="1199d-148">Sebbene Azure sia molto flessibile, per poter usare nomi DNS per la risoluzione dei nomi di macchine virtuali, è necessario crearli come schede di interfaccia di rete virtuale mediante l'etichettatura DNS.</span><span class="sxs-lookup"><span data-stu-id="1199d-148">Azure is very flexible, but to use DNS names for VMs name resolution, you need to create them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="1199d-149">Le schede di interfaccia di rete virtuale sono importanti in quanto possono essere riusate connettendole ad altre macchine virtuali. In questo senso, la scheda di interfaccia di rete virtuale è una risorsa statica, mentre le macchine virtuali possono essere temporanee.</span><span class="sxs-lookup"><span data-stu-id="1199d-149">VNics are important as you can reuse them by connecting them to different VMs, which keeps the VNic as a static resource while the VMs can be temporary.</span></span>  <span data-ttu-id="1199d-150">Applicando l'etichettatura DNS a una scheda di interfaccia di rete virtuale, è possibile abilitare nella rete virtuale la risoluzione di nomi semplici provenienti da altre macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1199d-150">By using DNS labeling on the VNic, we are able to enable simple name resolution from other VMs in the VNet.</span></span>  <span data-ttu-id="1199d-151">L'uso di nomi risolvibili consente anche ad altre macchine virtuali di accedere al server di automazione in base al nome DNS `Jenkins` o al server Git come `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="1199d-151">Using resolvable names enables other VMs to access the automation server by the DNS name `Jenkins` or the Git server as `gitrepo`.</span></span>  <span data-ttu-id="1199d-152">Creare una scheda di rete virtuale e associarla alla subnet creata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="1199d-152">Create a VNic and associate it with the Subnet created in the previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="1199d-153">Distribuire la macchina virtuale nella rete virtuale e nel gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="1199d-153">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="1199d-154">A questo punto sono disponibili una rete virtuale, una subnet all'interno di tale rete virtuale e un gruppo di sicurezza di rete che funge da firewall per proteggere la subnet bloccando tutto il traffico in ingresso tranne quello verso la porta 22 per SSH.</span><span class="sxs-lookup"><span data-stu-id="1199d-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="1199d-155">È ora possibile distribuire la macchina virtuale all'interno di questa infrastruttura di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="1199d-155">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="1199d-156">Con l'interfaccia della riga di comando di Azure e il comando `azure vm create`, la VM Linux viene distribuita nel gruppo di risorse, nella rete virtuale, nella subnet e nella scheda di rete virtuale esistenti.</span><span class="sxs-lookup"><span data-stu-id="1199d-156">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="1199d-157">Per altre informazioni sull'utilizzo dell'interfaccia della riga di comando per distribuire una macchina virtuale completa, vedere [Creare un ambiente Linux completo tramite l'interfaccia della riga di comando di Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1199d-157">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

<span data-ttu-id="1199d-158">Usando i flag dell'interfaccia della riga di comando per chiamare le risorse esistenti, si indica ad Azure di distribuire la macchina virtuale all'interno della rete esistente.</span><span class="sxs-lookup"><span data-stu-id="1199d-158">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span></span>  <span data-ttu-id="1199d-159">Come già detto, dopo essere state distribuite la rete virtuale e la subnet possono essere usate come risorse statiche o permanenti nell'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="1199d-159">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1199d-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1199d-160">Next steps</span></span>
* [<span data-ttu-id="1199d-161">Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="1199d-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="1199d-162">Creare una VM Linux in Azure usando i modelli</span><span class="sxs-lookup"><span data-stu-id="1199d-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
