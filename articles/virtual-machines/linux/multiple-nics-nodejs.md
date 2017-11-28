---
title: "una VM Linux di Azure con più schede di rete aaaCreate | Documenti Microsoft"
description: "Informazioni su come toocreate una VM Linux con più schede di rete associata tooit modelli hello CLI di Azure o di gestione delle risorse."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="8eedc-103">Creare una macchina virtuale Linux con più schede di rete utilizzando hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8eedc-103">Create a Linux virtual machine with multiple NICs using hello Azure CLI 1.0</span></span>
<span data-ttu-id="8eedc-104">È possibile creare una macchina virtuale (VM) in Azure con più tooit interfacce (NIC) collegate di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8eedc-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="8eedc-105">Uno scenario comune è toohave subnet diverse per la connettività front-end e back-end, o una rete dedicata tooa monitoraggio o una soluzione di backup.</span><span class="sxs-lookup"><span data-stu-id="8eedc-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="8eedc-106">Questo articolo fornisce comandi rapidi toocreate una macchina virtuale con più schede di rete associate tooit.</span><span class="sxs-lookup"><span data-stu-id="8eedc-106">This article provides quick commands toocreate a VM with multiple NICs attached tooit.</span></span> <span data-ttu-id="8eedc-107">Per informazioni dettagliate, incluso come toocreate più schede di rete all'interno del proprio Bash script, altre informazioni sui [la distribuzione di macchine virtuali multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8eedc-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="8eedc-108">Le differenti [dimensioni della macchina virtuale](sizes.md) supportano un numero variabile di schede di rete, pertanto scegliere le dimensioni della macchina virtuale di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="8eedc-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="8eedc-109">Quando si crea una macchina virtuale: non è possibile aggiungere schede NIC tooan esistente VM con hello Azure CLI 1.0, è necessario collegare più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="8eedc-109">You must attach multiple NICs when you create a VM - you cannot add NICs tooan existing VM with hello Azure CLI 1.0.</span></span> <span data-ttu-id="8eedc-110">È possibile [aggiungere NIC tooan esistente VM con hello Azure CLI 2.0](multiple-nics.md).</span><span class="sxs-lookup"><span data-stu-id="8eedc-110">You can [add NICs tooan existing VM with hello Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="8eedc-111">È anche possibile [creare una macchina virtuale in base a dischi virtuali originale hello](copy-vm.md) e creare più schede di rete quando si distribuisce hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8eedc-111">You can also [create a VM based on hello original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy hello VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="8eedc-112">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="8eedc-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="8eedc-113">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="8eedc-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="8eedc-114">[Azure CLI 1.0](#create-supporting-resources) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="8eedc-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="8eedc-115">[Azure CLI 2.0](multiple-nics.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="8eedc-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="8eedc-116">Creare risorse di supporto</span><span class="sxs-lookup"><span data-stu-id="8eedc-116">Create supporting resources</span></span>
<span data-ttu-id="8eedc-117">Assicurarsi di avere hello [CLI di Azure](../../cli-install-nodejs.md) effettuato l'accesso e utilizzo della modalità di gestione delle risorse:</span><span class="sxs-lookup"><span data-stu-id="8eedc-117">Make sure that you have hello [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="8eedc-118">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="8eedc-118">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8eedc-119">I nomi dei parametri di esempio includono *myResourceGroup*, *mystorageaccount* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="8eedc-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="8eedc-120">Creare prima un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8eedc-120">First, create a resource group.</span></span> <span data-ttu-id="8eedc-121">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="8eedc-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="8eedc-122">Creare un toohold di account di archiviazione delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8eedc-122">Create a storage account toohold your VMs.</span></span> <span data-ttu-id="8eedc-123">esempio Hello crea un account di archiviazione denominato *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="8eedc-123">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="8eedc-124">Creare una rete virtuale di tooconnect le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8eedc-124">Create a virtual network tooconnect your VMs to.</span></span> <span data-ttu-id="8eedc-125">esempio Hello crea una rete virtuale denominata *myVnet* con un prefisso dell'indirizzo *192.168.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="8eedc-125">hello following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="8eedc-126">Creare due subnet per la rete virtuale: una per il traffico front-end e l'altra per il traffico di back-end.</span><span class="sxs-lookup"><span data-stu-id="8eedc-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="8eedc-127">esempio Hello crea due subnet, denominata *mySubnetFrontEnd* e *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="8eedc-127">hello following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="8eedc-128">Creare e configurare più schede di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="8eedc-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="8eedc-129">È possibile leggere altre informazioni su [la distribuzione di più schede di rete mediante Azure CLI hello](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), inclusi gli script di processo hello scorrere in ciclo toocreate tutte le NIC hello.</span><span class="sxs-lookup"><span data-stu-id="8eedc-129">You can read more details about [deploying multiple NICs using hello Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting hello process of looping through toocreate all hello NICs.</span></span>

<span data-ttu-id="8eedc-130">esempio Hello crea due schede di rete, denominati *myNic1* e *myNic2*, con una scheda di rete che connettono tooeach subnet:</span><span class="sxs-lookup"><span data-stu-id="8eedc-130">hello following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting tooeach subnet:</span></span>

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

<span data-ttu-id="8eedc-131">In genere si crea anche un [Network Security Group](../../virtual-network/virtual-networks-nsg.md) o [bilanciamento del carico](../../load-balancer/load-balancer-overview.md) toohelp gestire e distribuire il traffico tra le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8eedc-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="8eedc-132">esempio Hello crea un gruppo di sicurezza di rete denominata *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8eedc-132">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="8eedc-133">Associare il gruppo di sicurezza di rete toohello NIC utilizzando `azure network nic set`.</span><span class="sxs-lookup"><span data-stu-id="8eedc-133">Bind your NICs toohello Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="8eedc-134">Hello esempio associa *myNic1* e *myNic2* con *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8eedc-134">hello following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="8eedc-135">Creare una macchina virtuale e collegare le schede NIC hello</span><span class="sxs-lookup"><span data-stu-id="8eedc-135">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="8eedc-136">Quando si creano hello VM, è ora possibile specificare più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="8eedc-136">When creating hello VM, you now specify multiple NICs.</span></span> <span data-ttu-id="8eedc-137">Utilizzano invece `--nic-name` tooprovide una singola scheda di rete, usare invece la `--nic-names` e fornire un elenco delimitato da virgole di schede di rete.</span><span class="sxs-lookup"><span data-stu-id="8eedc-137">Rather using `--nic-name` tooprovide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="8eedc-138">È necessario anche tootake attenzione quando si seleziona hello dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8eedc-138">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="8eedc-139">Vi sono limiti per il numero totale di schede di rete che è possibile aggiungere VM tooa hello.</span><span class="sxs-lookup"><span data-stu-id="8eedc-139">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="8eedc-140">Ulteriori informazioni sulle [dimensioni delle macchine virtuali di Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="8eedc-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="8eedc-141">Hello esempio seguente viene illustrato come toospecify più schede di rete e quindi una macchina virtuale di dimensione che supporta l'utilizzo di più schede di rete (*Standard_DS2_v2*):</span><span class="sxs-lookup"><span data-stu-id="8eedc-141">hello following example shows how toospecify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="8eedc-142">Creare più schede di interfaccia di rete usando i modelli di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8eedc-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="8eedc-143">Modelli di gestione risorse di Azure utilizzano dichiarativa JSON file toodefine l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="8eedc-143">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="8eedc-144">È possibile consultare una [panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8eedc-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="8eedc-145">Modelli di gestione risorse forniscono un modo toocreate più istanze di una risorsa durante la distribuzione, ad esempio la creazione di più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="8eedc-145">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="8eedc-146">Utilizzare *copia* numero hello toospecify di toocreate istanze:</span><span class="sxs-lookup"><span data-stu-id="8eedc-146">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="8eedc-147">Ulteriori informazioni sulla [creazione di più istanze utilizzando *Copia*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="8eedc-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="8eedc-148">È inoltre possibile utilizzare un `copyIndex()` toothen aggiungere un nome di risorsa tooa numero, che consente di toocreate `myNic1`, `myNic2`, e così via hello seguito è riportato un esempio di aggiunta di valore di indice hello:</span><span class="sxs-lookup"><span data-stu-id="8eedc-148">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="8eedc-149">È possibile consultare un esempio completo di [creazione di più schede di rete utilizzando i modelli di Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="8eedc-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8eedc-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8eedc-150">Next steps</span></span>
<span data-ttu-id="8eedc-151">Verificare che tooreview [le dimensioni di VM Linux](sizes.md) durante il tentativo di toocreating una macchina virtuale con più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="8eedc-151">Make sure tooreview [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="8eedc-152">Prestare attenzione toohello massimo NIC supporta ogni dimensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8eedc-152">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="8eedc-153">Tenere presente che non è possibile aggiungere ulteriori tooan di schede di rete VM esistente, è necessario creare tutte le NIC hello quando si distribuisce hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8eedc-153">Remember that you cannot add additional NICs tooan existing VM, you must create all hello NICs when you deploy hello VM.</span></span> <span data-ttu-id="8eedc-154">Prestare attenzione quando si pianifica la toomake le distribuzioni di avere hello necessaria la connettività di rete sin hello.</span><span class="sxs-lookup"><span data-stu-id="8eedc-154">Take care when planning your deployments toomake sure that you have all hello required network connectivity from hello outset.</span></span>

