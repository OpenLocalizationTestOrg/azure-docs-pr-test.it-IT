---
title: "aaaVirtual computer estensioni e funzionalità per Linux | Documenti Microsoft"
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
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="f3e7e-103">Estensioni della macchina virtuale e funzionalità per Linux</span><span class="sxs-lookup"><span data-stu-id="f3e7e-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="f3e7e-104">Le estensioni della macchina virtuale di Azure sono piccole applicazioni che eseguono attività di configurazione e automazione post-distribuzione sulle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="f3e7e-105">Ad esempio, se una macchina virtuale richiede l'installazione del software, protezione antivirus o configurazione di Docker, un'estensione della macchina virtuale può essere utilizzato toocomplete queste attività.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="f3e7e-106">Le estensioni VM di Azure possono essere eseguite tramite hello CLI di Azure PowerShell, i modelli, Gestione risorse di Azure e hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-106">Azure VM extensions can be run using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="f3e7e-107">Le estensioni possono essere unite in bundle con una nuova distribuzione di macchina virtuale o eseguite su un sistema esistente.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="f3e7e-108">Questo documento fornisce una panoramica delle estensioni di macchina virtuale, i prerequisiti per l'utilizzo di estensioni di macchina virtuale di Azure e indicazioni su come gestire toodetect e rimuovere estensioni di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how toodetect, manage, and remove VM extensions.</span></span> <span data-ttu-id="f3e7e-109">Questo documento fornisce informazioni generali perché sono disponibili molte estensioni della macchina virtuale, ognuna con una configurazione potenzialmente univoca.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="f3e7e-110">Dettagli specifici dell'estensione sono disponibili in ogni estensione singoli toohello specifico di documento.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="f3e7e-111">Casi d'uso ed esempi</span><span class="sxs-lookup"><span data-stu-id="f3e7e-111">Use cases and samples</span></span>

<span data-ttu-id="f3e7e-112">Sono disponibili numerose estensioni della macchina virtuale di Azure, ognuna con uno specifico caso d'uso.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="f3e7e-113">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="f3e7e-113">Some examples are:</span></span>

- <span data-ttu-id="f3e7e-114">Applicare una macchina virtuale tooa configurazioni dello stato desiderato di PowerShell utilizzando hello estensione DSC per Linux.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-114">Apply PowerShell Desired State configurations tooa virtual machine using hello DSC extension for Linux.</span></span> <span data-ttu-id="f3e7e-115">Per altre informazioni, vedere l'argomento relativo all'[Estensione DSC (Desired State Configuration) di Azure](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span><span class="sxs-lookup"><span data-stu-id="f3e7e-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="f3e7e-116">Configurare il monitoraggio di una macchina virtuale con hello estensione di macchina virtuale di Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-116">Configure monitoring of a virtual machine with hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="f3e7e-117">Per ulteriori informazioni, vedere [come toomonitor una VM Linux](tutorial-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="f3e7e-117">For more information, see [How toomonitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="f3e7e-118">Configurare il monitoraggio dell'infrastruttura di Azure con estensione Datadog hello.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="f3e7e-119">Per ulteriori informazioni, vedere hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="f3e7e-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="f3e7e-120">Configurare un host Docker nella macchina virtuale di Azure utilizzando l'estensione della macchina virtuale Docker hello.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-120">Configure a Docker host on an Azure virtual machine using hello Docker VM extension.</span></span> <span data-ttu-id="f3e7e-121">Per altre informazioni, vedere [Estensione macchina virtuale per Docker](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="f3e7e-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="f3e7e-122">Inoltre estensioni specifiche di tooprocess, un'estensione Script personalizzato è disponibile per le macchine virtuali Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="f3e7e-123">estensione Script personalizzato per Linux Hello consente qualsiasi toobe script Bash eseguire in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-123">hello Custom Script extension for Linux allows any Bash script toobe run on a virtual machine.</span></span> <span data-ttu-id="f3e7e-124">Gli script personalizzati sono utili per la progettazione di distribuzioni di Azure che richiedono una configurazione in aggiunta a quella offerta dagli strumenti nativi di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="f3e7e-125">Per altre informazioni, vedere [Estensione di script personalizzata per le VM Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="f3e7e-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f3e7e-126">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f3e7e-126">Prerequisites</span></span>

<span data-ttu-id="f3e7e-127">Ogni estensione macchina virtuale può avere un insieme specifico di prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="f3e7e-128">Ad esempio, hello estensione della macchina virtuale Docker è un prerequisito di una distribuzione di Linux supportata.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="f3e7e-129">Requisiti di singole estensioni vengono descritti in dettaglio nella documentazione di hello specifiche dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="f3e7e-130">Agente VM di Azure</span><span class="sxs-lookup"><span data-stu-id="f3e7e-130">Azure VM agent</span></span>

<span data-ttu-id="f3e7e-131">agente VM di Azure Hello gestisce le interazioni tra una macchina virtuale di Azure e il controller di infrastruttura di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-131">hello Azure VM agent manages interactions between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="f3e7e-132">agente VM Hello è responsabile per molti aspetti funzionali di distribuzione e gestione di macchine virtuali di Azure, incluse l'esecuzione di estensioni di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="f3e7e-133">agente VM di Azure Hello è preinstallato in immagini di Azure Marketplace e può essere installato manualmente su sistemi operativi supportati.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="f3e7e-134">Per informazioni sui sistemi operativi supportati e per le istruzioni di installazione, vedere [Agente delle macchine virtuali di Azure](../windows/classic/agents-and-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="f3e7e-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="f3e7e-135">Individuare le estensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f3e7e-135">Discover VM extensions</span></span>

<span data-ttu-id="f3e7e-136">Molte estensioni delle macchine virtuali di diverso tipo sono disponibili per l'uso con macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="f3e7e-137">toosee un elenco completo, eseguire hello comando con hello CLI di Azure seguente, sostituendo il percorso di esempio hello con hello nel percorso desiderato.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-137">toosee a complete list, run hello following command with hello Azure CLI, replacing hello example location with hello location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="f3e7e-138">Eseguire le estensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f3e7e-138">Run VM extensions</span></span>

<span data-ttu-id="f3e7e-139">Estensioni di macchina virtuale di Azure possono essere eseguite nelle macchine virtuali esistenti, sono utili quando è necessario toomake modifiche di configurazione o ripristinare la connessione in una macchina virtuale già distribuita.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="f3e7e-140">Le estensioni della macchina virtuale possono essere anche unite in bundle con le distribuzioni del modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="f3e7e-141">L'uso delle estensioni con i modelli di Resource Manager consente di distribuire e configurare le macchine virtuali di Azure senza l'intervento post-distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="f3e7e-142">Hello dei seguenti metodi può essere utilizzati toorun un'estensione in una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-142">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="f3e7e-143">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f3e7e-143">Azure CLI</span></span>

<span data-ttu-id="f3e7e-144">Estensioni di macchina virtuale di Azure possono essere eseguite su una macchina virtuale esistente con hello `az vm extension set` comando.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-144">Azure virtual machine extensions can be run against an existing virtual machine by using hello `az vm extension set` command.</span></span> <span data-ttu-id="f3e7e-145">In questo esempio esegue l'estensione script personalizzata hello su una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-145">This example runs hello custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="f3e7e-146">Hello script genera output simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="f3e7e-146">hello script produces output similar toohello following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="f3e7e-147">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f3e7e-147">Azure portal</span></span>

<span data-ttu-id="f3e7e-148">Estensioni di macchina virtuale possono essere applicato tooan macchina virtuale esistente tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-148">VM extensions can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="f3e7e-149">toodo in tal caso, selezionare hello macchina virtuale, scegliere **estensioni**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-149">toodo so, select hello virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="f3e7e-150">Selezionare l'estensione di hello desiderato dall'elenco di hello delle estensioni disponibili e seguire le istruzioni di hello nella procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-150">Select hello extension you want from hello list of available extensions and follow hello instructions in hello wizard.</span></span>

<span data-ttu-id="f3e7e-151">Hello immagine seguente mostra installazione hello di hello estensione Script personalizzato Linux da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-151">hello following image shows hello installation of hello Linux Custom Script extension from hello Azure portal.</span></span>

![Installare l'estensione di script personalizzata](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="f3e7e-153">Modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="f3e7e-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="f3e7e-154">Estensioni di macchina virtuale possono essere aggiunto tooan modello di gestione risorse di Azure ed eseguita con la distribuzione di hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-154">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="f3e7e-155">Quando si distribuisce un'estensione con un modello, è possibile creare distribuzioni di Azure completamente configurate.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="f3e7e-156">Ad esempio, hello che JSON seguente viene eseguita da un modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-156">For example, hello following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="f3e7e-157">modello Hello distribuisce un insieme di macchine virtuali di bilanciamento del carico e un database SQL di Azure e quindi installa un'applicazione .NET Core su ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-157">hello template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="f3e7e-158">estensione della macchina virtuale Hello occupa hello dell'installazione del software.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-158">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="f3e7e-159">Per ulteriori informazioni, vedere hello completo [modello di gestione risorse](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="f3e7e-159">For more information, see hello full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

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

<span data-ttu-id="f3e7e-160">Per altre informazioni, vedere [Creazione di modelli di Azure Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="f3e7e-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="f3e7e-161">Proteggere i dati dell'estensione della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f3e7e-161">Secure VM extension data</span></span>

<span data-ttu-id="f3e7e-162">Quando si esegue un'estensione della macchina virtuale, potrebbe essere necessario tooinclude informazioni riservate, ad esempio le credenziali e i nomi degli account di archiviazione chiavi di accesso di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-162">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="f3e7e-163">Molte estensioni VM includono una configurazione protetta, che crittografa i dati e lo decrittografa solo all'interno di hello macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="f3e7e-164">Ogni estensione dispone di uno schema di configurazione protetta specifico, descritto in dettaglio nella documentazione specifica dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="f3e7e-165">Hello di esempio seguente mostra un'istanza di hello estensione Script personalizzato per Linux.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-165">hello following example shows an instance of hello Custom Script extension for Linux.</span></span> <span data-ttu-id="f3e7e-166">Si noti che tooexecute comando hello include un set di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-166">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="f3e7e-167">In questo esempio hello comando tooexecute non verrà crittografati.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-167">In this example, hello command tooexecute will not be encrypted.</span></span>


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

<span data-ttu-id="f3e7e-168">Hello mobile **comando tooexecute** proprietà toohello **protetti** configurazione consente di proteggere la stringa di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-168">Moving hello **command tooexecute** property toohello **protected** configuration secures hello execution string.</span></span>

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

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="f3e7e-169">Risoluzione dei problemi relativi alle estensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f3e7e-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="f3e7e-170">Ogni estensione della macchina virtuale abbia estensione toohello specifici passaggi di risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-170">Each VM extension may have troubleshooting steps specific toohello extension.</span></span> <span data-ttu-id="f3e7e-171">Ad esempio, quando si utilizza l'estensione Custom Script hello, dettagli sull'esecuzione di script è reperibile in locale nella macchina virtuale hello in cui è stata eseguita l'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-171">For example, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="f3e7e-172">Tutti i passaggi per la risoluzione dei problemi specifici dell'estensione sono descritti in dettaglio nella documentazione specifica dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="f3e7e-173">Hello risoluzione dei problemi relativi alla procedura seguente si applica tooall estensioni delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-173">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="f3e7e-174">Visualizzare lo stato dell'estensione</span><span class="sxs-lookup"><span data-stu-id="f3e7e-174">View extension status</span></span>

<span data-ttu-id="f3e7e-175">Dopo l'esecuzione di un'estensione della macchina virtuale in una macchina virtuale, utilizzare hello seguente lo stato dell'estensione tooreturn comando CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-175">After a virtual machine extension has been run against a virtual machine, use hello following Azure CLI command tooreturn extension status.</span></span> <span data-ttu-id="f3e7e-176">Sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="f3e7e-177">output di Hello è simile hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="f3e7e-177">hello output looks like hello following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="f3e7e-178">Lo stato dell'esecuzione di estensione può essere rilevata anche in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-178">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="f3e7e-179">stato hello tooview di un'estensione, hello selezionare macchina virtuale, scegliere **estensioni**, e selezionare hello estensione desiderata.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-179">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="f3e7e-180">Rieseguire un'estensione macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f3e7e-180">Rerun a VM extension</span></span>

<span data-ttu-id="f3e7e-181">Potrebbero essere presenti i casi in cui un'estensione della macchina virtuale deve toobe eseguire di nuovo.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-181">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="f3e7e-182">È possibile eseguire nuovamente un'estensione rimuovendola e quindi eseguire nuovamente estensione hello con un metodo di esecuzione di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-182">You can rerun an extension by removing it, and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="f3e7e-183">tooremove un'estensione, eseguire hello comando con hello CLI di Azure seguente.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-183">tooremove an extension, run hello following command with hello Azure CLI.</span></span> <span data-ttu-id="f3e7e-184">Sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="f3e7e-185">È possibile rimuovere un'estensione tramite hello in hello portale di Azure come segue:</span><span class="sxs-lookup"><span data-stu-id="f3e7e-185">You can remove an extension by using hello following steps in hello Azure portal:</span></span>

1. <span data-ttu-id="f3e7e-186">Selezionare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="f3e7e-187">Scegliere **Estensioni**.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="f3e7e-188">Selezionare l'estensione hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-188">Select hello desired extension.</span></span>
4. <span data-ttu-id="f3e7e-189">Scegliere **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="f3e7e-190">Riferimento alle estensioni della macchina virtuale comuni</span><span class="sxs-lookup"><span data-stu-id="f3e7e-190">Common VM extension reference</span></span>
| <span data-ttu-id="f3e7e-191">Nome estensione</span><span class="sxs-lookup"><span data-stu-id="f3e7e-191">Extension name</span></span> | <span data-ttu-id="f3e7e-192">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f3e7e-192">Description</span></span> | <span data-ttu-id="f3e7e-193">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="f3e7e-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f3e7e-194">Estensione script personalizzata per Linux</span><span class="sxs-lookup"><span data-stu-id="f3e7e-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="f3e7e-195">Eseguire gli script in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="f3e7e-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="f3e7e-196">Estensione script personalizzata per Linux</span><span class="sxs-lookup"><span data-stu-id="f3e7e-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="f3e7e-197">Estensione per Docker</span><span class="sxs-lookup"><span data-stu-id="f3e7e-197">Docker extension</span></span> |<span data-ttu-id="f3e7e-198">Installare hello Docker daemon toosupport comandi Docker remoti.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-198">Install hello Docker daemon toosupport remote Docker commands.</span></span> |[<span data-ttu-id="f3e7e-199">Estensione macchina virtuale per Docker</span><span class="sxs-lookup"><span data-stu-id="f3e7e-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="f3e7e-200">Estensione dell'accesso alle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f3e7e-200">VM Access extension</span></span> |<span data-ttu-id="f3e7e-201">Ripristinare l'accesso tooan macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="f3e7e-201">Regain access tooan Azure virtual machine</span></span> |[<span data-ttu-id="f3e7e-202">Estensione dell'accesso alle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f3e7e-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="f3e7e-203">Estensione di Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="f3e7e-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="f3e7e-204">Gestisce Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e7e-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="f3e7e-205">Estensione di Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="f3e7e-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="f3e7e-206">Estensione dell'accesso alla VM di Azure</span><span class="sxs-lookup"><span data-stu-id="f3e7e-206">Azure VM Access extension</span></span> |<span data-ttu-id="f3e7e-207">Gestire gli utenti e le credenziali</span><span class="sxs-lookup"><span data-stu-id="f3e7e-207">Manage users and credentials</span></span> |[<span data-ttu-id="f3e7e-208">Estensione dell'accesso alla VM per Linux</span><span class="sxs-lookup"><span data-stu-id="f3e7e-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
