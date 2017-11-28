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
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a><span data-ttu-id="794db-103">Analizzare i dati di Twitter mediante Hive e Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="794db-103">Analyze Twitter data using Hive and Hadoop on HDInsight</span></span>

<span data-ttu-id="794db-104">Informazioni su come toouse Apache Hive tooprocess dati Twitter.</span><span class="sxs-lookup"><span data-stu-id="794db-104">Learn how toouse Apache Hive tooprocess Twitter data.</span></span> <span data-ttu-id="794db-105">il risultato di Hello è un elenco di utenti di Twitter che ha inviato hello la maggior parte dei TWEET che contengono una determinata parola.</span><span class="sxs-lookup"><span data-stu-id="794db-105">hello result is a list of Twitter users who sent hello most tweets that contain a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="794db-106">passaggi di Hello in questo documento sono stati testati su HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="794db-106">hello steps in this document were tested on HDInsight 3.6.</span></span>
>
> <span data-ttu-id="794db-107">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="794db-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="794db-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="794db-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="get-hello-data"></a><span data-ttu-id="794db-109">Ottenere dati hello</span><span class="sxs-lookup"><span data-stu-id="794db-109">Get hello data</span></span>

<span data-ttu-id="794db-110">Twitter consente hello tooretrieve [dati per ogni tweet](https://dev.twitter.com/docs/platform-objects/tweets) come documento di JavaScript Object Notation (JSON) attraverso un'API REST.</span><span class="sxs-lookup"><span data-stu-id="794db-110">Twitter allows you tooretrieve hello [data for each tweet](https://dev.twitter.com/docs/platform-objects/tweets) as a JavaScript Object Notation (JSON) document through a REST API.</span></span> <span data-ttu-id="794db-111">[OAuth](http://oauth.net) è necessaria per l'autenticazione toohello API.</span><span class="sxs-lookup"><span data-stu-id="794db-111">[OAuth](http://oauth.net) is required for authentication toohello API.</span></span>

### <a name="create-a-twitter-application"></a><span data-ttu-id="794db-112">Creare un'applicazione Twitter</span><span class="sxs-lookup"><span data-stu-id="794db-112">Create a Twitter application</span></span>

1. <span data-ttu-id="794db-113">Da un web browser, accesso anche[https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="794db-113">From a web browser, sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="794db-114">Fare clic su hello **iscriversi ora** collegare se non si dispone di un account Twitter.</span><span class="sxs-lookup"><span data-stu-id="794db-114">Click hello **Sign-up now** link if you don't have a Twitter account.</span></span>

2. <span data-ttu-id="794db-115">Fare clic su **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="794db-115">Click **Create New App**.</span></span>

3. <span data-ttu-id="794db-116">Compilare i campi **Name**, **Description**, **Website**.</span><span class="sxs-lookup"><span data-stu-id="794db-116">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="794db-117">Si può creare un URL per hello **sito Web** campo.</span><span class="sxs-lookup"><span data-stu-id="794db-117">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="794db-118">Hello nella tabella seguente mostra alcuni toouse di valori di esempio:</span><span class="sxs-lookup"><span data-stu-id="794db-118">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="794db-119">Campo</span><span class="sxs-lookup"><span data-stu-id="794db-119">Field</span></span> | <span data-ttu-id="794db-120">Valore</span><span class="sxs-lookup"><span data-stu-id="794db-120">Value</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="794db-121">Nome</span><span class="sxs-lookup"><span data-stu-id="794db-121">Name</span></span> |<span data-ttu-id="794db-122">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="794db-122">MyHDInsightApp</span></span> |
   | <span data-ttu-id="794db-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="794db-123">Description</span></span> |<span data-ttu-id="794db-124">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="794db-124">MyHDInsightApp</span></span> |
   | <span data-ttu-id="794db-125">Website</span><span class="sxs-lookup"><span data-stu-id="794db-125">Website</span></span> |<span data-ttu-id="794db-126">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="794db-126">http://www.myhdinsightapp.com</span></span> |

4. <span data-ttu-id="794db-127">Fare clic su **Yes, I agree** e su **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="794db-127">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>

5. <span data-ttu-id="794db-128">Fare clic su hello **autorizzazioni** all'autorizzazione predefinita hello scheda **di sola lettura**.</span><span class="sxs-lookup"><span data-stu-id="794db-128">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span>

6. <span data-ttu-id="794db-129">Fare clic su hello **chiavi e i token di accesso** scheda.</span><span class="sxs-lookup"><span data-stu-id="794db-129">Click hello **Keys and Access Tokens** tab.</span></span>

7. <span data-ttu-id="794db-130">Fare clic su **Create my access token**.</span><span class="sxs-lookup"><span data-stu-id="794db-130">Click **Create my access token**.</span></span>

8. <span data-ttu-id="794db-131">Fare clic su **Test OAuth** nell'angolo superiore destro di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="794db-131">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>

9. <span data-ttu-id="794db-132">Compilare i campi **Consumer key**, **Consumer secret**, **Access token** e **Access token secret**.</span><span class="sxs-lookup"><span data-stu-id="794db-132">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span>

### <a name="download-tweets"></a><span data-ttu-id="794db-133">Scaricare tweet</span><span class="sxs-lookup"><span data-stu-id="794db-133">Download tweets</span></span>

<span data-ttu-id="794db-134">Hello seguente codice Python Scarica 10.000 TWEET da Twitter e salvare i file tooa denominato **tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="794db-134">hello following Python code downloads 10,000 tweets from Twitter and save them tooa file named **tweets.txt**.</span></span>

> [!NOTE]
> <span data-ttu-id="794db-135">Hello alla procedura seguente viene eseguita nel cluster HDInsight hello, poiché è già installato Python.</span><span class="sxs-lookup"><span data-stu-id="794db-135">hello following steps are performed on hello HDInsight cluster, since Python is already installed.</span></span>

1. <span data-ttu-id="794db-136">Connettere il cluster di HDInsight toohello tramite SSH:</span><span class="sxs-lookup"><span data-stu-id="794db-136">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="794db-137">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="794db-137">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="794db-138">Seguente hello utilizzare comandi tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2)e altri pacchetti richiesti:</span><span class="sxs-lookup"><span data-stu-id="794db-138">Use hello following commands tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2), and other required packages:</span></span>

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

4. <span data-ttu-id="794db-139">Comando che segue hello utilizzare toocreate un file denominato **gettweets.py**:</span><span class="sxs-lookup"><span data-stu-id="794db-139">Use hello following command toocreate a file named **gettweets.py**:</span></span>

   ```bash
   nano gettweets.py
   ```

5. <span data-ttu-id="794db-140">Hello utilizzo successivo di testo come contenuto di hello di hello **gettweets.py** file:</span><span class="sxs-lookup"><span data-stu-id="794db-140">Use hello following text as hello contents of hello **gettweets.py** file:</span></span>

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
    > <span data-ttu-id="794db-141">Sostituire il testo segnaposto hello per i seguenti elementi con le informazioni di hello dall'applicazione twitter hello:</span><span class="sxs-lookup"><span data-stu-id="794db-141">Replace hello placeholder text for hello following items with hello information from your twitter application:</span></span>
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. <span data-ttu-id="794db-142">Utilizzare **Ctrl + X**, quindi **Y** file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="794db-142">Use **Ctrl + X**, then **Y** toosave hello file.</span></span>

7. <span data-ttu-id="794db-143">Utilizzare i seguenti file di comando toorun hello hello e scaricare TWEET:</span><span class="sxs-lookup"><span data-stu-id="794db-143">Use hello following command toorun hello file and download tweets:</span></span>

    ```bash
    python gettweets.py
    ```

    <span data-ttu-id="794db-144">Viene visualizzato un indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="794db-144">A progress indicator appears.</span></span> <span data-ttu-id="794db-145">Considerata too100% hello TWEET vengono scaricati.</span><span class="sxs-lookup"><span data-stu-id="794db-145">It counts up too100% as hello tweets are downloaded.</span></span>

   > [!NOTE]
   > <span data-ttu-id="794db-146">Se l'operazione impiega molto tempo per tooadvance barra di stato di avanzamento hello, è necessario modificare gli argomenti relativi alle tendenze di hello filtro tootrack.</span><span class="sxs-lookup"><span data-stu-id="794db-146">If it is taking a long time for hello progress bar tooadvance, you should change hello filter tootrack trending topics.</span></span> <span data-ttu-id="794db-147">Quando sono presenti molti TWEET su argomento hello nel filtro, puoi ottenere velocemente hello 10000 TWEET necessari.</span><span class="sxs-lookup"><span data-stu-id="794db-147">When there are many tweets about hello topic in your filter, you can quickly get hello 10000 tweets needed.</span></span>

### <a name="upload-hello-data"></a><span data-ttu-id="794db-148">Caricare i dati di hello</span><span class="sxs-lookup"><span data-stu-id="794db-148">Upload hello data</span></span>

<span data-ttu-id="794db-149">tooupload hello tooHDInsight di archiviazione, hello di utilizzare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="794db-149">tooupload hello data tooHDInsight storage, use hello following commands:</span></span>

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

<span data-ttu-id="794db-150">Questi comandi archiviano dati hello in una posizione che possono accedere tutti i nodi nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="794db-150">These commands store hello data in a location that all nodes in hello cluster can access.</span></span>

## <a name="run-hello-hiveql-job"></a><span data-ttu-id="794db-151">Eseguire il processo di HiveQL hello</span><span class="sxs-lookup"><span data-stu-id="794db-151">Run hello HiveQL job</span></span>

1. <span data-ttu-id="794db-152">Utilizzare hello seguente di un file contenente le istruzioni HiveQL toocreate comando:</span><span class="sxs-lookup"><span data-stu-id="794db-152">Use hello following command toocreate a file containing HiveQL statements:</span></span>

   ```bash
   nano twitter.hql
   ```

    <span data-ttu-id="794db-153">Utilizzare hello segue testo come contenuto di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="794db-153">Use hello following text as hello contents of hello file:</span></span>

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

2. <span data-ttu-id="794db-154">Premere **Ctrl + X**, quindi premere **Y** file hello toosave.</span><span class="sxs-lookup"><span data-stu-id="794db-154">Press **Ctrl + X**, then press **Y** toosave hello file.</span></span>
3. <span data-ttu-id="794db-155">Utilizzare hello comando toorun hello che hiveql contenute nel file hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="794db-155">Use hello following command toorun hello HiveQL contained in hello file:</span></span>

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    <span data-ttu-id="794db-156">Questo comando viene eseguito hello hello **twitter.hql** file.</span><span class="sxs-lookup"><span data-stu-id="794db-156">This command runs hello hello **twitter.hql** file.</span></span> <span data-ttu-id="794db-157">Una volta completata la query hello, vedrai un `jdbc:hive2//localhost:10001/>` prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="794db-157">Once hello query completes, you see a `jdbc:hive2//localhost:10001/>` prompt.</span></span>

4. <span data-ttu-id="794db-158">Dal prompt dei comandi beeline hello, utilizzare hello tooverify query che è stati importati i dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="794db-158">From hello beeline prompt, use hello following query tooverify that data was imported:</span></span>

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    <span data-ttu-id="794db-159">Questa query restituisce un massimo di 10 TWEET che contengono la parola hello **Azure** nel testo del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="794db-159">This query returns a maximum of 10 tweets that contain hello word **Azure** in hello message text.</span></span>

## <a name="next-steps"></a><span data-ttu-id="794db-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="794db-160">Next steps</span></span>

<span data-ttu-id="794db-161">Si è appreso come tootransform un set di dati non strutturati JSON in una tabella Hive strutturata.</span><span class="sxs-lookup"><span data-stu-id="794db-161">You have learned how tootransform an unstructured JSON dataset into a structured Hive table.</span></span> <span data-ttu-id="794db-162">toolearn ulteriori informazioni su Hive in HDInsight, vedere hello seguenti documenti:</span><span class="sxs-lookup"><span data-stu-id="794db-162">toolearn more about Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="794db-163">Introduzione all'uso di HDInsight</span><span class="sxs-lookup"><span data-stu-id="794db-163">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="794db-164">Analizzare i dati sui ritardi dei voli con HDInsight</span><span class="sxs-lookup"><span data-stu-id="794db-164">Analyze flight delay data using HDInsight</span></span>](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
