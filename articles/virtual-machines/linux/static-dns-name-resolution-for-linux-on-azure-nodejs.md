---
title: aaaUsing DNS interno per la macchina virtuale la risoluzione dei nomi in Azure | Documenti Microsoft
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
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="afe5d-103">Uso del DNS interno per la risoluzione dei nomi di macchine virtuali in Azure</span><span class="sxs-lookup"><span data-stu-id="afe5d-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="afe5d-104">Questo articolo illustra come tooset nomi DNS interni statici per le macchine virtuali Linux con schede di rete virtuale (VNic) e i nomi DNS con etichetta.</span><span class="sxs-lookup"><span data-stu-id="afe5d-104">This article shows how tooset static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="afe5d-105">Si ricorre ai nomi DNS statici per i servizi di infrastruttura permanenti, ad esempio per un server di compilazione Jenkins, usato per questo documento, o un server Git.</span><span class="sxs-lookup"><span data-stu-id="afe5d-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="afe5d-106">requisiti di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="afe5d-106">hello requirements are:</span></span>

* [<span data-ttu-id="afe5d-107">Un account di Azure</span><span class="sxs-lookup"><span data-stu-id="afe5d-107">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="afe5d-108">File di chiavi SSH pubbliche e private</span><span class="sxs-lookup"><span data-stu-id="afe5d-108">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="afe5d-109">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="afe5d-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="afe5d-110">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="afe5d-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="afe5d-111">[Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="afe5d-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="afe5d-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="afe5d-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="afe5d-113">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="afe5d-113">Quick commands</span></span>

<span data-ttu-id="afe5d-114">Se è necessario tooquickly attività hello, hello successiva sezione Dettagli comandi hello necessari.</span><span class="sxs-lookup"><span data-stu-id="afe5d-114">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="afe5d-115">Ulteriori informazioni e il contesto per ogni passaggio è reperibile rest hello del documento hello, [avvio qui](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="afe5d-115">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="afe5d-116">Prerequisiti: gruppo di risorse, rete virtuale, gruppo di sicurezza di rete con SSH in ingresso, subnet.</span><span class="sxs-lookup"><span data-stu-id="afe5d-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="afe5d-117">Creare una scheda di interfaccia di rete virtuale con un nome DNS interno statico</span><span class="sxs-lookup"><span data-stu-id="afe5d-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="afe5d-118">Hello `-r` flag cli è per l'etichetta DNS di impostazione hello, che fornisce nome DNS statico hello per hello scheda di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="afe5d-118">hello `-r` cli flag is for setting hello DNS label, which provides hello static DNS name for hello VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a><span data-ttu-id="afe5d-119">Distribuire hello VM in hello rete virtuale, gruppo e, connettersi hello VNic</span><span class="sxs-lookup"><span data-stu-id="afe5d-119">Deploy hello VM into hello VNet, NSG and, connect hello VNic</span></span>

<span data-ttu-id="afe5d-120">Hello `-N` si connette hello VNic toohello nuova macchina virtuale durante hello tooAzure di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="afe5d-120">hello `-N` connects hello VNic toohello new VM during hello deployment tooAzure.</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="afe5d-121">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="afe5d-121">Detailed walkthrough</span></span>

<span data-ttu-id="afe5d-122">Un'integrazione completa continua e distribuzione continua (CiCd) infrastruttura di Azure richiede alcuni server server toobe statico o di lunga durata.</span><span class="sxs-lookup"><span data-stu-id="afe5d-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span>  <span data-ttu-id="afe5d-123">È consigliabile che le risorse di Azure come le reti virtuali (Vnet) hello e rete sicurezza gruppi, deve essere statiche e le risorse distribuite raramente di lunga durata.</span><span class="sxs-lookup"><span data-stu-id="afe5d-123">It is recommended that Azure assets like hello Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="afe5d-124">Dopo la distribuzione di una rete virtuale, può essere riutilizzato per nuove distribuzioni senza alcuna infrastruttura toohello effetto negativo.</span><span class="sxs-lookup"><span data-stu-id="afe5d-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span>  <span data-ttu-id="afe5d-125">Aggiunta di rete statica toothis un Git repository server e un server di automazione di Jenkins offre CiCd tooyour gli ambienti di sviluppo o test.</span><span class="sxs-lookup"><span data-stu-id="afe5d-125">Adding toothis static network a Git repository server and a Jenkins automation server delivers CiCd tooyour development or test environments.</span></span>  

<span data-ttu-id="afe5d-126">I nomi DNS interni sono risolvibili solo all'interno di una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="afe5d-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="afe5d-127">I nomi DNS hello sono interni, pertanto non sono toohello risolvibile all'esterno di internet, offre un'infrastruttura toohello aggiuntiva di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="afe5d-127">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="afe5d-128">_Sostituire i nomi nell'esempio con nomi personalizzati._</span><span class="sxs-lookup"><span data-stu-id="afe5d-128">_Replace any examples with your own naming._</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="afe5d-129">Creare il gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="afe5d-129">Create hello Resource group</span></span>

<span data-ttu-id="afe5d-130">Un gruppo di risorse è necessario tooorganize tutto ciò che viene creata nella procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="afe5d-130">A Resource Group is needed tooorganize everything we create in this walkthrough.</span></span>  <span data-ttu-id="afe5d-131">Per altre informazioni sui gruppi di risorse di Azure, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="afe5d-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="afe5d-132">Creare hello rete virtuale</span><span class="sxs-lookup"><span data-stu-id="afe5d-132">Create hello VNet</span></span>

<span data-ttu-id="afe5d-133">primo passaggio Hello è toobuild toolaunch una rete virtuale hello macchine virtuali in.</span><span class="sxs-lookup"><span data-stu-id="afe5d-133">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span>  <span data-ttu-id="afe5d-134">Hello rete virtuale contiene una subnet per questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="afe5d-134">hello VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="afe5d-135">Per ulteriori informazioni sulle reti virtuali di Azure, vedere [creare una rete virtuale tramite hello CLI di Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="afe5d-135">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a><span data-ttu-id="afe5d-136">Creare hello NSG</span><span class="sxs-lookup"><span data-stu-id="afe5d-136">Create hello NSG</span></span>

<span data-ttu-id="afe5d-137">Hello Subnet si basa dietro a un gruppo di sicurezza di rete esistente, creata hello NSG prima hello Subnet.</span><span class="sxs-lookup"><span data-stu-id="afe5d-137">hello Subnet is built behind an existing Network Security Group so we build hello NSG before hello Subnet.</span></span>  <span data-ttu-id="afe5d-138">Azure NSGs sono equivalenti tooa firewall a livello di rete hello.</span><span class="sxs-lookup"><span data-stu-id="afe5d-138">Azure NSGs are equivalent tooa firewall at hello network layer.</span></span>  <span data-ttu-id="afe5d-139">Per ulteriori informazioni su Azure NSGs, vedere [come NSGs toocreate in hello CLI di Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="afe5d-139">For more information on Azure NSGs, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="afe5d-140">Aggiungere una regola di assenso SSH in ingresso</span><span class="sxs-lookup"><span data-stu-id="afe5d-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="afe5d-141">Hello VM Linux richiede l'accesso da hello internet in modo da una regola che consente di porta in ingresso traffico 22 toobe passati tramite hello rete tooport 22 hello VM Linux è necessaria.</span><span class="sxs-lookup"><span data-stu-id="afe5d-141">hello Linux VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello Linux VM is needed.</span></span>

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

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="afe5d-142">Aggiungere un toohello subnet rete virtuale</span><span class="sxs-lookup"><span data-stu-id="afe5d-142">Add a subnet toohello VNet</span></span>

<span data-ttu-id="afe5d-143">Macchine virtuali all'interno di hello rete virtuale devono trovarsi in una subnet.</span><span class="sxs-lookup"><span data-stu-id="afe5d-143">VMs within hello VNet must be located in a subnet.</span></span>  <span data-ttu-id="afe5d-144">Ogni rete virtuale può avere più subnet.</span><span class="sxs-lookup"><span data-stu-id="afe5d-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="afe5d-145">Creare subnet hello e associare subnet hello hello NSG tooadd una subnet toohello firewall.</span><span class="sxs-lookup"><span data-stu-id="afe5d-145">Create hello subnet and associate hello subnet with hello NSG tooadd a firewall toohello subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="afe5d-146">Hello Subnet è ora aggiunto all'interno di reti virtuali hello e associata a hello gruppo e regola gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="afe5d-146">hello Subnet is now added inside hello VNet and associated with hello NSG and hello NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="afe5d-147">Creazione di nomi DNS statici</span><span class="sxs-lookup"><span data-stu-id="afe5d-147">Creating static DNS names</span></span>

<span data-ttu-id="afe5d-148">Azure è molto flessibile, ma toouse i nomi DNS per la risoluzione dei nomi di macchine virtuali, è necessario toocreate come virtuale schede (VNics) tramite l'assegnazione di etichette DNS di rete.</span><span class="sxs-lookup"><span data-stu-id="afe5d-148">Azure is very flexible, but toouse DNS names for VMs name resolution, you need toocreate them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="afe5d-149">VNics sono importanti per poterli usare di nuovo connettendo le macchine virtuali toodifferent, che consente di mantenere hello VNic come una risorsa statica hello macchine virtuali può essere temporaneo.</span><span class="sxs-lookup"><span data-stu-id="afe5d-149">VNics are important as you can reuse them by connecting them toodifferent VMs, which keeps hello VNic as a static resource while hello VMs can be temporary.</span></span>  <span data-ttu-id="afe5d-150">Tramite l'assegnazione di etichette in hello VNic DNS, siamo tooenable in grado di risoluzione dei nomi semplici da altre macchine virtuali nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="afe5d-150">By using DNS labeling on hello VNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span>  <span data-ttu-id="afe5d-151">Utilizzo dei nomi di risolvibili consente altri server di automazione hello tooaccess macchine virtuali in base al nome DNS hello `Jenkins` o di server di Git hello `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="afe5d-151">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  <span data-ttu-id="afe5d-152">Creare una scheda di rete virtuale e associarlo a hello che subnet creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="afe5d-152">Create a VNic and associate it with hello Subnet created in hello previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="afe5d-153">Distribuire hello VM nella rete virtuale hello e gruppo</span><span class="sxs-lookup"><span data-stu-id="afe5d-153">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="afe5d-154">È ora disponibile una rete virtuale, una subnet all'interno di tale rete virtuale e un gruppo che agisce come un tooprotect firewall la subnet bloccare tutto il traffico in ingresso, ad eccezione di porta 22 per SSH.</span><span class="sxs-lookup"><span data-stu-id="afe5d-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="afe5d-155">è ora possibile distribuire Hello VM all'interno di questa infrastruttura di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="afe5d-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="afe5d-156">Utilizzando hello Azure CLI e hello `azure vm create` comando hello VM Linux è toohello distribuito esistente al gruppo di risorse di Azure, rete virtuale, Subnet e scheda di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="afe5d-156">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="afe5d-157">Per ulteriori informazioni sull'utilizzo di hello CLI toodeploy una VM completezza, vedere [creare un ambiente completo di Linux mediante hello CLI di Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="afe5d-157">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

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

<span data-ttu-id="afe5d-158">Utilizzando hello CLI flag toocall risorse esistente, è indicare hello toodeploy Azure VM all'interno di una rete esistente hello.</span><span class="sxs-lookup"><span data-stu-id="afe5d-158">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span>  <span data-ttu-id="afe5d-159">tooreiterate, dopo una rete virtuale e subnet sono stati distribuiti, essi possono essere lasciati come statiche o permanente di risorse all'interno di propria area di Azure.</span><span class="sxs-lookup"><span data-stu-id="afe5d-159">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="afe5d-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="afe5d-160">Next steps</span></span>
* [<span data-ttu-id="afe5d-161">Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="afe5d-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="afe5d-162">Creare una VM Linux in Azure usando i modelli</span><span class="sxs-lookup"><span data-stu-id="afe5d-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
