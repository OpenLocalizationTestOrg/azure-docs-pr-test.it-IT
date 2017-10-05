---
title: "Creare una VM Linux in Azure con più schede di interfaccia di rete | Documentazione Microsoft"
description: "Informazioni su come creare una VM Linux con più schede di interfaccia di rete collegate utilizzando l'interfaccia della riga di comando di Azure o i modelli di Resource Manager."
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
ms.openlocfilehash: 814825cce61909167a1247a96c17a3ee9c5f2af4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="9be43-103">Creare una macchina virtuale Linux con più schede di interfaccia di rete usando l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9be43-103">Create a Linux virtual machine with multiple NICs using the Azure CLI 1.0</span></span>
<span data-ttu-id="9be43-104">È possibile creare una macchina virtuale (VM) in Azure con più interfacce di rete virtuale (NIC) collegate.</span><span class="sxs-lookup"><span data-stu-id="9be43-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="9be43-105">Uno scenario comune è quello di avere subnet diverse per la connettività front-end e back-end oppure una rete dedicata a una soluzione di monitoraggio o backup.</span><span class="sxs-lookup"><span data-stu-id="9be43-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="9be43-106">In questo articolo vengono presentati i comandi rapidi per creare una macchina virtuale con più schede di rete collegate.</span><span class="sxs-lookup"><span data-stu-id="9be43-106">This article provides quick commands to create a VM with multiple NICs attached to it.</span></span> <span data-ttu-id="9be43-107">Per informazioni dettagliate, incluse quelle sulla creazione di più schede di rete all'interno degli script di Bash, consultare la sezione dedicata alla [distribuzione di macchine virtuali con più schede di rete](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9be43-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="9be43-108">Le differenti [dimensioni della macchina virtuale](sizes.md) supportano un numero variabile di schede di rete, pertanto scegliere le dimensioni della macchina virtuale di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="9be43-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="9be43-109">È necessario collegare più schede di interfaccia di rete quando si crea una VM, perché non è possibile aggiungere le schede a una VM esistente con l'interfaccia della riga di comando di Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="9be43-109">You must attach multiple NICs when you create a VM - you cannot add NICs to an existing VM with the Azure CLI 1.0.</span></span> <span data-ttu-id="9be43-110">È possibile [aggiungere schede di interfaccia di rete a una VM esistente con l'interfaccia della riga di comando di Azure 2.0](multiple-nics.md).</span><span class="sxs-lookup"><span data-stu-id="9be43-110">You can [add NICs to an existing VM with the Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="9be43-111">È anche possibile [creare una VM basata sui dischi virtuali originali](copy-vm.md) e creare più schede di interfaccia di rete quando si distribuisce la VM.</span><span class="sxs-lookup"><span data-stu-id="9be43-111">You can also [create a VM based on the original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy the VM.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="9be43-112">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="9be43-112">CLI versions to complete the task</span></span>
<span data-ttu-id="9be43-113">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="9be43-113">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="9be43-114">[Interfaccia della riga di comando di Azure 1.0](#create-supporting-resources): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="9be43-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="9be43-115">[Interfaccia della riga di comando di Azure 2.0](multiple-nics.md): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="9be43-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="9be43-116">Creare risorse di supporto</span><span class="sxs-lookup"><span data-stu-id="9be43-116">Create supporting resources</span></span>
<span data-ttu-id="9be43-117">Controllare di aver effettuato l'accesso tramite l'[interfaccia della riga di comando di Azure](../../cli-install-nodejs.md) in modalità Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="9be43-117">Make sure that you have the [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="9be43-118">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="9be43-118">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="9be43-119">I nomi dei parametri di esempio includono *myResourceGroup*, *mystorageaccount* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="9be43-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="9be43-120">Creare prima un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="9be43-120">First, create a resource group.</span></span> <span data-ttu-id="9be43-121">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="9be43-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="9be43-122">Creare un account di archiviazione in cui salvare le VM.</span><span class="sxs-lookup"><span data-stu-id="9be43-122">Create a storage account to hold your VMs.</span></span> <span data-ttu-id="9be43-123">L'esempio seguente crea un account di archiviazione denominato *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="9be43-123">The following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="9be43-124">Creare una rete virtuale alla quale connettere le VM.</span><span class="sxs-lookup"><span data-stu-id="9be43-124">Create a virtual network to connect your VMs to.</span></span> <span data-ttu-id="9be43-125">L'esempio seguente crea una rete virtuale denominata *myVnet* con prefisso dell'indirizzo *192.168.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="9be43-125">The following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="9be43-126">Creare due subnet per la rete virtuale: una per il traffico front-end e l'altra per il traffico di back-end.</span><span class="sxs-lookup"><span data-stu-id="9be43-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="9be43-127">L'esempio seguente crea due subnet denominate *mySubnetFrontEnd* e *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="9be43-127">The following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

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

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="9be43-128">Creare e configurare più schede di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="9be43-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="9be43-129">È possibile leggere ulteriori informazioni sulla [distribuzione di più schede di rete tramite l'interfaccia della riga di comando di Azure](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), incluso lo script del processo di ciclo per creare tutte le schede NIC.</span><span class="sxs-lookup"><span data-stu-id="9be43-129">You can read more details about [deploying multiple NICs using the Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting the process of looping through to create all the NICs.</span></span>

<span data-ttu-id="9be43-130">L'esempio seguente crea due schede di interfaccia di rete, denominate *myNic1* e *myNic2*, con una scheda che si connette a ogni subnet:</span><span class="sxs-lookup"><span data-stu-id="9be43-130">The following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting to each subnet:</span></span>

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

<span data-ttu-id="9be43-131">In genere è necessario creare anche un [gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md) o un [servizio di bilanciamento del carico](../../load-balancer/load-balancer-overview.md) per gestire e distribuire il traffico tra le VM.</span><span class="sxs-lookup"><span data-stu-id="9be43-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="9be43-132">L'esempio seguente crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="9be43-132">The following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="9be43-133">Associare le due schede di interfaccia di rete al gruppo di sicurezza di rete usando `azure network nic set`.</span><span class="sxs-lookup"><span data-stu-id="9be43-133">Bind your NICs to the Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="9be43-134">L'esempio seguente associa *myNic1* e *myNic2* a *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="9be43-134">The following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

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

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="9be43-135">Creare una macchina virtuale e collegare le schede di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="9be43-135">Create a VM and attach the NICs</span></span>
<span data-ttu-id="9be43-136">In fase di creazione della macchina virtuale, è ora possibile specificare più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="9be43-136">When creating the VM, you now specify multiple NICs.</span></span> <span data-ttu-id="9be43-137">Anziché utilizzare `--nic-name` per fornire una singola scheda di rete, si utilizza `--nic-names` per fornire un elenco delimitato da virgole di schede di rete.</span><span class="sxs-lookup"><span data-stu-id="9be43-137">Rather using `--nic-name` to provide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="9be43-138">L'utente deve anche fare attenzione quando seleziona la dimensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9be43-138">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="9be43-139">Esistono dei limiti per quanto riguarda il numero totale di schede di rete che è possibile aggiungere.</span><span class="sxs-lookup"><span data-stu-id="9be43-139">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="9be43-140">Ulteriori informazioni sulle [dimensioni delle macchine virtuali di Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="9be43-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="9be43-141">L'esempio seguente mostra come specificare più schede di interfaccia di rete e quindi una dimensione di VM che supporta l'uso di più schede di interfaccia di rete (*Standard_DS2_v2*):</span><span class="sxs-lookup"><span data-stu-id="9be43-141">The following example shows how to specify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

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

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="9be43-142">Creare più schede di interfaccia di rete usando i modelli di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9be43-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="9be43-143">I modelli di Azure Resource Manager utilizzano i file JSON dichiarativi per definire l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="9be43-143">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="9be43-144">È possibile consultare una [panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9be43-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="9be43-145">I modelli di Resource Manager offrono un modo di creare più istanze di una risorsa durante la distribuzione, come ad esempio la creazione di più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="9be43-145">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="9be43-146">Utilizzare *Copia* per specificare il numero di istanze da creare:</span><span class="sxs-lookup"><span data-stu-id="9be43-146">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="9be43-147">Ulteriori informazioni sulla [creazione di più istanze utilizzando *Copia*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="9be43-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="9be43-148">È inoltre possibile utilizzare un `copyIndex()` per poi aggiungere un numero al nome di una risorsa, che consente di creare `myNic1`, `myNic2`, e così via. Di seguito viene riportato un esempio di aggiunta del valore di indice:</span><span class="sxs-lookup"><span data-stu-id="9be43-148">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="9be43-149">È possibile consultare un esempio completo di [creazione di più schede di rete utilizzando i modelli di Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="9be43-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9be43-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9be43-150">Next steps</span></span>
<span data-ttu-id="9be43-151">Assicurarsi di consultare [Dimensioni delle macchine virtuali di Linux](sizes.md) durante il tentativo di creazione di una macchina virtuale con più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="9be43-151">Make sure to review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="9be43-152">Prestare attenzione al numero massimo di schede di rete supportato per ogni dimensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9be43-152">Pay attention to the maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="9be43-153">Tenere presente che non è possibile aggiungere altre schede di rete a una macchina virtuale esistente. È necessario creare tutte le schede di rete quando si distribuisce la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9be43-153">Remember that you cannot add additional NICs to an existing VM, you must create all the NICs when you deploy the VM.</span></span> <span data-ttu-id="9be43-154">Prestare attenzione quando si pianificano le distribuzioni per assicurarsi di avere la connettività di rete necessaria fin dall'inizio.</span><span class="sxs-lookup"><span data-stu-id="9be43-154">Take care when planning your deployments to make sure that you have all the required network connectivity from the outset.</span></span>

