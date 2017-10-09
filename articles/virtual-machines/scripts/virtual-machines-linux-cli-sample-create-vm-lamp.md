---
title: "aaaAzure CLI Script di esempio - distribuire hello Stack LAMP in un Set di scalabilità di Machin virtuale Load-Balanced | Documenti Microsoft"
description: "Utilizzare hello toodeploy estensione di uno script personalizzato Stack LAMP in un carico = scalabilità della macchina virtuale con bilanciamento impostato in Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="fe338-103">Distribuire stack LAMP hello in un set di scalabilità della macchina virtuale di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="fe338-103">Deploy hello LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="fe338-104">In questo esempio crea un set di scalabilità della macchina virtuale e si applica un'estensione che viene eseguito uno stack di luce hello toodeploy script personalizzato in ogni macchina virtuale nel set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="fe338-104">This example creates a virtual machine scale set and applies an extension that runs a custom script toodeploy hello LAMP stack on each virtual machine in hello scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="fe338-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="fe338-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a><span data-ttu-id="fe338-106">Connettere</span><span class="sxs-lookup"><span data-stu-id="fe338-106">Connect</span></span>

<span data-ttu-id="fe338-107">Utilizzare questo codice toosee come impostare tooconnect tooyour macchine virtuali e la scala.</span><span class="sxs-lookup"><span data-stu-id="fe338-107">Use this code toosee how tooconnect tooyour VMs and your scale set.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fe338-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="fe338-108">Clean up deployment</span></span> 

<span data-ttu-id="fe338-109">Eseguire hello seguente gruppo di risorse di comando tooremove hello, hello set di scalabilità e le macchine virtuali e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="fe338-109">Run hello following command tooremove hello resource group, hello scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fe338-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="fe338-110">Script explanation</span></span>

<span data-ttu-id="fe338-111">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, macchina virtuale, set di disponibilità, bilanciamento del carico e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="fe338-111">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="fe338-112">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="fe338-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fe338-113">Comando</span><span class="sxs-lookup"><span data-stu-id="fe338-113">Command</span></span> | <span data-ttu-id="fe338-114">Note</span><span class="sxs-lookup"><span data-stu-id="fe338-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fe338-115">az group create</span><span class="sxs-lookup"><span data-stu-id="fe338-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fe338-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="fe338-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fe338-117">az vmss create</span><span class="sxs-lookup"><span data-stu-id="fe338-117">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="fe338-118">Consente di creare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="fe338-118">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="fe338-119">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="fe338-119">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="fe338-120">Consente di aggiungere un endpoint con carico bilanciato</span><span class="sxs-lookup"><span data-stu-id="fe338-120">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="fe338-121">az vmss extension set</span><span class="sxs-lookup"><span data-stu-id="fe338-121">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="fe338-122">Creare l'estensione hello che esegue uno script personalizzato hello sulla distribuzione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fe338-122">Create hello extension that runs hello custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="fe338-123">az vmss update-instances</span><span class="sxs-lookup"><span data-stu-id="fe338-123">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="fe338-124">Eseguire uno script personalizzato hello nelle istanze VM hello che sono state distribuite prima dell'applicazione di estensione hello toohello set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="fe338-124">Run hello custom script on hello VM instances that were deployed before hello extension was applied toohello scale set.</span></span> |
| [<span data-ttu-id="fe338-125">az vmss scale</span><span class="sxs-lookup"><span data-stu-id="fe338-125">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="fe338-126">La scalabilità verticale hello scala impostata tramite l'aggiunta di più istanze di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fe338-126">Scale up hello scale set by adding more VM instances.</span></span> <span data-ttu-id="fe338-127">script personalizzato Hello viene eseguito su questi quando vengono distribuiti.</span><span class="sxs-lookup"><span data-stu-id="fe338-127">hello custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="fe338-128">az network public-ip list</span><span class="sxs-lookup"><span data-stu-id="fe338-128">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="fe338-129">Ottenere gli indirizzi IP di hello di macchine virtuali create da esempio hello hello.</span><span class="sxs-lookup"><span data-stu-id="fe338-129">Get hello IP addresses of hello VMs created by hello sample.</span></span> |
| [<span data-ttu-id="fe338-130">az network lb show</span><span class="sxs-lookup"><span data-stu-id="fe338-130">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="fe338-131">Porte utilizzate dal servizio di bilanciamento del carico hello ottenere back-end e front-end hello.</span><span class="sxs-lookup"><span data-stu-id="fe338-131">Get hello frontend and backend ports used by hello load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fe338-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fe338-132">Next steps</span></span>

<span data-ttu-id="fe338-133">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fe338-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fe338-134">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe338-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
