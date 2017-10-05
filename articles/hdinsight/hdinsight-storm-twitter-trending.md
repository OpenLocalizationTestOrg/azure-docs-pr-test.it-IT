---
title: Temi di tendenza Twitter con Apache Storm in HDInsight | Documentazione Microsoft
description: Informazioni su come usare Trident per creare una topologia Apache Storm in grado di determinare i temi di tendenza in base agli hashtag Twitter.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 63b280ea-5c07-4dc8-a35f-dccf5a96ba93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: d588221586f151319436525c5098b0bb2694e5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="f861a-103">Determinare i temi di tendenza Twitter con Apache Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f861a-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="f861a-104">Informazioni su come usare Trident per creare una topologia Storm in grado di determinare i temi di tendenza (hashtag) in Twitter.</span><span class="sxs-lookup"><span data-stu-id="f861a-104">Learn how to use Trident to create a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="f861a-105">Trident è un'astrazione generale che fornisce strumenti quali join, aggregazioni, raggruppamento, funzioni e filtri.</span><span class="sxs-lookup"><span data-stu-id="f861a-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="f861a-106">Trident fornisce inoltre primitive per l'elaborazione incrementale e con informazioni sullo stato.</span><span class="sxs-lookup"><span data-stu-id="f861a-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="f861a-107">L'esempio usato in questo documento è una topologia Trident con un spout personalizzato e una funzione.</span><span class="sxs-lookup"><span data-stu-id="f861a-107">The example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="f861a-108">Vengono inoltre usate diverse funzioni predefinite offerte da Trident.</span><span class="sxs-lookup"><span data-stu-id="f861a-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="f861a-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="f861a-109">Requirements</span></span>

* <span data-ttu-id="f861a-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java e JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="f861a-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and the JDK 1.8</a></span></span>

* <span data-ttu-id="f861a-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="f861a-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="f861a-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="f861a-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="f861a-113">Un account sviluppatore Twitter</span><span class="sxs-lookup"><span data-stu-id="f861a-113">A Twitter developer account</span></span>

## <a name="download-the-project"></a><span data-ttu-id="f861a-114">Scaricare il progetto</span><span class="sxs-lookup"><span data-stu-id="f861a-114">Download the project</span></span>

<span data-ttu-id="f861a-115">Usare il codice seguente per clonare il progetto in locale.</span><span class="sxs-lookup"><span data-stu-id="f861a-115">Use the following code to clone the project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-the-topology"></a><span data-ttu-id="f861a-116">Informazioni sulla topologia</span><span class="sxs-lookup"><span data-stu-id="f861a-116">Understanding the topology</span></span>

<span data-ttu-id="f861a-117">Il diagramma seguente mostra il flusso dei dati tramite questa topologia:</span><span class="sxs-lookup"><span data-stu-id="f861a-117">The following diagram shows of how data flows through this topology:</span></span>

![Topologia](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="f861a-119">Questo diagramma è una visualizzazione semplificata della topologia.</span><span class="sxs-lookup"><span data-stu-id="f861a-119">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="f861a-120">Tra i nodi del cluster vengono distribuite più istanze dei componenti.</span><span class="sxs-lookup"><span data-stu-id="f861a-120">Multiple instances of the components are distributed across the nodes in the cluster.</span></span>


<span data-ttu-id="f861a-121">Il codice Trident che implementa la topologia è il seguente:</span><span class="sxs-lookup"><span data-stu-id="f861a-121">The Trident code that implements the topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="f861a-122">Il codice esegue le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f861a-122">This code performs the following actions:</span></span>

1. <span data-ttu-id="f861a-123">Crea un nuovo flusso dallo spout.</span><span class="sxs-lookup"><span data-stu-id="f861a-123">Creates a stream from the spout.</span></span> <span data-ttu-id="f861a-124">Lo spout recupera tweet da Twitter filtrandoli in base a parole chiave specifiche. In questo esempio, si tratta delle parole amore, musica e caffè.</span><span class="sxs-lookup"><span data-stu-id="f861a-124">The spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="f861a-125">Uso della funzione personalizzata HashtagExtractor per estrarre gli hashtag da ciascun tweet.</span><span class="sxs-lookup"><span data-stu-id="f861a-125">HashtagExtractor, a custom function, is used to extract hash tags from each tweet.</span></span> <span data-ttu-id="f861a-126">Gli hashtag vengono indirizzati al flusso.</span><span class="sxs-lookup"><span data-stu-id="f861a-126">The hash tags are emitted to the stream.</span></span>

3. <span data-ttu-id="f861a-127">Raggruppamento del flusso in base agli hashtag e passaggio a un aggregatore.</span><span class="sxs-lookup"><span data-stu-id="f861a-127">The stream is grouped by hash tag, and passed to an aggregator.</span></span> <span data-ttu-id="f861a-128">L'aggregatore crea un conteggio delle occorrenze di ciascun hashtag,</span><span class="sxs-lookup"><span data-stu-id="f861a-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="f861a-129">informazione che viene mantenuta in memoria.</span><span class="sxs-lookup"><span data-stu-id="f861a-129">This data is persisted in memory.</span></span> <span data-ttu-id="f861a-130">Al termine viene generato un nuovo flusso contenente l'hashtag e la relativa frequenza.</span><span class="sxs-lookup"><span data-stu-id="f861a-130">Finally, a new stream is emitted that contains the hash tag and the count.</span></span>

4. <span data-ttu-id="f861a-131">L'assembly **FirstN** viene applicato per restituire solo i primi 10 valori, in base al campo Conteggio.</span><span class="sxs-lookup"><span data-stu-id="f861a-131">The **FirstN** assembly is applied to return only the top 10 values, based on the count field.</span></span>

> [!NOTE]
> <span data-ttu-id="f861a-132">Per altre informazioni su Trident, vedere il documento [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) (Panoramica dell'API Trident).</span><span class="sxs-lookup"><span data-stu-id="f861a-132">For more information on working with Trident, see the [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="the-spout"></a><span data-ttu-id="f861a-133">Spout</span><span class="sxs-lookup"><span data-stu-id="f861a-133">The spout</span></span>

<span data-ttu-id="f861a-134">Lo spout, **TwitterSpout**, usa [Twitter4j](http://twitter4j.org/en/) per recuperare tweet da Twitter.</span><span class="sxs-lookup"><span data-stu-id="f861a-134">The spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) to retrieve tweets from Twitter.</span></span> <span data-ttu-id="f861a-135">Viene creato un filtro per le parole __amore__, **musica** e **caffè**.</span><span class="sxs-lookup"><span data-stu-id="f861a-135">A filter is created for the words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="f861a-136">I tweet in arrivo (stato) che corrispondono al filtro vengono archiviati in una coda di blocco collegata.</span><span class="sxs-lookup"><span data-stu-id="f861a-136">Incoming tweets (status) that match the filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="f861a-137">Al termine, gli elementi vengono rimossi dalla coda e inseriti nella topologia.</span><span class="sxs-lookup"><span data-stu-id="f861a-137">Finally, items are pulled off the queue and emitted to the topology.</span></span>

### <a name="the-hashtagextractor"></a><span data-ttu-id="f861a-138">HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="f861a-138">The HashtagExtractor</span></span>

<span data-ttu-id="f861a-139">Per estrarre gli hashtag, usare [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) per recuperare tutti gli hashtag contenuti nel tweet.</span><span class="sxs-lookup"><span data-stu-id="f861a-139">To extract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used to retrieve all hash tags that are contained in the tweet.</span></span> <span data-ttu-id="f861a-140">Gli hashtag vengono quindi indirizzati nel flusso.</span><span class="sxs-lookup"><span data-stu-id="f861a-140">These are then emitted to the stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="f861a-141">Configurare Twitter</span><span class="sxs-lookup"><span data-stu-id="f861a-141">Configure Twitter</span></span>

<span data-ttu-id="f861a-142">Per registrare una nuova applicazione Twitter e ottenere informazioni sull'utente e sul token di accesso necessarie per leggere da Twitter, effettuare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f861a-142">Use the following steps to register a new Twitter application and obtain the consumer and access token information needed to read from Twitter:</span></span>

1. <span data-ttu-id="f861a-143">Passare a [Twitter Apps](https://apps.twitter.com) (App Twitter) e quindi fare clic sul pulsante **Create new app** (Crea nuova app).</span><span class="sxs-lookup"><span data-stu-id="f861a-143">Go to [Twitter Apps](https://apps.twitter.com) and click the **Create new app** button.</span></span> <span data-ttu-id="f861a-144">Quando si compila il modulo, lasciare il campo **Callback URL** vuoto.</span><span class="sxs-lookup"><span data-stu-id="f861a-144">When filling in the form, leave the **Callback URL** field empty.</span></span>

2. <span data-ttu-id="f861a-145">Quando l'app viene creata, fare clic sulla scheda **Keys and Access Tokens** .</span><span class="sxs-lookup"><span data-stu-id="f861a-145">When the app is created, click the **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="f861a-146">Copiare le informazioni **Consumer Key** (Chiave utente) e **Consumer Secret** (Segreto utente).</span><span class="sxs-lookup"><span data-stu-id="f861a-146">Copy the **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="f861a-147">Se non è disponibile alcun token, selezionare **Create my access token** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="f861a-147">At the bottom of the page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="f861a-148">Dopo aver creato i token, copiare le informazioni **Access Token** (Token di accesso) e **Access Token Secret** (Segreto del token di accesso).</span><span class="sxs-lookup"><span data-stu-id="f861a-148">When the tokens have been created, copy the **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="f861a-149">Nel progetto **TwitterSpoutTopology** clonato in precedenza aprire il file **resources/twitter4j.properties**, aggiungere le informazioni copiate nei passaggi precedenti e salvare il file.</span><span class="sxs-lookup"><span data-stu-id="f861a-149">In the **TwitterSpoutTopology** project you previously cloned, open the **resources/twitter4j.properties** file, add the information you gathered in the previous steps, and then save the file.</span></span>

## <a name="build-the-topology"></a><span data-ttu-id="f861a-150">Creare la topologia</span><span class="sxs-lookup"><span data-stu-id="f861a-150">Build the topology</span></span>

<span data-ttu-id="f861a-151">Per creare il progetto, usare il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="f861a-151">Use the following code to build the project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-the-topology"></a><span data-ttu-id="f861a-152">Testare la topologia</span><span class="sxs-lookup"><span data-stu-id="f861a-152">Test the topology</span></span>

<span data-ttu-id="f861a-153">Per testare la topologia in locale, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="f861a-153">Use the following command to test the topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="f861a-154">Dopo l'avvio della topologia, vengono visualizzate informazioni di debug contenenti gli hashtag e i conteggi generati dalla topologia stessa.</span><span class="sxs-lookup"><span data-stu-id="f861a-154">After the topology starts, you should see debug information that contains the hash tags and counts emitted by the topology.</span></span> <span data-ttu-id="f861a-155">L'output sarà simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="f861a-155">The output should appear similar to the following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="f861a-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f861a-156">Next steps</span></span>

<span data-ttu-id="f861a-157">Dopo aver eseguito il test della topologia in locale, è possibile apprendere come distribuire la topologia. Vedere l'articolo [Distribuire e gestire topologie Apache Storm in HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="f861a-157">Now that you have tested the topology locally, discover how to deploy the topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="f861a-158">Altri argomenti di interesse:</span><span class="sxs-lookup"><span data-stu-id="f861a-158">You may also be interested in the following Storm topics:</span></span>

* [<span data-ttu-id="f861a-159">Sviluppare topologie Java per Storm in HDInsight con Maven</span><span class="sxs-lookup"><span data-stu-id="f861a-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="f861a-160">Sviluppare topologie C# per Storm in HDInsight con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f861a-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="f861a-161">Per altri esempi su Storm per HDinsight:</span><span class="sxs-lookup"><span data-stu-id="f861a-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="f861a-162">Topologie di esempio per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f861a-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

