---
title: "Creare una VM Linux in Azure con più schede di interfaccia di rete | Documentazione Microsoft"
description: "Informazioni su come creare una VM Linux con più schede di interfaccia di rete collegate usando l'interfaccia della riga di comando di Azure 2.0 o i modelli di Resource Manager."
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
ms.openlocfilehash: 8a2931e462079c101c91497d459d7d3126234244
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="3e7b7-103">Come creare una macchina virtuale Linux in Azure con più schede di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="3e7b7-103">How to create a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="3e7b7-104">È possibile creare una macchina virtuale (VM) in Azure con più interfacce di rete virtuale (NIC) collegate.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="3e7b7-105">Uno scenario comune è quello di avere subnet diverse per la connettività front-end e back-end oppure una rete dedicata a una soluzione di monitoraggio o backup.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="3e7b7-106">Questo articolo illustra come creare una VM con più schede di interfaccia di rete collegate e come aggiungere o rimuovere le schede di interfaccia di rete da una VM esistente.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-106">This article details how to create a VM with multiple NICs attached to it and how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="3e7b7-107">Per informazioni dettagliate, incluse quelle sulla creazione di più schede di rete all'interno degli script di Bash, consultare la sezione dedicata alla [distribuzione di macchine virtuali con più schede di rete](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="3e7b7-108">Le differenti [dimensioni della macchina virtuale](sizes.md) supportano un numero variabile di schede di rete, pertanto scegliere le dimensioni della macchina virtuale di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="3e7b7-109">Questo articolo illustra come creare una macchina virtuale con più schede di interfaccia di rete usando l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-109">This article details how to create a VM with multiple NICs with the Azure CLI 2.0.</span></span> <span data-ttu-id="3e7b7-110">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](multiple-nics-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-110">You can also perform these steps with the [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="3e7b7-111">Creare risorse di supporto</span><span class="sxs-lookup"><span data-stu-id="3e7b7-111">Create supporting resources</span></span>
<span data-ttu-id="3e7b7-112">Installare la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e accedere a un account Azure tramite il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-112">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="3e7b7-113">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="3e7b7-114">I nomi dei parametri di esempio includono *myResourceGroup*, *mystorageaccount* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="3e7b7-115">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="3e7b7-116">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="3e7b7-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="3e7b7-117">Creare la rete virtuale con [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-117">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="3e7b7-118">L'esempio seguente crea una rete virtuale denominata *myVnet* e una subnet denominata *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="3e7b7-118">The following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="3e7b7-119">Creare una subnet per il traffico di back-end con il comando [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-119">Create a subnet for the back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="3e7b7-120">L'esempio seguente crea una subnet denominata *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="3e7b7-120">The following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="3e7b7-121">Creare un gruppo di sicurezza di rete con il comando [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="3e7b7-122">L'esempio seguente crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="3e7b7-122">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="3e7b7-123">Creare e configurare più schede di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="3e7b7-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="3e7b7-124">Creare due schede di interfaccia di rete con il comando [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="3e7b7-125">L'esempio seguente crea due schede di interfaccia di rete, denominate *myNic1* e *myNic2*, connesse al gruppo di sicurezza di rete, con una scheda che si connette a ogni subnet:</span><span class="sxs-lookup"><span data-stu-id="3e7b7-125">The following example creates two NICs, named *myNic1* and *myNic2*, connected the network security group, with one NIC connecting to each subnet:</span></span>

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

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="3e7b7-126">Creare una macchina virtuale e collegare le schede di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="3e7b7-126">Create a VM and attach the NICs</span></span>
<span data-ttu-id="3e7b7-127">Quando si crea la macchina virtuale, specificare le schede di interfaccia di rete create con `--nics`.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-127">When you create the VM, specify the NICs you created with `--nics`.</span></span> <span data-ttu-id="3e7b7-128">L'utente deve anche fare attenzione quando seleziona la dimensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-128">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="3e7b7-129">Esistono dei limiti per quanto riguarda il numero totale di schede di rete che è possibile aggiungere.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-129">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="3e7b7-130">Ulteriori informazioni sulle [dimensioni delle macchine virtuali di Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="3e7b7-131">Creare una macchina virtuale con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="3e7b7-132">L'esempio seguente crea una VM denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="3e7b7-132">The following example creates a VM named *myVM*:</span></span>

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

## <a name="add-a-nic-to-a-vm"></a><span data-ttu-id="3e7b7-133">Aggiungere una scheda di interfaccia di rete a una VM</span><span class="sxs-lookup"><span data-stu-id="3e7b7-133">Add a NIC to a VM</span></span>
<span data-ttu-id="3e7b7-134">I passaggi precedenti hanno consentito di creare una VM con più schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-134">The previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="3e7b7-135">È anche possibile aggiungere schede di interfaccia di rete a una VM esistente con l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-135">You can also add NICs to an existing VM with the Azure CLI 2.0.</span></span> 

<span data-ttu-id="3e7b7-136">Creare un'altra scheda di interfaccia di rete con [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="3e7b7-137">L'esempio seguente crea una scheda di interfaccia rete denominata *myNic3* connessa alla subnet back-end e al gruppo di sicurezza di rete creato nei passaggi precedenti:</span><span class="sxs-lookup"><span data-stu-id="3e7b7-137">The following example creates a NIC named *myNic3* connected to the back-end subnet and network security group created in the previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="3e7b7-138">Per aggiungere una scheda di interfaccia di rete a una VM esistente, deallocare prima di tutto la VM con [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-138">To add a NIC to an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="3e7b7-139">L'esempio seguente dealloca la VM denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="3e7b7-139">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="3e7b7-140">Aggiungere la scheda di interfaccia di rete con [az vm nic add](/cli/azure/vm/nic#add).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-140">Add the NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="3e7b7-141">L'esempio seguente aggiunge *myNic3* a *myVM*:</span><span class="sxs-lookup"><span data-stu-id="3e7b7-141">The following example adds *myNic3* to *myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="3e7b7-142">Avviare la VM con [az vm start](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="3e7b7-142">Start the VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="3e7b7-143">Rimuovere una scheda di interfaccia di rete da una VM</span><span class="sxs-lookup"><span data-stu-id="3e7b7-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="3e7b7-144">Per rimuovere una scheda di interfaccia di rete da una VM esistente, deallocare prima di tutto la VM con [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-144">To remove a NIC from an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="3e7b7-145">L'esempio seguente dealloca la VM denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="3e7b7-145">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="3e7b7-146">Rimuovere la scheda di interfaccia di rete con [az vm nic remove](/cli/azure/vm/nic#remove).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-146">Remove the NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="3e7b7-147">L'esempio seguente rimuove *myNic3* da *myVM*:</span><span class="sxs-lookup"><span data-stu-id="3e7b7-147">The following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="3e7b7-148">Avviare la VM con [az vm start](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="3e7b7-148">Start the VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="3e7b7-149">Creare più schede di interfaccia di rete usando i modelli di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3e7b7-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="3e7b7-150">I modelli di Azure Resource Manager utilizzano i file JSON dichiarativi per definire l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-150">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="3e7b7-151">È possibile consultare una [panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="3e7b7-152">I modelli di Resource Manager offrono un modo di creare più istanze di una risorsa durante la distribuzione, come ad esempio la creazione di più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-152">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="3e7b7-153">Utilizzare *Copia* per specificare il numero di istanze da creare:</span><span class="sxs-lookup"><span data-stu-id="3e7b7-153">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="3e7b7-154">Ulteriori informazioni sulla [creazione di più istanze utilizzando *Copia*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="3e7b7-155">È inoltre possibile utilizzare un `copyIndex()` per poi aggiungere un numero al nome di una risorsa, che consente di creare `myNic1`, `myNic2`, e così via. Di seguito viene riportato un esempio di aggiunta del valore di indice:</span><span class="sxs-lookup"><span data-stu-id="3e7b7-155">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="3e7b7-156">È possibile consultare un esempio completo di [creazione di più schede di rete utilizzando i modelli di Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e7b7-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3e7b7-157">Next steps</span></span>
<span data-ttu-id="3e7b7-158">Quando si cerca di creare una macchina virtuale con più schede di rete, consultare [Dimensioni per le macchine virtuali di Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="3e7b7-158">Review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="3e7b7-159">Prestare attenzione al numero massimo di schede di rete supportato per ogni dimensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3e7b7-159">Pay attention to the maximum number of NICs each VM size supports.</span></span> 