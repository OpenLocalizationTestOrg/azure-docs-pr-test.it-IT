---
title: Distribuire macchine virtuali Linux in una rete esistente con l'interfaccia della riga di comando Azure 2.0 | Microsoft Docs
description: Informazioni su come distribuire una macchina virtuale Linux in una rete virtuale esistente dall'interfaccia della riga di comando di Azure 2.0
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
ms.openlocfilehash: 932fd74ec83f43b604382346ee2c273f5453fcd0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli"></a><span data-ttu-id="8a469-103">Come distribuire una macchina virtuale Linux in una rete virtuale Azure esistente con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="8a469-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI</span></span>

<span data-ttu-id="8a469-104">Questo articolo illustra come usare l'interfaccia della riga di comando di Azure 2.0 per distribuire una macchina virtuale in una rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="8a469-104">This article shows you how to use the Azure CLI 2.0 to deploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="8a469-105">I requisiti sono:</span><span class="sxs-lookup"><span data-stu-id="8a469-105">The requirements are:</span></span>

- [<span data-ttu-id="8a469-106">Un account di Azure</span><span class="sxs-lookup"><span data-stu-id="8a469-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="8a469-107">File di chiavi SSH pubbliche e private</span><span class="sxs-lookup"><span data-stu-id="8a469-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

<span data-ttu-id="8a469-108">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8a469-108">You can also perform these steps with the [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="8a469-109">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="8a469-109">Quick Commands</span></span>
<span data-ttu-id="8a469-110">Se si vuole eseguire rapidamente l'attività, la sezione seguente indica in dettaglio i comandi necessari.</span><span class="sxs-lookup"><span data-stu-id="8a469-110">If you need to quickly accomplish the task, the following section details the  commands needed.</span></span> <span data-ttu-id="8a469-111">Altre informazioni dettagliate e il contesto per ogni passaggio sono disponibili nelle sezioni successive del documento, [a partire da qui](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="8a469-111">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="8a469-112">Per creare questo ambiente personalizzato, è necessario installare la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e connetterla a un account Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8a469-112">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="8a469-113">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="8a469-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8a469-114">I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="8a469-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="8a469-115">**Pre-requisiti:** gruppo di risorse di Azure, rete virtuale e subnet, gruppo di sicurezza di rete con SSH in ingresso e una scheda di interfaccia di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8a469-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="8a469-116">Distribuire la macchina virtuale nell'infrastruttura di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="8a469-116">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="8a469-117">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="8a469-117">Detailed walkthrough</span></span>

<span data-ttu-id="8a469-118">Gli asset di Azure, come le reti virtuali e i gruppi di sicurezza di rete devono essere risorse statiche, ovvero di lunga durata e distribuite raramente.</span><span class="sxs-lookup"><span data-stu-id="8a469-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="8a469-119">Dopo essere stata distribuita, una rete virtuale può essere usata in nuove distribuzioni senza alcun effetto negativo sull'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="8a469-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="8a469-120">Si pensi a una rete virtuale come se fosse analoga a uno switch di rete hardware tradizionale, il quale non richiede una nuova configurazione a ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8a469-120">Think about a virtual network as being a traditional hardware network switch - you would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="8a469-121">In una rete virtuale configurata in modo appropriato, è possibile continuare a distribuire nuovi server nella rete virtuale più volte, apportando solo le modifiche indispensabili durante il ciclo di vita della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8a469-121">With a correctly configured virtual network, you can continue to deploy new VMs into that virtual network over and over with few, if any, changes required over the life of the virtual network.</span></span>

<span data-ttu-id="8a469-122">Per creare questo ambiente personalizzato, è necessario installare la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e connetterla a un account Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8a469-122">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="8a469-123">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="8a469-123">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8a469-124">I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="8a469-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="8a469-125">Creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8a469-125">Create the resource group</span></span>

<span data-ttu-id="8a469-126">Prima creare un gruppo di risorse di Azure per organizzare tutti gli elementi che si creano durante questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="8a469-126">First, create an Azure resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="8a469-127">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a469-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="8a469-128">Creare il gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8a469-128">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8a469-129">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="8a469-129">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-the-virtual-network"></a><span data-ttu-id="8a469-130">Creare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="8a469-130">Create the virtual network</span></span>

<span data-ttu-id="8a469-131">Viene create una rete virtuale di Azure nella quale avviare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8a469-131">Lets build an Azure virtual network to launch the VMs into.</span></span> <span data-ttu-id="8a469-132">Per altre informazioni sulle reti virtuali, vedere [Creare una rete virtuale usando l'interfaccia della riga di comando di Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8a469-132">For more information on virtual networks, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="8a469-133">Creare la rete virtuale con [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="8a469-133">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="8a469-134">L'esempio seguente crea una rete virtuale denominata *myVnet* e una subnet denominata *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="8a469-134">The following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="8a469-135">Creare il gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="8a469-135">Create the network security group</span></span>

<span data-ttu-id="8a469-136">I gruppi di sicurezza di rete di Azure sono analoghi a un firewall a livello di rete.</span><span class="sxs-lookup"><span data-stu-id="8a469-136">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="8a469-137">Per altre informazioni sui gruppi di sicurezza di rete, vedere [Come creare gruppi di sicurezza di rete usando l'interfaccia della riga di comando di Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8a469-137">For more information on network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="8a469-138">Creare il gruppo di sicurezza di rete con [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="8a469-138">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="8a469-139">L'esempio seguente crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8a469-139">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="8a469-140">Aggiungere una regola di assenso SSH in ingresso</span><span class="sxs-lookup"><span data-stu-id="8a469-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="8a469-141">La macchina virtuale deve accedere da Internet, pertanto è necessaria una regola che consenta di lasciare entrare il traffico in ingresso verso la porta 22 della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8a469-141">The VM needs access from the internet, so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span> <span data-ttu-id="8a469-142">Aggiungere una regole in ingresso per il gruppo di sicurezza di rete con [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="8a469-142">Add an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="8a469-143">L'esempio seguente crea una regola denominata *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="8a469-143">The following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-the-subnet-to-the-network-security-group"></a><span data-ttu-id="8a469-144">Collegare la subnet al gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="8a469-144">Attach the subnet to the network security group</span></span>

<span data-ttu-id="8a469-145">È possibile applicare le regole del gruppo di sicurezza di rete a una subnet o a una specifica interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="8a469-145">The network security group rules can be applied to a subnet or a specific virtual network interface.</span></span> <span data-ttu-id="8a469-146">Collegare quindi il gruppo di sicurezza di rete alla subnet.</span><span class="sxs-lookup"><span data-stu-id="8a469-146">Lets attach the network security group to our subnet.</span></span> <span data-ttu-id="8a469-147">Collegare la subnet al gruppo di sicurezza di rete con [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span><span class="sxs-lookup"><span data-stu-id="8a469-147">Attach your subnet to the network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-to-the-subnet"></a><span data-ttu-id="8a469-148">Aggiungere una scheda di interfaccia di rete virtuale alla subnet</span><span class="sxs-lookup"><span data-stu-id="8a469-148">Add a virtual network interface card to the subnet</span></span>

<span data-ttu-id="8a469-149">Le schede di interfaccia di rete virtuale sono importanti in quanto è possibile riusarle connettendole a macchine virtuali differenti.</span><span class="sxs-lookup"><span data-stu-id="8a469-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="8a469-150">In questo modo la scheda di interfaccia di rete virtuale diventa una risorsa statica, mentre le macchine virtuali possono essere temporanee.</span><span class="sxs-lookup"><span data-stu-id="8a469-150">This reuse allows you to keep the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="8a469-151">Creare una scheda di interfaccia di rete virtuale e associarla alla subnet con [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="8a469-151">Create a VNic and associate it with the subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="8a469-152">L'esempio seguente crea una scheda di interfaccia di rete virtuale denominata *myNic*:</span><span class="sxs-lookup"><span data-stu-id="8a469-152">The following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="8a469-153">Distribuire la macchina virtuale nell'infrastruttura di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="8a469-153">Deploy the VM into the virtual network infrastructure</span></span>

<span data-ttu-id="8a469-154">A questo punto sono disponibili una rete virtuale e un gruppo di sicurezza di rete che protegge la subnet bloccando tutto il traffico in ingresso tranne quello verso la porta 22 per SSH.</span><span class="sxs-lookup"><span data-stu-id="8a469-154">You now have a virtual network and subnet, and a network security group to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="8a469-155">È ora possibile distribuire la macchina virtuale all'interno di questa infrastruttura di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="8a469-155">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="8a469-156">Creare la macchina virtuale con [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="8a469-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="8a469-157">Per altre informazioni sui flag da usare con l'interfaccia della riga di comando di Azure 2.0 per distribuire una macchina virtuale completa, vedere [Creare un ambiente Linux completo usando l'interfaccia della riga di comando di Azure](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="8a469-157">For more information on the flags to use with the Azure CLI 2.0 to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="8a469-158">Nell'esempio seguente viene creata una VM usando Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="8a469-158">The following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="8a469-159">Questi dischi vengono gestiti dalla piattaforma Azure e non richiedono alcuna pianificazione o alcuna posizione per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8a469-159">These disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="8a469-160">Per altre informazioni sui dischi gestiti, vedere [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md) (Panoramica di Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="8a469-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="8a469-161">Se si desidera usare dischi non gestiti, vedere la nota aggiuntiva seguente.</span><span class="sxs-lookup"><span data-stu-id="8a469-161">If you wish to use unmanaged disks, see the additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="8a469-162">Se si usa Managed Disks, ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="8a469-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="8a469-163">Se si desidera usare dischi non gestiti, è necessario aggiungere i parametri aggiuntivi seguenti al comando della procedura per creare dischi non gestiti nell'account di archiviazione denominato `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="8a469-163">If you wish to use unmanaged disks, you need to add the following additional parameters to the proceeding command to create unmanaged disks in the storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="8a469-164">Usando i flag dell'interfaccia della riga di comando per chiamare le risorse esistenti, si indica ad Azure di distribuire la macchina virtuale all'interno della rete esistente.</span><span class="sxs-lookup"><span data-stu-id="8a469-164">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="8a469-165">Una volta distribuite la rete virtuale e la subnet possono essere usate come risorse statiche o permanenti nell'area di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a469-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="8a469-166">In questo esempio non si è creato e assegnato un indirizzo IP pubblico alla scheda di interfaccia di rete virtuale, pertanto questa macchina virtuale non è accessibile pubblicamente da Internet.</span><span class="sxs-lookup"><span data-stu-id="8a469-166">In this example, you did not create and assign a public IP address to the VNic, so this VM is not publicly accessible over the Internet.</span></span> <span data-ttu-id="8a469-167">Per altre informazioni, vedere [Creare una macchina virtuale con un IP pubblico statico usando l'interfaccia della riga di comando di Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8a469-167">For more information, see [Create a VM with a static public IP using the Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a469-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a469-168">Next steps</span></span>
<span data-ttu-id="8a469-169">Per altre informazioni sulle modalità per creare macchine virtuali in Azure, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a469-169">For more information about ways to create virtual machines in Azure, see the following resources:</span></span>

* [<span data-ttu-id="8a469-170">Usare un modello di Azure Resource Manager per creare una distribuzione specifica</span><span class="sxs-lookup"><span data-stu-id="8a469-170">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="8a469-171">Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="8a469-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="8a469-172">Creare una VM Linux in Azure usando i modelli</span><span class="sxs-lookup"><span data-stu-id="8a469-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
