---
title: 'Backup di Azure: Utilizzo di PowerShell tooback dei carichi di lavoro DPM | Documenti Microsoft'
description: Informazioni su come toodeploy e gestire il Backup di Azure per Data Protection Manager (DPM) tramite PowerShell
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 48ebe6b520857836e89749ffb6fe83d1f14c5597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="01cd8-103">Distribuire e gestire backup tooAzure per i server di Data Protection Manager (DPM) mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="01cd8-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="01cd8-104">ARM</span><span class="sxs-lookup"><span data-stu-id="01cd8-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="01cd8-105">Classico</span><span class="sxs-lookup"><span data-stu-id="01cd8-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="01cd8-106">Questo articolo viene illustrato come toouse PowerShell tooback backup e ripristinare i dati DPM da un insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="01cd8-106">This article explains how toouse PowerShell tooback up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="01cd8-107">Microsoft consiglia l'uso di insiemi di credenziali dei Servizi di ripristino per tutte le nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="01cd8-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="01cd8-108">Nel caso di un nuovo utente di Backup di Azure, usare l'articolo hello [distribuire e gestire Data Protection Manager dati tooAzure tramite PowerShell](backup-dpm-automation.md), pertanto si archiviano i dati in un insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="01cd8-108">If you are a new Azure Backup user, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="01cd8-109">È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery.</span><span class="sxs-lookup"><span data-stu-id="01cd8-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="01cd8-110">Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="01cd8-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="01cd8-111">Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.</span><span class="sxs-lookup"><span data-stu-id="01cd8-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="01cd8-112">Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup.</span><span class="sxs-lookup"><span data-stu-id="01cd8-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="01cd8-113">**Entro il 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="01cd8-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="01cd8-114">Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.</span><span class="sxs-lookup"><span data-stu-id="01cd8-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="01cd8-115">Si sarà in grado di tooaccess ai dati di backup nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="01cd8-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="01cd8-116">Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="01cd8-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="01cd8-117">Impostazione di ambiente PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="01cd8-117">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="01cd8-118">Prima di poter utilizzare PowerShell toomanage backup da Data Protection Manager tooAzure, sarà necessario toohave hello destra ambiente PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01cd8-118">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you will need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="01cd8-119">All'inizio di hello della sessione di PowerShell hello, assicurarsi di eseguire hello seguenti moduli destra di comando tooimport hello e consentono di determinare i cmdlet DPM toocorrectly riferimento hello:</span><span class="sxs-lookup"><span data-stu-id="01cd8-119">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="01cd8-120">Installazione e registrazione</span><span class="sxs-lookup"><span data-stu-id="01cd8-120">Setup and Registration</span></span>
<span data-ttu-id="01cd8-121">toobegin:</span><span class="sxs-lookup"><span data-stu-id="01cd8-121">toobegin:</span></span>

1. <span data-ttu-id="01cd8-122">[Scaricare la versione più recente di PowerShell](https://github.com/Azure/azure-powershell/releases) (la versione minima richiesta è: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="01cd8-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="01cd8-123">Abilitare i commandlet del Backup di Azure hello passando troppo*AzureResourceManager* modalità tramite hello **Switch-AzureMode** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="01cd8-123">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="01cd8-124">Hello seguente programma di installazione e le attività di registrazione può essere automatizzata con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="01cd8-124">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="01cd8-125">Creare un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="01cd8-125">Create a backup vault</span></span>
* <span data-ttu-id="01cd8-126">Installare hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="01cd8-126">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="01cd8-127">Registrazione con hello servizio Azure Backup</span><span class="sxs-lookup"><span data-stu-id="01cd8-127">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="01cd8-128">Impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="01cd8-128">Networking settings</span></span>
* <span data-ttu-id="01cd8-129">Impostazioni crittografia</span><span class="sxs-lookup"><span data-stu-id="01cd8-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="01cd8-130">Creare un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="01cd8-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="01cd8-131">Per i clienti che usano Azure Backup per hello prima volta, è necessario tooregister hello Azure Backup provider toobe utilizzato con la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="01cd8-131">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="01cd8-132">Questa operazione può essere eseguita tramite l'esecuzione di hello comando seguente: "Microsoft.Backup" Register AzureProvider - ProviderNamespace</span><span class="sxs-lookup"><span data-stu-id="01cd8-132">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="01cd8-133">È possibile creare un nuovo insieme di credenziali di backup utilizzando hello **New AzureRMBackupVault** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-133">You can create a new backup vault using hello **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="01cd8-134">insieme di credenziali backup Hello è una risorsa ARM, pertanto è necessario tooplace all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="01cd8-134">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="01cd8-135">In una console di Azure PowerShell con privilegi elevata, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="01cd8-135">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="01cd8-136">È possibile ottenere un elenco di tutti gli archivi di backup hello in una specifica sottoscrizione utilizzando hello **Get AzureRMBackupVault** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-136">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="01cd8-137">Installazione agente Azure Backup hello in un Server DPM</span><span class="sxs-lookup"><span data-stu-id="01cd8-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="01cd8-138">Prima di installare l'agente Azure Backup hello, è necessario il programma di installazione di toohave hello scaricato e presenti sul Server di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="01cd8-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="01cd8-139">È possibile ottenere una versione più recente di hello del programma di installazione hello da hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) o dalla pagina Dashboard hello backup vault.</span><span class="sxs-lookup"><span data-stu-id="01cd8-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="01cd8-140">Salvare installer hello tooan posizione facilmente accessibile, ad esempio * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="01cd8-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="01cd8-141">esecuzione comando in una console di PowerShell con privilegi elevata seguente hello tooinstall agente hello **nel server DPM hello**:</span><span class="sxs-lookup"><span data-stu-id="01cd8-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="01cd8-142">Consente di installare agente hello con tutte le opzioni predefinite di hello.</span><span class="sxs-lookup"><span data-stu-id="01cd8-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="01cd8-143">installazione di Hello richiede alcuni minuti in background hello.</span><span class="sxs-lookup"><span data-stu-id="01cd8-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="01cd8-144">Se non si specifica hello */nu* hello opzione **Windows Update** aprirà la finestra alla fine hello hello toocheck di installazione per tutti gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="01cd8-144">If you do not specify hello */nu* option hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="01cd8-145">agente Hello verrà visualizzato nell'elenco di hello dei programmi installati.</span><span class="sxs-lookup"><span data-stu-id="01cd8-145">hello agent will show in hello list of installed programs.</span></span> <span data-ttu-id="01cd8-146">elenco di hello toosee dei programmi installati, andare troppo**Pannello di controllo** > **programmi** > **programmi e funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="01cd8-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente installato](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="01cd8-148">Opzioni di installazione</span><span class="sxs-lookup"><span data-stu-id="01cd8-148">Installation options</span></span>
<span data-ttu-id="01cd8-149">toosee tutti hello opzioni disponibili tramite hello della riga di comando, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="01cd8-149">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="01cd8-150">Hello le opzioni disponibili includono:</span><span class="sxs-lookup"><span data-stu-id="01cd8-150">hello available options include:</span></span>

| <span data-ttu-id="01cd8-151">Opzione</span><span class="sxs-lookup"><span data-stu-id="01cd8-151">Option</span></span> | <span data-ttu-id="01cd8-152">Dettagli</span><span class="sxs-lookup"><span data-stu-id="01cd8-152">Details</span></span> | <span data-ttu-id="01cd8-153">Default</span><span class="sxs-lookup"><span data-stu-id="01cd8-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="01cd8-154">/q</span><span class="sxs-lookup"><span data-stu-id="01cd8-154">/q</span></span> |<span data-ttu-id="01cd8-155">Installazione non interattiva</span><span class="sxs-lookup"><span data-stu-id="01cd8-155">Quiet installation</span></span> |- |
| <span data-ttu-id="01cd8-156">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="01cd8-156">/p:"location"</span></span> |<span data-ttu-id="01cd8-157">Cartella di installazione toohello percorso per l'agente Azure Backup hello.</span><span class="sxs-lookup"><span data-stu-id="01cd8-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="01cd8-158">C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="01cd8-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="01cd8-159">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="01cd8-159">/s:"location"</span></span> |<span data-ttu-id="01cd8-160">Cartella cache toohello percorso per l'agente Azure Backup hello.</span><span class="sxs-lookup"><span data-stu-id="01cd8-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="01cd8-161">C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure\Scratch</span><span class="sxs-lookup"><span data-stu-id="01cd8-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="01cd8-162">/m</span><span class="sxs-lookup"><span data-stu-id="01cd8-162">/m</span></span> |<span data-ttu-id="01cd8-163">Consenso esplicito tooMicrosoft aggiornamento</span><span class="sxs-lookup"><span data-stu-id="01cd8-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="01cd8-164">/nu</span><span class="sxs-lookup"><span data-stu-id="01cd8-164">/nu</span></span> |<span data-ttu-id="01cd8-165">Al termine dell'installazione non vengono cercati gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="01cd8-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="01cd8-166">/d</span><span class="sxs-lookup"><span data-stu-id="01cd8-166">/d</span></span> |<span data-ttu-id="01cd8-167">Disinstalla l'agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="01cd8-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="01cd8-168">/ph</span><span class="sxs-lookup"><span data-stu-id="01cd8-168">/ph</span></span> |<span data-ttu-id="01cd8-169">Indirizzo host proxy</span><span class="sxs-lookup"><span data-stu-id="01cd8-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="01cd8-170">/po</span><span class="sxs-lookup"><span data-stu-id="01cd8-170">/po</span></span> |<span data-ttu-id="01cd8-171">Numero porta host proxy</span><span class="sxs-lookup"><span data-stu-id="01cd8-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="01cd8-172">/pu</span><span class="sxs-lookup"><span data-stu-id="01cd8-172">/pu</span></span> |<span data-ttu-id="01cd8-173">Nome utente host proxy</span><span class="sxs-lookup"><span data-stu-id="01cd8-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="01cd8-174">/pw</span><span class="sxs-lookup"><span data-stu-id="01cd8-174">/pw</span></span> |<span data-ttu-id="01cd8-175">Password proxy</span><span class="sxs-lookup"><span data-stu-id="01cd8-175">Proxy Password</span></span> |- |

### <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="01cd8-176">Registrazione con hello servizio Azure Backup</span><span class="sxs-lookup"><span data-stu-id="01cd8-176">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="01cd8-177">Prima di poter registrare con hello servizio Backup di Azure, è necessario tooensure tale hello [prerequisiti](backup-azure-dpm-introduction.md) sono soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="01cd8-177">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="01cd8-178">È necessario:</span><span class="sxs-lookup"><span data-stu-id="01cd8-178">You must:</span></span>

* <span data-ttu-id="01cd8-179">Avere una sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="01cd8-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="01cd8-180">Ottieni un archivio di backup</span><span class="sxs-lookup"><span data-stu-id="01cd8-180">Have a backup vault</span></span>

<span data-ttu-id="01cd8-181">toodownload hello insieme di credenziali, eseguire hello **Get AzureBackupVaultCredentials** cmdlet in una console PowerShell di Azure e l'archivio in una posizione comoda come * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="01cd8-181">toodownload hello vault credentials, run hello **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="01cd8-182">Registrazione macchina hello con insieme di credenziali hello avviene utilizzando hello [inizio DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="01cd8-182">Registering hello machine with hello vault is done using hello [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="01cd8-183">Consente di registrare il Server DPM denominato "TestingServer" hello insieme di credenziali di Microsoft Azure hello specificato utilizzando le credenziali dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="01cd8-183">This will register hello DPM Server named “TestingServer” with Microsoft Azure Vault using hello specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="01cd8-184">Non usare file delle credenziali dell'insieme di credenziali hello toospecify i percorsi relativi.</span><span class="sxs-lookup"><span data-stu-id="01cd8-184">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="01cd8-185">È necessario fornire un percorso assoluto come un cmdlet toohello input.</span><span class="sxs-lookup"><span data-stu-id="01cd8-185">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="01cd8-186">Impostazioni di configurazione iniziali</span><span class="sxs-lookup"><span data-stu-id="01cd8-186">Initial configuration settings</span></span>
<span data-ttu-id="01cd8-187">Una volta hello Server DPM registrato insieme di credenziali di Backup di Azure hello, verrà avviato con le impostazioni di sottoscrizione predefinite.</span><span class="sxs-lookup"><span data-stu-id="01cd8-187">Once hello DPM Server is registered with hello Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="01cd8-188">Queste impostazioni di sottoscrizione includono funzionalità di rete, la crittografia e hello area di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="01cd8-188">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="01cd8-189">toobegin modifica hello le impostazioni di sottoscrizione è necessario toofirst ottenere un handle su hello (predefinito) le impostazioni esistenti utilizzando hello [Get DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="01cd8-189">toobegin changing hello subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="01cd8-190">Tutte le modifiche vengono apportate toothis locale PowerShell oggetto ```$setting``` e quindi completa dell'oggetto hello è tooDPM eseguito il commit e Backup di Azure toosave loro utilizzando hello [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-190">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="01cd8-191">È necessario hello toouse ```–Commit``` tooensure di flag che hello le modifiche vengono mantenute.</span><span class="sxs-lookup"><span data-stu-id="01cd8-191">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="01cd8-192">le impostazioni di Hello saranno non applicate e utilizzate dal Backup di Azure, a meno che il commit.</span><span class="sxs-lookup"><span data-stu-id="01cd8-192">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="01cd8-193">Rete</span><span class="sxs-lookup"><span data-stu-id="01cd8-193">Networking</span></span>
<span data-ttu-id="01cd8-194">Se la connettività di hello di hello DPM macchina toohello servizio di Backup di Azure su hello internet è tramite un server proxy, impostazioni del server proxy hello devono essere fornite per i backup toosucceed.</span><span class="sxs-lookup"><span data-stu-id="01cd8-194">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for backups toosucceed.</span></span> <span data-ttu-id="01cd8-195">Questa operazione viene eseguita tramite hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` hello e ```ProxyPassword``` parametri con hello [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-195">This is done by using hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="01cd8-196">In questo esempio non esiste alcun server proxy, pertanto sono state eliminate tutte le informazioni relative al proxy.</span><span class="sxs-lookup"><span data-stu-id="01cd8-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="01cd8-197">Utilizzo della larghezza di banda può essere controllata anche con le opzioni di ```-WorkHourBandwidth``` e ```-NonWorkHourBandwidth``` per un set specificato di giorni della settimana hello.</span><span class="sxs-lookup"><span data-stu-id="01cd8-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="01cd8-198">In questo esempio non viene impostata alcuna limitazione.</span><span class="sxs-lookup"><span data-stu-id="01cd8-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-hello-staging-area"></a><span data-ttu-id="01cd8-199">Configurare l'Area di gestione temporanea hello</span><span class="sxs-lookup"><span data-stu-id="01cd8-199">Configuring hello staging Area</span></span>
<span data-ttu-id="01cd8-200">Hello Azure Backup agent in esecuzione nel server DPM hello deve archiviazione temporanea per i dati ripristinati dal cloud hello (area di gestione temporanea).</span><span class="sxs-lookup"><span data-stu-id="01cd8-200">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="01cd8-201">Configurare l'area di gestione temporanea hello utilizzando hello [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet e hello ```-StagingAreaPath``` parametro.</span><span class="sxs-lookup"><span data-stu-id="01cd8-201">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="01cd8-202">Nell'esempio hello sopra, hello area di gestione temporanea verrà impostata troppo*C:\StagingArea* nell'oggetto PowerShell hello ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="01cd8-202">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="01cd8-203">Verificare che hello specificato esiste già, altrimenti il commit finale hello delle impostazioni di sottoscrizione hello avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="01cd8-203">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="01cd8-204">Impostazioni crittografia</span><span class="sxs-lookup"><span data-stu-id="01cd8-204">Encryption settings</span></span>
<span data-ttu-id="01cd8-205">backup di dati inviati di Hello tooAzure Backup è tooprotect crittografato hello riservatezza dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="01cd8-205">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="01cd8-206">la passphrase di crittografia Hello è dati hello toodecrypt di password"hello" in fase di hello del ripristino.</span><span class="sxs-lookup"><span data-stu-id="01cd8-206">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="01cd8-207">È importante tookeep sicuro le informazioni e secure dopo che è stata impostata.</span><span class="sxs-lookup"><span data-stu-id="01cd8-207">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="01cd8-208">Nel seguente esempio hello primo comando hello Converte la stringa hello ```passphrase123456789``` tooa sicura stringa e assegna hello stringa sicura toohello variabile denominata ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="01cd8-208">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="01cd8-209">Hello secondo comando imposta la stringa sicura hello in ```$Passphrase``` come password hello per la crittografia dei backup.</span><span class="sxs-lookup"><span data-stu-id="01cd8-209">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="01cd8-210">Mantenere informazioni passphrase hello sicuro e dopo che è stata impostata.</span><span class="sxs-lookup"><span data-stu-id="01cd8-210">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="01cd8-211">Non sarà in grado di toorestore dati da Azure senza questa passphrase.</span><span class="sxs-lookup"><span data-stu-id="01cd8-211">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="01cd8-212">A questo punto, avrebbe dovuto effettuare tutti hello necessarie modifiche toohello ```$setting``` oggetto.</span><span class="sxs-lookup"><span data-stu-id="01cd8-212">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="01cd8-213">Tenere presente che le modifiche di hello toocommit.</span><span class="sxs-lookup"><span data-stu-id="01cd8-213">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="01cd8-214">Proteggere dati tooAzure Backup</span><span class="sxs-lookup"><span data-stu-id="01cd8-214">Protect data tooAzure Backup</span></span>
<span data-ttu-id="01cd8-215">In questa sezione verrà aggiunta una tooDPM di server di produzione e quindi proteggere l'archiviazione di DPM toolocal dati hello e quindi tooAzure Backup.</span><span class="sxs-lookup"><span data-stu-id="01cd8-215">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="01cd8-216">Negli esempi di hello verrà illustrato come tooback backup di file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="01cd8-216">In hello examples we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="01cd8-217">Hello logica può facilmente essere estesa toobackup qualsiasi origine dati con supporto di DPM.</span><span class="sxs-lookup"><span data-stu-id="01cd8-217">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="01cd8-218">Tutti i backup DPM sono regolati da un gruppo protezione dati costituito da quattro parti:</span><span class="sxs-lookup"><span data-stu-id="01cd8-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="01cd8-219">**I membri del gruppo** è un elenco di tutti gli oggetti da proteggere con hello (noto anche come *origini dati* in Data Protection Manager) che si desidera tooprotect in hello stesso gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="01cd8-219">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="01cd8-220">Ad esempio, è consigliabile tooprotect produzione, le macchine virtuali in un gruppo protezione dati e i database di SQL Server in un altro gruppo protezione dati come presentare requisiti diversi per il backup.</span><span class="sxs-lookup"><span data-stu-id="01cd8-220">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="01cd8-221">Prima di eseguire il backup di qualsiasi origine dati in un server di produzione è necessario toomake hello che agente Data Protection Manager è installato nel server di hello ed è gestito da DPM.</span><span class="sxs-lookup"><span data-stu-id="01cd8-221">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="01cd8-222">Seguire i passaggi di hello per [installazione hello agente DPM](https://technet.microsoft.com/library/bb870935.aspx) e il relativo collegamento toohello appropriati Server DPM.</span><span class="sxs-lookup"><span data-stu-id="01cd8-222">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="01cd8-223">**Metodo protezione dati** specifica hello backup i percorsi di destinazione - nastro, disco e cloud.</span><span class="sxs-lookup"><span data-stu-id="01cd8-223">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="01cd8-224">In questo esempio è proteggerà dati toohello locale su disco e toohello nel cloud.</span><span class="sxs-lookup"><span data-stu-id="01cd8-224">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="01cd8-225">Oggetto **pianificazione del backup** che specifica quando i backup necessitano toobe eseguito e la frequenza con cui hello di sincronizzazione dei dati tra hello Server DPM e il server di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="01cd8-225">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="01cd8-226">Oggetto **pianificazione della conservazione** che specifica quanto tempo i punti di ripristino hello tooretain in Azure.</span><span class="sxs-lookup"><span data-stu-id="01cd8-226">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="01cd8-227">Creazione di un gruppo di protezione</span><span class="sxs-lookup"><span data-stu-id="01cd8-227">Creating a protection group</span></span>
<span data-ttu-id="01cd8-228">Iniziare creando un nuovo gruppo di protezione utilizzando hello [New DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-228">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="01cd8-229">Hello sopra cmdlet verrà creato un gruppo di protezione denominato *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="01cd8-229">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="01cd8-230">Inoltre possibile modificare un gruppo protezione dati successiva tooadd toohello backup cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="01cd8-230">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="01cd8-231">Tuttavia, toomake modifiche toohello gruppo protezione dati - nuovo o esistente, è necessario tooget un handle in un *modificabile* oggetto utilizzando hello [Get DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-231">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="01cd8-232">Aggiunta di membri di gruppo toohello gruppo protezione dati</span><span class="sxs-lookup"><span data-stu-id="01cd8-232">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="01cd8-233">Ogni agente DPM SA elenco hello di origini dati nel server di hello cui è installato.</span><span class="sxs-lookup"><span data-stu-id="01cd8-233">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="01cd8-234">tooadd toohello un'origine dati gruppo protezione dati, hello agente DPM esigenze toofirst invia un elenco di server DPM toohello indietro di hello origini dati.</span><span class="sxs-lookup"><span data-stu-id="01cd8-234">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="01cd8-235">Uno o più origini dati vengono quindi selezionate e aggiunte toohello gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="01cd8-235">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="01cd8-236">è possibile ottenere tooget di Hello PowerShell passaggi necessari sono:</span><span class="sxs-lookup"><span data-stu-id="01cd8-236">hello PowerShell steps needed tooget achieve this are:</span></span>

1. <span data-ttu-id="01cd8-237">Recuperare un elenco di tutti i server gestiti da DPM tramite hello agente DPM.</span><span class="sxs-lookup"><span data-stu-id="01cd8-237">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="01cd8-238">Scegliere un server specifico.</span><span class="sxs-lookup"><span data-stu-id="01cd8-238">Choose a specific server.</span></span>
3. <span data-ttu-id="01cd8-239">Recuperare un elenco di tutte le origini dati nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="01cd8-239">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="01cd8-240">Scegliere uno o più origini dati e aggiungerli toohello gruppo protezione dati</span><span class="sxs-lookup"><span data-stu-id="01cd8-240">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="01cd8-241">elenco di Hello del server in cui hello agente Data Protection Manager è installato e viene gestito dal Server DPM hello viene acquisito con hello [Get DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-241">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="01cd8-242">In questo esempio verrà applicato un filtro e per il backup verrà configurato solo il server di produzione denominato *productionserver01* .</span><span class="sxs-lookup"><span data-stu-id="01cd8-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="01cd8-243">Ora recuperare elenco hello di origini dati in ```$server``` utilizzando hello [Get DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-243">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="01cd8-244">In questo esempio si Filtra per volume hello * unità d:\* che si desidera tooconfigure per il backup.</span><span class="sxs-lookup"><span data-stu-id="01cd8-244">In this example we are filtering for hello volume *D:\* which we want tooconfigure for backup.</span></span> <span data-ttu-id="01cd8-245">L'origine dati viene quindi aggiunto toohello gruppo protezione dati utilizzando hello [Aggiungi DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-245">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="01cd8-246">Ricordare hello toouse *modifable* oggetto gruppo protezione dati ```$MPG``` aggiunte hello toomake.</span><span class="sxs-lookup"><span data-stu-id="01cd8-246">Remember toouse hello *modifable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="01cd8-247">Ripetere questo passaggio il numero di volte in base alle esigenze fino a quando non sono stati aggiunti tutti hello gruppo protezione dati di origini dati toohello scelto.</span><span class="sxs-lookup"><span data-stu-id="01cd8-247">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="01cd8-248">È possibile iniziare con una sola origine dati e del flusso di lavoro hello completo per la creazione di hello gruppo protezione dati e successivamente aggiungere altre origini dati toohello gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="01cd8-248">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="01cd8-249">Selezione metodo protezione dati di hello</span><span class="sxs-lookup"><span data-stu-id="01cd8-249">Selecting hello data protection method</span></span>
<span data-ttu-id="01cd8-250">Dopo aver aggiunto le origini dati hello toohello gruppo protezione dati, passaggio successivo hello è metodo di protezione hello toospecify utilizzando hello [Set DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-250">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="01cd8-251">In questo esempio hello gruppo protezione dati verrà configurato per il disco locale e il backup nel cloud.</span><span class="sxs-lookup"><span data-stu-id="01cd8-251">In this example, hello Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="01cd8-252">È inoltre necessario toospecify hello datasource che si desidera toocloud tooprotect utilizzando hello [Aggiungi DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet con - flag Online.</span><span class="sxs-lookup"><span data-stu-id="01cd8-252">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="01cd8-253">Impostazione di un intervallo di conservazione hello</span><span class="sxs-lookup"><span data-stu-id="01cd8-253">Setting hello retention range</span></span>
<span data-ttu-id="01cd8-254">Impostare il mantenimento dati hello per i punti di backup hello utilizzando hello [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-254">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="01cd8-255">Anche se potrebbe sembrare memorizzazione hello tooset dispari prima di pianificazione del backup hello è stato definito utilizzando hello ```Set-DPMPolicyObjective``` imposta automaticamente una pianificazione di backup predefinito che può quindi essere modificata.</span><span class="sxs-lookup"><span data-stu-id="01cd8-255">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="01cd8-256">È sempre possibile tooset pianificazione del backup hello innanzitutto e hello criteri di conservazione dopo.</span><span class="sxs-lookup"><span data-stu-id="01cd8-256">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="01cd8-257">Nel seguente esempio hello hello imposta i parametri di memorizzazione hello per i backup su disco.</span><span class="sxs-lookup"><span data-stu-id="01cd8-257">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="01cd8-258">Questo verrà conservazione dei backup per 10 giorni e sincronizzare i dati ogni 6 ore tra il server di produzione hello e hello Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="01cd8-258">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="01cd8-259">Hello ```SynchronizationFrequencyMinutes``` non definisce la frequenza con cui un punto di ripristino viene creato, ma come spesso dati sono il server DPM toohello copiati; in questo modo i backup non diventino troppo grandi.</span><span class="sxs-lookup"><span data-stu-id="01cd8-259">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="01cd8-260">Per i backup verranno tooAzure (Data Protection Manager si riferisce toothese come backup in linea) periodi di mantenimento hello possono essere configurati per [utilizzando uno schema nonno-padre-figlio (condivisione file di Groove) di memorizzazione a lungo termine](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="01cd8-260">For backups going tooAzure (DPM refers toothese as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="01cd8-261">Ciò significa che è possibile definire un criterio di conservazione combinato che includa criteri giornalieri, settimanali, mensili e annuali.</span><span class="sxs-lookup"><span data-stu-id="01cd8-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="01cd8-262">In questo esempio è una matrice che rappresenta lo schema di memorizzazione complesso hello che si desidera creare e quindi configurare l'intervallo di conservazione hello utilizzando hello [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-262">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="01cd8-263">Pianificazione del backup hello set</span><span class="sxs-lookup"><span data-stu-id="01cd8-263">Set hello backup schedule</span></span>
<span data-ttu-id="01cd8-264">DPM imposta automaticamente una pianificazione di backup predefinito se si specifica l'obiettivo di protezione di hello utilizzando hello ```Set-DPMPolicyObjective``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-264">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="01cd8-265">le pianificazioni predefinite hello toochange, utilizzare hello [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet seguito da hello [Set DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-265">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="01cd8-266">Nell'esempio hello sopra, ```$onlineSch``` è una matrice con quattro elementi che contiene pianificazione protezione dati online esistente hello per hello gruppo protezione dati nello schema di condivisione file di Groove hello:</span><span class="sxs-lookup"><span data-stu-id="01cd8-266">In hello example above, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="01cd8-267">```$onlineSch[0]```conterrà una pianificazione giornaliera hello</span><span class="sxs-lookup"><span data-stu-id="01cd8-267">```$onlineSch[0]``` will contain hello daily schedule</span></span>
2. <span data-ttu-id="01cd8-268">```$onlineSch[1]```conterrà la pianificazione settimanale hello</span><span class="sxs-lookup"><span data-stu-id="01cd8-268">```$onlineSch[1]``` will contain hello weekly schedule</span></span>
3. <span data-ttu-id="01cd8-269">```$onlineSch[2]```conterrà la pianificazione mensile hello</span><span class="sxs-lookup"><span data-stu-id="01cd8-269">```$onlineSch[2]``` will contain hello monthly schedule</span></span>
4. <span data-ttu-id="01cd8-270">```$onlineSch[3]```conterrà pianificazione annuale hello</span><span class="sxs-lookup"><span data-stu-id="01cd8-270">```$onlineSch[3]``` will contain hello yearly schedule</span></span>

<span data-ttu-id="01cd8-271">Pertanto se è necessaria una pianificazione settimanale di hello toomodify, è necessario toorefer toohello ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="01cd8-271">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="01cd8-272">Backup iniziale</span><span class="sxs-lookup"><span data-stu-id="01cd8-272">Initial backup</span></span>
<span data-ttu-id="01cd8-273">Per eseguire il backup un'origine dati per hello prima volta, DPM deve toocreate una replica iniziale che verrà creata una copia di hello datasource toobe protetti nel volume di replica DPM.</span><span class="sxs-lookup"><span data-stu-id="01cd8-273">When backing up a datasource for hello first time, DPM needs toocreate an initial replica which will create a copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="01cd8-274">Questa attività possono essere pianificata per un momento specifico o può essere attivata manualmente, utilizzando hello [Set DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet con il parametro hello ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="01cd8-274">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="01cd8-275">Modifica delle dimensioni di hello di Replica DPM & volume del punto di ripristino</span><span class="sxs-lookup"><span data-stu-id="01cd8-275">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="01cd8-276">È inoltre possibile modificare le dimensioni di hello del volume di Replica di DPM, nonché la copia Shadow volume mediante [Set DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet come hello di esempio seguente: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-manuale - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="01cd8-276">You can also change hello size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="01cd8-277">Il commit hello modifiche toohello gruppo protezione dati</span><span class="sxs-lookup"><span data-stu-id="01cd8-277">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="01cd8-278">Infine, le modifiche di hello necessario toobe eseguito il commit prima che DPM può eseguire il backup di hello in base alla configurazione di hello nuovo gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="01cd8-278">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="01cd8-279">Questa operazione viene eseguita utilizzando hello [Set DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-279">This is done using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="01cd8-280">Visualizzare i punti di backup hello</span><span class="sxs-lookup"><span data-stu-id="01cd8-280">View hello backup points</span></span>
<span data-ttu-id="01cd8-281">È possibile utilizzare hello [Get DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget cmdlet un elenco di tutti i punti di ripristino per un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="01cd8-281">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="01cd8-282">Nell'esempio seguente, vengono:</span><span class="sxs-lookup"><span data-stu-id="01cd8-282">In this example, we will:</span></span>

* <span data-ttu-id="01cd8-283">recuperare tutti i PGs hello nel server DPM hello che verrà archiviato in una matrice```$PG```</span><span class="sxs-lookup"><span data-stu-id="01cd8-283">fetch all hello PGs on hello DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="01cd8-284">ottenere toohello corrispondente di hello origini dati```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="01cd8-284">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="01cd8-285">ottenere tutti i punti di ripristino hello per un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="01cd8-285">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="01cd8-286">Ripristino dei dati protetti su Azure</span><span class="sxs-lookup"><span data-stu-id="01cd8-286">Restore data protected on Azure</span></span>
<span data-ttu-id="01cd8-287">Il ripristino dei dati è una combinazione tra un oggetto ```RecoverableItem``` e un oggetto ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="01cd8-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="01cd8-288">Nella sezione precedente hello, abbiamo un elenco di punti di backup hello per un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="01cd8-288">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="01cd8-289">Nell'esempio hello riportato di seguito viene illustrato come macchina virtuale di Hyper-V toorestore da Azure Backup dai punti di backup in combinazione con hello destinazione per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="01cd8-289">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="01cd8-290">Sono inclusi:</span><span class="sxs-lookup"><span data-stu-id="01cd8-290">This includes:</span></span>

* <span data-ttu-id="01cd8-291">Creazione di un'opzione di ripristino utilizzando hello [New DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-291">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="01cd8-292">Matrice di hello recupero dei punti di backup utilizzando hello ```Get-DPMRecoveryPoint``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01cd8-292">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="01cd8-293">Scelta di un backup toorestore punto da.</span><span class="sxs-lookup"><span data-stu-id="01cd8-293">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="01cd8-294">i comandi di Hello possono essere facilmente esteso per qualsiasi tipo di origine dati.</span><span class="sxs-lookup"><span data-stu-id="01cd8-294">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01cd8-295">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="01cd8-295">Next steps</span></span>
* <span data-ttu-id="01cd8-296">Per ulteriori informazioni sui Backup di Azure per DPM vedere [tooDPM introduzione Backup](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="01cd8-296">For more information about Azure Backup for DPM see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
