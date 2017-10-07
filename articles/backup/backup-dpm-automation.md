---
title: Backup - utilizzo di PowerShell tooback dei carichi di lavoro DPM aaaAzure | Documenti Microsoft
description: Informazioni su come toodeploy e gestire il Backup di Azure per Data Protection Manager (DPM) tramite PowerShell
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 27d2b4b3127b68c9da564697eb61dc3ccbc34b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="a18bc-103">Distribuire e gestire backup tooAzure per i server di Data Protection Manager (DPM) mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="a18bc-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a18bc-104">ARM</span><span class="sxs-lookup"><span data-stu-id="a18bc-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="a18bc-105">Classico</span><span class="sxs-lookup"><span data-stu-id="a18bc-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="a18bc-106">In questo articolo illustra come toosetup PowerShell toouse Backup di Azure in un server DPM e toomanage backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="a18bc-106">This article shows you how toouse PowerShell toosetup Azure Backup on a DPM server, and toomanage backup and recovery.</span></span>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="a18bc-107">Impostazione di ambiente PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="a18bc-107">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="a18bc-108">Prima di poter utilizzare PowerShell toomanage backup da Data Protection Manager tooAzure, è necessario toohave hello destra ambiente PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a18bc-108">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="a18bc-109">All'inizio di hello della sessione di PowerShell hello, assicurarsi di eseguire hello seguenti moduli destra di comando tooimport hello e consentono di determinare i cmdlet DPM toocorrectly riferimento hello:</span><span class="sxs-lookup"><span data-stu-id="a18bc-109">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="a18bc-110">Installazione e registrazione</span><span class="sxs-lookup"><span data-stu-id="a18bc-110">Setup and Registration</span></span>
<span data-ttu-id="a18bc-111">toobegin:</span><span class="sxs-lookup"><span data-stu-id="a18bc-111">toobegin:</span></span>

1. <span data-ttu-id="a18bc-112">[Scaricare la versione più recente di PowerShell](https://github.com/Azure/azure-powershell/releases) (versione minima richiesta: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="a18bc-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="a18bc-113">Abilitare i commandlet del Backup di Azure hello passando troppo*AzureResourceManager* modalità tramite hello **Switch-AzureMode** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a18bc-113">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="a18bc-114">Hello seguente programma di installazione e le attività di registrazione può essere automatizzata con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a18bc-114">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="a18bc-115">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="a18bc-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="a18bc-116">Installare hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="a18bc-116">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="a18bc-117">Registrazione con hello servizio Azure Backup</span><span class="sxs-lookup"><span data-stu-id="a18bc-117">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="a18bc-118">Impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="a18bc-118">Networking settings</span></span>
* <span data-ttu-id="a18bc-119">Impostazioni crittografia</span><span class="sxs-lookup"><span data-stu-id="a18bc-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="a18bc-120">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="a18bc-120">Create a recovery services vault</span></span>
<span data-ttu-id="a18bc-121">Hello alla procedura seguente per facilitare la creazione di un insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="a18bc-121">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="a18bc-122">Un insieme di credenziali dei servizi di ripristino è diverso da un insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="a18bc-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="a18bc-123">Se si utilizza Azure Backup per hello prima volta, è necessario utilizzare hello **registro AzureRMResourceProvider** provider di servizi di ripristino di Azure di cmdlet tooregister hello con la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a18bc-123">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="a18bc-124">Hello insieme di credenziali di servizi di ripristino è una risorsa ARM, pertanto è necessario tooplace all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a18bc-124">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="a18bc-125">È possibile usare un gruppo di risorse esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="a18bc-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="a18bc-126">Quando si crea un nuovo gruppo di risorse, specificare il nome di hello e il percorso per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-126">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="a18bc-127">Hello utilizzare **New AzureRmRecoveryServicesVault** toocreate cmdlet un nuovo insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="a18bc-127">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate a new vault.</span></span> <span data-ttu-id="a18bc-128">Assicurarsi che toospecify hello stesso percorso per l'insieme di credenziali hello utilizzata per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-128">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="a18bc-129">Specificare il tipo di hello di toouse di ridondanza di archiviazione; è possibile utilizzare [archiviazione con ridondanza locale (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) o [archiviazione con ridondanza geografica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="a18bc-129">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="a18bc-130">Hello riportato di seguito hello - BackupStorageRedundancy per testVault impostazione tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="a18bc-130">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="a18bc-131">Molti cmdlet di Azure Backup richiede l'oggetto insieme di credenziali di servizi di ripristino hello come input.</span><span class="sxs-lookup"><span data-stu-id="a18bc-131">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="a18bc-132">Per questo motivo, è utile toostore hello servizi di ripristino di Backup dell'insieme di credenziali oggetto in una variabile.</span><span class="sxs-lookup"><span data-stu-id="a18bc-132">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="a18bc-133">Visualizza gli insiemi di credenziali hello in una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="a18bc-133">View hello vaults in a subscription</span></span>
<span data-ttu-id="a18bc-134">Utilizzare **Get AzureRmRecoveryServicesVault** elenco hello tooview di tutti gli insiemi di credenziali nella sottoscrizione corrente hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-134">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="a18bc-135">È possibile utilizzare questo toocheck di comando che è stato creato un nuovo insieme di credenziali o toosee quali insiemi di credenziali sono disponibili nella sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-135">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="a18bc-136">Comando hello, Get-AzureRmRecoveryServicesVault, e sono elencati tutti gli insiemi di credenziali di sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-136">Run hello command, Get-AzureRmRecoveryServicesVault, and all vaults in hello subscription are listed.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="a18bc-137">Installazione agente Azure Backup hello in un Server DPM</span><span class="sxs-lookup"><span data-stu-id="a18bc-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="a18bc-138">Prima di installare l'agente Azure Backup hello, è necessario il programma di installazione di toohave hello scaricato e presenti sul Server di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="a18bc-139">È possibile ottenere una versione più recente di hello del programma di installazione hello da hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) o dalla pagina Dashboard dell'insieme di credenziali hello servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="a18bc-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="a18bc-140">Salvare installer hello tooan posizione facilmente accessibile, ad esempio * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="a18bc-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="a18bc-141">esecuzione comando in una console di PowerShell con privilegi elevata seguente hello tooinstall agente hello **nel server DPM hello**:</span><span class="sxs-lookup"><span data-stu-id="a18bc-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="a18bc-142">Consente di installare agente hello con tutte le opzioni predefinite di hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="a18bc-143">installazione di Hello richiede alcuni minuti in background hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="a18bc-144">Se non si specifica hello */nu* hello opzione **Windows Update** verrà visualizzata la finestra alla fine hello hello toocheck di installazione per tutti gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="a18bc-144">If you do not specify hello */nu* option hello **Windows Update** window opens at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="a18bc-145">agente Hello viene visualizzato nell'elenco di hello dei programmi installati.</span><span class="sxs-lookup"><span data-stu-id="a18bc-145">hello agent shows up in hello list of installed programs.</span></span> <span data-ttu-id="a18bc-146">elenco di hello toosee dei programmi installati, andare troppo**Pannello di controllo** > **programmi** > **programmi e funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="a18bc-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente installato](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="a18bc-148">Opzioni di installazione</span><span class="sxs-lookup"><span data-stu-id="a18bc-148">Installation options</span></span>
<span data-ttu-id="a18bc-149">toosee tutte le opzioni di hello disponibile tramite hello della riga di comando, utilizzare hello seguente comando:</span><span class="sxs-lookup"><span data-stu-id="a18bc-149">toosee all hello options available via hello commandline, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="a18bc-150">Hello le opzioni disponibili includono:</span><span class="sxs-lookup"><span data-stu-id="a18bc-150">hello available options include:</span></span>

| <span data-ttu-id="a18bc-151">Opzione</span><span class="sxs-lookup"><span data-stu-id="a18bc-151">Option</span></span> | <span data-ttu-id="a18bc-152">Dettagli</span><span class="sxs-lookup"><span data-stu-id="a18bc-152">Details</span></span> | <span data-ttu-id="a18bc-153">Default</span><span class="sxs-lookup"><span data-stu-id="a18bc-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a18bc-154">/q</span><span class="sxs-lookup"><span data-stu-id="a18bc-154">/q</span></span> |<span data-ttu-id="a18bc-155">Installazione non interattiva</span><span class="sxs-lookup"><span data-stu-id="a18bc-155">Quiet installation</span></span> |- |
| <span data-ttu-id="a18bc-156">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="a18bc-156">/p:"location"</span></span> |<span data-ttu-id="a18bc-157">Cartella di installazione toohello percorso per l'agente Azure Backup hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="a18bc-158">C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a18bc-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="a18bc-159">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="a18bc-159">/s:"location"</span></span> |<span data-ttu-id="a18bc-160">Cartella cache toohello percorso per l'agente Azure Backup hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="a18bc-161">C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure\Scratch</span><span class="sxs-lookup"><span data-stu-id="a18bc-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="a18bc-162">/m</span><span class="sxs-lookup"><span data-stu-id="a18bc-162">/m</span></span> |<span data-ttu-id="a18bc-163">Consenso esplicito tooMicrosoft aggiornamento</span><span class="sxs-lookup"><span data-stu-id="a18bc-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="a18bc-164">/nu</span><span class="sxs-lookup"><span data-stu-id="a18bc-164">/nu</span></span> |<span data-ttu-id="a18bc-165">Al termine dell'installazione non vengono cercati gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="a18bc-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="a18bc-166">/d</span><span class="sxs-lookup"><span data-stu-id="a18bc-166">/d</span></span> |<span data-ttu-id="a18bc-167">Disinstalla l'agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a18bc-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="a18bc-168">/ph</span><span class="sxs-lookup"><span data-stu-id="a18bc-168">/ph</span></span> |<span data-ttu-id="a18bc-169">Indirizzo host proxy</span><span class="sxs-lookup"><span data-stu-id="a18bc-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="a18bc-170">/po</span><span class="sxs-lookup"><span data-stu-id="a18bc-170">/po</span></span> |<span data-ttu-id="a18bc-171">Numero porta host proxy</span><span class="sxs-lookup"><span data-stu-id="a18bc-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="a18bc-172">/pu</span><span class="sxs-lookup"><span data-stu-id="a18bc-172">/pu</span></span> |<span data-ttu-id="a18bc-173">Nome utente host proxy</span><span class="sxs-lookup"><span data-stu-id="a18bc-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="a18bc-174">/pw</span><span class="sxs-lookup"><span data-stu-id="a18bc-174">/pw</span></span> |<span data-ttu-id="a18bc-175">Password proxy</span><span class="sxs-lookup"><span data-stu-id="a18bc-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-tooa-recovery-services-vault"></a><span data-ttu-id="a18bc-176">Registrazione di Data Protection Manager tooa insieme di credenziali di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="a18bc-176">Registering DPM tooa Recovery Services Vault</span></span>
<span data-ttu-id="a18bc-177">Dopo la creazione di credenziali di servizi di ripristino hello, scaricare l'ultima versione dell'agente hello e l'insieme di credenziali hello e archiviarlo in una posizione comoda come C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="a18bc-177">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="a18bc-178">Nel server DPM hello eseguire hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) macchina di hello tooregister cmdlet con insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-178">On hello DPM server, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="a18bc-179">Impostazioni di configurazione iniziali</span><span class="sxs-lookup"><span data-stu-id="a18bc-179">Initial configuration settings</span></span>
<span data-ttu-id="a18bc-180">Una volta registrato con hello hello Server DPM l'insieme di credenziali di servizi di ripristino, viene avviato con le impostazioni di sottoscrizione predefinite.</span><span class="sxs-lookup"><span data-stu-id="a18bc-180">Once hello DPM Server is registered with hello Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="a18bc-181">Queste impostazioni di sottoscrizione includono funzionalità di rete, la crittografia e hello area di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="a18bc-181">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="a18bc-182">le impostazioni di sottoscrizione toochange necessari toofirst ottenere un handle su hello (predefinito) le impostazioni esistenti utilizzando hello [Get DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a18bc-182">toochange subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="a18bc-183">Tutte le modifiche vengono apportate toothis locale PowerShell oggetto ```$setting``` e quindi completa dell'oggetto hello è tooDPM eseguito il commit e Backup di Azure toosave loro utilizzando hello [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-183">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="a18bc-184">È necessario hello toouse ```–Commit``` tooensure di flag che hello le modifiche vengono mantenute.</span><span class="sxs-lookup"><span data-stu-id="a18bc-184">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="a18bc-185">le impostazioni di Hello saranno non applicate e utilizzate dal Backup di Azure, a meno che il commit.</span><span class="sxs-lookup"><span data-stu-id="a18bc-185">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="a18bc-186">Rete</span><span class="sxs-lookup"><span data-stu-id="a18bc-186">Networking</span></span>
<span data-ttu-id="a18bc-187">Se la connettività di hello di hello DPM macchina toohello servizio di Backup di Azure su hello internet è tramite un server proxy, impostazioni del server proxy hello devono essere fornite per i backup riusciti.</span><span class="sxs-lookup"><span data-stu-id="a18bc-187">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="a18bc-188">Questa operazione viene eseguita tramite hello ```-ProxyServer```e ```-ProxyPort```, ```-ProxyUsername``` hello e ```ProxyPassword``` parametri con hello [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-188">This is done by using hello ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="a18bc-189">In questo esempio non esiste alcun server proxy, pertanto sono state eliminate tutte le informazioni relative al proxy.</span><span class="sxs-lookup"><span data-stu-id="a18bc-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="a18bc-190">Utilizzo della larghezza di banda può essere controllata anche con le opzioni di ```-WorkHourBandwidth``` e ```-NonWorkHourBandwidth``` per un set specificato di giorni della settimana hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="a18bc-191">In questo esempio non viene impostata alcuna limitazione.</span><span class="sxs-lookup"><span data-stu-id="a18bc-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a><span data-ttu-id="a18bc-192">Configurare l'Area di gestione temporanea hello</span><span class="sxs-lookup"><span data-stu-id="a18bc-192">Configuring hello staging Area</span></span>
<span data-ttu-id="a18bc-193">Hello Azure Backup agent in esecuzione nel server DPM hello deve archiviazione temporanea per i dati ripristinati dal cloud hello (area di gestione temporanea).</span><span class="sxs-lookup"><span data-stu-id="a18bc-193">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="a18bc-194">Configurare l'area di gestione temporanea hello utilizzando hello [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet e hello ```-StagingAreaPath``` parametro.</span><span class="sxs-lookup"><span data-stu-id="a18bc-194">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="a18bc-195">Nell'esempio hello sopra, hello area di gestione temporanea verrà impostata troppo*C:\StagingArea* nell'oggetto PowerShell hello ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="a18bc-195">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="a18bc-196">Verificare che hello specificato esiste già, altrimenti il commit finale hello delle impostazioni di sottoscrizione hello avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="a18bc-196">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="a18bc-197">Impostazioni crittografia</span><span class="sxs-lookup"><span data-stu-id="a18bc-197">Encryption settings</span></span>
<span data-ttu-id="a18bc-198">backup di dati inviati di Hello tooAzure Backup è tooprotect crittografato hello riservatezza dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-198">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="a18bc-199">la passphrase di crittografia Hello è dati hello toodecrypt di password"hello" in fase di hello del ripristino.</span><span class="sxs-lookup"><span data-stu-id="a18bc-199">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="a18bc-200">È importante tookeep sicuro le informazioni e secure dopo che è stata impostata.</span><span class="sxs-lookup"><span data-stu-id="a18bc-200">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="a18bc-201">Nel seguente esempio hello primo comando hello Converte la stringa hello ```passphrase123456789``` tooa sicura stringa e assegna hello stringa sicura toohello variabile denominata ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="a18bc-201">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="a18bc-202">Hello secondo comando imposta la stringa sicura hello in ```$Passphrase``` come password hello per la crittografia dei backup.</span><span class="sxs-lookup"><span data-stu-id="a18bc-202">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="a18bc-203">Mantenere informazioni passphrase hello sicuro e dopo che è stata impostata.</span><span class="sxs-lookup"><span data-stu-id="a18bc-203">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="a18bc-204">Non sarà in grado di toorestore dati da Azure senza questa passphrase.</span><span class="sxs-lookup"><span data-stu-id="a18bc-204">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="a18bc-205">A questo punto, avrebbe dovuto effettuare tutti hello necessarie modifiche toohello ```$setting``` oggetto.</span><span class="sxs-lookup"><span data-stu-id="a18bc-205">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="a18bc-206">Tenere presente che le modifiche di hello toocommit.</span><span class="sxs-lookup"><span data-stu-id="a18bc-206">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="a18bc-207">Proteggere dati tooAzure Backup</span><span class="sxs-lookup"><span data-stu-id="a18bc-207">Protect data tooAzure Backup</span></span>
<span data-ttu-id="a18bc-208">In questa sezione verrà aggiunta una tooDPM di server di produzione e quindi proteggere l'archiviazione di DPM toolocal dati hello e quindi tooAzure Backup.</span><span class="sxs-lookup"><span data-stu-id="a18bc-208">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="a18bc-209">Negli esempi di hello, verrà illustrato come tooback backup di file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="a18bc-209">In hello examples, we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="a18bc-210">Hello logica può facilmente essere estesa toobackup qualsiasi origine dati con supporto di DPM.</span><span class="sxs-lookup"><span data-stu-id="a18bc-210">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="a18bc-211">Tutti i backup DPM sono regolati da un gruppo protezione dati costituito da quattro parti:</span><span class="sxs-lookup"><span data-stu-id="a18bc-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="a18bc-212">**I membri del gruppo** è un elenco di tutti gli oggetti da proteggere con hello (noto anche come *origini dati* in Data Protection Manager) che si desidera tooprotect in hello stesso gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="a18bc-212">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="a18bc-213">Ad esempio, è consigliabile tooprotect produzione, le macchine virtuali in un gruppo protezione dati e i database di SQL Server in un altro gruppo protezione dati come presentare requisiti diversi per il backup.</span><span class="sxs-lookup"><span data-stu-id="a18bc-213">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="a18bc-214">Prima di eseguire il backup di qualsiasi origine dati in un server di produzione è necessario toomake hello che agente Data Protection Manager è installato nel server di hello ed è gestito da DPM.</span><span class="sxs-lookup"><span data-stu-id="a18bc-214">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="a18bc-215">Seguire i passaggi di hello per [installazione hello agente DPM](https://technet.microsoft.com/library/bb870935.aspx) e il relativo collegamento toohello appropriati Server DPM.</span><span class="sxs-lookup"><span data-stu-id="a18bc-215">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="a18bc-216">**Metodo protezione dati** specifica hello backup i percorsi di destinazione - nastro, disco e cloud.</span><span class="sxs-lookup"><span data-stu-id="a18bc-216">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="a18bc-217">In questo esempio è proteggerà dati toohello locale su disco e toohello nel cloud.</span><span class="sxs-lookup"><span data-stu-id="a18bc-217">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="a18bc-218">Oggetto **pianificazione del backup** che specifica quando i backup necessitano toobe eseguito e la frequenza con cui hello di sincronizzazione dei dati tra hello Server DPM e il server di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-218">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="a18bc-219">Oggetto **pianificazione della conservazione** che specifica quanto tempo i punti di ripristino hello tooretain in Azure.</span><span class="sxs-lookup"><span data-stu-id="a18bc-219">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="a18bc-220">Creazione di un gruppo di protezione</span><span class="sxs-lookup"><span data-stu-id="a18bc-220">Creating a protection group</span></span>
<span data-ttu-id="a18bc-221">Iniziare creando un nuovo gruppo di protezione utilizzando hello [New DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-221">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="a18bc-222">Hello sopra cmdlet verrà creato un gruppo di protezione denominato *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="a18bc-222">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="a18bc-223">Inoltre possibile modificare un gruppo protezione dati successiva tooadd toohello backup cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="a18bc-223">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="a18bc-224">Tuttavia, toomake modifiche toohello gruppo protezione dati - nuovo o esistente, è necessario tooget un handle in un *modificabile* oggetto utilizzando hello [Get DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-224">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="a18bc-225">Aggiunta di membri di gruppo toohello gruppo protezione dati</span><span class="sxs-lookup"><span data-stu-id="a18bc-225">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="a18bc-226">Ogni agente DPM SA elenco hello di origini dati nel server di hello cui è installato.</span><span class="sxs-lookup"><span data-stu-id="a18bc-226">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="a18bc-227">tooadd toohello un'origine dati gruppo protezione dati, hello agente DPM esigenze toofirst invia un elenco di server DPM toohello indietro di hello origini dati.</span><span class="sxs-lookup"><span data-stu-id="a18bc-227">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="a18bc-228">Uno o più origini dati vengono quindi selezionate e aggiunte toohello gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="a18bc-228">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="a18bc-229">i passaggi di PowerShell Hello necessarie tooachieve questo sono:</span><span class="sxs-lookup"><span data-stu-id="a18bc-229">hello PowerShell steps needed tooachieve this are:</span></span>

1. <span data-ttu-id="a18bc-230">Recuperare un elenco di tutti i server gestiti da DPM tramite hello agente DPM.</span><span class="sxs-lookup"><span data-stu-id="a18bc-230">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="a18bc-231">Scegliere un server specifico.</span><span class="sxs-lookup"><span data-stu-id="a18bc-231">Choose a specific server.</span></span>
3. <span data-ttu-id="a18bc-232">Recuperare un elenco di tutte le origini dati nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="a18bc-232">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="a18bc-233">Scegliere uno o più origini dati e aggiungerli toohello gruppo protezione dati</span><span class="sxs-lookup"><span data-stu-id="a18bc-233">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="a18bc-234">elenco di Hello del server in cui hello agente Data Protection Manager è installato e viene gestito dal Server DPM hello viene acquisito con hello [Get DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-234">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="a18bc-235">In questo esempio verrà applicato un filtro e per il backup verrà configurato solo il server di produzione denominato *productionserver01* .</span><span class="sxs-lookup"><span data-stu-id="a18bc-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="a18bc-236">Ora recuperare elenco hello di origini dati in ```$server``` utilizzando hello [Get DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-236">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="a18bc-237">In questo esempio si Filtra per volume hello * unità d:\* che tooconfigure per il backup.</span><span class="sxs-lookup"><span data-stu-id="a18bc-237">In this example we are filtering for hello volume *D:\* that we want tooconfigure for backup.</span></span> <span data-ttu-id="a18bc-238">L'origine dati viene quindi aggiunto toohello gruppo protezione dati utilizzando hello [Aggiungi DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-238">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="a18bc-239">Ricordare hello toouse *modificabile* oggetto gruppo protezione dati ```$MPG``` aggiunte hello toomake.</span><span class="sxs-lookup"><span data-stu-id="a18bc-239">Remember toouse hello *modifiable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="a18bc-240">Ripetere questo passaggio il numero di volte in base alle esigenze fino a quando non sono stati aggiunti tutti hello gruppo protezione dati di origini dati toohello scelto.</span><span class="sxs-lookup"><span data-stu-id="a18bc-240">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="a18bc-241">È possibile iniziare con una sola origine dati e del flusso di lavoro hello completo per la creazione di hello gruppo protezione dati e successivamente aggiungere altre origini dati toohello gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="a18bc-241">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="a18bc-242">Selezione metodo protezione dati di hello</span><span class="sxs-lookup"><span data-stu-id="a18bc-242">Selecting hello data protection method</span></span>
<span data-ttu-id="a18bc-243">Dopo aver aggiunto le origini dati hello toohello gruppo protezione dati, passaggio successivo hello è metodo di protezione hello toospecify utilizzando hello [Set DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-243">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="a18bc-244">In questo esempio hello gruppo protezione dati è configurato per il disco locale e il backup nel cloud.</span><span class="sxs-lookup"><span data-stu-id="a18bc-244">In this example, hello Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="a18bc-245">È inoltre necessario toospecify hello datasource che si desidera toocloud tooprotect utilizzando hello [Aggiungi DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet con - flag Online.</span><span class="sxs-lookup"><span data-stu-id="a18bc-245">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="a18bc-246">Impostazione di un intervallo di conservazione hello</span><span class="sxs-lookup"><span data-stu-id="a18bc-246">Setting hello retention range</span></span>
<span data-ttu-id="a18bc-247">Impostare il mantenimento dati hello per i punti di backup hello utilizzando hello [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-247">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="a18bc-248">Anche se potrebbe sembrare memorizzazione hello tooset dispari prima di pianificazione del backup hello è stato definito utilizzando hello ```Set-DPMPolicyObjective``` imposta automaticamente una pianificazione di backup predefinito che può quindi essere modificata.</span><span class="sxs-lookup"><span data-stu-id="a18bc-248">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="a18bc-249">È sempre possibile tooset pianificazione del backup hello innanzitutto e hello criteri di conservazione dopo.</span><span class="sxs-lookup"><span data-stu-id="a18bc-249">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="a18bc-250">Nel seguente esempio hello hello imposta i parametri di memorizzazione hello per i backup su disco.</span><span class="sxs-lookup"><span data-stu-id="a18bc-250">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="a18bc-251">Questo verrà conservazione dei backup per 10 giorni e sincronizzare i dati ogni 6 ore tra il server di produzione hello e hello Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="a18bc-251">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="a18bc-252">Hello ```SynchronizationFrequencyMinutes``` non definisce la frequenza con cui un punto di ripristino viene creato, ma come spesso dati sono il server DPM toohello copiato.</span><span class="sxs-lookup"><span data-stu-id="a18bc-252">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server.</span></span>  <span data-ttu-id="a18bc-253">Questa impostazione impedisce che i backup diventino di dimensioni eccessive.</span><span class="sxs-lookup"><span data-stu-id="a18bc-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="a18bc-254">Per i backup verranno tooAzure (Data Protection Manager si riferisce toothem come backup in linea) periodi di mantenimento hello possono essere configurati per [utilizzando uno schema nonno-padre-figlio (condivisione file di Groove) di memorizzazione a lungo termine](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="a18bc-254">For backups going tooAzure (DPM refers toothem as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="a18bc-255">Ciò significa che è possibile definire un criterio di conservazione combinato che includa criteri giornalieri, settimanali, mensili e annuali.</span><span class="sxs-lookup"><span data-stu-id="a18bc-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="a18bc-256">In questo esempio è una matrice che rappresenta lo schema di memorizzazione complesso hello che si desidera creare e quindi configurare l'intervallo di conservazione hello utilizzando hello [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-256">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="a18bc-257">Pianificazione del backup hello set</span><span class="sxs-lookup"><span data-stu-id="a18bc-257">Set hello backup schedule</span></span>
<span data-ttu-id="a18bc-258">DPM imposta automaticamente una pianificazione di backup predefinito se si specifica l'obiettivo di protezione di hello utilizzando hello ```Set-DPMPolicyObjective``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-258">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="a18bc-259">le pianificazioni predefinite hello toochange, utilizzare hello [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet seguito da hello [Set DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-259">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="a18bc-260">In hello sopra riportato, ```$onlineSch``` è una matrice con quattro elementi che contiene pianificazione protezione dati online esistente hello per hello gruppo protezione dati nello schema di condivisione file di Groove hello:</span><span class="sxs-lookup"><span data-stu-id="a18bc-260">In hello above example, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="a18bc-261">```$onlineSch[0]```contiene una pianificazione giornaliera hello</span><span class="sxs-lookup"><span data-stu-id="a18bc-261">```$onlineSch[0]``` contains hello daily schedule</span></span>
2. <span data-ttu-id="a18bc-262">```$onlineSch[1]```contiene una pianificazione settimanale hello</span><span class="sxs-lookup"><span data-stu-id="a18bc-262">```$onlineSch[1]``` contains hello weekly schedule</span></span>
3. <span data-ttu-id="a18bc-263">```$onlineSch[2]```contiene la pianificazione mensile hello</span><span class="sxs-lookup"><span data-stu-id="a18bc-263">```$onlineSch[2]``` contains hello monthly schedule</span></span>
4. <span data-ttu-id="a18bc-264">```$onlineSch[3]```contiene pianificazione annuale hello</span><span class="sxs-lookup"><span data-stu-id="a18bc-264">```$onlineSch[3]``` contains hello yearly schedule</span></span>

<span data-ttu-id="a18bc-265">Pertanto se è necessaria una pianificazione settimanale di hello toomodify, è necessario toorefer toohello ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="a18bc-265">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="a18bc-266">Backup iniziale</span><span class="sxs-lookup"><span data-stu-id="a18bc-266">Initial backup</span></span>
<span data-ttu-id="a18bc-267">Quando backup di un'origine dati per hello prima volta, DPM deve creare la replica iniziale che crea una copia completa di hello datasource toobe protetti nel volume di replica DPM.</span><span class="sxs-lookup"><span data-stu-id="a18bc-267">When backing up a datasource for hello first time, DPM needs creates initial replica that creates a full copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="a18bc-268">Questa attività possono essere pianificata per un momento specifico o può essere attivata manualmente, utilizzando hello [Set DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet con il parametro hello ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="a18bc-268">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="a18bc-269">Modifica delle dimensioni di hello di Replica DPM & volume del punto di ripristino</span><span class="sxs-lookup"><span data-stu-id="a18bc-269">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="a18bc-270">È possibile inoltre modificare hello dimensioni del volume di Replica di DPM e l'utilizzo di copia Shadow volume [Set DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet come hello di esempio seguente: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-manuale - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="a18bc-270">You can also change hello size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="a18bc-271">Il commit hello modifiche toohello gruppo protezione dati</span><span class="sxs-lookup"><span data-stu-id="a18bc-271">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="a18bc-272">Infine, le modifiche di hello necessario toobe eseguito il commit prima che DPM può eseguire il backup di hello in base alla configurazione di hello nuovo gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="a18bc-272">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="a18bc-273">Ciò può essere ottenuto utilizzando hello [Set DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-273">This can be achieved using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="a18bc-274">Visualizzare i punti di backup hello</span><span class="sxs-lookup"><span data-stu-id="a18bc-274">View hello backup points</span></span>
<span data-ttu-id="a18bc-275">È possibile utilizzare hello [Get DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget cmdlet un elenco di tutti i punti di ripristino per un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="a18bc-275">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="a18bc-276">Nell'esempio seguente, vengono:</span><span class="sxs-lookup"><span data-stu-id="a18bc-276">In this example, we will:</span></span>

* <span data-ttu-id="a18bc-277">FETCH tutti hello PGs nel server DPM hello e archiviati in una matrice```$PG```</span><span class="sxs-lookup"><span data-stu-id="a18bc-277">fetch all hello PGs on hello DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="a18bc-278">ottenere toohello corrispondente di hello origini dati```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="a18bc-278">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="a18bc-279">ottenere tutti i punti di ripristino hello per un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="a18bc-279">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="a18bc-280">Ripristino dei dati protetti su Azure</span><span class="sxs-lookup"><span data-stu-id="a18bc-280">Restore data protected on Azure</span></span>
<span data-ttu-id="a18bc-281">Il ripristino dei dati è una combinazione tra un oggetto ```RecoverableItem``` e un oggetto ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="a18bc-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="a18bc-282">Nella sezione precedente hello, abbiamo un elenco di punti di backup hello per un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="a18bc-282">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="a18bc-283">Nell'esempio hello riportato di seguito viene illustrato come macchina virtuale di Hyper-V toorestore da Azure Backup dai punti di backup in combinazione con hello destinazione per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="a18bc-283">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="a18bc-284">L'esempio include quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a18bc-284">This example includes:</span></span>

* <span data-ttu-id="a18bc-285">Creazione di un'opzione di ripristino utilizzando hello [New DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-285">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="a18bc-286">Matrice di hello recupero dei punti di backup utilizzando hello ```Get-DPMRecoveryPoint``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a18bc-286">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="a18bc-287">Scelta di un backup toorestore punto da.</span><span class="sxs-lookup"><span data-stu-id="a18bc-287">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="a18bc-288">i comandi di Hello possono essere facilmente esteso per qualsiasi tipo di origine dati.</span><span class="sxs-lookup"><span data-stu-id="a18bc-288">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a18bc-289">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a18bc-289">Next steps</span></span>
* <span data-ttu-id="a18bc-290">Per altre informazioni su DPM vedere Backup tooAzure [tooDPM introduzione Backup](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="a18bc-290">For more information about DPM tooAzure Backup see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
