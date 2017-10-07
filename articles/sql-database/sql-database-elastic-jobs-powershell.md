---
title: aaaCreate e gestire processi elastici mediante PowerShell | Documenti Microsoft
description: Utilizzare PowerShell per il pool di Database SQL di Azure toomanage
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a>Creare e gestire processi elastici del database SQL con PowerShell (anteprima)

Hello APIs di PowerShell per **i processi di Database elastico** (in anteprima), consentono di definire un gruppo di database sul quale script verranno eseguiti. Questo articolo viene illustrato come toocreate e gestire **i processi di Database elastico** utilizzando i cmdlet di PowerShell. Vedere [Panoramica dei processi di database elastici](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Prerequisiti
* Una sottoscrizione di Azure. Per una versione di valutazione gratuita, vedere [Versione di valutazione gratuita di un mese](https://azure.microsoft.com/pricing/free-trial/).
* Un set di database creati con gli strumenti di Database elastico hello. Vedere [Iniziare a usare gli strumenti di database elastici](sql-database-elastic-scale-get-started.md).
* Azure PowerShell. Per informazioni dettagliate, vedere [come tooinstall e configurare Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
* **processi di database elastici** di PowerShell, vedere [Installing processi di database elastici](sql-database-elastic-jobs-service-installation.md)

### <a name="select-your-azure-subscription"></a>Selezionare la sottoscrizione ad Azure
sottoscrizione di hello tooselect è necessario l'Id sottoscrizione (**- SubscriptionId**) o nome della sottoscrizione (**- SubscriptionName**). Se si dispone di più sottoscrizioni, è possibile eseguire hello **Get AzureRmSubscription** hello cmdlet e copia desiderato informazioni sulla sottoscrizione dal set di risultati hello. Dopo aver creato le informazioni di sottoscrizione, eseguire hello seguente cmdlet tooset questa sottoscrizione come valore predefinito di hello, vale a dire hello destinazione per la creazione e la gestione dei processi:

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

Hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) è consigliato per l'utilizzo toodevelop ed eseguire gli script di PowerShell in processi di Database elastico hello.

## <a name="elastic-database-jobs-objects"></a>Oggetti dei processi di database elastici
Hello seguente tabella vengono elencati tutti i tipi di oggetto hello di **i processi di Database elastico** con la descrizione e APIs PowerShell rilevanti.

<table style="width:100%">
  <tr>
    <th>Tipo di oggetto</th>
    <th>Descrizione</th>
    <th>API correlate di PowerShell</th>
  </tr>
  <tr>
    <td>Credenziali</td>
    <td>Nome utente e password toouse quando ci si connette toodatabases per l'esecuzione di script o applicazione del file dacpac. <p>password Hello viene crittografata prima dell'invio tooand archiviato nel database di processi di Database elastico hello.  password Hello viene decrittografata dal servizio processi di Database elastico tramite credenziali hello creato e caricato da uno script di installazione di hello hello.</td>
    <td><p>Get-AzureSqlJobCredential</p>
    <p>New-AzureSqlJobCredential</p><p>Set-AzureSqlJobCredential</p></td></td>
  </tr>

  <tr>
    <td>Script</td>
    <td>Toobe di script Transact-SQL utilizzato per l'esecuzione tra i database.  script Hello dovrebbe essere idempotente toobe creati in quanto hello verrà ritentata l'esecuzione dello script hello al momento di errori.
    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>Get-AzureSqlJobContentDefinition</p>
    <p>New-AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>

  <tr>
    <td>DACPAC</td>
    <td><a href="https://msdn.microsoft.com/library/ee210546.aspx">Applicazione livello dati </a> toobe applicate ai database del pacchetto.

    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>New-AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>
  <tr>
    <td>Destinazione del database</td>
    <td>Server e database nome puntamento tooan Database SQL di Azure.

    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    </td>
  </tr>
  <tr>
    <td>Destinazione di partizionamento della mappa</td>
    <td>Combinazione di un database di destinazione e una credenziale toobe ha usato informazioni toodetermine archiviate all'interno di una mappa partizioni di Database elastico.
    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    <p>Set-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Destinazione di una raccolta personalizzata</td>
    <td>Gruppo definito di toocollectively database utilizzare per l'esecuzione.</td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Destinazione figlio di una raccolta personalizzata</td>
    <td>Destinazione di database a cui fa riferimento una raccolta personalizzata.</td>
    <td>
    <p>Add-AzureSqlJobChildTarget</p>
    <p>Remove-AzureSqlJobChildTarget</p>
    </td>
  </tr>

<tr>
    <td>Job</td>
    <td>
    <p>Definizione dei parametri per un processo che può essere utilizzato tootrigger esecuzione o toofulfill una pianificazione.</p>
    </td>
    <td>
    <p>Get-AzureSqlJob</p>
    <p>New-AzureSqlJob</p>
    <p>Set-AzureSqlJob</p>
    </td>
  </tr>

<tr>
    <td>Esecuzione del processo</td>
    <td>
    <p>Contenitore di attività toofulfill necessario eseguire uno script o l'applicazione di una destinazione tooa DACPAC utilizzando le credenziali per le connessioni di database a causa di errori gestiti in Criteri di conformità tooan esecuzione.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Wait-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>Esecuzione dell'attività di processo</td>
    <td>
    <p>Singola unità di lavoro toofulfill un processo.</p>
    <p>Se un'attività di processo non è in grado di toosuccessfully execute, verrà registrato il messaggio di eccezione risultante hello e una nuova attività di processo corrispondente verrà creata ed eseguite in base toohello specificato criteri di esecuzione.</p></p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Wait-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>Criterio di esecuzione del processo</td>
    <td>
    <p>Controlla le sospensioni dell’esecuzione dei processi, gli intervalli tra i tentativi, e i limiti dei tentativi.</p>
    <p>I Processi di database elastici includono un criterio di esecuzione di processo predefinito che provoca essenzialmente infiniti tentativi quando si verificano errori di attività di processo con backoff esponenziale di intervalli tra ogni tentativo.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecutionPolicy</p>
    <p>New-AzureSqlJobExecutionPolicy</p>
    <p>Set-AzureSqlJobExecutionPolicy</p>
    </td>
  </tr>

<tr>
    <td>Pianificazione</td>
    <td>
    <p>Tempo base specifica per l'esecuzione tootake luogo un intervallo ricorrente o su una sola volta.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobSchedule</p>
    <p>New-AzureSqlJobSchedule</p>
    <p>Set-AzureSqlJobSchedule</p>
    </td>
  </tr>

<tr>
    <td>Trigger del processo</td>
    <td>
    <p>Un mapping tra un processo e l'esecuzione del processo tootrigger una pianificazione in base toohello pianificazione.</p>
    </td>
    <td>
    <p>New-AzureSqlJobTrigger</p>
    <p>Remove-AzureSqlJobTrigger</p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a>Tipi di gruppo di processi di database elastici supportati
processo Hello esegue script Transact-SQL (T-SQL) o un'applicazione di dacpac tra un gruppo di database. Quando un processo viene inviato toobe eseguita in un gruppo di database, il processo di hello "espande" hello in processi figlio in cui ogni esegue hello richiesto l'esecuzione su un singolo database nel gruppo di hello. 

Si possono creare due tipi di gruppi: 

* [Mappa partizioni](sql-database-elastic-scale-shard-map-management.md) gruppo: quando tootarget inviato una mappa partizioni è un processo, processo hello query hello partizioni mappa toodetermine il set di partizioni corrente e quindi crea i processi per ogni partizione figlio nella mappa partizioni hello.
* Gruppo Raccolta personalizzata: set di database personalizzato. Quando un processo è destinato a una raccolta personalizzata, li crea i processi per ogni database attualmente in una raccolta personalizzata hello.

## <a name="tooset-hello-elastic-database-jobs-connection"></a>hello tooset connessione di processi di Database elastico
Una connessione è necessario impostare toohello processi di toobe *database del controllo* toousing precedente hello processi API. Esecuzione di questo cmdlet attiva un toopop finestra credential per richiedere nome utente hello e la password creata durante l'installazione di processi di Database elastico. Tutti gli esempi forniti in questo argomento presuppongono che il primo passaggio sia già stato eseguito.

Aprire i processi di Database elastico toohello una connessione:

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a>Credenziali crittografate all'interno di processi di Database elastico hello
Le credenziali del database possono essere inserite nei processi hello *database del controllo* con la password crittografata. È necessario toostore credenziali tooenable processi toobe eseguita in un secondo momento (utilizzando le pianificazioni dei processi).

Crittografia tramite un certificato creato come parte dello script di installazione di hello. Crea script di installazione di Hello e caricamenti hello certificato hello servizio Cloud di Azure per la decrittografia di hello archiviate password crittografate. in un secondo momento Hello servizio Cloud di Azure archivia la chiave pubblica hello all'interno di processi hello *database del controllo* che consente di hello API di PowerShell o portale di Azure classico interfaccia tooencrypt una password fornita senza richiedere il certificato di hello toobe installato nel computer locale.

le password delle credenziali di Hello sono crittografati e protetti da utenti accesso in sola lettura tooElastic processi degli oggetti di Database. Ma è possibile che un utente malintenzionato con accesso in lettura-scrittura tooElastic processi Database oggetti tooextract una password. Le credenziali sono progettate toobe riutilizzati tra esecuzioni del processo. Le credenziali vengono passate tootarget database quando si stabiliscono connessioni. Non sono attualmente presenti restrizioni per i database di destinazione hello utilizzati per le credenziali, l'utente malintenzionato aggiunga un database di destinazione per un database nel controllo del codice dell'utente malintenzionato hello. utente Hello successivamente è stato possibile avviare un processo di destinazione password della credenziale in questo database toogain hello.

Le procedure consigliate per i processi di database elastici includono:

* Limitare l'utilizzo dei singoli utenti di tootrusted API hello.
* Le credenziali devono avere hello almeno dei privilegi necessari tooperform hello mansione.  Per altre informazioni, vedere l'articolo [Autorizzazioni in SQL Server](https://msdn.microsoft.com/library/bb669084.aspx) di MSDN.

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a>toocreate una credenziale per l'esecuzione del processo tra i database crittografata
toocreate crittografata con una nuova credenziale, hello [ **cmdlet Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) richiede un nome utente e una password che può essere passata toohello [ **New AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a>credenziali tooupdate
Quando si modificano le password, utilizzare hello [ **cmdlet Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) e set hello **CredentialName** parametro.

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a>toodefine una destinazione di mappa partizioni di Database elastico
un processo in tutti i database in un set di partizioni tooexecute (creato utilizzando [libreria client di Database elastico](sql-database-elastic-database-client-library.md)), utilizzare una mappa partizioni come destinazione database hello. In questo esempio richiede un'applicazione partizionata utilizzando la libreria client di Database elastico hello. Vedere l'esempio in [Iniziare a usare gli strumenti di database elastici](sql-database-elastic-scale-get-started.md).

database di gestione della mappa partizioni Hello deve essere impostato come database di destinazione e quindi mappa partizioni specifici hello deve essere specificata come destinazione.

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Creare uno Script T-SQL per l'esecuzione tra database
Durante la creazione di script T-SQL per l'esecuzione, è consigliabile toobuild li toobe [idempotente](https://en.wikipedia.org/wiki/Idempotence) e resilienti in caso di errori. I processi di Database elastici ritenterà l'esecuzione di uno script ogni volta che l'esecuzione si verifica un errore, indipendentemente dalla classificazione hello dell'errore hello.

Hello utilizzare [ **cmdlet New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate e salvare uno script per l'esecuzione e impostare hello **- documento ContentName** e **- CommandText**parametri.

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a>Creare un nuovo script da un file
Se lo script T-SQL hello è definito all'interno di un file, utilizzare questo script hello tooimport:

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a>script tooupdate T-SQL per l'esecuzione tra database
L'aggiornamento di script di PowerShell hello testo del comando T-SQL per uno script esistente.

Set hello seguente variabili tooreflect hello desiderato script definizione toobe insieme:

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a>script esistente tooan tooupdate hello definizione
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a>toocreate tooexecute un processo uno script in una mappa partizioni
Questo script di PowerShell avvia un processo per l'esecuzione di uno script in ogni partizione di una mappa partizioni di scalabilità elastica.

Hello set seguenti hello tooreflect variabili desiderato script e destinazione:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a>tooexecute un processo
Questo script di PowerShell esegue un processo esistente:

Aggiornare hello toohave nome di variabile tooreflect hello desiderato processo eseguito seguenti:

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a>stato hello tooretrieve una singola esecuzione dei processi
Hello utilizzare [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) e set hello **JobExecutionId** stato hello tooview di parametro di esecuzione del processo.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

Utilizzare hello stesso **Get AzureSqlJobExecution** cmdlet con hello **IncludeChildren** parametro tooview hello stato esecuzioni del processo figlio, vale a dire hello stato specifico per ogni esecuzione del processo su ogni database di destinazione dal processo hello.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a>stato hello tooview tra più esecuzioni di processo
Hello [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) ha più parametri facoltativi che possono essere utilizzati toodisplay più esecuzioni di processo, filtrate tramite parametri hello fornito. esempio Hello vengono illustrate alcune delle possibili modi di hello toouse Get AzureSqlJobExecution:

Recuperare tutte le esecuzioni attive di processo di primo livello:

    Get-AzureSqlJobExecution

Recuperare tutte le esecuzioni di processo di primo livello, incluse le esecuzioni di processo inattive:

    Get-AzureSqlJobExecution -IncludeInactive

Recuperare tutte le esecuzioni di processo figlio di un ID di esecuzione processo fornito, incluse le esecuzioni di processo inattive:

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

Recuperare tutte le esecuzioni di processo create utilizzando una pianificazione / processo di combinazione, inclusi i processi inattivi:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

Recuperare tutti i processi destinati a una mappa di partizione specificata, inclusi i processi inattivi:

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Recuperare tutti i processi destinati a una raccolta personalizzata specificata, inclusi i processi inattivi:

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Recuperare l'elenco di hello di esecuzioni di attività del processo in esecuzione un processo specifico:

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

Recuperare i dettagli di esecuzione delle attività di processo:

Hello lo script di PowerShell seguente può essere utilizzato tooview hello dettagli di un'esecuzione di attività di processo, è particolarmente utile quando il debug degli errori di esecuzione.

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a>errori di tooretrieve all'interno di esecuzioni di attività di processo
Hello **JobTaskExecution oggetto** include una proprietà per hello del ciclo di vita dell'attività hello insieme a una proprietà del messaggio. Se un'esecuzione di attività del processo non è riuscita, hello del ciclo di vita e verrà impostata troppo*Failed* e verrà impostata la proprietà del messaggio hello toohello messaggio di eccezione risultante e il relativo stack. Se un processo non riuscito, è importante tooview i dettagli di hello delle attività di processo che non è riuscita per un determinato processo.

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a>toowait per toocomplete di esecuzione un processo
Hello lo script di PowerShell seguente può essere utilizzato toowait per un toocomplete attività processo:

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a>Creare un criterio di esecuzione personalizzata
I processi di database elastici supportano la creazione di criteri di esecuzione personalizzati che possono essere applicati all'avvio dei processi.

Criteri di esecuzione che attualmente consentono la definizione di:

* Nome: Identificatore per i criteri di esecuzione hello.
* Timeout del processo: tempo totale prima che un processo venga annullato dai processi di database elastici.
* Intervallo tra tentativi iniziale: Intervallo toowait prima del primo nuovo tentativo.
* Intervallo tra tentativi massimo: Limite massimo di tentativi intervalli toouse.
* Coefficiente di Backoff intervallo tentativi: Coefficiente utilizzato successivo intervallo hello toocalculate tra i tentativi.  Hello formula seguente viene utilizzata: (intervallo di tentativi iniziale) * Math.pow (intervallo Backoff coefficiente (), (numero di tentativi) - 2). 
* Numero massimo di tentativi: hello massimo di ripetizione tentativi tooperform all'interno di un processo.

criteri di esecuzione predefiniti Hello utilizzano hello seguenti valori:

* Nome: Criterio di esecuzione predefinito
* Timeout del processo: 1 settimana
* Intervallo tra tentativi iniziale: 100 millisecondi
* Intervallo massimo tra tentativi: 30 minuti
* Coefficiente di intervallo tra tentativi: 2
* Numero massimo di tentativi: 2,147,483,647

Creare criteri di esecuzione hello desiderato:

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a>Aggiornare il criterio di esecuzione personalizzato
Aggiornare tooupdate criteri di esecuzione hello desiderato:

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a>Annullare un processo
I processi di database elastici supportano le richieste di annullamento dei processi.  Se i processi di Database elastico rileva una richiesta di annullamento per un processo in fase di esecuzione, verrà eseguito un tentativo con il processo di hello toostop.

E’ possibile cancellare un processo in due modi diversi tramite i processi di database elastici:

1. Annullamento di attività attualmente in esecuzione: se un annullamento viene rilevato durante un'attività è attualmente in esecuzione, verrà tentato un annullamento all'interno di hello aspetto dell'attività hello attualmente in esecuzione.  Ad esempio: se è presente una query a lunga esecuzione viene eseguita quando viene eseguito un tentativo di annullamento, sarà presente una query di hello toocancel tentativo.
2. Annullamento di tentativi dell'attività: se un annullamento viene rilevato dal thread di controllo hello prima di un'attività viene avviata per l'esecuzione, il thread di controllo hello evitare avvio attività hello e dichiarare richiesta hello come annullata.

Se è richiesto un annullamento di processo per un processo padre, la richiesta di annullamento hello sarà rispettata per il processo padre hello e per tutti i relativi processi figlio.

toosubmit una richiesta di annullamento, utilizzare hello [ **cmdlet Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) e set hello **JobExecutionId** parametro.

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a>toodelete un processo e la cronologia dei processi in modo asincrono
I processi di database elastici supportano l'eliminazione asincrona dei processi. Un processo può essere contrassegnato per l'eliminazione e sistema hello eliminerà processo hello e tutta la relativa cronologia processo dopo aver completato tutte le esecuzioni di processo per il processo di hello. sistema Hello non annullerà automaticamente le esecuzioni di processo attivo.  

Richiamare [ **Stop AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel esecuzioni di processo attivo.

l'eliminazione di processo tootrigger, utilizzare hello [ **cmdlet Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) e set hello **JobName** parametro.

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a>toocreate una destinazione di database personalizzati
È possibile definire destinazioni di database personalizzate per l'esecuzione diretta o per l'inclusione in un gruppo di database personalizzato. Ad esempio, in quanto **pool elastici** sono non ancora supportato direttamente tramite APIs di PowerShell, è possibile creare un database personalizzato di destinazione e destinazione della raccolta di database personalizzata che comprende tutti i database nel pool di hello hello.

Impostare le seguenti variabili tooreflect hello desiderato database informazioni hello:

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a>toocreate una destinazione di raccolta di database personalizzati
Hello utilizzare [ **New AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) toodefine cmdlet un'esecuzione di database personalizzato insieme destinazione tooenable tra più destinazioni definita per il database. Dopo aver creato un gruppo di database, database possono essere associati a una destinazione di una raccolta personalizzata hello.

Impostare hello seguente configurazione di destinazione di variabili tooreflect hello raccolta personalizzata desiderata:

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a>destinazione della raccolta tooadd database tooa database personalizzato
una raccolta personalizzata specifica database tooa tooadd utilizzare hello [ **Aggiungi AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Esaminare i database hello all'interno di una destinazione di raccolta di database personalizzati
Hello utilizzare [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) database di cmdlet tooretrieve hello figlio all'interno di una destinazione di raccolta database personalizzato. 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Creare un processo tooexecute uno script per una destinazione di raccolta database personalizzato
Hello utilizzare [ **New AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) toocreate cmdlet un processo rispetto a un gruppo di database definiti da una destinazione di raccolta database personalizzato. I processi di Database elastici espanderà processo hello in più processi figlio, ogni database tooa corrispondente associata alla destinazione di raccolta di database personalizzata hello e assicurarsi che viene eseguito lo script di hello in tutti i database. Nuovamente, è importante che gli script siano idempotenti toobe resilienti tooretries.

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a>Raccolta dei dati tra database
È possibile utilizzare tooexecute un processo una query in un gruppo di database e tabella specifica di hello risultati tooa di trasmissione. è possibile eseguire query di tabella Hello dopo i risultati della query di hello fatti toosee hello da ogni database. In questo modo una query tooexecute un metodo asincrono in numerosi database. I tentativi non riusciti vengono gestiti automaticamente tramite la ripetizione dei tentativi.

tabella di destinazione specificato Hello verrà creata automaticamente se non esiste ancora. nuova tabella Hello corrisponde allo schema di hello di hello restituito set di risultati. Se uno script restituisce più set di risultati, i processi di Database elastico invierà prima tabella di destinazione toohello hello.

Hello seguente script di PowerShell esegue uno script e raccoglie i risultati in una tabella specificata. Questo script presuppone che sia stato creato uno script T-SQL che restituisce un singolo set di risultati e che sia stata creata una destinazione della raccolta di database personalizzata.

Questo script utilizza hello [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet. Impostare i parametri di hello per script, le credenziali e la destinazione di esecuzione:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a>toocreate e avviare un processo per gli scenari di raccolta dati
Questo script utilizza hello [ **inizio AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a>un trigger di processo esecuzione tooschedule
Hello lo script di PowerShell seguente può essere utilizzato toocreate a una pianificazione ricorrente. Questo script usa l'intervallo di minuti, ma [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) supporta anche i parametri -DayInterval, -HourInterval, -MonthInterval e -WeekInterval. Le pianificazioni che vengono eseguite una sola volta possono essere create specificando -OneTime.

Creare una nuova pianificazione:

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a>un processo eseguito su una pianificazione temporale tootrigger
Un trigger di processo può essere definito toohave un processo eseguito in base tooa tempo di pianificazione. Hello lo script di PowerShell seguente può essere utilizzato toocreate un trigger di processo.

Utilizzare [New AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) e set hello seguendo le variabili toocorrespond toohello desiderato processo e pianificazione:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>tooremove un processo toostop associazione pianificata l'esecuzione su pianificazione
esecuzione del processo tramite un trigger di processo, il trigger di processo hello ripresenta toodiscontinue può essere rimosso. Rimuovere un toostop trigger di processo un processo venga eseguito secondo pianificazione tooa utilizzando hello [ **cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a>Recuperare la pianificazione di processo trigger associati tooa ora
Hello lo script di PowerShell seguente può essere utilizzato tooobtain e visualizzare hello processo trigger tooa registrati ora determinata pianificazione.

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a>i trigger di processo tooretrieve associato tooa processo
Utilizzare [Get AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain e la visualizzazione di pianificazioni contenente un processo registrato.

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a>toocreate un'applicazione livello dati (con estensione DACPAC) per l'esecuzione tra database
toocreate un file DACPAC, vedere [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx). un file DACPAC, toodeploy utilizzare hello [cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent). Hello DACPAC deve essere accessibile toohello servizio. È consigliabile tooupload un tooAzure DACPAC creato, archiviazione e creare un [firma di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) per hello DACPAC.

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a>tooupdate un'applicazione livello dati (con estensione DACPAC) per l'esecuzione tra database
Dacpac esistente registrati all'interno di processi di Database elastico può essere aggiornato toopoint toonew URI. Hello utilizzare [ **cmdlet Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello URI DACPAC su un oggetto esistente registrato DACPAC:

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a>toocreate tooapply un processo un'applicazione livello dati (con estensione DACPAC) tra database
Dopo aver creato un file DACPAC all'interno di processi di Database elastico, è possibile creare un processo tooapply hello DACPAC in un gruppo di database. Hello lo script di PowerShell seguente può essere utilizzato toocreate un processo con estensione DACPAC in una raccolta personalizzata di database:

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
