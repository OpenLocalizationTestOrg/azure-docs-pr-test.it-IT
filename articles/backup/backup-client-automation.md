---
title: aaaUse tooback di PowerShell di Windows Server tooAzure | Documenti Microsoft
description: Informazioni su come toodeploy e gestire il Backup di Azure tramite PowerShell
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="5b5fd-103">Distribuire e gestire backup tooAzure per Windows Server e Windows Client tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b5fd-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b5fd-104">ARM</span><span class="sxs-lookup"><span data-stu-id="5b5fd-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="5b5fd-105">Classico</span><span class="sxs-lookup"><span data-stu-id="5b5fd-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="5b5fd-106">In questo articolo illustra come toouse PowerShell per la configurazione di Backup di Azure in Windows Server o un client Windows e la gestione di backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-106">This article shows you how toouse PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="5b5fd-107">Installare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b5fd-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="5b5fd-108">Questo articolo è incentrato su hello Azure Resource Manager (ARM) e hello MS Online Backup cmdlet che consentono di toouse un insieme di credenziali di servizi di ripristino in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-108">This article focuses on hello Azure Resource Manager (ARM) and hello MS Online Backup PowerShell cmdlets that enable you toouse a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="5b5fd-109">A ottobre 2015 è stato rilasciato Azure PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="5b5fd-110">Questa versione ha avuto esito positivo versione 0.9.8 hello e portato sulle modifiche significative, in particolare nel modello di denominazione dei cmdlet hello hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-110">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="5b5fd-111">eseguire i cmdlet 1.0 hello del modello di denominazione {verbo di}-AzureRm {nome}; mentre, non includono nomi hello 0.9.8 **Rm** (ad esempio, New-AzureRmResourceGroup anziché New AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="5b5fd-111">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="5b5fd-112">Quando si utilizza Azure PowerShell 0.9.8, è prima necessario attivare la modalità di gestione risorse hello eseguendo hello **Switch-AzureMode AzureResourceManager** comando.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-112">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="5b5fd-113">Questo comando non è necessario nella versione di 1.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="5b5fd-114">Se si desidera toouse gli script scritti per ambiente hello 0.9.8, nell'hello 1.0 o versione successiva, si deve aggiornare e testare attentamente script hello in un ambiente di pre-produzione prima di usarli in produzione tooavoid impatto imprevisto.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-114">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully update and test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="5b5fd-115">[Scaricare l'ultima versione di PowerShell hello](https://github.com/Azure/azure-powershell/releases) (versione minima richiesta è: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="5b5fd-115">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="5b5fd-116">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="5b5fd-116">Create a recovery services vault</span></span>
<span data-ttu-id="5b5fd-117">Hello alla procedura seguente per facilitare la creazione di un insieme di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-117">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="5b5fd-118">Un insieme di credenziali dei servizi di ripristino è diverso da un insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="5b5fd-119">Se si utilizza Azure Backup per hello prima volta, è necessario utilizzare hello **registro AzureRMResourceProvider** provider di servizi di ripristino di Azure di cmdlet tooregister hello con la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-119">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="5b5fd-120">Hello insieme di credenziali di servizi di ripristino è una risorsa ARM, pertanto è necessario tooplace all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-120">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="5b5fd-121">È possibile usare un gruppo di risorse esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="5b5fd-122">Quando si crea un nuovo gruppo di risorse, specificare il nome di hello e il percorso per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-122">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="5b5fd-123">Hello utilizzare **New AzureRmRecoveryServicesVault** cmdlet toocreate hello nuovo insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-123">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate hello new vault.</span></span> <span data-ttu-id="5b5fd-124">Assicurarsi che toospecify hello stesso percorso per l'insieme di credenziali hello utilizzata per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-124">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="5b5fd-125">Specificare il tipo di hello di toouse di ridondanza di archiviazione; è possibile utilizzare [archiviazione con ridondanza locale (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) o [archiviazione con ridondanza geografica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="5b5fd-125">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="5b5fd-126">Hello riportato di seguito hello - BackupStorageRedundancy per testVault impostazione tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-126">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="5b5fd-127">Molti cmdlet di Azure Backup richiede l'oggetto insieme di credenziali di servizi di ripristino hello come input.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-127">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="5b5fd-128">Per questo motivo, è utile toostore hello servizi di ripristino di Backup dell'insieme di credenziali oggetto in una variabile.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-128">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="5b5fd-129">Visualizza gli insiemi di credenziali hello in una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="5b5fd-129">View hello vaults in a subscription</span></span>
<span data-ttu-id="5b5fd-130">Utilizzare **Get AzureRmRecoveryServicesVault** elenco hello tooview di tutti gli insiemi di credenziali nella sottoscrizione corrente hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-130">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="5b5fd-131">È possibile utilizzare questo toocheck di comando che è stato creato un nuovo insieme di credenziali o toosee quali insiemi di credenziali sono disponibili nella sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-131">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="5b5fd-132">Eseguire il comando di hello, **Get AzureRmRecoveryServicesVault**, e sono elencati tutti gli insiemi di credenziali di sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-132">Run hello command, **Get-AzureRmRecoveryServicesVault**, and all vaults in hello subscription are listed.</span></span>

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


## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="5b5fd-133">Installare hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="5b5fd-133">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="5b5fd-134">Prima di installare l'agente Azure Backup hello, è necessario il programma di installazione di toohave hello scaricato e presenti sul Server di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-134">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="5b5fd-135">È possibile ottenere una versione più recente di hello del programma di installazione hello da hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) o dalla pagina Dashboard dell'insieme di credenziali hello servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-135">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="5b5fd-136">Salvare installer hello tooan posizione facilmente accessibile, ad esempio * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-136">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="5b5fd-137">In alternativa, usare il downloader di hello tooget di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-137">Alternatively, use PowerShell tooget hello downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="5b5fd-138">tooinstall hello esecuzione dell'agente, hello seguente comando in una console di PowerShell con privilegi elevata:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-138">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="5b5fd-139">Consente di installare agente hello con tutte le opzioni predefinite di hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-139">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="5b5fd-140">installazione di Hello richiede alcuni minuti in background hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-140">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="5b5fd-141">Se non si specifica hello */nu* opzione quindi hello **Windows Update** aprirà la finestra alla fine hello hello toocheck di installazione per tutti gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-141">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="5b5fd-142">Una volta installato, agente hello verrà visualizzati nell'elenco di hello dei programmi installati.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-142">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="5b5fd-143">elenco di hello toosee dei programmi installati, andare troppo**Pannello di controllo** > **programmi** > **programmi e funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-143">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente installato](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="5b5fd-145">Opzioni di installazione</span><span class="sxs-lookup"><span data-stu-id="5b5fd-145">Installation options</span></span>
<span data-ttu-id="5b5fd-146">toosee tutti hello opzioni disponibili tramite hello della riga di comando, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-146">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="5b5fd-147">Hello le opzioni disponibili includono:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-147">hello available options include:</span></span>

| <span data-ttu-id="5b5fd-148">Opzione</span><span class="sxs-lookup"><span data-stu-id="5b5fd-148">Option</span></span> | <span data-ttu-id="5b5fd-149">Dettagli</span><span class="sxs-lookup"><span data-stu-id="5b5fd-149">Details</span></span> | <span data-ttu-id="5b5fd-150">Default</span><span class="sxs-lookup"><span data-stu-id="5b5fd-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b5fd-151">/q</span><span class="sxs-lookup"><span data-stu-id="5b5fd-151">/q</span></span> |<span data-ttu-id="5b5fd-152">Installazione non interattiva</span><span class="sxs-lookup"><span data-stu-id="5b5fd-152">Quiet installation</span></span> |- |
| <span data-ttu-id="5b5fd-153">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="5b5fd-153">/p:"location"</span></span> |<span data-ttu-id="5b5fd-154">Cartella di installazione toohello percorso per l'agente Azure Backup hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-154">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="5b5fd-155">C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5b5fd-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="5b5fd-156">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="5b5fd-156">/s:"location"</span></span> |<span data-ttu-id="5b5fd-157">Cartella cache toohello percorso per l'agente Azure Backup hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-157">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="5b5fd-158">C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure\Scratch</span><span class="sxs-lookup"><span data-stu-id="5b5fd-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="5b5fd-159">/m</span><span class="sxs-lookup"><span data-stu-id="5b5fd-159">/m</span></span> |<span data-ttu-id="5b5fd-160">Consenso esplicito tooMicrosoft aggiornamento</span><span class="sxs-lookup"><span data-stu-id="5b5fd-160">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="5b5fd-161">/nu</span><span class="sxs-lookup"><span data-stu-id="5b5fd-161">/nu</span></span> |<span data-ttu-id="5b5fd-162">Al termine dell'installazione non vengono cercati gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="5b5fd-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="5b5fd-163">/d</span><span class="sxs-lookup"><span data-stu-id="5b5fd-163">/d</span></span> |<span data-ttu-id="5b5fd-164">Disinstalla l'agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5b5fd-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="5b5fd-165">/ph</span><span class="sxs-lookup"><span data-stu-id="5b5fd-165">/ph</span></span> |<span data-ttu-id="5b5fd-166">Indirizzo host proxy</span><span class="sxs-lookup"><span data-stu-id="5b5fd-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="5b5fd-167">/po</span><span class="sxs-lookup"><span data-stu-id="5b5fd-167">/po</span></span> |<span data-ttu-id="5b5fd-168">Numero porta host proxy</span><span class="sxs-lookup"><span data-stu-id="5b5fd-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="5b5fd-169">/pu</span><span class="sxs-lookup"><span data-stu-id="5b5fd-169">/pu</span></span> |<span data-ttu-id="5b5fd-170">Nome utente host proxy</span><span class="sxs-lookup"><span data-stu-id="5b5fd-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="5b5fd-171">/pw</span><span class="sxs-lookup"><span data-stu-id="5b5fd-171">/pw</span></span> |<span data-ttu-id="5b5fd-172">Password proxy</span><span class="sxs-lookup"><span data-stu-id="5b5fd-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a><span data-ttu-id="5b5fd-173">Registrazione di Windows Server o Windows client macchina tooa insieme di credenziali di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="5b5fd-173">Registering Windows Server or Windows client machine tooa Recovery Services Vault</span></span>
<span data-ttu-id="5b5fd-174">Dopo la creazione di credenziali di servizi di ripristino hello, scaricare l'ultima versione dell'agente hello e l'insieme di credenziali hello e archiviarlo in una posizione comoda come C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-174">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="5b5fd-175">Nel Server di Windows hello o computer client Windows, eseguire hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) macchina di hello tooregister cmdlet con insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-175">On hello Windows Server or Windows client machine, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>
<span data-ttu-id="5b5fd-176">Questo e altri cmdlet utilizzati per il backup, sono dal modulo MSONLINE hello quali hello Agent Installer Mars aggiunti come parte del processo di installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-176">This, and other cmdlets used for backup, are from hello MSONLINE module which hello Mars AgentInstaller added as part of hello installation process.</span></span> 

<span data-ttu-id="5b5fd-177">programma di installazione dell'agente Hello non aggiorna hello $Env: variabile PSModulePath.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-177">hello Agent installer does not update hello $Env:PSModulePath variable.</span></span> <span data-ttu-id="5b5fd-178">Il caricamento automatico del modulo avrà quindi esito negativo.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-178">This means module auto-load fails.</span></span> <span data-ttu-id="5b5fd-179">tooresolve questo è possibile eseguire il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-179">tooresolve this you can do hello following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="5b5fd-180">In alternativa, è possibile caricare manualmente il modulo hello nello script come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-180">Alternatively, you can manually load hello module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="5b5fd-181">Dopo aver caricato i cmdlet di Backup in linea hello, per registrare l'insieme di credenziali hello:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-181">Once you load hello Online Backup cmdlets, you register hello vault credentials:</span></span>


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="5b5fd-182">Non usare file delle credenziali dell'insieme di credenziali hello toospecify i percorsi relativi.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-182">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="5b5fd-183">È necessario fornire un percorso assoluto come un cmdlet toohello input.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-183">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="5b5fd-184">Impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="5b5fd-184">Networking settings</span></span>
<span data-ttu-id="5b5fd-185">Quando la connettività di hello di hello toohello che è internet tramite un server proxy del computer Windows, impostazioni del proxy hello è possibile specificare anche toohello agente.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-185">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="5b5fd-186">In questo esempio non è presente alcun server proxy, pertanto sono state eliminate tutte le informazioni relative al proxy.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="5b5fd-187">Utilizzo della larghezza di banda può essere controllata anche con le opzioni di hello di ```work hour bandwidth``` e ```non-work hour bandwidth``` per un set specificato di giorni della settimana hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-187">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="5b5fd-188">L'impostazione dei dettagli di proxy e la larghezza di banda hello viene eseguita utilizzando hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-188">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="5b5fd-189">Impostazioni crittografia</span><span class="sxs-lookup"><span data-stu-id="5b5fd-189">Encryption settings</span></span>
<span data-ttu-id="5b5fd-190">backup di dati inviati di Hello tooAzure Backup è tooprotect crittografato hello riservatezza dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-190">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="5b5fd-191">la passphrase di crittografia Hello è dati hello toodecrypt di password"hello" in fase di hello del ripristino.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-191">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="5b5fd-192">Mantenere informazioni passphrase hello sicuro e dopo che è stata impostata.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-192">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="5b5fd-193">Non è in grado di toorestore dati da Azure senza questa passphrase.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-193">You are not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="5b5fd-194">Eseguire il backup di file e cartelle</span><span class="sxs-lookup"><span data-stu-id="5b5fd-194">Back up files and folders</span></span>
<span data-ttu-id="5b5fd-195">Tutti i backup di Windows Server e client tooAzure Backup sono regolati da criteri.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-195">All backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="5b5fd-196">criteri di Hello è costituito da tre parti:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-196">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="5b5fd-197">Oggetto **pianificazione del backup** che specifica quando i backup necessitano toobe portato e sincronizzato con il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-197">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="5b5fd-198">Oggetto **pianificazione della conservazione** che specifica quanto tempo i punti di ripristino hello tooretain in Azure.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-198">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="5b5fd-199">Una **specifica di inclusione/esclusione di file** che determina i contenuti di cui eseguire il backup.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="5b5fd-200">Dal momento che in questo documento si esegue un backup automatico, si presuppone che non siano stati configurati elementi.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="5b5fd-201">Iniziare creando un nuovo criterio di backup utilizzando hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-201">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="5b5fd-202">In questo hello ora criteri sono vuoto e altri cmdlet sono necessari toodefine gli elementi che verranno inclusi o esclusi, quando i backup verranno eseguiti e hello in cui verranno archiviati i backup.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-202">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="5b5fd-203">La configurazione della pianificazione di backup hello</span><span class="sxs-lookup"><span data-stu-id="5b5fd-203">Configuring hello backup schedule</span></span>
<span data-ttu-id="5b5fd-204">Hello prima di hello 3 parti di un criterio è hello pianificazione dei backup, che viene creata utilizzando hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-204">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="5b5fd-205">pianificazione del backup Hello definisce quando i backup necessitano toobe eseguita.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-205">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="5b5fd-206">Quando si crea una pianificazione è necessario toospecify 2 parametri di input:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-206">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="5b5fd-207">**Giorni della settimana hello** deve essere eseguito il backup di hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-207">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="5b5fd-208">È possibile eseguire processo di backup in un solo giorno, hello o ogni giorno della settimana hello o qualsiasi combinazione tra.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-208">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="5b5fd-209">**Ore del giorno hello** quando eseguire il backup di hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-209">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="5b5fd-210">È possibile definire le ore del giorno di hello quando verrà attivato backup hello too3.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-210">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="5b5fd-211">Ad esempio, è possibile configurare un criterio di backup eseguito alle 16.00 ogni sabato e domenica.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="5b5fd-212">pianificazione del backup Hello deve toobe associati ai criteri e questo può essere ottenuto utilizzando hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-212">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="5b5fd-213">Configurazione di un criterio di conservazione</span><span class="sxs-lookup"><span data-stu-id="5b5fd-213">Configuring a retention policy</span></span>
<span data-ttu-id="5b5fd-214">criteri di conservazione Hello definiscono il tempo di ripristino punti creati dai processi di backup vengono mantenuti.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-214">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="5b5fd-215">Quando si crea un nuovo criterio di conservazione utilizzando hello [New OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, è possibile specificare il numero di hello di giorni per cui hello punti di ripristino di backup necessario toobe mantenuti con Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-215">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="5b5fd-216">esempio Hello seguente imposta i criteri di conservazione di 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-216">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="5b5fd-217">Hello criteri di conservazione devono essere associato a criteri di hello principale utilizzando cmdlet hello [Set OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="5b5fd-217">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="5b5fd-218">Inclusione ed esclusione di file toobe backup</span><span class="sxs-lookup"><span data-stu-id="5b5fd-218">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="5b5fd-219">Un ```OBFileSpec``` oggetto definisce hello file toobe inclusi ed esclusi in un backup.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-219">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="5b5fd-220">Si tratta di un set di regole di ambito out hello file e cartelle protetti in un computer.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-220">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="5b5fd-221">È possibile disporre del numero desiderato di regole di inclusione o esclusione di file e associare le regole a un criterio.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="5b5fd-222">Quando si crea un nuovo oggetto OBFileSpec, è possibile:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="5b5fd-223">Specificare hello toobe file e cartelle inclusi</span><span class="sxs-lookup"><span data-stu-id="5b5fd-223">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="5b5fd-224">Specificare hello toobe cartelle e file esclusi</span><span class="sxs-lookup"><span data-stu-id="5b5fd-224">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="5b5fd-225">Specificare ricorsiva di backup dei dati in una cartella (o) che devono essere eseguiti solo hello file di primo livello nella cartella specificata hello backup.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-225">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="5b5fd-226">Hello quest'ultimo viene ottenuta utilizzando il flag - non ricorsive di hello nel comando New-OBFileSpec hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-226">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="5b5fd-227">Nell'esempio hello riportato di seguito viene backup volume c: e d ed escludere i file binari del sistema operativo hello nella cartella di Windows hello e le cartelle temporanee.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-227">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="5b5fd-228">toodo verrà quindi creata utilizzando hello due specifiche di file [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - uno per l'inclusione e uno per l'esclusione.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-228">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="5b5fd-229">Dopo avere create le specifiche di file hello, ma sono associati con criteri di hello mediante hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-229">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-hello-policy"></a><span data-ttu-id="5b5fd-230">L'applicazione dei criteri di hello</span><span class="sxs-lookup"><span data-stu-id="5b5fd-230">Applying hello policy</span></span>
<span data-ttu-id="5b5fd-231">Ora l'oggetto Criteri di hello è stata completata e dispone di una pianificazione di backup associata, criteri di conservazione e un elenco di inclusione/esclusione dei file.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-231">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="5b5fd-232">Questo criterio può essere eseguito il commit per toouse Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-232">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="5b5fd-233">Prima di applicare hello appena creato criteri verificare che non sono presenti criteri di backup esistenti associati a server hello utilizzando hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-233">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="5b5fd-234">Rimozione dei criteri di hello verrà chiesta conferma.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-234">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="5b5fd-235">Conferma hello tooskip utilizzare hello ```-Confirm:$false``` flag con i cmdlet di hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-235">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="5b5fd-236">Viene eseguito il commit oggetto Criteri di hello utilizzando hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-236">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="5b5fd-237">Anche in questo caso verrà richiesto di confermare.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-237">This will also ask for confirmation.</span></span> <span data-ttu-id="5b5fd-238">Conferma hello tooskip utilizzare hello ```-Confirm:$false``` flag con i cmdlet di hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-238">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

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

<span data-ttu-id="5b5fd-239">È possibile visualizzare i dettagli di hello hello esistenti del criterio di backup utilizzando hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-239">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="5b5fd-240">È possibile drill-down usando hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet per la pianificazione del backup hello e hello [Get OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet per i criteri di conservazione hello</span><span class="sxs-lookup"><span data-stu-id="5b5fd-240">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="5b5fd-241">Esecuzione di un backup ad hoc</span><span class="sxs-lookup"><span data-stu-id="5b5fd-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="5b5fd-242">Dopo aver impostato un criterio di backup verrà eseguito alcun backup hello per ogni pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-242">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="5b5fd-243">Attivazione di un backup ad hoc è inoltre possibile utilizzare hello [inizio OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-243">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="5b5fd-244">Ripristinare i dati da Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="5b5fd-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="5b5fd-245">In questa sezione guiderà passaggi hello per automatizzare il ripristino dei dati da Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-245">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="5b5fd-246">Ciò comporta pertanto hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-246">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="5b5fd-247">Selezionare il volume di origine hello</span><span class="sxs-lookup"><span data-stu-id="5b5fd-247">Pick hello source volume</span></span>
2. <span data-ttu-id="5b5fd-248">Scegliere un backup toorestore punto</span><span class="sxs-lookup"><span data-stu-id="5b5fd-248">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="5b5fd-249">Scegliere un elemento di toorestore</span><span class="sxs-lookup"><span data-stu-id="5b5fd-249">Choose an item toorestore</span></span>
4. <span data-ttu-id="5b5fd-250">Processo di ripristino hello trigger</span><span class="sxs-lookup"><span data-stu-id="5b5fd-250">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="5b5fd-251">Volume di origine di prelievo hello</span><span class="sxs-lookup"><span data-stu-id="5b5fd-251">Picking hello source volume</span></span>
<span data-ttu-id="5b5fd-252">In ordine toorestore un elemento da Backup di Azure, è necessario innanzitutto origine hello tooidentify dell'elemento hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-252">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="5b5fd-253">Poiché l'esecuzione nel contesto di hello di un Server di Windows o un client Windows, i comandi di hello macchina hello è già identificato.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-253">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="5b5fd-254">passaggio successivo Hello identificazione origine hello è volume hello tooidentify che lo contiene.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-254">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="5b5fd-255">Un elenco di volumi o di origine viene eseguito il backup da questo computer può essere recuperato tramite l'esecuzione di hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-255">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="5b5fd-256">Questo comando restituisce una matrice di tutte le origini hello backup da questo server/client.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-256">This command returns an array of all hello sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-from-which-toorestore"></a><span data-ttu-id="5b5fd-257">Scelta di un punto di backup da cui toorestore</span><span class="sxs-lookup"><span data-stu-id="5b5fd-257">Choosing a backup point from which toorestore</span></span>
<span data-ttu-id="5b5fd-258">Per recuperare un elenco di punti di backup eseguendo hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet con i parametri appropriati.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-258">You retreive a list of backup points by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="5b5fd-259">In questo esempio, verrà scelto punto di backup più recente hello per volume di origine hello *unità d:* e usarlo toorecover un file specifico.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-259">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

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
<span data-ttu-id="5b5fd-260">oggetto Hello ```$rps``` è una matrice di punti di backup.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-260">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="5b5fd-261">primo elemento Hello è l'ultimo punto di hello ed ennesimo elemento hello è punto meno recente hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-261">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="5b5fd-262">ultimo punto hello toochoose, si utilizzerà ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-262">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="5b5fd-263">Scelta di un elemento di toorestore</span><span class="sxs-lookup"><span data-stu-id="5b5fd-263">Choosing an item toorestore</span></span>
<span data-ttu-id="5b5fd-264">tooidentify hello esatti del file o cartella toorestore, in modo ricorsivo utilizzare hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-264">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="5b5fd-265">Gerarchia di cartelle hello che modo può essere visualizzato utilizzando esclusivamente hello ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-265">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="5b5fd-266">In questo esempio, se lo si desidera file hello toorestore *finances.xls* si può fare riferimento che utilizzano oggetti hello ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-266">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="5b5fd-267">È inoltre possibile cercare elementi toorestore utilizzando hello ```Get-OBRecoverableItem``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-267">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="5b5fd-268">In questo esempio, toosearch per *finances.xls* è stato possibile ottenere un handle di file hello eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-268">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="5b5fd-269">Attivare il processo di ripristino hello</span><span class="sxs-lookup"><span data-stu-id="5b5fd-269">Triggering hello restore process</span></span>
<span data-ttu-id="5b5fd-270">processo di ripristino tootrigger hello, è necessario innanzitutto le opzioni di ripristino toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-270">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="5b5fd-271">Questa operazione può essere eseguita tramite hello [New OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-271">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="5b5fd-272">In questo esempio, si supponga ad esempio che si desidera file hello toorestore troppo*C:\temp*. Si supponga inoltre che si desidera tooskip i file già esistenti nella cartella di destinazione hello *C:\temp*. toocreate tali un'opzione di ripristino, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-272">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="5b5fd-273">Attivare ora il processo di ripristino hello utilizzando hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) comando hello selezionato ```$item``` dall'output di hello di hello ```Get-OBRecoverableItem``` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-273">Now trigger hello restore process by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="5b5fd-274">La disinstallazione dell'agente di Backup di Azure hello</span><span class="sxs-lookup"><span data-stu-id="5b5fd-274">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="5b5fd-275">La disinstallazione dell'agente di Backup di Azure hello può essere eseguita con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-275">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="5b5fd-276">La disinstallazione di binari agente hello dalla macchina di hello è tooconsider alcune conseguenze:</span><span class="sxs-lookup"><span data-stu-id="5b5fd-276">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="5b5fd-277">Filtro di file hello viene rimosso dal computer hello e viene arrestato il rilevamento delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-277">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="5b5fd-278">Tutte le informazioni dei criteri viene rimossa dalla macchina di hello, ma le informazioni sui criteri hello continua toobe archiviati nel servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-278">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="5b5fd-279">Tutte le pianificazioni dei backup vengono rimosse e non vengono eseguiti ulteriori backup.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="5b5fd-280">Tuttavia, hello dati archiviati in Azure rimane e viene mantenuto in base a impostazione dei criteri di conservazione hello da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-280">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="5b5fd-281">I punti meno recenti scadono automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="5b5fd-282">Gestione remota</span><span class="sxs-lookup"><span data-stu-id="5b5fd-282">Remote management</span></span>
<span data-ttu-id="5b5fd-283">Tutti i management hello intorno agente Azure Backup hello, i criteri e le origini dati può essere eseguito in remoto tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-283">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="5b5fd-284">macchina Hello che verrà gestito in modalità remota deve toobe preparato correttamente.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-284">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="5b5fd-285">Per impostazione predefinita, il servizio Gestione remota Windows hello è configurato per l'avvio manuale.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-285">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="5b5fd-286">è necessario impostare il tipo di avvio Hello troppo*automatica* e hello servizio deve essere avviato.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-286">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="5b5fd-287">tooverify che hello servizio Gestione remota Windows è in esecuzione, il valore di hello di hello proprietà Status deve essere *esecuzione*.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-287">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="5b5fd-288">PowerShell deve essere configurato per la comunicazione remota.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="5b5fd-289">macchina Hello può ora essere gestita in remoto, a partire dall'installazione hello dell'agente di hello.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-289">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="5b5fd-290">Ad esempio, hello lo script seguente computer remoto di hello agente toohello copia e lo installa.</span><span class="sxs-lookup"><span data-stu-id="5b5fd-290">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="5b5fd-291">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5b5fd-291">Next steps</span></span>
<span data-ttu-id="5b5fd-292">Per altre informazioni su Backup di Azure per Windows Server/Client, vedere</span><span class="sxs-lookup"><span data-stu-id="5b5fd-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="5b5fd-293">Introduzione tooAzure Backup</span><span class="sxs-lookup"><span data-stu-id="5b5fd-293">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="5b5fd-294">Backup di server Windows</span><span class="sxs-lookup"><span data-stu-id="5b5fd-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
