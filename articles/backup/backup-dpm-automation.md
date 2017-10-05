---
title: Backup di Azure - Utilizzo di PowerShell per eseguire il backup dei carichi di lavoro DPM | Documentazione Microsoft
description: Informazioni su come distribuire e gestire Backup di Azure per Data Protection Manager (DPM) usando PowerShell
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
ms.openlocfilehash: 2e3b4a094511a59cfa02917efc2e3e053840af0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="ecc00-103">Distribuire e gestire il backup in Azure per server Data Protection Manager (DPM) mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecc00-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ecc00-104">ARM</span><span class="sxs-lookup"><span data-stu-id="ecc00-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="ecc00-105">Classico</span><span class="sxs-lookup"><span data-stu-id="ecc00-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="ecc00-106">Questo articolo illustra come usare PowerShell per configurare Backup di Azure in un server DPM, e per gestire le operazioni di backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="ecc00-106">This article shows you how to use PowerShell to setup Azure Backup on a DPM server, and to manage backup and recovery.</span></span>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="ecc00-107">Configurazione dell'ambiente di PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecc00-107">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="ecc00-108">Prima di poter usare PowerShell per gestire i backup da Data Protection Manager ad Azure, è necessario avere l'ambiente appropriato in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ecc00-108">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you need to have the right environment in PowerShell.</span></span> <span data-ttu-id="ecc00-109">All'inizio della sessione di PowerShell, assicurarsi di eseguire il comando seguente per importare i moduli appropriati e fare riferimento correttamente ai cmdlet DPM:</span><span class="sxs-lookup"><span data-stu-id="ecc00-109">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="ecc00-110">Installazione e registrazione</span><span class="sxs-lookup"><span data-stu-id="ecc00-110">Setup and Registration</span></span>
<span data-ttu-id="ecc00-111">Per iniziare:</span><span class="sxs-lookup"><span data-stu-id="ecc00-111">To begin:</span></span>

1. <span data-ttu-id="ecc00-112">[Scaricare la versione più recente di PowerShell](https://github.com/Azure/azure-powershell/releases) (versione minima richiesta: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="ecc00-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="ecc00-113">Per iniziare, abilitare i cmdlet del servizio Backup di Azure passando alla modalità *AzureResourceManager* usando il cmdlet **Switch-AzureMode** :</span><span class="sxs-lookup"><span data-stu-id="ecc00-113">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="ecc00-114">Le attività di installazione e registrazione seguenti possono essere automatizzate tramite PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ecc00-114">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="ecc00-115">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="ecc00-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="ecc00-116">Installazione dell'agente di Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="ecc00-116">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="ecc00-117">Registrazione del servizio Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="ecc00-117">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="ecc00-118">Impostazioni di rete</span><span class="sxs-lookup"><span data-stu-id="ecc00-118">Networking settings</span></span>
* <span data-ttu-id="ecc00-119">Impostazioni crittografia</span><span class="sxs-lookup"><span data-stu-id="ecc00-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="ecc00-120">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="ecc00-120">Create a recovery services vault</span></span>
<span data-ttu-id="ecc00-121">Nei passaggi seguenti viene descritto come creare un insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="ecc00-121">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="ecc00-122">Un insieme di credenziali dei servizi di ripristino è diverso da un insieme di credenziali di backup.</span><span class="sxs-lookup"><span data-stu-id="ecc00-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="ecc00-123">Se si sta usando Backup di Azure per la prima volta, è necessario usare il cmdlet **Register-AzureRMResourceProvider** per registrare il provider di Servizi di ripristino di Azure con la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ecc00-123">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="ecc00-124">L'insieme di credenziali dei servizi di ripristino è una risorsa ARM, pertanto è necessario inserirlo all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ecc00-124">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="ecc00-125">È possibile usare un gruppo di risorse esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="ecc00-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="ecc00-126">Quando si crea un nuovo gruppo di risorse, è necessario specificare il nome e percorso per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ecc00-126">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="ecc00-127">Usare il cmdlet **New-AzureRmRecoveryServicesVault** per creare un nuovo insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ecc00-127">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create a new vault.</span></span> <span data-ttu-id="ecc00-128">Assicurarsi di specificare per l'insieme di credenziali lo stesso percorso usato per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ecc00-128">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="ecc00-129">Specificare il tipo di ridondanza di archiviazione da usare, ad esempio [archiviazione con ridondanza locale (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) o [archiviazione con ridondanza geografica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="ecc00-129">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="ecc00-130">Nell'esempio seguente l'opzione BackupStorageRedundancy per testVault è impostata su GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="ecc00-130">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="ecc00-131">Molti cmdlet di Backup di Azure richiedono l'oggetto dell'insieme di credenziali dei servizi di ripristino come input.</span><span class="sxs-lookup"><span data-stu-id="ecc00-131">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="ecc00-132">Per questo motivo, è utile archiviare l'oggetto dell'insieme di credenziali dei servizi di ripristino di Backup in una variabile.</span><span class="sxs-lookup"><span data-stu-id="ecc00-132">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="ecc00-133">Visualizzare gli insiemi di credenziali in un abbonamento</span><span class="sxs-lookup"><span data-stu-id="ecc00-133">View the vaults in a subscription</span></span>
<span data-ttu-id="ecc00-134">Usare **Get-AzureRmRecoveryServicesVault** per visualizzare l'elenco di tutti gli insiemi di credenziali della sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="ecc00-134">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="ecc00-135">È possibile usare questo comando per verificare che sia stato creato un nuovo insieme di credenziali o per vedere quali insiemi di credenziali sono disponibili nell'abbonamento.</span><span class="sxs-lookup"><span data-stu-id="ecc00-135">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="ecc00-136">L'esecuzione del comando Get-AzureRmRecoveryServicesVault visualizza tutti gli insiemi di credenziali disponibili nell'abbonamento.</span><span class="sxs-lookup"><span data-stu-id="ecc00-136">Run the command, Get-AzureRmRecoveryServicesVault, and all vaults in the subscription are listed.</span></span>

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


## <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="ecc00-137">Installazione dell'agente di Backup di Azure in un server DPM</span><span class="sxs-lookup"><span data-stu-id="ecc00-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="ecc00-138">Per installare l'agente di Backup di Azure, è necessario aver scaricato il programma di installazione nel server Windows.</span><span class="sxs-lookup"><span data-stu-id="ecc00-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="ecc00-139">È possibile ottenere la versione più recente del programma di installazione dall' [Area download Microsoft](http://aka.ms/azurebackup_agent) o dalla pagina Dashboard dell'insieme di credenziali dei servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="ecc00-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="ecc00-140">Salvare il programma di installazione in un percorso facilmente accessibile come *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="ecc00-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="ecc00-141">Per installare l'agente, eseguire il comando seguente in una console di PowerShell con privilegi elevati **nel server DPM**:</span><span class="sxs-lookup"><span data-stu-id="ecc00-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="ecc00-142">L'agente verrà installato con tutte le opzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="ecc00-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="ecc00-143">L'installazione richiede alcuni minuti in background.</span><span class="sxs-lookup"><span data-stu-id="ecc00-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="ecc00-144">Se non si specifica l'opzione */nu* , al termine dell'installazione verrà aperta la finestra **Windows Update** per verificare la presenza di eventuali aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="ecc00-144">If you do not specify the */nu* option the **Windows Update** window opens at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="ecc00-145">L'agente verrà visualizzato nell'elenco dei programmi installati.</span><span class="sxs-lookup"><span data-stu-id="ecc00-145">The agent shows up in the list of installed programs.</span></span> <span data-ttu-id="ecc00-146">Per visualizzare l'elenco dei programmi installati, passare a **Pannello di controllo** > **Programmi** > **Programmi e funzionalità**.</span><span class="sxs-lookup"><span data-stu-id="ecc00-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente installato](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="ecc00-148">Opzioni di installazione</span><span class="sxs-lookup"><span data-stu-id="ecc00-148">Installation options</span></span>
<span data-ttu-id="ecc00-149">Per visualizzare tutte le opzioni disponibili tramite la riga di comando, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ecc00-149">To see all the options available via the commandline, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="ecc00-150">Le opzioni disponibili includono:</span><span class="sxs-lookup"><span data-stu-id="ecc00-150">The available options include:</span></span>

| <span data-ttu-id="ecc00-151">Opzione</span><span class="sxs-lookup"><span data-stu-id="ecc00-151">Option</span></span> | <span data-ttu-id="ecc00-152">Dettagli</span><span class="sxs-lookup"><span data-stu-id="ecc00-152">Details</span></span> | <span data-ttu-id="ecc00-153">Default</span><span class="sxs-lookup"><span data-stu-id="ecc00-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ecc00-154">/q</span><span class="sxs-lookup"><span data-stu-id="ecc00-154">/q</span></span> |<span data-ttu-id="ecc00-155">Installazione non interattiva</span><span class="sxs-lookup"><span data-stu-id="ecc00-155">Quiet installation</span></span> |- |
| <span data-ttu-id="ecc00-156">/p:"location"</span><span class="sxs-lookup"><span data-stu-id="ecc00-156">/p:"location"</span></span> |<span data-ttu-id="ecc00-157">Percorso della cartella di installazione per l'agente di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc00-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="ecc00-158">C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ecc00-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="ecc00-159">/s:"location"</span><span class="sxs-lookup"><span data-stu-id="ecc00-159">/s:"location"</span></span> |<span data-ttu-id="ecc00-160">Percorso della cartella della cache per l'agente di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc00-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="ecc00-161">C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure\Scratch</span><span class="sxs-lookup"><span data-stu-id="ecc00-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="ecc00-162">/m</span><span class="sxs-lookup"><span data-stu-id="ecc00-162">/m</span></span> |<span data-ttu-id="ecc00-163">Consenso esplicito a Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="ecc00-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="ecc00-164">/nu</span><span class="sxs-lookup"><span data-stu-id="ecc00-164">/nu</span></span> |<span data-ttu-id="ecc00-165">Al termine dell'installazione non vengono cercati gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="ecc00-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="ecc00-166">/d</span><span class="sxs-lookup"><span data-stu-id="ecc00-166">/d</span></span> |<span data-ttu-id="ecc00-167">Disinstalla l'agente di Servizi di ripristino di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ecc00-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="ecc00-168">/ph</span><span class="sxs-lookup"><span data-stu-id="ecc00-168">/ph</span></span> |<span data-ttu-id="ecc00-169">Indirizzo host proxy</span><span class="sxs-lookup"><span data-stu-id="ecc00-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="ecc00-170">/po</span><span class="sxs-lookup"><span data-stu-id="ecc00-170">/po</span></span> |<span data-ttu-id="ecc00-171">Numero porta host proxy</span><span class="sxs-lookup"><span data-stu-id="ecc00-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="ecc00-172">/pu</span><span class="sxs-lookup"><span data-stu-id="ecc00-172">/pu</span></span> |<span data-ttu-id="ecc00-173">Nome utente host proxy</span><span class="sxs-lookup"><span data-stu-id="ecc00-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="ecc00-174">/pw</span><span class="sxs-lookup"><span data-stu-id="ecc00-174">/pw</span></span> |<span data-ttu-id="ecc00-175">Password proxy</span><span class="sxs-lookup"><span data-stu-id="ecc00-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-to-a-recovery-services-vault"></a><span data-ttu-id="ecc00-176">Registrazione di Data Protection Manager (DPM) con l'insieme di credenziali dei servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="ecc00-176">Registering DPM to a Recovery Services Vault</span></span>
<span data-ttu-id="ecc00-177">Dopo aver creato l'insieme di credenziali dei servizi di ripristino, scaricare l'ultimo agente e le credenziali dell'insieme di credenziali e archiviarli in un percorso semplice da ricordare, ad esempio C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="ecc00-177">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="ecc00-178">Eseguire il cmdlet [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) nel server DPM per registrare il computer con l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="ecc00-178">On the DPM server, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="ecc00-179">Impostazioni di configurazione iniziali</span><span class="sxs-lookup"><span data-stu-id="ecc00-179">Initial configuration settings</span></span>
<span data-ttu-id="ecc00-180">Dopo la registrazione con l'insieme di credenziali dei servizi di ripristino, il server DPM verrà avviato con le impostazioni di sottoscrizione predefinite.</span><span class="sxs-lookup"><span data-stu-id="ecc00-180">Once the DPM Server is registered with the Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="ecc00-181">Tali impostazioni includono rete, crittografia e area di staging.</span><span class="sxs-lookup"><span data-stu-id="ecc00-181">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="ecc00-182">Per modificare le impostazioni di sottoscrizione, è prima necessario ottenere un handle sulle impostazioni (predefinite) esistenti usando il cmdlet [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) :</span><span class="sxs-lookup"><span data-stu-id="ecc00-182">To change subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="ecc00-183">Tutte le modifiche vengono apportate a questo oggetto locale PowerShell ```$setting``` e poi viene eseguito il commit dell'oggetto completo in DPM e in Backup di Azure eseguendo il salvataggio mediante il cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791).</span><span class="sxs-lookup"><span data-stu-id="ecc00-183">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="ecc00-184">È necessario usare il flag ```–Commit``` per garantire che le modifiche vengano mantenute.</span><span class="sxs-lookup"><span data-stu-id="ecc00-184">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="ecc00-185">Le impostazioni vengono applicate e usate da Backup di Azure solo dopo il commit.</span><span class="sxs-lookup"><span data-stu-id="ecc00-185">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="ecc00-186">Rete</span><span class="sxs-lookup"><span data-stu-id="ecc00-186">Networking</span></span>
<span data-ttu-id="ecc00-187">Se per la connettività del computer DPM al servizio Backup di Azure in Internet viene usato un server proxy, per consentire la corretta esecuzione dei backup è necessario specificare le impostazioni del server proxy.</span><span class="sxs-lookup"><span data-stu-id="ecc00-187">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="ecc00-188">A tale scopo, usare i parametri ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` e ```ProxyPassword``` con il cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791).</span><span class="sxs-lookup"><span data-stu-id="ecc00-188">This is done by using the ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="ecc00-189">In questo esempio non esiste alcun server proxy, pertanto sono state eliminate tutte le informazioni relative al proxy.</span><span class="sxs-lookup"><span data-stu-id="ecc00-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="ecc00-190">È anche possibile controllare l'utilizzo della larghezza di banda con le opzioni ```-WorkHourBandwidth``` e ```-NonWorkHourBandwidth``` per un determinato set di giorni della settimana.</span><span class="sxs-lookup"><span data-stu-id="ecc00-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="ecc00-191">In questo esempio non viene impostata alcuna limitazione.</span><span class="sxs-lookup"><span data-stu-id="ecc00-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-the-staging-area"></a><span data-ttu-id="ecc00-192">Configurazione dell'area di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="ecc00-192">Configuring the staging Area</span></span>
<span data-ttu-id="ecc00-193">L'agente del servizio Backup di Azure in esecuzione nel server DPM deve disporre di archiviazione temporanea per i dati ripristinati dal cloud (area di staging locale).</span><span class="sxs-lookup"><span data-stu-id="ecc00-193">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="ecc00-194">Configurare l'area di gestione temporanea usando il cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) e il parametro ```-StagingAreaPath```.</span><span class="sxs-lookup"><span data-stu-id="ecc00-194">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="ecc00-195">Nell'esempio precedente, l'area di gestione temporanea verrà impostata su *C:\StagingArea* nell'oggetto di PowerShell ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="ecc00-195">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="ecc00-196">Assicurarsi che la cartella specificata esista già, altrimenti il commit finale delle impostazioni di sottoscrizione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="ecc00-196">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="ecc00-197">Impostazioni crittografia</span><span class="sxs-lookup"><span data-stu-id="ecc00-197">Encryption settings</span></span>
<span data-ttu-id="ecc00-198">I dati di backup inviati a Backup di Azure vengono crittografati per proteggere la riservatezza dei dati.</span><span class="sxs-lookup"><span data-stu-id="ecc00-198">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="ecc00-199">La passphrase di crittografia è la "password" per decrittografare i dati in fase di ripristino.</span><span class="sxs-lookup"><span data-stu-id="ecc00-199">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="ecc00-200">È importante conservarla al sicuro e proteggerla dopo averla impostata.</span><span class="sxs-lookup"><span data-stu-id="ecc00-200">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="ecc00-201">Nel seguente esempio, il primo comando consente di convertire la passphrase della stringa ```passphrase123456789``` in una stringa sicura; inoltre, consente di assegnare la stringa sicura alla variabile denominata ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="ecc00-201">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="ecc00-202">Il secondo comando imposta la stringa sicura in ```$Passphrase``` come password per la crittografia dei backup.</span><span class="sxs-lookup"><span data-stu-id="ecc00-202">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="ecc00-203">Dopo l'impostazione, conservare le informazioni sulla passphrase al sicuro.</span><span class="sxs-lookup"><span data-stu-id="ecc00-203">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="ecc00-204">Non sarà possibile ripristinare i dati da Azure senza la passphrase.</span><span class="sxs-lookup"><span data-stu-id="ecc00-204">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="ecc00-205">A questo punto, sono state apportate tutte le modifiche necessarie all'oggetto ```$setting``` .</span><span class="sxs-lookup"><span data-stu-id="ecc00-205">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="ecc00-206">Ricordarsi di eseguire il commit delle modifiche:</span><span class="sxs-lookup"><span data-stu-id="ecc00-206">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="ecc00-207">Proteggere i dati in Backup di Azure</span><span class="sxs-lookup"><span data-stu-id="ecc00-207">Protect data to Azure Backup</span></span>
<span data-ttu-id="ecc00-208">In questa sezione verrà aggiunto un server di produzione a DPM e i dati verranno protetti nell'archivio DPM locale e quindi in Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc00-208">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="ecc00-209">Negli esempi verrà descritto come eseguire il backup di file e cartelle.</span><span class="sxs-lookup"><span data-stu-id="ecc00-209">In the examples, we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="ecc00-210">È possibile estendere in modo semplice la logica al fine di eseguire il backup di qualsiasi origine dati supportata da DPM.</span><span class="sxs-lookup"><span data-stu-id="ecc00-210">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="ecc00-211">Tutti i backup DPM sono regolati da un gruppo protezione dati costituito da quattro parti:</span><span class="sxs-lookup"><span data-stu-id="ecc00-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="ecc00-212">**Membri del gruppo** : elenco di tutti gli oggetti che è possibile proteggere (anche detti *origini dati* in DPM) e che si desidera proteggere nello stesso gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="ecc00-212">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="ecc00-213">Ad esempio, è possibile proteggere le macchine virtuali di produzione in un gruppo protezione dati e i database di SQL Server in un altro gruppo, in quanto potrebbero avere requisiti di backup diversi.</span><span class="sxs-lookup"><span data-stu-id="ecc00-213">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="ecc00-214">Prima di eseguire il backup di qualsiasi origine dati in un server di produzione, è necessario assicurarsi che l'agente DPM sia installato nel server e gestito da DPM.</span><span class="sxs-lookup"><span data-stu-id="ecc00-214">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="ecc00-215">Seguire la procedura di [installazione dell'agente DPM](https://technet.microsoft.com/library/bb870935.aspx) e collegamento dell'agente al server DPM appropriato.</span><span class="sxs-lookup"><span data-stu-id="ecc00-215">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="ecc00-216">**Metodo di protezione dati** : specifica le posizioni di destinazione dei backup, ad esempio nastro, disco e cloud.</span><span class="sxs-lookup"><span data-stu-id="ecc00-216">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="ecc00-217">In questo esempio i dati verranno protetti nel disco locale e nel cloud.</span><span class="sxs-lookup"><span data-stu-id="ecc00-217">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="ecc00-218">**Pianificazione dei backup** : specifica quando devono essere eseguiti i backup e con quale frequenza i dati devono essere sincronizzati tra il server DPM e il server di produzione.</span><span class="sxs-lookup"><span data-stu-id="ecc00-218">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="ecc00-219">Una **pianificazione di conservazione** che indica per quanto tempo è necessario conservare i punti di ripristino in Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc00-219">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="ecc00-220">Creazione di un gruppo di protezione</span><span class="sxs-lookup"><span data-stu-id="ecc00-220">Creating a protection group</span></span>
<span data-ttu-id="ecc00-221">Creare innanzitutto un nuovo gruppo protezione dati usando il cmdlet [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) .</span><span class="sxs-lookup"><span data-stu-id="ecc00-221">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="ecc00-222">Il cmdlet precedente creerà un gruppo protezione dati denominato *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="ecc00-222">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="ecc00-223">Un gruppo protezione dati esistente può anche essere modificato in seguito per aggiungere il backup nel cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="ecc00-223">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="ecc00-224">Tuttavia, per apportare modifiche al gruppo protezione dati, nuovo o esistente, è necessario ottenere un handle su un oggetto *modificabile* usando il cmdlet [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) .</span><span class="sxs-lookup"><span data-stu-id="ecc00-224">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="ecc00-225">Aggiunta di membri al gruppo protezione dati</span><span class="sxs-lookup"><span data-stu-id="ecc00-225">Adding group members to the Protection Group</span></span>
<span data-ttu-id="ecc00-226">Ogni agente DPM conosce l'elenco di origini dati nel server in cui è installato.</span><span class="sxs-lookup"><span data-stu-id="ecc00-226">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="ecc00-227">Per aggiungere un'origine dati al gruppo protezione dati, l'agente DPM deve innanzitutto inviare un elenco delle origini dati al server DPM.</span><span class="sxs-lookup"><span data-stu-id="ecc00-227">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="ecc00-228">Vengono quindi selezionate una o più origini dati, che vengono aggiunte al gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="ecc00-228">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="ecc00-229">La procedura di PowerShell da eseguire a questo scopo è la seguente:</span><span class="sxs-lookup"><span data-stu-id="ecc00-229">The PowerShell steps needed to achieve this are:</span></span>

1. <span data-ttu-id="ecc00-230">Recuperare un elenco di tutti i server gestiti da DPM tramite l'agente DPM.</span><span class="sxs-lookup"><span data-stu-id="ecc00-230">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="ecc00-231">Scegliere un server specifico.</span><span class="sxs-lookup"><span data-stu-id="ecc00-231">Choose a specific server.</span></span>
3. <span data-ttu-id="ecc00-232">Recuperare un elenco di tutte le origini dati nel server.</span><span class="sxs-lookup"><span data-stu-id="ecc00-232">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="ecc00-233">Scegliere una o più origini dati e aggiungerle al gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="ecc00-233">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="ecc00-234">È possibile acquisire l'elenco di tutti i server in cui è installato l'agente DPM e che sono gestiti dal server DPM tramite il cmdlet [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) .</span><span class="sxs-lookup"><span data-stu-id="ecc00-234">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="ecc00-235">In questo esempio verrà applicato un filtro e per il backup verrà configurato solo il server di produzione denominato *productionserver01* .</span><span class="sxs-lookup"><span data-stu-id="ecc00-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="ecc00-236">Recuperare quindi l'elenco di origini dati in ```$server``` usando il cmdlet [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605).</span><span class="sxs-lookup"><span data-stu-id="ecc00-236">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="ecc00-237">In questo esempio viene filtrato il volume *D:\*, da configurare per il backup.</span><span class="sxs-lookup"><span data-stu-id="ecc00-237">In this example we are filtering for the volume *D:\* that we want to configure for backup.</span></span> <span data-ttu-id="ecc00-238">L'origine dati viene quindi aggiunta al gruppo protezione dati usando il cmdlet [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732).</span><span class="sxs-lookup"><span data-stu-id="ecc00-238">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="ecc00-239">Ricordarsi di usare l'oggetto gruppo protezione dati *modificabile* ```$MPG``` per effettuare le aggiunte.</span><span class="sxs-lookup"><span data-stu-id="ecc00-239">Remember to use the *modifiable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="ecc00-240">Ripetere questo passaggio il numero di volte necessario per aggiungere tutte le origini dati scelte al gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="ecc00-240">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="ecc00-241">È anche possibile iniziare con una sola origine dati e completare il flusso di lavoro per la creazione del gruppo protezione dati, quindi, in un secondo momento, aggiungere altre origini dati al gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="ecc00-241">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="ecc00-242">Selezione del metodo di protezione dati</span><span class="sxs-lookup"><span data-stu-id="ecc00-242">Selecting the data protection method</span></span>
<span data-ttu-id="ecc00-243">Una volta aggiunte le origini dati al gruppo protezione dati, il passaggio successivo consiste nello specificare il metodo di protezione usando il cmdlet [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) .</span><span class="sxs-lookup"><span data-stu-id="ecc00-243">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="ecc00-244">In questo esempio, il gruppo protezione dati viene configurato per il backup su disco locale e nel cloud.</span><span class="sxs-lookup"><span data-stu-id="ecc00-244">In this example, the Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="ecc00-245">È inoltre necessario specificare l'origine dati che si desidera proteggere per il cloud utilizzando il cmdlet [Aggiungi DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) con -flag Online.</span><span class="sxs-lookup"><span data-stu-id="ecc00-245">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="ecc00-246">Impostazione del periodo di mantenimento dati</span><span class="sxs-lookup"><span data-stu-id="ecc00-246">Setting the retention range</span></span>
<span data-ttu-id="ecc00-247">Impostare il periodo di conservazione per i punti di backup usando il cmdlet [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="ecc00-247">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="ecc00-248">Anche se può sembrare strano impostare il periodo di conservazione prima di definire la pianificazione dei backup, usando il cmdlet ```Set-DPMPolicyObjective``` viene automaticamente impostata una pianificazione dei backup predefinita che può quindi essere modificata.</span><span class="sxs-lookup"><span data-stu-id="ecc00-248">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="ecc00-249">È sempre possibile impostare prima la pianificazione dei backup e successivamente i criteri di conservazione.</span><span class="sxs-lookup"><span data-stu-id="ecc00-249">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="ecc00-250">Nell'esempio seguente il cmdlet imposta i parametri di conservazione per i backup su disco.</span><span class="sxs-lookup"><span data-stu-id="ecc00-250">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="ecc00-251">I backup verranno conservati per 10 giorni e i dati verranno sincronizzati ogni 6 ore tra il server di produzione e il server DPM.</span><span class="sxs-lookup"><span data-stu-id="ecc00-251">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="ecc00-252">```SynchronizationFrequencyMinutes``` non definisce la frequenza di creazione di un punto di backup, ma la frequenza con cui i dati vengono copiati nel server DPM.</span><span class="sxs-lookup"><span data-stu-id="ecc00-252">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server.</span></span>  <span data-ttu-id="ecc00-253">Questa impostazione impedisce che i backup diventino di dimensioni eccessive.</span><span class="sxs-lookup"><span data-stu-id="ecc00-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="ecc00-254">Per i backup destinati ad Azure (indicati in DPM come backup online), è possibile configurare i periodi di mantenimento dati per la [conservazione a lungo termine con uno schema GFS (Grandfather-Father-Son)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="ecc00-254">For backups going to Azure (DPM refers to them as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="ecc00-255">Ciò significa che è possibile definire un criterio di conservazione combinato che includa criteri giornalieri, settimanali, mensili e annuali.</span><span class="sxs-lookup"><span data-stu-id="ecc00-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="ecc00-256">In questo esempio viene creata una matrice che rappresenta lo schema di conservazione complesso desiderato e quindi viene configurato il periodo di mantenimento dati usando il cmdlet [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="ecc00-256">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="ecc00-257">Impostare la pianificazione dei backup</span><span class="sxs-lookup"><span data-stu-id="ecc00-257">Set the backup schedule</span></span>
<span data-ttu-id="ecc00-258">Se si specifica l'obiettivo di protezione usando il cmdlet ```Set-DPMPolicyObjective``` , DPM imposta automaticamente una pianificazione dei backup predefinita.</span><span class="sxs-lookup"><span data-stu-id="ecc00-258">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="ecc00-259">Per modificare le pianificazioni predefinite, usare il cmdlet [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749), seguito da quello [Set DPMPolicySchedule](https://technet.microsoft.com/library/hh881723).</span><span class="sxs-lookup"><span data-stu-id="ecc00-259">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="ecc00-260">Nell'esempio precedente, ```$onlineSch``` è una matrice con quattro elementi che contiene la pianificazione della protezione online esistente per il gruppo protezione dati nello schema GFS:</span><span class="sxs-lookup"><span data-stu-id="ecc00-260">In the above example, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="ecc00-261">```$onlineSch[0]``` contiene la pianificazione giornaliera</span><span class="sxs-lookup"><span data-stu-id="ecc00-261">```$onlineSch[0]``` contains the daily schedule</span></span>
2. <span data-ttu-id="ecc00-262">```$onlineSch[1]``` contiene la pianificazione settimanale</span><span class="sxs-lookup"><span data-stu-id="ecc00-262">```$onlineSch[1]``` contains the weekly schedule</span></span>
3. <span data-ttu-id="ecc00-263">```$onlineSch[2]``` contiene la pianificazione mensile</span><span class="sxs-lookup"><span data-stu-id="ecc00-263">```$onlineSch[2]``` contains the monthly schedule</span></span>
4. <span data-ttu-id="ecc00-264">```$onlineSch[3]``` contiene la pianificazione annuale</span><span class="sxs-lookup"><span data-stu-id="ecc00-264">```$onlineSch[3]``` contains the yearly schedule</span></span>

<span data-ttu-id="ecc00-265">Se pertanto è necessario modificare la pianificazione settimanale, è necessario fare riferimento a ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="ecc00-265">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="ecc00-266">Backup iniziale</span><span class="sxs-lookup"><span data-stu-id="ecc00-266">Initial backup</span></span>
<span data-ttu-id="ecc00-267">Quando si esegue il backup di un'origine dati per la prima volta, DPM deve creare una replica iniziale con cui viene creata una copia completa dell'origine dati da proteggere nel volume di replica DPM.</span><span class="sxs-lookup"><span data-stu-id="ecc00-267">When backing up a datasource for the first time, DPM needs creates initial replica that creates a full copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="ecc00-268">È possibile pianificare questa attività a un orario specifico oppure attivarla manualmente, usando il cmdlet [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) con il parametro ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="ecc00-268">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="ecc00-269">Modifica delle dimensioni della replica DPM e volume del punto di ripristino</span><span class="sxs-lookup"><span data-stu-id="ecc00-269">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="ecc00-270">È anche possibile modificare le dimensioni del volume di replica DPM e del volume della copia shadow usando il cmdlet [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) come nell'esempio seguente: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span><span class="sxs-lookup"><span data-stu-id="ecc00-270">You can also change the size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="ecc00-271">Commit delle modifiche nel gruppo protezione dati</span><span class="sxs-lookup"><span data-stu-id="ecc00-271">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="ecc00-272">Infine, è necessario eseguire il commit delle modifiche affinché DPM possa eseguire il backup in base alla nuova configurazione del gruppo protezione dati.</span><span class="sxs-lookup"><span data-stu-id="ecc00-272">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="ecc00-273">A tale scopo, usare il cmdlet [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) .</span><span class="sxs-lookup"><span data-stu-id="ecc00-273">This can be achieved using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="ecc00-274">Visualizzare i punti di backup</span><span class="sxs-lookup"><span data-stu-id="ecc00-274">View the backup points</span></span>
<span data-ttu-id="ecc00-275">È possibile usare il cmdlet [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) per ottenere un elenco di tutti i punti di ripristino per un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="ecc00-275">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="ecc00-276">Nell'esempio seguente, vengono:</span><span class="sxs-lookup"><span data-stu-id="ecc00-276">In this example, we will:</span></span>

* <span data-ttu-id="ecc00-277">recuperati tutti i gruppi protezione dati (PG) nel server DPM con archiviazione in una matrice ```$PG```</span><span class="sxs-lookup"><span data-stu-id="ecc00-277">fetch all the PGs on the DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="ecc00-278">ottenuti le origini dati corrispondenti alla matrice ```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="ecc00-278">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="ecc00-279">ottenuti tutti i punti di ripristino per un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="ecc00-279">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="ecc00-280">Ripristino dei dati protetti su Azure</span><span class="sxs-lookup"><span data-stu-id="ecc00-280">Restore data protected on Azure</span></span>
<span data-ttu-id="ecc00-281">Il ripristino dei dati è una combinazione tra un oggetto ```RecoverableItem``` e un oggetto ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="ecc00-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="ecc00-282">Nella sezione precedente è stato ottenuto un elenco dei punti di backup per un'origine dati.</span><span class="sxs-lookup"><span data-stu-id="ecc00-282">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="ecc00-283">Nell'esempio seguente viene illustrato come ripristinare una macchina virtuale Hyper-V da Backup di Azure mediante la combinazione di punti di backup con la destinazione per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="ecc00-283">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="ecc00-284">L'esempio include quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ecc00-284">This example includes:</span></span>

* <span data-ttu-id="ecc00-285">Creazione di un'opzione di ripristino usando il cmdlet [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592).</span><span class="sxs-lookup"><span data-stu-id="ecc00-285">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="ecc00-286">Recupero della matrice di punti di backup usando il cmdlet ```Get-DPMRecoveryPoint``` .</span><span class="sxs-lookup"><span data-stu-id="ecc00-286">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="ecc00-287">Scelta di un punto di backup da cui eseguire il ripristino.</span><span class="sxs-lookup"><span data-stu-id="ecc00-287">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="ecc00-288">I comandi possono essere facilmente estesi per qualsiasi tipo di origine dati.</span><span class="sxs-lookup"><span data-stu-id="ecc00-288">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecc00-289">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ecc00-289">Next steps</span></span>
* <span data-ttu-id="ecc00-290">Per altre informazioni su DPM e Backup di Azure, vedere [Preparazione del backup dei carichi di lavoro in Azure con DPM](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="ecc00-290">For more information about DPM to Azure Backup see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
