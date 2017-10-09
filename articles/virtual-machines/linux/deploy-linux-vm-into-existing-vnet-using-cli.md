---
title: aaaDeploy le macchine virtuali Linux in una rete esistente con Azure CLI 2.0 | Documenti Microsoft
description: Informazioni su come una macchina virtuale di Linux in una rete virtuale esistente usando toodeploy hello Azure CLI 2.0
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
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a><span data-ttu-id="a6e92-103">Come toodeploy una macchina virtuale di Linux in una rete virtuale di Azure esistente con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="a6e92-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI</span></span>

<span data-ttu-id="a6e92-104">Questo articolo illustra come toouse hello Azure CLI 2.0 toodeploy una macchina virtuale (VM) in una rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="a6e92-104">This article shows you how toouse hello Azure CLI 2.0 toodeploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="a6e92-105">requisiti di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="a6e92-105">hello requirements are:</span></span>

- [<span data-ttu-id="a6e92-106">Un account di Azure</span><span class="sxs-lookup"><span data-stu-id="a6e92-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="a6e92-107">File di chiavi SSH pubbliche e private</span><span class="sxs-lookup"><span data-stu-id="a6e92-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

<span data-ttu-id="a6e92-108">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a6e92-108">You can also perform these steps with hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="a6e92-109">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="a6e92-109">Quick Commands</span></span>
<span data-ttu-id="a6e92-110">Se è necessario tooquickly attività hello, hello successiva sezione Dettagli comandi hello necessari.</span><span class="sxs-lookup"><span data-stu-id="a6e92-110">If you need tooquickly accomplish hello task, hello following section details hello  commands needed.</span></span> <span data-ttu-id="a6e92-111">Ulteriori informazioni e il contesto per ogni passaggio è reperibile rest hello del documento hello, [avvio qui](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="a6e92-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="a6e92-112">toocreate questo ambiente personalizzato, è necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="a6e92-112">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="a6e92-113">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="a6e92-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="a6e92-114">I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="a6e92-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="a6e92-115">**Pre-requisiti:** gruppo di risorse di Azure, rete virtuale e subnet, gruppo di sicurezza di rete con SSH in ingresso e una scheda di interfaccia di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a6e92-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="a6e92-116">Distribuire hello VM nell'infrastruttura di rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="a6e92-116">Deploy hello VM into hello virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="a6e92-117">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="a6e92-117">Detailed walkthrough</span></span>

<span data-ttu-id="a6e92-118">Gli asset di Azure, come le reti virtuali e i gruppi di sicurezza di rete devono essere risorse statiche, ovvero di lunga durata e distribuite raramente.</span><span class="sxs-lookup"><span data-stu-id="a6e92-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="a6e92-119">Dopo la distribuzione di una rete virtuale, può essere riutilizzato per nuove distribuzioni senza alcuna infrastruttura toohello effetto negativo.</span><span class="sxs-lookup"><span data-stu-id="a6e92-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="a6e92-120">Pensare a una rete virtuale come un commutatore di rete tradizionale hardware: non è necessario passare un nuovo hardware per ciascuna distribuzione tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="a6e92-120">Think about a virtual network as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="a6e92-121">Con una rete virtuale configurata correttamente, è possibile continuare toodeploy nuove macchine virtuali in tale rete virtuale più volte con poche, eventuali modifiche necessarie per la durata hello della rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="a6e92-121">With a correctly configured virtual network, you can continue toodeploy new VMs into that virtual network over and over with few, if any, changes required over hello life of hello virtual network.</span></span>

<span data-ttu-id="a6e92-122">toocreate questo ambiente personalizzato, è necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="a6e92-122">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="a6e92-123">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="a6e92-123">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="a6e92-124">I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="a6e92-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="a6e92-125">Creare il gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="a6e92-125">Create hello resource group</span></span>

<span data-ttu-id="a6e92-126">Creare innanzitutto un tooorganize gruppo di risorse di Azure tutti gli oggetti creati in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="a6e92-126">First, create an Azure resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="a6e92-127">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6e92-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="a6e92-128">Creare il gruppo di risorse hello con [gruppo az creare](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a6e92-128">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a6e92-129">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="a6e92-129">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="a6e92-130">Creare una rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="a6e92-130">Create hello virtual network</span></span>

<span data-ttu-id="a6e92-131">Consente di compilare un hello toolaunch di rete virtuale di Azure le macchine virtuali in.</span><span class="sxs-lookup"><span data-stu-id="a6e92-131">Lets build an Azure virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="a6e92-132">Per ulteriori informazioni sulle reti virtuali, vedere [creare una rete virtuale mediante Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a6e92-132">For more information on virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="a6e92-133">Creare una rete virtuale di hello con [creazione della rete virtuale di rete az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="a6e92-133">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="a6e92-134">esempio Hello crea una rete virtuale denominata *myVnet* e subnet denominata *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="a6e92-134">hello following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="a6e92-135">Creare un gruppo di sicurezza di rete hello</span><span class="sxs-lookup"><span data-stu-id="a6e92-135">Create hello network security group</span></span>

<span data-ttu-id="a6e92-136">Gruppi di sicurezza di rete di Azure sono equivalenti tooa firewall a livello di rete hello.</span><span class="sxs-lookup"><span data-stu-id="a6e92-136">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="a6e92-137">Per ulteriori informazioni sui gruppi di sicurezza di rete, vedere [come i gruppi di sicurezza di rete toocreate in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a6e92-137">For more information on network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="a6e92-138">Creare un gruppo di sicurezza di rete hello con [rete az creare](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="a6e92-138">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="a6e92-139">esempio Hello crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="a6e92-139">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="a6e92-140">Aggiungere una regola di assenso SSH in ingresso</span><span class="sxs-lookup"><span data-stu-id="a6e92-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="a6e92-141">Hello VM richiede l'accesso da internet, in modo da una regola che consente la porta in ingresso 22 traffico toobe passati tramite hello rete tooport 22 hello VM è necessario hello.</span><span class="sxs-lookup"><span data-stu-id="a6e92-141">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span> <span data-ttu-id="a6e92-142">Aggiungere una regola in ingresso per il gruppo di sicurezza di rete hello con [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="a6e92-142">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="a6e92-143">esempio Hello crea una regola denominata *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="a6e92-143">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a><span data-ttu-id="a6e92-144">Collegare gruppi di sicurezza di rete di hello subnet toohello</span><span class="sxs-lookup"><span data-stu-id="a6e92-144">Attach hello subnet toohello network security group</span></span>

<span data-ttu-id="a6e92-145">regole di gruppo di sicurezza di rete Hello possono essere applicato tooa subnet o un'interfaccia di rete virtuale specifica.</span><span class="sxs-lookup"><span data-stu-id="a6e92-145">hello network security group rules can be applied tooa subnet or a specific virtual network interface.</span></span> <span data-ttu-id="a6e92-146">Consente di collegare la subnet tooour hello rete sicurezza gruppo.</span><span class="sxs-lookup"><span data-stu-id="a6e92-146">Lets attach hello network security group tooour subnet.</span></span> <span data-ttu-id="a6e92-147">Collegare il gruppo di sicurezza della rete toohello subnet con [aggiornare subnet rete virtuale di rete az](/cli/azure/network/vnet/subnet#update):</span><span class="sxs-lookup"><span data-stu-id="a6e92-147">Attach your subnet toohello network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a><span data-ttu-id="a6e92-148">Aggiungere una subnet di toohello scheda di interfaccia rete virtuale</span><span class="sxs-lookup"><span data-stu-id="a6e92-148">Add a virtual network interface card toohello subnet</span></span>

<span data-ttu-id="a6e92-149">Schede di interfaccia di rete virtuale (VNics) sono importanti, come è possibile riutilizzare gli connettendo le macchine virtuali toodifferent.</span><span class="sxs-lookup"><span data-stu-id="a6e92-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="a6e92-150">In questo modo consente hello tookeep VNic come una risorsa statica hello macchine virtuali può essere temporaneo.</span><span class="sxs-lookup"><span data-stu-id="a6e92-150">This reuse allows you tookeep hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="a6e92-151">Creare una scheda di rete virtuale e associarlo a subnet hello [az rete nic creare](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="a6e92-151">Create a VNic and associate it with hello subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="a6e92-152">esempio Hello crea una scheda di rete virtuale denominata *myNic*:</span><span class="sxs-lookup"><span data-stu-id="a6e92-152">hello following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="a6e92-153">Distribuire hello VM nell'infrastruttura di rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="a6e92-153">Deploy hello VM into hello virtual network infrastructure</span></span>

<span data-ttu-id="a6e92-154">Bloccare tutto il traffico in ingresso, ad eccezione di porta 22 per SSH è disponibile una rete virtuale e subnet e una subnet hello di tooprotect gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="a6e92-154">You now have a virtual network and subnet, and a network security group tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="a6e92-155">è ora possibile distribuire Hello VM all'interno di questa infrastruttura di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="a6e92-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="a6e92-156">Creare la macchina virtuale con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a6e92-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a6e92-157">Per ulteriori informazioni su hello flag toouse con toodeploy hello Azure CLI 2.0 una VM completezza, vedere [creare un ambiente completo di Linux mediante Azure CLI hello](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="a6e92-157">For more information on hello flags toouse with hello Azure CLI 2.0 toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="a6e92-158">Hello di esempio seguente crea una macchina virtuale tramite dischi gestiti di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6e92-158">hello following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="a6e92-159">I dischi vengono gestiti dalla piattaforma Azure hello e non richiedono alcun toostore preparazione o percorso li.</span><span class="sxs-lookup"><span data-stu-id="a6e92-159">These disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="a6e92-160">Per altre informazioni sui dischi gestiti, vedere [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md) (Panoramica di Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="a6e92-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="a6e92-161">Se si desiderano dischi toouse non gestita, vedere la nota aggiuntive hello sotto.</span><span class="sxs-lookup"><span data-stu-id="a6e92-161">If you wish toouse unmanaged disks, see hello additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="a6e92-162">Se si usa Managed Disks, ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="a6e92-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="a6e92-163">Se si desiderano dischi toouse non gestita, è necessario hello tooadd seguendo i dischi parametri aggiuntivi toohello procedere comando toocreate non gestita nell'account di archiviazione hello denominato `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="a6e92-163">If you wish toouse unmanaged disks, you need tooadd hello following additional parameters toohello proceeding command toocreate unmanaged disks in hello storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="a6e92-164">Utilizzando hello CLI flag toocall risorse esistente, indicando hello toodeploy Azure VM all'interno di una rete esistente hello.</span><span class="sxs-lookup"><span data-stu-id="a6e92-164">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="a6e92-165">Una volta distribuite la rete virtuale e la subnet possono essere usate come risorse statiche o permanenti nell'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6e92-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="a6e92-166">In questo esempio, si non creare e assegnare un toohello di indirizzo IP pubblico scheda di rete virtuale, in modo che questa macchina virtuale non è accessibile pubblicamente su Internet hello.</span><span class="sxs-lookup"><span data-stu-id="a6e92-166">In this example, you did not create and assign a public IP address toohello VNic, so this VM is not publicly accessible over hello Internet.</span></span> <span data-ttu-id="a6e92-167">Per ulteriori informazioni, vedere [creare una macchina virtuale con un indirizzo IP pubblico statico mediante Azure CLI hello](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a6e92-167">For more information, see [Create a VM with a static public IP using hello Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6e92-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6e92-168">Next steps</span></span>
<span data-ttu-id="a6e92-169">Per ulteriori informazioni su modi toocreate le macchine virtuali in Azure, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="a6e92-169">For more information about ways toocreate virtual machines in Azure, see hello following resources:</span></span>

* [<span data-ttu-id="a6e92-170">Utilizzare un toocreate modello di gestione risorse di Azure una distribuzione specifica</span><span class="sxs-lookup"><span data-stu-id="a6e92-170">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="a6e92-171">Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a6e92-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="a6e92-172">Creare una VM Linux in Azure usando i modelli</span><span class="sxs-lookup"><span data-stu-id="a6e92-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
