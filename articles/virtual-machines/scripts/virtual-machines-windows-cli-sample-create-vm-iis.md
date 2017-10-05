---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Installare IIS | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Installare IIS
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/28/2017
ms.author: nepeters
ms.openlocfilehash: 426418c01b23845372443af5b8f4e826fb321f7d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="quick-create-a-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="e5522-103">Creare rapidamente una macchina virtuale con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e5522-103">Quick Create a virtual machine with the Azure CLI</span></span>

<span data-ttu-id="e5522-104">Questo script crea una macchina virtuale di Azure con Windows Server 2016 e usa l'estensione dello script personalizzato di Macchina virtuale di Azure per installare IIS.</span><span class="sxs-lookup"><span data-stu-id="e5522-104">This script creates an Azure Virtual Machine running Windows Server 2016, and uses the Azure Virtual Machine Custom Script Extension to install IIS.</span></span> <span data-ttu-id="e5522-105">Dopo l'esecuzione dello script, è possibile accedere al sito Web IIS predefinito tramite l'indirizzo IP pubblico della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e5522-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e5522-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="e5522-106">Sample script</span></span>

<span data-ttu-id="e5522-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "Creazione rapida della macchina virtuale")]</span><span class="sxs-lookup"><span data-stu-id="e5522-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="e5522-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="e5522-108">Clean up deployment</span></span> 

<span data-ttu-id="e5522-109">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="e5522-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="e5522-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="e5522-110">Script explanation</span></span>

<span data-ttu-id="e5522-111">Questo script usa i comandi seguenti per creare un gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="e5522-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="e5522-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="e5522-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e5522-113">Comando</span><span class="sxs-lookup"><span data-stu-id="e5522-113">Command</span></span> | <span data-ttu-id="e5522-114">Note</span><span class="sxs-lookup"><span data-stu-id="e5522-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e5522-115">az group create</span><span class="sxs-lookup"><span data-stu-id="e5522-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e5522-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="e5522-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e5522-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="e5522-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="e5522-118">Consente di creare la macchina virtuale e la connette alla scheda di rete, alla rete virtuale, alla subnet e al gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="e5522-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="e5522-119">Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="e5522-119">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="e5522-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="e5522-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="e5522-121">Consente di creare una regola del gruppo di sicurezza di rete per consentire il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="e5522-121">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="e5522-122">In questo esempio, la porta 80 è aperta al traffico HTTP.</span><span class="sxs-lookup"><span data-stu-id="e5522-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="e5522-123">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="e5522-123">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e5522-124">Consente di aggiungere ed eseguire un'estensione di macchina virtuale in una VM.</span><span class="sxs-lookup"><span data-stu-id="e5522-124">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="e5522-125">In questo esempio, l'estensione dello script personalizzato è usata per installare IIS.</span><span class="sxs-lookup"><span data-stu-id="e5522-125">In this sample, the custom script extension is used to install IIS.</span></span>|
| [<span data-ttu-id="e5522-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="e5522-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e5522-127">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="e5522-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e5522-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e5522-128">Next steps</span></span>

<span data-ttu-id="e5522-129">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e5522-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e5522-130">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della macchina virtuale Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5522-130">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
