---
title: Script dell'interfaccia della riga di comando Azure di esempio - Creare due macchine virtuali con NSG interno ed esterno | Microsoft Docs
description: Script dell'interfaccia della riga di comando Azure di esempio - Creare due macchine virtuali con NSG interno ed esterno
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: cc80e3fc5aaa12200e9a441db9d4a9c613c0548a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="a6ec7-103">Proteggere il traffico di rete tra le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="a6ec7-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="a6ec7-104">Questo script crea due macchine virtuali e protegge il traffico in ingresso su entrambe le macchine.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-104">This script creates two virtual machines and secures incoming traffic to both.</span></span> <span data-ttu-id="a6ec7-105">Una macchina virtuale è accessibile su Internet e dispone di un gruppo di sicurezza di rete (NSG) configurato per consentire il traffico sulle porte 3389 e 80.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-105">One virtual machine is accessible on the internet and has a network security group (NSG) configured to allow traffic on port 3389 and port 80.</span></span> <span data-ttu-id="a6ec7-106">La seconda macchina virtuale non è accessibile su Internet e dispone di un NSG configurato per consentire solo il traffico proveniente dalla prima macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-106">The second virtual machine is not accessible on the internet, and has an NSG configured to only allow traffic from the first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a6ec7-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="a6ec7-107">Sample script</span></span>

<span data-ttu-id="a6ec7-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "Creare una macchina virtuale con NSG")]</span><span class="sxs-lookup"><span data-stu-id="a6ec7-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "Create VM with NSG")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a6ec7-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="a6ec7-109">Clean up deployment</span></span> 

<span data-ttu-id="a6ec7-110">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="a6ec7-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="a6ec7-111">Script explanation</span></span>

<span data-ttu-id="a6ec7-112">Questo script usa i comandi seguenti per creare un gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="a6ec7-113">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a6ec7-114">Comando</span><span class="sxs-lookup"><span data-stu-id="a6ec7-114">Command</span></span> | <span data-ttu-id="a6ec7-115">Note</span><span class="sxs-lookup"><span data-stu-id="a6ec7-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a6ec7-116">az group create</span><span class="sxs-lookup"><span data-stu-id="a6ec7-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a6ec7-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a6ec7-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="a6ec7-118">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="a6ec7-119">Consente di creare una rete virtuale e una subnet di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="a6ec7-120">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="a6ec7-120">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="a6ec7-121">Consente di creare una subnet.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-121">Creates a subnet.</span></span> |
| [<span data-ttu-id="a6ec7-122">az vm create</span><span class="sxs-lookup"><span data-stu-id="a6ec7-122">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="a6ec7-123">Consente di creare la macchina virtuale e la connette alla scheda di rete, alla rete virtuale, alla subnet e al gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-123">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="a6ec7-124">Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-124">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="a6ec7-125">az network nsg rule update</span><span class="sxs-lookup"><span data-stu-id="a6ec7-125">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="a6ec7-126">Consente di aggiornare una regola NSG.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-126">Updates an NSG rule.</span></span> <span data-ttu-id="a6ec7-127">In questo esempio la regola di back-end viene aggiornata affinché il traffico passi solo attraverso la subnet front-end.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-127">In this sample, the back-end rule is updated to pass through traffic only from the front-end subnet.</span></span> |
| [<span data-ttu-id="a6ec7-128">az network nsg rule list</span><span class="sxs-lookup"><span data-stu-id="a6ec7-128">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="a6ec7-129">Restituisce informazioni sulla regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-129">Returns information about a network security group rule.</span></span> <span data-ttu-id="a6ec7-130">In questo esempio, il nome della regola è archiviato in una variabile da usare successivamente nello script.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-130">In this sample, the rule name is stored in a variable for use later in the script.</span></span> |
| [<span data-ttu-id="a6ec7-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="a6ec7-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="a6ec7-132">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="a6ec7-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a6ec7-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6ec7-133">Next steps</span></span>

<span data-ttu-id="a6ec7-134">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a6ec7-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a6ec7-135">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della macchina virtuale Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6ec7-135">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
