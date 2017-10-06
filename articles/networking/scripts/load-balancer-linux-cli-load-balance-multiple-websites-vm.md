---
title: "bilanciamento del carico aaaAzure CLI Script di esempio - più siti Web con hello CLI di Azure | Documenti Microsoft"
description: "Esempio di Script di Azure CLI - più siti Web toohello il bilanciamento del carico stessa macchina virtuale"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="5fb43-103">Eseguire il bilanciamento del carico per più siti Web</span><span class="sxs-lookup"><span data-stu-id="5fb43-103">Load balance multiple websites</span></span>

<span data-ttu-id="5fb43-104">Questo esempio di script crea una rete virtuale con due macchine virtuali che fanno parte di un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="5fb43-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="5fb43-105">Un servizio di bilanciamento del carico indirizza il traffico di due macchine virtuali toohello due indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="5fb43-105">A load balancer directs traffic for two separate IP addresses toohello two VMs.</span></span> <span data-ttu-id="5fb43-106">Dopo l'esecuzione dello script hello, è possibile distribuire toohello software tramite server web le macchine virtuali e ospitare più siti web, ciascuno con il proprio indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="5fb43-106">After running hello script, you could deploy web server software toohello VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5fb43-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5fb43-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5fb43-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="5fb43-108">Clean up deployment</span></span> 

<span data-ttu-id="5fb43-109">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="5fb43-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="5fb43-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="5fb43-110">Script explanation</span></span>

<span data-ttu-id="5fb43-111">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, la rete virtuale, bilanciamento del carico e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="5fb43-111">This script uses hello following commands toocreate a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="5fb43-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="5fb43-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5fb43-113">Comando</span><span class="sxs-lookup"><span data-stu-id="5fb43-113">Command</span></span> | <span data-ttu-id="5fb43-114">Note</span><span class="sxs-lookup"><span data-stu-id="5fb43-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5fb43-115">az group create</span><span class="sxs-lookup"><span data-stu-id="5fb43-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5fb43-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="5fb43-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5fb43-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="5fb43-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="5fb43-118">Consente di creare una rete virtuale e una subnet di Azure.</span><span class="sxs-lookup"><span data-stu-id="5fb43-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="5fb43-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="5fb43-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="5fb43-120">Consente di creare un indirizzo IP pubblico con un indirizzo IP statico e un nome DNS associato.</span><span class="sxs-lookup"><span data-stu-id="5fb43-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="5fb43-121">az network lb create</span><span class="sxs-lookup"><span data-stu-id="5fb43-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="5fb43-122">Crea un servizio di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="5fb43-122">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="5fb43-123">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="5fb43-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="5fb43-124">Crea un probe di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="5fb43-124">Creates a load balancer probe.</span></span> <span data-ttu-id="5fb43-125">Un probe di bilanciamento del carico è toomonitor usato ogni macchina virtuale nel set di bilanciamento carico di hello.</span><span class="sxs-lookup"><span data-stu-id="5fb43-125">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="5fb43-126">Se qualsiasi macchina virtuale non è accessibile, il traffico non è indirizzato toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5fb43-126">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="5fb43-127">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="5fb43-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="5fb43-128">Crea una regola di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="5fb43-128">Creates a load balancer rule.</span></span> <span data-ttu-id="5fb43-129">In questo esempio viene creata una regola per la porta 80.</span><span class="sxs-lookup"><span data-stu-id="5fb43-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="5fb43-130">Come il traffico HTTP arriva al servizio di bilanciamento del carico hello, è indirizzato tooport 80 una delle macchine virtuali di hello nel set di bilanciamento carico di hello.</span><span class="sxs-lookup"><span data-stu-id="5fb43-130">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello load balancer set.</span></span> |
| [<span data-ttu-id="5fb43-131">az network lb frontend-ip create</span><span class="sxs-lookup"><span data-stu-id="5fb43-131">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="5fb43-132">Creare un indirizzo IP di front-end per hello bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="5fb43-132">Create a frontend IP address for hello Load Balancer.</span></span> |
| [<span data-ttu-id="5fb43-133">az network lb address-pool create</span><span class="sxs-lookup"><span data-stu-id="5fb43-133">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="5fb43-134">Crea un pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="5fb43-134">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="5fb43-135">az network nic create</span><span class="sxs-lookup"><span data-stu-id="5fb43-135">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="5fb43-136">Crea una scheda di rete virtuale e la collega toohello di rete virtuale e la subnet.</span><span class="sxs-lookup"><span data-stu-id="5fb43-136">Creates a virtual network card and attaches it toohello virtual network, and subnet.</span></span> |
| [<span data-ttu-id="5fb43-137">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="5fb43-137">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="5fb43-138">Consente di creare un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="5fb43-138">Creates an availability set.</span></span> <span data-ttu-id="5fb43-139">Set di disponibilità la distribuzione di macchine virtuali hello tra risorse fisiche in modo che se si verifica l'errore, non è stato eseguito alcun set intero di hello assicurare la disponibilità dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5fb43-139">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="5fb43-140">az network nic ip-config create</span><span class="sxs-lookup"><span data-stu-id="5fb43-140">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="5fb43-141">Crea una configurazione IP.</span><span class="sxs-lookup"><span data-stu-id="5fb43-141">Creates an IP confiuration.</span></span> <span data-ttu-id="5fb43-142">È necessario disporre di funzionalità Microsoft.Network/AllowMultipleIpConfigurationsPerNic hello abilitata per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5fb43-142">You must have hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="5fb43-143">Solo una configurazione può essere definita come configurazione IP primaria hello per ogni scheda di rete, utilizzando hello - flag di creazione primario.</span><span class="sxs-lookup"><span data-stu-id="5fb43-143">Only one configuration may be designated as hello primary IP configuration per NIC, using hello --make-primary flag.</span></span> |
| [<span data-ttu-id="5fb43-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="5fb43-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="5fb43-145">Crea macchina virtuale hello e lo connette la scheda di rete toohello, rete virtuale, subnet e gruppo.</span><span class="sxs-lookup"><span data-stu-id="5fb43-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="5fb43-146">Questo comando specifica inoltre toobe immagine di macchina virtuale hello usato e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="5fb43-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="5fb43-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="5fb43-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="5fb43-148">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="5fb43-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5fb43-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5fb43-149">Next steps</span></span>

<span data-ttu-id="5fb43-150">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5fb43-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5fb43-151">Ulteriori esempi di script CLI rete sono reperibili hello [documentazione Cenni preliminari sulle reti di Azure](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5fb43-151">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
