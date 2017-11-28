---
title: "una VM Linux di Azure con più schede di rete aaaCreate | Documenti Microsoft"
description: "Informazioni su come toocreate una VM Linux con più schede di rete associata tooit modelli hello CLI di Azure 2.0 o gestione delle risorse."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="d0d64-103">Come toocreate una macchina virtuale di Linux in Azure con la rete di più schede di interfaccia</span><span class="sxs-lookup"><span data-stu-id="d0d64-103">How toocreate a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="d0d64-104">È possibile creare una macchina virtuale (VM) in Azure con più tooit interfacce (NIC) collegate di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d0d64-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="d0d64-105">Uno scenario comune è toohave subnet diverse per la connettività front-end e back-end, o una rete dedicata tooa monitoraggio o una soluzione di backup.</span><span class="sxs-lookup"><span data-stu-id="d0d64-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="d0d64-106">In questo articolo illustra in dettaglio come toocreate una macchina virtuale con più schede di rete associata tooit e come le schede NIC tooadd o rimuovere da una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="d0d64-106">This article details how toocreate a VM with multiple NICs attached tooit and how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="d0d64-107">Per informazioni dettagliate, incluso come toocreate più schede di rete all'interno del proprio Bash script, altre informazioni sui [la distribuzione di macchine virtuali multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d0d64-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="d0d64-108">Le differenti [dimensioni della macchina virtuale](sizes.md) supportano un numero variabile di schede di rete, pertanto scegliere le dimensioni della macchina virtuale di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="d0d64-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="d0d64-109">In questo articolo illustra in dettaglio come toocreate una macchina virtuale con più schede di rete con hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="d0d64-109">This article details how toocreate a VM with multiple NICs with hello Azure CLI 2.0.</span></span> <span data-ttu-id="d0d64-110">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](multiple-nics-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d0d64-110">You can also perform these steps with hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="d0d64-111">Creare risorse di supporto</span><span class="sxs-lookup"><span data-stu-id="d0d64-111">Create supporting resources</span></span>
<span data-ttu-id="d0d64-112">Hello installazione più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d0d64-112">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="d0d64-113">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="d0d64-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d0d64-114">I nomi dei parametri di esempio includono *myResourceGroup*, *mystorageaccount* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="d0d64-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="d0d64-115">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d0d64-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d0d64-116">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="d0d64-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="d0d64-117">Creare una rete virtuale di hello con [creazione della rete virtuale di rete az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="d0d64-117">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="d0d64-118">esempio Hello crea una rete virtuale denominata *myVnet* e subnet denominata *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="d0d64-118">hello following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="d0d64-119">Creare una subnet per il traffico di back-end hello con [creare subnet della rete virtuale rete az](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="d0d64-119">Create a subnet for hello back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="d0d64-120">esempio Hello crea una subnet denominata *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="d0d64-120">hello following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="d0d64-121">Creare un gruppo di sicurezza di rete con il comando [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="d0d64-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="d0d64-122">esempio Hello crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="d0d64-122">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="d0d64-123">Creare e configurare più schede di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="d0d64-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="d0d64-124">Creare due schede di interfaccia di rete con il comando [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="d0d64-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="d0d64-125">esempio Hello crea due schede di rete, denominati *myNic1* e *myNic2*connesse, gruppo di sicurezza rete hello, con una scheda di rete che connettono tooeach subnet:</span><span class="sxs-lookup"><span data-stu-id="d0d64-125">hello following example creates two NICs, named *myNic1* and *myNic2*, connected hello network security group, with one NIC connecting tooeach subnet:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="d0d64-126">Creare una macchina virtuale e collegare le schede NIC hello</span><span class="sxs-lookup"><span data-stu-id="d0d64-126">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="d0d64-127">Quando si crea hello macchina virtuale, specificare le schede NIC hello creato con `--nics`.</span><span class="sxs-lookup"><span data-stu-id="d0d64-127">When you create hello VM, specify hello NICs you created with `--nics`.</span></span> <span data-ttu-id="d0d64-128">È necessario anche tootake attenzione quando si seleziona hello dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d0d64-128">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="d0d64-129">Vi sono limiti per il numero totale di schede di rete che è possibile aggiungere VM tooa hello.</span><span class="sxs-lookup"><span data-stu-id="d0d64-129">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="d0d64-130">Ulteriori informazioni sulle [dimensioni delle macchine virtuali di Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="d0d64-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="d0d64-131">Creare una VM con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="d0d64-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="d0d64-132">esempio Hello crea una macchina virtuale denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="d0d64-132">hello following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a><span data-ttu-id="d0d64-133">Aggiungere un tooa NIC VM</span><span class="sxs-lookup"><span data-stu-id="d0d64-133">Add a NIC tooa VM</span></span>
<span data-ttu-id="d0d64-134">passaggi precedenti Hello creato una macchina virtuale con più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="d0d64-134">hello previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="d0d64-135">È inoltre possibile aggiungere NIC tooan esistente VM con hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="d0d64-135">You can also add NICs tooan existing VM with hello Azure CLI 2.0.</span></span> 

<span data-ttu-id="d0d64-136">Creare un'altra scheda di interfaccia di rete con [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="d0d64-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="d0d64-137">esempio Hello crea una scheda di rete denominata *myNic3* connesso toohello subnet di back-end e il gruppo di sicurezza di rete creato nei passaggi precedenti hello:</span><span class="sxs-lookup"><span data-stu-id="d0d64-137">hello following example creates a NIC named *myNic3* connected toohello back-end subnet and network security group created in hello previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="d0d64-138">tooadd tooan una scheda di rete macchina virtuale esistente, prima di deallocare hello macchina virtuale con [az vm deallocare](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="d0d64-138">tooadd a NIC tooan existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="d0d64-139">esempio Hello dealloca hello macchina virtuale denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="d0d64-139">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d0d64-140">Aggiungere NIC con hello [scheda nic vm az aggiungere](/cli/azure/vm/nic#add).</span><span class="sxs-lookup"><span data-stu-id="d0d64-140">Add hello NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="d0d64-141">Hello esempio aggiunge *myNic3* troppo*myVM*:</span><span class="sxs-lookup"><span data-stu-id="d0d64-141">hello following example adds *myNic3* too*myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="d0d64-142">Avvia macchina virtuale con hello [inizio vm az](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="d0d64-142">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="d0d64-143">Rimuovere una scheda di interfaccia di rete da una VM</span><span class="sxs-lookup"><span data-stu-id="d0d64-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="d0d64-144">tooremove una scheda di rete da una macchina virtuale esistente, prima di deallocare hello VM con [az vm deallocare](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="d0d64-144">tooremove a NIC from an existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="d0d64-145">esempio Hello dealloca hello macchina virtuale denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="d0d64-145">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d0d64-146">Rimuovere hello NIC con [rimuovere la scheda nic vm az](/cli/azure/vm/nic#remove).</span><span class="sxs-lookup"><span data-stu-id="d0d64-146">Remove hello NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="d0d64-147">Hello esempio seguente viene rimosso *myNic3* da *myVM*:</span><span class="sxs-lookup"><span data-stu-id="d0d64-147">hello following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="d0d64-148">Avvia macchina virtuale con hello [inizio vm az](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="d0d64-148">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="d0d64-149">Creare più schede di interfaccia di rete usando i modelli di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d0d64-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="d0d64-150">Modelli di gestione risorse di Azure utilizzano dichiarativa JSON file toodefine l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="d0d64-150">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="d0d64-151">È possibile consultare una [panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d0d64-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="d0d64-152">Modelli di gestione risorse forniscono un modo toocreate più istanze di una risorsa durante la distribuzione, ad esempio la creazione di più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="d0d64-152">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="d0d64-153">Utilizzare *copia* numero hello toospecify di toocreate istanze:</span><span class="sxs-lookup"><span data-stu-id="d0d64-153">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="d0d64-154">Ulteriori informazioni sulla [creazione di più istanze utilizzando *Copia*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="d0d64-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="d0d64-155">È inoltre possibile utilizzare un `copyIndex()` toothen aggiungere un nome di risorsa tooa numero, che consente di toocreate `myNic1`, `myNic2`, e così via hello seguito è riportato un esempio di aggiunta di valore di indice hello:</span><span class="sxs-lookup"><span data-stu-id="d0d64-155">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="d0d64-156">È possibile consultare un esempio completo di [creazione di più schede di rete utilizzando i modelli di Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="d0d64-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0d64-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0d64-157">Next steps</span></span>
<span data-ttu-id="d0d64-158">Revisione [le dimensioni di VM Linux](sizes.md) durante il tentativo di toocreating una macchina virtuale con più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="d0d64-158">Review [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="d0d64-159">Prestare attenzione toohello massimo NIC supporta ogni dimensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d0d64-159">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 
