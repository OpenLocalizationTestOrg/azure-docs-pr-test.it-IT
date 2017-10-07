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
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a>Distribuire e gestire backup tooAzure per i server di Data Protection Manager (DPM) mediante PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-dpm-automation.md)
> * [Classico](backup-dpm-automation-classic.md)
>
>

Questo articolo viene illustrato come toouse PowerShell tooback backup e ripristinare i dati DPM da un insieme di credenziali di backup. Microsoft consiglia l'uso di insiemi di credenziali dei Servizi di ripristino per tutte le nuove distribuzioni. Nel caso di un nuovo utente di Backup di Azure, usare l'articolo hello [distribuire e gestire Data Protection Manager dati tooAzure tramite PowerShell](backup-dpm-automation.md), pertanto si archiviano i dati in un insieme di credenziali di servizi di ripristino.

> [!IMPORTANT]
> È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery. Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup. Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup. **Entro il 1° novembre 2017**:
>- Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.
>- Si sarà in grado di tooaccess ai dati di backup nel portale classico hello. Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.
>

## <a name="setting-up-hello-powershell-environment"></a>Impostazione di ambiente PowerShell hello
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Prima di poter utilizzare PowerShell toomanage backup da Data Protection Manager tooAzure, sarà necessario toohave hello destra ambiente PowerShell. All'inizio di hello della sessione di PowerShell hello, assicurarsi di eseguire hello seguenti moduli destra di comando tooimport hello e consentono di determinare i cmdlet DPM toocorrectly riferimento hello:

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

1. [Scaricare la versione più recente di PowerShell](https://github.com/Azure/azure-powershell/releases) (la versione minima richiesta è: 1.0.0)
2. Abilitare i commandlet del Backup di Azure hello passando troppo*AzureResourceManager* modalità tramite hello **Switch-AzureMode** cmdlet:

```
PS C:\> Switch-AzureMode AzureResourceManager
```

Hello seguente programma di installazione e le attività di registrazione può essere automatizzata con PowerShell:

* Creare un insieme di credenziali per il backup
* Installare hello Azure Backup agent
* Registrazione con hello servizio Azure Backup
* Impostazioni di rete
* Impostazioni crittografia

### <a name="create-a-backup-vault"></a>Creare un insieme di credenziali per il backup
> [!WARNING]
> Per i clienti che usano Azure Backup per hello prima volta, è necessario tooregister hello Azure Backup provider toobe utilizzato con la sottoscrizione. Questa operazione può essere eseguita tramite l'esecuzione di hello comando seguente: "Microsoft.Backup" Register AzureProvider - ProviderNamespace
>
>

È possibile creare un nuovo insieme di credenziali di backup utilizzando hello **New AzureRMBackupVault** cmdlet. insieme di credenziali backup Hello è una risorsa ARM, pertanto è necessario tooplace all'interno di un gruppo di risorse. In una console di Azure PowerShell con privilegi elevata, eseguire hello seguenti comandi:

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

È possibile ottenere un elenco di tutti gli archivi di backup hello in una specifica sottoscrizione utilizzando hello **Get AzureRMBackupVault** cmdlet.

### <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a>Installazione agente Azure Backup hello in un Server DPM
Prima di installare l'agente Azure Backup hello, è necessario il programma di installazione di toohave hello scaricato e presenti sul Server di Windows hello. È possibile ottenere una versione più recente di hello del programma di installazione hello da hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) o dalla pagina Dashboard hello backup vault. Salvare installer hello tooan posizione facilmente accessibile, ad esempio * C:\Downloads\*.

esecuzione comando in una console di PowerShell con privilegi elevata seguente hello tooinstall agente hello **nel server DPM hello**:

```
PS C:\> MARSAgentInstaller.exe /q
```

Consente di installare agente hello con tutte le opzioni predefinite di hello. installazione di Hello richiede alcuni minuti in background hello. Se non si specifica hello */nu* hello opzione **Windows Update** aprirà la finestra alla fine hello hello toocheck di installazione per tutti gli aggiornamenti.

agente Hello verrà visualizzato nell'elenco di hello dei programmi installati. elenco di hello toosee dei programmi installati, andare troppo**Pannello di controllo** > **programmi** > **programmi e funzionalità**.

![Agente installato](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a>Opzioni di installazione
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

### <a name="registering-with-hello-azure-backup-service"></a>Registrazione con hello servizio Azure Backup
Prima di poter registrare con hello servizio Backup di Azure, è necessario tooensure tale hello [prerequisiti](backup-azure-dpm-introduction.md) sono soddisfatti. È necessario:

* Avere una sottoscrizione di Azure valida
* Ottieni un archivio di backup

toodownload hello insieme di credenziali, eseguire hello **Get AzureBackupVaultCredentials** cmdlet in una console PowerShell di Azure e l'archivio in una posizione comoda come * C:\Downloads\*.

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

Registrazione macchina hello con insieme di credenziali hello avviene utilizzando hello [inizio DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

Consente di registrare il Server DPM denominato "TestingServer" hello insieme di credenziali di Microsoft Azure hello specificato utilizzando le credenziali dell'insieme di credenziali.

> [!IMPORTANT]
> Non usare file delle credenziali dell'insieme di credenziali hello toospecify i percorsi relativi. È necessario fornire un percorso assoluto come un cmdlet toohello input.
>
>

### <a name="initial-configuration-settings"></a>Impostazioni di configurazione iniziali
Una volta hello Server DPM registrato insieme di credenziali di Backup di Azure hello, verrà avviato con le impostazioni di sottoscrizione predefinite. Queste impostazioni di sottoscrizione includono funzionalità di rete, la crittografia e hello area di gestione temporanea. toobegin modifica hello le impostazioni di sottoscrizione è necessario toofirst ottenere un handle su hello (predefinito) le impostazioni esistenti utilizzando hello [Get DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

Tutte le modifiche vengono apportate toothis locale PowerShell oggetto ```$setting``` e quindi completa dell'oggetto hello è tooDPM eseguito il commit e Backup di Azure toosave loro utilizzando hello [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet. È necessario hello toouse ```–Commit``` tooensure di flag che hello le modifiche vengono mantenute. le impostazioni di Hello saranno non applicate e utilizzate dal Backup di Azure, a meno che il commit.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a>Rete
Se la connettività di hello di hello DPM macchina toohello servizio di Backup di Azure su hello internet è tramite un server proxy, impostazioni del server proxy hello devono essere fornite per i backup toosucceed. Questa operazione viene eseguita tramite hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` hello e ```ProxyPassword``` parametri con hello [Set DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet. In questo esempio non esiste alcun server proxy, pertanto sono state eliminate tutte le informazioni relative al proxy.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

Utilizzo della larghezza di banda può essere controllata anche con le opzioni di ```-WorkHourBandwidth``` e ```-NonWorkHourBandwidth``` per un set specificato di giorni della settimana hello. In questo esempio non viene impostata alcuna limitazione.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-hello-staging-area"></a>Configurare l'Area di gestione temporanea hello
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
In questa sezione verrà aggiunta una tooDPM di server di produzione e quindi proteggere l'archiviazione di DPM toolocal dati hello e quindi tooAzure Backup. Negli esempi di hello verrà illustrato come tooback backup di file e cartelle. Hello logica può facilmente essere estesa toobackup qualsiasi origine dati con supporto di DPM. Tutti i backup DPM sono regolati da un gruppo protezione dati costituito da quattro parti:

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
Ogni agente DPM SA elenco hello di origini dati nel server di hello cui è installato. tooadd toohello un'origine dati gruppo protezione dati, hello agente DPM esigenze toofirst invia un elenco di server DPM toohello indietro di hello origini dati. Uno o più origini dati vengono quindi selezionate e aggiunte toohello gruppo protezione dati. è possibile ottenere tooget di Hello PowerShell passaggi necessari sono:

1. Recuperare un elenco di tutti i server gestiti da DPM tramite hello agente DPM.
2. Scegliere un server specifico.
3. Recuperare un elenco di tutte le origini dati nel server di hello.
4. Scegliere uno o più origini dati e aggiungerli toohello gruppo protezione dati

elenco di Hello del server in cui hello agente Data Protection Manager è installato e viene gestito dal Server DPM hello viene acquisito con hello [Get DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet. In questo esempio verrà applicato un filtro e per il backup verrà configurato solo il server di produzione denominato *productionserver01* .

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

Ora recuperare elenco hello di origini dati in ```$server``` utilizzando hello [Get DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet. In questo esempio si Filtra per volume hello * unità d:\* che si desidera tooconfigure per il backup. L'origine dati viene quindi aggiunto toohello gruppo protezione dati utilizzando hello [Aggiungi DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet. Ricordare hello toouse *modifable* oggetto gruppo protezione dati ```$MPG``` aggiunte hello toomake.

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

Ripetere questo passaggio il numero di volte in base alle esigenze fino a quando non sono stati aggiunti tutti hello gruppo protezione dati di origini dati toohello scelto. È possibile iniziare con una sola origine dati e del flusso di lavoro hello completo per la creazione di hello gruppo protezione dati e successivamente aggiungere altre origini dati toohello gruppo protezione dati.

### <a name="selecting-hello-data-protection-method"></a>Selezione metodo protezione dati di hello
Dopo aver aggiunto le origini dati hello toohello gruppo protezione dati, passaggio successivo hello è metodo di protezione hello toospecify utilizzando hello [Set DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet. In questo esempio hello gruppo protezione dati verrà configurato per il disco locale e il backup nel cloud. È inoltre necessario toospecify hello datasource che si desidera toocloud tooprotect utilizzando hello [Aggiungi DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet con - flag Online.

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a>Impostazione di un intervallo di conservazione hello
Impostare il mantenimento dati hello per i punti di backup hello utilizzando hello [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet. Anche se potrebbe sembrare memorizzazione hello tooset dispari prima di pianificazione del backup hello è stato definito utilizzando hello ```Set-DPMPolicyObjective``` imposta automaticamente una pianificazione di backup predefinito che può quindi essere modificata. È sempre possibile tooset pianificazione del backup hello innanzitutto e hello criteri di conservazione dopo.

Nel seguente esempio hello hello imposta i parametri di memorizzazione hello per i backup su disco. Questo verrà conservazione dei backup per 10 giorni e sincronizzare i dati ogni 6 ore tra il server di produzione hello e hello Data Protection Manager. Hello ```SynchronizationFrequencyMinutes``` non definisce la frequenza con cui un punto di ripristino viene creato, ma come spesso dati sono il server DPM toohello copiati; in questo modo i backup non diventino troppo grandi.

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

Per i backup verranno tooAzure (Data Protection Manager si riferisce toothese come backup in linea) periodi di mantenimento hello possono essere configurati per [utilizzando uno schema nonno-padre-figlio (condivisione file di Groove) di memorizzazione a lungo termine](backup-azure-backup-cloud-as-tape.md). Ciò significa che è possibile definire un criterio di conservazione combinato che includa criteri giornalieri, settimanali, mensili e annuali. In questo esempio è una matrice che rappresenta lo schema di memorizzazione complesso hello che si desidera creare e quindi configurare l'intervallo di conservazione hello utilizzando hello [Set DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.

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

Nell'esempio hello sopra, ```$onlineSch``` è una matrice con quattro elementi che contiene pianificazione protezione dati online esistente hello per hello gruppo protezione dati nello schema di condivisione file di Groove hello:

1. ```$onlineSch[0]```conterrà una pianificazione giornaliera hello
2. ```$onlineSch[1]```conterrà la pianificazione settimanale hello
3. ```$onlineSch[2]```conterrà la pianificazione mensile hello
4. ```$onlineSch[3]```conterrà pianificazione annuale hello

Pertanto se è necessaria una pianificazione settimanale di hello toomodify, è necessario toorefer toohello ```$onlineSch[1]```.

### <a name="initial-backup"></a>Backup iniziale
Per eseguire il backup un'origine dati per hello prima volta, DPM deve toocreate una replica iniziale che verrà creata una copia di hello datasource toobe protetti nel volume di replica DPM. Questa attività possono essere pianificata per un momento specifico o può essere attivata manualmente, utilizzando hello [Set DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet con il parametro hello ```-NOW```.

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a>Modifica delle dimensioni di hello di Replica DPM & volume del punto di ripristino
È inoltre possibile modificare le dimensioni di hello del volume di Replica di DPM, nonché la copia Shadow volume mediante [Set DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet come hello di esempio seguente: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-manuale - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)

### <a name="committing-hello-changes-toohello-protection-group"></a>Il commit hello modifiche toohello gruppo protezione dati
Infine, le modifiche di hello necessario toobe eseguito il commit prima che DPM può eseguire il backup di hello in base alla configurazione di hello nuovo gruppo protezione dati. Questa operazione viene eseguita utilizzando hello [Set DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a>Visualizzare i punti di backup hello
È possibile utilizzare hello [Get DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget cmdlet un elenco di tutti i punti di ripristino per un'origine dati. Nell'esempio seguente, vengono:

* recuperare tutti i PGs hello nel server DPM hello che verrà archiviato in una matrice```$PG```
* ottenere toohello corrispondente di hello origini dati```$PG[0]```
* ottenere tutti i punti di ripristino hello per un'origine dati.

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a>Ripristino dei dati protetti su Azure
Il ripristino dei dati è una combinazione tra un oggetto ```RecoverableItem``` e un oggetto ```RecoveryOption```. Nella sezione precedente hello, abbiamo un elenco di punti di backup hello per un'origine dati.

Nell'esempio hello riportato di seguito viene illustrato come macchina virtuale di Hyper-V toorestore da Azure Backup dai punti di backup in combinazione con hello destinazione per il ripristino. Sono inclusi:

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
* Per ulteriori informazioni sui Backup di Azure per DPM vedere [tooDPM introduzione Backup](backup-azure-dpm-introduction.md)
