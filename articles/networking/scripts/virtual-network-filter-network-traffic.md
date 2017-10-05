---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Filtrare il traffico di rete della VM | Documentazione Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Filtrare il traffico di rete della VM in ingresso e in uscita.
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: 68ee013cff4e0be15af30239e0314f779f50177a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="b93f5-103">Filtrare il traffico della VM in ingresso e in uscita</span><span class="sxs-lookup"><span data-stu-id="b93f5-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="b93f5-104">Questo script di esempio crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="b93f5-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="b93f5-105">Il traffico di rete in ingresso alla subnet front-end è limitato a HTTP, HTTPS e SSH, mentre il traffico in uscita verso Internet dalla subnet back-end non è consentito.</span><span class="sxs-lookup"><span data-stu-id="b93f5-105">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="b93f5-106">Dopo aver eseguito lo script sarà presente una macchina virtuale con due NIC.</span><span class="sxs-lookup"><span data-stu-id="b93f5-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="b93f5-107">Ogni NIC è collegata a una subnet diversa.</span><span class="sxs-lookup"><span data-stu-id="b93f5-107">Each NIC is connected to a different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b93f5-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="b93f5-108">Sample script</span></span>


<span data-ttu-id="b93f5-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filtrare il traffico di rete della VM")]</span><span class="sxs-lookup"><span data-stu-id="b93f5-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b93f5-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="b93f5-110">Clean up deployment</span></span> 

<span data-ttu-id="b93f5-111">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="b93f5-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="b93f5-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="b93f5-112">Script explanation</span></span>

<span data-ttu-id="b93f5-113">Questo script usa i comandi seguenti per creare un gruppo di risorse, una rete virtuale e i gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="b93f5-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="b93f5-114">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="b93f5-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="b93f5-115">Comando</span><span class="sxs-lookup"><span data-stu-id="b93f5-115">Command</span></span> | <span data-ttu-id="b93f5-116">Note</span><span class="sxs-lookup"><span data-stu-id="b93f5-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b93f5-117">az group create</span><span class="sxs-lookup"><span data-stu-id="b93f5-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="b93f5-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="b93f5-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b93f5-119">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="b93f5-119">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="b93f5-120">Consente di creare una rete virtuale e una subnet front-end di Azure.</span><span class="sxs-lookup"><span data-stu-id="b93f5-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="b93f5-121">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="b93f5-121">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="b93f5-122">Consente di creare una subnet back-end.</span><span class="sxs-lookup"><span data-stu-id="b93f5-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="b93f5-123">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="b93f5-123">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="b93f5-124">Consente di associare i gruppi di risorse di rete alla subnet.</span><span class="sxs-lookup"><span data-stu-id="b93f5-124">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="b93f5-125">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="b93f5-125">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="b93f5-126">Consente di creare un indirizzo IP pubblico per accedere alla VM da Internet.</span><span class="sxs-lookup"><span data-stu-id="b93f5-126">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="b93f5-127">az network nic create</span><span class="sxs-lookup"><span data-stu-id="b93f5-127">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="b93f5-128">Consente di creare interfacce di rete virtuale e di associarle alle subnet front-end e back-end della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b93f5-128">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="b93f5-129">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="b93f5-129">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="b93f5-130">Consente di creare gruppi di sicurezza di rete associati alle subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="b93f5-130">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="b93f5-131">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="b93f5-131">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="b93f5-132">Consente di creare regole del gruppo di sicurezza di rete che consentono o bloccano porte specifiche su subnet specifiche.</span><span class="sxs-lookup"><span data-stu-id="b93f5-132">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="b93f5-133">az vm create</span><span class="sxs-lookup"><span data-stu-id="b93f5-133">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="b93f5-134">Consente di creare macchine virtuali e associa una NIC a ogni VM.</span><span class="sxs-lookup"><span data-stu-id="b93f5-134">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="b93f5-135">Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="b93f5-135">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="b93f5-136">az group delete</span><span class="sxs-lookup"><span data-stu-id="b93f5-136">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="b93f5-137">Consente di eliminare un gruppo di risorse e tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="b93f5-137">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b93f5-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b93f5-138">Next steps</span></span>

<span data-ttu-id="b93f5-139">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b93f5-139">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="b93f5-140">Altri esempi di script dell'interfaccia della riga di comando per la rete sono disponibili nella documentazione sulla [Panoramica delle reti di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b93f5-140">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>