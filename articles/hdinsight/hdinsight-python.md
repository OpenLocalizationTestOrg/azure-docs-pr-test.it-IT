---
title: funzione definita dall'utente con Apache Hive e Pig - Azure HDInsight aaaPython | Documenti Microsoft
description: Informazioni su come stack di chiamate toouse Python utente definite funzioni (UDF) dall'Hive e Pig in HDInsight, hello tecnologia di Hadoop su Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 26d8160cc6ed7fc22c3f06f7c1c9954c224b2366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a>Usare le funzioni definite dall'utente di Python (UDF) con Hive e Pig in HDInsight

Informazioni su come toouse Python definito dall'utente (UDF) di funzioni con Apache Hive e Pig in Hadoop in HDInsight di Azure.

## <a name="python"></a>Python in HDInsight

Python 2.7 viene installato per impostazione predefinita in HDInsight 3.0 e versioni successive. Apache Hive può essere usato con questa versione di Python per l'elaborazione di flussi. L'elaborazione di flusso Usa STDOUT e STDIN dati toopass tra Hive e hello funzione definita dall'utente.

HDInsight include anche Jython, un'implementazione di Python scritta in Java. Jython viene eseguito direttamente sulla macchina virtuale Java hello e non utilizzare il flusso. Jython è hello consigliato interprete Python quando si usa Python con Pig.

> [!WARNING]
> passaggi di Hello in questo documento si hello seguenti presupposti: 
>
> * Script Python hello è creare nell'ambiente di sviluppo locale.
> * Caricare tooHDInsight script hello utilizzando entrambi hello `scp` comando da una sessione Bash locale o hello fornito uno script di PowerShell.
>
> Se si desidera hello toouse [Shell di Cloud di Azure (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) anteprima toowork con HDInsight, è necessario:
>
> * Creare script hello all'interno di ambiente della shell hello cloud.
> * Utilizzare `scp` file hello tooupload hello cloud tooHDInsight shell.
> * Utilizzare `ssh` da hello cloud shell tooconnect tooHDInsight ed esempi di esecuzione hello.

## <a name="hivepython"></a>UDF di Hive

Python può essere utilizzato come una funzione definita dall'utente dall'Hive tramite HiveQL hello `TRANSFORM` istruzione. Ad esempio, hello HiveQL seguente richiama hello `hiveudf.py` file archiviato nell'account di archiviazione di Azure hello predefinito per il cluster hello.

**HDInsight basato su Linux**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

**HDInsight basato su Windows**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> Nei cluster HDInsight basati su Windows, hello `USING` clausola deve specificare toopython.exe percorso completo hello.

Ecco cosa fa l'esempio:

1. Hello `add file` istruzione all'inizio di hello del file hello aggiunge hello `hiveudf.py` toohello file distribuito cache, in modo che sia accessibile da tutti i nodi nel cluster hello.
2. Hello `SELECT TRANSFORM ... USING` istruzione vengono selezionati dati hello `hivesampletable`. Passa inoltre clientid hello e devicemake devicemodel valori toohello `hiveudf.py` script.
3. Hello `AS` clausola descrive campi hello restituiti da `hiveudf.py`.

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a>Creare file hiveudf.py hello


Nell'ambiente di sviluppo creare un file di testo denominato `hiveudf.py`. Utilizzare hello seguente di codice come contenuto di hello del file hello:

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

Questo script esegue hello seguenti azioni:

1. Leggere una riga di dati da STDIN.
2. Hello carattere di nuova riga finale viene rimosso mediante `string.strip(line, "\n ")`.
3. Quando si esegue l'elaborazione del flusso, una singola riga contiene tutti i valori hello con un carattere di tabulazione tra ogni valore. Pertanto, `string.split(line, "\t")` può essere utilizzato toosplit hello l'input in ogni scheda, restituendo solo i campi di hello.
4. Una volta completata l'elaborazione, è possibile che l'output di hello deve scritto tooSTDOUT come una singola riga, con una scheda tra ogni campo. ad esempio `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.
5. Hello `while` ciclo si ripete fino a quando non `line` è di lettura.

output di Hello dello script è una concatenazione di valori di input per hello `devicemake` e `devicemodel`, e un hash di hello valore concatenato.

Vedere [esecuzione esempi hello](#running) come toorun in questo esempio il cluster HDInsight.

## <a name="pigpython"></a>UDF di Pig

Script Python può essere utilizzato come una funzione definita dall'utente da Pig tramite hello `GENERATE` istruzione. È possibile eseguire script hello utilizzando Jython o Python C.

* Jython viene eseguito su hello JVM e può essere chiamato in modo nativo da Pig.
* C Python è un processo esterno, pertanto dati hello Pig in hello JVM viene inviato toohello script in esecuzione in un processo di Python. output di Hello di script Python hello viene inviato nuovamente nel Pig.

interprete Python di hello toospecify, utilizzare `register` quando si fa riferimento a script Python hello. Hello negli esempi seguenti registrarsi script Pig come `myfuncs`:

* **toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`
* **toouse Python C**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`

> [!IMPORTANT]
> Quando si utilizza Jython, hello percorso toohello pig_jython file può essere un percorso locale o un WASB: / / percorso. Tuttavia, quando si usa Python C, è necessario fare riferimento un file hello file System locale del nodo hello che si sta utilizzando un processo Pig di hello toosubmit.

Una volta dopo la registrazione, hello latino Pig per questo esempio hello stesso per entrambi:

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

Ecco cosa fa l'esempio:

1. Hello prima riga Carica file di dati di esempio hello, `sample.log` in `LOGS`. Definisce anche ogni record come `chararray`.
2. riga successiva Hello esclude tramite filtro i valori null, archiviando hello risultato dell'operazione di hello in `LOG`.
3. Successivamente, scorre record hello `LOG` e utilizza `GENERATE` tooinvoke hello `create_structure` metodo contenuto nello script Python/Jython hello caricato come `myfuncs`. `LINE`viene utilizzato toopass funzione toohello record corrente hello.
4. Infine, gli output di hello sono tooSTDOUT dumping tramite hello `DUMP` comando. Questo comando Visualizza i risultati di hello al termine dell'operazione di hello.

### <a name="create-hello-pigudfpy-file"></a>Creare file pigudf.py hello

Nell'ambiente di sviluppo creare un file di testo denominato `pigudf.py`. Utilizzare hello seguente di codice come contenuto di hello del file hello:

<a name="streamingpy"></a>

```python
# Uncomment hello following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

Nell'esempio Pig latino hello è definito hello `LINE` di input come un chararray perché nessuno schema coerente per l'input hello. Hello script Python Trasforma dati hello in uno schema coerente per l'output.

1. Hello `@outputSchema` istruzione definisce il formato di hello dei dati di hello restituito tooPig. In questo caso si tratta di un **contenitore di dati**, ovvero un tipo di dati Pig. contenitore Hello contiene hello seguenti campi, ognuno dei quali sono chararray (stringhe):

   * Data - hello data hello voce del log è stata creata
   * ora - hello voce di log hello è stato creato
   * ClassName - voce hello nome di classe hello è stato creato per
   * livello - hello log
   * voce di log dettagliate per hello - dettagli

2. Successivamente, hello `def create_structure(input)` definisce una funzione hello Pig passa voci.

3. dati di esempio, Hello `sample.log`, principalmente toohello data, ora, NomeClasse, livello, è conforme e schema desideriamo tooreturn in dettaglio. Contengono tuttavia alcune righe che iniziano con `*java.lang.Exception*`. Queste righe devono essere schema hello toomatch modificato. Hello `if` istruzione verifica la presenza di quelli quindi terapeutici hello hello toomove dati di input `*java.lang.Exception*` fine toohello stringa, riportare hello dati in linea con il nostro schema output previsto.

4. Successivamente, hello `split` comando è utilizzati toosplit hello dati hello prima quattro spazi. output di Hello viene assegnato in `date`, `time`, `classname`, `level`, e `detail`.

5. Infine, i valori hello vengono restituiti tooPig.

Quando vengono restituiti i dati di hello tooPig ha uno schema coerente, come definito in hello `@outputSchema` istruzione.

## <a name="running"></a>Caricare ed eseguire gli esempi di hello

> [!IMPORTANT]
> Hello **SSH** procedura funziona solo con un cluster HDInsight basati su Linux. Hello **PowerShell** passaggi lavorare con i cluster HDInsight basati su Windows o Linux, ma richiede un client di Windows.

### <a name="ssh"></a>SSH

Per altre informazioni sull'uso di SSH, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

1. Utilizzare `scp` cluster di HDInsight tooyour file hello toocopy. Ad esempio, hello comando copie hello cluster tooa file denominato seguente **mycluster**.

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. Usare SSH tooconnect toohello cluster.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. Dalla sessione SSH hello, aggiungere i file di python hello caricato precedentemente archiviazione WASB toohello per cluster hello.

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

Dopo aver caricato il file hello, seguente hello utilizzare passaggi toorun hello Hive e processi Pig.

#### <a name="use-hello-hive-udf"></a>Utilizzare hello Hive definita dall'utente

1. Hello utilizzare `hive` toostart hello hive shell dei comandi. Verrà visualizzato un `hive>` richiedere una volta caricate shell hello.

2. Immettere hello seguente query hello `hive>` prompt dei comandi:

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. Dopo aver immesso l'ultima riga hello, deve iniziare il processo di hello. Al termine del processo di hello, verrà restituito toohello simili di output esempio seguente:

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a>Utilizzare hello Pig funzione definita dall'utente

1. Hello utilizzare `pig` toostart hello shell dei comandi. Viene visualizzato un `grunt>` richiedere una volta caricate shell hello.

2. Immettere hello seguendo le istruzioni nel hello `grunt>` prompt dei comandi:

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. Dopo aver immesso hello successiva riga, deve iniziare il processo di hello. Al termine del processo di hello, verrà restituito toohello simili di output dati seguenti:

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. Utilizzare `quit` tooexit hello shell Grunt e quindi utilizzare hello seguenti tooedit hello pigudf.py file hello file System locale:

    ```bash
    nano pigudf.py
    ```

5. Una volta nell'editor di hello, rimuovere il commento hello successiva riga rimuovendo hello `#` caratteri dall'inizio di hello della riga hello:

    ```bash
    #from pig_util import outputSchema
    ```

    Una volta effettuato modifica hello, utilizzare l'editor di hello tooexit Ctrl + X. Selezionare Y e quindi immettere toosave hello modifiche.

6. Hello utilizzare `pig` toostart hello shell dei comandi nuovamente. Una volta visualizzato hello `grunt>` prompt, usare lo script Python di hello toorun usando interprete Python C hello seguente hello.

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    Dopo aver completato questo processo, dovrebbe essere stesso output di hello come quando è stato precedentemente eseguito script hello utilizzando Jython.

### <a name="powershell-upload-hello-files"></a>PowerShell: Caricare i file di hello

È possibile utilizzare PowerShell tooupload hello file toohello HDInsight per il server. Utilizzare i seguenti file di script tooupload hello Python hello:

> [!IMPORTANT] 
> passaggi di Hello in questa sezione utilizzano Azure PowerShell. Per ulteriori informazioni sull'utilizzo di Azure PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
# Change hello path toomatch hello file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

Set-AzureStorageBlobContent `
    -File $pathToStreamingFile `
    -Blob "hiveudf.py" `
    -Container $container `
    -Context $context

Set-AzureStorageBlobContent `
    -File $pathToJythonFile `
    -Blob "pigudf.py" `
    -Container $container `
    -Context $context
```
> [!IMPORTANT]
> Hello modifica `C:\path\to` toohello percorso toohello file nell'ambiente di sviluppo di valore.

Questo script recupera le informazioni per il cluster HDInsight, quindi estrae account hello e una chiave per l'account di archiviazione predefinito hello e caricamenti hello radice toohello file contenitore hello.

> [!NOTE]
> Per ulteriori informazioni sul caricamento di file, vedere hello [caricare dati per i processi di Hadoop in HDInsight](hdinsight-upload-data.md) documento.

#### <a name="powershell-use-hello-hive-udf"></a>PowerShell: Utilizzo hello Hive definita dall'utente

PowerShell può essere anche le query Hive tooremotely utilizzati eseguire. Hello utilizzare seguente script di PowerShell toorun una query Hive che utilizza **hiveudf.py** script:

> [!IMPORTANT]
> Prima dell'esecuzione, script hello chiede hello HTTPs/Admin informazioni dell'account per il cluster HDInsight.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

# If using a Windows-based HDInsight cluster, change hello USING statement to:
# "USING 'D:\Python27\python.exe hiveudf.py' AS " +
$HiveQuery = "add file wasb:///hiveudf.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python hiveudf.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for hello Hive job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

output di hello Hello **Hive** processo compariranno simile toohello esempio seguente:

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a>Pig (Jython)

PowerShell può essere anche usato toorun latino Pig processi. un processo Pig latino che utilizza hello toorun **pigudf.py** script, utilizzare hello lo script di PowerShell seguente:

> [!NOTE]
> Quando si inviano in remoto un processo tramite PowerShell, non è possibile toouse Python C come interprete hello.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

$PigQuery = "Register wasb:///pigudf.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for hello Pig job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

output di hello Hello **Pig** processo compariranno simile toohello dati seguenti:

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="errors-when-running-jobs"></a>Errori durante l'esecuzione di processi

Quando si esegue il processo di hive hello, è possibile riscontrare un toohello simile di errore seguente testo:

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

Questo problema può essere causato da file Python hello terminazioni di riga hello. Molti editor di Windows predefinito toousing CR/LF come terminazione di riga hello, ma le applicazioni Linux prevedono in genere LF.

È possibile utilizzare i caratteri di hello CR tooremove di PowerShell istruzioni prima di caricare tooHDInsight file hello hello:

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a>Script di PowerShell

Entrambi hello esempio gli script di PowerShell utilizzati esempi hello toorun contiene una riga di commento che viene visualizzato l'output di errore per il processo di hello. Se non viene visualizzato l'output di hello previsto per il processo di hello, rimuovere il commento seguente hello di riga e visualizzare informazioni sull'errore hello indica un problema relativo.

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

informazioni sull'errore Hello (STDERR) e il risultato di hello del processo di hello (STDOUT) vengono anche registrati tooyour HDInsight archiviazione.

| Processo | Esaminare questi file nel contenitore blob hello |
| --- | --- |
| Hive |/HivePython/stderr<p>/HivePython/stdout |
| Pig |/PigPython/stderr<p>/PigPython/stdout |

## <a name="next"></a>Passaggi successivi

Se è necessario moduli Python tooload che non sono disponibili per impostazione predefinita, vedere [come toodeploy tooAzure un modulo HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).

Per altri modi toouse Pig, Hive e toolearn sull'utilizzo di MapReduce, vedere hello seguenti documenti:

* [Usare Hive con HDInsight](hdinsight-use-hive.md)
* [Usare Pig con HDInsight](hdinsight-use-pig.md)
* [Usare MapReduce con HDInsight](hdinsight-use-mapreduce.md)
