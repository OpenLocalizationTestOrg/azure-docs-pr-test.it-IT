---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una rete per applicazioni multilivello | Documentazione Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una rete virtuale per applicazioni multilivello
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
ms.openlocfilehash: de65d820f2d9eea49b58185c81d815675fd76740
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="7598a-103">Creare una rete per applicazioni multilivello</span><span class="sxs-lookup"><span data-stu-id="7598a-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="7598a-104">Questo script di esempio crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="7598a-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="7598a-105">Il traffico verso la subnet front-end è limitato a HTTP e SSH, mentre il traffico verso la subnet back-end è limitato a MySQL sulla porta 3306.</span><span class="sxs-lookup"><span data-stu-id="7598a-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="7598a-106">Dopo aver eseguito lo script saranno presenti due macchine virtuali, una in ogni subnet in cui è possibile distribuire server Web e software MySQL.</span><span class="sxs-lookup"><span data-stu-id="7598a-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="7598a-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="7598a-107">Sample script</span></span>


<span data-ttu-id="7598a-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Rete virtuale per applicazioni multilivello")]</span><span class="sxs-lookup"><span data-stu-id="7598a-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="7598a-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="7598a-109">Clean up deployment</span></span> 

<span data-ttu-id="7598a-110">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="7598a-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="7598a-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="7598a-111">Script explanation</span></span>

<span data-ttu-id="7598a-112">Questo script usa i comandi seguenti per creare un gruppo di risorse, una rete virtuale e i gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="7598a-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="7598a-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="7598a-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="7598a-114">Comando</span><span class="sxs-lookup"><span data-stu-id="7598a-114">Command</span></span> | <span data-ttu-id="7598a-115">Note</span><span class="sxs-lookup"><span data-stu-id="7598a-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7598a-116">az group create</span><span class="sxs-lookup"><span data-stu-id="7598a-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="7598a-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="7598a-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7598a-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="7598a-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="7598a-119">Consente di creare una rete virtuale e una subnet front-end di Azure.</span><span class="sxs-lookup"><span data-stu-id="7598a-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="7598a-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="7598a-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="7598a-121">Consente di creare una subnet back-end.</span><span class="sxs-lookup"><span data-stu-id="7598a-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="7598a-122">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="7598a-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="7598a-123">Consente di creare un indirizzo IP pubblico per accedere alla VM da Internet.</span><span class="sxs-lookup"><span data-stu-id="7598a-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="7598a-124">az network nic create</span><span class="sxs-lookup"><span data-stu-id="7598a-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="7598a-125">Consente di creare interfacce di rete virtuale e di associarle alle subnet front-end e back-end della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="7598a-125">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="7598a-126">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="7598a-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="7598a-127">Consente di creare gruppi di sicurezza di rete associati alle subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="7598a-127">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="7598a-128">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="7598a-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="7598a-129">Consente di creare regole del gruppo di sicurezza di rete che consentono o bloccano porte specifiche su subnet specifiche.</span><span class="sxs-lookup"><span data-stu-id="7598a-129">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="7598a-130">az vm create</span><span class="sxs-lookup"><span data-stu-id="7598a-130">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="7598a-131">Consente di creare macchine virtuali e associa una NIC a ogni VM.</span><span class="sxs-lookup"><span data-stu-id="7598a-131">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="7598a-132">Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="7598a-132">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="7598a-133">az group delete</span><span class="sxs-lookup"><span data-stu-id="7598a-133">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="7598a-134">Consente di eliminare un gruppo di risorse e tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="7598a-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7598a-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7598a-135">Next steps</span></span>

<span data-ttu-id="7598a-136">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7598a-136">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="7598a-137">Altri esempi di script dell'interfaccia della riga di comando per la rete sono disponibili nella documentazione sulla [Panoramica delle reti di Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7598a-137">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>