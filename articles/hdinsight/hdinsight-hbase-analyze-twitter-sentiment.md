---
title: Analizzare i sentiment di Twitter in tempo reale con HBase - Azure | Microsoft Docs
description: Istruzioni per l'esecuzione dell'analisi dei sentimenti dei Big Data in tempo reale da Twitter con HBase in un cluster HDInsight (Hadoop).
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5c798ad3-a20d-4385-a463-f4f7705f9566
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jgao
ms.openlocfilehash: 4d5bb90c0e7573afb75282810c9ba58e7163e127
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-real-time-twitter-sentiment-with-hbase-in-hdinsight"></a><span data-ttu-id="4ffee-103">Analisi dei sentimenti Twitter in tempo reale con HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ffee-103">Analyze real-time Twitter sentiment with HBase in HDInsight</span></span>
<span data-ttu-id="4ffee-104">Informazioni su come eseguire l'[analisi del sentiment](http://en.wikipedia.org/wiki/Sentiment_analysis) di Big Data in tempo reale da Twitter usando un cluster HBase in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ffee-104">Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data from Twitter by using a HBase cluster in HDInsight.</span></span>

<span data-ttu-id="4ffee-105">I siti Web di social networking rappresentano una delle principali forze trainanti per l'adozione di Big Data.</span><span class="sxs-lookup"><span data-stu-id="4ffee-105">Social websites are one of the major driving forces for big data adoption.</span></span> <span data-ttu-id="4ffee-106">Le API pubbliche offerte da siti quali Twitter costituiscono un'utile origine di dati per l'analisi e la comprensione delle tendenze più popolari.</span><span class="sxs-lookup"><span data-stu-id="4ffee-106">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span> <span data-ttu-id="4ffee-107">In questa esercitazione viene spiegato come sviluppare un'applicazione di servizio per lo streaming su console e un'applicazione Web ASP.NET al fine di:</span><span class="sxs-lookup"><span data-stu-id="4ffee-107">In this tutorial, you develop a console streaming service application and an ASP.NET web application to perform the following:</span></span>

![Analisi del sentiment di Twitter con HBase in HDInsight][img-app-arch]

* <span data-ttu-id="4ffee-109">Applicazione di streaming</span><span class="sxs-lookup"><span data-stu-id="4ffee-109">The streaming application</span></span>

  * <span data-ttu-id="4ffee-110">ottenere tweet geotaggati in tempo reale usando l'API di streaming di Twitter</span><span class="sxs-lookup"><span data-stu-id="4ffee-110">get geo-tagged tweets in real time by using the Twitter streaming API</span></span>
  * <span data-ttu-id="4ffee-111">valutare i sentimenti di tali tweet</span><span class="sxs-lookup"><span data-stu-id="4ffee-111">evaluate the sentiment of these tweets</span></span>
  * <span data-ttu-id="4ffee-112">memorizzare i dati sui sentimenti in HBase usando la SDK di Microsoft HBase</span><span class="sxs-lookup"><span data-stu-id="4ffee-112">store the sentiment information in HBase by using the Microsoft HBase SDK</span></span>
* <span data-ttu-id="4ffee-113">Applicazione Siti Web di Azure</span><span class="sxs-lookup"><span data-stu-id="4ffee-113">The Azure Websites application</span></span>

  * <span data-ttu-id="4ffee-114">tracciare i dati statistici in tempo reale sulle mappe Bing usando un'applicazione Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4ffee-114">plot the real-time statistical results on Bing maps by using an ASP.NET web application.</span></span> <span data-ttu-id="4ffee-115">Una visualizzazione dei tweet è simile alla schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="4ffee-115">A visualization of the tweets is similar to the following screenshot:</span></span>

    ![hdinsight.hbase.twitter.sentiment.bing.map][img-bing-map]

    <span data-ttu-id="4ffee-117">È possibile effettuare query sui tweet usando specifiche parole chiave per determinare se l'opinione espressa nei tweet è positiva, negativa o neutrale.</span><span class="sxs-lookup"><span data-stu-id="4ffee-117">You are able to query tweets with certain keywords to get a sense of if the expressed opinion in the tweets is positive, negative, or neutral.</span></span>

<span data-ttu-id="4ffee-118">Un esempio di soluzione completa di Visual Studio è disponibile su GitHub, ovvero l' [app di analisi dei sentimenti dei social media in tempo reale](https://github.com/maxluk/tweet-sentiment).</span><span class="sxs-lookup"><span data-stu-id="4ffee-118">A complete Visual Studio solution sample can be found on GitHub: [Realtime social sentiment analysis app](https://github.com/maxluk/tweet-sentiment).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4ffee-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4ffee-119">Prerequisites</span></span>
<span data-ttu-id="4ffee-120">Prima di iniziare questa esercitazione, è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="4ffee-120">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="4ffee-121">**Un cluster HBase in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-121">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="4ffee-122">Per istruzioni sulla creazione di cluster, vedere l'[introduzione all'uso di HBase con Hadoop in HDInsight][hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="4ffee-122">For instructions about creating clusters, see  [Get started using HBase with Hadoop in HDInsight][hbase-get-started].</span></span> 

* <span data-ttu-id="4ffee-123">**Una workstation** in cui sia installato Visual Studio 2013/2015/2017.</span><span class="sxs-lookup"><span data-stu-id="4ffee-123">**A workstation** with Visual Studio 2013/2015/2017 installed.</span></span> <span data-ttu-id="4ffee-124">Per le istruzioni, vedere [Installazione di Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ffee-124">For instructions, see [Installing Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx).</span></span>

## <a name="create-a-twitter-application-id-and-secrets"></a><span data-ttu-id="4ffee-125">Creazione dell'ID e dei segreti di un'applicazione Twitter</span><span class="sxs-lookup"><span data-stu-id="4ffee-125">Create a Twitter application ID and secrets</span></span>
<span data-ttu-id="4ffee-126">Le API di streaming di Twitter usano [OAuth](http://oauth.net/) per l'autorizzazione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="4ffee-126">The Twitter streaming APIs use [OAuth](http://oauth.net/) to authorize requests.</span></span> <span data-ttu-id="4ffee-127">Il primo passaggio da seguire per usare OAuth consiste nel creare una nuova applicazione sul sito Twitter Developers.</span><span class="sxs-lookup"><span data-stu-id="4ffee-127">The first step to use OAuth is to create a new application on the Twitter developer site.</span></span>

<span data-ttu-id="4ffee-128">**Per creare l'ID e i segreti di un'applicazione Twitter**</span><span class="sxs-lookup"><span data-stu-id="4ffee-128">**To create Twitter application ID and secrets**</span></span>

1. <span data-ttu-id="4ffee-129">Accedere a [Twitter Apps](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="4ffee-129">Sign in to [Twitter Apps](https://apps.twitter.com/).</span></span> <span data-ttu-id="4ffee-130">Se non si dispone di un account Twitter, fare clic sul collegamento **Sign up now** .</span><span class="sxs-lookup"><span data-stu-id="4ffee-130">Click the **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="4ffee-131">Fare clic su **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-131">Click **Create New App**.</span></span>
3. <span data-ttu-id="4ffee-132">Compilare i campi **Name** (Nome), **Description** (Descrizione) e **Website** (Sito Web).</span><span class="sxs-lookup"><span data-stu-id="4ffee-132">Enter a **Name**, **Description**, and **Website**.</span></span> <span data-ttu-id="4ffee-133">Il nome dell'applicazione Twitter deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="4ffee-133">The Twitter application name must be a unique name.</span></span> <span data-ttu-id="4ffee-134">Il campo Website non viene realmente usato.</span><span class="sxs-lookup"><span data-stu-id="4ffee-134">The Website field is not really used.</span></span> <span data-ttu-id="4ffee-135">Non è necessario inserire un URL valido.</span><span class="sxs-lookup"><span data-stu-id="4ffee-135">It doesn't have to be a valid URL.</span></span>
4. <span data-ttu-id="4ffee-136">Fare clic su **Yes, I agree** e su **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-136">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="4ffee-137">Fare clic sulla scheda **Permissions** (Autorizzazioni) e quindi su **Read only** (Sola lettura).</span><span class="sxs-lookup"><span data-stu-id="4ffee-137">Click the **Permissions** tab, and then click **Read only**.</span></span> <span data-ttu-id="4ffee-138">L'autorizzazione di sola lettura è sufficiente ai fini di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4ffee-138">The read-only permission is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="4ffee-139">Fare clic sulla scheda **Keys and Access Tokens** .</span><span class="sxs-lookup"><span data-stu-id="4ffee-139">Click the **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="4ffee-140">Fare clic su **Create my access token** (Crea il mio token di accesso) nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="4ffee-140">Click **Create my access token** on the bottom of the page.</span></span>
9. <span data-ttu-id="4ffee-141">Copiare i valori dei campi **Consumer Key (API Key)** (Chiave utente - Chiave API), **Consumer Secret (API Secret)** (Segreto utente - Segreto API), **Access token** (Token di accesso) e **Access token secret** (Segreto token di accesso).</span><span class="sxs-lookup"><span data-stu-id="4ffee-141">Copy the **Consumer Key (API Key)**, **Consumer Secret (API Secret)**, **Access token**, and **Access token secret** values.</span></span> <span data-ttu-id="4ffee-142">Sarà necessario usare questi valori più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4ffee-142">You need these values later in the tutorial.</span></span>

    > <span data-ttu-id="4ffee-143">![NOTA] Il pulsante Test OAuth non funziona più.</span><span class="sxs-lookup"><span data-stu-id="4ffee-143">![NOTE] The Test OAuth button does not work anymore.</span></span>

## <a name="create-twitter-streaming-service"></a><span data-ttu-id="4ffee-144">Creare un servizio di streaming di Twitter</span><span class="sxs-lookup"><span data-stu-id="4ffee-144">Create Twitter streaming service</span></span>
<span data-ttu-id="4ffee-145">È necessario creare un'applicazione per ricevere i tweet, calcolare i punteggi dei sentimenti dei tweet e inviare i termini dei tweet elaborati a HBase.</span><span class="sxs-lookup"><span data-stu-id="4ffee-145">You need to create an application to get tweets, calculate tweet sentiment score, and send the processed tweet words to HBase.</span></span>

<span data-ttu-id="4ffee-146">**Per creare l'applicazione di streaming**</span><span class="sxs-lookup"><span data-stu-id="4ffee-146">**To create the streaming application**</span></span>

1. <span data-ttu-id="4ffee-147">Aprire **Visual Studio** e creare un'applicazione console Visual C# denominata **TweetSentimentStreaming**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-147">Open **Visual Studio**, and create a Visual C# console application called **TweetSentimentStreaming**.</span></span>
2. <span data-ttu-id="4ffee-148">Nella finestra **Console di Gestione pacchetti**eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ffee-148">From **Package Manager Console**, run the following commands:</span></span>

        Install-Package Microsoft.HBase.Client -version 0.4.2.0
        Install-Package TweetinviAPI -version 1.0.0.0

    <span data-ttu-id="4ffee-149">I comandi seguenti permettono di installare il pacchetto [HBase .NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/), ovvero la libreria client che consente di accedere al cluster HBase, e il pacchetto [Tweetinvi API](https://www.nuget.org/packages/TweetinviAPI/), usato per accedere all'API Twitter.</span><span class="sxs-lookup"><span data-stu-id="4ffee-149">These commands install the [HBase .NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/) package, which is the client library to access the HBase cluster, and the [Tweetinvi API](https://www.nuget.org/packages/TweetinviAPI/) package, which is used to access the Twitter API.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4ffee-150">L'esempio usato in questo articolo è stato testato con la versione specificata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4ffee-150">The sample used in this article has been tested using the version specified above.</span></span>  <span data-ttu-id="4ffee-151">È possibile rimuovere la versione per installare la più recente.</span><span class="sxs-lookup"><span data-stu-id="4ffee-151">You can remove the -version switch to install the latest version.</span></span>
   >
   >
3. <span data-ttu-id="4ffee-152">In **Esplora soluzioni** aggiungere **System.Configuration** al riferimento.</span><span class="sxs-lookup"><span data-stu-id="4ffee-152">From **Solution Explorer**, add **System.Configuration** to the reference.</span></span>
4. <span data-ttu-id="4ffee-153">Aggiungere un nuovo file di classe al progetto denominato **HBaseWriter.cs**e quindi sostituire il codice con quanto segue:</span><span class="sxs-lookup"><span data-stu-id="4ffee-153">Add a new class file to the project called **HBaseWriter.cs**, and then replace the code with the following:</span></span>

        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Text;
        using System.Threading;
        using Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling;
        using org.apache.hadoop.hbase.rest.protobuf.generated;
        using Microsoft.HBase.Client;
        using Tweetinvi.Models;

        namespace TweetSentimentStreaming
        {
            class HBaseWriter
            {
                // HDinsight HBase cluster and HBase table information
                const string CLUSTERNAME = "https://<Enter Your Cluster Name>.azurehdinsight.net/";
                const string HADOOPUSERNAME = "admin"; //the default name is "admin"
                const string HADOOPUSERPASSWORD = "<Enter the Hadoop User Password>";

                const string HBASETABLENAME = "tweets_by_words";
                const string COUNT_ROW_KEY = "~ROWCOUNT";
                const string COUNT_COLUMN_NAME = "d:COUNT";

                long rowCount = 0;

                // Sentiment dictionary file and the punctuation characters
                const string DICTIONARYFILENAME = @"..\..\dictionary.tsv";
                private static char[] _punctuationChars = new[] {
            ' ', '!', '\"', '#', '$', '%', '&', '\'', '(', ')', '*', '+', ',', '-', '.', '/',   //ascii 23--47
            ':', ';', '<', '=', '>', '?', '@', '[', ']', '^', '_', '`', '{', '|', '}', '~' };   //ascii 58--64 + misc.

                // For writting to HBase
                HBaseClient client;

                // a sentiment dictionary for estimate sentiment. It is loaded from a physical file.
                Dictionary<string, DictionaryItem> dictionary;

                // use multithread write
                Thread writerThread;
                Queue<ITweet> queue = new Queue<ITweet>();
                bool threadRunning = true;

                // This function connects to HBase, loads the sentiment dictionary, and starts the thread for writting.
                public HBaseWriter()
                {
                    ClusterCredentials credentials = new ClusterCredentials(new Uri(CLUSTERNAME), HADOOPUSERNAME, HADOOPUSERPASSWORD);
                    client = new HBaseClient(credentials);

                    // create the HBase table if it doesn't exist
                    if (!client.ListTablesAsync().Result.name.Contains(HBASETABLENAME))
                    {
                        TableSchema tableSchema = new TableSchema();
                        tableSchema.name = HBASETABLENAME;
                        tableSchema.columns.Add(new ColumnSchema { name = "d" });
                        client.CreateTableAsync(tableSchema).Wait();
                        Console.WriteLine("Table \"{0}\" is created.", HBASETABLENAME);
                    }

                    // Read current row count cell
                    rowCount = GetRowCount();

                    // Load sentiment dictionary from a file
                    LoadDictionary();

                    // Start a thread for writting to HBase
                    writerThread = new Thread(new ThreadStart(WriterThreadFunction));
                    writerThread.Start();
                }

                ~HBaseWriter()
                {
                    threadRunning = false;
                }

                private long GetRowCount()
                {
                    try
                    {
                        RequestOptions options = RequestOptions.GetDefaultOptions();
                        options.RetryPolicy = RetryPolicy.NoRetry;
                        var cellSet = client.GetCellsAsync(HBASETABLENAME, COUNT_ROW_KEY, null, null, options).Result;
                        if (cellSet.rows.Count != 0)
                        {
                            var countCol = cellSet.rows[0].values.Find(cell => Encoding.UTF8.GetString(cell.column) == COUNT_COLUMN_NAME);
                            if (countCol != null)
                            {
                                return Convert.ToInt64(Encoding.UTF8.GetString(countCol.data));
                            }
                        }
                    }
                    catch(Exception ex)
                    {
                        if (ex.InnerException.Message.Equals("The remote server returned an error: (404) Not Found.", StringComparison.OrdinalIgnoreCase))
                        {
                            return 0;
                        }
                        else
                        {
                            throw ex;
                        }

                    }

                    return 0;
                }

                // Enqueue the Tweets received
                public void WriteTweet(ITweet tweet)
                {
                    lock (queue)
                    {
                        queue.Enqueue(tweet);
                    }
                }

                // Load sentiment dictionary from a file
                private void LoadDictionary()
                {
                    List<string> lines = File.ReadAllLines(DICTIONARYFILENAME).ToList();
                    var items = lines.Select(line =>
                    {
                        var fields = line.Split('\t');
                        var pos = 0;
                        return new DictionaryItem
                        {
                            Type = fields[pos++],
                            Length = Convert.ToInt32(fields[pos++]),
                            Word = fields[pos++],
                            Pos = fields[pos++],
                            Stemmed = fields[pos++],
                            Polarity = fields[pos++]
                        };
                    });

                    dictionary = new Dictionary<string, DictionaryItem>();
                    foreach (var item in items)
                    {
                        if (!dictionary.Keys.Contains(item.Word))
                        {
                            dictionary.Add(item.Word, item);
                        }
                    }
                }

                // Calculate sentiment score
                private int CalcSentimentScore(string[] words)
                {
                    Int32 total = 0;
                    foreach (string word in words)
                    {
                        if (dictionary.Keys.Contains(word))
                        {
                            switch (dictionary[word].Polarity)
                            {
                                case "negative": total -= 1; break;
                                case "positive": total += 1; break;
                            }
                        }
                    }
                    if (total > 0)
                    {
                        return 1;
                    }
                    else if (total < 0)
                    {
                        return -1;
                    }
                    else
                    {
                        return 0;
                    }
                }

                // Popular a CellSet object to be written into HBase
                private void CreateTweetByWordsCells(CellSet set, ITweet tweet)
                {
                    // Split the Tweet into words
                    string[] words = tweet.Text.ToLower().Split(_punctuationChars);

                    // Calculate sentiment score base on the words
                    int sentimentScore = CalcSentimentScore(words);
                    var word_pairs = words.Take(words.Length - 1)
                                        .Select((word, idx) => string.Format("{0} {1}", word, words[idx + 1]));
                    var all_words = words.Concat(word_pairs).ToList();

                    // For each word in the Tweet add a row to the HBase table
                    foreach (string word in all_words)
                    {
                        string time_index = (ulong.MaxValue - (ulong)tweet.CreatedAt.ToBinary()).ToString().PadLeft(20) + tweet.IdStr;
                        string key = word + "_" + time_index;

                        // Create a row
                        var row = new CellSet.Row { key = Encoding.UTF8.GetBytes(key) };

                        // Add columns to the row, including Tweet identifier, language, coordinator(if available), and sentiment
                        var value = new Cell { column = Encoding.UTF8.GetBytes("d:id_str"), data = Encoding.UTF8.GetBytes(tweet.IdStr) };
                        row.values.Add(value);

                        value = new Cell { column = Encoding.UTF8.GetBytes("d:lang"), data = Encoding.UTF8.GetBytes(tweet.Language.ToString()) };
                        row.values.Add(value);

                        if (tweet.Coordinates != null)
                        {
                            var str = tweet.Coordinates.Longitude.ToString() + "," + tweet.Coordinates.Latitude.ToString();
                            value = new Cell { column = Encoding.UTF8.GetBytes("d:coor"), data = Encoding.UTF8.GetBytes(str) };
                            row.values.Add(value);
                        }

                        value = new Cell { column = Encoding.UTF8.GetBytes("d:sentiment"), data = Encoding.UTF8.GetBytes(sentimentScore.ToString()) };
                        row.values.Add(value);

                        set.rows.Add(row);
                    }
                }

                // Write a Tweet (CellSet) to HBase
                public void WriterThreadFunction()
                {
                    try
                    {
                        while (threadRunning)
                        {
                            if (queue.Count > 0)
                            {
                                CellSet set = new CellSet();
                                lock (queue)
                                {
                                    do
                                    {
                                        ITweet tweet = queue.Dequeue();
                                        CreateTweetByWordsCells(set, tweet);
                                    } while (queue.Count > 0);
                                }

                                // Write the Tweet by words cell set to the HBase table
                                client.StoreCellsAsync(HBASETABLENAME, set).Wait();
                                Console.WriteLine("\tRows written: {0}", set.rows.Count);
                            }
                            Thread.Sleep(100);
                        }
                    }
                    catch (Exception ex)
                    {
                        Console.WriteLine("Exception: " + ex.Message);
                    }
                }
            }
            public class DictionaryItem
            {
                public string Type { get; set; }
                public int Length { get; set; }
                public string Word { get; set; }
                public string Pos { get; set; }
                public string Stemmed { get; set; }
                public string Polarity { get; set; }
            }
        }
5. <span data-ttu-id="4ffee-154">Impostare le costanti nel codice precedente, incluse **CLUSTERNAME**, **HADOOPUSERNAME**, **HADOOPUSERPASSWORD** e DICTIONARYFILENAME.</span><span class="sxs-lookup"><span data-stu-id="4ffee-154">Set the constants in the previous code, including **CLUSTERNAME**, **HADOOPUSERNAME**, **HADOOPUSERPASSWORD**, and DICTIONARYFILENAME.</span></span> <span data-ttu-id="4ffee-155">DICTIONARYFILENAME è il nome e il percorso del file direction.tsv.</span><span class="sxs-lookup"><span data-stu-id="4ffee-155">The DICTIONARYFILENAME is the filename and the location of the direction.tsv.</span></span>  <span data-ttu-id="4ffee-156">Il file può essere scaricato da **https://hditutorialdata.blob.core.windows.net/twittersentiment/dictionary.tsv**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-156">The file can be downloaded from **https://hditutorialdata.blob.core.windows.net/twittersentiment/dictionary.tsv**.</span></span> <span data-ttu-id="4ffee-157">Per cambiare il nome della tabella HBase, è necessario modificare il nome della tabella nell'applicazione Web di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="4ffee-157">If you want to change the HBase table name, you must change the table name in the web application accordingly.</span></span>
6. <span data-ttu-id="4ffee-158">Aprire **Program.cs**e sostituire il codice con quello seguente:</span><span class="sxs-lookup"><span data-stu-id="4ffee-158">Open **Program.cs**, and replace the code with the following:</span></span>

        using System;
        using System.Diagnostics;
        using Tweetinvi;
        using Tweetinvi.Models;

        namespace TweetSentimentStreaming
        {
            class Program
            {
                const string TWITTERAPPACCESSTOKEN = "<Enter Twitter App Access Token>";
                const string TWITTERAPPACCESSTOKENSECRET = "<Enter Twitter Access Token Secret>";
                const string TWITTERAPPAPIKEY = "<Enter Twitter App API Key>";
                const string TWITTERAPPAPISECRET = "<Enter Twitter App API Secret>";

                static void Main(string[] args)
                {
                    Auth.SetUserCredentials(TWITTERAPPAPIKEY, TWITTERAPPAPISECRET, TWITTERAPPACCESSTOKEN, TWITTERAPPACCESSTOKENSECRET);

                    Stream_FilteredStreamExample();
                }

                private static void Stream_FilteredStreamExample()
                {
                    for (;;)
                    {
                        try
                        {
                            HBaseWriter hbase = new HBaseWriter();
                            var stream = Stream.CreateFilteredStream();
                            stream.AddLocation(new Coordinates(90, -180), new Coordinates(-90,180));

                            var tweetCount = 0;
                            var timer = Stopwatch.StartNew();

                            stream.MatchingTweetReceived += (sender, args) =>
                            {
                                tweetCount++;
                                var tweet = args.Tweet;

                                // Write Tweets to HBase
                                hbase.WriteTweet(tweet);

                                if (timer.ElapsedMilliseconds > 1000)
                                {
                                    if (tweet.Coordinates != null)
                                    {
                                        Console.ForegroundColor = ConsoleColor.Green;
                                        Console.WriteLine("\n{0}: {1} {2}", tweet.Id, tweet.Language.ToString(), tweet.Text);
                                        Console.ForegroundColor = ConsoleColor.White;
                                        Console.WriteLine("\tLocation: {0}, {1}", tweet.Coordinates.Longitude, tweet.Coordinates.Latitude);
                                    }

                                    timer.Restart();
                                    Console.WriteLine("\tTweets/sec: {0}", tweetCount);
                                    tweetCount = 0;
                                }
                            };

                            stream.StartStreamMatchingAllConditions();
                        }
                        catch (Exception ex)
                        {
                            Console.WriteLine("Exception: {0}", ex.Message);
                        }
                    }
                }

            }
        }
7. <span data-ttu-id="4ffee-159">Impostare le costanti, incluse **TWITTERAPPACCESSTOKEN**, **TWITTERAPPACCESSTOKENSECRET**, **TWITTERAPPAPIKEY** e **TWITTERAPPAPISECRET**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-159">Set the constants including **TWITTERAPPACCESSTOKEN**, **TWITTERAPPACCESSTOKENSECRET**, **TWITTERAPPAPIKEY** and **TWITTERAPPAPISECRET**.</span></span>

<span data-ttu-id="4ffee-160">Per eseguire il servizio di streaming, premere **F5**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-160">To run the streaming service, press **F5**.</span></span> <span data-ttu-id="4ffee-161">Di seguito è riportata una schermata dell'applicazione console:</span><span class="sxs-lookup"><span data-stu-id="4ffee-161">The following is a screenshot of the console application:</span></span>

![hdinsight.hbase.twitter.sentiment.streaming.service][img-streaming-service]

<span data-ttu-id="4ffee-163">Lasciare l'applicazione console di streaming in esecuzione durante lo sviluppo dell'applicazione Web, al fine di disporre di una maggiore quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="4ffee-163">Keep the streaming console application running while you develop the web application, so you have more data to use.</span></span> <span data-ttu-id="4ffee-164">Per esaminare i dati inseriti nella tabella, è possibile usare la shell HBase.</span><span class="sxs-lookup"><span data-stu-id="4ffee-164">To examine the data inserted into the table, you can use HBase Shell.</span></span> <span data-ttu-id="4ffee-165">Vedere [Introduzione a HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md#create-tables-and-insert-data).</span><span class="sxs-lookup"><span data-stu-id="4ffee-165">See [Get started with HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md#create-tables-and-insert-data).</span></span>

## <a name="visualize-real-time-sentiment"></a><span data-ttu-id="4ffee-166">Visualizzare i sentimenti in tempo reale</span><span class="sxs-lookup"><span data-stu-id="4ffee-166">Visualize real-time sentiment</span></span>
<span data-ttu-id="4ffee-167">In questa sezione si creerà un'applicazione Web ASP.NET MVC per leggere i dati dei sentimenti in tempo reale su HBase e tracciare i dati sulle mappe Bing.</span><span class="sxs-lookup"><span data-stu-id="4ffee-167">In this section, you create an ASP.NET MVC web application to read the real-time sentiment data from HBase and plot the data on Bing maps.</span></span>

<span data-ttu-id="4ffee-168">**Per creare un'applicazione Web ASP.NET MVC**</span><span class="sxs-lookup"><span data-stu-id="4ffee-168">**To create an ASP.NET MVC Web application**</span></span>

1. <span data-ttu-id="4ffee-169">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4ffee-169">Open Visual Studio.</span></span>
2. <span data-ttu-id="4ffee-170">Fare clic su **File**, **Nuovo** e quindi su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-170">Click **File**, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="4ffee-171">Immettere le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="4ffee-171">Enter the following information:</span></span>

   * <span data-ttu-id="4ffee-172">Categoria modello: **Visual C#/Web**</span><span class="sxs-lookup"><span data-stu-id="4ffee-172">Template category: **Visual C#/Web**</span></span>
   * <span data-ttu-id="4ffee-173">Modello: **Applicazione Web ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="4ffee-173">Template: **ASP.NET Web Application**</span></span>
   * <span data-ttu-id="4ffee-174">Nome: **TweetSentimentWeb**</span><span class="sxs-lookup"><span data-stu-id="4ffee-174">Name: **TweetSentimentWeb**</span></span>
   * <span data-ttu-id="4ffee-175">Percorso: **C:\Tutorials**</span><span class="sxs-lookup"><span data-stu-id="4ffee-175">Location: **C:\Tutorials**</span></span>
4. <span data-ttu-id="4ffee-176">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-176">Click **OK**.</span></span>
5. <span data-ttu-id="4ffee-177">In **Seleziona un modello** fare clic su **MVC**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-177">In **Select a template**, click **MVC**.</span></span>
6. <span data-ttu-id="4ffee-178">In **Microsoft Azure** fare clic su **Gestisci sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-178">In **Microsoft Azure**, click **Manage Subscriptions**.</span></span>
7. <span data-ttu-id="4ffee-179">In **Gestisci sottoscrizioni di Microsoft Azure** fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-179">From **Manage Microsoft Azure Subscriptions**, click **Sign in**.</span></span>
8. <span data-ttu-id="4ffee-180">Immettere le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ffee-180">Enter your Azure credentials.</span></span> <span data-ttu-id="4ffee-181">Le informazioni relative alla sottoscrizione di Azure vengono visualizzate nella scheda **Account**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-181">Your Azure subscription information is shown on the **Accounts** tab.</span></span>
9. <span data-ttu-id="4ffee-182">Fare clic su **Chiudi** per chiudere la finestra **Gestisci sottoscrizioni di Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-182">Click **Close** to close the **Manage Microsoft Azure Subscriptions** window.</span></span>
10. <span data-ttu-id="4ffee-183">In **Nuovo progetto ASP.NET - TweetSentimentWeb** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-183">From **New ASP.NET Project - TweetSentimentWeb**, click **OK**.</span></span>
11. <span data-ttu-id="4ffee-184">In **Configura impostazioni sito Web di Microsoft Azure** selezionare l'area geografica più vicina nel campo **Area geografica**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-184">From **Configure Microsoft Azure Site Settings**, select the **Region** that is closest to you.</span></span> <span data-ttu-id="4ffee-185">Non è necessario specificare un server database.</span><span class="sxs-lookup"><span data-stu-id="4ffee-185">You don't need to specify a database server.</span></span>
12. <span data-ttu-id="4ffee-186">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-186">Click **OK**.</span></span>

<span data-ttu-id="4ffee-187">**Per installare i pacchetti NuGet**</span><span class="sxs-lookup"><span data-stu-id="4ffee-187">**To install NuGet packages**</span></span>

1. <span data-ttu-id="4ffee-188">Dal menu **Strumenti** fare clic su **Gestione pacchetti NuGet**, quindi su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-188">From the **Tools** menu, click **Nuget Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="4ffee-189">Il pannello della console viene visualizzato nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="4ffee-189">The console panel is opened at the bottom of the page.</span></span>
2. <span data-ttu-id="4ffee-190">Usare il comando seguente per installare il pacchetto [HBase .NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/) , ovvero la libreria client che consente di accedere al cluster HBase:</span><span class="sxs-lookup"><span data-stu-id="4ffee-190">Use the following command to install the [HBase .NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/) package, which is the client library to access HBase cluster:</span></span>

        Install-Package Microsoft.HBase.Client

<span data-ttu-id="4ffee-191">**Per aggiungere una classe HBaseReader**</span><span class="sxs-lookup"><span data-stu-id="4ffee-191">**To add HBaseReader class**</span></span>

1. <span data-ttu-id="4ffee-192">In **Esplora soluzioni** espandere **TweetSentiment**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-192">From **Solution Explorer**, expand **TweetSentiment**.</span></span>
2. <span data-ttu-id="4ffee-193">Fare clic con il pulsante destro del mouse su **Modelli**, fare clic su **Aggiungi**, quindi su **Classe**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-193">Right-click **Models**, click **Add**, and then click **Class**.</span></span>
3. <span data-ttu-id="4ffee-194">Nel campo **Nome** digitare **HBaseReader.cs** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-194">In the **Name** field, type **HBaseReader.cs**, and then click **Add**.</span></span>
4. <span data-ttu-id="4ffee-195">Sostituire il codice con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="4ffee-195">Replace the code with the following:</span></span>

        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Web;

        using System.Configuration;
        using System.Threading.Tasks;
        using System.Text;
        using Microsoft.HBase.Client;
        using org.apache.hadoop.hbase.rest.protobuf.generated;

        namespace TweetSentimentWeb.Models
        {
            public class HBaseReader
            {
                // For reading Tweet sentiment data from HDInsight HBase
                HBaseClient client;

                // HDinsight HBase cluster and HBase table information
                const string CLUSTERNAME = "<HBaseClusterName>";
                const string HADOOPUSERNAME = "<HBaseClusterHadoopUserName>"
                const string HADOOPUSERPASSWORD = "<HBaseCluserUserPassword>";
                const string HBASETABLENAME = "tweets_by_words";

                // The constructor
                public HBaseReader()
                {
                    ClusterCredentials creds = new ClusterCredentials(
                                    new Uri(CLUSTERNAME),
                                    HADOOPUSERNAME,
                                    HADOOPUSERPASSWORD);
                    client = new HBaseClient(creds);
                }

                // Query Tweets sentiment data from the HBase table asynchronously
                public async Task<IEnumerable<Tweet>> QueryTweetsByKeywordAsync(string keyword)
                {
                    List<Tweet> list = new List<Tweet>();

                    // Demonstrate Filtering the data from the past 6 hours the row key
                    string timeIndex = (ulong.MaxValue -
                        (ulong)DateTime.UtcNow.Subtract(new TimeSpan(6, 0, 0)).ToBinary()).ToString().PadLeft(20);
                    string startRow = keyword + "_" + timeIndex;
                    string endRow = keyword + "|";
                    Scanner scanSettings = new Scanner
                    {
                        batch = 100000,
                        startRow = Encoding.UTF8.GetBytes(startRow),
                        endRow = Encoding.UTF8.GetBytes(endRow)
                    };

                    // Make async scan call
                    ScannerInformation scannerInfo =
                        await client.CreateScannerAsync(HBASETABLENAME, scanSettings);

                    CellSet next;

                    while ((next = await client.ScannerGetNextAsync(scannerInfo)) != null)
                    {
                        foreach (CellSet.Row row in next.rows)
                        {
                            // find the cell with string pattern "d:coor"
                            var coordinates =
                                row.values.Find(c => Encoding.UTF8.GetString(c.column) == "d:coor");

                            if (coordinates != null)
                            {
                                string[] lonlat = Encoding.UTF8.GetString(coordinates.data).Split(',');

                                var sentimentField =
                                    row.values.Find(c => Encoding.UTF8.GetString(c.column) == "d:sentiment");
                                Int32 sentiment = 0;
                                if (sentimentField != null)
                                {
                                    sentiment = Convert.ToInt32(Encoding.UTF8.GetString(sentimentField.data));
                                }

                                list.Add(new Tweet
                                {
                                    Longtitude = Convert.ToDouble(lonlat[0]),
                                    Latitude = Convert.ToDouble(lonlat[1]),
                                    Sentiment = sentiment
                                });
                            }

                            if (coordinates != null)
                            {
                                string[] lonlat = Encoding.UTF8.GetString(coordinates.data).Split(',');
                            }
                        }
                    }

                    return list;
                }
            }

            public class Tweet
            {
                public string IdStr { get; set; }
                public string Text { get; set; }
                public string Lang { get; set; }
                public double Longtitude { get; set; }
                public double Latitude { get; set; }
                public int Sentiment { get; set; }
            }
        }
5. <span data-ttu-id="4ffee-196">Nella classe **HBaseReader** modificare i valori costanti, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="4ffee-196">Inside the **HBaseReader** class, change the constant values as follows:</span></span>

   * <span data-ttu-id="4ffee-197">**CLUSTERNAME**: nome del cluster HBase, ad esempio *https://<HBaseClusterName>.azurehdinsight.net/*.</span><span class="sxs-lookup"><span data-stu-id="4ffee-197">**CLUSTERNAME**: The HBase cluster name, for example, *https://<HBaseClusterName>.azurehdinsight.net/*.</span></span>
   * <span data-ttu-id="4ffee-198">**HADOOPUSERNAME**: nome utente del cluster HBase (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="4ffee-198">**HADOOPUSERNAME**: The HBase cluster Hadoop user user name.</span></span> <span data-ttu-id="4ffee-199">Il nome predefinito è *admin*.</span><span class="sxs-lookup"><span data-stu-id="4ffee-199">The default name is *admin*.</span></span>
   * <span data-ttu-id="4ffee-200">**HADOOPUSERPASSWORD**: password utente del cluster HBase (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="4ffee-200">**HADOOPUSERPASSWORD**: The HBase cluster Hadoop user password.</span></span>
   * <span data-ttu-id="4ffee-201">**HBASETABLENAME** = "tweets_by_words";</span><span class="sxs-lookup"><span data-stu-id="4ffee-201">**HBASETABLENAME** = "tweets_by_words";</span></span>

     <span data-ttu-id="4ffee-202">Il nome della tabella HBase è **"tweets_by_words"**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-202">The HBase table name is **"tweets_by_words";**.</span></span> <span data-ttu-id="4ffee-203">Per consentire all'applicazione Web di leggere i dati dalla stessa tabella HBase, i valori devono corrispondere a quelli inviati nel servizio streaming.</span><span class="sxs-lookup"><span data-stu-id="4ffee-203">The values must match the values you sent in the streaming service, so that the web application reads the data from the same HBase table.</span></span>

<span data-ttu-id="4ffee-204">**Per aggiungere il controller TweetsController**</span><span class="sxs-lookup"><span data-stu-id="4ffee-204">**To add TweetsController controller**</span></span>

1. <span data-ttu-id="4ffee-205">In **Esplora soluzioni** espandere **TweetSentimentWeb**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-205">From **Solution Explorer**, expand **TweetSentimentWeb**.</span></span>
2. <span data-ttu-id="4ffee-206">Fare clic con il pulsante destro del mouse su **Controller**, quindi scegliere **Aggiungi** e infine fare clic su **Controller**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-206">Right-click **Controllers**, click **Add**, and then click **Controller**.</span></span>
3. <span data-ttu-id="4ffee-207">Fare clic su **Web API 2 Controller - Empty** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-207">Click **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
4. <span data-ttu-id="4ffee-208">Nel campo **Nome controller** digitare **TweetsController**, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-208">In the **Controller name** field, type **TweetsController**, and then click **Add**.</span></span>
5. <span data-ttu-id="4ffee-209">In **Esplora soluzioni**fare doppio clic su TweetsController.cs per aprire il file.</span><span class="sxs-lookup"><span data-stu-id="4ffee-209">From **Solution Explorer**, double-click TweetsController.cs to open the file.</span></span>
6. <span data-ttu-id="4ffee-210">Modificare il file come segue:</span><span class="sxs-lookup"><span data-stu-id="4ffee-210">Modify the file, so it looks like the following:</span></span>

        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Http;

        using System.Threading.Tasks;
        using TweetSentimentWeb.Models;

        namespace TweetSentimentWeb.Controllers
        {
            public class TweetsController : ApiController
            {
                HBaseReader hbase = new HBaseReader();

                public async Task<IEnumerable<Tweet>> GetTweetsByQuery(string query)
                {
                    return await hbase.QueryTweetsByKeywordAsync(query);
                }
            }
        }

<span data-ttu-id="4ffee-211">**Per aggiungere heatmap.js**</span><span class="sxs-lookup"><span data-stu-id="4ffee-211">**To add heatmap.js**</span></span>

1. <span data-ttu-id="4ffee-212">In **Esplora soluzioni** espandere **TweetSentimentWeb**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-212">From **Solution Explorer**, expand **TweetSentimentWeb**.</span></span>
2. <span data-ttu-id="4ffee-213">Fare clic con il pulsante destro del mouse su **Script**, quindi scegliere **Aggiungi** e infine fare clic su **File JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-213">Right-click **Scripts**, click **Add**, click **JavaScript File**.</span></span>
3. <span data-ttu-id="4ffee-214">Nel campo **Nome elemento** digitare **heatmap.js**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-214">In the **Item name** field, type **heatmap.js**.</span></span>
4. <span data-ttu-id="4ffee-215">Incollare il seguente codice nel file.</span><span class="sxs-lookup"><span data-stu-id="4ffee-215">Paste the following code into the file.</span></span> <span data-ttu-id="4ffee-216">Il codice è stato scritto da Alastair Alastair Aitchison.</span><span class="sxs-lookup"><span data-stu-id="4ffee-216">The code was written by Alastair Aitchison.</span></span> <span data-ttu-id="4ffee-217">Per altre informazioni, vedere la [libreria HeatMap di Bing Maps AJAX v7](http://alastaira.wordpress.com/2011/04/15/bing-maps-ajax-v7-heatmap-library/).</span><span class="sxs-lookup"><span data-stu-id="4ffee-217">For more information, see [Bing Maps AJAX v7 HeatMap Library](http://alastaira.wordpress.com/2011/04/15/bing-maps-ajax-v7-heatmap-library/).</span></span>

        /*******************************************************************************
        * Author: Alastair Aitchison
        * Website: http://alastaira.wordpress.com
        * Date: 15th April 2011
        *
        * Description:
        * This JavaScript file provides an algorithm that can be used to add a heatmap
        * overlay on a Bing Maps v7 control. The intensity and temperature palette
        * of the heatmap are designed to be easily customisable.
        *
        * Requirements:
        * The heatmap layer itself is created dynamically on the client-side using
        * the HTML5 &lt;canvas> element, and therefore requires a browser that supports
        * this element. It has been tested on IE9, Firefox 3.6/4 and
        * Chrome 10 browsers. If you can confirm whether it works on other browsers or
        * not, I'd love to hear from you!
        *
        * Usage:
        * The HeatMapLayer constructor requires:
        * - A reference to a map object
        * - An array or Microsoft.Maps.Location items
        * - Optional parameters to customise the appearance of the layer
        *  (Radius,, Unit, Intensity, and ColourGradient), and a callback function
        */

        var HeatMapLayer = function (map, locations, options) {

            /* Private Properties */
            var _map = map,
                _canvas,
                _temperaturemap,
                _locations = [],
                _viewchangestarthandler,
                _viewchangeendhandler;

            // Set default options
            var _options = {
                // Opacity at the centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 1000,

                // Whether the radius is an absolute pixel value or meters
                unit: 'meters',

                // Colour temperature gradient of the map
                colourgradient: {
                    "0.00": 'rgba(255,0,255,20)',  // Magenta
                    "0.25": 'rgba(0,0,255,40)',    // Blue
                    "0.50": 'rgba(0,255,0,80)',    // Green
                    "0.75": 'rgba(255,255,0,120)', // Yellow
                    "1.00": 'rgba(255,0,0,150)'    // Red
                },

                // Callback function to be fired after heatmap layer has been redrawn
                callback: null
            };

            /* Private Methods */
            function _init() {
                var _mapDiv = _map.getRootElement();

                if (_mapDiv.childNodes.length >= 3 && _mapDiv.childNodes[2].childNodes.length >= 2) {
                    // Create the canvas element
                    _canvas = document.createElement('canvas');
                    _canvas.style.position = 'relative';

                    var container = document.createElement('div');
                    container.style.position = 'absolute';
                    container.style.left = '0px';
                    container.style.top = '0px';
                    container.appendChild(_canvas);

                    _mapDiv.childNodes[2].childNodes[1].appendChild(container);

                    // Override defaults with any options passed in the constructor
                    _setOptions(options);

                    // Load array of location data
                    _setPoints(locations);

                    // Create a colour gradient from the suppied colourstops
                    _temperaturemap = _createColourGradient(_options.colourgradient);

                    // Wire up the event handler to redraw heatmap canvas
                    _viewchangestarthandler = Microsoft.Maps.Events.addHandler(_map, 'viewchangestart', _clearHeatMap);
                    _viewchangeendhandler = Microsoft.Maps.Events.addHandler(_map, 'viewchangeend', _createHeatMap);

                    _createHeatMap();

                    delete _init;
                } else {
                    setTimeout(_init, 100);
                }
            }

            // Resets the heat map
            function _clearHeatMap() {
                var ctx = _canvas.getContext("2d");
                ctx.clearRect(0, 0, _canvas.width, _canvas.height);
            }

            // Creates a colour gradient from supplied colour stops on initialisation
            function _createColourGradient(colourstops) {
                var ctx = document.createElement('canvas').getContext('2d');
                var grd = ctx.createLinearGradient(0, 0, 256, 0);
                for (var c in colourstops) {
                    grd.addColorStop(c, colourstops[c]);
                }
                ctx.fillStyle = grd;
                ctx.fillRect(0, 0, 256, 1);
                return ctx.getImageData(0, 0, 256, 1).data;
            }

            // Applies a colour gradient to the intensity map
            function _colouriseHeatMap() {
                var ctx = _canvas.getContext("2d");
                var dat = ctx.getImageData(0, 0, _canvas.width, _canvas.height);
                var pix = dat.data; // pix is a CanvasPixelArray containing height x width x 4 bytes of data (RGBA)
                for (var p = 0, len = pix.length; p < len;) {
                    var a = pix[p + 3] * 4; // get the alpha of this pixel
                    if (a != 0) { // If there is any data to plot
                        pix[p] = _temperaturemap[a]; // set the red value of the gradient that corresponds to this alpha
                        pix[p + 1] = _temperaturemap[a + 1]; //set the green value based on alpha
                        pix[p + 2] = _temperaturemap[a + 2]; //set the blue value based on alpha
                    }
                    p += 4; // Move on to the next pixel
                }
                ctx.putImageData(dat, 0, 0);
            }

            // Sets any options passed in
            function _setOptions(options) {
                for (attrname in options) {
                    _options[attrname] = options[attrname];
                }
            }

            // Sets the heatmap points from an array of Microsoft.Maps.Locations  
            function _setPoints(locations) {
                _locations = locations;
            }

            // Main method to draw the heatmap
            function _createHeatMap() {
                // Ensure the canvas matches the current dimensions of the map
                // This also has the effect of resetting the canvas
                _canvas.height = _map.getHeight();
                _canvas.width = _map.getWidth();

                _canvas.style.top = -_canvas.height / 2 + 'px';
                _canvas.style.left = -_canvas.width / 2 + 'px';

                // Calculate the pixel radius of each heatpoint at the current map zoom
                if (_options.unit == "pixels") {
                    radiusInPixel = _options.radius;
                } else {
                    radiusInPixel = _options.radius / _map.getMetersPerPixel();
                }

                var ctx = _canvas.getContext("2d");

                // Convert lat/long to pixel location
                var pixlocs = _map.tryLocationToPixel(_locations, Microsoft.Maps.PixelReference.control);
                var shadow = 'rgba(0, 0, 0, ' + _options.intensity + ')';
                var mapWidth = 256 * Math.pow(2, _map.getZoom());

                // Create the Intensity Map by looping through each location
                for (var i = 0, len = pixlocs.length; i < len; i++) {
                    var x = pixlocs[i].x;
                    var y = pixlocs[i].y;

                    if (x < 0) {
                        x += mapWidth * Math.ceil(Math.abs(x / mapWidth));
                    }

                    // Create radial gradient centred on this point
                    var grd = ctx.createRadialGradient(x, y, 0, x, y, radiusInPixel);
                    grd.addColorStop(0.0, shadow);
                    grd.addColorStop(1.0, 'transparent');

                    // Draw the heatpoint onto the canvas
                    ctx.fillStyle = grd;
                    ctx.fillRect(x - radiusInPixel, y - radiusInPixel, 2 * radiusInPixel, 2 * radiusInPixel);
                }

                // Apply the specified colour gradient to the intensity map
                _colouriseHeatMap();

                // Call the callback function, if specified
                if (_options.callback) {
                    _options.callback();
                }
            }

            /* Public Methods */

            this.Show = function () {
                if (_canvas) {
                    _canvas.style.display = '';
                }
            };

            this.Hide = function () {
                if (_canvas) {
                    _canvas.style.display = 'none';
                }
            };

            // Sets options for intensity, radius, colourgradient etc.
            this.SetOptions = function (options) {
                _setOptions(options);
            }

            // Sets an array of Microsoft.Maps.Locations from which the heatmap is created
            this.SetPoints = function (locations) {
                // Reset the existing heatmap layer
                _clearHeatMap();
                // Pass in the new set of locations
                _setPoints(locations);
                // Recreate the layer
                _createHeatMap();
            }

            // Removes the heatmap layer from the DOM
            this.Remove = function () {
                _canvas.parentNode.parentNode.removeChild(_canvas.parentNode);

                if (_viewchangestarthandler) { Microsoft.Maps.Events.removeHandler(_viewchangestarthandler); }
                if (_viewchangeendhandler) { Microsoft.Maps.Events.removeHandler(_viewchangeendhandler); }

                _locations = null;
                _temperaturemap = null;
                _canvas = null;
                _options = null;
                _viewchangestarthandler = null;
                _viewchangeendhandler = null;
            }

            // Call the initialisation routine
            _init();
        };

        // Call the Module Loaded method
        Microsoft.Maps.moduleLoaded('HeatMapModule');

<span data-ttu-id="4ffee-218">**Per aggiungere twitterStream.js**</span><span class="sxs-lookup"><span data-stu-id="4ffee-218">**To add twitterStream.js**</span></span>

1. <span data-ttu-id="4ffee-219">In **Esplora soluzioni** espandere **TweetSentimentWeb**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-219">From **Solution Explorer**, expand **TweetSentimentWeb**.</span></span>
2. <span data-ttu-id="4ffee-220">Fare clic con il pulsante destro del mouse su **Script**, quindi scegliere **Aggiungi** e infine fare clic su **File JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-220">Right-click **Scripts**, click **Add**, click **JavaScript File**.</span></span>
3. <span data-ttu-id="4ffee-221">Nel campo **Nome elemento** digitare **twitterStream.js**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-221">In the **Item name** field, type**twitterStream.js**.</span></span>
4. <span data-ttu-id="4ffee-222">Copiare e incollare il seguente codice nel file:</span><span class="sxs-lookup"><span data-stu-id="4ffee-222">Copy and paste the following code into the file:</span></span>

        var liveTweetsPos = [];
        var liveTweets = [];
        var liveTweetsNeg = [];
        var map;
        var heatmap;
        var heatmapNeg;
        var heatmapPos;

        function initialize() {
            // Initialize the map
            var options = {
                credentials: "AvFJTZPZv8l3gF8VC3Y7BPBd0r7LKo8dqKG02EAlqg9WAi0M7la6zSIT-HwkMQbx",
                center: new Microsoft.Maps.Location(23.0, 8.0),
                mapTypeId: Microsoft.Maps.MapTypeId.ordnanceSurvey,
                labelOverlay: Microsoft.Maps.LabelOverlay.hidden,
                zoom: 2.5
            };
            var map = new Microsoft.Maps.Map(document.getElementById('map_canvas'), options);

            // Heatmap options for positive, neutral and negative layers

            var heatmapOptions = {
                // Opacity at the centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether the radius is an absolute pixel value or meters
                unit: 'pixels'
            };

            var heatmapPosOptions = {
                // Opacity at the centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether the radius is an absolute pixel value or meters
                unit: 'pixels',

                colourgradient: {
                    0.0: 'rgba(0, 255, 255, 0)',
                    0.1: 'rgba(0, 255, 255, 1)',
                    0.2: 'rgba(0, 255, 191, 1)',
                    0.3: 'rgba(0, 255, 127, 1)',
                    0.4: 'rgba(0, 255, 63, 1)',
                    0.5: 'rgba(0, 127, 0, 1)',
                    0.7: 'rgba(0, 159, 0, 1)',
                    0.8: 'rgba(0, 191, 0, 1)',
                    0.9: 'rgba(0, 223, 0, 1)',
                    1.0: 'rgba(0, 255, 0, 1)'
                }
            };

            var heatmapNegOptions = {
                // Opacity at the centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether the radius is an absolute pixel value or meters
                unit: 'pixels',

                colourgradient: {
                    0.0: 'rgba(0, 255, 255, 0)',
                    0.1: 'rgba(0, 255, 255, 1)',
                    0.2: 'rgba(0, 191, 255, 1)',
                    0.3: 'rgba(0, 127, 255, 1)',
                    0.4: 'rgba(0, 63, 255, 1)',
                    0.5: 'rgba(0, 0, 127, 1)',
                    0.7: 'rgba(0, 0, 159, 1)',
                    0.8: 'rgba(0, 0, 191, 1)',
                    0.9: 'rgba(0, 0, 223, 1)',
                    1.0: 'rgba(0, 0, 255, 1)'
                }
            };

            // Register and load the Client Side HeatMap Module
            Microsoft.Maps.registerModule("HeatMapModule", "scripts/heatmap.js");
            Microsoft.Maps.loadModule("HeatMapModule", {
                callback: function () {
                    // Create heatmap layers for positive, neutral and negative tweets
                    heatmapPos = new HeatMapLayer(map, liveTweetsPos, heatmapPosOptions);
                    heatmap = new HeatMapLayer(map, liveTweets, heatmapOptions);
                    heatmapNeg = new HeatMapLayer(map, liveTweetsNeg, heatmapNegOptions);
                }
            });

            $("#searchbox").val("xbox");
            $("#searchBtn").click(onsearch);
            $("#positiveBtn").click(onPositiveBtn);
            $("#negativeBtn").click(onNegativeBtn);
            $("#neutralBtn").click(onNeutralBtn);
            $("#neutralBtn").button("toggle");
        }

        function onsearch() {
            var uri = 'api/tweets?query=';
            var query = $('#searchbox').val();
            $.getJSON(uri + query)
                .done(function (data) {
                    liveTweetsPos = [];
                    liveTweets = [];
                    liveTweetsNeg = [];

                    // On success, 'data' contains a list of tweets.
                    $.each(data, function (key, item) {
                        addTweet(item);
                    });

                    if (!$("#neutralBtn").hasClass('active')) {
                        $("#neutralBtn").button("toggle");
                    }
                    onNeutralBtn();
                })
                .fail(function (jqXHR, textStatus, err) {
                    $('#statustext').text('Error: ' + err);
                });
        }

        function addTweet(item) {
            //Add tweet to the heat map arrays.
            var tweetLocation = new Microsoft.Maps.Location(item.Latitude, item.Longtitude);
            if (item.Sentiment > 0) {
                liveTweetsPos.push(tweetLocation);
            } else if (item.Sentiment < 0) {
                liveTweetsNeg.push(tweetLocation);
            } else {
                liveTweets.push(tweetLocation);
            }
        }

        function onPositiveBtn() {
            if ($("#neutralBtn").hasClass('active')) {
                $("#neutralBtn").button("toggle");
            }
            if ($("#negativeBtn").hasClass('active')) {
                $("#negativeBtn").button("toggle");
            }

            heatmapPos.SetPoints(liveTweetsPos);
            heatmapPos.Show();
            heatmapNeg.Hide();
            heatmap.Hide();

            $('#statustext').text('Tweets: ' + liveTweetsPos.length + "   " + getPosNegRatio());
        }

        function onNeutralBtn() {
            if ($("#positiveBtn").hasClass('active')) {
                $("#positiveBtn").button("toggle");
            }
            if ($("#negativeBtn").hasClass('active')) {
                $("#negativeBtn").button("toggle");
            }

            heatmap.SetPoints(liveTweets);
            heatmap.Show();
            heatmapNeg.Hide();
            heatmapPos.Hide();

            $('#statustext').text('Tweets: ' + liveTweets.length + "   " + getPosNegRatio());
        }

        function onNegativeBtn() {
            if ($("#positiveBtn").hasClass('active')) {
                $("#positiveBtn").button("toggle");
            }
            if ($("#neutralBtn").hasClass('active')) {
                $("#neutralBtn").button("toggle");
            }

            heatmapNeg.SetPoints(liveTweetsNeg);
            heatmapNeg.Show();
            heatmap.Hide();;
            heatmapPos.Hide();;

            $('#statustext').text('Tweets: ' + liveTweetsNeg.length + "\t" + getPosNegRatio());
        }

        function getPosNegRatio() {
            if (liveTweetsNeg.length == 0) {
                return "";
            }
            else {
                var ratio = liveTweetsPos.length / liveTweetsNeg.length;
                var str = parseFloat(Math.round(ratio * 10) / 10).toFixed(1);
                return "Positive/Negative Ratio: " + str;
            }
        }

<span data-ttu-id="4ffee-223">**Per modificare layout.cshtml**</span><span class="sxs-lookup"><span data-stu-id="4ffee-223">**To modify the layout.cshtml**</span></span>

1. <span data-ttu-id="4ffee-224">In **Esplora soluzioni**, espandere **TweetSentimentWeb**, espandere **Viste**, espandere **Condivise** e fare doppio clic su _**Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-224">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Views**, expand **Shared**, and then double-click _**Layout.cshtml**.</span></span>
2. <span data-ttu-id="4ffee-225">Sostituire il contenuto con i contenuti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ffee-225">Replace the content with the following:</span></span>

        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="utf-8" />
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>@ViewBag.Title</title>
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
            <!-- Bing Maps -->
            <script type="text/javascript" src="http://ecn.dev.virtualearth.net/mapcontrol/mapcontrol.ashx?v=7.0&mkt=en-gb"></script>
            <!-- Spatial Dashboard JavaScript -->
            <script src="~/Scripts/twitterStream.js" type="text/javascript"></script>
        </head>
        <body onload="initialize()">
            <div class="navbar navbar-inverse navbar-fixed-top">
                <div class="container">
                    <div class="navbar-header">
                        <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                        </button>
                    </div>
                    <div class="navbar-collapse collapse">
                        <div class="row">
                            <ul class="nav navbar-nav col-lg-5">
                                <li class="col-lg-12">
                                    <div class="navbar-form">
                                        <input id="searchbox" type="search" class="form-control">
                                        <button type="button" id="searchBtn" class="btn btn-primary">Go</button>
                                    </div>
                                </li>
                            </ul>
                            <ul class="nav navbar-nav col-lg-7">
                                <li>
                                    <div class="navbar-form">
                                        <div class="btn-group" data-toggle="buttons-radio">
                                            <button type="button" id="positiveBtn" class="btn btn-primary">Positive</button>
                                            <button type="button" id="neutralBtn" class="btn btn-primary">Neutral</button>
                                            <button type="button" id="negativeBtn" class="btn btn-primary">Negative</button>
                                        </div>
                                    </div>
                                </li>
                                <li><span id="statustext" class="navbar-text"></span></li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
            <div class="map_container">
                @RenderBody()
            </div>
            @Scripts.Render("~/bundles/jquery")
            @Scripts.Render("~/bundles/bootstrap")
            @RenderSection("scripts", required: false)
        </body>
        </html>

<span data-ttu-id="4ffee-226">**Per modificare Index.cshtml**</span><span class="sxs-lookup"><span data-stu-id="4ffee-226">**To modify the Index.cshtml**</span></span>

1. <span data-ttu-id="4ffee-227">In **Esplora soluzioni**, espandere **TweetSentimentWeb**, espandere **Viste**, espandere **Home** e fare doppio clic su _**Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-227">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Views**, expand **Home**, and then double-click **Index.cshtml**.</span></span>
2. <span data-ttu-id="4ffee-228">Sostituire il contenuto con i contenuti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ffee-228">Replace the content with the following:</span></span>

        @{
            ViewBag.Title = "Tweet Sentiment";
        }

        <div class="map_container">
            <div id="map_canvas"/>
        </div>

<span data-ttu-id="4ffee-229">**Per modificare il file site.css**</span><span class="sxs-lookup"><span data-stu-id="4ffee-229">**To modify the site.css file**</span></span>

1. <span data-ttu-id="4ffee-230">In **Esplora soluzioni**, espandere **TweetSentimentWeb**, espandere **Contenuto** e fare doppio clic su _**Site.css**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-230">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Content**, and then double-click **Site.css**.</span></span>
2. <span data-ttu-id="4ffee-231">Aggiungere il seguente codice al file:</span><span class="sxs-lookup"><span data-stu-id="4ffee-231">Append the following code to the file:</span></span>

        /* make container, and thus map, 100% width */
        .map_container {
            width: 100%;
            height: 100%;
        }

        #map_canvas{
          height:100%;
        }

        #tweets{
          position: absolute;
          top: 60px;
          left: 75px;
          z-index:1000;
          font-size: 30px;
        }

<span data-ttu-id="4ffee-232">**Per modificare il file global.asax**</span><span class="sxs-lookup"><span data-stu-id="4ffee-232">**To modify the global.asax file**</span></span>

1. <span data-ttu-id="4ffee-233">In **Esplora soluzioni**, espandere **TweetSentimentWeb** e fare doppio clic su _**Global.asax**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-233">From **Solution Explorer**, expand **TweetSentimentWeb**, and then double-click **Global.asax**.</span></span>
2. <span data-ttu-id="4ffee-234">Aggiungere l'istruzione **using** seguente:</span><span class="sxs-lookup"><span data-stu-id="4ffee-234">Add the following **using** statement:</span></span>

        using System.Web.Http;
3. <span data-ttu-id="4ffee-235">Aggiungere le seguenti righe all'interno della funzione **Application_Start()**:</span><span class="sxs-lookup"><span data-stu-id="4ffee-235">Add the following lines inside the **Application_Start()** function:</span></span>

        // Register API routes
        GlobalConfiguration.Configure(WebApiConfig.Register);

    <span data-ttu-id="4ffee-236">Modificare la registrazione delle route API per consentire il funzionamento del controller API Web all'interno dell'applicazione MVC.</span><span class="sxs-lookup"><span data-stu-id="4ffee-236">Modify the registration of the API routes to make the Web API controller work inside the MVC application.</span></span>

<span data-ttu-id="4ffee-237">**Per eseguire l'applicazione Web**</span><span class="sxs-lookup"><span data-stu-id="4ffee-237">**To run the web application**</span></span>

1. <span data-ttu-id="4ffee-238">Accertarsi che l'applicazione console di streaming sia ancora in esecuzione, in modo tale da visualizzare le modifiche in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="4ffee-238">Verify that the streaming service console application is still running so you can see the real-time changes.</span></span>
2. <span data-ttu-id="4ffee-239">Premere **F5** per eseguire l'applicazione Web:</span><span class="sxs-lookup"><span data-stu-id="4ffee-239">Press **F5** to run the web application:</span></span>

    ![hdinsight.hbase.twitter.sentiment.bing.map][img-bing-map]
3. <span data-ttu-id="4ffee-241">Immettere una parola chiave nella casella di testo, quindi fare clic su **Go**.</span><span class="sxs-lookup"><span data-stu-id="4ffee-241">In the text box, enter a keyword, and then click **Go**.</span></span>  <span data-ttu-id="4ffee-242">A seconda dei dati prelevati dalla tabella HBase, alcune parole chiave potrebbero non essere rilevate.</span><span class="sxs-lookup"><span data-stu-id="4ffee-242">Depending on the data collected in the HBase table, some keywords might not be found.</span></span> <span data-ttu-id="4ffee-243">Provare con parole chiavi comuni come "amore", xbox" e "playstation".</span><span class="sxs-lookup"><span data-stu-id="4ffee-243">Try some common keywords, such as "love," "xbox," and "playstation."</span></span>
4. <span data-ttu-id="4ffee-244">Selezionare **Positive** (Positivo), **Neutral** (Neutro) e **Negative** (Negativo) per confrontare i sentimenti sull'argomento.</span><span class="sxs-lookup"><span data-stu-id="4ffee-244">Toggle among **Positive**, **Neutral**, and **Negative** to compare sentiment on the subject.</span></span>
5. <span data-ttu-id="4ffee-245">Lasciare il servizio streaming in esecuzione per un'altra ora, quindi cercare le stesse parole chiave e confrontare i risultati.</span><span class="sxs-lookup"><span data-stu-id="4ffee-245">Let the streaming service run for another hour, and then search the same keywords, and compare the results.</span></span>

<span data-ttu-id="4ffee-246">In alternativa, è possibile distribuire l'applicazione in Siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ffee-246">Optionally, you can deploy the application to Azure Websites.</span></span> <span data-ttu-id="4ffee-247">Per le istruzioni vedere l'[introduzione ai siti Web di Azure e ASP.NET][website-get-started].</span><span class="sxs-lookup"><span data-stu-id="4ffee-247">For instructions, see [Get started with Azure Websites and ASP.NET][website-get-started].</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ffee-248">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4ffee-248">Next Steps</span></span>
<span data-ttu-id="4ffee-249">In questa esercitazione si è appreso come ricevere tweet, analizzare i sentimenti dei tweet, salvare i dati sui sentimenti su HBase e presentare i dati sui sentimenti di Twitter in tempo reale sulle mappe Bing.</span><span class="sxs-lookup"><span data-stu-id="4ffee-249">In this tutorial, you learned how to get tweets, analyze the sentiment of tweets, save the sentiment data to HBase, and present the real-time Twitter sentiment data to Bing maps.</span></span> <span data-ttu-id="4ffee-250">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="4ffee-250">To learn more, see:</span></span>

* <span data-ttu-id="4ffee-251">[Introduzione a HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="4ffee-251">[Get started with HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="4ffee-252">Configurare la replica di HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ffee-252">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* <span data-ttu-id="4ffee-253">[Analizzare i dati di Twitter con Hadoop in HDInsight][hdinsight-analyze-twitter-data]</span><span class="sxs-lookup"><span data-stu-id="4ffee-253">[Analyze Twitter data with Hadoop in HDInsight][hdinsight-analyze-twitter-data]</span></span>
* <span data-ttu-id="4ffee-254">[Analizzare i dati sui ritardi dei voli con HDInsight][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="4ffee-254">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="4ffee-255">[Sviluppare programmi MapReduce Java per HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="4ffee-255">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[website-get-started]: ../app-service-web/app-service-web-get-started-dotnet.md



[img-app-arch]: ./media/hdinsight-hbase-analyze-twitter-sentiment/AppArchitecture.png
[img-twitter-app]: ./media/hdinsight-hbase-analyze-twitter-sentiment/TwitterApp.png
[img-streaming-service]: ./media/hdinsight-hbase-analyze-twitter-sentiment/StreamingService.png
[img-bing-map]: ./media/hdinsight-hbase-analyze-twitter-sentiment/TwitterSentimentBingMap.png



[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-analyze-twitter-data]: hdinsight-analyze-twitter-data.md




[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
