---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM Linux con il monitoraggio di OMS | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM Linux con il monitoraggio di OMS
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 31bfcc532a7d1ea418fb9a15ec882963d1913756
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="5fa1f-103">Monitorare una macchina virtuale con Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="5fa1f-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="5fa1f-104">Questo script consente di creare una macchina virtuale di Azure, installare l'agente Operations Management Suite (OMS) e registrare il sistema in un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="5fa1f-105">Dopo l'esecuzione dello script, la macchina virtuale sarà visibile nella console di OMS.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5fa1f-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5fa1f-106">Sample script</span></span>

<span data-ttu-id="5fa1f-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Creazione rapida della macchina virtuale")]</span><span class="sxs-lookup"><span data-stu-id="5fa1f-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5fa1f-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="5fa1f-108">Clean up deployment</span></span> 

<span data-ttu-id="5fa1f-109">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5fa1f-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="5fa1f-110">Script explanation</span></span>

<span data-ttu-id="5fa1f-111">Questo script usa i comandi seguenti per creare un gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="5fa1f-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5fa1f-113">Comando</span><span class="sxs-lookup"><span data-stu-id="5fa1f-113">Command</span></span> | <span data-ttu-id="5fa1f-114">Note</span><span class="sxs-lookup"><span data-stu-id="5fa1f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5fa1f-115">az group create</span><span class="sxs-lookup"><span data-stu-id="5fa1f-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5fa1f-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5fa1f-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="5fa1f-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="5fa1f-118">Consente di creare la macchina virtuale e la connette alla scheda di rete, alla rete virtuale, alla subnet e al gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="5fa1f-119">Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="5fa1f-120">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="5fa1f-120">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="5fa1f-121">Consente di eseguire un'estensione di VM in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-121">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="5fa1f-122">In questo caso, l'estensione dell'agente Operations Management Suite viene usata per installare l'agente OMS e registrare la VM in un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-122">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="5fa1f-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="5fa1f-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="5fa1f-124">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5fa1f-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5fa1f-125">Next steps</span></span>

<span data-ttu-id="5fa1f-126">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5fa1f-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5fa1f-127">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5fa1f-127">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
