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
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a>Distribuire e gestire backup tooAzure per i server di Data Protection Manager (DPM) mediante PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-dpm-automation.md)
> * [Classico](backup-dpm-automation-classic.md)
>
>

In questo articolo illustra come toosetup PowerShell toouse Backup di Azure in un server DPM e toomanage backup e ripristino.

## <a name="setting-up-hello-powershell-environment"></a>Impostazione di ambiente PowerShell hello
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Prima di poter utilizzare PowerShell toomanage backup da Data Protection Manager tooAzure, è necessario toohave hello destra ambiente PowerShell. All'inizio di hello della sessione di PowerShell hello, assicurarsi di eseguire hello seguenti moduli destra di comando tooimport hello e consentono di determinare i cmdlet DPM toocorrectly riferimento hello:

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

## <a name="setup-and-registration"></a>Installazione e registrazione
toobegin:

1. [Scaricare la versione più recente di PowerShell](https://github.com/Azure/azure-powershell/releases) (versione minima richiesta: 1.0.0)
2. Abilitare i commandlet del Backup di Azure hello passando troppo*AzureResourceManager* modalità tramite hello **Switch-AzureMode** cmdlet:

```
PS C:\> Switch-AzureMode AzureResourceManager
```

Hello seguente programma di installazione e le attività di registrazione può essere automatizzata con PowerShell:

* Creare un insieme di credenziali di Servizi di ripristino
* Installare hello Azure Backup agent
* Registrazione con hello servizio Azure Backup
* Impostazioni di rete
* Impostazioni crittografia

## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino
Hello alla procedura seguente per facilitare la creazione di un insieme di credenziali di servizi di ripristino. Un insieme di credenziali dei servizi di ripristino è diverso da un insieme di credenziali di backup.

1. Se si utilizza Azure Backup per hello prima volta, è necessario utilizzare hello **registro AzureRMResourceProvider** provider di servizi di ripristino di Azure di cmdlet tooregister hello con la sottoscrizione.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Hello insieme di credenziali di servizi di ripristino è una risorsa ARM, pertanto è necessario tooplace all'interno di un gruppo di risorse. È possibile usare un gruppo di risorse esistente o crearne uno nuovo. Quando si crea un nuovo gruppo di risorse, specificare il nome di hello e il percorso per il gruppo di risorse hello.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. Hello utilizzare **New AzureRmRecoveryServicesVault** toocreate cmdlet un nuovo insieme di credenziali. Assicurarsi che toospecify hello stesso percorso per l'insieme di credenziali hello utilizzata per il gruppo di risorse hello.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
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

Comando hello, Get-AzureRmRecoveryServicesVault, e sono elencati tutti gli insiemi di credenziali di sottoscrizione hello.

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


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a>Installazione agente Azure Backup hello in un Server DPM
Prima di installare l'agente Azure Backup hello, è necessario il programma di installazione di toohave hello scaricato e presenti sul Server di Windows hello. È possibile ottenere una versione più recente di hello del programma di installazione hello da hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) o dalla pagina Dashboard dell'insieme di credenziali hello servizi di ripristino. Salvare installer hello tooan posizione facilmente accessibile, ad esempio * C:\Downloads\*.

esecuzione comando in una console di PowerShell con privilegi elevata seguente hello tooinstall agente hello **nel server DPM hello**:

```
PS C:\> MARSAgentInstaller.exe /q
```

Consente di installare agente hello con tutte le opzioni predefinite di hello. installazione di Hello richiede alcuni minuti in background hello. Se non si specifica hello */nu* hello opzione **Windows Update** verrà visualizzata la finestra alla fine hello hello toocheck di installazione per tutti gli aggiornamenti.

agente Hello viene visualizzato nell'elenco di hello dei programmi installati. elenco di hello toosee dei programmi installati, andare troppo**Pannello di controllo** > **programmi** > **programmi e funzionalità**.

![Agente installato](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a>Opzioni di installazione
toosee tutte le opzioni di hello disponibile tramite hello della riga di comando, utilizzare hello seguente comando:

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

## <a name="registering-dpm-tooa-recovery-services-vault"></a>Registrazione di Data Protection Manager tooa insieme di credenziali di servizi di ripristino
Dopo la creazione di credenziali di servizi di ripristino hello, scaricare l'ultima versione dell'agente hello e l'insieme di credenziali hello e archiviarlo in una posizione comoda come C:\Downloads.

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

Nel server DPM hello eseguire hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) macchina di hello tooregister cmdlet con insieme di credenziali hello.

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a>Impostazioni di configurazione iniziali
Una volta registrato con hello hello Server DPM l'insieme di credenziali di servizi di ripristino, viene avviato con le impostazioni di sottoscrizione predefinite. Queste impostazioni di sottoscrizione includono funzionalità di rete, la crittografia e hello area di gestione temporanea. le impostazioni di sottoscrizione toochange necessari toofirst ottenere un handle su hello (predefinito) le impostazioni esistenti utilizzando hello [Get DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

Tutte le modifiche vengono apportate toothis locale PowerShell oggetto ```$setting``` e quindi completa dell'oggetto hello è tooDPM eseguito il commit e Backup di Azure toosave loro utilizzando hello [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet. È necessario hello toouse ```–Commit``` tooensure di flag che hello le modifiche vengono mantenute. le impostazioni di Hello saranno non applicate e utilizzate dal Backup di Azure, a meno che il commit.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a>Rete
Se la connettività di hello di hello DPM macchina toohello servizio di Backup di Azure su hello internet è tramite un server proxy, impostazioni del server proxy hello devono essere fornite per i backup riusciti. Questa operazione viene eseguita tramite hello ```-ProxyServer```e ```-ProxyPort```, ```-ProxyUsername``` hello e ```ProxyPassword``` parametri con hello [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet. In questo esempio non esiste alcun server proxy, pertanto sono state eliminate tutte le informazioni relative al proxy.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

Utilizzo della larghezza di banda può essere controllata anche con le opzioni di ```-WorkHourBandwidth``` e ```-NonWorkHourBandwidth``` per un set specificato di giorni della settimana hello. In questo esempio non viene impostata alcuna limitazione.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a>Configurare l'Area di gestione temporanea hello
Hello Azure Backup agent in esecuzione nel server DPM hello deve archiviazione temporanea per i dati ripristinati dal cloud hello (area di gestione temporanea). Configurare l'area di gestione temporanea hello utilizzando hello [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet e hello ```-StagingAreaPath``` parametro.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

Nell'esempio hello sopra, hello area di gestione temporanea verrà impostata troppo*C:\StagingArea* nell'oggetto PowerShell hello ```$setting```. Verificare che hello specificato esiste già, altrimenti il commit finale hello delle impostazioni di sottoscrizione hello avrà esito negativo.

### <a name="encryption-settings"></a>Impostazioni crittografia
backup di dati inviati di Hello tooAzure Backup è tooprotect crittografato hello riservatezza dei dati di hello. la passphrase di crittografia Hello è dati hello toodecrypt di password"hello" in fase di hello del ripristino. È importante tookeep sicuro le informazioni e secure dopo che è stata impostata.

Nel seguente esempio hello primo comando hello Converte la stringa hello ```passphrase123456789``` tooa sicura stringa e assegna hello stringa sicura toohello variabile denominata ```$Passphrase```. Hello secondo comando imposta la stringa sicura hello in ```$Passphrase``` come password hello per la crittografia dei backup.

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> Mantenere informazioni passphrase hello sicuro e dopo che è stata impostata. Non sarà in grado di toorestore dati da Azure senza questa passphrase.
>
>

A questo punto, avrebbe dovuto effettuare tutti hello necessarie modifiche toohello ```$setting``` oggetto. Tenere presente che le modifiche di hello toocommit.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a>Proteggere dati tooAzure Backup
In questa sezione verrà aggiunta una tooDPM di server di produzione e quindi proteggere l'archiviazione di DPM toolocal dati hello e quindi tooAzure Backup. Negli esempi di hello, verrà illustrato come tooback backup di file e cartelle. Hello logica può facilmente essere estesa toobackup qualsiasi origine dati con supporto di DPM. Tutti i backup DPM sono regolati da un gruppo protezione dati costituito da quattro parti:

1. **I membri del gruppo** è un elenco di tutti gli oggetti da proteggere con hello (noto anche come *origini dati* in Data Protection Manager) che si desidera tooprotect in hello stesso gruppo protezione dati. Ad esempio, è consigliabile tooprotect produzione, le macchine virtuali in un gruppo protezione dati e i database di SQL Server in un altro gruppo protezione dati come presentare requisiti diversi per il backup. Prima di eseguire il backup di qualsiasi origine dati in un server di produzione è necessario toomake hello che agente Data Protection Manager è installato nel server di hello ed è gestito da DPM. Seguire i passaggi di hello per [installazione hello agente DPM](https://technet.microsoft.com/library/bb870935.aspx) e il relativo collegamento toohello appropriati Server DPM.
2. **Metodo protezione dati** specifica hello backup i percorsi di destinazione - nastro, disco e cloud. In questo esempio è proteggerà dati toohello locale su disco e toohello nel cloud.
3. Oggetto **pianificazione del backup** che specifica quando i backup necessitano toobe eseguito e la frequenza con cui hello di sincronizzazione dei dati tra hello Server DPM e il server di produzione hello.
4. Oggetto **pianificazione della conservazione** che specifica quanto tempo i punti di ripristino hello tooretain in Azure.

### <a name="creating-a-protection-group"></a>Creazione di un gruppo di protezione
Iniziare creando un nuovo gruppo di protezione utilizzando hello [New DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

Hello sopra cmdlet verrà creato un gruppo di protezione denominato *ProtectGroup01*. Inoltre possibile modificare un gruppo protezione dati successiva tooadd toohello backup cloud di Azure. Tuttavia, toomake modifiche toohello gruppo protezione dati - nuovo o esistente, è necessario tooget un handle in un *modificabile* oggetto utilizzando hello [Get DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a>Aggiunta di membri di gruppo toohello gruppo protezione dati
Ogni agente DPM SA elenco hello di origini dati nel server di hello cui è installato. tooadd toohello un'origine dati gruppo protezione dati, hello agente DPM esigenze toofirst invia un elenco di server DPM toohello indietro di hello origini dati. Uno o più origini dati vengono quindi selezionate e aggiunte toohello gruppo protezione dati. i passaggi di PowerShell Hello necessarie tooachieve questo sono:

1. Recuperare un elenco di tutti i server gestiti da DPM tramite hello agente DPM.
2. Scegliere un server specifico.
3. Recuperare un elenco di tutte le origini dati nel server di hello.
4. Scegliere uno o più origini dati e aggiungerli toohello gruppo protezione dati

elenco di Hello del server in cui hello agente Data Protection Manager è installato e viene gestito dal Server DPM hello viene acquisito con hello [Get DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet. In questo esempio verrà applicato un filtro e per il backup verrà configurato solo il server di produzione denominato *productionserver01* .

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

Ora recuperare elenco hello di origini dati in ```$server``` utilizzando hello [Get DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet. In questo esempio si Filtra per volume hello * unità d:\* che tooconfigure per il backup. L'origine dati viene quindi aggiunto toohello gruppo protezione dati utilizzando hello [Aggiungi DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet. Ricordare hello toouse *modificabile* oggetto gruppo protezione dati ```$MPG``` aggiunte hello toomake.

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

Ripetere questo passaggio il numero di volte in base alle esigenze fino a quando non sono stati aggiunti tutti hello gruppo protezione dati di origini dati toohello scelto. È possibile iniziare con una sola origine dati e del flusso di lavoro hello completo per la creazione di hello gruppo protezione dati e successivamente aggiungere altre origini dati toohello gruppo protezione dati.

### <a name="selecting-hello-data-protection-method"></a>Selezione metodo protezione dati di hello
Dopo aver aggiunto le origini dati hello toohello gruppo protezione dati, passaggio successivo hello è metodo di protezione hello toospecify utilizzando hello [Set DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet. In questo esempio hello gruppo protezione dati è configurato per il disco locale e il backup nel cloud. È inoltre necessario toospecify hello datasource che si desidera toocloud tooprotect utilizzando hello [Aggiungi DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet con - flag Online.

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a>Impostazione di un intervallo di conservazione hello
Impostare il mantenimento dati hello per i punti di backup hello utilizzando hello [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet. Anche se potrebbe sembrare memorizzazione hello tooset dispari prima di pianificazione del backup hello è stato definito utilizzando hello ```Set-DPMPolicyObjective``` imposta automaticamente una pianificazione di backup predefinito che può quindi essere modificata. È sempre possibile tooset pianificazione del backup hello innanzitutto e hello criteri di conservazione dopo.

Nel seguente esempio hello hello imposta i parametri di memorizzazione hello per i backup su disco. Questo verrà conservazione dei backup per 10 giorni e sincronizzare i dati ogni 6 ore tra il server di produzione hello e hello Data Protection Manager. Hello ```SynchronizationFrequencyMinutes``` non definisce la frequenza con cui un punto di ripristino viene creato, ma come spesso dati sono il server DPM toohello copiato.  Questa impostazione impedisce che i backup diventino di dimensioni eccessive.

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

Per i backup verranno tooAzure (Data Protection Manager si riferisce toothem come backup in linea) periodi di mantenimento hello possono essere configurati per [utilizzando uno schema nonno-padre-figlio (condivisione file di Groove) di memorizzazione a lungo termine](backup-azure-backup-cloud-as-tape.md). Ciò significa che è possibile definire un criterio di conservazione combinato che includa criteri giornalieri, settimanali, mensili e annuali. In questo esempio è una matrice che rappresenta lo schema di memorizzazione complesso hello che si desidera creare e quindi configurare l'intervallo di conservazione hello utilizzando hello [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a>Pianificazione del backup hello set
DPM imposta automaticamente una pianificazione di backup predefinito se si specifica l'obiettivo di protezione di hello utilizzando hello ```Set-DPMPolicyObjective``` cmdlet. le pianificazioni predefinite hello toochange, utilizzare hello [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet seguito da hello [Set DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

In hello sopra riportato, ```$onlineSch``` è una matrice con quattro elementi che contiene pianificazione protezione dati online esistente hello per hello gruppo protezione dati nello schema di condivisione file di Groove hello:

1. ```$onlineSch[0]```contiene una pianificazione giornaliera hello
2. ```$onlineSch[1]```contiene una pianificazione settimanale hello
3. ```$onlineSch[2]```contiene la pianificazione mensile hello
4. ```$onlineSch[3]```contiene pianificazione annuale hello

Pertanto se è necessaria una pianificazione settimanale di hello toomodify, è necessario toorefer toohello ```$onlineSch[1]```.

### <a name="initial-backup"></a>Backup iniziale
Quando backup di un'origine dati per hello prima volta, DPM deve creare la replica iniziale che crea una copia completa di hello datasource toobe protetti nel volume di replica DPM. Questa attività possono essere pianificata per un momento specifico o può essere attivata manualmente, utilizzando hello [Set DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet con il parametro hello ```-NOW```.

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a>Modifica delle dimensioni di hello di Replica DPM & volume del punto di ripristino
È possibile inoltre modificare hello dimensioni del volume di Replica di DPM e l'utilizzo di copia Shadow volume [Set DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet come hello di esempio seguente: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-manuale - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)

### <a name="committing-hello-changes-toohello-protection-group"></a>Il commit hello modifiche toohello gruppo protezione dati
Infine, le modifiche di hello necessario toobe eseguito il commit prima che DPM può eseguire il backup di hello in base alla configurazione di hello nuovo gruppo protezione dati. Ciò può essere ottenuto utilizzando hello [Set DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a>Visualizzare i punti di backup hello
È possibile utilizzare hello [Get DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget cmdlet un elenco di tutti i punti di ripristino per un'origine dati. Nell'esempio seguente, vengono:

* FETCH tutti hello PGs nel server DPM hello e archiviati in una matrice```$PG```
* ottenere toohello corrispondente di hello origini dati```$PG[0]```
* ottenere tutti i punti di ripristino hello per un'origine dati.

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a>Ripristino dei dati protetti su Azure
Il ripristino dei dati è una combinazione tra un oggetto ```RecoverableItem``` e un oggetto ```RecoveryOption```. Nella sezione precedente hello, abbiamo un elenco di punti di backup hello per un'origine dati.

Nell'esempio hello riportato di seguito viene illustrato come macchina virtuale di Hyper-V toorestore da Azure Backup dai punti di backup in combinazione con hello destinazione per il ripristino. L'esempio include quanto segue:

* Creazione di un'opzione di ripristino utilizzando hello [New DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.
* Matrice di hello recupero dei punti di backup utilizzando hello ```Get-DPMRecoveryPoint``` cmdlet.
* Scelta di un backup toorestore punto da.

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

i comandi di Hello possono essere facilmente esteso per qualsiasi tipo di origine dati.

## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni su DPM vedere Backup tooAzure [tooDPM introduzione Backup](backup-azure-dpm-introduction.md)
