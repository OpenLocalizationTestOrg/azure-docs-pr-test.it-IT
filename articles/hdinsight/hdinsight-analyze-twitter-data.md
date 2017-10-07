---
title: dati di Twitter con Hadoop in HDInsight - Azure aaaAnalyze | Documenti Microsoft
description: Informazioni su come toouse Hive tooanalyze Twitter dei dati in Hadoop in HDInsight toofind hello frequenza di utilizzo di una determinata parola.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a>Analizzare i dati di Twitter con Hive in HDInsight
Siti Web sociali sono uno dei hello principali le forze per l'adozione dei big data. Le API pubbliche offerte da siti quali Twitter costituiscono un'utile origine di dati per l'analisi e la comprensione delle tendenze più popolari.
In questa esercitazione consente di ottenere TWEET utilizzando un Twitter streaming API e di utilizzare Apache Hive in Azure HDInsight tooget un elenco di utenti di Twitter che ha inviato hello TWEET la maggior parte dei contenuti di una determinata parola.

> [!IMPORTANT]
> Hello passaggi in questo documento richiedono un cluster HDInsight basati su Windows. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Per cluster basati su Linux tooa specifica di passaggi, vedere [dati analizzare Twitter usando Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:

* **Una workstation** in cui sia stato installato e configurato Azure PowerShell.

    script di Windows PowerShell tooexecute, è necessario eseguire Azure PowerShell come amministratore e impostare i criteri di esecuzione hello troppo*RemoteSigned*. Vedere [Run Windows PowerShell scripts][powershell-script] (Eseguire script di Windows PowerShell).

    Prima di eseguire script di Windows PowerShell, verificare di disporre connesso tooyour sottoscrizione di Azure tramite hello seguente cmdlet:

    ```powershell
    Login-AzureRmAccount
    ```

    Se si dispone di più sottoscrizioni di Azure, utilizzare hello sottoscrizione corrente hello tooset di cmdlet seguenti:

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** ed è stato rimosso dal 1° gennaio 2017. Hello passaggi in questo documento usa hello nuovi cmdlet di HDInsight che funzionano con Gestione risorse di Azure.
    >
    > Eseguire le operazioni di hello in [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello più recente di Azure PowerShell. Se si dispone di script che toobe necessità modificato toouse hello nuovi cmdlet che funzionano con Gestione risorse di Azure, vedere [di strumenti di migrazione tooAzure sviluppo basato su Gestione risorse per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) per ulteriori informazioni.

* **Un cluster HDInsight di Azure**. Per istruzioni sul provisioning del cluster, vedere [Introduzione a HDInsight][hdinsight-get-started] o [Effettuare il provisioning di cluster HDInsight][hdinsight-provision]. Nome del cluster hello sarà necessario più avanti nell'esercitazione di hello.

Hello nella tabella seguente sono elencati i file hello utilizzati in questa esercitazione:

| File | Descrizione |
| --- | --- |
| /tutorials/twitter/data/tweets.txt |dati di origine Hello per processo Hive hello. |
| /tutorials/twitter/output |cartella di output di Hello per processo Hive hello. Hello Hive processo output nome file predefinito è **000000_0**. |
| tutorials/twitter/twitter.hql |file di script HiveQL Hello. |
| /tutorials/twitter/jobstatus |lo stato del processo Hadoop Hello. |

## <a name="get-twitter-feed"></a>Ricezione di feed Twitter
In questa esercitazione si utilizzerà hello [Twitter API di flusso][twitter-streaming-api]. è Hello Twitter specifico streaming API si utilizzerà [stati/filtro][twitter-statuses-filter].

> [!NOTE]
> Un file contenente 10.000 TWEET e file di script Hive hello (descritta nella sezione successiva hello) sono stati caricati in un contenitore di Blob pubblico. È possibile ignorare questa sezione se si desidera toouse hello caricamento file.

[TWEET dati](https://dev.twitter.com/docs/platform-objects/tweets) viene archiviato in formato JavaScript Object Notation (JSON) hello che contiene una struttura nidificata complessa. Invece di scrivere molte righe di codice usando un linguaggio di programmazione convenzionale, è possibile trasformare la struttura annidata in una tabella Hive, in modo da consentire l'esecuzione di query tramite un linguaggio analogo a SQL ( Structured Query Language), denominato HiveQL.

Twitter utilizza OAuth tooprovide autorizzato accesso tooits API. OAuth è un protocollo di autenticazione che consente agli utenti tooapprove applicazioni tooact per conto del cliente senza condividere la propria password. Altre informazioni sono reperibile in [oauth.net](http://oauth.net/) o hello eccellente [tooOAuth Guida per principianti](http://hueniverse.com/oauth/) da Hueniverse.

Hello primo passaggio toouse OAuth è toocreate una nuova applicazione nel sito per sviluppatori di Twitter hello.

**toocreate un'applicazione di Twitter**

1. Accedi troppo[https://apps.twitter.com/](https://apps.twitter.com/). Fare clic su hello **Iscriviti ora** collegare se non si dispone di un account Twitter.
2. Fare clic su **Create New App**.
3. Compilare i campi **Name**, **Description**, **Website**. Si può creare un URL per hello **sito Web** campo. Hello nella tabella seguente mostra alcuni toouse di valori di esempio:

   | Campo | Valore |
   | --- | --- |
   |  Nome |MyHDInsightApp |
   |  Descrizione |MyHDInsightApp |
   |  Website |http://www.myhdinsightapp.com |
4. Fare clic su **Yes, I agree** e su **Create your Twitter application**.
5. Fare clic su hello **autorizzazioni** all'autorizzazione predefinita hello scheda **di sola lettura**. Questo livello di autorizzazione è sufficiente per l'esercitazione.
6. Fare clic su hello **chiavi e i token di accesso** scheda.
7. Fare clic su **Create my access token**.
8. Fare clic su **Test OAuth** nell'angolo superiore destro di hello della pagina hello.
9. Compilare i campi **Consumer key**, **Consumer secret**, **Access token** e **Access token secret**. I valori hello sarà necessario più avanti nell'esercitazione di hello.

In questa esercitazione si utilizzerà chiamata del servizio web di Windows PowerShell toomake hello. Per un esempio di .NET C#, vedere [Analizzare i sentiment di Twitter in tempo reale con HBase in HDInsight][hdinsight-hbase-twitter-sentiment]. è Hello altre chiamate al servizio web toomake strumento comune [ *Curl*][curl]. Curl può essere scaricato da [questa pagina][curl-download].

> [!NOTE]
> Quando si utilizza il comando di curl hello in Windows, utilizzare le virgolette doppie anziché le virgolette singole per i valori di opzione hello.

**tooget tweets**

1. Aprire Windows PowerShell Integrated Scripting Environment (ISE) hello. (Nella schermata iniziale di Windows 8 hello digitare **PowerShell_ISE** e quindi fare clic su **Windows PowerShell ISE**. Vedere [Start Windows PowerShell on Windows 8 and Windows][powershell-start] (Avviare Windows PowerShell in Windows 8 e Windows).
2. Copiare lo script seguente nel riquadro di script hello hello:

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Impostare le variabili tooeight primi cinque hello nello script hello:

    Variabile|Descrizione
    ---|---
    $clusterName|Questo è il nome di hello del cluster HDInsight hello in cui si desidera un'applicazione hello toorun.
    $oauth_consumer_key|Si tratta di un'applicazione hello Twitter **chiave consumer** annotato in precedenza durante la creazione di un'applicazione hello Twitter.
    $oauth_consumer_secret|Si tratta di un'applicazione hello Twitter **segreto del cliente** annotato in precedenza.
    $oauth_token|Si tratta di un'applicazione hello Twitter **token di accesso** annotato in precedenza.
    $oauth_token_secret|Si tratta di un'applicazione hello Twitter **segreto del token di accesso** annotato in precedenza.
    $destBlobName|Si tratta di nome di blob di output di hello. valore predefinito di Hello è **tutorials/twitter/data/tweets.txt**. Se si modifica il valore di predefinito hello, è necessario pertanto gli script di Windows PowerShell hello tooupdate.
    $trackString|servizio web Hello restituirà le parole chiave correlate toothese TWEET. valore predefinito di Hello è **HDInsight di Azure, Cloud,**. Se si modifica il valore di predefinito hello, sarà necessario aggiornare gli script di PowerShell di Windows hello conseguenza.
    $lineMax|il valore di Hello determina quanti TWEET hello script leggerà. Sono necessari circa tre minuti tooread 100 TWEET. È possibile impostare un numero maggiore, ma richiederà più toodownload ora.

1. Premere **F5** script hello toorun. Se si verificano problemi, in alternativa, selezionare tutte le righe hello e quindi premere **F8**.
2. Alla fine dell'output verrà visualizzato alla fine di hello dell'output di hello. Eventuali messaggi di errore verranno visualizzati in rosso.

Come procedura di convalida, è possibile controllare il file di output di hello, **/tutorials/twitter/data/tweets.txt**, alla risorsa di archiviazione Blob di Azure usando un Esplora archivi Azure o Azure PowerShell. Per uno script di Windows PowerShell di esempio per l'elenco dei file, vedere [Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage-powershell].

## <a name="create-hiveql-script"></a>Creare uno script HiveQL
Con Azure PowerShell, è possibile eseguire più istruzioni HiveQL uno alla volta oppure hello pacchetto HiveQL istruzione in un file di script. In questa esercitazione verrà creato uno script HiveQL. file di script Hello deve essere tooAzure caricato nell'archiviazione Blob. Nella sezione successiva hello, si eseguirà il file di script hello tramite Azure PowerShell.

> [!NOTE]
> file di script Hive Hello e un file contenente 10.000 TWEET sono stati caricati in un contenitore di Blob pubblico. È possibile ignorare questa sezione se si desidera toouse hello caricamento file.

Hello script HiveQL eseguirà seguente hello:

1. **Elimina tabella tweets_raw hello** nel caso in cui hello tabella esiste già.
2. **Creare una tabella Hive di hello tweets_raw**. Questa tabella strutturata Hive temporanea contiene i dati di hello per ulteriormente estrarre, trasformare e caricare l'elaborazione (ETL). Per informazioni sulle partizioni, vedere [Hive tutorial][apache-hive-tutorial] (Esercitazione su Hive).
3. **Caricare i dati** dalla cartella di origine hello, /tutorials/twitter/data. Hello TWEET grandi set di dati in formato JSON nidificato a questo punto è stata trasformata in una struttura di tabella temporanea Hive.
4. **Eliminazione hello TWEET tabella** nel caso in cui hello tabella esiste già.
5. **Creare una tabella TWEET hello**. È possibile eseguire una query sul set di dati TWEET hello utilizzando Hive, è necessario toorun un altro processo ETL. Questo processo ETL definisce uno schema di tabella più dettagliato per i dati archiviati nella tabella "twitter_raw" hello hello.
6. **Inserire la tabella di sovrascrittura**. Questo script Hive complesso provoca un set di processi MapReduce lungo da un cluster Hadoop hello. A seconda del set di dati e hello delle dimensioni del cluster, l'operazione potrebbe richiedere circa 10 minuti.
7. **Inserire la directory di sovrascrittura**. Eseguire una query e output hello dataset tooa un file. Questa query restituirà un elenco di utenti di Twitter che ha inviato la maggior parte dei TWEET contenenti la parola hello "Azure".

**un Hive toocreate script e caricarlo tooAzure**

1. Aprire Windows PowerShell ISE.
2. Copiare lo script seguente nel riquadro di script hello hello:

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Impostare hello innanzitutto due variabili nello script hello:

   | Variabile | Descrizione |
   | --- | --- |
   |  $clusterName |Immettere nome del cluster HDInsight hello in cui si desidera un'applicazione hello toorun. |
   |  $subscriptionID |Inserire L'ID della sottoscrizione di Azure. |
   |  $sourceDataPath |percorso di archiviazione Blob di Azure in cui le query Hive hello verranno leggere i dati hello Hello. Non è necessario toochange questa variabile. |
   |  $outputPath |percorso di archiviazione Blob di Azure in cui le query Hive hello fornirà risultati hello Hello. Non è necessario toochange questa variabile. |
   |  $hqlScriptFile |percorso di Hello e il nome di file hello hello HiveQL del file di script. Non è necessario toochange questa variabile. |
4. Premere **F5** script hello toorun. Se si verificano problemi, in alternativa, selezionare tutte le righe hello e quindi premere **F8**.
5. Alla fine dell'output verrà visualizzato alla fine di hello dell'output di hello. Eventuali messaggi di errore verranno visualizzati in rosso.

Come procedura di convalida, è possibile controllare il file di output di hello, **/tutorials/twitter/twitter.hql**, alla risorsa di archiviazione Blob di Azure usando un Esplora archivi Azure o Azure PowerShell. Per uno script di Windows PowerShell di esempio per l'elenco dei file, vedere [Usare l'archivio BLOB di Azure con HDInsight][hdinsight-storage-powershell].

## <a name="process-twitter-data-by-using-hive"></a>Elaborare i dati di Twitter tramite Hive
Tutte le operazioni di preparazione hello completata. A questo punto, è possibile richiamare script Hive hello e controllare i risultati di hello.

### <a name="submit-a-hive-job"></a>Inviare un processo Hive
Utilizzare lo script Hive di Windows PowerShell script toorun hello seguente hello. È necessario prima variabile di tooset hello.

> [!NOTE]
> hello toouse TWEET e script HiveQL caricato hello ultime due sezioni, set $hqlScriptFile too"/tutorials/twitter/twitter.hql hello". hello toouse quelli che sono stati caricati blob pubblici tooa, impostare $hqlScriptFile troppo"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a>Controllare i risultati di hello
Utilizzare hello seguente hello toocheck di Windows PowerShell script Hive output del processo. È necessario innanzitutto due variabili di tooset hello.

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> tabella Hive Hello utilizza \001 come hello delimitatore di campo. delimitatore di Hello non è visibile nell'output di hello.

Dopo che i risultati dell'analisi hello vengono inseriti nell'archiviazione Blob di Azure, è possibile esportare hello dati tooan Azure SQL database di SQL server, esportare hello dati tooExcel tramite Power Query o la connessione dati toohello dell'applicazione utilizzando hello Hive Driver ODBC. Per ulteriori informazioni, vedere [utilizzare Sqoop con HDInsight][hdinsight-use-sqoop], [analizza i dati di ritardo di volo con HDInsight][hdinsight-analyze-flight-delay-data], [ Connettere Excel tooHDInsight con Power Query][hdinsight-power-query], e [tooHDInsight connessione Excel con il Driver ODBC di Hive Microsoft hello][hdinsight-hive-odbc].

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione abbiamo visto come tootransform un set di dati non strutturati JSON in un tooquery di tabella Hive strutturata, esplorare e analizzare i dati da Twitter usando HDInsight in Azure. toolearn informazioni, vedere:

* [Introduzione a HDInsight][hdinsight-get-started]
* [Analizzare i sentimenti Twitter in tempo reale con HBase in HDInsight][hdinsight-hbase-twitter-sentiment]
* [Analizzare i dati sui ritardi dei voli con HDInsight][hdinsight-analyze-flight-delay-data]
* [Connettere Excel tooHDInsight con Power Query][hdinsight-power-query]
* [Connettere Excel tooHDInsight con il Driver ODBC di Hive Microsoft hello][hdinsight-hive-odbc]
* [Usare Sqoop con Hadoop in HDInsight][hdinsight-use-sqoop]

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
