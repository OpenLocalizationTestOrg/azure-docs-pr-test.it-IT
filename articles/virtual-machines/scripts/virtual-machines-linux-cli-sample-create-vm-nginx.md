---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM Linux con NGINX | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una VM Linux con NGINX
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 416624d9e378d09f4fb0593119dbc30adeb09f91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="398ff-103">Creare una VM con NGINX</span><span class="sxs-lookup"><span data-stu-id="398ff-103">Create a VM with NGINX</span></span>

<span data-ttu-id="398ff-104">Questo script crea una macchina virtuale di Azure e quindi usa l'estensione dello script personalizzato della macchina virtuale di Azure per installare NGINX.</span><span class="sxs-lookup"><span data-stu-id="398ff-104">This script creates an Azure Virtual Machine and uses the Azure Virtual Machine Custom Script Extension to install NGINX.</span></span> <span data-ttu-id="398ff-105">Dopo aver eseguito lo script, è possibile accedere a un sito Web demo sull'indirizzo IP pubblico della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="398ff-105">After running the script, you can access a demo website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="398ff-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="398ff-106">Sample script</span></span>

<span data-ttu-id="398ff-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Creazione rapida della macchina virtuale")]</span><span class="sxs-lookup"><span data-stu-id="398ff-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]</span></span>

## <a name="custom-script-extension"></a><span data-ttu-id="398ff-108">Estensione di script personalizzati</span><span class="sxs-lookup"><span data-stu-id="398ff-108">Custom Script Extension</span></span>

<span data-ttu-id="398ff-109">Questa estensione di script personalizzata copia questo script nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="398ff-109">The custom script extension copies this script onto the virtual machine.</span></span> <span data-ttu-id="398ff-110">Lo script viene quindi eseguito per installare e configurare un server web NGINX.</span><span class="sxs-lookup"><span data-stu-id="398ff-110">The script is then run to install and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="398ff-111">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="398ff-111">Clean up deployment</span></span> 

<span data-ttu-id="398ff-112">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="398ff-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="398ff-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="398ff-113">Script explanation</span></span>

<span data-ttu-id="398ff-114">Questo script usa i comandi seguenti per creare un gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="398ff-114">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="398ff-115">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="398ff-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="398ff-116">Comando</span><span class="sxs-lookup"><span data-stu-id="398ff-116">Command</span></span> | <span data-ttu-id="398ff-117">Note</span><span class="sxs-lookup"><span data-stu-id="398ff-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="398ff-118">az group create</span><span class="sxs-lookup"><span data-stu-id="398ff-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="398ff-119">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="398ff-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="398ff-120">az vm create</span><span class="sxs-lookup"><span data-stu-id="398ff-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="398ff-121">Creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="398ff-121">Creates the virtual machine.</span></span> <span data-ttu-id="398ff-122">Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="398ff-122">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="398ff-123">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="398ff-123">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="398ff-124">Consente di creare una regola del gruppo di sicurezza di rete per consentire il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="398ff-124">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="398ff-125">In questo esempio, la porta 80 è aperta al traffico HTTP.</span><span class="sxs-lookup"><span data-stu-id="398ff-125">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="398ff-126">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="398ff-126">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="398ff-127">Consente di aggiungere ed eseguire un'estensione di macchina virtuale in una VM.</span><span class="sxs-lookup"><span data-stu-id="398ff-127">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="398ff-128">In questo esempio, l'estensione dello script personalizzato viene usata per installare NGINX.</span><span class="sxs-lookup"><span data-stu-id="398ff-128">In this sample, the custom script extension is used to install NGINX.</span></span>|
| [<span data-ttu-id="398ff-129">az group delete</span><span class="sxs-lookup"><span data-stu-id="398ff-129">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="398ff-130">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="398ff-130">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="398ff-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="398ff-131">Next steps</span></span>

<span data-ttu-id="398ff-132">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="398ff-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="398ff-133">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="398ff-133">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
