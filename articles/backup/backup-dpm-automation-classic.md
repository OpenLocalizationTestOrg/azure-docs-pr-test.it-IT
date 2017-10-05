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
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a>Distribuire e gestire il backup in Azure per server Data Protection Manager (DPM) mediante PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-dpm-automation.md)
> * [Classico](backup-dpm-automation-classic.md)
>
>

Questo articolo spiega come usare PowerShell per il backup e il ripristino di dati di DPM da un insieme di credenziali di backup. Microsoft consiglia l'uso di insiemi di credenziali dei Servizi di ripristino per tutte le nuove distribuzioni. Se si è un nuovo utente di Backup di Azure, vedere l'articolo [Distribuire e gestire i dati di Data Protection Manager in Azure mediante PowerShell](backup-dpm-automation.md), in modo da archiviare i dati in un insieme di credenziali dei Servizi di ripristino.

> [!IMPORTANT]
> È ora possibile aggiornare gli insiemi di credenziali di Backup ad insiemi di credenziali dei servizi di ripristino. Per altre informazioni, vedere l'articolo [Aggiornare un insieme di credenziali di Backup a un insieme di credenziali di Servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft consiglia di aggiornare gli insiemi di credenziali di Backup a insiemi di credenziali dei servizi di ripristino. Dopo il 15 ottobre 2017 non sarà possibile usare PowerShell per creare insiemi di credenziali di backup. **Entro il 1° novembre 2017**:
>- Tutti gli insiemi di credenziali di backup rimanenti verranno aggiornati automaticamente a insiemi di credenziali dei servizi di ripristino.
>- e non sarà più possibile accedere ai dati di backup nel portale classico. Sarà possibile invece usare il portale di Azure per accedere ai dati di backup negli insiemi di credenziali di servizi di ripristino.
>

## <a name="setting-up-the-powershell-environment"></a>Configurazione dell'ambiente di PowerShell
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Prima di poter usare PowerShell per gestire i backup da Data Protection Manager ad Azure, sarà necessario disporre dell'ambiente appropriato in PowerShell. All'inizio della sessione di PowerShell, assicurarsi di eseguire il comando seguente per importare i moduli appropriati e fare riferimento correttamente ai cmdlet DPM:

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

## <a name="setup-and-registration"></a>Installazione e registrazione
Per iniziare:

1. [Scaricare la versione più recente di PowerShell](https://github.com/Azure/azure-powershell/releases) (la versione minima richiesta è: 1.0.0)
2. Per iniziare, abilitare i cmdlet del servizio Backup di Azure passando alla modalità *AzureResourceManager* usando il cmdlet **Switch-AzureMode** :

```
PS C:\> Switch-AzureMode AzureResourceManager
```

Le attività di installazione e registrazione seguenti possono essere automatizzate tramite PowerShell:

* Creare un insieme di credenziali per il backup
* Installazione dell'agente di Backup di Azure
* Registrazione del servizio Backup di Azure
* Impostazioni di rete
* Impostazioni crittografia

### <a name="create-a-backup-vault"></a>Creare un insieme di credenziali per il backup
> [!WARNING]
> I clienti che usano il servizio Backup di Azure per la prima volta, dovranno registrare il provider di Backup di Azure da usare con la propria sottoscrizione. A tale scopo, eseguire il comando seguente: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"
>
>

È possibile creare un nuovo insieme di credenziali per il backup usando il cmdlet **New-AzureRMBackupVault** . L’archivio di backup è una risorsa ARM, pertanto è necessario inserirlo all'interno di un gruppo di risorse. Eseguire i comandi seguenti in una console di Azure PowerShell con privilegi elevati:

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

È possibile ottenere un elenco di tutti gli insiemi di credenziali per il backup in una determinata sottoscrizione usando il cmdlet **Get-AzureRMBackupVault** .

### <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a>Installazione dell'agente di Backup di Azure in un server DPM
Per installare l'agente di Backup di Azure, è necessario aver scaricato il programma di installazione nel server Windows. È possibile ottenere la versione più recente del programma di installazione dall' [Area download Microsoft](http://aka.ms/azurebackup_agent) .o dalla pagina Dashboard dell’archivio di backup. Salvare il programma di installazione in un percorso facilmente accessibile come *C:\Downloads\*.

Per installare l'agente, eseguire il comando seguente in una console di PowerShell con privilegi elevati **nel server DPM**:

```
PS C:\> MARSAgentInstaller.exe /q
```

L'agente verrà installato con tutte le opzioni predefinite. L'installazione richiede alcuni minuti in background. Se non si specifica l'opzione */nu* , la finestra **Windows Update** si aprirà al termine dell'installazione per verificare la presenza di eventuali aggiornamenti.

L'agente verrà visualizzato nell'elenco dei programmi installati. Per visualizzare l'elenco dei programmi installati, passare a **Pannello di controllo** > **Programmi** > **Programmi e funzionalità**.

![Agente installato](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a>Opzioni di installazione
Per visualizzare tutte le opzioni disponibili tramite la riga di comando, utilizzare il comando seguente:

```
PS C:\> MARSAgentInstaller.exe /?
```

Le opzioni disponibili includono:

| Opzione | Dettagli | Default |
| --- | --- | --- |
| /q |Installazione non interattiva |- |
| /p:"location" |Percorso della cartella di installazione per l'agente di Backup di Azure. |C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure |
| /s:"location" |Percorso della cartella della cache per l'agente di Backup di Azure. |C:\Programmi\Agente di Servizi di ripristino di Microsoft Azure\Scratch |
| /m |Consenso esplicito a Microsoft Update |- |
| /nu |Al termine dell'installazione non vengono cercati gli aggiornamenti |- |
| /d |Disinstalla l'agente di Servizi di ripristino di Microsoft Azure |- |
| /ph |Indirizzo host proxy |- |
| /po |Numero porta host proxy |- |
| /pu |Nome utente host proxy |- |
| /pw |Password proxy |- |

### <a name="registering-with-the-azure-backup-service"></a>Registrazione del servizio Backup di Azure
Per poter eseguire la registrazione con il servizio Backup di Azure, è necessario assicurarsi che i [prerequisiti](backup-azure-dpm-introduction.md) siano soddisfatti. È necessario:

* Avere una sottoscrizione di Azure valida
* Ottieni un archivio di backup

Per scaricare le credenziali dell'archivio, eseguire il commandlet **Get AzureBackupVaultCredentials** in una console Azure PowerShell e archiviarlo in una posizione comoda come *C:\Downloads\*.

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

La registrazione del computer con l'insieme di credenziali viene eseguita utilizzando il cmdlet [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) :

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

In questo modo, il server DPM denominato "TestingServer" verrà registrato con l'insieme di credenziali di Microsoft Azure usando le credenziali specificate.

> [!IMPORTANT]
> Non utilizzare percorsi relativi per specificare il file dell'insieme di credenziali. È necessario fornire un percorso assoluto come input per il cmdlet.
>
>

### <a name="initial-configuration-settings"></a>Impostazioni di configurazione iniziali
Una volta registrato il server DPM con l'insieme di credenziali di Backup di Azure, il server verrà avviato con le impostazioni di sottoscrizione predefinite. Tali impostazioni includono rete, crittografia e area di staging. Per iniziare a modificare le impostazioni di sottoscrizione, è necessario innanzitutto ottenere un handle sulle impostazioni (predefinite) esistenti usando il cmdlet [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) :

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

Tutte le modifiche vengono apportate a questo oggetto locale PowerShell ```$setting``` e poi viene eseguito il commit dell'oggetto completo in DPM e in Backup di Azure eseguendo il salvataggio mediante il cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791). È necessario usare il flag ```–Commit``` per garantire che le modifiche vengano mantenute. Le impostazioni vengono applicate e usate da Backup di Azure solo dopo il commit.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a>Rete
Se la connettività del computer DPM al servizio Backup di Azure in Internet usa un server proxy, per consentire la corretta esecuzione dei backup è necessario fornire le impostazioni del server proxy. A tale scopo, usare i parametri ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` e ```ProxyPassword``` con il cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791). In questo esempio non esiste alcun server proxy, pertanto sono state eliminate tutte le informazioni relative al proxy.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

È anche possibile controllare l'utilizzo della larghezza di banda con le opzioni ```-WorkHourBandwidth``` e ```-NonWorkHourBandwidth``` per un determinato set di giorni della settimana. In questo esempio non viene impostata alcuna limitazione.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-the-staging-area"></a>Configurazione dell'area di gestione temporanea
L'agente del servizio Backup di Azure in esecuzione nel server DPM deve disporre di archiviazione temporanea per i dati ripristinati dal cloud (area di staging locale). Configurare l'area di gestione temporanea usando il cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) e il parametro ```-StagingAreaPath```.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

Nell'esempio precedente, l'area di gestione temporanea verrà impostata su *C:\StagingArea* nell'oggetto di PowerShell ```$setting```. Assicurarsi che la cartella specificata esista già, altrimenti il commit finale delle impostazioni di sottoscrizione avrà esito negativo.

### <a name="encryption-settings"></a>Impostazioni crittografia
I dati di backup inviati a Backup di Azure vengono crittografati per proteggere la riservatezza dei dati. La passphrase di crittografia è la "password" per decrittografare i dati in fase di ripristino. È importante conservarla al sicuro e proteggerla dopo averla impostata.

Nel seguente esempio, il primo comando consente di convertire la passphrase della stringa ```passphrase123456789``` in una stringa sicura; inoltre, consente di assegnare la stringa sicura alla variabile denominata ```$Passphrase```. Il secondo comando imposta la stringa sicura in ```$Passphrase``` come password per la crittografia dei backup.

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> Dopo l'impostazione, conservare le informazioni sulla passphrase al sicuro. Non sarà possibile ripristinare i dati da Azure senza la passphrase.
>
>

A questo punto, sono state apportate tutte le modifiche necessarie all'oggetto ```$setting``` . Ricordarsi di eseguire il commit delle modifiche:

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a>Proteggere i dati in Backup di Azure
In questa sezione verrà aggiunto un server di produzione a DPM e i dati verranno protetti nell'archivio DPM locale e quindi in Backup di Azure. Negli esempi, viene descritto come eseguire il backup di file e cartelle. È possibile estendere in modo semplice la logica al fine di eseguire il backup di qualsiasi origine dati supportata da DPM. Tutti i backup DPM sono regolati da un gruppo protezione dati costituito da quattro parti:

1. **Membri del gruppo** : elenco di tutti gli oggetti che è possibile proteggere (anche detti *origini dati* in DPM) e che si desidera proteggere nello stesso gruppo protezione dati. Ad esempio, è possibile proteggere le macchine virtuali di produzione in un gruppo protezione dati e i database di SQL Server in un altro gruppo, in quanto potrebbero avere requisiti di backup diversi. Prima di eseguire il backup di qualsiasi origine dati in un server di produzione, è necessario assicurarsi che l'agente DPM sia installato nel server e gestito da DPM. Seguire la procedura di [installazione dell'agente DPM](https://technet.microsoft.com/library/bb870935.aspx) e collegamento dell'agente al server DPM appropriato.
2. **Metodo di protezione dati** : specifica le posizioni di destinazione dei backup, ad esempio nastro, disco e cloud. In questo esempio i dati verranno protetti nel disco locale e nel cloud.
3. **Pianificazione dei backup** : specifica quando devono essere eseguiti i backup e con quale frequenza i dati devono essere sincronizzati tra il server DPM e il server di produzione.
4. Una **pianificazione di conservazione** che indica per quanto tempo è necessario conservare i punti di ripristino in Azure.

### <a name="creating-a-protection-group"></a>Creazione di un gruppo di protezione
Creare innanzitutto un nuovo gruppo protezione dati usando il cmdlet [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) .

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

Il cmdlet precedente creerà un gruppo protezione dati denominato *ProtectGroup01*. Un gruppo protezione dati esistente può anche essere modificato in seguito per aggiungere il backup nel cloud Azure. Tuttavia, per apportare modifiche al gruppo protezione dati, nuovo o esistente, è necessario ottenere un handle su un oggetto *modificabile* usando il cmdlet [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) .

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a>Aggiunta di membri al gruppo protezione dati
Ogni agente DPM conosce l'elenco di origini dati nel server in cui è installato. Per aggiungere un'origine dati al gruppo protezione dati, l'agente DPM deve innanzitutto inviare un elenco delle origini dati al server DPM. Vengono quindi selezionate una o più origini dati, che vengono aggiunte al gruppo protezione dati. La procedura di PowerShell da eseguire a questo scopo è la seguente:

1. Recuperare un elenco di tutti i server gestiti da DPM tramite l'agente DPM.
2. Scegliere un server specifico.
3. Recuperare un elenco di tutte le origini dati nel server.
4. Scegliere una o più origini dati e aggiungerle al gruppo protezione dati.

È possibile acquisire l'elenco di tutti i server in cui è installato l'agente DPM e che sono gestiti dal server DPM tramite il cmdlet [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) . In questo esempio verrà applicato un filtro e per il backup verrà configurato solo il server di produzione denominato *productionserver01* .

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

Recuperare quindi l'elenco di origini dati in ```$server``` usando il cmdlet [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605). In questo esempio viene filtrato il volume *D:\*, da configurare per il backup. L'origine dati viene quindi aggiunta al gruppo protezione dati usando il cmdlet [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732). Ricordarsi di usare l'oggetto gruppo protezione dati *modificabile* ```$MPG``` per effettuare le aggiunte.

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

Ripetere questo passaggio il numero di volte necessario per aggiungere tutte le origini dati scelte al gruppo protezione dati. È anche possibile iniziare con una sola origine dati e completare il flusso di lavoro per la creazione del gruppo protezione dati, quindi, in un secondo momento, aggiungere altre origini dati al gruppo protezione dati.

### <a name="selecting-the-data-protection-method"></a>Selezione del metodo di protezione dati
Una volta aggiunte le origini dati al gruppo protezione dati, il passaggio successivo consiste nello specificare il metodo di protezione usando il cmdlet [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) . In questo esempio il gruppo protezione dati verrà configurato per il backup su disco locale e nel cloud. È inoltre necessario specificare l'origine dati che si desidera proteggere per il cloud utilizzando il cmdlet [Aggiungi DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) con -flag Online.

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a>Impostazione del periodo di mantenimento dati
Impostare il periodo di conservazione per i punti di backup usando il cmdlet [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) . Anche se può sembrare strano impostare il periodo di conservazione prima di definire la pianificazione dei backup, usando il cmdlet ```Set-DPMPolicyObjective``` viene automaticamente impostata una pianificazione dei backup predefinita che può quindi essere modificata. È sempre possibile impostare prima la pianificazione dei backup e successivamente i criteri di conservazione.

Nell'esempio seguente il cmdlet imposta i parametri di conservazione per i backup su disco. I backup verranno conservati per 10 giorni e i dati verranno sincronizzati ogni 6 ore tra il server di produzione e il server DPM. ```SynchronizationFrequencyMinutes``` non definisce la frequenza di creazione di un punto di backup, ma la frequenza con cui i dati vengono copiati nel server DPM. In questo modo, si impedisce che i backup diventino troppo grossi.

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

Per i backup destinati ad Azure (indicati in DPM come backup online), è possibile configurare i periodi di mantenimento dati per la [conservazione a lungo termine usando uno schema GFS (Grandfather-Father-Son, nonno-padre-figlio)](backup-azure-backup-cloud-as-tape.md). Ciò significa che è possibile definire un criterio di conservazione combinato che includa criteri giornalieri, settimanali, mensili e annuali. In questo esempio viene creata una matrice che rappresenta lo schema di conservazione complesso desiderato e quindi viene configurato il periodo di mantenimento dati usando il cmdlet [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a>Impostare la pianificazione dei backup
Se si specifica l'obiettivo di protezione usando il cmdlet ```Set-DPMPolicyObjective``` , DPM imposta automaticamente una pianificazione dei backup predefinita. Per modificare le pianificazioni predefinite, usare il cmdlet [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749), seguito da quello [Set DPMPolicySchedule](https://technet.microsoft.com/library/hh881723).

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

Nell'esempio precedente ```$onlineSch``` è una matrice con quattro elementi che contiene la pianificazione della protezione online esistente per il gruppo protezione dati nello schema GFS:

1. ```$onlineSch[0]``` conterrà la pianificazione giornaliera
2. ```$onlineSch[1]``` conterrà la pianificazione settimanale
3. ```$onlineSch[2]``` conterrà la pianificazione mensile
4. ```$onlineSch[3]``` conterrà la pianificazione annuale

Se pertanto è necessario modificare la pianificazione settimanale, è necessario fare riferimento a ```$onlineSch[1]```.

### <a name="initial-backup"></a>Backup iniziale
Quando si esegue il backup di un'origine dati per la prima volta, DPM deve creare una replica iniziale che a sua volta creerà una copia dell'origine dati da proteggere nel volume di replica DPM. È possibile pianificare questa attività a un orario specifico oppure attivarla manualmente, usando il cmdlet [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) con il parametro ```-NOW```.

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a>Modifica delle dimensioni della replica DPM e volume del punto di ripristino
È inoltre possibile modificare le dimensioni del volume della replica DPM e del volume copia shadow [utilizzando il cmdlet Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) come nell'esempio seguente: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)

### <a name="committing-the-changes-to-the-protection-group"></a>Commit delle modifiche nel gruppo protezione dati
Infine, è necessario eseguire il commit delle modifiche affinché DPM possa eseguire il backup in base alla nuova configurazione del gruppo protezione dati. A tale scopo, usare il cmdlet [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) .

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a>Visualizzare i punti di backup
È possibile usare il cmdlet [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) per ottenere un elenco di tutti i punti di ripristino per un'origine dati. Nell'esempio seguente, vengono:

* recuperati tutti i gruppi di protezione (PG) nel server DPM da archiviare in una matrice ```$PG```
* ottenuti le origini dati corrispondenti alla matrice ```$PG[0]```
* ottenuti tutti i punti di ripristino per un'origine dati.

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a>Ripristino dei dati protetti su Azure
Il ripristino dei dati è una combinazione tra un oggetto ```RecoverableItem``` e un oggetto ```RecoveryOption```. Nella sezione precedente è stato ottenuto un elenco dei punti di backup per un'origine dati.

Nell'esempio seguente viene illustrato come ripristinare una macchina virtuale Hyper-V da Backup di Azure mediante la combinazione di punti di backup con la destinazione per il ripristino. Sono inclusi:

* Creazione di un'opzione di ripristino usando il cmdlet [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592).
* Recupero della matrice di punti di backup usando il cmdlet ```Get-DPMRecoveryPoint``` .
* Scelta di un punto di backup da cui eseguire il ripristino.

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

I comandi possono essere facilmente estesi per qualsiasi tipo di origine dati.

## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni su Backup di Azure per DPM, vedere [Introduzione al backup di DPM](backup-azure-dpm-introduction.md)
