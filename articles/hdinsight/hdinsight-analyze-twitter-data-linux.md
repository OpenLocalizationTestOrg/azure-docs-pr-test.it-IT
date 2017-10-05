---
title: 'Analizzare i dati di Twitter con Apache Hive: Azure HDInsight | Microsoft Docs'
description: Informazioni su come usare Hive e Hadoop in HDInsight per trasformare i dati di Twitter non elaborati in una tabella Hive ricercabile.
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
ms.openlocfilehash: b8656123fa9c5158f366872ab050f370080ec18a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a><span data-ttu-id="4ec19-103">Analizzare i dati di Twitter mediante Hive e Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ec19-103">Analyze Twitter data using Hive and Hadoop on HDInsight</span></span>

<span data-ttu-id="4ec19-104">Informazioni su come usare Apache Hive per elaborare i dati di Twitter.</span><span class="sxs-lookup"><span data-stu-id="4ec19-104">Learn how to use Apache Hive to process Twitter data.</span></span> <span data-ttu-id="4ec19-105">Il risultato è un elenco di utenti Twitter che hanno inviato il maggior numero di tweet contenenti una determinata parola.</span><span class="sxs-lookup"><span data-stu-id="4ec19-105">The result is a list of Twitter users who sent the most tweets that contain a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ec19-106">I passaggi descritti in questo documento sono stati testati in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="4ec19-106">The steps in this document were tested on HDInsight 3.6.</span></span>
>
> <span data-ttu-id="4ec19-107">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="4ec19-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4ec19-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4ec19-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="get-the-data"></a><span data-ttu-id="4ec19-109">Ottenere i dati</span><span class="sxs-lookup"><span data-stu-id="4ec19-109">Get the data</span></span>

<span data-ttu-id="4ec19-110">Twitter consente di recuperare i [dati relativi ad ogni tweet](https://dev.twitter.com/docs/platform-objects/tweets) come documento JSON (JavaScript Object Notation) attraverso un'API REST.</span><span class="sxs-lookup"><span data-stu-id="4ec19-110">Twitter allows you to retrieve the [data for each tweet](https://dev.twitter.com/docs/platform-objects/tweets) as a JavaScript Object Notation (JSON) document through a REST API.</span></span> <span data-ttu-id="4ec19-111">[OAuth](http://oauth.net) .</span><span class="sxs-lookup"><span data-stu-id="4ec19-111">[OAuth](http://oauth.net) is required for authentication to the API.</span></span>

### <a name="create-a-twitter-application"></a><span data-ttu-id="4ec19-112">Creare un'applicazione Twitter</span><span class="sxs-lookup"><span data-stu-id="4ec19-112">Create a Twitter application</span></span>

1. <span data-ttu-id="4ec19-113">Da un Web browser accedere a [https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="4ec19-113">From a web browser, sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="4ec19-114">Se non si dispone di un account Twitter, fare clic sul collegamento **Sign up now** (Registrati ora).</span><span class="sxs-lookup"><span data-stu-id="4ec19-114">Click the **Sign-up now** link if you don't have a Twitter account.</span></span>

2. <span data-ttu-id="4ec19-115">Fare clic su **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="4ec19-115">Click **Create New App**.</span></span>

3. <span data-ttu-id="4ec19-116">Compilare i campi **Name**, **Description**, **Website**.</span><span class="sxs-lookup"><span data-stu-id="4ec19-116">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="4ec19-117">Per il campo **Website** è possibile creare un URL fittizio.</span><span class="sxs-lookup"><span data-stu-id="4ec19-117">You can make up a URL for the **Website** field.</span></span> <span data-ttu-id="4ec19-118">Nella tabella seguente vengono mostrati alcuni valori di esempio da usare:</span><span class="sxs-lookup"><span data-stu-id="4ec19-118">The following table shows some sample values to use:</span></span>

   | <span data-ttu-id="4ec19-119">Campo</span><span class="sxs-lookup"><span data-stu-id="4ec19-119">Field</span></span> | <span data-ttu-id="4ec19-120">Valore</span><span class="sxs-lookup"><span data-stu-id="4ec19-120">Value</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="4ec19-121">Nome</span><span class="sxs-lookup"><span data-stu-id="4ec19-121">Name</span></span> |<span data-ttu-id="4ec19-122">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="4ec19-122">MyHDInsightApp</span></span> |
   | <span data-ttu-id="4ec19-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4ec19-123">Description</span></span> |<span data-ttu-id="4ec19-124">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="4ec19-124">MyHDInsightApp</span></span> |
   | <span data-ttu-id="4ec19-125">Website</span><span class="sxs-lookup"><span data-stu-id="4ec19-125">Website</span></span> |<span data-ttu-id="4ec19-126">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="4ec19-126">http://www.myhdinsightapp.com</span></span> |

4. <span data-ttu-id="4ec19-127">Fare clic su **Yes, I agree** e su **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="4ec19-127">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>

5. <span data-ttu-id="4ec19-128">Fare clic sulla scheda **Permissions** . L'autorizzazione predefinita è **Read only**.</span><span class="sxs-lookup"><span data-stu-id="4ec19-128">Click the **Permissions** tab. The default permission is **Read only**.</span></span>

6. <span data-ttu-id="4ec19-129">Fare clic sulla scheda **Keys and Access Tokens** .</span><span class="sxs-lookup"><span data-stu-id="4ec19-129">Click the **Keys and Access Tokens** tab.</span></span>

7. <span data-ttu-id="4ec19-130">Fare clic su **Create my access token**.</span><span class="sxs-lookup"><span data-stu-id="4ec19-130">Click **Create my access token**.</span></span>

8. <span data-ttu-id="4ec19-131">Fare clic su **Test OAuth** nell'angolo superiore destro della pagina.</span><span class="sxs-lookup"><span data-stu-id="4ec19-131">Click **Test OAuth** in the upper-right corner of the page.</span></span>

9. <span data-ttu-id="4ec19-132">Compilare i campi **Consumer key**, **Consumer secret**, **Access token** e **Access token secret**.</span><span class="sxs-lookup"><span data-stu-id="4ec19-132">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span>

### <a name="download-tweets"></a><span data-ttu-id="4ec19-133">Scaricare tweet</span><span class="sxs-lookup"><span data-stu-id="4ec19-133">Download tweets</span></span>

<span data-ttu-id="4ec19-134">Il codice Python seguente consente di scaricare 10.000 tweet da Twitter e salvarli in un file denominato **tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="4ec19-134">The following Python code downloads 10,000 tweets from Twitter and save them to a file named **tweets.txt**.</span></span>

> [!NOTE]
> <span data-ttu-id="4ec19-135">I passaggi indicati di seguito vengono eseguiti nel cluster HDInsight, poiché Python è già installato.</span><span class="sxs-lookup"><span data-stu-id="4ec19-135">The following steps are performed on the HDInsight cluster, since Python is already installed.</span></span>

1. <span data-ttu-id="4ec19-136">Connettersi al cluster HDInsight usando SSH:</span><span class="sxs-lookup"><span data-stu-id="4ec19-136">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="4ec19-137">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4ec19-137">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="4ec19-138">Per installare i moduli [Tweepy](http://www.tweepy.org/) e [Progressbar](https://pypi.python.org/pypi/progressbar/2.2) e altri pacchetti obbligatori, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ec19-138">Use the following commands to install [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2), and other required packages:</span></span>

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

4. <span data-ttu-id="4ec19-139">Usare il comando seguente per creare un file denominato **gettweets.py**:</span><span class="sxs-lookup"><span data-stu-id="4ec19-139">Use the following command to create a file named **gettweets.py**:</span></span>

   ```bash
   nano gettweets.py
   ```

5. <span data-ttu-id="4ec19-140">Usare il testo seguente come contenuto del file **gettweets.py**:</span><span class="sxs-lookup"><span data-stu-id="4ec19-140">Use the following text as the contents of the **gettweets.py** file:</span></span>

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

   #The number of tweets we want to get
   max_tweets=10000

   #Create the listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set the counter to zero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append the tweet to the 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment the number of tweets
               self.num_tweets += 1
               #Check to see if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment the progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get the OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use the listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > <span data-ttu-id="4ec19-141">Sostituire il testo segnaposto per gli elementi seguenti con le informazioni fornite dall'app Twitter:</span><span class="sxs-lookup"><span data-stu-id="4ec19-141">Replace the placeholder text for the following items with the information from your twitter application:</span></span>
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. <span data-ttu-id="4ec19-142">Usare **Ctrl + X**, quindi premere **Y** per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="4ec19-142">Use **Ctrl + X**, then **Y** to save the file.</span></span>

7. <span data-ttu-id="4ec19-143">Usare il comando seguente per aprire il file e scaricare i tweet:</span><span class="sxs-lookup"><span data-stu-id="4ec19-143">Use the following command to run the file and download tweets:</span></span>

    ```bash
    python gettweets.py
    ```

    <span data-ttu-id="4ec19-144">Viene visualizzato un indicatore di stato</span><span class="sxs-lookup"><span data-stu-id="4ec19-144">A progress indicator appears.</span></span> <span data-ttu-id="4ec19-145">che mostra un valore fino al 100% mentre vengono scaricati i tweet.</span><span class="sxs-lookup"><span data-stu-id="4ec19-145">It counts up to 100% as the tweets are downloaded.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4ec19-146">Se l'indicatore di stato impiega molto tempo per avanzare, è necessario modificare il filtro per monitorare gli argomenti di tendenza.</span><span class="sxs-lookup"><span data-stu-id="4ec19-146">If it is taking a long time for the progress bar to advance, you should change the filter to track trending topics.</span></span> <span data-ttu-id="4ec19-147">Quando sono presenti molti tweet relativi all'argomento del filtro, è possibile ottenere rapidamente i 10000 tweet necessari.</span><span class="sxs-lookup"><span data-stu-id="4ec19-147">When there are many tweets about the topic in your filter, you can quickly get the 10000 tweets needed.</span></span>

### <a name="upload-the-data"></a><span data-ttu-id="4ec19-148">Caricare i dati</span><span class="sxs-lookup"><span data-stu-id="4ec19-148">Upload the data</span></span>

<span data-ttu-id="4ec19-149">Usare i comandi seguenti per aggiornare i dati nell'archiviazione HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4ec19-149">To upload the data to HDInsight storage, use the following commands:</span></span>

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

<span data-ttu-id="4ec19-150">Questi comandi archiviano i dati in un percorso accessibile a tutti i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="4ec19-150">These commands store the data in a location that all nodes in the cluster can access.</span></span>

## <a name="run-the-hiveql-job"></a><span data-ttu-id="4ec19-151">Eseguire il processo di HiveQL</span><span class="sxs-lookup"><span data-stu-id="4ec19-151">Run the HiveQL job</span></span>

1. <span data-ttu-id="4ec19-152">Usare il comando seguente per creare un file contenente istruzioni HiveQL:</span><span class="sxs-lookup"><span data-stu-id="4ec19-152">Use the following command to create a file containing HiveQL statements:</span></span>

   ```bash
   nano twitter.hql
   ```

    <span data-ttu-id="4ec19-153">Usare il testo seguente come contenuto del file:</span><span class="sxs-lookup"><span data-stu-id="4ec19-153">Use the following text as the contents of the file:</span></span>

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward the tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate the destination table
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
   -- Select tweets from the imported data, parse the JSON,
   -- and insert into the tweets table
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

2. <span data-ttu-id="4ec19-154">Premere **Ctrl + X**, quindi **Y** per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="4ec19-154">Press **Ctrl + X**, then press **Y** to save the file.</span></span>
3. <span data-ttu-id="4ec19-155">Usare il comando riportato di seguito per eseguire lo script HiveQL contenuto nel file:</span><span class="sxs-lookup"><span data-stu-id="4ec19-155">Use the following command to run the HiveQL contained in the file:</span></span>

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    <span data-ttu-id="4ec19-156">Questo comando esegue il file **twitter.hql**.</span><span class="sxs-lookup"><span data-stu-id="4ec19-156">This command runs the the **twitter.hql** file.</span></span> <span data-ttu-id="4ec19-157">Dopo il completamento della query, viene visualizzato un prompt `jdbc:hive2//localhost:10001/>`.</span><span class="sxs-lookup"><span data-stu-id="4ec19-157">Once the query completes, you see a `jdbc:hive2//localhost:10001/>` prompt.</span></span>

4. <span data-ttu-id="4ec19-158">Dal prompt dei comandi Beeline usare la query seguente per verificare che i dati siano stati importati:</span><span class="sxs-lookup"><span data-stu-id="4ec19-158">From the beeline prompt, use the following query to verify that data was imported:</span></span>

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    <span data-ttu-id="4ec19-159">Viene restituito un massimo di 10 tweet contenenti la parola **Azure** nel testo del messaggio.</span><span class="sxs-lookup"><span data-stu-id="4ec19-159">This query returns a maximum of 10 tweets that contain the word **Azure** in the message text.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ec19-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4ec19-160">Next steps</span></span>

<span data-ttu-id="4ec19-161">Si è appreso come trasformare un set di dati JSON non strutturato in una tabella Hive strutturata.</span><span class="sxs-lookup"><span data-stu-id="4ec19-161">You have learned how to transform an unstructured JSON dataset into a structured Hive table.</span></span> <span data-ttu-id="4ec19-162">Per altre informazioni su Hive in HDInsight, vedere i documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ec19-162">To learn more about Hive on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="4ec19-163">Introduzione all'uso di HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ec19-163">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="4ec19-164">Analizzare i dati sui ritardi dei voli con HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ec19-164">Analyze flight delay data using HDInsight</span></span>](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
