---
title: backup di Windows Server toomanage PowerShell aaaUse in Azure | Documenti Microsoft
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
ms.openlocfilehash: 72292e510b0f059102440bd49a195be4ef700a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="dc203-103">Distribuire e gestire backup tooAzure per Windows Server e Windows Client tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc203-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dc203-104">ARM</span><span class="sxs-lookup"><span data-stu-id="dc203-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="dc203-105">Classico</span><span class="sxs-lookup"><span data-stu-id="dc203-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="dc203-106">Questo articolo viene illustrato come eseguire il backup dell'insieme di credenziali toouse PowerShell tooback tooa dati workstation di Windows o di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="dc203-106">This article explains how toouse PowerShell tooback up Windows Server or Windows workstation data tooa backup vault.</span></span> <span data-ttu-id="dc203-107">Microsoft consiglia l'uso di insiemi di credenziali dei Servizi di ripristino per tutte le nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="dc203-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="dc203-108">Se si è un nuovo utente Azure Backup e non è stato creato un insieme di credenziali di backup nella sottoscrizione, utilizzare articolo hello [distribuire e gestire Data Protection Manager dati tooAzure tramite PowerShell](backup-client-automation.md) in modo che i dati vengono memorizzati in un insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="dc203-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="dc203-109">È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery.</span><span class="sxs-lookup"><span data-stu-id="dc203-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="dc203-110">Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="dc203-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="dc203-111">Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.</span><span class="sxs-lookup"><span data-stu-id="dc203-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="dc203-112">Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup.</span><span class="sxs-lookup"><span data-stu-id="dc203-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="dc203-113">**Entro il 1° novembre 2017**:</span><span class="sxs-lookup"><span data-stu-id="dc203-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="dc203-114">Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.</span><span class="sxs-lookup"><span data-stu-id="dc203-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="dc203-115">Si sarà in grado di tooaccess ai dati di backup nel portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="dc203-116">Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="dc203-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="dc203-117">Installare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc203-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="dc203-118">A ottobre 2015 è stato rilasciato Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="dc203-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="dc203-119">Questa versione ha avuto esito positivo versione 0.9.8 hello e portato sulle modifiche significative, in particolare nel modello di denominazione dei cmdlet hello hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-119">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="dc203-120">eseguire i cmdlet 1.0 hello del modello di denominazione {verbo di}-AzureRm {nome}; mentre, non includono nomi hello 0.9.8 **Rm** (ad esempio, New-AzureRmResourceGroup anziché New AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="dc203-120">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="dc203-121">Quando si utilizza Azure PowerShell 0.9.8, è prima necessario attivare la modalità di gestione risorse hello eseguendo hello **Switch-AzureMode AzureResourceManager** comando.</span><span class="sxs-lookup"><span data-stu-id="dc203-121">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="dc203-122">Questo comando non è necessario nella versione di 1.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="dc203-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="dc203-123">Se si desidera toouse gli script scritti per ambiente hello 0.9.8, nell'hello 1.0 o versione successiva, occorre verificare attentamente gli script hello in un ambiente di pre-produzione prima di usarli in produzione tooavoid impatto imprevisto.</span><span class="sxs-lookup"><span data-stu-id="dc203-123">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="dc203-124">[Scaricare l'ultima versione di PowerShell hello](https://github.com/Azure/azure-powershell/releases) (versione minima richiesta è: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="dc203-124">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="dc203-125">Creare un insieme di credenziali per il backup</span><span class="sxs-lookup"><span data-stu-id="dc203-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="dc203-126">Per i clienti che usano Azure Backup per hello prima volta, è necessario tooregister hello Azure Backup provider toobe utilizzato con la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dc203-126">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="dc203-127">Questa operazione può essere eseguita tramite l'esecuzione di hello comando seguente: "Microsoft.Backup" Register AzureProvider - ProviderNamespace</span><span class="sxs-lookup"><span data-stu-id="dc203-127">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="dc203-128">È possibile creare un nuovo insieme di credenziali di backup utilizzando hello **New AzureRMBackupVault** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dc203-128">You can create a new backup vault using hello **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="dc203-129">insieme di credenziali backup Hello è una risorsa ARM, pertanto è necessario tooplace all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="dc203-129">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="dc203-130">In una console di Azure PowerShell con privilegi elevata, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="dc203-130">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="dc203-131">Hello utilizzare **Get AzureRMBackupVault** insiemi di credenziali di backup di hello toolist cmdlet in una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dc203-131">Use hello **Get-AzureRMBackupVault** cmdlet toolist hello backup vaults in a subscription.</span></span>

## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="dc203-132">Installare hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="dc203-132">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="dc203-133">Prima di installare l'agente Azure Backup hello, è necessario il programma di installazione di toohave hello scaricato e presenti sul Server di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-133">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="dc203-134">È possibile ottenere una versione più recente di hello del programma di installazione hello da hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) o dalla pagina Dashboard hello backup vault.</span><span class="sxs-lookup"><span data-stu-id="dc203-134">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="dc203-135">Salvare installer hello tooan posizione facilmente accessibile, ad esempio * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="dc203-135">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="dc203-136">tooinstall hello esecuzione dell'agente, hello seguente comando in una console di PowerShell con privilegi elevata:</span><span class="sxs-lookup"><span data-stu-id="dc203-136">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="dc203-137">Consente di installare agente hello con tutte le opzioni predefinite di hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-137">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="dc203-138">installazione di Hello richiede alcuni minuti in background hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-138">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="dc203-139">Se non si specifica hello */nu* opzione quindi hello **Windows Update** aprirà la finestra alla fine hello hello toocheck di installazione per tutti gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="dc203-139">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="dc203-140">Una volta installato, agente hello verrà visualizzati nell'elenco di hello dei programmi installati.</span><span class="sxs-lookup"><span data-stu-id="dc203-140">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="dc203-141">elenco di hello toosee dei programmi installati, andare troppo**Pannello di controllo** > **programmi** > **programmi e funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="dc203-141">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente installato](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="dc203-143">Opzioni di installazione</span><span class="sxs-lookup"><span data-stu-id="dc203-143">Installation options</span></span>
<span data-ttu-id="dc203-144">toosee tutti hello opzioni disponibili tramite hello della riga di comando, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dc203-144">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="dc203-145">Hello le opzioni disponibili includono:</span><span class="sxs-lookup"><span data-stu-id="dc203-145">hello available options include:</span></span>

| <span data-ttu-id="dc203-146">Opzione</span><span class="sxs-lookup"><span data-stu-id="dc203-146">Option</span></span> | <span data-ttu-id="dc203-147">Dettagli</span><span class="sxs-lookup"><span data-stu-id="dc203-147">Details</span></span> | <span data-ttu-id="dc203-148">Default</span><span class="sxs-lookup"><span data-stu-id="dc203-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc203-149">/q</span><span class="sxs-lookup"><span data-stu-id="dc203-149">/q</span></span> |<span data-ttu-id="dc203-150">Installazione non interattiva</span><span class="sxs-lookup"><span data-stu-id="dc203-150">Quiet installation</span></span> |- |
| <span data-ttu-id="dc203-151">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="dc203-151">/p:"location"</span></span> |<span data-ttu-id="dc203-152">Cartella di installazione toohello percorso per l'agente Azure Backup hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-152">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="dc203-153">C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="dc203-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="dc203-154">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="dc203-154">/s:"location"</span></span> |<span data-ttu-id="dc203-155">Cartella cache toohello percorso per l'agente Azure Backup hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-155">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="dc203-156">C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure\Scratch</span><span class="sxs-lookup"><span data-stu-id="dc203-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="dc203-157">/m</span><span class="sxs-lookup"><span data-stu-id="dc203-157">/m</span></span> |<span data-ttu-id="dc203-158">Consenso esplicito tooMicrosoft aggiornamento</span><span class="sxs-lookup"><span data-stu-id="dc203-158">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="dc203-159">/nu</span><span class="sxs-lookup"><span data-stu-id="dc203-159">/nu</span></span> |<span data-ttu-id="dc203-160">Al termine dell'installazione non vengono cercati gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="dc203-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="dc203-161">/d</span><span class="sxs-lookup"><span data-stu-id="dc203-161">/d</span></span> |<span data-ttu-id="dc203-162">Disinstalla l'agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="dc203-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="dc203-163">/ph</span><span class="sxs-lookup"><span data-stu-id="dc203-163">/ph</span></span> |<span data-ttu-id="dc203-164">Indirizzo host proxy</span><span class="sxs-lookup"><span data-stu-id="dc203-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="dc203-165">/po</span><span class="sxs-lookup"><span data-stu-id="dc203-165">/po</span></span> |<span data-ttu-id="dc203-166">Numero porta host proxy</span><span class="sxs-lookup"><span data-stu-id="dc203-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="dc203-167">/pu</span><span class="sxs-lookup"><span data-stu-id="dc203-167">/pu</span></span> |<span data-ttu-id="dc203-168">Nome utente host proxy</span><span class="sxs-lookup"><span data-stu-id="dc203-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="dc203-169">/pw</span><span class="sxs-lookup"><span data-stu-id="dc203-169">/pw</span></span> |<span data-ttu-id="dc203-170">Password proxy</span><span class="sxs-lookup"><span data-stu-id="dc203-170">Proxy Password</span></span> |- |

## <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="dc203-171">Registrazione con hello servizio Azure Backup</span><span class="sxs-lookup"><span data-stu-id="dc203-171">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="dc203-172">Prima di poter registrare con hello servizio Backup di Azure, è necessario tooensure tale hello [prerequisiti](backup-configure-vault.md) sono soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="dc203-172">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="dc203-173">È necessario:</span><span class="sxs-lookup"><span data-stu-id="dc203-173">You must:</span></span>

* <span data-ttu-id="dc203-174">Avere una sottoscrizione di Azure valida</span><span class="sxs-lookup"><span data-stu-id="dc203-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="dc203-175">Ottieni un archivio di backup</span><span class="sxs-lookup"><span data-stu-id="dc203-175">Have a backup vault</span></span>

<span data-ttu-id="dc203-176">toodownload hello insieme di credenziali, eseguire hello **Get AzureRMBackupVaultCredentials** cmdlet in una console PowerShell di Azure e l'archivio in una posizione comoda come * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="dc203-176">toodownload hello vault credentials, run hello **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="dc203-177">Registrazione macchina hello con insieme di credenziali hello avviene utilizzando hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dc203-177">Registering hello machine with hello vault is done using hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

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
> <span data-ttu-id="dc203-178">Non usare file delle credenziali dell'insieme di credenziali hello toospecify i percorsi relativi.</span><span class="sxs-lookup"><span data-stu-id="dc203-178">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="dc203-179">È necessario fornire un percorso assoluto come un cmdlet toohello input.</span><span class="sxs-lookup"><span data-stu-id="dc203-179">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="dc203-180">Impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="dc203-180">Networking settings</span></span>
<span data-ttu-id="dc203-181">Quando la connettività di hello di hello toohello che è internet tramite un server proxy del computer Windows, impostazioni del proxy hello è possibile specificare anche toohello agente.</span><span class="sxs-lookup"><span data-stu-id="dc203-181">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="dc203-182">In questo esempio non è presente alcun server proxy, pertanto sono state eliminate tutte le informazioni relative al proxy.</span><span class="sxs-lookup"><span data-stu-id="dc203-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="dc203-183">Utilizzo della larghezza di banda può essere controllata anche con le opzioni di hello di ```work hour bandwidth``` e ```non-work hour bandwidth``` per un set specificato di giorni della settimana hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-183">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="dc203-184">L'impostazione dei dettagli di proxy e la larghezza di banda hello viene eseguita utilizzando hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dc203-184">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="dc203-185">Impostazioni crittografia</span><span class="sxs-lookup"><span data-stu-id="dc203-185">Encryption settings</span></span>
<span data-ttu-id="dc203-186">backup di dati inviati di Hello tooAzure Backup è tooprotect crittografato hello riservatezza dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-186">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="dc203-187">la passphrase di crittografia Hello è dati hello toodecrypt di password"hello" in fase di hello del ripristino.</span><span class="sxs-lookup"><span data-stu-id="dc203-187">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="dc203-188">Mantenere informazioni passphrase hello sicuro e dopo che è stata impostata.</span><span class="sxs-lookup"><span data-stu-id="dc203-188">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="dc203-189">Non sarà in grado di toorestore dati da Azure senza questa passphrase.</span><span class="sxs-lookup"><span data-stu-id="dc203-189">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="dc203-190">Eseguire il backup di file e cartelle</span><span class="sxs-lookup"><span data-stu-id="dc203-190">Back up files and folders</span></span>
<span data-ttu-id="dc203-191">Tutti i backup di Windows Server e client tooAzure Backup sono regolati da criteri.</span><span class="sxs-lookup"><span data-stu-id="dc203-191">All your backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="dc203-192">criteri di Hello è costituito da tre parti:</span><span class="sxs-lookup"><span data-stu-id="dc203-192">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="dc203-193">Oggetto **pianificazione del backup** che specifica quando i backup necessitano toobe portato e sincronizzato con il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-193">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="dc203-194">Oggetto **pianificazione della conservazione** che specifica quanto tempo i punti di ripristino hello tooretain in Azure.</span><span class="sxs-lookup"><span data-stu-id="dc203-194">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="dc203-195">Una **specifica di inclusione/esclusione di file** che determina i contenuti di cui eseguire il backup.</span><span class="sxs-lookup"><span data-stu-id="dc203-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="dc203-196">Dal momento che in questo documento si esegue un backup automatico, si presuppone che non siano stati configurati elementi.</span><span class="sxs-lookup"><span data-stu-id="dc203-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="dc203-197">Iniziare creando un nuovo criterio di backup utilizzando hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet e l'uso.</span><span class="sxs-lookup"><span data-stu-id="dc203-197">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="dc203-198">In questo hello ora criteri sono vuoto e altri cmdlet sono necessari toodefine gli elementi che verranno inclusi o esclusi, quando i backup verranno eseguiti e hello in cui verranno archiviati i backup.</span><span class="sxs-lookup"><span data-stu-id="dc203-198">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="dc203-199">La configurazione della pianificazione di backup hello</span><span class="sxs-lookup"><span data-stu-id="dc203-199">Configuring hello backup schedule</span></span>
<span data-ttu-id="dc203-200">Hello prima di hello 3 parti di un criterio è hello pianificazione dei backup, che viene creata utilizzando hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dc203-200">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="dc203-201">pianificazione del backup Hello definisce quando i backup necessitano toobe eseguita.</span><span class="sxs-lookup"><span data-stu-id="dc203-201">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="dc203-202">Quando si crea una pianificazione è necessario toospecify 2 parametri di input:</span><span class="sxs-lookup"><span data-stu-id="dc203-202">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="dc203-203">**Giorni della settimana hello** deve essere eseguito il backup di hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-203">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="dc203-204">È possibile eseguire processo di backup in un solo giorno, hello o ogni giorno della settimana hello o qualsiasi combinazione tra.</span><span class="sxs-lookup"><span data-stu-id="dc203-204">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="dc203-205">**Ore del giorno hello** quando eseguire il backup di hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-205">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="dc203-206">È possibile definire le ore del giorno di hello quando verrà attivato backup hello too3.</span><span class="sxs-lookup"><span data-stu-id="dc203-206">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="dc203-207">Ad esempio, è possibile configurare un criterio di backup eseguito alle 16.00 ogni sabato e domenica.</span><span class="sxs-lookup"><span data-stu-id="dc203-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="dc203-208">pianificazione del backup Hello deve toobe associati ai criteri e questo può essere ottenuto utilizzando hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dc203-208">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="dc203-209">Configurazione di un criterio di conservazione</span><span class="sxs-lookup"><span data-stu-id="dc203-209">Configuring a retention policy</span></span>
<span data-ttu-id="dc203-210">criteri di conservazione Hello definiscono il tempo di ripristino punti creati dai processi di backup vengono mantenuti.</span><span class="sxs-lookup"><span data-stu-id="dc203-210">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="dc203-211">Quando si crea un nuovo criterio di conservazione utilizzando hello [New OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, è possibile specificare il numero di hello di giorni per cui hello punti di ripristino di backup necessario toobe mantenuti con Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="dc203-211">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="dc203-212">esempio Hello seguente imposta i criteri di conservazione di 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="dc203-212">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="dc203-213">Hello criteri di conservazione devono essere associato a criteri di hello principale utilizzando cmdlet hello [Set OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="dc203-213">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="dc203-214">Inclusione ed esclusione di file toobe backup</span><span class="sxs-lookup"><span data-stu-id="dc203-214">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="dc203-215">Un ```OBFileSpec``` oggetto definisce hello file toobe inclusi ed esclusi in un backup.</span><span class="sxs-lookup"><span data-stu-id="dc203-215">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="dc203-216">Si tratta di un set di regole di ambito out hello file e cartelle protetti in un computer.</span><span class="sxs-lookup"><span data-stu-id="dc203-216">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="dc203-217">È possibile disporre del numero desiderato di regole di inclusione o esclusione di file e associare le regole a un criterio.</span><span class="sxs-lookup"><span data-stu-id="dc203-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="dc203-218">Quando si crea un nuovo oggetto OBFileSpec, è possibile:</span><span class="sxs-lookup"><span data-stu-id="dc203-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="dc203-219">Specificare hello toobe file e cartelle inclusi</span><span class="sxs-lookup"><span data-stu-id="dc203-219">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="dc203-220">Specificare hello toobe cartelle e file esclusi</span><span class="sxs-lookup"><span data-stu-id="dc203-220">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="dc203-221">Specificare ricorsiva di backup dei dati in una cartella (o) che devono essere eseguiti solo hello file di primo livello nella cartella specificata hello backup.</span><span class="sxs-lookup"><span data-stu-id="dc203-221">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="dc203-222">Hello quest'ultimo viene ottenuta utilizzando il flag - non ricorsive di hello nel comando New-OBFileSpec hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-222">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="dc203-223">Nell'esempio hello riportato di seguito viene backup volume c: e d ed escludere i file binari del sistema operativo hello nella cartella di Windows hello e le cartelle temporanee.</span><span class="sxs-lookup"><span data-stu-id="dc203-223">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="dc203-224">toodo verrà quindi creata utilizzando hello due specifiche di file [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - uno per l'inclusione e uno per l'esclusione.</span><span class="sxs-lookup"><span data-stu-id="dc203-224">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="dc203-225">Dopo avere create le specifiche di file hello, ma sono associati con criteri di hello mediante hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dc203-225">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-hello-policy"></a><span data-ttu-id="dc203-226">L'applicazione dei criteri di hello</span><span class="sxs-lookup"><span data-stu-id="dc203-226">Applying hello policy</span></span>
<span data-ttu-id="dc203-227">Ora l'oggetto Criteri di hello è stata completata e dispone di una pianificazione di backup associata, criteri di conservazione e un elenco di inclusione/esclusione dei file.</span><span class="sxs-lookup"><span data-stu-id="dc203-227">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="dc203-228">Questo criterio può essere eseguito il commit per toouse Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="dc203-228">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="dc203-229">Prima di applicare hello appena creato criteri verificare che non sono presenti criteri di backup esistenti associati a server hello utilizzando hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dc203-229">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="dc203-230">Rimozione dei criteri di hello verrà chiesta conferma.</span><span class="sxs-lookup"><span data-stu-id="dc203-230">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="dc203-231">Conferma hello tooskip utilizzare hello ```-Confirm:$false``` flag con i cmdlet di hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-231">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="dc203-232">Viene eseguito il commit oggetto Criteri di hello utilizzando hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dc203-232">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="dc203-233">Anche in questo caso verrà richiesto di confermare.</span><span class="sxs-lookup"><span data-stu-id="dc203-233">This will also ask for confirmation.</span></span> <span data-ttu-id="dc203-234">Conferma hello tooskip utilizzare hello ```-Confirm:$false``` flag con i cmdlet di hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-234">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
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

<span data-ttu-id="dc203-235">È possibile visualizzare i dettagli di hello hello esistenti del criterio di backup utilizzando hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dc203-235">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="dc203-236">È possibile drill-down usando hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet per la pianificazione del backup hello e hello [Get OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet per i criteri di conservazione hello</span><span class="sxs-lookup"><span data-stu-id="dc203-236">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="dc203-237">Esecuzione di un backup ad hoc</span><span class="sxs-lookup"><span data-stu-id="dc203-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="dc203-238">Dopo aver impostato un criterio di backup verrà eseguito alcun backup hello per ogni pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-238">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="dc203-239">Attivazione di un backup ad hoc è inoltre possibile utilizzare hello [inizio OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dc203-239">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="dc203-240">Ripristinare i dati da Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="dc203-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="dc203-241">In questa sezione guiderà passaggi hello per automatizzare il ripristino dei dati da Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc203-241">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="dc203-242">Ciò comporta pertanto hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="dc203-242">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="dc203-243">Selezionare il volume di origine hello</span><span class="sxs-lookup"><span data-stu-id="dc203-243">Pick hello source volume</span></span>
2. <span data-ttu-id="dc203-244">Scegliere un backup toorestore punto</span><span class="sxs-lookup"><span data-stu-id="dc203-244">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="dc203-245">Scegliere un elemento di toorestore</span><span class="sxs-lookup"><span data-stu-id="dc203-245">Choose an item toorestore</span></span>
4. <span data-ttu-id="dc203-246">Processo di ripristino hello trigger</span><span class="sxs-lookup"><span data-stu-id="dc203-246">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="dc203-247">Volume di origine di prelievo hello</span><span class="sxs-lookup"><span data-stu-id="dc203-247">Picking hello source volume</span></span>
<span data-ttu-id="dc203-248">In ordine toorestore un elemento da Backup di Azure, è necessario innanzitutto origine hello tooidentify dell'elemento hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-248">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="dc203-249">Poiché l'esecuzione nel contesto di hello di un Server di Windows o un client Windows, i comandi di hello macchina hello è già identificato.</span><span class="sxs-lookup"><span data-stu-id="dc203-249">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="dc203-250">passaggio successivo Hello identificazione origine hello è volume hello tooidentify che lo contiene.</span><span class="sxs-lookup"><span data-stu-id="dc203-250">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="dc203-251">Un elenco di volumi o di origine viene eseguito il backup da questo computer può essere recuperato tramite l'esecuzione di hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dc203-251">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="dc203-252">Questo comando restituisce una matrice di tutte le origini hello backup da questo server/client.</span><span class="sxs-lookup"><span data-stu-id="dc203-252">This command returns an array of all hello sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-toorestore"></a><span data-ttu-id="dc203-253">Scelta di un backup toorestore punto</span><span class="sxs-lookup"><span data-stu-id="dc203-253">Choosing a backup point toorestore</span></span>
<span data-ttu-id="dc203-254">Hello elenco dei punti di backup può essere recuperato tramite l'esecuzione di hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet con i parametri appropriati.</span><span class="sxs-lookup"><span data-stu-id="dc203-254">hello list of backup points can be retrieved by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="dc203-255">In questo esempio, verrà scelto punto di backup più recente hello per volume di origine hello *unità d:* e usarlo toorecover un file specifico.</span><span class="sxs-lookup"><span data-stu-id="dc203-255">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

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
<span data-ttu-id="dc203-256">oggetto Hello ```$rps``` è una matrice di punti di backup.</span><span class="sxs-lookup"><span data-stu-id="dc203-256">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="dc203-257">primo elemento Hello è l'ultimo punto di hello ed ennesimo elemento hello è punto meno recente hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-257">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="dc203-258">ultimo punto hello toochoose, si utilizzerà ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="dc203-258">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="dc203-259">Scelta di un elemento di toorestore</span><span class="sxs-lookup"><span data-stu-id="dc203-259">Choosing an item toorestore</span></span>
<span data-ttu-id="dc203-260">tooidentify hello esatti del file o cartella toorestore, in modo ricorsivo utilizzare hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dc203-260">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="dc203-261">Gerarchia di cartelle hello che modo può essere visualizzato utilizzando esclusivamente hello ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="dc203-261">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="dc203-262">In questo esempio, se lo si desidera file hello toorestore *finances.xls* si può fare riferimento che utilizzano oggetti hello ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="dc203-262">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="dc203-263">È inoltre possibile cercare elementi toorestore utilizzando hello ```Get-OBRecoverableItem``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dc203-263">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="dc203-264">In questo esempio, toosearch per *finances.xls* è stato possibile ottenere un handle di file hello eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="dc203-264">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="dc203-265">Attivare il processo di ripristino hello</span><span class="sxs-lookup"><span data-stu-id="dc203-265">Triggering hello restore process</span></span>
<span data-ttu-id="dc203-266">processo di ripristino tootrigger hello, è necessario innanzitutto le opzioni di ripristino toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-266">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="dc203-267">Questa operazione può essere eseguita tramite hello [New OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dc203-267">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="dc203-268">In questo esempio, si supponga ad esempio che si desidera file hello toorestore troppo*C:\temp*. Si supponga inoltre che si desidera tooskip i file già esistenti nella cartella di destinazione hello *C:\temp*. toocreate tali un'opzione di ripristino, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dc203-268">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="dc203-269">Attivare questo punto di ripristino utilizzando hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) comando hello selezionato ```$item``` dall'output di hello di hello ```Get-OBRecoverableItem``` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="dc203-269">Now trigger restore by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="dc203-270">La disinstallazione dell'agente di Backup di Azure hello</span><span class="sxs-lookup"><span data-stu-id="dc203-270">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="dc203-271">La disinstallazione dell'agente di Backup di Azure hello può essere eseguita con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dc203-271">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="dc203-272">La disinstallazione di binari agente hello dalla macchina di hello è tooconsider alcune conseguenze:</span><span class="sxs-lookup"><span data-stu-id="dc203-272">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="dc203-273">Filtro di file hello viene rimosso dal computer hello e viene arrestato il rilevamento delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="dc203-273">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="dc203-274">Tutte le informazioni dei criteri viene rimossa dalla macchina di hello, ma le informazioni sui criteri hello continua toobe archiviati nel servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-274">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="dc203-275">Tutte le pianificazioni dei backup vengono rimosse e non vengono eseguiti ulteriori backup.</span><span class="sxs-lookup"><span data-stu-id="dc203-275">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="dc203-276">Tuttavia, hello dati archiviati in Azure rimane e viene mantenuto in base a impostazione dei criteri di conservazione hello da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="dc203-276">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="dc203-277">I punti meno recenti scadono automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dc203-277">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="dc203-278">Gestione remota</span><span class="sxs-lookup"><span data-stu-id="dc203-278">Remote management</span></span>
<span data-ttu-id="dc203-279">Tutti i management hello intorno agente Azure Backup hello, i criteri e le origini dati può essere eseguito in remoto tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc203-279">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="dc203-280">macchina Hello che verrà gestito in modalità remota deve toobe preparato correttamente.</span><span class="sxs-lookup"><span data-stu-id="dc203-280">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="dc203-281">Per impostazione predefinita, il servizio Gestione remota Windows hello è configurato per l'avvio manuale.</span><span class="sxs-lookup"><span data-stu-id="dc203-281">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="dc203-282">è necessario impostare il tipo di avvio Hello troppo*automatica* e hello servizio deve essere avviato.</span><span class="sxs-lookup"><span data-stu-id="dc203-282">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="dc203-283">tooverify che hello servizio Gestione remota Windows è in esecuzione, il valore di hello di hello proprietà Status deve essere *esecuzione*.</span><span class="sxs-lookup"><span data-stu-id="dc203-283">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="dc203-284">PowerShell deve essere configurato per la comunicazione remota.</span><span class="sxs-lookup"><span data-stu-id="dc203-284">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="dc203-285">macchina Hello può ora essere gestita in remoto, a partire dall'installazione hello dell'agente di hello.</span><span class="sxs-lookup"><span data-stu-id="dc203-285">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="dc203-286">Ad esempio, hello lo script seguente computer remoto di hello agente toohello copia e lo installa.</span><span class="sxs-lookup"><span data-stu-id="dc203-286">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="dc203-287">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc203-287">Next steps</span></span>
<span data-ttu-id="dc203-288">Per altre informazioni su Backup di Azure per Windows Server/Client, vedere</span><span class="sxs-lookup"><span data-stu-id="dc203-288">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="dc203-289">Introduzione tooAzure Backup</span><span class="sxs-lookup"><span data-stu-id="dc203-289">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="dc203-290">Backup di server Windows</span><span class="sxs-lookup"><span data-stu-id="dc203-290">Back up Windows Servers</span></span>](backup-configure-vault.md)
