---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare rapidamente una VM Linux | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare rapidamente una VM Linux
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
ms.openlocfilehash: 3df3affcedf9edbe6e548d881a877f14204ec280
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine"></a><span data-ttu-id="38e1a-103">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="38e1a-103">Create a virtual machine</span></span>

<span data-ttu-id="38e1a-104">Questo script crea una macchina virtuale di Azure con sistema operativo Ubuntu e le relative risorse di rete.</span><span class="sxs-lookup"><span data-stu-id="38e1a-104">This script creates an Azure Virtual Machine with an Ubuntu operating system and related networking resources.</span></span> <span data-ttu-id="38e1a-105">Dopo aver eseguito lo script, è possibile accedere alla macchina virtuale tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="38e1a-105">After running the script, you can access the virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="38e1a-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="38e1a-106">Sample script</span></span>

<span data-ttu-id="38e1a-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "Creazione rapida della macchina virtuale")]</span><span class="sxs-lookup"><span data-stu-id="38e1a-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="38e1a-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="38e1a-108">Clean up deployment</span></span> 

<span data-ttu-id="38e1a-109">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="38e1a-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="38e1a-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="38e1a-110">Script explanation</span></span>

<span data-ttu-id="38e1a-111">Questo script usa i comandi seguenti per creare un gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="38e1a-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="38e1a-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="38e1a-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="38e1a-113">Comando</span><span class="sxs-lookup"><span data-stu-id="38e1a-113">Command</span></span> | <span data-ttu-id="38e1a-114">Note</span><span class="sxs-lookup"><span data-stu-id="38e1a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="38e1a-115">az group create</span><span class="sxs-lookup"><span data-stu-id="38e1a-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="38e1a-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="38e1a-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="38e1a-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="38e1a-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="38e1a-118">Consente di creare la macchina virtuale e la connette alla scheda di rete, alla rete virtuale, alla subnet e al gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="38e1a-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="38e1a-119">Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="38e1a-119">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="38e1a-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="38e1a-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="38e1a-121">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="38e1a-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="38e1a-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38e1a-122">Next steps</span></span>

<span data-ttu-id="38e1a-123">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="38e1a-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="38e1a-124">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="38e1a-124">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
