---
title: aaaDeploy le macchine virtuali Linux in una rete esistente con 1.0 CLI di Azure | Documenti Microsoft
description: Come toodeploy una VM Linux in una rete virtuale esistente usando hello Azure CLI 1.0
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a><span data-ttu-id="d25d5-103">Come una macchina virtuale di Linux in una rete virtuale di Azure esistente con hello Azure CLI 1.0 toodeploy</span><span class="sxs-lookup"><span data-stu-id="d25d5-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI 1.0</span></span>

<span data-ttu-id="d25d5-104">In questo articolo illustra come toouse CLI di Azure 1.0 toodeploy una macchina virtuale (VM) in una rete virtuale esistente (VNet).</span><span class="sxs-lookup"><span data-stu-id="d25d5-104">This article shows you how toouse Azure CLI 1.0 toodeploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="d25d5-105">requisiti di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="d25d5-105">hello requirements are:</span></span>

- [<span data-ttu-id="d25d5-106">Un account di Azure</span><span class="sxs-lookup"><span data-stu-id="d25d5-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="d25d5-107">File di chiavi SSH pubbliche e private</span><span class="sxs-lookup"><span data-stu-id="d25d5-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="d25d5-108">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="d25d5-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="d25d5-109">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="d25d5-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="d25d5-110">[Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="d25d5-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="d25d5-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="d25d5-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="d25d5-112">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="d25d5-112">Quick Commands</span></span>

<span data-ttu-id="d25d5-113">Se è necessario tooquickly attività hello, hello successiva sezione Dettagli comandi hello necessari.</span><span class="sxs-lookup"><span data-stu-id="d25d5-113">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="d25d5-114">Ulteriori informazioni e il contesto per ogni passaggio è reperibile rest hello del documento hello, [avvio qui](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="d25d5-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="d25d5-115">Prerequisiti: gruppo di risorse, rete virtuale, gruppo di sicurezza di rete con SSH in ingresso, subnet.</span><span class="sxs-lookup"><span data-stu-id="d25d5-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="d25d5-116">Sostituire gli esempi con le impostazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="d25d5-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="d25d5-117">Distribuire hello VM nell'infrastruttura di rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="d25d5-117">Deploy hello VM into hello virtual network infrastructure</span></span>

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="d25d5-118">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="d25d5-118">Detailed walkthrough</span></span>

<span data-ttu-id="d25d5-119">Risorse di Azure come hello reti virtuali e i gruppi di sicurezza di rete devono essere statici e le risorse distribuite raramente di lunga durata.</span><span class="sxs-lookup"><span data-stu-id="d25d5-119">Azure assets like hello VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="d25d5-120">Dopo la distribuzione di una rete virtuale, può essere riutilizzato per nuove distribuzioni senza alcuna infrastruttura toohello effetto negativo.</span><span class="sxs-lookup"><span data-stu-id="d25d5-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="d25d5-121">Si pensi a una rete virtuale come se fosse uno switch di rete hardware tradizionale.</span><span class="sxs-lookup"><span data-stu-id="d25d5-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="d25d5-122">Non è necessario passare un nuovo hardware per ciascuna distribuzione tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="d25d5-122">You would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="d25d5-123">Con una rete virtuale è configurata correttamente, è possibile continuare toodeploy nuovi server in tale rete virtuale a più volte con alcuni, se presente, le modifiche richieste per la durata hello di hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d25d5-123">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="d25d5-124">Creare il gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="d25d5-124">Create hello resource group</span></span>

<span data-ttu-id="d25d5-125">Creare innanzitutto un tooorganize gruppo di risorse tutti gli oggetti creati in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="d25d5-125">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="d25d5-126">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d25d5-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="d25d5-127">Creare hello rete virtuale</span><span class="sxs-lookup"><span data-stu-id="d25d5-127">Create hello VNet</span></span>

<span data-ttu-id="d25d5-128">primo passaggio Hello è toobuild toolaunch una rete virtuale hello macchine virtuali in.</span><span class="sxs-lookup"><span data-stu-id="d25d5-128">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="d25d5-129">Hello rete virtuale contiene una subnet per questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="d25d5-129">hello VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="d25d5-130">Per ulteriori informazioni sulle reti virtuali di Azure, vedere [creare una rete virtuale tramite hello CLI di Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d25d5-130">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="d25d5-131">Creare un gruppo di sicurezza di rete hello</span><span class="sxs-lookup"><span data-stu-id="d25d5-131">Create hello network security group</span></span>

<span data-ttu-id="d25d5-132">subnet Hello viene compilato dietro a un gruppo di sicurezza di rete esistente pertanto creare gruppi di sicurezza di rete hello prima subnet hello.</span><span class="sxs-lookup"><span data-stu-id="d25d5-132">hello subnet is built behind an existing network security group so build hello network security group before hello subnet.</span></span> <span data-ttu-id="d25d5-133">Gruppi di sicurezza di rete di Azure sono equivalenti tooa firewall a livello di rete hello.</span><span class="sxs-lookup"><span data-stu-id="d25d5-133">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="d25d5-134">Per ulteriori informazioni sui gruppi di sicurezza di rete di Azure, vedere [come i gruppi di sicurezza di rete toocreate in hello CLI di Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d25d5-134">For more information on Azure network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="d25d5-135">Aggiungere una regola di assenso SSH in ingresso</span><span class="sxs-lookup"><span data-stu-id="d25d5-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="d25d5-136">Hello VM richiede l'accesso da hello internet in modo da una regola che consente la porta in ingresso 22 traffico toobe passati tramite hello rete tooport 22 hello macchina virtuale è necessaria.</span><span class="sxs-lookup"><span data-stu-id="d25d5-136">hello VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="d25d5-137">Aggiungere un toohello subnet rete virtuale</span><span class="sxs-lookup"><span data-stu-id="d25d5-137">Add a subnet toohello VNet</span></span>

<span data-ttu-id="d25d5-138">Macchine virtuali all'interno di hello rete virtuale devono trovarsi in una subnet.</span><span class="sxs-lookup"><span data-stu-id="d25d5-138">VMs within hello VNet must be located in a subnet.</span></span> <span data-ttu-id="d25d5-139">Ogni rete virtuale può avere più subnet.</span><span class="sxs-lookup"><span data-stu-id="d25d5-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="d25d5-140">Creare subnet hello e associare al gruppo di sicurezza di rete hello.</span><span class="sxs-lookup"><span data-stu-id="d25d5-140">Create hello subnet and associate with hello network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="d25d5-141">Hello Subnet è ora aggiunto all'interno di reti virtuali hello e associata alla regola e gruppo di sicurezza di rete hello.</span><span class="sxs-lookup"><span data-stu-id="d25d5-141">hello Subnet is now added inside hello VNet and associated with hello network security group and rule.</span></span>


## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="d25d5-142">Aggiungere una subnet toohello VNic</span><span class="sxs-lookup"><span data-stu-id="d25d5-142">Add a VNic toohello subnet</span></span>

<span data-ttu-id="d25d5-143">Schede di rete virtuale (VNics) sono importanti, come è possibile riutilizzare gli connettendo le macchine virtuali toodifferent.</span><span class="sxs-lookup"><span data-stu-id="d25d5-143">Virtual network cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="d25d5-144">Questo approccio consente di mantenere hello VNic come una risorsa statica durante hello macchine virtuali può essere temporaneo.</span><span class="sxs-lookup"><span data-stu-id="d25d5-144">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="d25d5-145">Creare una scheda di rete virtuale e associarlo a subnet hello creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d25d5-145">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="d25d5-146">Distribuire hello VM nella rete virtuale hello e gruppo</span><span class="sxs-lookup"><span data-stu-id="d25d5-146">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="d25d5-147">È ora disponibile una rete virtuale e una subnet all'interno di tale rete virtuale e un gruppo di sicurezza di rete che agisce subnet hello tooprotect bloccare tutto il traffico in ingresso, ad eccezione di porta 22 per SSH.</span><span class="sxs-lookup"><span data-stu-id="d25d5-147">You now have a VNet and subnet inside that VNet, and a network security group acting tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="d25d5-148">è ora possibile distribuire Hello VM all'interno di questa infrastruttura di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="d25d5-148">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="d25d5-149">Utilizzando hello Azure CLI e hello `azure vm create` comando hello VM Linux è toohello distribuito esistente al gruppo di risorse di Azure, rete virtuale, Subnet e scheda di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d25d5-149">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="d25d5-150">Per ulteriori informazioni sull'utilizzo di hello CLI toodeploy una VM completezza, vedere [creare un ambiente completo di Linux mediante hello CLI di Azure](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="d25d5-150">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md)</span></span>

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

<span data-ttu-id="d25d5-151">Utilizzando hello CLI flag toocall risorse esistente, indicando hello toodeploy Azure VM all'interno di una rete esistente hello.</span><span class="sxs-lookup"><span data-stu-id="d25d5-151">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="d25d5-152">Una volta distribuite la rete virtuale e la subnet possono essere usate come risorse statiche o permanenti nell'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="d25d5-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d25d5-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d25d5-153">Next steps</span></span>

* [<span data-ttu-id="d25d5-154">Utilizzare un toocreate modello di gestione risorse di Azure una distribuzione specifica</span><span class="sxs-lookup"><span data-stu-id="d25d5-154">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="d25d5-155">Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d25d5-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="d25d5-156">Creare una VM Linux in Azure usando i modelli</span><span class="sxs-lookup"><span data-stu-id="d25d5-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
