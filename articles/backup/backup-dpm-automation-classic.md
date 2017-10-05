---
title: 'Backup di Azure: utilizzare PowerShell per eseguire il backup dei carichi di lavoro DPM | Documentazione Microsoft'
description: Informazioni su come distribuire e gestire Backup di Azure per Data Protection Manager (DPM) usando PowerShell
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
ms.openlocfilehash: 943a12dcba49a114d206b9dab968da332ea99926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="51bec-103">Distribuire e gestire il backup in Azure per server Data Protection Manager (DPM) mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="51bec-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="51bec-104">ARM</span><span class="sxs-lookup"><span data-stu-id="51bec-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="51bec-105">Classico</span><span class="sxs-lookup"><span data-stu-id="51bec-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="51bec-106">Questo articolo spiega come usare PowerShell per il backup e il ripristino di dati di DPM da un insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="51bec-106">This article explains how to use PowerShell to back up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="51bec-107">Microsoft consiglia l'uso di insiemi di credenziali dei Servizi di ripristino per tutte le nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="51bec-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="51bec-108">Se si è un nuovo utente di Backup di Azure, vedere l'articolo [Distribuire e gestire i dati di Data Protection Manager in Azure mediante PowerShell](backup-dpm-automation.md), in modo da archiviare i dati in un insieme di credenziali dei Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="51bec-108">If you are a new Azure Backup user, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51bec-109">È ora possibile aggiornare gli insiemi di credenziali di Backup ad insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="51bec-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="51bec-110">Per altre informazioni, vedere l'articolo [Aggiornare un insieme di credenziali di Backup a un insieme di credenziali di Servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="51bec-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="51bec-111">Microsoft consiglia di aggiornare gli insiemi di credenziali di Backup a insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="51bec-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="51bec-112">Dopo il 15 ottobre 2017 non sarà possibile usare PowerShell per creare insiemi di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="51bec-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="51bec-113">**Entro il 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="51bec-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="51bec-114">Tutti gli insiemi di credenziali di backup rimanenti verranno aggiornati automaticamente a insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="51bec-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="51bec-115">e non sarà più possibile accedere ai dati di backup nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="51bec-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="51bec-116">Sarà possibile invece usare il portale di Azure per accedere ai dati di backup negli insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="51bec-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="51bec-117">Configurazione dell'ambiente di PowerShell</span><span class="sxs-lookup"><span data-stu-id="51bec-117">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="51bec-118">Prima di poter usare PowerShell per gestire i backup da Data Protection Manager ad Azure, sarà necessario disporre dell'ambiente appropriato in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51bec-118">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you will need to have the right environment in PowerShell.</span></span> <span data-ttu-id="51bec-119">All'inizio della sessione di PowerShell, assicurarsi di eseguire il comando seguente per importare i moduli appropriati e fare riferimento correttamente ai cmdlet DPM:</span><span class="sxs-lookup"><span data-stu-id="51bec-119">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome to the DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="51bec-120">Installazione e registrazione</span><span class="sxs-lookup"><span data-stu-id="51bec-120">Setup and Registration</span></span>
<span data-ttu-id="51bec-121">Per iniziare:</span><span class="sxs-lookup"><span data-stu-id="51bec-121">To begin:</span></span>

1. <span data-ttu-id="51bec-122">[Scaricare la versione più recente di PowerShell](https://github.com/Azure/azure-powershell/releases) (la versione minima richiesta è: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="51bec-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="51bec-123">Per iniziare, abilitare i cmdlet del servizio Backup di Azure passando alla modalità *AzureResourceManager* usando il cmdlet **Switch-AzureMode** :</span><span class="sxs-lookup"><span data-stu-id="51bec-123">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="51bec-124">Le attività di installazione e registrazione seguenti possono essere automatizzate tramite PowerShell:</span><span class="sxs-lookup"><span data-stu-id="51bec-124">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="51bec-125">Creare un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="51bec-125">Create a backup vault</span></span>
* <span data-ttu-id="51bec-126">Installazione dell'agente di Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="51bec-126">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="51bec-127">Registrazione del servizio Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="51bec-127">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="51bec-128">Impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="51bec-128">Networking settings</span></span>
* <span data-ttu-id="51bec-129">Impostazioni crittografia</span><span class="sxs-lookup"><span data-stu-id="51bec-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="51bec-130">Creare un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="51bec-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="51bec-131">I clienti che usano il servizio Backup di Azure per la prima volta, dovranno registrare il provider di Backup di Azure da usare con la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="51bec-131">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="51bec-132">A tale scopo, eseguire il comando seguente: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="51bec-132">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="51bec-133">È possibile creare un nuovo insieme di credenziali per il backup usando il cmdlet **New-AzureRMBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="51bec-133">You can create a new backup vault using the **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="51bec-134">L’archivio di backup è una risorsa ARM, pertanto è necessario inserirlo all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="51bec-134">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="51bec-135">Eseguire i comandi seguenti in una console di Azure PowerShell con privilegi elevati:</span><span class="sxs-lookup"><span data-stu-id="51bec-135">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="51bec-136">È possibile ottenere un elenco di tutti gli insiemi di credenziali per il backup in una determinata sottoscrizione usando il cmdlet **Get-AzureRMBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="51bec-136">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="51bec-137">Installazione dell'agente di Backup di Azure in un server DPM</span><span class="sxs-lookup"><span data-stu-id="51bec-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="51bec-138">Per installare l'agente di Backup di Azure, è necessario aver scaricato il programma di installazione nel server Windows.</span><span class="sxs-lookup"><span data-stu-id="51bec-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="51bec-139">È possibile ottenere la versione più recente del programma di installazione dall' [Area download Microsoft](http://aka.ms/azurebackup_agent) .o dalla pagina Dashboard dell’archivio di backup.</span><span class="sxs-lookup"><span data-stu-id="51bec-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="51bec-140">Salvare il programma di installazione in un percorso facilmente accessibile come *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="51bec-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="51bec-141">Per installare l'agente, eseguire il comando seguente in una console di PowerShell con privilegi elevati **nel server DPM**:</span><span class="sxs-lookup"><span data-stu-id="51bec-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="51bec-142">L'agente verrà installato con tutte le opzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="51bec-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="51bec-143">L'installazione richiede alcuni minuti in background.</span><span class="sxs-lookup"><span data-stu-id="51bec-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="51bec-144">Se non si specifica l'opzione */nu* , la finestra **Windows Update** si aprirà al termine dell'installazione per verificare la presenza di eventuali aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="51bec-144">If you do not specify the */nu* option the **Windows Update** window will open at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="51bec-145">L'agente verrà visualizzato nell'elenco dei programmi installati.</span><span class="sxs-lookup"><span data-stu-id="51bec-145">The agent will show in the list of installed programs.</span></span> <span data-ttu-id="51bec-146">Per visualizzare l'elenco dei programmi installati, passare a **Pannello di controllo** > **Programmi** > **Programmi e funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="51bec-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente installato](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="51bec-148">Opzioni di installazione</span><span class="sxs-lookup"><span data-stu-id="51bec-148">Installation options</span></span>
<span data-ttu-id="51bec-149">Per visualizzare tutte le opzioni disponibili tramite la riga di comando, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="51bec-149">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="51bec-150">Le opzioni disponibili includono:</span><span class="sxs-lookup"><span data-stu-id="51bec-150">The available options include:</span></span>

| <span data-ttu-id="51bec-151">Opzione</span><span class="sxs-lookup"><span data-stu-id="51bec-151">Option</span></span> | <span data-ttu-id="51bec-152">Dettagli</span><span class="sxs-lookup"><span data-stu-id="51bec-152">Details</span></span> | <span data-ttu-id="51bec-153">Default</span><span class="sxs-lookup"><span data-stu-id="51bec-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="51bec-154">/q</span><span class="sxs-lookup"><span data-stu-id="51bec-154">/q</span></span> |<span data-ttu-id="51bec-155">Installazione non interattiva</span><span class="sxs-lookup"><span data-stu-id="51bec-155">Quiet installation</span></span> |- |
| <span data-ttu-id="51bec-156">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="51bec-156">/p:"location"</span></span> |<span data-ttu-id="51bec-157">Percorso della cartella di installazione per l'agente di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="51bec-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="51bec-158">C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="51bec-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="51bec-159">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="51bec-159">/s:"location"</span></span> |<span data-ttu-id="51bec-160">Percorso della cartella della cache per l'agente di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="51bec-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="51bec-161">C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure\Scratch</span><span class="sxs-lookup"><span data-stu-id="51bec-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="51bec-162">/m</span><span class="sxs-lookup"><span data-stu-id="51bec-162">/m</span></span> |<span data-ttu-id="51bec-163">Consenso esplicito a Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="51bec-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="51bec-164">/nu</span><span class="sxs-lookup"><span data-stu-id="51bec-164">/nu</span></span> |<span data-ttu-id="51bec-165">Al termine dell'installazione non vengono cercati gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="51bec-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="51bec-166">/d</span><span class="sxs-lookup"><span data-stu-id="51bec-166">/d</span></span> |<span data-ttu-id="51bec-167">Disinstalla l'agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="51bec-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="51bec-168">/ph</span><span class="sxs-lookup"><span data-stu-id="51bec-168">/ph</span></span> |<span data-ttu-id="51bec-169">Indirizzo host proxy</span><span class="sxs-lookup"><span data-stu-id="51bec-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="51bec-170">/po</span><span class="sxs-lookup"><span data-stu-id="51bec-170">/po</span></span> |<span data-ttu-id="51bec-171">Numero porta host proxy</span><span class="sxs-lookup"><span data-stu-id="51bec-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="51bec-172">/pu</span><span class="sxs-lookup"><span data-stu-id="51bec-172">/pu</span></span> |<span data-ttu-id="51bec-173">Nome utente host proxy</span><span class="sxs-lookup"><span data-stu-id="51bec-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="51bec-174">/pw</span><span class="sxs-lookup"><span data-stu-id="51bec-174">/pw</span></span> |<span data-ttu-id="51bec-175">Password proxy</span><span class="sxs-lookup"><span data-stu-id="51bec-175">Proxy Password</span></span> |- |

### <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="51bec-176">Registrazione del servizio Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="51bec-176">Registering with the Azure Backup service</span></span>
<span data-ttu-id="51bec-177">Per poter eseguire la registrazione con il servizio Backup di Azure, è necessario assicurarsi che i [prerequisiti](backup-azure-dpm-introduction.md) siano soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="51bec-177">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="51bec-178">È necessario:</span><span class="sxs-lookup"><span data-stu-id="51bec-178">You must:</span></span>

* <span data-ttu-id="51bec-179">Avere una sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="51bec-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="51bec-180">Ottieni un archivio di backup</span><span class="sxs-lookup"><span data-stu-id="51bec-180">Have a backup vault</span></span>

<span data-ttu-id="51bec-181">Per scaricare le credenziali dell'archivio, eseguire il commandlet **Get AzureBackupVaultCredentials** in una console Azure PowerShell e archiviarlo in una posizione comoda come *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="51bec-181">To download the vault credentials, run the **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="51bec-182">La registrazione del computer con l'insieme di credenziali viene eseguita utilizzando il cmdlet [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) :</span><span class="sxs-lookup"><span data-stu-id="51bec-182">Registering the machine with the vault is done using the [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="51bec-183">In questo modo, il server DPM denominato "TestingServer" verrà registrato con l'insieme di credenziali di Microsoft Azure usando le credenziali specificate.</span><span class="sxs-lookup"><span data-stu-id="51bec-183">This will register the DPM Server named “TestingServer” with Microsoft Azure Vault using the specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51bec-184">Non utilizzare percorsi relativi per specificare il file dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="51bec-184">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="51bec-185">È necessario fornire un percorso assoluto come input per il cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51bec-185">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="51bec-186">Impostazioni di configurazione iniziali</span><span class="sxs-lookup"><span data-stu-id="51bec-186">Initial configuration settings</span></span>
<span data-ttu-id="51bec-187">Una volta registrato il server DPM con l'insieme di credenziali di Backup di Azure, il server verrà avviato con le impostazioni di sottoscrizione predefinite.</span><span class="sxs-lookup"><span data-stu-id="51bec-187">Once the DPM Server is registered with the Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="51bec-188">Tali impostazioni includono rete, crittografia e area di staging.</span><span class="sxs-lookup"><span data-stu-id="51bec-188">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="51bec-189">Per iniziare a modificare le impostazioni di sottoscrizione, è necessario innanzitutto ottenere un handle sulle impostazioni (predefinite) esistenti usando il cmdlet [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) :</span><span class="sxs-lookup"><span data-stu-id="51bec-189">To begin changing the subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="51bec-190">Tutte le modifiche vengono apportate a questo oggetto locale PowerShell ```$setting``` e poi viene eseguito il commit dell'oggetto completo in DPM e in Backup di Azure eseguendo il salvataggio mediante il cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791).</span><span class="sxs-lookup"><span data-stu-id="51bec-190">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="51bec-191">È necessario usare il flag ```–Commit``` per garantire che le modifiche vengano mantenute.</span><span class="sxs-lookup"><span data-stu-id="51bec-191">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="51bec-192">Le impostazioni vengono applicate e usate da Backup di Azure solo dopo il commit.</span><span class="sxs-lookup"><span data-stu-id="51bec-192">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="51bec-193">Rete</span><span class="sxs-lookup"><span data-stu-id="51bec-193">Networking</span></span>
<span data-ttu-id="51bec-194">Se la connettività del computer DPM al servizio Backup di Azure in Internet usa un server proxy, per consentire la corretta esecuzione dei backup è necessario fornire le impostazioni del server proxy.</span><span class="sxs-lookup"><span data-stu-id="51bec-194">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for backups to succeed.</span></span> <span data-ttu-id="51bec-195">A tale scopo, usare i parametri ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` e ```ProxyPassword``` con il cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791).</span><span class="sxs-lookup"><span data-stu-id="51bec-195">This is done by using the ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="51bec-196">In questo esempio non esiste alcun server proxy, pertanto sono state eliminate tutte le informazioni relative al proxy.</span><span class="sxs-lookup"><span data-stu-id="51bec-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="51bec-197">È anche possibile controllare l'utilizzo della larghezza di banda con le opzioni ```-WorkHourBandwidth``` e ```-NonWorkHourBandwidth``` per un determinato set di giorni della settimana.</span><span class="sxs-lookup"><span data-stu-id="51bec-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="51bec-198">In questo esempio non viene impostata alcuna limitazione.</span><span class="sxs-lookup"><span data-stu-id="51bec-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-the-staging-area"></a><span data-ttu-id="51bec-199">Configurazione dell'area di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="51bec-199">Configuring the staging Area</span></span>
<span data-ttu-id="51bec-200">L'agente del servizio Backup di Azure in esecuzione nel server DPM deve disporre di archiviazione temporanea per i dati ripristinati dal cloud (area di staging locale).</span><span class="sxs-lookup"><span data-stu-id="51bec-200">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="51bec-201">Configurare l'area di gestione temporanea usando il cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) e il parametro ```-StagingAreaPath```.</span><span class="sxs-lookup"><span data-stu-id="51bec-201">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="51bec-202">Nell'esempio precedente, l'area di gestione temporanea verrà impostata su *C:\StagingArea* nell'oggetto di PowerShell ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="51bec-202">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="51bec-203">Assicurarsi che la cartella specificata esista già, altrimenti il commit finale delle impostazioni di sottoscrizione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="51bec-203">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="51bec-204">Impostazioni crittografia</span><span class="sxs-lookup"><span data-stu-id="51bec-204">Encryption settings</span></span>
<span data-ttu-id="51bec-205">I dati di backup inviati a Backup di Azure vengono crittografati per proteggere la riservatezza dei dati.</span><span class="sxs-lookup"><span data-stu-id="51bec-205">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="51bec-206">La passphrase di crittografia è la "password" per decrittografare i dati in fase di ripristino.</span><span class="sxs-lookup"><span data-stu-id="51bec-206">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="51bec-207">È importante conservarla al sicuro e proteggerla dopo averla impostata.</span><span class="sxs-lookup"><span data-stu-id="51bec-207">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="51bec-208">Nel seguente esempio, il primo comando consente di convertire la passphrase della stringa ```passphrase123456789``` in una stringa sicura; inoltre, consente di assegnare la stringa sicura alla variabile denominata ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="51bec-208">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="51bec-209">Il secondo comando imposta la stringa sicura in ```$Passphrase``` come password per la crittografia dei backup.</span><span class="sxs-lookup"><span data-stu-id="51bec-209">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="51bec-210">Dopo l'impostazione, conservare le informazioni sulla passphrase al sicuro.</span><span class="sxs-lookup"><span data-stu-id="51bec-210">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="51bec-211">Non sarà possibile ripristinare i dati da Azure senza la passphrase.</span><span class="sxs-lookup"><span data-stu-id="51bec-211">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="51bec-212">A questo punto, sono state apportate tutte le modifiche necessarie all'oggetto ```$setting``` .</span><span class="sxs-lookup"><span data-stu-id="51bec-212">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="51bec-213">Ricordarsi di eseguire il commit delle modifiche:</span><span class="sxs-lookup"><span data-stu-id="51bec-213">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="51bec-214">Proteggere i dati in Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="51bec-214">Protect data to Azure Backup</span></span>
<span data-ttu-id="51bec-215">In questa sezione verrà aggiunto un server di produzione a DPM e i dati verranno protetti nell'archivio DPM locale e quindi in Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="51bec-215">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="51bec-216">Negli esempi, viene descritto come eseguire il backup di file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="51bec-216">In the examples we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="51bec-217">È possibile estendere in modo semplice la logica al fine di eseguire il backup di qualsiasi origine dati supportata da DPM.</span><span class="sxs-lookup"><span data-stu-id="51bec-217">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="51bec-218">Tutti i backup DPM sono regolati da un gruppo protezione dati costituito da quattro parti:</span><span class="sxs-lookup"><span data-stu-id="51bec-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="51bec-219">**Membri del gruppo** : elenco di tutti gli oggetti che è possibile proteggere (anche detti *origini dati* in DPM) e che si desidera proteggere nello stesso gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="51bec-219">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="51bec-220">Ad esempio, è possibile proteggere le macchine virtuali di produzione in un gruppo protezione dati e i database di SQL Server in un altro gruppo, in quanto potrebbero avere requisiti di backup diversi.</span><span class="sxs-lookup"><span data-stu-id="51bec-220">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="51bec-221">Prima di eseguire il backup di qualsiasi origine dati in un server di produzione, è necessario assicurarsi che l'agente DPM sia installato nel server e gestito da DPM.</span><span class="sxs-lookup"><span data-stu-id="51bec-221">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="51bec-222">Seguire la procedura di [installazione dell'agente DPM](https://technet.microsoft.com/library/bb870935.aspx) e collegamento dell'agente al server DPM appropriato.</span><span class="sxs-lookup"><span data-stu-id="51bec-222">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="51bec-223">**Metodo di protezione dati** : specifica le posizioni di destinazione dei backup, ad esempio nastro, disco e cloud.</span><span class="sxs-lookup"><span data-stu-id="51bec-223">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="51bec-224">In questo esempio i dati verranno protetti nel disco locale e nel cloud.</span><span class="sxs-lookup"><span data-stu-id="51bec-224">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="51bec-225">**Pianificazione dei backup** : specifica quando devono essere eseguiti i backup e con quale frequenza i dati devono essere sincronizzati tra il server DPM e il server di produzione.</span><span class="sxs-lookup"><span data-stu-id="51bec-225">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="51bec-226">Una **pianificazione di conservazione** che indica per quanto tempo è necessario conservare i punti di ripristino in Azure.</span><span class="sxs-lookup"><span data-stu-id="51bec-226">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="51bec-227">Creazione di un gruppo di protezione</span><span class="sxs-lookup"><span data-stu-id="51bec-227">Creating a protection group</span></span>
<span data-ttu-id="51bec-228">Creare innanzitutto un nuovo gruppo protezione dati usando il cmdlet [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) .</span><span class="sxs-lookup"><span data-stu-id="51bec-228">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="51bec-229">Il cmdlet precedente creerà un gruppo protezione dati denominato *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="51bec-229">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="51bec-230">Un gruppo protezione dati esistente può anche essere modificato in seguito per aggiungere il backup nel cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="51bec-230">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="51bec-231">Tuttavia, per apportare modifiche al gruppo protezione dati, nuovo o esistente, è necessario ottenere un handle su un oggetto *modificabile* usando il cmdlet [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) .</span><span class="sxs-lookup"><span data-stu-id="51bec-231">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="51bec-232">Aggiunta di membri al gruppo protezione dati</span><span class="sxs-lookup"><span data-stu-id="51bec-232">Adding group members to the Protection Group</span></span>
<span data-ttu-id="51bec-233">Ogni agente DPM conosce l'elenco di origini dati nel server in cui è installato.</span><span class="sxs-lookup"><span data-stu-id="51bec-233">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="51bec-234">Per aggiungere un'origine dati al gruppo protezione dati, l'agente DPM deve innanzitutto inviare un elenco delle origini dati al server DPM.</span><span class="sxs-lookup"><span data-stu-id="51bec-234">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="51bec-235">Vengono quindi selezionate una o più origini dati, che vengono aggiunte al gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="51bec-235">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="51bec-236">La procedura di PowerShell da eseguire a questo scopo è la seguente:</span><span class="sxs-lookup"><span data-stu-id="51bec-236">The PowerShell steps needed to get achieve this are:</span></span>

1. <span data-ttu-id="51bec-237">Recuperare un elenco di tutti i server gestiti da DPM tramite l'agente DPM.</span><span class="sxs-lookup"><span data-stu-id="51bec-237">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="51bec-238">Scegliere un server specifico.</span><span class="sxs-lookup"><span data-stu-id="51bec-238">Choose a specific server.</span></span>
3. <span data-ttu-id="51bec-239">Recuperare un elenco di tutte le origini dati nel server.</span><span class="sxs-lookup"><span data-stu-id="51bec-239">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="51bec-240">Scegliere una o più origini dati e aggiungerle al gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="51bec-240">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="51bec-241">È possibile acquisire l'elenco di tutti i server in cui è installato l'agente DPM e che sono gestiti dal server DPM tramite il cmdlet [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) .</span><span class="sxs-lookup"><span data-stu-id="51bec-241">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="51bec-242">In questo esempio verrà applicato un filtro e per il backup verrà configurato solo il server di produzione denominato *productionserver01* .</span><span class="sxs-lookup"><span data-stu-id="51bec-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="51bec-243">Recuperare quindi l'elenco di origini dati in ```$server``` usando il cmdlet [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605).</span><span class="sxs-lookup"><span data-stu-id="51bec-243">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="51bec-244">In questo esempio viene filtrato il volume *D:\*, da configurare per il backup.</span><span class="sxs-lookup"><span data-stu-id="51bec-244">In this example we are filtering for the volume *D:\* which we want to configure for backup.</span></span> <span data-ttu-id="51bec-245">L'origine dati viene quindi aggiunta al gruppo protezione dati usando il cmdlet [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732).</span><span class="sxs-lookup"><span data-stu-id="51bec-245">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="51bec-246">Ricordarsi di usare l'oggetto gruppo protezione dati *modificabile* ```$MPG``` per effettuare le aggiunte.</span><span class="sxs-lookup"><span data-stu-id="51bec-246">Remember to use the *modifable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="51bec-247">Ripetere questo passaggio il numero di volte necessario per aggiungere tutte le origini dati scelte al gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="51bec-247">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="51bec-248">È anche possibile iniziare con una sola origine dati e completare il flusso di lavoro per la creazione del gruppo protezione dati, quindi, in un secondo momento, aggiungere altre origini dati al gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="51bec-248">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="51bec-249">Selezione del metodo di protezione dati</span><span class="sxs-lookup"><span data-stu-id="51bec-249">Selecting the data protection method</span></span>
<span data-ttu-id="51bec-250">Una volta aggiunte le origini dati al gruppo protezione dati, il passaggio successivo consiste nello specificare il metodo di protezione usando il cmdlet [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) .</span><span class="sxs-lookup"><span data-stu-id="51bec-250">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="51bec-251">In questo esempio il gruppo protezione dati verrà configurato per il backup su disco locale e nel cloud.</span><span class="sxs-lookup"><span data-stu-id="51bec-251">In this example, the Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="51bec-252">È inoltre necessario specificare l'origine dati che si desidera proteggere per il cloud utilizzando il cmdlet [Aggiungi DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) con -flag Online.</span><span class="sxs-lookup"><span data-stu-id="51bec-252">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="51bec-253">Impostazione del periodo di mantenimento dati</span><span class="sxs-lookup"><span data-stu-id="51bec-253">Setting the retention range</span></span>
<span data-ttu-id="51bec-254">Impostare il periodo di conservazione per i punti di backup usando il cmdlet [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="51bec-254">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="51bec-255">Anche se può sembrare strano impostare il periodo di conservazione prima di definire la pianificazione dei backup, usando il cmdlet ```Set-DPMPolicyObjective``` viene automaticamente impostata una pianificazione dei backup predefinita che può quindi essere modificata.</span><span class="sxs-lookup"><span data-stu-id="51bec-255">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="51bec-256">È sempre possibile impostare prima la pianificazione dei backup e successivamente i criteri di conservazione.</span><span class="sxs-lookup"><span data-stu-id="51bec-256">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="51bec-257">Nell'esempio seguente il cmdlet imposta i parametri di conservazione per i backup su disco.</span><span class="sxs-lookup"><span data-stu-id="51bec-257">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="51bec-258">I backup verranno conservati per 10 giorni e i dati verranno sincronizzati ogni 6 ore tra il server di produzione e il server DPM.</span><span class="sxs-lookup"><span data-stu-id="51bec-258">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="51bec-259">```SynchronizationFrequencyMinutes``` non definisce la frequenza di creazione di un punto di backup, ma la frequenza con cui i dati vengono copiati nel server DPM. In questo modo, si impedisce che i backup diventino troppo grossi.</span><span class="sxs-lookup"><span data-stu-id="51bec-259">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="51bec-260">Per i backup destinati ad Azure (indicati in DPM come backup online), è possibile configurare i periodi di mantenimento dati per la [conservazione a lungo termine usando uno schema GFS (Grandfather-Father-Son, nonno-padre-figlio)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="51bec-260">For backups going to Azure (DPM refers to these as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="51bec-261">Ciò significa che è possibile definire un criterio di conservazione combinato che includa criteri giornalieri, settimanali, mensili e annuali.</span><span class="sxs-lookup"><span data-stu-id="51bec-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="51bec-262">In questo esempio viene creata una matrice che rappresenta lo schema di conservazione complesso desiderato e quindi viene configurato il periodo di mantenimento dati usando il cmdlet [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="51bec-262">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="51bec-263">Impostare la pianificazione dei backup</span><span class="sxs-lookup"><span data-stu-id="51bec-263">Set the backup schedule</span></span>
<span data-ttu-id="51bec-264">Se si specifica l'obiettivo di protezione usando il cmdlet ```Set-DPMPolicyObjective``` , DPM imposta automaticamente una pianificazione dei backup predefinita.</span><span class="sxs-lookup"><span data-stu-id="51bec-264">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="51bec-265">Per modificare le pianificazioni predefinite, usare il cmdlet [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749), seguito da quello [Set DPMPolicySchedule](https://technet.microsoft.com/library/hh881723).</span><span class="sxs-lookup"><span data-stu-id="51bec-265">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="51bec-266">Nell'esempio precedente ```$onlineSch``` è una matrice con quattro elementi che contiene la pianificazione della protezione online esistente per il gruppo protezione dati nello schema GFS:</span><span class="sxs-lookup"><span data-stu-id="51bec-266">In the example above, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="51bec-267">```$onlineSch[0]``` conterrà la pianificazione giornaliera</span><span class="sxs-lookup"><span data-stu-id="51bec-267">```$onlineSch[0]``` will contain the daily schedule</span></span>
2. <span data-ttu-id="51bec-268">```$onlineSch[1]``` conterrà la pianificazione settimanale</span><span class="sxs-lookup"><span data-stu-id="51bec-268">```$onlineSch[1]``` will contain the weekly schedule</span></span>
3. <span data-ttu-id="51bec-269">```$onlineSch[2]``` conterrà la pianificazione mensile</span><span class="sxs-lookup"><span data-stu-id="51bec-269">```$onlineSch[2]``` will contain the monthly schedule</span></span>
4. <span data-ttu-id="51bec-270">```$onlineSch[3]``` conterrà la pianificazione annuale</span><span class="sxs-lookup"><span data-stu-id="51bec-270">```$onlineSch[3]``` will contain the yearly schedule</span></span>

<span data-ttu-id="51bec-271">Se pertanto è necessario modificare la pianificazione settimanale, è necessario fare riferimento a ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="51bec-271">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="51bec-272">Backup iniziale</span><span class="sxs-lookup"><span data-stu-id="51bec-272">Initial backup</span></span>
<span data-ttu-id="51bec-273">Quando si esegue il backup di un'origine dati per la prima volta, DPM deve creare una replica iniziale che a sua volta creerà una copia dell'origine dati da proteggere nel volume di replica DPM.</span><span class="sxs-lookup"><span data-stu-id="51bec-273">When backing up a datasource for the first time, DPM needs to create an initial replica which will create a copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="51bec-274">È possibile pianificare questa attività a un orario specifico oppure attivarla manualmente, usando il cmdlet [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) con il parametro ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="51bec-274">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="51bec-275">Modifica delle dimensioni della replica DPM e volume del punto di ripristino</span><span class="sxs-lookup"><span data-stu-id="51bec-275">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="51bec-276">È inoltre possibile modificare le dimensioni del volume della replica DPM e del volume copia shadow [utilizzando il cmdlet Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) come nell'esempio seguente: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span><span class="sxs-lookup"><span data-stu-id="51bec-276">You can also change the size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="51bec-277">Commit delle modifiche nel gruppo protezione dati</span><span class="sxs-lookup"><span data-stu-id="51bec-277">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="51bec-278">Infine, è necessario eseguire il commit delle modifiche affinché DPM possa eseguire il backup in base alla nuova configurazione del gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="51bec-278">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="51bec-279">A tale scopo, usare il cmdlet [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) .</span><span class="sxs-lookup"><span data-stu-id="51bec-279">This is done using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="51bec-280">Visualizzare i punti di backup</span><span class="sxs-lookup"><span data-stu-id="51bec-280">View the backup points</span></span>
<span data-ttu-id="51bec-281">È possibile usare il cmdlet [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) per ottenere un elenco di tutti i punti di ripristino per un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="51bec-281">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="51bec-282">Nell'esempio seguente, vengono:</span><span class="sxs-lookup"><span data-stu-id="51bec-282">In this example, we will:</span></span>

* <span data-ttu-id="51bec-283">recuperati tutti i gruppi di protezione (PG) nel server DPM da archiviare in una matrice ```$PG```</span><span class="sxs-lookup"><span data-stu-id="51bec-283">fetch all the PGs on the DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="51bec-284">ottenuti le origini dati corrispondenti alla matrice ```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="51bec-284">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="51bec-285">ottenuti tutti i punti di ripristino per un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="51bec-285">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="51bec-286">Ripristino dei dati protetti su Azure</span><span class="sxs-lookup"><span data-stu-id="51bec-286">Restore data protected on Azure</span></span>
<span data-ttu-id="51bec-287">Il ripristino dei dati è una combinazione tra un oggetto ```RecoverableItem``` e un oggetto ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="51bec-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="51bec-288">Nella sezione precedente è stato ottenuto un elenco dei punti di backup per un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="51bec-288">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="51bec-289">Nell'esempio seguente viene illustrato come ripristinare una macchina virtuale Hyper-V da Backup di Azure mediante la combinazione di punti di backup con la destinazione per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="51bec-289">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="51bec-290">Sono inclusi:</span><span class="sxs-lookup"><span data-stu-id="51bec-290">This includes:</span></span>

* <span data-ttu-id="51bec-291">Creazione di un'opzione di ripristino usando il cmdlet [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592).</span><span class="sxs-lookup"><span data-stu-id="51bec-291">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="51bec-292">Recupero della matrice di punti di backup usando il cmdlet ```Get-DPMRecoveryPoint``` .</span><span class="sxs-lookup"><span data-stu-id="51bec-292">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="51bec-293">Scelta di un punto di backup da cui eseguire il ripristino.</span><span class="sxs-lookup"><span data-stu-id="51bec-293">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="51bec-294">I comandi possono essere facilmente estesi per qualsiasi tipo di origine dati.</span><span class="sxs-lookup"><span data-stu-id="51bec-294">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51bec-295">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="51bec-295">Next steps</span></span>
* <span data-ttu-id="51bec-296">Per altre informazioni su Backup di Azure per DPM, vedere [Introduzione al backup di DPM](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="51bec-296">For more information about Azure Backup for DPM see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
