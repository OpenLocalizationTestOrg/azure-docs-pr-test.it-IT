---
title: "Estensioni e funzionalità delle macchine virtuali per Windows in Azure | Documentazione Microsoft"
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
ms.openlocfilehash: 1ce0eebd2585c9457d7f922898d7f2fa3e7ffad7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="607ee-103">Estensioni e funzionalità della macchina virtuale per Windows</span><span class="sxs-lookup"><span data-stu-id="607ee-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="607ee-104">Le estensioni della macchina virtuale di Azure sono piccole applicazioni che eseguono attività di configurazione e automazione post-distribuzione sulle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="607ee-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="607ee-105">Ad esempio, se una macchina virtuale richiede l'installazione di software, la protezione antivirus o la configurazione di Docker, è possibile usare un'estensione di macchina virtuale per completare queste attività.</span><span class="sxs-lookup"><span data-stu-id="607ee-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span></span> <span data-ttu-id="607ee-106">Le estensioni della macchina virtuale di Azure possono essere eseguite tramite l'interfaccia della riga di comando di Azure, PowerShell, i modelli di Azure Resource Manager e il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="607ee-106">Azure VM extensions can be run by using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span> <span data-ttu-id="607ee-107">Le estensioni possono essere unite in bundle con una nuova distribuzione di macchina virtuale o eseguite su un sistema esistente.</span><span class="sxs-lookup"><span data-stu-id="607ee-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="607ee-108">Questo documento fornisce una panoramica delle estensioni macchina virtuale, i prerequisiti per l'uso delle estensioni macchina virtuale e le indicazioni su come rilevare, gestire e rimuovere le estensioni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="607ee-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how to detect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="607ee-109">Questo documento fornisce informazioni generali perché sono disponibili molte estensioni della macchina virtuale, ognuna con una configurazione potenzialmente univoca.</span><span class="sxs-lookup"><span data-stu-id="607ee-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="607ee-110">I dettagli sono disponibili nel documento specifico della singola estensione.</span><span class="sxs-lookup"><span data-stu-id="607ee-110">Extension-specific details can be found in each document specific to the individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="607ee-111">Casi d'uso ed esempi</span><span class="sxs-lookup"><span data-stu-id="607ee-111">Use cases and samples</span></span>

<span data-ttu-id="607ee-112">Sono disponibili numerose estensioni della macchina virtuale di Azure, ognuna con un caso d'uso specifico.</span><span class="sxs-lookup"><span data-stu-id="607ee-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="607ee-113">Alcuni esempi di casi d'uso sono:</span><span class="sxs-lookup"><span data-stu-id="607ee-113">Some example use cases are:</span></span>

- <span data-ttu-id="607ee-114">Applicare le configurazioni dello stato desiderato tramite PowerShell a una macchina virtuale usando l'estensione DSC per Windows.</span><span class="sxs-lookup"><span data-stu-id="607ee-114">Apply PowerShell Desired State configurations to a virtual machine by using the DSC extension for Windows.</span></span> <span data-ttu-id="607ee-115">Per altre informazioni, vedere l'argomento relativo all'[Estensione DSC (Desired State Configuration) di Azure](extensions-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="607ee-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="607ee-116">Configurare il monitoraggio di una macchina virtuale con l'estensione della macchina virtuale di Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="607ee-116">Configure virtual machine monitoring by using the Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="607ee-117">Per altre informazioni, vedere l'argomento [Connettere macchine virtuali di Azure a Log Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="607ee-117">For more information, see [Connect Azure virtual machines to Log Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="607ee-118">Configurare il monitoraggio dell'infrastruttura di Azure con l'estensione Datadog.</span><span class="sxs-lookup"><span data-stu-id="607ee-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span></span> <span data-ttu-id="607ee-119">Per altre informazioni, vedere il [blog Datadog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="607ee-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="607ee-120">Configurare una macchina virtuale di Azure con Chef.</span><span class="sxs-lookup"><span data-stu-id="607ee-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="607ee-121">Per altre informazioni, vedere l'argomento [Automazione della distribuzione delle macchine virtuali di Azure con Chef](chef-automation.md)</span><span class="sxs-lookup"><span data-stu-id="607ee-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="607ee-122">Oltre alle estensioni specifiche del processo, è disponibile un'estensione Script personalizzato per le macchine virtuali Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="607ee-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="607ee-123">L'estensione Script personalizzato per Windows consente l'esecuzione di qualsiasi script PowerShell su una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="607ee-123">The Custom Script extension for Windows allows any PowerShell script to be run on a virtual machine.</span></span> <span data-ttu-id="607ee-124">È utile per la progettazione di distribuzioni di Azure che richiedono una configurazione oltre a quella offerta dagli strumenti nativi di Azure.</span><span class="sxs-lookup"><span data-stu-id="607ee-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="607ee-125">Per altre informazioni, vedere [Estensione Script personalizzato per macchine virtuali Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="607ee-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="607ee-126">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="607ee-126">Prerequisites</span></span>

<span data-ttu-id="607ee-127">Ogni estensione macchina virtuale può avere un insieme specifico di prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="607ee-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="607ee-128">Ad esempio, un prerequisito dell'estensione della macchina virtuale Docker è una distribuzione Linux supportata.</span><span class="sxs-lookup"><span data-stu-id="607ee-128">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="607ee-129">La documentazione specifica dell'estensione illustra in dettaglio i requisiti delle singole estensioni.</span><span class="sxs-lookup"><span data-stu-id="607ee-129">Requirements of individual extensions are detailed in the extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="607ee-130">Agente di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="607ee-130">Azure VM agent</span></span>
<span data-ttu-id="607ee-131">L'agente di macchine virtuali di Azure gestisce l'interazione tra una macchina virtuale di Azure e il controller di infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="607ee-131">The Azure VM agent manages interaction between an Azure virtual machine and the Azure fabric controller.</span></span> <span data-ttu-id="607ee-132">L'agente di macchine virtuali è responsabile di molti aspetti funzionali della distribuzione e della gestione delle macchine virtuali di Azure, tra cui l'esecuzione delle estensioni delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="607ee-132">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="607ee-133">L'agente di macchine virtuali di Azure è preinstallato nelle immagini di Azure Marketplace e può essere installato nei sistemi operativi supportati.</span><span class="sxs-lookup"><span data-stu-id="607ee-133">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="607ee-134">Per informazioni sui sistemi operativi supportati e per le istruzioni di installazione, vedere [Agente delle macchine virtuali di Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="607ee-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="607ee-135">Individuare le estensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="607ee-135">Discover VM extensions</span></span>
<span data-ttu-id="607ee-136">Molte estensioni delle macchine virtuali di diverso tipo sono disponibili per l'uso con macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="607ee-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="607ee-137">Per visualizzare un elenco completo, eseguire il comando seguente con il modulo Azure Resource Manager di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="607ee-137">To see a complete list, run the following command with the Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="607ee-138">Assicurarsi di specificare il percorso desiderato quando si esegue questo comando.</span><span class="sxs-lookup"><span data-stu-id="607ee-138">Make sure to specify the desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="607ee-139">Eseguire le estensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="607ee-139">Run VM extensions</span></span>

<span data-ttu-id="607ee-140">Le estensioni della macchina virtuale di Azure possono essere eseguite nelle macchine virtuali esistenti e sono utili quando è necessario apportare modifiche alla configurazione o ripristinare la connettività in una VM già distribuita.</span><span class="sxs-lookup"><span data-stu-id="607ee-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="607ee-141">Le estensioni della macchina virtuale possono essere anche unite in bundle con le distribuzioni del modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="607ee-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="607ee-142">L'uso delle estensioni con i modelli di Resource Manager consente di distribuire e configurare le macchine virtuali di Azure senza che sia necessario l'intervento post-distribuzione.</span><span class="sxs-lookup"><span data-stu-id="607ee-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines to be deployed and configured without the need for post-deployment intervention.</span></span>

<span data-ttu-id="607ee-143">Per eseguire un'estensione in una macchina virtuale esistente, è possibile usare i metodi seguenti.</span><span class="sxs-lookup"><span data-stu-id="607ee-143">The following methods can be used to run an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="607ee-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="607ee-144">PowerShell</span></span>

<span data-ttu-id="607ee-145">Molti comandi di PowerShell vengono utilizzati per l'esecuzione di estensioni singole.</span><span class="sxs-lookup"><span data-stu-id="607ee-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="607ee-146">Per visualizzare un elenco, eseguire i seguenti comandi PowerShell.</span><span class="sxs-lookup"><span data-stu-id="607ee-146">To see a list, run the following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="607ee-147">L'output generato sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="607ee-147">This provides output similar to the following:</span></span>

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

<span data-ttu-id="607ee-148">Nell'esempio seguente si utilizza l'estensione Script personalizzato per scaricare uno script da un archivio GitHub nella macchina virtuale di destinazione e quindi eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="607ee-148">The following example uses the Custom Script extension to download a script from a GitHub repository onto the target virtual machine and then run the script.</span></span> <span data-ttu-id="607ee-149">Per altre informazioni sull'estensione Script personalizzato, vedere [Custom Script extension overview](extensions-customscript.md) (Panoramica delle estensioni dello script personalizzato).</span><span class="sxs-lookup"><span data-stu-id="607ee-149">For more information on the Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="607ee-150">In questo esempio, l'estensione Accesso alla macchina virtuale viene usata per reimpostare la password amministrativa di una macchina virtuale Windows.</span><span class="sxs-lookup"><span data-stu-id="607ee-150">In this example, the VM Access extension is used to reset the administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="607ee-151">Per altre informazioni sull'estensione Accesso alla macchina virtuale, vedere [Reset Remote Desktop service in a Windows VM](reset-rdp.md) (Reimpostare il servizio Desktop Remoto in una macchina virtuale Windows).</span><span class="sxs-lookup"><span data-stu-id="607ee-151">For more information on the VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="607ee-152">Il comando `Set-AzureRmVMExtension` può essere utilizzato per avviare qualsiasi estensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="607ee-152">The `Set-AzureRmVMExtension` command can be used to start any VM extension.</span></span> <span data-ttu-id="607ee-153">Per altre informazioni, vedere il [riferimento Set-AzureRmVMExtension](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="607ee-153">For more information, see the [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="607ee-154">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="607ee-154">Azure portal</span></span>

<span data-ttu-id="607ee-155">Un'estensione macchina virtuale può essere applicata a una macchina virtuale esistente tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="607ee-155">A VM extension can be applied to an existing virtual machine through the Azure portal.</span></span> <span data-ttu-id="607ee-156">A tale scopo, selezionare la macchina virtuale che si desidera utilizzare, scegliere **Estensioni** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="607ee-156">To do so, select the virtual machine you want to use, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="607ee-157">In questo modo si ottiene un elenco di estensioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="607ee-157">This provides a list of available extensions.</span></span> <span data-ttu-id="607ee-158">Selezionare quella desiderata, quindi seguire le istruzioni nella procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="607ee-158">Select the one you want and follow the steps in the wizard.</span></span>

<span data-ttu-id="607ee-159">L'immagine seguente illustra l'installazione dell'estensione Microsoft Antimalware dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="607ee-159">The following image shows the installation of the Microsoft Antimalware extension from the Azure portal.</span></span>

![Installare un'estensione antimalware](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="607ee-161">Modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="607ee-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="607ee-162">Le estensioni macchina virtuale possono essere aggiunte a un modello di Azure Resource Manager ed eseguite con la distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="607ee-162">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span></span> <span data-ttu-id="607ee-163">La distribuzione di estensioni con un modello è utile per la creazione di distribuzioni di Azure completamente configurate.</span><span class="sxs-lookup"><span data-stu-id="607ee-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="607ee-164">Ad esempio, il codice JSON seguente viene eseguito da un modello di Resource Manager che consente di distribuire un set di macchine virtuali con carico bilanciato e un database SQL di Azure, quindi installa un'applicazione .NET Core in ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="607ee-164">For example, the following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="607ee-165">L'estensione della macchina virtuale gestisce l'installazione del software.</span><span class="sxs-lookup"><span data-stu-id="607ee-165">The VM extension takes care of the software installation.</span></span>

<span data-ttu-id="607ee-166">Per altre informazioni, vedere il [modello di Resource Manager completo](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="607ee-166">For more information, see the [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

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

<span data-ttu-id="607ee-167">Per altre informazioni, vedere [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions) (Creazione di modelli di Azure Resource Manager con le estensioni della macchina virtuale Windows).</span><span class="sxs-lookup"><span data-stu-id="607ee-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="607ee-168">Proteggere i dati dell'estensione della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="607ee-168">Secure VM extension data</span></span>

<span data-ttu-id="607ee-169">Quando si esegue un'estensione macchina virtuale, potrebbe essere necessario includere informazioni riservate, ad esempio le credenziali, i nomi degli account di archiviazione e le chiavi di accesso dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="607ee-169">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="607ee-170">Molte estensioni della macchina virtuale includono una configurazione protetta, che consente di crittografare dati e di decrittografarli solo all'interno della macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="607ee-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span></span> <span data-ttu-id="607ee-171">Ogni estensione ha uno schema di configurazione protetto specifico che sarà descritto in maniera dettagliata nella documentazione specifica dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="607ee-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="607ee-172">L'esempio seguente illustra un'istanza dell'estensione Script personalizzato per Windows.</span><span class="sxs-lookup"><span data-stu-id="607ee-172">The following example shows an instance of the Custom Script extension for Windows.</span></span> <span data-ttu-id="607ee-173">Si noti che il comando da eseguire include un insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="607ee-173">Notice that the command to execute includes a set of credentials.</span></span> <span data-ttu-id="607ee-174">In questo esempio, il comando da eseguire non verrà crittografato.</span><span class="sxs-lookup"><span data-stu-id="607ee-174">In this example, the command to execute will not be encrypted.</span></span>


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

<span data-ttu-id="607ee-175">Proteggere la stringa di esecuzione spostando la proprietà **comando da eseguire** nella configurazione **protetta**.</span><span class="sxs-lookup"><span data-stu-id="607ee-175">Secure the execution string by moving the **command to execute** property to the **protected** configuration.</span></span>

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

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="607ee-176">Risoluzione dei problemi relativi alle estensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="607ee-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="607ee-177">Ogni estensione macchina virtuale può disporre di passaggi per la risoluzione dei problemi specifici.</span><span class="sxs-lookup"><span data-stu-id="607ee-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="607ee-178">Ad esempio, quando si usa l'estensione script personalizzato, i dettagli sull'esecuzione dello script sono reperibili in locale nella macchina virtuale in cui è stata eseguita l'estensione.</span><span class="sxs-lookup"><span data-stu-id="607ee-178">For instance, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span></span> <span data-ttu-id="607ee-179">Tutti i passaggi per la risoluzione dei problemi specifici dell'estensione sono descritti in dettaglio nella documentazione specifica dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="607ee-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="607ee-180">I passaggi per la risoluzione dei problemi seguenti si applicano a tutte le estensioni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="607ee-180">The following troubleshooting steps apply to all virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="607ee-181">Visualizzare lo stato dell'estensione</span><span class="sxs-lookup"><span data-stu-id="607ee-181">View extension status</span></span>

<span data-ttu-id="607ee-182">Dopo l'esecuzione dell'estensione di una macchina virtuale, usare il comando seguente di PowerShell per restituire lo stato dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="607ee-182">After a virtual machine extension has been run against a virtual machine, use the following PowerShell command to return extension status.</span></span> <span data-ttu-id="607ee-183">Sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="607ee-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="607ee-184">Il parametro `Name` accetta il nome specificato per l'estensione durante l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="607ee-184">The `Name` parameter takes the name given to the extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="607ee-185">L'output è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="607ee-185">The output looks like the following:</span></span>

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

<span data-ttu-id="607ee-186">Lo stato di esecuzione dell'estensione è disponibile anche nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="607ee-186">Extension execution status can also be found in the Azure portal.</span></span> <span data-ttu-id="607ee-187">Per visualizzare lo stato di un'estensione, selezionare la macchina virtuale, scegliere **Estensioni** e selezionare l'estensione desiderata.</span><span class="sxs-lookup"><span data-stu-id="607ee-187">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="607ee-188">Eseguire nuovamente le estensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="607ee-188">Rerun VM extensions</span></span>

<span data-ttu-id="607ee-189">In alcuni casi potrebbe essere necessario rieseguire un'estensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="607ee-189">There may be cases in which a virtual machine extension needs to be rerun.</span></span> <span data-ttu-id="607ee-190">È possibile farlo rimuovendo l'estensione e quindi eseguendo di nuovo l'estensione con il metodo di esecuzione scelto.</span><span class="sxs-lookup"><span data-stu-id="607ee-190">You can do this by removing the extension and then rerunning the extension with an execution method of your choice.</span></span> <span data-ttu-id="607ee-191">Per rimuovere un'estensione, eseguire il comando seguente con il modulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="607ee-191">To remove an extension, run the following command with the Azure PowerShell module.</span></span> <span data-ttu-id="607ee-192">Sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="607ee-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="607ee-193">Un'estensione può essere eliminata anche tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="607ee-193">An extension can also be removed using the Azure portal.</span></span> <span data-ttu-id="607ee-194">A tale scopo, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="607ee-194">To do so:</span></span>

1. <span data-ttu-id="607ee-195">Selezionare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="607ee-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="607ee-196">Selezionare **Estensioni**.</span><span class="sxs-lookup"><span data-stu-id="607ee-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="607ee-197">Selezionare l'estensione desiderata.</span><span class="sxs-lookup"><span data-stu-id="607ee-197">Choose the desired extension.</span></span>
4. <span data-ttu-id="607ee-198">Selezionare **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="607ee-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="607ee-199">Riferimento alle estensioni della macchina virtuale comuni</span><span class="sxs-lookup"><span data-stu-id="607ee-199">Common VM extensions reference</span></span>
| <span data-ttu-id="607ee-200">Nome estensione</span><span class="sxs-lookup"><span data-stu-id="607ee-200">Extension name</span></span> | <span data-ttu-id="607ee-201">Descrizione</span><span class="sxs-lookup"><span data-stu-id="607ee-201">Description</span></span> | <span data-ttu-id="607ee-202">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="607ee-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="607ee-203">Estensione Script personalizzato per Windows</span><span class="sxs-lookup"><span data-stu-id="607ee-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="607ee-204">Eseguire script su una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="607ee-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="607ee-205">Estensione script personalizzata per Windows</span><span class="sxs-lookup"><span data-stu-id="607ee-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="607ee-206">Estensione DSC per Windows</span><span class="sxs-lookup"><span data-stu-id="607ee-206">DSC Extension for Windows</span></span> |<span data-ttu-id="607ee-207">Estensione PowerShell DSC (Desired State Configuration)</span><span class="sxs-lookup"><span data-stu-id="607ee-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="607ee-208">Estensione DSC per Windows</span><span class="sxs-lookup"><span data-stu-id="607ee-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="607ee-209">Estensione di Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="607ee-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="607ee-210">Gestisce Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="607ee-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="607ee-211">Estensione di Diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="607ee-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="607ee-212">Estensione dell'accesso alla VM di Azure</span><span class="sxs-lookup"><span data-stu-id="607ee-212">Azure VM Access Extension</span></span> |<span data-ttu-id="607ee-213">Gestire gli utenti e le credenziali</span><span class="sxs-lookup"><span data-stu-id="607ee-213">Manage users and credentials</span></span> |[<span data-ttu-id="607ee-214">Estensione dell'accesso alle macchine virtuali per Linux</span><span class="sxs-lookup"><span data-stu-id="607ee-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
