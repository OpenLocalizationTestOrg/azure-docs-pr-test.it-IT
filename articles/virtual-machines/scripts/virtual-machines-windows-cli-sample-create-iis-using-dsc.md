---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una macchina virtuale Windows Server 2016 con IIS usando DSC | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una macchina virtuale Windows Server 2016 con IIS usando DSC
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.custom: mvc
ms.openlocfilehash: 1f605c0260fcaea29851d76c90ba0b287bec5ae7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-iis-using-dsc"></a><span data-ttu-id="5c5b2-103">Creare una macchina virtuale con IIS usando DSC</span><span class="sxs-lookup"><span data-stu-id="5c5b2-103">Create a VM with IIS using DSC</span></span>

<span data-ttu-id="5c5b2-104">Questo script crea una macchina virtuale e usa l'estensione dello script personalizzato DSC di Macchina virtuale di Azure per installare e configurare IIS.</span><span class="sxs-lookup"><span data-stu-id="5c5b2-104">This script creates a virtual machine, and uses the Azure Virtual Machine DSC custom script extension to install and configure IIS.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5c5b2-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5c5b2-105">Sample script</span></span>

<span data-ttu-id="5c5b2-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Creazione rapida della macchina virtuale")]</span><span class="sxs-lookup"><span data-stu-id="5c5b2-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5c5b2-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="5c5b2-107">Clean up deployment</span></span> 

<span data-ttu-id="5c5b2-108">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="5c5b2-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="5c5b2-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="5c5b2-109">Script explanation</span></span>

<span data-ttu-id="5c5b2-110">Questo script usa i comandi seguenti per creare un gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="5c5b2-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="5c5b2-111">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="5c5b2-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5c5b2-112">Comando</span><span class="sxs-lookup"><span data-stu-id="5c5b2-112">Command</span></span> | <span data-ttu-id="5c5b2-113">Note</span><span class="sxs-lookup"><span data-stu-id="5c5b2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5c5b2-114">az group create</span><span class="sxs-lookup"><span data-stu-id="5c5b2-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5c5b2-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="5c5b2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5c5b2-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="5c5b2-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="5c5b2-117">Consente di creare la macchina virtuale e la connette alla scheda di rete, alla rete virtuale, alla subnet e al gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="5c5b2-117">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="5c5b2-118">Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="5c5b2-118">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="5c5b2-119">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="5c5b2-119">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="5c5b2-120">Consente di aggiungere l'estensione dello script personalizzato alla macchina virtuale che richiama uno script per installare IIS.</span><span class="sxs-lookup"><span data-stu-id="5c5b2-120">Add the Custom Script Extension to the virtual machine which invokes a script to install IIS.</span></span> |
| [<span data-ttu-id="5c5b2-121">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="5c5b2-121">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="5c5b2-122">Consente di creare una regola del gruppo di sicurezza di rete per consentire il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="5c5b2-122">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="5c5b2-123">In questo esempio, la porta 80 è aperta al traffico HTTP.</span><span class="sxs-lookup"><span data-stu-id="5c5b2-123">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="5c5b2-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="5c5b2-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="5c5b2-125">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="5c5b2-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5c5b2-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c5b2-126">Next steps</span></span>

<span data-ttu-id="5c5b2-127">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5c5b2-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5c5b2-128">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della macchina virtuale Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c5b2-128">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
