---
title: Utilizzare PowerShell per gestire i backup di Windows Server in Azure | Documentazione Microsoft
description: Distribuire e gestire backup di Windows Server mediante PowerShell.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: e7e269e2-1f11-41a9-957b-a2155de6a1e0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: saurse;markgal;nkolli;trinadhk
ms.openlocfilehash: a8e20356ae383ee4fa2158ea544d5d0905028124
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="f66da-103">Distribuire e gestire il backup in Azure per server Windows/client Windows mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="f66da-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f66da-104">ARM</span><span class="sxs-lookup"><span data-stu-id="f66da-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="f66da-105">Classico</span><span class="sxs-lookup"><span data-stu-id="f66da-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="f66da-106">Questo articolo spiega come usare PowerShell per eseguire il backup dei dati di una workstation Windows Server o Windows in un insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="f66da-106">This article explains how to use PowerShell to back up Windows Server or Windows workstation data to a backup vault.</span></span> <span data-ttu-id="f66da-107">Microsoft consiglia l'uso di insiemi di credenziali dei Servizi di ripristino per tutte le nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="f66da-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="f66da-108">Per i nuovi utenti di Backup di Microsoft Azure che non hanno creato un insieme di credenziali di backup nella propria sottoscrizione è consigliabile leggere l'articolo [Distribuire e gestire i dati di Data Protection Manager in Azure mediante PowerShell](backup-client-automation.md) per archiviare i dati in un insieme di credenziali dei Servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f66da-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f66da-109">È ora possibile aggiornare gli insiemi di credenziali di Backup ad insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f66da-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="f66da-110">Per altre informazioni, vedere l'articolo [Aggiornare un insieme di credenziali di Backup a un insieme di credenziali di Servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="f66da-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="f66da-111">Microsoft consiglia di aggiornare gli insiemi di credenziali di Backup a insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f66da-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="f66da-112">Dopo il 15 ottobre 2017 non sarà possibile usare PowerShell per creare insiemi di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="f66da-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="f66da-113">**Entro il 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="f66da-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="f66da-114">Tutti gli insiemi di credenziali di backup rimanenti verranno aggiornati automaticamente a insiemi di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f66da-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="f66da-115">e non sarà più possibile accedere ai dati di backup nel portale classico.</span><span class="sxs-lookup"><span data-stu-id="f66da-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="f66da-116">Sarà possibile invece usare il portale di Azure per accedere ai dati di backup negli insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f66da-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="f66da-117">Installare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f66da-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="f66da-118">A ottobre 2015 è stato rilasciato Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="f66da-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="f66da-119">Questa versione ha fatto seguito alla versione 0.9.8 introducendo alcune modifiche significative, in particolare nel modello di denominazione dei cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f66da-119">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span></span> <span data-ttu-id="f66da-120">I cmdlet 1.0 seguono il criterio di denominazione {verb}-AzureRm{noun}, mentre i nomi 0.9.8 non includono **Rm** (ad esempio, New-AzureRmResourceGroup anziché New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="f66da-120">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="f66da-121">Quando si usa Azure PowerShell 0.9.8, è innanzitutto necessario abilitare la modalità Gestione risorse eseguendo il comando **Switch-AzureMode AzureResourceManager** .</span><span class="sxs-lookup"><span data-stu-id="f66da-121">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="f66da-122">Questo comando non è necessario nella versione di 1.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="f66da-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="f66da-123">Se si vogliono usare script scritti per l'ambiente 0.9.8 nell'ambiente 1.0 o versione successiva, occorre testare attentamente gli script in un ambiente di preproduzione prima di usarli nell'ambiente di produzione, per evitare un impatto non previsto.</span><span class="sxs-lookup"><span data-stu-id="f66da-123">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span></span>

<span data-ttu-id="f66da-124">[Scaricare la versione più recente di PowerShell](https://github.com/Azure/azure-powershell/releases) (la versione minima richiesta è: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="f66da-124">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="f66da-125">Creare un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="f66da-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="f66da-126">I clienti che usano il servizio Backup di Azure per la prima volta, dovranno registrare il provider di Backup di Azure da usare con la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f66da-126">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="f66da-127">A tale scopo, eseguire il comando seguente: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="f66da-127">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="f66da-128">È possibile creare un nuovo insieme di credenziali per il backup usando il cmdlet **New-AzureRmBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="f66da-128">You can create a new backup vault using the **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="f66da-129">L’archivio di backup è una risorsa ARM, pertanto è necessario inserirlo all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f66da-129">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="f66da-130">Eseguire i comandi seguenti in una console di Azure PowerShell con privilegi elevati:</span><span class="sxs-lookup"><span data-stu-id="f66da-130">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="f66da-131">Usare il cmdlet **Get-AzureRMBackupVault** per elencare gli insiemi di credenziali di backup in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f66da-131">Use the **Get-AzureRMBackupVault** cmdlet to list the backup vaults in a subscription.</span></span>

## <a name="installing-the-azure-backup-agent"></a><span data-ttu-id="f66da-132">Installazione dell'agente di Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="f66da-132">Installing the Azure Backup agent</span></span>
<span data-ttu-id="f66da-133">Per installare l'agente di Backup di Azure, è necessario aver scaricato il programma di installazione nel server Windows.</span><span class="sxs-lookup"><span data-stu-id="f66da-133">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="f66da-134">È possibile ottenere la versione più recente del programma di installazione dall' [Area download Microsoft](http://aka.ms/azurebackup_agent) .o dalla pagina Dashboard dell’archivio di backup.</span><span class="sxs-lookup"><span data-stu-id="f66da-134">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="f66da-135">Salvare il programma di installazione in un percorso facilmente accessibile come *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="f66da-135">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="f66da-136">Per installare l'agente, eseguire il comando seguente in una console di Azure PowerShell con privilegi elevati:</span><span class="sxs-lookup"><span data-stu-id="f66da-136">To install the agent, run the following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="f66da-137">L'agente verrà installato con tutte le opzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="f66da-137">This installs the agent with all the default options.</span></span> <span data-ttu-id="f66da-138">L'installazione richiede alcuni minuti in background.</span><span class="sxs-lookup"><span data-stu-id="f66da-138">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="f66da-139">Se non si specifica l'opzione */nu* , la finestra **Windows Update** si aprirà al termine dell'installazione per verificare la presenza di eventuali aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="f66da-139">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span></span> <span data-ttu-id="f66da-140">Dopo essere stato installato, l'agente verrà visualizzato nell'elenco dei programmi installati.</span><span class="sxs-lookup"><span data-stu-id="f66da-140">Once installed, the agent will show in the list of installed programs.</span></span>

<span data-ttu-id="f66da-141">Per visualizzare l'elenco dei programmi installati, passare a **Pannello di controllo** > **Programmi** > **Programmi e funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="f66da-141">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente installato](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="f66da-143">Opzioni di installazione</span><span class="sxs-lookup"><span data-stu-id="f66da-143">Installation options</span></span>
<span data-ttu-id="f66da-144">Per visualizzare tutte le opzioni disponibili tramite la riga di comando, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f66da-144">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="f66da-145">Le opzioni disponibili includono:</span><span class="sxs-lookup"><span data-stu-id="f66da-145">The available options include:</span></span>

| <span data-ttu-id="f66da-146">Opzione</span><span class="sxs-lookup"><span data-stu-id="f66da-146">Option</span></span> | <span data-ttu-id="f66da-147">Dettagli</span><span class="sxs-lookup"><span data-stu-id="f66da-147">Details</span></span> | <span data-ttu-id="f66da-148">Default</span><span class="sxs-lookup"><span data-stu-id="f66da-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f66da-149">/q</span><span class="sxs-lookup"><span data-stu-id="f66da-149">/q</span></span> |<span data-ttu-id="f66da-150">Installazione non interattiva</span><span class="sxs-lookup"><span data-stu-id="f66da-150">Quiet installation</span></span> |- |
| <span data-ttu-id="f66da-151">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="f66da-151">/p:"location"</span></span> |<span data-ttu-id="f66da-152">Percorso della cartella di installazione per l'agente di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="f66da-152">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="f66da-153">C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f66da-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="f66da-154">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="f66da-154">/s:"location"</span></span> |<span data-ttu-id="f66da-155">Percorso della cartella della cache per l'agente di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="f66da-155">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="f66da-156">C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure\Scratch</span><span class="sxs-lookup"><span data-stu-id="f66da-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="f66da-157">/m</span><span class="sxs-lookup"><span data-stu-id="f66da-157">/m</span></span> |<span data-ttu-id="f66da-158">Consenso esplicito a Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="f66da-158">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="f66da-159">/nu</span><span class="sxs-lookup"><span data-stu-id="f66da-159">/nu</span></span> |<span data-ttu-id="f66da-160">Al termine dell'installazione non vengono cercati gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="f66da-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="f66da-161">/d</span><span class="sxs-lookup"><span data-stu-id="f66da-161">/d</span></span> |<span data-ttu-id="f66da-162">Disinstalla l'agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f66da-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="f66da-163">/ph</span><span class="sxs-lookup"><span data-stu-id="f66da-163">/ph</span></span> |<span data-ttu-id="f66da-164">Indirizzo host proxy</span><span class="sxs-lookup"><span data-stu-id="f66da-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="f66da-165">/po</span><span class="sxs-lookup"><span data-stu-id="f66da-165">/po</span></span> |<span data-ttu-id="f66da-166">Numero porta host proxy</span><span class="sxs-lookup"><span data-stu-id="f66da-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="f66da-167">/pu</span><span class="sxs-lookup"><span data-stu-id="f66da-167">/pu</span></span> |<span data-ttu-id="f66da-168">Nome utente host proxy</span><span class="sxs-lookup"><span data-stu-id="f66da-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="f66da-169">/pw</span><span class="sxs-lookup"><span data-stu-id="f66da-169">/pw</span></span> |<span data-ttu-id="f66da-170">Password proxy</span><span class="sxs-lookup"><span data-stu-id="f66da-170">Proxy Password</span></span> |- |

## <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="f66da-171">Registrazione del servizio Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="f66da-171">Registering with the Azure Backup service</span></span>
<span data-ttu-id="f66da-172">Per poter eseguire la registrazione con il servizio Backup di Azure, è necessario assicurarsi che i [prerequisiti](backup-configure-vault.md) siano soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="f66da-172">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="f66da-173">È necessario:</span><span class="sxs-lookup"><span data-stu-id="f66da-173">You must:</span></span>

* <span data-ttu-id="f66da-174">Avere una sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="f66da-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="f66da-175">Ottieni un archivio di backup</span><span class="sxs-lookup"><span data-stu-id="f66da-175">Have a backup vault</span></span>

<span data-ttu-id="f66da-176">Per scaricare le credenziali dell'insieme di credenziali, eseguire il cmdlet **Get-AzureRMBackupVaultCredentials** nella console di Azure PowerShell e archiviarle in una posizione pratica, ad esempio *C:\Download\*.</span><span class="sxs-lookup"><span data-stu-id="f66da-176">To download the vault credentials, run the **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="f66da-177">La registrazione del computer con l'insieme di credenziali viene eseguita utilizzando il cmdlet [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) :</span><span class="sxs-lookup"><span data-stu-id="f66da-177">Registering the machine with the vault is done using the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration -VaultCredentials $cred -Confirm:$false

CertThumbprint      : 7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName : test-vault
Region              : West US

Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="f66da-178">Non utilizzare percorsi relativi per specificare il file dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f66da-178">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="f66da-179">È necessario fornire un percorso assoluto come input per il cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f66da-179">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="f66da-180">Impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="f66da-180">Networking settings</span></span>
<span data-ttu-id="f66da-181">Quando il computer Windows si connette a Internet mediante un server proxy, le impostazioni del proxy possono essere fornite anche all'agente.</span><span class="sxs-lookup"><span data-stu-id="f66da-181">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span></span> <span data-ttu-id="f66da-182">In questo esempio non è presente alcun server proxy, pertanto sono state eliminate tutte le informazioni relative al proxy.</span><span class="sxs-lookup"><span data-stu-id="f66da-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="f66da-183">È anche possibile controllare l'utilizzo della larghezza di banda con le opzioni ```work hour bandwidth``` e ```non-work hour bandwidth``` per un dato set di giorni della settimana.</span><span class="sxs-lookup"><span data-stu-id="f66da-183">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span></span>

<span data-ttu-id="f66da-184">L'impostazione dei dettagli relativi a proxy e larghezza di banda viene eseguita mediante il cmdlet [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) :</span><span class="sxs-lookup"><span data-stu-id="f66da-184">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="f66da-185">Impostazioni crittografia</span><span class="sxs-lookup"><span data-stu-id="f66da-185">Encryption settings</span></span>
<span data-ttu-id="f66da-186">I dati di backup inviati a Backup di Azure vengono crittografati per proteggere la riservatezza dei dati.</span><span class="sxs-lookup"><span data-stu-id="f66da-186">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="f66da-187">La passphrase di crittografia è la "password" per decrittografare i dati in fase di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f66da-187">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="f66da-188">Dopo l'impostazione, conservare le informazioni sulla passphrase al sicuro.</span><span class="sxs-lookup"><span data-stu-id="f66da-188">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="f66da-189">Non sarà possibile ripristinare i dati da Azure senza la passphrase.</span><span class="sxs-lookup"><span data-stu-id="f66da-189">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="f66da-190">Eseguire il backup di file e cartelle</span><span class="sxs-lookup"><span data-stu-id="f66da-190">Back up files and folders</span></span>
<span data-ttu-id="f66da-191">Tutti i backup dei server e dei client Windows in Backup di Azure sono regolati da un criterio,</span><span class="sxs-lookup"><span data-stu-id="f66da-191">All your backups from Windows Servers and clients to Azure Backup are governed by a policy.</span></span> <span data-ttu-id="f66da-192">costituito da tre parti:</span><span class="sxs-lookup"><span data-stu-id="f66da-192">The policy comprises three parts:</span></span>

1. <span data-ttu-id="f66da-193">Una **pianificazione dei backup** che specifica quando è necessario eseguire i backup e sincronizzarli con il servizio.</span><span class="sxs-lookup"><span data-stu-id="f66da-193">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span></span>
2. <span data-ttu-id="f66da-194">Una **pianificazione di conservazione** che indica per quanto tempo è necessario conservare i punti di ripristino in Azure.</span><span class="sxs-lookup"><span data-stu-id="f66da-194">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>
3. <span data-ttu-id="f66da-195">Una **specifica di inclusione/esclusione di file** che determina i contenuti di cui eseguire il backup.</span><span class="sxs-lookup"><span data-stu-id="f66da-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="f66da-196">Dal momento che in questo documento si esegue un backup automatico, si presuppone che non siano stati configurati elementi.</span><span class="sxs-lookup"><span data-stu-id="f66da-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="f66da-197">Si inizia creando un nuovo criterio di backup tramite il cmdlet [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) e usando il criterio.</span><span class="sxs-lookup"><span data-stu-id="f66da-197">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="f66da-198">In questo momento il criterio è vuoto e sono necessari altri cmdlet per definire quali elementi verranno inclusi o esclusi, quando verranno eseguiti i backup e dove verranno archiviati.</span><span class="sxs-lookup"><span data-stu-id="f66da-198">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span></span>

### <a name="configuring-the-backup-schedule"></a><span data-ttu-id="f66da-199">Configurazione della pianificazione dei backup</span><span class="sxs-lookup"><span data-stu-id="f66da-199">Configuring the backup schedule</span></span>
<span data-ttu-id="f66da-200">La prima delle tre parti di un criterio è la pianificazione dei backup, che viene creata tramite il cmdlet [New-OBSchedule](https://technet.microsoft.com/library/hh770401) .</span><span class="sxs-lookup"><span data-stu-id="f66da-200">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="f66da-201">La pianificazione dei backup definisce quando è necessario eseguire i backup.</span><span class="sxs-lookup"><span data-stu-id="f66da-201">The backup schedule defines when backups need to be taken.</span></span> <span data-ttu-id="f66da-202">Quando si crea una pianificazione è necessario specificare due parametri di input:</span><span class="sxs-lookup"><span data-stu-id="f66da-202">When creating a schedule you need to specify 2 input parameters:</span></span>

* <span data-ttu-id="f66da-203">**Giorni della settimana** in cui deve essere eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="f66da-203">**Days of the week** that the backup should run.</span></span> <span data-ttu-id="f66da-204">È possibile eseguire il processo di backup in un solo giorno oppure tutti i giorni della settimana o specificando qualsiasi combinazione di giorni.</span><span class="sxs-lookup"><span data-stu-id="f66da-204">You can run the backup job on just one day, or every day of the week, or any combination in between.</span></span>
* <span data-ttu-id="f66da-205">**Orari della giornata** in cui deve essere eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="f66da-205">**Times of the day** when the backup should run.</span></span> <span data-ttu-id="f66da-206">È possibile definire fino a tre orari della giornata diversi in cui verrà attivato il backup.</span><span class="sxs-lookup"><span data-stu-id="f66da-206">You can define up to 3 different times of the day when the backup will be triggered.</span></span>

<span data-ttu-id="f66da-207">Ad esempio, è possibile configurare un criterio di backup eseguito alle 16.00 ogni sabato e domenica.</span><span class="sxs-lookup"><span data-stu-id="f66da-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="f66da-208">La pianificazione dei backup deve essere associata a un criterio ed è possibile eseguire questa operazione tramite il cmdlet [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) .</span><span class="sxs-lookup"><span data-stu-id="f66da-208">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="f66da-209">Configurazione di un criterio di conservazione</span><span class="sxs-lookup"><span data-stu-id="f66da-209">Configuring a retention policy</span></span>
<span data-ttu-id="f66da-210">Il criterio di conservazione definisce il periodo di conservazione dei punti di ripristino creati dai processi di backup.</span><span class="sxs-lookup"><span data-stu-id="f66da-210">The retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="f66da-211">Quando si crea un nuovo criterio di conservazione usando il cmdlet [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) , è possibile specificare il numero di giorni per cui conservare i punti di ripristino dei backup con Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="f66da-211">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span></span> <span data-ttu-id="f66da-212">L'esempio seguente imposta un criterio di conservazione di 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="f66da-212">The example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="f66da-213">Il criterio di conservazione deve essere associato al criterio principale usando il cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="f66da-213">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-to-be-backed-up"></a><span data-ttu-id="f66da-214">Inclusione ed esclusione di file per il backup</span><span class="sxs-lookup"><span data-stu-id="f66da-214">Including and excluding files to be backed up</span></span>
<span data-ttu-id="f66da-215">Un oggetto ```OBFileSpec``` definisce i file da includere o escludere in un backup.</span><span class="sxs-lookup"><span data-stu-id="f66da-215">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span></span> <span data-ttu-id="f66da-216">Si tratta di un set di regole che definiscono l'ambito di cartelle e file protetti in un computer.</span><span class="sxs-lookup"><span data-stu-id="f66da-216">This is a set of rules that scope out the protected files and folders on a machine.</span></span> <span data-ttu-id="f66da-217">È possibile disporre del numero desiderato di regole di inclusione o esclusione di file e associare le regole a un criterio.</span><span class="sxs-lookup"><span data-stu-id="f66da-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="f66da-218">Quando si crea un nuovo oggetto OBFileSpec, è possibile:</span><span class="sxs-lookup"><span data-stu-id="f66da-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="f66da-219">Specificare file e cartelle da includere</span><span class="sxs-lookup"><span data-stu-id="f66da-219">Specify the files and folders to be included</span></span>
* <span data-ttu-id="f66da-220">Specificare file e cartelle da escludere</span><span class="sxs-lookup"><span data-stu-id="f66da-220">Specify the files and folders to be excluded</span></span>
* <span data-ttu-id="f66da-221">Specificare un backup ricorsivo dei dati in una cartella (o) se eseguire il backup solo dei file di livello principale nella cartella specificata.</span><span class="sxs-lookup"><span data-stu-id="f66da-221">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span></span>

<span data-ttu-id="f66da-222">Quest'ultima impostazione si ottiene usando il flag -NonRecursive nel comando New-OBFileSpec.</span><span class="sxs-lookup"><span data-stu-id="f66da-222">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span></span>

<span data-ttu-id="f66da-223">Nell'esempio seguente viene eseguito il backup dei volumi C: e D: e vengono esclusi i file binari del sistema operativo nella cartella Windows e nelle cartelle temporanee.</span><span class="sxs-lookup"><span data-stu-id="f66da-223">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span></span> <span data-ttu-id="f66da-224">A tale scopo, vengono create due specifiche dei file usando il cmdlet [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) , una per l'inclusione e una per l'esclusione.</span><span class="sxs-lookup"><span data-stu-id="f66da-224">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="f66da-225">Dopo essere state create, le specifiche dei file vengono associate al criterio usando il cmdlet [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) .</span><span class="sxs-lookup"><span data-stu-id="f66da-225">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-the-policy"></a><span data-ttu-id="f66da-226">Applicazione del criterio</span><span class="sxs-lookup"><span data-stu-id="f66da-226">Applying the policy</span></span>
<span data-ttu-id="f66da-227">A questo punto l'oggetto criterio è completo e associato a una pianificazione dei backup, un criterio di conservazione e un elenco di inclusione o esclusione di file.</span><span class="sxs-lookup"><span data-stu-id="f66da-227">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="f66da-228">È ora possibile eseguire il commit del criterio affinché venga usato in Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="f66da-228">This policy can now be committed for Azure Backup to use.</span></span> <span data-ttu-id="f66da-229">Prima di applicare il criterio appena creato, assicurarsi che non vi siano criteri di backup esistenti associati al server usando il cmdlet [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) .</span><span class="sxs-lookup"><span data-stu-id="f66da-229">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="f66da-230">Per la rimozione del criterio verrà richiesta una conferma.</span><span class="sxs-lookup"><span data-stu-id="f66da-230">Removing the policy will prompt for confirmation.</span></span> <span data-ttu-id="f66da-231">Per ignorare la conferma, usare il flag ```-Confirm:$false``` con il cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f66da-231">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want to remove this backup policy? This will delete all the backed up data. [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="f66da-232">Il commit dell'oggetto criterio viene eseguito usando il cmdlet [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) .</span><span class="sxs-lookup"><span data-stu-id="f66da-232">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="f66da-233">Anche in questo caso verrà richiesto di confermare.</span><span class="sxs-lookup"><span data-stu-id="f66da-233">This will also ask for confirmation.</span></span> <span data-ttu-id="f66da-234">Per ignorare la conferma, usare il flag ```-Confirm:$false``` con il cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f66da-234">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want to save this backup policy ? [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

<span data-ttu-id="f66da-235">È possibile visualizzare i dettagli del criterio di backup esistente usando il cmdlet [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) .</span><span class="sxs-lookup"><span data-stu-id="f66da-235">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="f66da-236">È possibile eseguire ulteriormente il drill-down usando il cmdlet [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) per la pianificazione dei backup e il cmdlet[Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) per i criteri di conservazione</span><span class="sxs-lookup"><span data-stu-id="f66da-236">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span></span>

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="f66da-237">Esecuzione di un backup ad hoc</span><span class="sxs-lookup"><span data-stu-id="f66da-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="f66da-238">Una volta impostato un criterio di backup, i backup verranno eseguiti in base alla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="f66da-238">Once a backup policy has been set the backups will occur per the schedule.</span></span> <span data-ttu-id="f66da-239">È possibile attivare un backup ad hoc anche tramite il cmdlet [Start-OBBackup](https://technet.microsoft.com/library/hh770426) :</span><span class="sxs-lookup"><span data-stu-id="f66da-239">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
The backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="f66da-240">Ripristinare i dati da Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="f66da-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="f66da-241">Questa sezione illustra i passaggi per l'automazione del ripristino dei dati da Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="f66da-241">This section will guide you through the steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="f66da-242">A tale scopo, sono necessari i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f66da-242">Doing so involves the following steps:</span></span>

1. <span data-ttu-id="f66da-243">Selezionare il volume di origine</span><span class="sxs-lookup"><span data-stu-id="f66da-243">Pick the source volume</span></span>
2. <span data-ttu-id="f66da-244">Scegliere un punto di backup da ripristinare</span><span class="sxs-lookup"><span data-stu-id="f66da-244">Choose a backup point to restore</span></span>
3. <span data-ttu-id="f66da-245">Scegliere un elemento da ripristinare</span><span class="sxs-lookup"><span data-stu-id="f66da-245">Choose an item to restore</span></span>
4. <span data-ttu-id="f66da-246">Attivare il processo di ripristino</span><span class="sxs-lookup"><span data-stu-id="f66da-246">Trigger the restore process</span></span>

### <a name="picking-the-source-volume"></a><span data-ttu-id="f66da-247">Selezione del volume di origine</span><span class="sxs-lookup"><span data-stu-id="f66da-247">Picking the source volume</span></span>
<span data-ttu-id="f66da-248">Per ripristinare un elemento da Backup di Azure, è necessario innanzitutto identificare l'origine dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="f66da-248">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span></span> <span data-ttu-id="f66da-249">Poiché i comandi vengono eseguiti nel contesto di un server o un client Windows, il computer è già identificato.</span><span class="sxs-lookup"><span data-stu-id="f66da-249">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span></span> <span data-ttu-id="f66da-250">Il passaggio successivo nell'identificazione dell'origine consiste nell'identificare il volume che la contiene.</span><span class="sxs-lookup"><span data-stu-id="f66da-250">The next step in identifying the source is to identify the volume containing it.</span></span> <span data-ttu-id="f66da-251">È possibile recuperare un elenco dei volumi o delle origini di cui viene eseguito il backup per il computer eseguendo il cmdlet [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) .</span><span class="sxs-lookup"><span data-stu-id="f66da-251">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="f66da-252">Questo comando restituisce una matrice di tutte le origini di cui viene eseguito il backup nel server/client.</span><span class="sxs-lookup"><span data-stu-id="f66da-252">This command returns an array of all the sources backed up from this server/client.</span></span>

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-to-restore"></a><span data-ttu-id="f66da-253">Scelta di un punto di backup da ripristinare</span><span class="sxs-lookup"><span data-stu-id="f66da-253">Choosing a backup point to restore</span></span>
<span data-ttu-id="f66da-254">È possibile recuperare l'elenco dei punti di backup eseguendo il cmdlet [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) con i parametri appropriati.</span><span class="sxs-lookup"><span data-stu-id="f66da-254">The list of backup points can be retrieved by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="f66da-255">Nell'esempio viene scelto il punto di backup più recente per il volume di origine *D:* , che viene usato per ripristinare un file specifico.</span><span class="sxs-lookup"><span data-stu-id="f66da-255">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span></span>

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
<span data-ttu-id="f66da-256">L'oggetto ```$rps``` è una matrice di punti di backup.</span><span class="sxs-lookup"><span data-stu-id="f66da-256">The object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="f66da-257">Il primo elemento è il punto più recente e l'elemento N è il punto meno recente.</span><span class="sxs-lookup"><span data-stu-id="f66da-257">The first element is the latest point and the Nth element is the oldest point.</span></span> <span data-ttu-id="f66da-258">Per scegliere il punto più recente, si userà ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="f66da-258">To choose the latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-to-restore"></a><span data-ttu-id="f66da-259">Scelta di un elemento da ripristinare</span><span class="sxs-lookup"><span data-stu-id="f66da-259">Choosing an item to restore</span></span>
<span data-ttu-id="f66da-260">Per identificare la cartella o il file esatto da ripristinare, usare in modo ricorsivo il cmdlet [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f66da-260">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="f66da-261">In questo modo, è possibile esplorare la gerarchia di cartelle usando esclusivamente ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="f66da-261">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="f66da-262">In questo esempio, se si desidera ripristinare il file *finances.xls*, è possibile farvi riferimento usando l'oggetto ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="f66da-262">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span></span>

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

<span data-ttu-id="f66da-263">È anche possibile cercare gli elementi da ripristinare usando il cmdlet ```Get-OBRecoverableItem``` .</span><span class="sxs-lookup"><span data-stu-id="f66da-263">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="f66da-264">Nell'esempio, per cercare *finances.xls* è possibile ottenere un handle sul file eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f66da-264">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-the-restore-process"></a><span data-ttu-id="f66da-265">Attivazione del processo di ripristino</span><span class="sxs-lookup"><span data-stu-id="f66da-265">Triggering the restore process</span></span>
<span data-ttu-id="f66da-266">Per attivare il processo di ripristino, è prima necessario specificare le opzioni di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f66da-266">To trigger the restore process, we first need to specify the recovery options.</span></span> <span data-ttu-id="f66da-267">A tale scopo, è possibile usare il cmdlet [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f66da-267">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="f66da-268">Per questo esempio, si supponga di voler ripristinare i file in *C:\temp*.</span><span class="sxs-lookup"><span data-stu-id="f66da-268">For this example, let's assume that we want to restore the files to *C:\temp*.</span></span> <span data-ttu-id="f66da-269">Si supponga inoltre di voler ignorare i file già presenti nella cartella di destinazione *C:\temp*.</span><span class="sxs-lookup"><span data-stu-id="f66da-269">Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*.</span></span> <span data-ttu-id="f66da-270">Per creare un'opzione di ripristino di questo tipo, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f66da-270">To create such a recovery option, use the following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="f66da-271">Attivare quindi il ripristino usando il comando [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) sull'oggetto ```$item``` selezionato dall'output del cmdlet ```Get-OBRecoverableItem```:</span><span class="sxs-lookup"><span data-stu-id="f66da-271">Now trigger restore by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
The recovery operation completed successfully.
```


## <a name="uninstalling-the-azure-backup-agent"></a><span data-ttu-id="f66da-272">Disinstallazione dell'agente di Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="f66da-272">Uninstalling the Azure Backup agent</span></span>
<span data-ttu-id="f66da-273">La disinstallazione dell'agente di Backup di Azure può essere eseguita mediante il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="f66da-273">Uninstalling the Azure Backup agent can be done by using the following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="f66da-274">La disinstallazione dei file binari dell'agente dal computer comporta alcune conseguenze da tenere in considerazione:</span><span class="sxs-lookup"><span data-stu-id="f66da-274">Uninstalling the agent binaries from the machine has some consequences to consider:</span></span>

* <span data-ttu-id="f66da-275">Il filtro di file viene rimosso dal computer e il rilevamento delle modifiche viene arrestato.</span><span class="sxs-lookup"><span data-stu-id="f66da-275">It removes the file-filter from the machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="f66da-276">Tutte le informazioni sui criteri vengono rimosse dal computer, ma continuano a essere archiviate nel servizio.</span><span class="sxs-lookup"><span data-stu-id="f66da-276">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span></span>
* <span data-ttu-id="f66da-277">Tutte le pianificazioni dei backup vengono rimosse e non vengono eseguiti ulteriori backup.</span><span class="sxs-lookup"><span data-stu-id="f66da-277">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="f66da-278">Tuttavia, i dati archiviati in Azure continueranno a rimanere presenti e verranno conservati in base alla configurazione del criterio di conservazione specificata.</span><span class="sxs-lookup"><span data-stu-id="f66da-278">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span></span> <span data-ttu-id="f66da-279">I punti meno recenti scadono automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f66da-279">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="f66da-280">Gestione remota</span><span class="sxs-lookup"><span data-stu-id="f66da-280">Remote management</span></span>
<span data-ttu-id="f66da-281">Tutte le operazioni di gestione di origini dati, criteri e agente di Backup di Azure possono essere eseguite in remoto mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f66da-281">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="f66da-282">Il computer che verrà gestito in remoto deve essere preparato correttamente.</span><span class="sxs-lookup"><span data-stu-id="f66da-282">The machine that will be managed remotely needs to be prepared correctly.</span></span>

<span data-ttu-id="f66da-283">Per impostazione predefinita, il servizio Gestione remota Windows è configurato per l'avvio manuale.</span><span class="sxs-lookup"><span data-stu-id="f66da-283">By default, the WinRM service is configured for manual startup.</span></span> <span data-ttu-id="f66da-284">Il tipo di avvio deve essere impostato su *Automatico* e il servizio deve essere avviato.</span><span class="sxs-lookup"><span data-stu-id="f66da-284">The startup type must be set to *Automatic* and the service should be started.</span></span> <span data-ttu-id="f66da-285">Per verificare che il servizio Gestione remota Windows sia in esecuzione, il valore della proprietà Status deve essere *In esecuzione*.</span><span class="sxs-lookup"><span data-stu-id="f66da-285">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="f66da-286">PowerShell deve essere configurato per la comunicazione remota.</span><span class="sxs-lookup"><span data-stu-id="f66da-286">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up to receive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="f66da-287">È ora possibile gestire il computer in remoto, a partire dall'installazione dell'agente.</span><span class="sxs-lookup"><span data-stu-id="f66da-287">The machine can now be managed remotely - starting from the installation of the agent.</span></span> <span data-ttu-id="f66da-288">Ad esempio, il seguente script copia l'agente nel computer remoto e lo installa.</span><span class="sxs-lookup"><span data-stu-id="f66da-288">For example, the following script copies the agent to the remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="f66da-289">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f66da-289">Next steps</span></span>
<span data-ttu-id="f66da-290">Per altre informazioni su Backup di Azure per Windows Server/Client, vedere</span><span class="sxs-lookup"><span data-stu-id="f66da-290">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="f66da-291">Introduzione a Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="f66da-291">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="f66da-292">Backup di server Windows</span><span class="sxs-lookup"><span data-stu-id="f66da-292">Back up Windows Servers</span></span>](backup-configure-vault.md)
