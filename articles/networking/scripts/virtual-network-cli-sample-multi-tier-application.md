---
title: 'script CLI aaaAzure di esempio: creare una rete per applicazioni multilivello | Documenti Microsoft'
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
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="bac5e-103">Creare una rete per applicazioni multilivello</span><span class="sxs-lookup"><span data-stu-id="bac5e-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="bac5e-104">Questo script di esempio crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="bac5e-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="bac5e-105">Subnet con traffico toohello front-end è limitato tooHTTP e SSH, mentre il traffico toohello subnet back-end è limitato tooMySQL, porta 3306.</span><span class="sxs-lookup"><span data-stu-id="bac5e-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="bac5e-106">Dopo l'esecuzione dello script hello, si avrà a disposizione due macchine virtuali, una in ogni subnet che è possibile distribuire server web e software MySQL.</span><span class="sxs-lookup"><span data-stu-id="bac5e-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="bac5e-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="bac5e-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="bac5e-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="bac5e-108">Clean up deployment</span></span> 

<span data-ttu-id="bac5e-109">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="bac5e-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="bac5e-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="bac5e-110">Script explanation</span></span>

<span data-ttu-id="bac5e-111">Questo script utilizza hello toocreate i comandi seguenti a un gruppo di risorse, rete virtuale e gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="bac5e-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="bac5e-112">Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.</span><span class="sxs-lookup"><span data-stu-id="bac5e-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="bac5e-113">Comando</span><span class="sxs-lookup"><span data-stu-id="bac5e-113">Command</span></span> | <span data-ttu-id="bac5e-114">Note</span><span class="sxs-lookup"><span data-stu-id="bac5e-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bac5e-115">az group create</span><span class="sxs-lookup"><span data-stu-id="bac5e-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="bac5e-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="bac5e-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bac5e-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="bac5e-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="bac5e-118">Consente di creare una rete virtuale e una subnet front-end di Azure.</span><span class="sxs-lookup"><span data-stu-id="bac5e-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="bac5e-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="bac5e-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="bac5e-120">Consente di creare una subnet back-end.</span><span class="sxs-lookup"><span data-stu-id="bac5e-120">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="bac5e-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="bac5e-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="bac5e-122">Crea un hello VM tooaccess indirizzo pubblico di IP da Internet hello.</span><span class="sxs-lookup"><span data-stu-id="bac5e-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="bac5e-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="bac5e-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="bac5e-124">Consente di creare interfacce di rete virtuale e lo connette le subnet front-end e back-end della rete virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="bac5e-124">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="bac5e-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="bac5e-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="bac5e-126">Crea gruppi di sicurezza di rete (gruppo) che sono subnet front-end e back-end di toohello associato.</span><span class="sxs-lookup"><span data-stu-id="bac5e-126">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="bac5e-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="bac5e-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="bac5e-128">Crea regole del gruppo che consentono o Blocca subnet toospecific porte specifiche.</span><span class="sxs-lookup"><span data-stu-id="bac5e-128">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="bac5e-129">az vm create</span><span class="sxs-lookup"><span data-stu-id="bac5e-129">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="bac5e-130">Crea le macchine virtuali e la collega tooeach una scheda di rete VM.</span><span class="sxs-lookup"><span data-stu-id="bac5e-130">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="bac5e-131">Questo comando specifica inoltre toouse immagine di macchina virtuale hello e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="bac5e-131">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="bac5e-132">az group delete</span><span class="sxs-lookup"><span data-stu-id="bac5e-132">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="bac5e-133">Consente di eliminare un gruppo di risorse e tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="bac5e-133">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bac5e-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bac5e-134">Next steps</span></span>

<span data-ttu-id="bac5e-135">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bac5e-135">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="bac5e-136">Ulteriori esempi di script CLI rete sono reperibili hello [documentazione Cenni preliminari sulle reti di Azure](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="bac5e-136">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
