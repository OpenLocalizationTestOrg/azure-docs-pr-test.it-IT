---
title: Panoramica di DSC (Desired State Configuration) per Azure | Microsoft Docs
description: "Panoramica sull'uso del gestore dell'estensione di Microsoft Azure per PowerShell DSC (Desired State Configuration). Inclusi prerequisiti, architettura, cmdlet e così via."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: c05c2d541a5f526f362f9cd72fe6d878374112b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-the-azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="7321b-104">Introduzione al gestore dell'estensione DSC (Desired State Configuration) di Azure</span><span class="sxs-lookup"><span data-stu-id="7321b-104">Introduction to the Azure Desired State Configuration extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="7321b-105">L'agente di macchine virtuali di Azure e le relative estensioni associate fanno parte dei servizi di infrastruttura di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7321b-105">The Azure VM Agent and associated Extensions are part of the Microsoft Azure Infrastructure Services.</span></span> <span data-ttu-id="7321b-106">Le estensioni di VM sono componenti software che estendono la funzionalità di una VM e semplificano varie operazioni di gestione delle VM.</span><span class="sxs-lookup"><span data-stu-id="7321b-106">VM Extensions are software components that extend the VM functionality and simplify various VM management operations.</span></span> <span data-ttu-id="7321b-107">Ad esempio, l'estensione VMAccess consente di reimpostare la password dell'amministratore; l'estensione Script personalizzato invece può essere usata per eseguire uno script nella VM.</span><span class="sxs-lookup"><span data-stu-id="7321b-107">For example, the VMAccess extension can be used to reset an administrator's password, or the Custom Script extension can be used to execute a script on the VM.</span></span>

<span data-ttu-id="7321b-108">Questo articolo illustra l'estensione DSC (Desired State Configuration) PowerShell per le VM di Azure in Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="7321b-108">This article introduces the PowerShell Desired State Configuration (DSC) Extension for Azure VMs as part of the Azure PowerShell SDK.</span></span> <span data-ttu-id="7321b-109">È possibile usare i nuovi cmdlet per caricare e applicare una configurazione DSC PowerShell in una macchina virtuale di Azure abilitata con l'estensione DSC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7321b-109">You can use new cmdlets to upload and apply a PowerShell DSC configuration on an Azure VM enabled with the PowerShell DSC extension.</span></span> <span data-ttu-id="7321b-110">L'estensione DSC PowerShell esegue una chiamata in PowerShell DSC per applicare la configurazione DSC ricevuta nella VM.</span><span class="sxs-lookup"><span data-stu-id="7321b-110">The PowerShell DSC extension calls into PowerShell DSC to enact the received DSC configuration on the VM.</span></span> <span data-ttu-id="7321b-111">Questa funzionalità è disponibile anche tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7321b-111">This functionality is also available through the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7321b-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7321b-112">Prerequisites</span></span>
<span data-ttu-id="7321b-113">**Computer locale** : per interagire con l'estensione della VM di Azure, è necessario usare il portale di Azure o Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="7321b-113">**Local machine** To interact with the Azure VM extension, you need to use either the Azure portal or the Azure PowerShell SDK.</span></span> 

<span data-ttu-id="7321b-114">**Agente guest** : la VM di Azure cui applicare la configurazione DSC deve essere un sistema operativo che supporta Windows Management Framework 4.0 o 5.0.</span><span class="sxs-lookup"><span data-stu-id="7321b-114">**Guest Agent** The Azure VM that is configured by the DSC configuration needs to be an OS that supports either Windows Management Framework (WMF) 4.0 or 5.0.</span></span> <span data-ttu-id="7321b-115">L'elenco completo delle versioni dei sistemi operativi supportati è disponibile nella [cronologia delle versioni dell'estensione DSC](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span><span class="sxs-lookup"><span data-stu-id="7321b-115">The full list of supported OS versions can be found at the [DSC Extension Version History](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span></span>

## <a name="terms-and-concepts"></a><span data-ttu-id="7321b-116">Termini e concetti</span><span class="sxs-lookup"><span data-stu-id="7321b-116">Terms and concepts</span></span>
<span data-ttu-id="7321b-117">Questa guida presuppone che si abbia familiarità con i concetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7321b-117">This guide presumes familiarity with the following concepts:</span></span>

<span data-ttu-id="7321b-118">Configurazione: documento di configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="7321b-118">Configuration - A DSC configuration document.</span></span> 

<span data-ttu-id="7321b-119">Nodo: destinazione per una configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="7321b-119">Node - A target for a DSC configuration.</span></span> <span data-ttu-id="7321b-120">In questo documento, "nodo" fa sempre riferimento a una VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="7321b-120">In this document, "node" always refers to an Azure VM.</span></span>

<span data-ttu-id="7321b-121">Dati di configurazione: file con estensione psd1 contenente i dati ambientali per una configurazione.</span><span class="sxs-lookup"><span data-stu-id="7321b-121">Configuration Data - A .psd1 file containing environmental data for a configuration</span></span>

## <a name="architectural-overview"></a><span data-ttu-id="7321b-122">Panoramica dell'architettura</span><span class="sxs-lookup"><span data-stu-id="7321b-122">Architectural overview</span></span>
<span data-ttu-id="7321b-123">L'estensione DSC di Azure usa il framework dell'agente VM di Azure per recapitare, applicare e generare report sulle configurazioni DSC in esecuzione nelle VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="7321b-123">The Azure DSC extension uses the Azure VM Agent framework to deliver, enact, and report on DSC configurations running on Azure VMs.</span></span> <span data-ttu-id="7321b-124">L'estensione DSC prevede un file ZIP contenente almeno un documento di configurazione e un set di parametri fornito tramite Azure PowerShell SDK oppure tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7321b-124">The DSC extension expects a .zip file containing at least a configuration document, and a set of parameters provided either through the Azure PowerShell SDK or through the Azure portal.</span></span>

<span data-ttu-id="7321b-125">Quando viene chiamata per la prima volta, l'estensione esegue un processo di installazione.</span><span class="sxs-lookup"><span data-stu-id="7321b-125">When the extension is called for the first time, it runs an installation process.</span></span> <span data-ttu-id="7321b-126">Tale processo installa una versione di Windows Management Framework adottando la logica seguente:</span><span class="sxs-lookup"><span data-stu-id="7321b-126">This process installs a version of the Windows Management Framework (WMF) using the following logic:</span></span>

1. <span data-ttu-id="7321b-127">Se il sistema operativo della macchina virtuale di Azure è Windows Server 2016, non viene eseguita alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="7321b-127">If the Azure VM OS is Windows Server 2016, no action is taken.</span></span> <span data-ttu-id="7321b-128">In Windows Server 2016 è già installata la versione più recente di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7321b-128">Windows Server 2016 already has the latest version of PowerShell installed.</span></span>
2. <span data-ttu-id="7321b-129">Se la proprietà `wmfVersion` è specificata, viene installata la versione di WMF corrispondente a meno che non sia incompatibile con il sistema operativo della VM.</span><span class="sxs-lookup"><span data-stu-id="7321b-129">If the `wmfVersion` property is specified, that version of the WMF is installed unless it is incompatible with the VM's OS.</span></span>
3. <span data-ttu-id="7321b-130">Se la proprietà `wmfVersion` non è specificata, viene installata la versione più recente applicabile di WMF.</span><span class="sxs-lookup"><span data-stu-id="7321b-130">If no `wmfVersion` property is specified, the latest applicable version of the WMF is installed.</span></span>

<span data-ttu-id="7321b-131">L'installazione di Windows Management Framework richiede il riavvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="7321b-131">Installation of the WMF requires a reboot.</span></span> <span data-ttu-id="7321b-132">Dopo il riavvio, l'estensione scarica il file .zip specificato nella proprietà `modulesUrl`.</span><span class="sxs-lookup"><span data-stu-id="7321b-132">After reboot, the extension downloads the .zip file specified in the `modulesUrl` property.</span></span> <span data-ttu-id="7321b-133">Se tale percorso si trova nell'archiviazione BLOB di Azure, è possibile specificare un token di firma di accesso condiviso nella proprietà `sasToken` per accedere al file.</span><span class="sxs-lookup"><span data-stu-id="7321b-133">If this location is in Azure blob storage, a SAS token can be specified in the `sasToken` property to access the file.</span></span> <span data-ttu-id="7321b-134">Dopo aver scaricato e decompresso il file .zip, la funzione di configurazione definita in `configurationFunction` viene eseguita per generare il file MOF.</span><span class="sxs-lookup"><span data-stu-id="7321b-134">After the .zip is downloaded and unpacked, the configuration function defined in `configurationFunction` is run to generate the MOF file.</span></span> <span data-ttu-id="7321b-135">L'estensione esegue quindi `Start-DscConfiguration -Force` nel file MOF generato,</span><span class="sxs-lookup"><span data-stu-id="7321b-135">The extension then runs `Start-DscConfiguration -Force` on the generated MOF file.</span></span> <span data-ttu-id="7321b-136">acquisisce l'output e lo riscrive nel canale di stato di Azure.</span><span class="sxs-lookup"><span data-stu-id="7321b-136">The extension captures output and writes it back out to the Azure Status Channel.</span></span> <span data-ttu-id="7321b-137">Da questo momento, Gestione configurazione locale DSC gestisce il monitoraggio e la correzione come di consueto.</span><span class="sxs-lookup"><span data-stu-id="7321b-137">From this point on, the DSC LCM handles monitoring and correction as normal.</span></span> 

## <a name="powershell-cmdlets"></a><span data-ttu-id="7321b-138">Cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="7321b-138">PowerShell cmdlets</span></span>
<span data-ttu-id="7321b-139">I cmdlet di PowerShell possono essere usati con Azure Resource Manager o con il modello di distribuzione classica per creare pacchetti, pubblicare e monitorare le distribuzioni di estensione DSC.</span><span class="sxs-lookup"><span data-stu-id="7321b-139">PowerShell cmdlets can be used with Azure Resource Manager or the classic deployment model to package, publish, and monitor DSC extension deployments.</span></span> <span data-ttu-id="7321b-140">I cmdlet elencati di seguito sono i moduli di distribuzione classica, ma "Azure" può essere sostituito con "AzureRm" per usare il modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7321b-140">The following cmdlets listed are the classic deployment modules, but "Azure" can be replaced with "AzureRm" to use the Azure Resource Manager model.</span></span> <span data-ttu-id="7321b-141">Ad esempio, `Publish-AzureVMDscConfiguration` usa il modello di distribuzione classica, mentre `Publish-AzureRmVMDscConfiguration` usa Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7321b-141">For example,  `Publish-AzureVMDscConfiguration` uses the classic deployment model, where `Publish-AzureRmVMDscConfiguration` uses Azure Resource Manager.</span></span> 

<span data-ttu-id="7321b-142">`Publish-AzureVMDscConfiguration` riceve un file di configurazione, lo analizza per cercare risorse DSC dipendenti e crea un file .zip contenente la configurazione e le risorse DSC necessarie per applicare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="7321b-142">`Publish-AzureVMDscConfiguration` takes in a configuration file, scans it for dependent DSC resources, and creates a .zip file containing the configuration and DSC resources needed to enact the configuration.</span></span> <span data-ttu-id="7321b-143">Può anche creare il pacchetto in locale usando il parametro `-ConfigurationArchivePath`</span><span class="sxs-lookup"><span data-stu-id="7321b-143">It can also create the package locally using the `-ConfigurationArchivePath` parameter.</span></span> <span data-ttu-id="7321b-144">oppure pubblica il file .zip nell'archiviazione BLOB di Azure e lo protegge con un token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="7321b-144">Otherwise, it publishes the .zip file to Azure blob storage and secures it with a SAS token.</span></span>

<span data-ttu-id="7321b-145">Il file ZIP creato da questo cmdlet include lo script di configurazione con estensione ps1 nella radice della cartella di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7321b-145">The .zip file created by this cmdlet has the .ps1 configuration script at the root of the archive folder.</span></span> <span data-ttu-id="7321b-146">Per le risorse, la cartella del modulo è posizionata nella cartella di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7321b-146">Resources have the module folder placed in the archive folder.</span></span> 

<span data-ttu-id="7321b-147">`Set-AzureVMDscExtension` inserisce le impostazioni necessarie per l'estensione DSC di PowerShell in un oggetto di configurazione VM.</span><span class="sxs-lookup"><span data-stu-id="7321b-147">`Set-AzureVMDscExtension` injects the settings needed by the PowerShell DSC extension into a VM configuration object.</span></span> <span data-ttu-id="7321b-148">Nel modello di distribuzione classica è necessario applicare le modifiche di una VM a una VM di Azure con `Update-AzureVM`.</span><span class="sxs-lookup"><span data-stu-id="7321b-148">In the classic deployment model, the VM changes must be applied to an Azure VM with `Update-AzureVM`.</span></span> 

<span data-ttu-id="7321b-149">`Get-AzureVMDscExtension` recupera lo stato dell'estensione DSC di una determinata VM.</span><span class="sxs-lookup"><span data-stu-id="7321b-149">`Get-AzureVMDscExtension` retrieves the DSC extension status of a particular VM.</span></span> 

<span data-ttu-id="7321b-150">`Get-AzureVMDscExtensionStatus` recupera lo stato della configurazione DSC applicata dal gestore dell'estensione DSC.</span><span class="sxs-lookup"><span data-stu-id="7321b-150">`Get-AzureVMDscExtensionStatus` retrieves the status of the DSC configuration enacted by the DSC extension handler.</span></span> <span data-ttu-id="7321b-151">Questa azione può essere eseguita su una singola VM o su un gruppo di VM.</span><span class="sxs-lookup"><span data-stu-id="7321b-151">This action can be performed on a single VM, or group of VMs.</span></span>

<span data-ttu-id="7321b-152">`Remove-AzureVMDscExtension` rimuove il gestore dell'estensione da una determinata macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7321b-152">`Remove-AzureVMDscExtension` removes the extension handler from a given virtual machine.</span></span> <span data-ttu-id="7321b-153">Questo cmdlet **non** rimuove la configurazione, non disinstalla WMF e non modifica le impostazioni applicate nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7321b-153">This cmdlet does **not** remove the configuration, uninstall the WMF, or change the applied settings on the virtual machine.</span></span> <span data-ttu-id="7321b-154">Rimuove soltanto il gestore dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="7321b-154">It only removes the extension handler.</span></span> 

<span data-ttu-id="7321b-155">**Differenze principali tra cmdlet ASM e cmdlet di Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="7321b-155">**Key differences in ASM and Azure Resource Manager cmdlets**</span></span>

* <span data-ttu-id="7321b-156">I cmdlet di Azure Resource Manager sono sincroni,</span><span class="sxs-lookup"><span data-stu-id="7321b-156">Azure Resource Manager cmdlets are synchronous.</span></span> <span data-ttu-id="7321b-157">mentre i cmdlet di Gestione dei servizi di Azure sono asincroni.</span><span class="sxs-lookup"><span data-stu-id="7321b-157">ASM cmdlets are asynchronous.</span></span>
* <span data-ttu-id="7321b-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version e Location sono tutti parametri obbligatori in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7321b-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, and Location are all required parameters in Azure Resource Manager.</span></span>
* <span data-ttu-id="7321b-159">ArchiveResourceGroupName è un nuovo parametro facoltativo per Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7321b-159">ArchiveResourceGroupName is a new optional parameter for Azure Resource Manager.</span></span> <span data-ttu-id="7321b-160">Questo parametro può essere specificato quando l'account di archiviazione appartiene a un gruppo di risorse diverso da quello in cui viene creata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7321b-160">You can specify this parameter when your storage account belongs to a different resource group than the one where the virtual machine is created.</span></span>
* <span data-ttu-id="7321b-161">ConfigurationArchive è denominato ArchiveBlobName in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7321b-161">ConfigurationArchive is called ArchiveBlobName in Azure Resource Manager</span></span>
* <span data-ttu-id="7321b-162">ContainerName è denominato ArchiveContainerName in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7321b-162">ContainerName is called ArchiveContainerName in Azure Resource Manager</span></span>
* <span data-ttu-id="7321b-163">StorageEndpointSuffix è denominato ArchiveStorageEndpointSuffix in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7321b-163">StorageEndpointSuffix is called ArchiveStorageEndpointSuffix in Azure Resource Manager</span></span>
* <span data-ttu-id="7321b-164">L'opzione AutoUpdate è stata aggiunta in Azure Resource Manager per consentire l'aggiornamento automatico del gestore dell'estensione alla versione più recente, non appena disponibile.</span><span class="sxs-lookup"><span data-stu-id="7321b-164">The AutoUpdate switch has been added to Azure Resource Manager to enable automatic updating of the extension handler to the latest version as and when it is available.</span></span> <span data-ttu-id="7321b-165">Si noti che questo parametro potrebbe causare il riavvio della VM quando viene rilasciata una nuova versione di WMF.</span><span class="sxs-lookup"><span data-stu-id="7321b-165">Note this parameter has the potential to cause reboots on the VM when a new version of the WMF is released.</span></span> 

## <a name="azure-portal-functionality"></a><span data-ttu-id="7321b-166">Funzionalità del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7321b-166">Azure portal functionality</span></span>
<span data-ttu-id="7321b-167">Passare a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7321b-167">Browse to a VM.</span></span> <span data-ttu-id="7321b-168">In Impostazioni -> Generale fare clic su "Estensioni".</span><span class="sxs-lookup"><span data-stu-id="7321b-168">Under Settings -> General click "Extensions."</span></span> <span data-ttu-id="7321b-169">Verrà creato un nuovo riquadro.</span><span class="sxs-lookup"><span data-stu-id="7321b-169">A new pane is created.</span></span> <span data-ttu-id="7321b-170">Fare clic su Add e selezionare PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="7321b-170">Click "Add" and select PowerShell DSC.</span></span>

<span data-ttu-id="7321b-171">Il portale richiede un input.</span><span class="sxs-lookup"><span data-stu-id="7321b-171">The portal needs input.</span></span>
<span data-ttu-id="7321b-172">**Configuration Modules or Script**(Moduli o script di configurazione): questo è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="7321b-172">**Configuration Modules or Script**: This field is mandatory.</span></span> <span data-ttu-id="7321b-173">Richiede un file con estensione .ps1 contenente uno script di configurazione oppure un file .zip con uno script di configurazione con estensione ps1 nella directory radice e tutte le risorse dipendenti nelle cartelle del modulo all'interno del file .zip.</span><span class="sxs-lookup"><span data-stu-id="7321b-173">Requires a .ps1 file containing a configuration script, or a .zip file with a .ps1 configuration script at the root, and all dependent resources in module folders within the .zip.</span></span> <span data-ttu-id="7321b-174">Può essere creato con il cmdlet `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` incluso in Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="7321b-174">It can be created with the `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet included in the Azure PowerShell SDK.</span></span> <span data-ttu-id="7321b-175">Il file .zip viene caricato nell'archiviazione BLOB dell'utente protetta da un token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="7321b-175">The .zip file is uploaded into your user blob storage secured by a SAS token.</span></span> 

<span data-ttu-id="7321b-176">**Configuration Data PSD1 File**(File PSD1 dati di configurazione): questo è un campo facoltativo.</span><span class="sxs-lookup"><span data-stu-id="7321b-176">**Configuration Data PSD1 File**: This field is optional.</span></span> <span data-ttu-id="7321b-177">Se la configurazione usata richiede un file di dati della configurazione con estensione .psd1, usare questo campo per selezionarlo e quindi caricarlo nell'archiviazione BLOB dell'utente, in cui sarà protetto da un token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="7321b-177">If your configuration requires a configuration data file in .psd1, use this field to select it and upload it to your user blob storage, where it is secured by a SAS token.</span></span> 

<span data-ttu-id="7321b-178">**Module-Qualified Name of Configuration**: i file con estensione .ps1 possono avere più funzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="7321b-178">**Module-Qualified Name of Configuration**: .ps1 files can have multiple configuration functions.</span></span> <span data-ttu-id="7321b-179">Immettere il nome dello script di configurazione con estensione ps1 seguito da '\' e dal nome della funzione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="7321b-179">Enter the name of the configuration .ps1 script followed by a  '\' and the name of the configuration function.</span></span> <span data-ttu-id="7321b-180">Ad esempio, se lo script con estensione .ps1 ha il nome "configuration.ps1" e la configurazione è "IisInstall", immettere: `configuration.ps1\IisInstall`</span><span class="sxs-lookup"><span data-stu-id="7321b-180">For example, if your .ps1 script has the name "configuration.ps1", and the configuration is "IisInstall", you would enter: `configuration.ps1\IisInstall`</span></span>

<span data-ttu-id="7321b-181">**Configuration Arguments**: se la funzione di configurazione accetta argomenti, immetterli qui nel formato `argumentName1=value1,argumentName2=value2`.</span><span class="sxs-lookup"><span data-stu-id="7321b-181">**Configuration Arguments**: If the configuration function takes arguments, enter them in here in the format `argumentName1=value1,argumentName2=value2`.</span></span> <span data-ttu-id="7321b-182">Questo formato è diverso rispetto a quello in cui vengono accettati gli argomenti di configurazione tramite i cmdlet di PowerShell o i modelli di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7321b-182">Note this format is a different format than how configuration arguments are accepted through PowerShell cmdlets or Resource Manager templates.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="7321b-183">Introduzione</span><span class="sxs-lookup"><span data-stu-id="7321b-183">Getting started</span></span>
<span data-ttu-id="7321b-184">L'estensione DSC di Azure riceve i documenti di configurazione DSC e li applica nelle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="7321b-184">The Azure DSC extension takes in DSC configuration documents and enacts them on Azure VMs.</span></span> <span data-ttu-id="7321b-185">Di seguito è riportato un semplice esempio di configurazione.</span><span class="sxs-lookup"><span data-stu-id="7321b-185">A simple example of a configuration follows.</span></span> <span data-ttu-id="7321b-186">Salvarlo in locale come "IisInstall.ps1":</span><span class="sxs-lookup"><span data-stu-id="7321b-186">Save it locally as "IisInstall.ps1":</span></span>

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

<span data-ttu-id="7321b-187">La procedura seguente posiziona lo script IisInstall.ps1 nella VM specificata, esegue la configurazione e invia un report sullo stato.</span><span class="sxs-lookup"><span data-stu-id="7321b-187">The following steps place the IisInstall.ps1 script on the specified VM, execute the configuration, and report back on status.</span></span>
###<a name="classic-model"></a><span data-ttu-id="7321b-188">Modello classico</span><span class="sxs-lookup"><span data-stu-id="7321b-188">Classic model</span></span>
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish the configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set the VM to run the DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update the configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a><span data-ttu-id="7321b-189">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7321b-189">Azure Resource Manager model</span></span>

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish the configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set the VM to run the DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a><span data-ttu-id="7321b-190">Registrazione</span><span class="sxs-lookup"><span data-stu-id="7321b-190">Logging</span></span>
<span data-ttu-id="7321b-191">I log vengono inseriti in:</span><span class="sxs-lookup"><span data-stu-id="7321b-191">Logs are placed in:</span></span>

<span data-ttu-id="7321b-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Numero versione]</span><span class="sxs-lookup"><span data-stu-id="7321b-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span></span>

## <a name="next-steps"></a><span data-ttu-id="7321b-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7321b-193">Next steps</span></span>
<span data-ttu-id="7321b-194">Per altre informazioni su PowerShell DSC, [vedere il centro di documentazione di PowerShell](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="7321b-194">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="7321b-195">Esaminare il [modello di Azure Resource Manager per l'estensione DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7321b-195">Examine the [Azure Resource Manager template for the DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="7321b-196">Per trovare altre funzionalità che è possibile gestire con PowerShell DSC, [cercare in PowerShell Gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) altre risorse DSC.</span><span class="sxs-lookup"><span data-stu-id="7321b-196">To find additional functionality you can manage with PowerShell DSC, [browse the PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

<span data-ttu-id="7321b-197">Per altre informazioni sul passaggio di parametri sensibili nelle configurazioni, vedere l'articolo [Gestione sicura delle credenziali con il gestore estensione DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7321b-197">For details on passing sensitive parameters into configurations, see [Manage credentials securely with the DSC extension handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

