---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM Linux | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM Linux
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
ms.openlocfilehash: dc7e7276bcea32c59c67a42dedaffcedfd0cf907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="08b5c-103">Creare una macchina virtuale completamente configurata</span><span class="sxs-lookup"><span data-stu-id="08b5c-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="08b5c-104">Questo script crea una macchina virtuale di Azure con un sistema operativo Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="08b5c-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="08b5c-105">Dopo aver eseguito lo script, è possibile accedere alla macchina virtuale tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="08b5c-105">After running the script, you can access the virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="08b5c-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="08b5c-106">Sample script</span></span>

<span data-ttu-id="08b5c-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Creazione rapida della macchina virtuale")]</span><span class="sxs-lookup"><span data-stu-id="08b5c-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="08b5c-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="08b5c-108">Clean up deployment</span></span> 

<span data-ttu-id="08b5c-109">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="08b5c-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="08b5c-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="08b5c-110">Script explanation</span></span>

<span data-ttu-id="08b5c-111">Questo script usa i comandi seguenti per creare un gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="08b5c-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="08b5c-112">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="08b5c-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="08b5c-113">Comando</span><span class="sxs-lookup"><span data-stu-id="08b5c-113">Command</span></span> | <span data-ttu-id="08b5c-114">Note</span><span class="sxs-lookup"><span data-stu-id="08b5c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="08b5c-115">az group create</span><span class="sxs-lookup"><span data-stu-id="08b5c-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="08b5c-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="08b5c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="08b5c-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="08b5c-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="08b5c-118">Consente di creare una rete virtuale e una subnet di Azure.</span><span class="sxs-lookup"><span data-stu-id="08b5c-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="08b5c-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="08b5c-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="08b5c-120">Consente di creare un indirizzo IP pubblico con un indirizzo IP statico e un nome DNS associato.</span><span class="sxs-lookup"><span data-stu-id="08b5c-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="08b5c-121">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="08b5c-121">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="08b5c-122">Consente di creare un gruppo di sicurezza di rete, ovvero un confine di sicurezza tra Internet e la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="08b5c-122">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="08b5c-123">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="08b5c-123">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="08b5c-124">Consente di creare una regola NSG per consentire il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="08b5c-124">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="08b5c-125">In questo esempio, la porta 22 è aperta al traffico SSH.</span><span class="sxs-lookup"><span data-stu-id="08b5c-125">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="08b5c-126">az network nic create</span><span class="sxs-lookup"><span data-stu-id="08b5c-126">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="08b5c-127">Consente di creare una scheda di rete virtuale e la collega alla rete virtuale, alla subnet e al gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="08b5c-127">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="08b5c-128">az vm create</span><span class="sxs-lookup"><span data-stu-id="08b5c-128">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="08b5c-129">Consente di creare la macchina virtuale e la connette alla scheda di rete, alla rete virtuale, alla subnet e al gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="08b5c-129">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="08b5c-130">Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="08b5c-130">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="08b5c-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="08b5c-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="08b5c-132">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="08b5c-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="08b5c-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08b5c-133">Next steps</span></span>

<span data-ttu-id="08b5c-134">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="08b5c-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="08b5c-135">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08b5c-135">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
