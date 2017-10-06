---
title: esempio di script CLI aaaAzure - il traffico di rete VM filtro | Documenti Microsoft
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
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="071c0-103">Filtrare il traffico della VM in ingresso e in uscita</span><span class="sxs-lookup"><span data-stu-id="071c0-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="071c0-104">Questo script di esempio crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="071c0-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="071c0-105">Il traffico di rete in ingresso subnet front-end toohello è limitato tooHTTP, toohello Internet dalla subnet di back-end hello non è consentito il traffico HTTPS e SSH, mentre in uscita.</span><span class="sxs-lookup"><span data-stu-id="071c0-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="071c0-106">Dopo l'esecuzione di script hello, si disporrà di una macchina virtuale con due schede di rete.</span><span class="sxs-lookup"><span data-stu-id="071c0-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="071c0-107">Ogni scheda è connessa tooa diverse subnet.</span><span class="sxs-lookup"><span data-stu-id="071c0-107">Each NIC is connected tooa different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="071c0-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="071c0-108">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="071c0-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="071c0-109">Clean up deployment</span></span> 

<span data-ttu-id="071c0-110">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="071c0-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="071c0-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="071c0-111">Script explanation</span></span>

<span data-ttu-id="071c0-112">Questo script utilizza hello toocreate i comandi seguenti a un gruppo di risorse, rete virtuale e gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="071c0-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="071c0-113">Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.</span><span class="sxs-lookup"><span data-stu-id="071c0-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="071c0-114">Comando</span><span class="sxs-lookup"><span data-stu-id="071c0-114">Command</span></span> | <span data-ttu-id="071c0-115">Note</span><span class="sxs-lookup"><span data-stu-id="071c0-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="071c0-116">az group create</span><span class="sxs-lookup"><span data-stu-id="071c0-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="071c0-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="071c0-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="071c0-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="071c0-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="071c0-119">Consente di creare una rete virtuale e una subnet front-end di Azure.</span><span class="sxs-lookup"><span data-stu-id="071c0-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="071c0-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="071c0-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="071c0-121">Consente di creare una subnet back-end.</span><span class="sxs-lookup"><span data-stu-id="071c0-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="071c0-122">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="071c0-122">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="071c0-123">Associa NSGs toosubnets.</span><span class="sxs-lookup"><span data-stu-id="071c0-123">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="071c0-124">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="071c0-124">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="071c0-125">Crea un hello VM tooaccess indirizzo pubblico di IP da Internet hello.</span><span class="sxs-lookup"><span data-stu-id="071c0-125">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="071c0-126">az network nic create</span><span class="sxs-lookup"><span data-stu-id="071c0-126">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="071c0-127">Consente di creare interfacce di rete virtuale e lo connette le subnet front-end e back-end della rete virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="071c0-127">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="071c0-128">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="071c0-128">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="071c0-129">Crea gruppi di sicurezza di rete (gruppo) che sono subnet front-end e back-end di toohello associato.</span><span class="sxs-lookup"><span data-stu-id="071c0-129">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="071c0-130">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="071c0-130">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="071c0-131">Crea regole del gruppo che consentono o Blocca subnet toospecific porte specifiche.</span><span class="sxs-lookup"><span data-stu-id="071c0-131">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="071c0-132">az vm create</span><span class="sxs-lookup"><span data-stu-id="071c0-132">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="071c0-133">Crea le macchine virtuali e la collega tooeach una scheda di rete VM.</span><span class="sxs-lookup"><span data-stu-id="071c0-133">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="071c0-134">Questo comando specifica inoltre toouse immagine di macchina virtuale hello e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="071c0-134">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="071c0-135">az group delete</span><span class="sxs-lookup"><span data-stu-id="071c0-135">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="071c0-136">Consente di eliminare un gruppo di risorse e tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="071c0-136">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="071c0-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="071c0-137">Next steps</span></span>

<span data-ttu-id="071c0-138">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="071c0-138">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="071c0-139">Ulteriori esempi di script CLI rete sono reperibili hello [documentazione Cenni preliminari sulle reti di Azure](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="071c0-139">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
