---
title: "aaaVirtual computer estensioni e funzionalità per Windows in Azure | Documenti Microsoft"
description: "Informazioni sulle estensioni disponibili per le macchine virtuali di Azure, raggruppate in base a ciò che forniscono o migliorano."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="b59d0-103">Estensioni e funzionalità della macchina virtuale per Windows</span><span class="sxs-lookup"><span data-stu-id="b59d0-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="b59d0-104">Le estensioni della macchina virtuale di Azure sono piccole applicazioni che eseguono attività di configurazione e automazione post-distribuzione sulle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="b59d0-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="b59d0-105">Ad esempio, se una macchina virtuale richiede l'installazione del software, protezione antivirus o configurazione di Docker, un'estensione della macchina virtuale può essere utilizzato toocomplete queste attività.</span><span class="sxs-lookup"><span data-stu-id="b59d0-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="b59d0-106">Le estensioni VM di Azure possono essere eseguite utilizzando hello CLI di Azure PowerShell, i modelli, Gestione risorse di Azure e hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b59d0-106">Azure VM extensions can be run by using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="b59d0-107">Le estensioni possono essere unite in bundle con una nuova distribuzione di macchina virtuale o eseguite su un sistema esistente.</span><span class="sxs-lookup"><span data-stu-id="b59d0-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="b59d0-108">Questo documento viene fornita una panoramica delle estensioni di macchina virtuale, i prerequisiti per l'utilizzo di estensioni di macchine virtuali e istruzioni su come gestire toodetect e rimuovere estensioni di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b59d0-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how toodetect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="b59d0-109">Questo documento fornisce informazioni generali perché sono disponibili molte estensioni della macchina virtuale, ognuna con una configurazione potenzialmente univoca.</span><span class="sxs-lookup"><span data-stu-id="b59d0-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="b59d0-110">Dettagli specifici dell'estensione sono disponibili in ogni estensione singoli toohello specifico di documento.</span><span class="sxs-lookup"><span data-stu-id="b59d0-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="b59d0-111">Casi d'uso ed esempi</span><span class="sxs-lookup"><span data-stu-id="b59d0-111">Use cases and samples</span></span>

<span data-ttu-id="b59d0-112">Sono disponibili numerose estensioni della macchina virtuale di Azure, ognuna con un caso d'uso specifico.</span><span class="sxs-lookup"><span data-stu-id="b59d0-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="b59d0-113">Alcuni esempi di casi d'uso sono:</span><span class="sxs-lookup"><span data-stu-id="b59d0-113">Some example use cases are:</span></span>

- <span data-ttu-id="b59d0-114">Applicare macchina virtuale di tooa configurazioni dello stato desiderato di PowerShell utilizzando l'estensione DSC hello per Windows.</span><span class="sxs-lookup"><span data-stu-id="b59d0-114">Apply PowerShell Desired State configurations tooa virtual machine by using hello DSC extension for Windows.</span></span> <span data-ttu-id="b59d0-115">Per altre informazioni, vedere l'argomento relativo all'[Estensione DSC (Desired State Configuration) di Azure](extensions-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b59d0-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="b59d0-116">Configurare il monitoraggio di macchina virtuale utilizzando l'estensione di macchina virtuale di Microsoft Monitoring Agent hello.</span><span class="sxs-lookup"><span data-stu-id="b59d0-116">Configure virtual machine monitoring by using hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="b59d0-117">Per ulteriori informazioni, vedere [tooLog di macchine virtuali di Azure connettersi Analitica](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="b59d0-117">For more information, see [Connect Azure virtual machines tooLog Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="b59d0-118">Configurare il monitoraggio dell'infrastruttura di Azure con estensione Datadog hello.</span><span class="sxs-lookup"><span data-stu-id="b59d0-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="b59d0-119">Per ulteriori informazioni, vedere hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="b59d0-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="b59d0-120">Configurare una macchina virtuale di Azure con Chef.</span><span class="sxs-lookup"><span data-stu-id="b59d0-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="b59d0-121">Per altre informazioni, vedere l'argomento [Automazione della distribuzione delle macchine virtuali di Azure con Chef](chef-automation.md)</span><span class="sxs-lookup"><span data-stu-id="b59d0-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="b59d0-122">Inoltre estensioni specifiche di tooprocess, un'estensione Script personalizzato è disponibile per le macchine virtuali Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="b59d0-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="b59d0-123">estensione Script personalizzato per Windows Hello consente qualsiasi toobe di script di PowerShell eseguire in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b59d0-123">hello Custom Script extension for Windows allows any PowerShell script toobe run on a virtual machine.</span></span> <span data-ttu-id="b59d0-124">È utile per la progettazione di distribuzioni di Azure che richiedono una configurazione oltre a quella offerta dagli strumenti nativi di Azure.</span><span class="sxs-lookup"><span data-stu-id="b59d0-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="b59d0-125">Per altre informazioni, vedere [Estensione Script personalizzato per macchine virtuali Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="b59d0-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b59d0-126">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b59d0-126">Prerequisites</span></span>

<span data-ttu-id="b59d0-127">Ogni estensione macchina virtuale può avere un insieme specifico di prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="b59d0-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="b59d0-128">Ad esempio, hello estensione della macchina virtuale Docker è un prerequisito di una distribuzione di Linux supportata.</span><span class="sxs-lookup"><span data-stu-id="b59d0-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="b59d0-129">Requisiti di singole estensioni vengono descritti in dettaglio nella documentazione di hello specifiche dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="b59d0-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="b59d0-130">Agente VM di Azure</span><span class="sxs-lookup"><span data-stu-id="b59d0-130">Azure VM agent</span></span>
<span data-ttu-id="b59d0-131">agente VM di Azure Hello gestisce l'interazione tra una macchina virtuale di Azure e il controller di infrastruttura di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b59d0-131">hello Azure VM agent manages interaction between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="b59d0-132">agente VM Hello è responsabile per molti aspetti funzionali di distribuzione e gestione di macchine virtuali di Azure, incluse l'esecuzione di estensioni di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b59d0-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="b59d0-133">agente VM di Azure Hello è preinstallato in immagini di Azure Marketplace e può essere installato nei sistemi operativi supportati.</span><span class="sxs-lookup"><span data-stu-id="b59d0-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="b59d0-134">Per informazioni sui sistemi operativi supportati e per le istruzioni di installazione, vedere [Agente delle macchine virtuali di Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="b59d0-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="b59d0-135">Individuare le estensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b59d0-135">Discover VM extensions</span></span>
<span data-ttu-id="b59d0-136">Molte estensioni delle macchine virtuali di diverso tipo sono disponibili per l'uso con macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="b59d0-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="b59d0-137">toosee un elenco completo, eseguire hello comando con il modulo di gestione risorse di Azure PowerShell hello seguente.</span><span class="sxs-lookup"><span data-stu-id="b59d0-137">toosee a complete list, run hello following command with hello Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="b59d0-138">Impostare percorsi di hello desiderato di toospecify che quando si esegue questo comando.</span><span class="sxs-lookup"><span data-stu-id="b59d0-138">Make sure toospecify hello desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="b59d0-139">Eseguire le estensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b59d0-139">Run VM extensions</span></span>

<span data-ttu-id="b59d0-140">Estensioni di macchina virtuale di Azure possono essere eseguite nelle macchine virtuali esistenti, che è utile quando è necessario toomake modifiche di configurazione o ripristinare la connessione in una macchina virtuale già distribuita.</span><span class="sxs-lookup"><span data-stu-id="b59d0-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="b59d0-141">Le estensioni della macchina virtuale possono essere anche unite in bundle con le distribuzioni del modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b59d0-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="b59d0-142">Utilizzando le estensioni con modelli di gestione risorse, è possibile abilitare toobe macchine virtuali di Azure distribuito e configurato senza la necessità di hello di interventi di post-distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b59d0-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines toobe deployed and configured without hello need for post-deployment intervention.</span></span>

<span data-ttu-id="b59d0-143">Hello dei seguenti metodi può essere utilizzati toorun un'estensione in una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="b59d0-143">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="b59d0-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b59d0-144">PowerShell</span></span>

<span data-ttu-id="b59d0-145">Molti comandi di PowerShell vengono utilizzati per l'esecuzione di estensioni singole.</span><span class="sxs-lookup"><span data-stu-id="b59d0-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="b59d0-146">toosee un elenco, eseguire i comandi di PowerShell seguente hello.</span><span class="sxs-lookup"><span data-stu-id="b59d0-146">toosee a list, run hello following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="b59d0-147">Questo fornisce seguenti toohello simili di output:</span><span class="sxs-lookup"><span data-stu-id="b59d0-147">This provides output similar toohello following:</span></span>

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

<span data-ttu-id="b59d0-148">Hello esempio utilizza toodownload di estensione Custom Script hello uno script da un repository di GitHub nella macchina virtuale di destinazione hello e quindi eseguirla script hello.</span><span class="sxs-lookup"><span data-stu-id="b59d0-148">hello following example uses hello Custom Script extension toodownload a script from a GitHub repository onto hello target virtual machine and then run hello script.</span></span> <span data-ttu-id="b59d0-149">Per ulteriori informazioni sull'estensione dello Script personalizzata hello, vedere [Panoramica di estensione Custom Script](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="b59d0-149">For more information on hello Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="b59d0-150">In questo esempio, hello estensione accesso alle macchine Virtuali è password amministrativa di hello tooreset usate di una macchina virtuale di Windows.</span><span class="sxs-lookup"><span data-stu-id="b59d0-150">In this example, hello VM Access extension is used tooreset hello administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="b59d0-151">Per ulteriori informazioni su hello estensione accesso alle macchine Virtuali, vedere [servizio reimpostare Desktop remoto in una macchina virtuale Windows](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="b59d0-151">For more information on hello VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="b59d0-152">Hello `Set-AzureRmVMExtension` comando può essere utilizzato toostart qualsiasi estensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b59d0-152">hello `Set-AzureRmVMExtension` command can be used toostart any VM extension.</span></span> <span data-ttu-id="b59d0-153">Per ulteriori informazioni, vedere hello [Set AzureRmVMExtension riferimento](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="b59d0-153">For more information, see hello [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="b59d0-154">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b59d0-154">Azure portal</span></span>

<span data-ttu-id="b59d0-155">Un'estensione della macchina virtuale può essere applicato tooan macchina virtuale esistente tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b59d0-155">A VM extension can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="b59d0-156">toodo in tal caso, selezionare macchina virtuale hello toouse desiderati, scegliere **estensioni**, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b59d0-156">toodo so, select hello virtual machine you want toouse, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="b59d0-157">In questo modo si ottiene un elenco di estensioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="b59d0-157">This provides a list of available extensions.</span></span> <span data-ttu-id="b59d0-158">Selezionare hello uno desiderato e quindi seguire i passaggi di hello nella procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="b59d0-158">Select hello one you want and follow hello steps in hello wizard.</span></span>

<span data-ttu-id="b59d0-159">Hello immagine seguente viene illustrata hello installazione dell'estensione di Microsoft Antimalware dal portale di Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="b59d0-159">hello following image shows hello installation of hello Microsoft Antimalware extension from hello Azure portal.</span></span>

![Installare un'estensione antimalware](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="b59d0-161">Modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="b59d0-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="b59d0-162">Estensioni di macchina virtuale possono essere aggiunto tooan modello di gestione risorse di Azure ed eseguita con la distribuzione di hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="b59d0-162">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="b59d0-163">La distribuzione di estensioni con un modello è utile per la creazione di distribuzioni di Azure completamente configurate.</span><span class="sxs-lookup"><span data-stu-id="b59d0-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="b59d0-164">Ad esempio, hello che JSON seguente viene eseguita da un modello di gestione risorse che distribuisce un insieme di macchine virtuali di bilanciamento del carico e un database SQL di Azure e quindi installa un'applicazione .NET Core su ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b59d0-164">For example, hello following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="b59d0-165">estensione della macchina virtuale Hello occupa hello dell'installazione del software.</span><span class="sxs-lookup"><span data-stu-id="b59d0-165">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="b59d0-166">Per ulteriori informazioni, vedere hello [complete dei modelli di gestione risorse](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="b59d0-166">For more information, see hello [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="b59d0-167">Per altre informazioni, vedere [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions) (Creazione di modelli di Azure Resource Manager con le estensioni della macchina virtuale Windows).</span><span class="sxs-lookup"><span data-stu-id="b59d0-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="b59d0-168">Proteggere i dati dell'estensione della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b59d0-168">Secure VM extension data</span></span>

<span data-ttu-id="b59d0-169">Quando si esegue un'estensione della macchina virtuale, potrebbe essere necessario tooinclude informazioni riservate, ad esempio le credenziali e i nomi degli account di archiviazione chiavi di accesso di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b59d0-169">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="b59d0-170">Molte estensioni VM includono una configurazione protetta, che crittografa i dati e lo decrittografa solo all'interno di hello macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b59d0-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="b59d0-171">Ogni estensione ha uno schema di configurazione protetto specifico che sarà descritto in maniera dettagliata nella documentazione specifica dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="b59d0-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="b59d0-172">Hello di esempio seguente mostra un'istanza di hello estensione Script personalizzato per Windows.</span><span class="sxs-lookup"><span data-stu-id="b59d0-172">hello following example shows an instance of hello Custom Script extension for Windows.</span></span> <span data-ttu-id="b59d0-173">Si noti che tooexecute comando hello include un set di credenziali.</span><span class="sxs-lookup"><span data-stu-id="b59d0-173">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="b59d0-174">In questo esempio hello comando tooexecute non verrà crittografati.</span><span class="sxs-lookup"><span data-stu-id="b59d0-174">In this example, hello command tooexecute will not be encrypted.</span></span>


```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="b59d0-175">Proteggere la stringa di esecuzione hello spostando hello **comando tooexecute** proprietà toohello **protetti** configurazione.</span><span class="sxs-lookup"><span data-stu-id="b59d0-175">Secure hello execution string by moving hello **command tooexecute** property toohello **protected** configuration.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="b59d0-176">Risoluzione dei problemi relativi alle estensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b59d0-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="b59d0-177">Ogni estensione macchina virtuale può disporre di passaggi per la risoluzione dei problemi specifici.</span><span class="sxs-lookup"><span data-stu-id="b59d0-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="b59d0-178">Ad esempio, quando si utilizza l'estensione Custom Script hello, dettagli sull'esecuzione di script è reperibile in locale nella macchina virtuale hello in cui è stata eseguita l'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="b59d0-178">For instance, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="b59d0-179">Tutti i passaggi per la risoluzione dei problemi specifici dell'estensione sono descritti in dettaglio nella documentazione specifica dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="b59d0-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="b59d0-180">Hello risoluzione dei problemi relativi alla procedura seguente si applica tooall estensioni delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="b59d0-180">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="b59d0-181">Visualizzare lo stato dell'estensione</span><span class="sxs-lookup"><span data-stu-id="b59d0-181">View extension status</span></span>

<span data-ttu-id="b59d0-182">Dopo l'esecuzione di un'estensione della macchina virtuale in una macchina virtuale, utilizzare hello lo stato dell'estensione tooreturn comando PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="b59d0-182">After a virtual machine extension has been run against a virtual machine, use hello following PowerShell command tooreturn extension status.</span></span> <span data-ttu-id="b59d0-183">Sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="b59d0-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="b59d0-184">Hello `Name` parametro accetta il nome di hello assegnato toohello estensione in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b59d0-184">hello `Name` parameter takes hello name given toohello extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="b59d0-185">output di Hello è simile hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b59d0-185">hello output looks like hello following:</span></span>

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

<span data-ttu-id="b59d0-186">Lo stato dell'esecuzione di estensione può essere rilevata anche in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b59d0-186">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="b59d0-187">stato hello tooview di un'estensione, hello selezionare macchina virtuale, scegliere **estensioni**, e selezionare hello estensione desiderata.</span><span class="sxs-lookup"><span data-stu-id="b59d0-187">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="b59d0-188">Eseguire nuovamente le estensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b59d0-188">Rerun VM extensions</span></span>

<span data-ttu-id="b59d0-189">Potrebbero essere presenti i casi in cui un'estensione della macchina virtuale deve toobe eseguire di nuovo.</span><span class="sxs-lookup"><span data-stu-id="b59d0-189">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="b59d0-190">È possibile farlo rimuovendo estensione hello e quindi eseguire nuovamente estensione hello con un metodo di esecuzione di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="b59d0-190">You can do this by removing hello extension and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="b59d0-191">tooremove un'estensione, eseguire hello comando con il modulo di Azure PowerShell hello seguente.</span><span class="sxs-lookup"><span data-stu-id="b59d0-191">tooremove an extension, run hello following command with hello Azure PowerShell module.</span></span> <span data-ttu-id="b59d0-192">Sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="b59d0-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="b59d0-193">Un'estensione può essere rimosso anche tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b59d0-193">An extension can also be removed using hello Azure portal.</span></span> <span data-ttu-id="b59d0-194">toodo in modo:</span><span class="sxs-lookup"><span data-stu-id="b59d0-194">toodo so:</span></span>

1. <span data-ttu-id="b59d0-195">Selezionare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b59d0-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="b59d0-196">Selezionare **Estensioni**.</span><span class="sxs-lookup"><span data-stu-id="b59d0-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="b59d0-197">Scegliere l'estensione hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="b59d0-197">Choose hello desired extension.</span></span>
4. <span data-ttu-id="b59d0-198">Selezionare **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="b59d0-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="b59d0-199">Riferimento alle estensioni della macchina virtuale comuni</span><span class="sxs-lookup"><span data-stu-id="b59d0-199">Common VM extensions reference</span></span>
| <span data-ttu-id="b59d0-200">Nome estensione</span><span class="sxs-lookup"><span data-stu-id="b59d0-200">Extension name</span></span> | <span data-ttu-id="b59d0-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b59d0-201">Description</span></span> | <span data-ttu-id="b59d0-202">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="b59d0-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b59d0-203">Estensione Script personalizzato per Windows</span><span class="sxs-lookup"><span data-stu-id="b59d0-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="b59d0-204">Eseguire script su una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b59d0-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="b59d0-205">Estensione script personalizzata per Windows</span><span class="sxs-lookup"><span data-stu-id="b59d0-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="b59d0-206">Estensione DSC per Windows</span><span class="sxs-lookup"><span data-stu-id="b59d0-206">DSC Extension for Windows</span></span> |<span data-ttu-id="b59d0-207">Estensione PowerShell DSC (Desired State Configuration)</span><span class="sxs-lookup"><span data-stu-id="b59d0-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="b59d0-208">Estensione DSC per Windows</span><span class="sxs-lookup"><span data-stu-id="b59d0-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="b59d0-209">Estensione di Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="b59d0-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="b59d0-210">Gestisce Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="b59d0-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="b59d0-211">Estensione di Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="b59d0-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="b59d0-212">Estensione dell'accesso alla VM di Azure</span><span class="sxs-lookup"><span data-stu-id="b59d0-212">Azure VM Access Extension</span></span> |<span data-ttu-id="b59d0-213">Gestire gli utenti e le credenziali</span><span class="sxs-lookup"><span data-stu-id="b59d0-213">Manage users and credentials</span></span> |[<span data-ttu-id="b59d0-214">Estensione dell'accesso alle macchine virtuali per Linux</span><span class="sxs-lookup"><span data-stu-id="b59d0-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
