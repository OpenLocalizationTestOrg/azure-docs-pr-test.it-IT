---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare rapidamente una macchina virtuale Windows Server 2016 | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare rapidamente una macchina virtuale Windows Server 2016
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rickstercdn
ms.openlocfilehash: 084518bf7bc1d01c4a146efe3e0b7fe08149ce35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="quick-create-a-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="f95ba-103">Creare rapidamente una macchina virtuale con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f95ba-103">Quick Create a virtual machine with the Azure CLI</span></span>

<span data-ttu-id="f95ba-104">Questo script crea una macchina virtuale di Azure che esegue Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f95ba-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="f95ba-105">Dopo aver eseguito lo script, è possibile accedere alla macchina virtuale tramite una connessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="f95ba-105">After running the script, you can access the virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f95ba-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="f95ba-106">Sample script</span></span>

<span data-ttu-id="f95ba-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Creazione rapida della macchina virtuale")]</span><span class="sxs-lookup"><span data-stu-id="f95ba-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f95ba-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="f95ba-108">Clean up deployment</span></span> 

<span data-ttu-id="f95ba-109">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="f95ba-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="f95ba-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="f95ba-110">Script explanation</span></span>

<span data-ttu-id="f95ba-111">Questo script usa i comandi seguenti per creare un gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="f95ba-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="f95ba-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="f95ba-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f95ba-113">Comando</span><span class="sxs-lookup"><span data-stu-id="f95ba-113">Command</span></span> | <span data-ttu-id="f95ba-114">Note</span><span class="sxs-lookup"><span data-stu-id="f95ba-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f95ba-115">az group create</span><span class="sxs-lookup"><span data-stu-id="f95ba-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f95ba-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="f95ba-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f95ba-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="f95ba-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="f95ba-118">Consente di creare la macchina virtuale e la connette alla scheda di rete, alla rete virtuale, alla subnet e al gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="f95ba-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="f95ba-119">Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="f95ba-119">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="f95ba-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="f95ba-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f95ba-121">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="f95ba-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f95ba-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f95ba-122">Next steps</span></span>

<span data-ttu-id="f95ba-123">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f95ba-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f95ba-124">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della macchina virtuale Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f95ba-124">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
