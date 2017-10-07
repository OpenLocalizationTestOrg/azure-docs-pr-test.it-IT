---
title: dati di Twitter con Apache Hive - Azure HDInsight aaaAnalyze | Documenti Microsoft
description: Informazioni su come toouse usano Hive e Hadoop in HDInsight tootransform raw TWitter dati in una tabella Hive ricercabile.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1e249ed-5f57-40d6-b3bc-a1b4d9a871d3
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 02c4d027c7bbf390ac1c3724c14f8d549ea5195e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a>Analizzare i dati di Twitter mediante Hive e Hadoop in HDInsight

Informazioni su come toouse Apache Hive tooprocess dati Twitter. il risultato di Hello è un elenco di utenti di Twitter che ha inviato hello la maggior parte dei TWEET che contengono una determinata parola.

> [!IMPORTANT]
> passaggi di Hello in questo documento sono stati testati su HDInsight 3.6.
>
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="get-hello-data"></a>Ottenere dati hello

Twitter consente hello tooretrieve [dati per ogni tweet](https://dev.twitter.com/docs/platform-objects/tweets) come documento di JavaScript Object Notation (JSON) attraverso un'API REST. [OAuth](http://oauth.net) è necessaria per l'autenticazione toohello API.

### <a name="create-a-twitter-application"></a>Creare un'applicazione Twitter

1. Da un web browser, accesso anche[https://apps.twitter.com/](https://apps.twitter.com/). Fare clic su hello **iscriversi ora** collegare se non si dispone di un account Twitter.

2. Fare clic su **Create New App**.

3. Compilare i campi **Name**, **Description**, **Website**. Si può creare un URL per hello **sito Web** campo. Hello nella tabella seguente mostra alcuni toouse di valori di esempio:

   | Campo | Valore |
   |:--- |:--- |
   | Nome |MyHDInsightApp |
   | Descrizione |MyHDInsightApp |
   | Website |http://www.myhdinsightapp.com |

4. Fare clic su **Yes, I agree** e su **Create your Twitter application**.

5. Fare clic su hello **autorizzazioni** all'autorizzazione predefinita hello scheda **di sola lettura**.

6. Fare clic su hello **chiavi e i token di accesso** scheda.

7. Fare clic su **Create my access token**.

8. Fare clic su **Test OAuth** nell'angolo superiore destro di hello della pagina hello.

9. Compilare i campi **Consumer key**, **Consumer secret**, **Access token** e **Access token secret**.

### <a name="download-tweets"></a>Scaricare tweet

Hello seguente codice Python Scarica 10.000 TWEET da Twitter e salvare i file tooa denominato **tweets.txt**.

> [!NOTE]
> Hello alla procedura seguente viene eseguita nel cluster HDInsight hello, poiché è già installato Python.

1. Connettere il cluster di HDInsight toohello tramite SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Seguente hello utilizzare comandi tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2)e altri pacchetti richiesti:

   ```bash
   sudo apt install python-dev libffi-dev libssl-dev
   sudo apt remove python-openssl
   pip install virtualenv
   mkdir gettweets
   cd gettweets
   virtualenv gettweets
   source gettweets/bin/activate
   pip install tweepy progressbar pyOpenSSL requests[security]
   ```

4. Comando che segue hello utilizzare toocreate un file denominato **gettweets.py**:

   ```bash
   nano gettweets.py
   ```

5. Hello utilizzo successivo di testo come contenuto di hello di hello **gettweets.py** file:

   ```python
   #!/usr/bin/python

   from tweepy import Stream, OAuthHandler
   from tweepy.streaming import StreamListener
   from progressbar import ProgressBar, Percentage, Bar
   import json
   import sys

   #Twitter app information
   consumer_secret='Your consumer secret'
   consumer_key='Your consumer key'
   access_token='Your access token'
   access_token_secret='Your access token secret'

   #hello number of tweets we want tooget
   max_tweets=10000

   #Create hello listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set hello counter toozero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append hello tweet toohello 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment hello number of tweets
               self.num_tweets += 1
               #Check toosee if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment hello progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get hello OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use hello listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > Sostituire il testo segnaposto hello per i seguenti elementi con le informazioni di hello dall'applicazione twitter hello:
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. Utilizzare **Ctrl + X**, quindi **Y** file hello toosave.

7. Utilizzare i seguenti file di comando toorun hello hello e scaricare TWEET:

    ```bash
    python gettweets.py
    ```

    Viene visualizzato un indicatore di stato Considerata too100% hello TWEET vengono scaricati.

   > [!NOTE]
   > Se l'operazione impiega molto tempo per tooadvance barra di stato di avanzamento hello, è necessario modificare gli argomenti relativi alle tendenze di hello filtro tootrack. Quando sono presenti molti TWEET su argomento hello nel filtro, puoi ottenere velocemente hello 10000 TWEET necessari.

### <a name="upload-hello-data"></a>Caricare i dati di hello

tooupload hello tooHDInsight di archiviazione, hello di utilizzare i comandi seguenti:

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

Questi comandi archiviano dati hello in una posizione che possono accedere tutti i nodi nel cluster hello.

## <a name="run-hello-hiveql-job"></a>Eseguire il processo di HiveQL hello

1. Utilizzare hello seguente di un file contenente le istruzioni HiveQL toocreate comando:

   ```bash
   nano twitter.hql
   ```

    Utilizzare hello segue testo come contenuto di hello del file hello:

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward hello tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate hello destination table
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
   -- Select tweets from hello imported data, parse hello JSON,
   -- and insert into hello tweets table
   FROM tweets_raw
   INSERT OVERWRITE TABLE tweets
   SELECT
       cast(get_json_object(json_response, '$.id_str') as BIGINT),
       get_json_object(json_response, '$.created_at'),
       concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
       substr (get_json_object(json_response, '$.created_at'),27,4)),
       substr (get_json_object(json_response, '$.created_at'),27,4),
       case substr (get_json_object(json_response,    '$.created_at'),5,3)
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
   ```

2. Premere **Ctrl + X**, quindi premere **Y** file hello toosave.
3. Utilizzare hello comando toorun hello che hiveql contenute nel file hello seguenti:

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    Questo comando viene eseguito hello hello **twitter.hql** file. Una volta completata la query hello, vedrai un `jdbc:hive2//localhost:10001/>` prompt dei comandi.

4. Dal prompt dei comandi beeline hello, utilizzare hello tooverify query che è stati importati i dati seguenti:

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    Questa query restituisce un massimo di 10 TWEET che contengono la parola hello **Azure** nel testo del messaggio hello.

## <a name="next-steps"></a>Passaggi successivi

Si è appreso come tootransform un set di dati non strutturati JSON in una tabella Hive strutturata. toolearn ulteriori informazioni su Hive in HDInsight, vedere hello seguenti documenti:

* [Introduzione all'uso di HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Analizzare i dati sui ritardi dei voli con HDInsight](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
