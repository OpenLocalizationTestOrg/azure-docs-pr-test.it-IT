---
title: "Estensioni della macchina virtuale e funzionalità per Linux | Documentazione Microsoft"
description: "Informazioni sulle estensioni disponibili per le macchine virtuali di Azure, raggruppate in base a ciò che forniscono o migliorano."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 8a5b39351f665c51ae7d83f755329e54ff3cf786
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="4ec05-103">Estensioni della macchina virtuale e funzionalità per Linux</span><span class="sxs-lookup"><span data-stu-id="4ec05-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="4ec05-104">Le estensioni della macchina virtuale di Azure sono piccole applicazioni che eseguono attività di configurazione e automazione post-distribuzione nelle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec05-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="4ec05-105">Ad esempio, se una macchina virtuale richiede l'installazione di software, la protezione antivirus o la configurazione di Docker, è possibile usare un'estensione di questo tipo per completare queste attività.</span><span class="sxs-lookup"><span data-stu-id="4ec05-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span></span> <span data-ttu-id="4ec05-106">Le estensioni della macchina virtuale di Azure possono essere eseguite tramite l'interfaccia della riga di comando di Azure, PowerShell, i modelli di Azure Resource Manager e il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec05-106">Azure VM extensions can be run using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span> <span data-ttu-id="4ec05-107">Le estensioni possono essere unite in bundle con una nuova distribuzione di macchina virtuale o eseguite su un sistema esistente.</span><span class="sxs-lookup"><span data-stu-id="4ec05-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="4ec05-108">Questo documento fornisce una panoramica delle estensioni della macchina virtuale, i prerequisiti per l'uso di queste estensioni di Azure e indicazioni su come rilevare, gestire e rimuovere le estensioni.</span><span class="sxs-lookup"><span data-stu-id="4ec05-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how to detect, manage, and remove VM extensions.</span></span> <span data-ttu-id="4ec05-109">Questo documento contiene informazioni generali perché sono disponibili molte estensioni della macchina virtuale, ognuna con una configurazione potenzialmente univoca.</span><span class="sxs-lookup"><span data-stu-id="4ec05-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="4ec05-110">I dettagli sono disponibili nel documento specifico della singola estensione.</span><span class="sxs-lookup"><span data-stu-id="4ec05-110">Extension-specific details can be found in each document specific to the individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="4ec05-111">Casi d'uso ed esempi</span><span class="sxs-lookup"><span data-stu-id="4ec05-111">Use cases and samples</span></span>

<span data-ttu-id="4ec05-112">Sono disponibili numerose estensioni della macchina virtuale di Azure, ognuna con uno specifico caso d'uso.</span><span class="sxs-lookup"><span data-stu-id="4ec05-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="4ec05-113">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="4ec05-113">Some examples are:</span></span>

- <span data-ttu-id="4ec05-114">Applicare le configurazioni dello stato desiderato tramite PowerShell a una macchina virtuale usando l'estensione DSC per Linux.</span><span class="sxs-lookup"><span data-stu-id="4ec05-114">Apply PowerShell Desired State configurations to a virtual machine using the DSC extension for Linux.</span></span> <span data-ttu-id="4ec05-115">Per altre informazioni, vedere l'argomento relativo all'[Introduzione al gestore dell'estensione DSC (Desired State Configuration) di Azure](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span><span class="sxs-lookup"><span data-stu-id="4ec05-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="4ec05-116">Configurare il monitoraggio di una macchina virtuale con l'estensione macchina virtuale di Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="4ec05-116">Configure monitoring of a virtual machine with the Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="4ec05-117">Per altre informazioni, vedere [Come monitorare una macchina virtuale Linux in Azure](tutorial-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="4ec05-117">For more information, see [How to monitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="4ec05-118">Configurare il monitoraggio dell'infrastruttura di Azure con l'estensione Datadog.</span><span class="sxs-lookup"><span data-stu-id="4ec05-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span></span> <span data-ttu-id="4ec05-119">Per altre informazioni, vedere il [blog Datadog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="4ec05-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="4ec05-120">Configurare un host Docker in una macchina virtuale di Azure usando l'estensione macchina virtuale Docker.</span><span class="sxs-lookup"><span data-stu-id="4ec05-120">Configure a Docker host on an Azure virtual machine using the Docker VM extension.</span></span> <span data-ttu-id="4ec05-121">Per altre informazioni, vedere [Estensione macchina virtuale per Docker](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="4ec05-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="4ec05-122">Oltre alle estensioni specifiche del processo, è disponibile un'estensione dello script personalizzata per le macchine virtuali Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="4ec05-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="4ec05-123">L'estensione dello script personalizzata per Linux consente l'esecuzione di qualsiasi script Bash su una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ec05-123">The Custom Script extension for Linux allows any Bash script to be run on a virtual machine.</span></span> <span data-ttu-id="4ec05-124">Gli script personalizzati sono utili per la progettazione di distribuzioni di Azure che richiedono una configurazione in aggiunta a quella offerta dagli strumenti nativi di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec05-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="4ec05-125">Per altre informazioni, vedere [Estensione di script personalizzata per le VM Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="4ec05-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4ec05-126">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4ec05-126">Prerequisites</span></span>

<span data-ttu-id="4ec05-127">Ogni estensione macchina virtuale può avere un insieme specifico di prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="4ec05-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="4ec05-128">Ad esempio, un prerequisito dell'estensione macchina virtuale per Docker è una distribuzione Linux supportata.</span><span class="sxs-lookup"><span data-stu-id="4ec05-128">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="4ec05-129">La documentazione specifica dell'estensione illustra in dettaglio i requisiti delle singole estensioni.</span><span class="sxs-lookup"><span data-stu-id="4ec05-129">Requirements of individual extensions are detailed in the extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="4ec05-130">Agente VM di Azure</span><span class="sxs-lookup"><span data-stu-id="4ec05-130">Azure VM agent</span></span>

<span data-ttu-id="4ec05-131">L'agente VM di Azure gestisce le interazioni tra una macchina virtuale di Azure e il controller di infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec05-131">The Azure VM agent manages interactions between an Azure virtual machine and the Azure fabric controller.</span></span> <span data-ttu-id="4ec05-132">L'agente VM è responsabile di molti aspetti funzionali della distribuzione e della gestione delle macchine virtuali di Azure, tra cui l'esecuzione delle estensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ec05-132">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="4ec05-133">L'agente VM di Azure è preinstallato nelle immagini di Azure Marketplace e può essere installato manualmente nei sistemi operativi supportati.</span><span class="sxs-lookup"><span data-stu-id="4ec05-133">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="4ec05-134">Per informazioni sui sistemi operativi supportati e per le istruzioni di installazione, vedere l'[agente VM di Azure](../windows/classic/agents-and-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="4ec05-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="4ec05-135">Individuare le estensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4ec05-135">Discover VM extensions</span></span>

<span data-ttu-id="4ec05-136">Molte estensioni della macchina virtuale di diverso tipo sono disponibili per l'uso con le macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec05-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="4ec05-137">Per visualizzare un elenco completo, eseguire il comando seguente con l'interfaccia della riga di comando di Azure, sostituendo il percorso di esempio con quello scelto.</span><span class="sxs-lookup"><span data-stu-id="4ec05-137">To see a complete list, run the following command with the Azure CLI, replacing the example location with the location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="4ec05-138">Eseguire le estensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4ec05-138">Run VM extensions</span></span>

<span data-ttu-id="4ec05-139">Le estensioni della macchina virtuale di Azure possono essere eseguite nelle macchine virtuali esistenti e sono utili quando è necessario apportare modifiche alla configurazione o ripristinare la connettività in una macchina virtuale già distribuita.</span><span class="sxs-lookup"><span data-stu-id="4ec05-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="4ec05-140">Le estensioni della macchina virtuale possono essere anche unite in bundle con le distribuzioni del modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4ec05-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="4ec05-141">L'uso delle estensioni con i modelli di Resource Manager consente di distribuire e configurare le macchine virtuali di Azure senza l'intervento post-distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4ec05-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="4ec05-142">Per eseguire un'estensione in una macchina virtuale esistente, è possibile usare i metodi seguenti.</span><span class="sxs-lookup"><span data-stu-id="4ec05-142">The following methods can be used to run an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="4ec05-143">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="4ec05-143">Azure CLI</span></span>

<span data-ttu-id="4ec05-144">Le estensioni della macchina virtuale di Azure possono essere eseguite in una macchina virtuale esistente usando il comando `az vm extension set`.</span><span class="sxs-lookup"><span data-stu-id="4ec05-144">Azure virtual machine extensions can be run against an existing virtual machine by using the `az vm extension set` command.</span></span> <span data-ttu-id="4ec05-145">Questo esempio esegue l'estensione script personalizzata in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ec05-145">This example runs the custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="4ec05-146">Lo script genera un output simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="4ec05-146">The script produces output similar to the following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up the VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="4ec05-147">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4ec05-147">Azure portal</span></span>

<span data-ttu-id="4ec05-148">Le estensioni della macchina virtuale possono essere applicate a una macchina virtuale esistente tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec05-148">VM extensions can be applied to an existing virtual machine through the Azure portal.</span></span> <span data-ttu-id="4ec05-149">A tale scopo, selezionare la macchina virtuale, scegliere **Estensioni**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4ec05-149">To do so, select the virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="4ec05-150">Selezionare l'estensione desiderata dall'elenco di quelle disponibili e quindi seguire le istruzioni della procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="4ec05-150">Select the extension you want from the list of available extensions and follow the instructions in the wizard.</span></span>

<span data-ttu-id="4ec05-151">L'immagine seguente illustra l'installazione dell'estensione di script personalizzata per Linux dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec05-151">The following image shows the installation of the Linux Custom Script extension from the Azure portal.</span></span>

![Installare l'estensione di script personalizzata](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="4ec05-153">Modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="4ec05-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="4ec05-154">Le estensioni della macchina virtuale possono essere aggiunte a un modello di Azure Resource Manager ed eseguite con la distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="4ec05-154">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span></span> <span data-ttu-id="4ec05-155">Quando si distribuisce un'estensione con un modello, è possibile creare distribuzioni di Azure completamente configurate.</span><span class="sxs-lookup"><span data-stu-id="4ec05-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="4ec05-156">Il codice JSON seguente, ad esempio, è tratto da un modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4ec05-156">For example, the following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="4ec05-157">Il modello distribuisce un set di macchine virtuali con carico bilanciato e un database SQL di Azure, quindi installa un'applicazione .NET Core in ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ec05-157">The template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="4ec05-158">L'estensione della macchina virtuale gestisce l'installazione del software.</span><span class="sxs-lookup"><span data-stu-id="4ec05-158">The VM extension takes care of the software installation.</span></span>

<span data-ttu-id="4ec05-159">Per altre informazioni, vedere il [modello di Resource Manager](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux) completo.</span><span class="sxs-lookup"><span data-stu-id="4ec05-159">For more information, see the full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

<span data-ttu-id="4ec05-160">Per altre informazioni, vedere [Creazione di modelli di Azure Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="4ec05-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="4ec05-161">Proteggere i dati dell'estensione della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4ec05-161">Secure VM extension data</span></span>

<span data-ttu-id="4ec05-162">Quando si esegue un'estensione macchina virtuale, potrebbe essere necessario includere informazioni riservate, ad esempio le credenziali, i nomi degli account di archiviazione e le chiavi di accesso dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4ec05-162">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="4ec05-163">Molte estensioni della macchina virtuale includono una configurazione protetta che crittografa i dati e li decrittografa solo all'interno della macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4ec05-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span></span> <span data-ttu-id="4ec05-164">Ogni estensione dispone di uno schema di configurazione protetta specifico, descritto in dettaglio nella documentazione specifica dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="4ec05-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="4ec05-165">L'esempio seguente illustra un'istanza dell'estensione script personalizzata per Linux.</span><span class="sxs-lookup"><span data-stu-id="4ec05-165">The following example shows an instance of the Custom Script extension for Linux.</span></span> <span data-ttu-id="4ec05-166">Si noti che il comando da eseguire include un insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="4ec05-166">Notice that the command to execute includes a set of credentials.</span></span> <span data-ttu-id="4ec05-167">In questo esempio, il comando da eseguire non verrà crittografato.</span><span class="sxs-lookup"><span data-stu-id="4ec05-167">In this example, the command to execute will not be encrypted.</span></span>


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="4ec05-168">Lo spostamento della proprietà del **comando da eseguire** nella configurazione **protetta** consente di proteggere la stringa di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4ec05-168">Moving the **command to execute** property to the **protected** configuration secures the execution string.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="4ec05-169">Risoluzione dei problemi relativi alle estensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4ec05-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="4ec05-170">Ogni estensione macchina virtuale può richiedere passaggi per la risoluzione dei problemi specifici per l'estensione.</span><span class="sxs-lookup"><span data-stu-id="4ec05-170">Each VM extension may have troubleshooting steps specific to the extension.</span></span> <span data-ttu-id="4ec05-171">Ad esempio, quando si usa l'estensione di script personalizzata, i dettagli sull'esecuzione dello script sono disponibili in locale nella macchina virtuale in cui è stata eseguita l'estensione.</span><span class="sxs-lookup"><span data-stu-id="4ec05-171">For example, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span></span> <span data-ttu-id="4ec05-172">Tutti i passaggi per la risoluzione dei problemi specifici dell'estensione sono descritti in dettaglio nella documentazione specifica dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="4ec05-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="4ec05-173">I passaggi per la risoluzione dei problemi seguenti si applicano a tutte le estensioni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ec05-173">The following troubleshooting steps apply to all virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="4ec05-174">Visualizzare lo stato dell'estensione</span><span class="sxs-lookup"><span data-stu-id="4ec05-174">View extension status</span></span>

<span data-ttu-id="4ec05-175">Dopo l'esecuzione di un'estensione macchina virtuale in una macchina virtuale, usare il comando dell'interfaccia della riga di comando seguente di Azure per ottenere lo stato dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="4ec05-175">After a virtual machine extension has been run against a virtual machine, use the following Azure CLI command to return extension status.</span></span> <span data-ttu-id="4ec05-176">Sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="4ec05-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="4ec05-177">L'output ha un aspetto simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="4ec05-177">The output looks like the following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="4ec05-178">Lo stato di esecuzione dell'estensione è disponibile anche nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec05-178">Extension execution status can also be found in the Azure portal.</span></span> <span data-ttu-id="4ec05-179">Per visualizzare lo stato di un'estensione, selezionare la macchina virtuale, scegliere **Estensioni** e selezionare l'estensione desiderata.</span><span class="sxs-lookup"><span data-stu-id="4ec05-179">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="4ec05-180">Rieseguire un'estensione macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4ec05-180">Rerun a VM extension</span></span>

<span data-ttu-id="4ec05-181">In alcuni casi potrebbe essere necessario rieseguire un'estensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ec05-181">There may be cases in which a virtual machine extension needs to be rerun.</span></span> <span data-ttu-id="4ec05-182">È possibile eseguire tale operazione rimuovendo l'estensione e quindi eseguendola di nuovo con il metodo scelto.</span><span class="sxs-lookup"><span data-stu-id="4ec05-182">You can rerun an extension by removing it, and then rerunning the extension with an execution method of your choice.</span></span> <span data-ttu-id="4ec05-183">Per rimuovere un'estensione, eseguire il comando seguente con l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec05-183">To remove an extension, run the following command with the Azure CLI.</span></span> <span data-ttu-id="4ec05-184">Sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="4ec05-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="4ec05-185">È possibile rimuovere un'estensione usando i passaggi seguenti nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="4ec05-185">You can remove an extension by using the following steps in the Azure portal:</span></span>

1. <span data-ttu-id="4ec05-186">Selezionare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4ec05-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="4ec05-187">Scegliere **Estensioni**.</span><span class="sxs-lookup"><span data-stu-id="4ec05-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="4ec05-188">Selezionare l'estensione desiderata.</span><span class="sxs-lookup"><span data-stu-id="4ec05-188">Select the desired extension.</span></span>
4. <span data-ttu-id="4ec05-189">Scegliere **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="4ec05-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="4ec05-190">Riferimento alle estensioni della macchina virtuale comuni</span><span class="sxs-lookup"><span data-stu-id="4ec05-190">Common VM extension reference</span></span>
| <span data-ttu-id="4ec05-191">Nome estensione</span><span class="sxs-lookup"><span data-stu-id="4ec05-191">Extension name</span></span> | <span data-ttu-id="4ec05-192">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4ec05-192">Description</span></span> | <span data-ttu-id="4ec05-193">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="4ec05-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4ec05-194">Estensione script personalizzata per Linux</span><span class="sxs-lookup"><span data-stu-id="4ec05-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="4ec05-195">Eseguire gli script in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="4ec05-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="4ec05-196">Estensione script personalizzata per Linux</span><span class="sxs-lookup"><span data-stu-id="4ec05-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="4ec05-197">Estensione per Docker</span><span class="sxs-lookup"><span data-stu-id="4ec05-197">Docker extension</span></span> |<span data-ttu-id="4ec05-198">Installare il daemon Docker per supportare i comandi Docker remoti.</span><span class="sxs-lookup"><span data-stu-id="4ec05-198">Install the Docker daemon to support remote Docker commands.</span></span> |[<span data-ttu-id="4ec05-199">Estensione macchina virtuale per Docker</span><span class="sxs-lookup"><span data-stu-id="4ec05-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="4ec05-200">Estensione dell'accesso alle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="4ec05-200">VM Access extension</span></span> |<span data-ttu-id="4ec05-201">Ripristinare l'accesso a una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="4ec05-201">Regain access to an Azure virtual machine</span></span> |[<span data-ttu-id="4ec05-202">Estensione dell'accesso alle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="4ec05-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="4ec05-203">Estensione di Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="4ec05-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="4ec05-204">Gestisce Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ec05-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="4ec05-205">Estensione di Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="4ec05-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="4ec05-206">Estensione dell'accesso alla VM di Azure</span><span class="sxs-lookup"><span data-stu-id="4ec05-206">Azure VM Access extension</span></span> |<span data-ttu-id="4ec05-207">Gestire gli utenti e le credenziali</span><span class="sxs-lookup"><span data-stu-id="4ec05-207">Manage users and credentials</span></span> |[<span data-ttu-id="4ec05-208">Estensione dell'accesso alla VM per Linux</span><span class="sxs-lookup"><span data-stu-id="4ec05-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
