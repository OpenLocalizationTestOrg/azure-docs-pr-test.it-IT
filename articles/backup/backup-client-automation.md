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
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a>Distribuire e gestire backup tooAzure per Windows Server e Windows Client tramite PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-client-automation.md)
> * [Classico](backup-client-automation-classic.md)
>
>

In questo articolo illustra come toouse PowerShell per la configurazione di Backup di Azure in Windows Server o un client Windows e la gestione di backup e ripristino.

## <a name="install-azure-powershell"></a>Installare Azure PowerShell
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Questo articolo è incentrato su hello Azure Resource Manager (ARM) e hello MS Online Backup cmdlet che consentono di toouse un insieme di credenziali di servizi di ripristino in un gruppo di risorse.

A ottobre 2015 è stato rilasciato Azure PowerShell 1.0. Questa versione ha avuto esito positivo versione 0.9.8 hello e portato sulle modifiche significative, in particolare nel modello di denominazione dei cmdlet hello hello. eseguire i cmdlet 1.0 hello del modello di denominazione {verbo di}-AzureRm {nome}; mentre, non includono nomi hello 0.9.8 **Rm** (ad esempio, New-AzureRmResourceGroup anziché New AzureResourceGroup). Quando si utilizza Azure PowerShell 0.9.8, è prima necessario attivare la modalità di gestione risorse hello eseguendo hello **Switch-AzureMode AzureResourceManager** comando. Questo comando non è necessario nella versione di 1.0 o successiva.

Se si desidera toouse gli script scritti per ambiente hello 0.9.8, nell'hello 1.0 o versione successiva, si deve aggiornare e testare attentamente script hello in un ambiente di pre-produzione prima di usarli in produzione tooavoid impatto imprevisto.

[Scaricare l'ultima versione di PowerShell hello](https://github.com/Azure/azure-powershell/releases) (versione minima richiesta è: 1.0.0)

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino
Hello alla procedura seguente per facilitare la creazione di un insieme di credenziali di servizi di ripristino. Un insieme di credenziali dei servizi di ripristino è diverso da un insieme di credenziali di backup.

1. Se si utilizza Azure Backup per hello prima volta, è necessario utilizzare hello **registro AzureRMResourceProvider** provider di servizi di ripristino di Azure di cmdlet tooregister hello con la sottoscrizione.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Hello insieme di credenziali di servizi di ripristino è una risorsa ARM, pertanto è necessario tooplace all'interno di un gruppo di risorse. È possibile usare un gruppo di risorse esistente o crearne uno nuovo. Quando si crea un nuovo gruppo di risorse, specificare il nome di hello e il percorso per il gruppo di risorse hello.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. Hello utilizzare **New AzureRmRecoveryServicesVault** cmdlet toocreate hello nuovo insieme di credenziali. Assicurarsi che toospecify hello stesso percorso per l'insieme di credenziali hello utilizzata per il gruppo di risorse hello.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. Specificare il tipo di hello di toouse di ridondanza di archiviazione; è possibile utilizzare [archiviazione con ridondanza locale (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) o [archiviazione con ridondanza geografica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage). Hello riportato di seguito hello - BackupStorageRedundancy per testVault impostazione tooGeoRedundant.

   > [!TIP]
   > Molti cmdlet di Azure Backup richiede l'oggetto insieme di credenziali di servizi di ripristino hello come input. Per questo motivo, è utile toostore hello servizi di ripristino di Backup dell'insieme di credenziali oggetto in una variabile.
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a>Visualizza gli insiemi di credenziali hello in una sottoscrizione
Utilizzare **Get AzureRmRecoveryServicesVault** elenco hello tooview di tutti gli insiemi di credenziali nella sottoscrizione corrente hello. È possibile utilizzare questo toocheck di comando che è stato creato un nuovo insieme di credenziali o toosee quali insiemi di credenziali sono disponibili nella sottoscrizione hello.

Eseguire il comando di hello, **Get AzureRmRecoveryServicesVault**, e sono elencati tutti gli insiemi di credenziali di sottoscrizione hello.

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


## <a name="installing-hello-azure-backup-agent"></a>Installare hello Azure Backup agent
Prima di installare l'agente Azure Backup hello, è necessario il programma di installazione di toohave hello scaricato e presenti sul Server di Windows hello. È possibile ottenere una versione più recente di hello del programma di installazione hello da hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) o dalla pagina Dashboard dell'insieme di credenziali hello servizi di ripristino. Salvare installer hello tooan posizione facilmente accessibile, ad esempio * C:\Downloads\*.

In alternativa, usare il downloader di hello tooget di PowerShell:
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

tooinstall hello esecuzione dell'agente, hello seguente comando in una console di PowerShell con privilegi elevata:

```
PS C:\> MARSAgentInstaller.exe /q
```

Consente di installare agente hello con tutte le opzioni predefinite di hello. installazione di Hello richiede alcuni minuti in background hello. Se non si specifica hello */nu* opzione quindi hello **Windows Update** aprirà la finestra alla fine hello hello toocheck di installazione per tutti gli aggiornamenti. Una volta installato, agente hello verrà visualizzati nell'elenco di hello dei programmi installati.

elenco di hello toosee dei programmi installati, andare troppo**Pannello di controllo** > **programmi** > **programmi e funzionalità**.

![Agente installato](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a>Opzioni di installazione
toosee tutti hello opzioni disponibili tramite hello della riga di comando, usare hello comando seguente:

```
PS C:\> MARSAgentInstaller.exe /?
```

Hello le opzioni disponibili includono:

| Opzione | Dettagli | Default |
| --- | --- | --- |
| /q |Installazione non interattiva |- |
| /p:"location" |Cartella di installazione toohello percorso per l'agente Azure Backup hello. |C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure |
| /s:"location" |Cartella cache toohello percorso per l'agente Azure Backup hello. |C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure\Scratch |
| /m |Consenso esplicito tooMicrosoft aggiornamento |- |
| /nu |Al termine dell'installazione non vengono cercati gli aggiornamenti |- |
| /d |Disinstalla l'agente di Servizi di ripristino di Microsoft Azure |- |
| /ph |Indirizzo host proxy |- |
| /po |Numero porta host proxy |- |
| /pu |Nome utente host proxy |- |
| /pw |Password proxy |- |

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a>Registrazione di Windows Server o Windows client macchina tooa insieme di credenziali di servizi di ripristino
Dopo la creazione di credenziali di servizi di ripristino hello, scaricare l'ultima versione dell'agente hello e l'insieme di credenziali hello e archiviarlo in una posizione comoda come C:\Downloads.

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

Nel Server di Windows hello o computer client Windows, eseguire hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) macchina di hello tooregister cmdlet con insieme di credenziali hello.
Questo e altri cmdlet utilizzati per il backup, sono dal modulo MSONLINE hello quali hello Agent Installer Mars aggiunti come parte del processo di installazione di hello. 

programma di installazione dell'agente Hello non aggiorna hello $Env: variabile PSModulePath. Il caricamento automatico del modulo avrà quindi esito negativo. tooresolve questo è possibile eseguire il seguente hello:

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

In alternativa, è possibile caricare manualmente il modulo hello nello script come indicato di seguito:

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

Dopo aver caricato i cmdlet di Backup in linea hello, per registrare l'insieme di credenziali hello:


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
> Non usare file delle credenziali dell'insieme di credenziali hello toospecify i percorsi relativi. È necessario fornire un percorso assoluto come un cmdlet toohello input.
>
>

## <a name="networking-settings"></a>Impostazioni di rete
Quando la connettività di hello di hello toohello che è internet tramite un server proxy del computer Windows, impostazioni del proxy hello è possibile specificare anche toohello agente. In questo esempio non è presente alcun server proxy, pertanto sono state eliminate tutte le informazioni relative al proxy.

Utilizzo della larghezza di banda può essere controllata anche con le opzioni di hello di ```work hour bandwidth``` e ```non-work hour bandwidth``` per un set specificato di giorni della settimana hello.

L'impostazione dei dettagli di proxy e la larghezza di banda hello viene eseguita utilizzando hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a>Impostazioni crittografia
backup di dati inviati di Hello tooAzure Backup è tooprotect crittografato hello riservatezza dei dati di hello. la passphrase di crittografia Hello è dati hello toodecrypt di password"hello" in fase di hello del ripristino.

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> Mantenere informazioni passphrase hello sicuro e dopo che è stata impostata. Non è in grado di toorestore dati da Azure senza questa passphrase.
>
>

## <a name="back-up-files-and-folders"></a>Eseguire il backup di file e cartelle
Tutti i backup di Windows Server e client tooAzure Backup sono regolati da criteri. criteri di Hello è costituito da tre parti:

1. Oggetto **pianificazione del backup** che specifica quando i backup necessitano toobe portato e sincronizzato con il servizio di hello.
2. Oggetto **pianificazione della conservazione** che specifica quanto tempo i punti di ripristino hello tooretain in Azure.
3. Una **specifica di inclusione/esclusione di file** che determina i contenuti di cui eseguire il backup.

Dal momento che in questo documento si esegue un backup automatico, si presuppone che non siano stati configurati elementi. Iniziare creando un nuovo criterio di backup utilizzando hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.

```
PS C:\> $newpolicy = New-OBPolicy
```

In questo hello ora criteri sono vuoto e altri cmdlet sono necessari toodefine gli elementi che verranno inclusi o esclusi, quando i backup verranno eseguiti e hello in cui verranno archiviati i backup.

### <a name="configuring-hello-backup-schedule"></a>La configurazione della pianificazione di backup hello
Hello prima di hello 3 parti di un criterio è hello pianificazione dei backup, che viene creata utilizzando hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet. pianificazione del backup Hello definisce quando i backup necessitano toobe eseguita. Quando si crea una pianificazione è necessario toospecify 2 parametri di input:

* **Giorni della settimana hello** deve essere eseguito il backup di hello. È possibile eseguire processo di backup in un solo giorno, hello o ogni giorno della settimana hello o qualsiasi combinazione tra.
* **Ore del giorno hello** quando eseguire il backup di hello. È possibile definire le ore del giorno di hello quando verrà attivato backup hello too3.

Ad esempio, è possibile configurare un criterio di backup eseguito alle 16.00 ogni sabato e domenica.

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

pianificazione del backup Hello deve toobe associati ai criteri e questo può essere ottenuto utilizzando hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a>Configurazione di un criterio di conservazione
criteri di conservazione Hello definiscono il tempo di ripristino punti creati dai processi di backup vengono mantenuti. Quando si crea un nuovo criterio di conservazione utilizzando hello [New OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, è possibile specificare il numero di hello di giorni per cui hello punti di ripristino di backup necessario toobe mantenuti con Azure Backup. esempio Hello seguente imposta i criteri di conservazione di 7 giorni.

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

Hello criteri di conservazione devono essere associato a criteri di hello principale utilizzando cmdlet hello [Set OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):

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
### <a name="including-and-excluding-files-toobe-backed-up"></a>Inclusione ed esclusione di file toobe backup
Un ```OBFileSpec``` oggetto definisce hello file toobe inclusi ed esclusi in un backup. Si tratta di un set di regole di ambito out hello file e cartelle protetti in un computer. È possibile disporre del numero desiderato di regole di inclusione o esclusione di file e associare le regole a un criterio. Quando si crea un nuovo oggetto OBFileSpec, è possibile:

* Specificare hello toobe file e cartelle inclusi
* Specificare hello toobe cartelle e file esclusi
* Specificare ricorsiva di backup dei dati in una cartella (o) che devono essere eseguiti solo hello file di primo livello nella cartella specificata hello backup.

Hello quest'ultimo viene ottenuta utilizzando il flag - non ricorsive di hello nel comando New-OBFileSpec hello.

Nell'esempio hello riportato di seguito viene backup volume c: e d ed escludere i file binari del sistema operativo hello nella cartella di Windows hello e le cartelle temporanee. toodo verrà quindi creata utilizzando hello due specifiche di file [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - uno per l'inclusione e uno per l'esclusione. Dopo avere create le specifiche di file hello, ma sono associati con criteri di hello mediante hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.

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

### <a name="applying-hello-policy"></a>L'applicazione dei criteri di hello
Ora l'oggetto Criteri di hello è stata completata e dispone di una pianificazione di backup associata, criteri di conservazione e un elenco di inclusione/esclusione dei file. Questo criterio può essere eseguito il commit per toouse Azure Backup. Prima di applicare hello appena creato criteri verificare che non sono presenti criteri di backup esistenti associati a server hello utilizzando hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet. Rimozione dei criteri di hello verrà chiesta conferma. Conferma hello tooskip utilizzare hello ```-Confirm:$false``` flag con i cmdlet di hello.

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

Viene eseguito il commit oggetto Criteri di hello utilizzando hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet. Anche in questo caso verrà richiesto di confermare. Conferma hello tooskip utilizzare hello ```-Confirm:$false``` flag con i cmdlet di hello.

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

È possibile visualizzare i dettagli di hello hello esistenti del criterio di backup utilizzando hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet. È possibile drill-down usando hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet per la pianificazione del backup hello e hello [Get OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet per i criteri di conservazione hello

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

### <a name="performing-an-ad-hoc-backup"></a>Esecuzione di un backup ad hoc
Dopo aver impostato un criterio di backup verrà eseguito alcun backup hello per ogni pianificazione hello. Attivazione di un backup ad hoc è inoltre possibile utilizzare hello [inizio OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:

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

## <a name="restore-data-from-azure-backup"></a>Ripristinare i dati da Backup di Azure
In questa sezione guiderà passaggi hello per automatizzare il ripristino dei dati da Backup di Azure. Ciò comporta pertanto hello alla procedura seguente:

1. Selezionare il volume di origine hello
2. Scegliere un backup toorestore punto
3. Scegliere un elemento di toorestore
4. Processo di ripristino hello trigger

### <a name="picking-hello-source-volume"></a>Volume di origine di prelievo hello
In ordine toorestore un elemento da Backup di Azure, è necessario innanzitutto origine hello tooidentify dell'elemento hello. Poiché l'esecuzione nel contesto di hello di un Server di Windows o un client Windows, i comandi di hello macchina hello è già identificato. passaggio successivo Hello identificazione origine hello è volume hello tooidentify che lo contiene. Un elenco di volumi o di origine viene eseguito il backup da questo computer può essere recuperato tramite l'esecuzione di hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet. Questo comando restituisce una matrice di tutte le origini hello backup da questo server/client.

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

### <a name="choosing-a-backup-point-from-which-toorestore"></a>Scelta di un punto di backup da cui toorestore
Per recuperare un elenco di punti di backup eseguendo hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet con i parametri appropriati. In questo esempio, verrà scelto punto di backup più recente hello per volume di origine hello *unità d:* e usarlo toorecover un file specifico.

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
oggetto Hello ```$rps``` è una matrice di punti di backup. primo elemento Hello è l'ultimo punto di hello ed ennesimo elemento hello è punto meno recente hello. ultimo punto hello toochoose, si utilizzerà ```$rps[0]```.

### <a name="choosing-an-item-toorestore"></a>Scelta di un elemento di toorestore
tooidentify hello esatti del file o cartella toorestore, in modo ricorsivo utilizzare hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet. Gerarchia di cartelle hello che modo può essere visualizzato utilizzando esclusivamente hello ```Get-OBRecoverableItem```.

In questo esempio, se lo si desidera file hello toorestore *finances.xls* si può fare riferimento che utilizzano oggetti hello ```$filesFolders[1]```.

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

È inoltre possibile cercare elementi toorestore utilizzando hello ```Get-OBRecoverableItem``` cmdlet. In questo esempio, toosearch per *finances.xls* è stato possibile ottenere un handle di file hello eseguendo questo comando:

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a>Attivare il processo di ripristino hello
processo di ripristino tootrigger hello, è necessario innanzitutto le opzioni di ripristino toospecify hello. Questa operazione può essere eseguita tramite hello [New OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet. In questo esempio, si supponga ad esempio che si desidera file hello toorestore troppo*C:\temp*. Si supponga inoltre che si desidera tooskip i file già esistenti nella cartella di destinazione hello *C:\temp*. toocreate tali un'opzione di ripristino, utilizzare hello comando seguente:

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

Attivare ora il processo di ripristino hello utilizzando hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) comando hello selezionato ```$item``` dall'output di hello di hello ```Get-OBRecoverableItem``` cmdlet:

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a>La disinstallazione dell'agente di Backup di Azure hello
La disinstallazione dell'agente di Backup di Azure hello può essere eseguita con hello comando seguente:

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

La disinstallazione di binari agente hello dalla macchina di hello è tooconsider alcune conseguenze:

* Filtro di file hello viene rimosso dal computer hello e viene arrestato il rilevamento delle modifiche.
* Tutte le informazioni dei criteri viene rimossa dalla macchina di hello, ma le informazioni sui criteri hello continua toobe archiviati nel servizio di hello.
* Tutte le pianificazioni dei backup vengono rimosse e non vengono eseguiti ulteriori backup.

Tuttavia, hello dati archiviati in Azure rimane e viene mantenuto in base a impostazione dei criteri di conservazione hello da parte dell'utente. I punti meno recenti scadono automaticamente.

## <a name="remote-management"></a>Gestione remota
Tutti i management hello intorno agente Azure Backup hello, i criteri e le origini dati può essere eseguito in remoto tramite PowerShell. macchina Hello che verrà gestito in modalità remota deve toobe preparato correttamente.

Per impostazione predefinita, il servizio Gestione remota Windows hello è configurato per l'avvio manuale. è necessario impostare il tipo di avvio Hello troppo*automatica* e hello servizio deve essere avviato. tooverify che hello servizio Gestione remota Windows è in esecuzione, il valore di hello di hello proprietà Status deve essere *esecuzione*.

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

PowerShell deve essere configurato per la comunicazione remota.

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

macchina Hello può ora essere gestita in remoto, a partire dall'installazione hello dell'agente di hello. Ad esempio, hello lo script seguente computer remoto di hello agente toohello copia e lo installa.

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni su Backup di Azure per Windows Server/Client, vedere

* [Introduzione tooAzure Backup](backup-introduction-to-azure-backup.md)
* [Backup di server Windows](backup-configure-vault.md)
