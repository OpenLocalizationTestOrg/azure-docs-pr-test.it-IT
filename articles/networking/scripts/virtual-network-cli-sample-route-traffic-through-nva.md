---
title: esempio di script CLI aaaAzure - instradare il traffico attraverso un dispositivo di rete virtuale | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Instradare il traffico attraverso un'appliance virtuale di rete.
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
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="6e31c-103">Instradare il traffico attraverso un'appliance virtuale di rete</span><span class="sxs-lookup"><span data-stu-id="6e31c-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="6e31c-104">Questo script di esempio crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="6e31c-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="6e31c-105">Viene inoltre creata una macchina virtuale con IP inoltro del traffico tra due subnet hello tooroute abilitato.</span><span class="sxs-lookup"><span data-stu-id="6e31c-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="6e31c-106">Dopo l'esecuzione di script hello è possibile distribuire il software di rete, ad esempio un'applicazione di firewall, toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e31c-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="6e31c-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="6e31c-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6e31c-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="6e31c-108">Clean up deployment</span></span> 

<span data-ttu-id="6e31c-109">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="6e31c-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="6e31c-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="6e31c-110">Script explanation</span></span>

<span data-ttu-id="6e31c-111">Questo script utilizza hello toocreate i comandi seguenti a un gruppo di risorse, rete virtuale e gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="6e31c-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="6e31c-112">Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.</span><span class="sxs-lookup"><span data-stu-id="6e31c-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="6e31c-113">Comando</span><span class="sxs-lookup"><span data-stu-id="6e31c-113">Command</span></span> | <span data-ttu-id="6e31c-114">Note</span><span class="sxs-lookup"><span data-stu-id="6e31c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6e31c-115">az group create</span><span class="sxs-lookup"><span data-stu-id="6e31c-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="6e31c-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="6e31c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6e31c-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="6e31c-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="6e31c-118">Consente di creare una rete virtuale e una subnet front-end di Azure.</span><span class="sxs-lookup"><span data-stu-id="6e31c-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="6e31c-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="6e31c-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="6e31c-120">Consente di creare le subnet back-end e di rete perimetrale.</span><span class="sxs-lookup"><span data-stu-id="6e31c-120">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="6e31c-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="6e31c-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="6e31c-122">Crea un hello VM tooaccess indirizzo pubblico di IP da Internet hello.</span><span class="sxs-lookup"><span data-stu-id="6e31c-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="6e31c-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="6e31c-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="6e31c-124">Consente di creare un'interfaccia di rete virtuale e attiva l'inoltro IP.</span><span class="sxs-lookup"><span data-stu-id="6e31c-124">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="6e31c-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="6e31c-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="6e31c-126">Consente di creare un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="6e31c-126">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="6e31c-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="6e31c-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="6e31c-128">Crea regole del gruppo che consentono le porte HTTP e HTTPS in ingresso toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e31c-128">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="6e31c-129">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="6e31c-129">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="6e31c-130">Associa hello NSGs e toosubnets nelle tabelle di route.</span><span class="sxs-lookup"><span data-stu-id="6e31c-130">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="6e31c-131">az network route-table create</span><span class="sxs-lookup"><span data-stu-id="6e31c-131">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="6e31c-132">Consente di creare una tabella di route per tutte le route.</span><span class="sxs-lookup"><span data-stu-id="6e31c-132">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="6e31c-133">az network route-table route create</span><span class="sxs-lookup"><span data-stu-id="6e31c-133">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="6e31c-134">Crea route tooroute il traffico tra subnet e hello Internet tramite hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e31c-134">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="6e31c-135">az vm create</span><span class="sxs-lookup"><span data-stu-id="6e31c-135">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="6e31c-136">Crea una macchina virtuale e collega tooit NIC hello.</span><span class="sxs-lookup"><span data-stu-id="6e31c-136">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="6e31c-137">Questo comando specifica inoltre toouse immagine di macchina virtuale hello e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="6e31c-137">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="6e31c-138">az group delete</span><span class="sxs-lookup"><span data-stu-id="6e31c-138">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="6e31c-139">Consente di eliminare un gruppo di risorse e tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="6e31c-139">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6e31c-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6e31c-140">Next steps</span></span>

<span data-ttu-id="6e31c-141">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6e31c-141">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="6e31c-142">Ulteriori esempi di script CLI rete sono reperibili hello [documentazione Cenni preliminari sulle reti di Azure](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="6e31c-142">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
