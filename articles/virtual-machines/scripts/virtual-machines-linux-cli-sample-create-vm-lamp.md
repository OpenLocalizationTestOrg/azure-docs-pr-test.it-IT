---
title: "Esempio di script dell'interfaccia della riga di comando di Azure: distribuire lo stack LAMP in un set di scalabilità di macchine virtuali con carico bilanciato | Microsoft Docs"
description: "Usare un'estensione di script personalizzato per distribuire lo stack LAMP in un set di scalabilità di macchine virtuali con carico bilanciato in Azure."
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
ms.openlocfilehash: 4007e8c85c0ff24bf5030881eac666582714eae3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="b4a49-103">Distribuire lo stack LAMP in un set di scalabilità di macchine virtuali con carico bilanciato</span><span class="sxs-lookup"><span data-stu-id="b4a49-103">Deploy the LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="b4a49-104">Questo esempio crea un set di scalabilità di macchine virtuali e applica un'estensione che esegue uno script personalizzato per distribuire lo stack LAMP in ogni macchina virtuale del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b4a49-104">This example creates a virtual machine scale set and applies an extension that runs a custom script to deploy the LAMP stack on each virtual machine in the scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="b4a49-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="b4a49-105">Sample script</span></span>

<span data-ttu-id="b4a49-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Creare set di scalabilità di macchine virtuali con lo stack LAMP")]</span><span class="sxs-lookup"><span data-stu-id="b4a49-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]</span></span>

## <a name="connect"></a><span data-ttu-id="b4a49-107">Connettere</span><span class="sxs-lookup"><span data-stu-id="b4a49-107">Connect</span></span>

<span data-ttu-id="b4a49-108">Usare questo codice per vedere come connettersi alle macchine virtuali e al set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b4a49-108">Use this code to see how to connect to your VMs and your scale set.</span></span>

<span data-ttu-id="b4a49-109">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Accedere al set di scalabilità di macchine virtuali")]</span><span class="sxs-lookup"><span data-stu-id="b4a49-109">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access the virtual machine scale set")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b4a49-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="b4a49-110">Clean up deployment</span></span> 

<span data-ttu-id="b4a49-111">Eseguire il comando seguente per rimuovere il gruppo di risorse, il set di scalabilità, le macchine virtuali e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="b4a49-111">Run the following command to remove the resource group, the scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b4a49-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="b4a49-112">Script explanation</span></span>

<span data-ttu-id="b4a49-113">Questo script usa i comandi seguenti per creare un gruppo di risorse, la macchina virtuale, il set di disponibilità, il bilanciamento del carico e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="b4a49-113">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="b4a49-114">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="b4a49-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b4a49-115">Comando</span><span class="sxs-lookup"><span data-stu-id="b4a49-115">Command</span></span> | <span data-ttu-id="b4a49-116">Note</span><span class="sxs-lookup"><span data-stu-id="b4a49-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b4a49-117">az group create</span><span class="sxs-lookup"><span data-stu-id="b4a49-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b4a49-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="b4a49-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b4a49-119">az vmss create</span><span class="sxs-lookup"><span data-stu-id="b4a49-119">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="b4a49-120">Consente di creare un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="b4a49-120">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="b4a49-121">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="b4a49-121">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="b4a49-122">Consente di aggiungere un endpoint con carico bilanciato</span><span class="sxs-lookup"><span data-stu-id="b4a49-122">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="b4a49-123">az vmss extension set</span><span class="sxs-lookup"><span data-stu-id="b4a49-123">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="b4a49-124">Consente di creare l'estensione che esegue lo script personalizzato sulla distribuzione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b4a49-124">Create the extension that runs the custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="b4a49-125">az vmss update-instances</span><span class="sxs-lookup"><span data-stu-id="b4a49-125">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="b4a49-126">Consente di eseguire lo script personalizzato nelle istanze di macchine virtuali che sono state distribuite prima che l'estensione sia stata applicata al set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b4a49-126">Run the custom script on the VM instances that were deployed before the extension was applied to the scale set.</span></span> |
| [<span data-ttu-id="b4a49-127">az vmss scale</span><span class="sxs-lookup"><span data-stu-id="b4a49-127">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="b4a49-128">Consente di aumentare il set di scalabilità mediante l'aggiunta di più istanze di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="b4a49-128">Scale up the scale set by adding more VM instances.</span></span> <span data-ttu-id="b4a49-129">Lo script personalizzato viene eseguito su queste quando vengono distribuite.</span><span class="sxs-lookup"><span data-stu-id="b4a49-129">The custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="b4a49-130">az network public-ip list</span><span class="sxs-lookup"><span data-stu-id="b4a49-130">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="b4a49-131">Consente di ottenere gli indirizzi IP delle macchine virtuali create dall'esempio.</span><span class="sxs-lookup"><span data-stu-id="b4a49-131">Get the IP addresses of the VMs created by the sample.</span></span> |
| [<span data-ttu-id="b4a49-132">az network lb show</span><span class="sxs-lookup"><span data-stu-id="b4a49-132">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="b4a49-133">Consente di ottenere le porte di front-end e back-end usate dal bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="b4a49-133">Get the frontend and backend ports used by the load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b4a49-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b4a49-134">Next steps</span></span>

<span data-ttu-id="b4a49-135">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b4a49-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b4a49-136">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4a49-136">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
