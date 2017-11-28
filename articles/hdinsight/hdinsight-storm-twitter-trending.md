---
title: argomenti relativi alle tendenze di aaaTwitter con Apache Storm in HDInsight | Documenti Microsoft
description: Informazioni su come toouse Trident toocreate una topologia di Apache Storm che determina gli argomenti relativi alle tendenze su Twitter basate sulla hashtag.
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
ms.openlocfilehash: 0281b495d10833c63868b36856c96369b139c553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="9871f-103">Determinare i temi di tendenza Twitter con Apache Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9871f-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="9871f-104">Informazioni su come toouse Trident toocreate una topologia di Storm che determina analisi delle tendenze di argomenti (tag hash) su Twitter.</span><span class="sxs-lookup"><span data-stu-id="9871f-104">Learn how toouse Trident toocreate a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="9871f-105">Trident è un'astrazione generale che fornisce strumenti quali join, aggregazioni, raggruppamento, funzioni e filtri.</span><span class="sxs-lookup"><span data-stu-id="9871f-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="9871f-106">Trident fornisce inoltre primitive per l'elaborazione incrementale e con informazioni sullo stato.</span><span class="sxs-lookup"><span data-stu-id="9871f-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="9871f-107">esempio Hello utilizzato in questo documento è una topologia Trident con un beccuccio personalizzato e una funzione.</span><span class="sxs-lookup"><span data-stu-id="9871f-107">hello example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="9871f-108">Vengono inoltre usate diverse funzioni predefinite offerte da Trident.</span><span class="sxs-lookup"><span data-stu-id="9871f-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="9871f-109">Requisiti</span><span class="sxs-lookup"><span data-stu-id="9871f-109">Requirements</span></span>

* <span data-ttu-id="9871f-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java e hello 1.8 JDK</a></span><span class="sxs-lookup"><span data-stu-id="9871f-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and hello JDK 1.8</a></span></span>

* <span data-ttu-id="9871f-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="9871f-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="9871f-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="9871f-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="9871f-113">Un account sviluppatore Twitter</span><span class="sxs-lookup"><span data-stu-id="9871f-113">A Twitter developer account</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="9871f-114">Scaricare il progetto hello</span><span class="sxs-lookup"><span data-stu-id="9871f-114">Download hello project</span></span>

<span data-ttu-id="9871f-115">Utilizzare hello seguente progetto hello tooclone di codice in locale.</span><span class="sxs-lookup"><span data-stu-id="9871f-115">Use hello following code tooclone hello project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a><span data-ttu-id="9871f-116">Informazioni sulla topologia di hello</span><span class="sxs-lookup"><span data-stu-id="9871f-116">Understanding hello topology</span></span>

<span data-ttu-id="9871f-117">esempio Hello diagramma mostra il flusso dei dati tramite questa topologia:</span><span class="sxs-lookup"><span data-stu-id="9871f-117">hello following diagram shows of how data flows through this topology:</span></span>

![Topologia](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="9871f-119">Questo diagramma è una visualizzazione semplificata della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="9871f-119">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="9871f-120">Più istanze dei componenti di hello vengono distribuite tra i nodi nel cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="9871f-120">Multiple instances of hello components are distributed across hello nodes in hello cluster.</span></span>


<span data-ttu-id="9871f-121">Hello codice Trident che implementa la topologia hello è indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9871f-121">hello Trident code that implements hello topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="9871f-122">Questo codice vengono eseguite hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="9871f-122">This code performs hello following actions:</span></span>

1. <span data-ttu-id="9871f-123">Crea un flusso da beccuccio hello.</span><span class="sxs-lookup"><span data-stu-id="9871f-123">Creates a stream from hello spout.</span></span> <span data-ttu-id="9871f-124">beccuccio Hello recupera TWEET da Twitter e consente di filtrare per parole chiave specifiche (piace, musica e caffè in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="9871f-124">hello spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="9871f-125">HashtagExtractor, una funzione personalizzata, è tag hash tooextract utilizzati da ogni tweet.</span><span class="sxs-lookup"><span data-stu-id="9871f-125">HashtagExtractor, a custom function, is used tooextract hash tags from each tweet.</span></span> <span data-ttu-id="9871f-126">i tag di hash Hello sono flusso toohello generato.</span><span class="sxs-lookup"><span data-stu-id="9871f-126">hello hash tags are emitted toohello stream.</span></span>

3. <span data-ttu-id="9871f-127">flusso Hello è raggruppato mediante tag di hash e passato tooan aggregator.</span><span class="sxs-lookup"><span data-stu-id="9871f-127">hello stream is grouped by hash tag, and passed tooan aggregator.</span></span> <span data-ttu-id="9871f-128">L'aggregatore crea un conteggio delle occorrenze di ciascun hashtag,</span><span class="sxs-lookup"><span data-stu-id="9871f-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="9871f-129">informazione che viene mantenuta in memoria.</span><span class="sxs-lookup"><span data-stu-id="9871f-129">This data is persisted in memory.</span></span> <span data-ttu-id="9871f-130">Infine, viene generato un nuovo flusso che contiene tag hash hello e conteggio hello.</span><span class="sxs-lookup"><span data-stu-id="9871f-130">Finally, a new stream is emitted that contains hello hash tag and hello count.</span></span>

4. <span data-ttu-id="9871f-131">Hello **FirstN** assembly viene applicato tooreturn solo hello primi 10 valori in base a campo del conteggio hello.</span><span class="sxs-lookup"><span data-stu-id="9871f-131">hello **FirstN** assembly is applied tooreturn only hello top 10 values, based on hello count field.</span></span>

> [!NOTE]
> <span data-ttu-id="9871f-132">Per ulteriori informazioni sull'uso di Trident, vedere hello [panoramica dell'API Trident](http://storm.apache.org/releases/current/Trident-API-Overview.html) documento.</span><span class="sxs-lookup"><span data-stu-id="9871f-132">For more information on working with Trident, see hello [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="hello-spout"></a><span data-ttu-id="9871f-133">beccuccio Hello</span><span class="sxs-lookup"><span data-stu-id="9871f-133">hello spout</span></span>

<span data-ttu-id="9871f-134">beccuccio Hello, **TwitterSpout**, Usa [Twitter4j](http://twitter4j.org/en/) tweets tooretrieve da Twitter.</span><span class="sxs-lookup"><span data-stu-id="9871f-134">hello spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets from Twitter.</span></span> <span data-ttu-id="9871f-135">Viene creato un filtro le parole hello __AMO__, **musica**, e **coffee**.</span><span class="sxs-lookup"><span data-stu-id="9871f-135">A filter is created for hello words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="9871f-136">TWEET in ingresso (stato) che corrispondono al filtro hello vengono archiviati in una coda di blocco collegata.</span><span class="sxs-lookup"><span data-stu-id="9871f-136">Incoming tweets (status) that match hello filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="9871f-137">Infine, gli elementi vengono estratti dalla coda hello e generato toohello topologia.</span><span class="sxs-lookup"><span data-stu-id="9871f-137">Finally, items are pulled off hello queue and emitted toohello topology.</span></span>

### <a name="hello-hashtagextractor"></a><span data-ttu-id="9871f-138">Hello HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="9871f-138">hello HashtagExtractor</span></span>

<span data-ttu-id="9871f-139">tag di hash tooextract, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) è tooretrieve utilizzati tutti i tag contenuti in tweet hello hash.</span><span class="sxs-lookup"><span data-stu-id="9871f-139">tooextract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used tooretrieve all hash tags that are contained in hello tweet.</span></span> <span data-ttu-id="9871f-140">Questi sono quindi flusso toohello generato.</span><span class="sxs-lookup"><span data-stu-id="9871f-140">These are then emitted toohello stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="9871f-141">Configurare Twitter</span><span class="sxs-lookup"><span data-stu-id="9871f-141">Configure Twitter</span></span>

<span data-ttu-id="9871f-142">Utilizzare i seguenti passaggi tooregister una nuova applicazione Twitter hello e ottenere hello consumer e l'accesso tooread di informazioni sul token necessite da Twitter:</span><span class="sxs-lookup"><span data-stu-id="9871f-142">Use hello following steps tooregister a new Twitter application and obtain hello consumer and access token information needed tooread from Twitter:</span></span>

1. <span data-ttu-id="9871f-143">Andare troppo[Twitter app](https://apps.twitter.com) e fare clic su hello **Crea nuova applicazione** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9871f-143">Go too[Twitter Apps](https://apps.twitter.com) and click hello **Create new app** button.</span></span> <span data-ttu-id="9871f-144">Durante la compilazione nel modulo hello, lasciare hello **URL Callback** campo vuoto.</span><span class="sxs-lookup"><span data-stu-id="9871f-144">When filling in hello form, leave hello **Callback URL** field empty.</span></span>

2. <span data-ttu-id="9871f-145">Quando viene creato l'applicazione hello, fare clic su hello **chiavi e i token di accesso** scheda.</span><span class="sxs-lookup"><span data-stu-id="9871f-145">When hello app is created, click hello **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="9871f-146">Hello copia **chiave Consumer** e **segreto del cliente** informazioni.</span><span class="sxs-lookup"><span data-stu-id="9871f-146">Copy hello **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="9871f-147">Nella parte inferiore di hello della pagina hello, selezionare **creare il token di accesso** se è presente alcun token.</span><span class="sxs-lookup"><span data-stu-id="9871f-147">At hello bottom of hello page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="9871f-148">Quando sono stati creati i token hello, hello copia **Token di accesso** e **segreto del Token di accesso** informazioni.</span><span class="sxs-lookup"><span data-stu-id="9871f-148">When hello tokens have been created, copy hello **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="9871f-149">In hello **TwitterSpoutTopology** progetto hello clonato in precedenza, aprire **resources/twitter4j.properties** file, aggiungere informazioni hello raccolte nei passaggi precedenti hello e quindi salvare il file hello .</span><span class="sxs-lookup"><span data-stu-id="9871f-149">In hello **TwitterSpoutTopology** project you previously cloned, open hello **resources/twitter4j.properties** file, add hello information you gathered in hello previous steps, and then save hello file.</span></span>

## <a name="build-hello-topology"></a><span data-ttu-id="9871f-150">Creare una topologia di hello</span><span class="sxs-lookup"><span data-stu-id="9871f-150">Build hello topology</span></span>

<span data-ttu-id="9871f-151">Utilizzare hello progetto hello toobuild di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="9871f-151">Use hello following code toobuild hello project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a><span data-ttu-id="9871f-152">Topologia hello test</span><span class="sxs-lookup"><span data-stu-id="9871f-152">Test hello topology</span></span>

<span data-ttu-id="9871f-153">Utilizzare hello localmente topologia di hello tootest comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9871f-153">Use hello following command tootest hello topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="9871f-154">Dopo l'avvio della topologia di hello, si noterà informazioni di debug che contiene l'hash hello tag e conta generate dalla topologia hello.</span><span class="sxs-lookup"><span data-stu-id="9871f-154">After hello topology starts, you should see debug information that contains hello hash tags and counts emitted by hello topology.</span></span> <span data-ttu-id="9871f-155">output di Hello risulterà simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="9871f-155">hello output should appear similar toohello following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="9871f-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9871f-156">Next steps</span></span>

<span data-ttu-id="9871f-157">Ora che il test di topologia hello localmente, individuare la modalità toodeploy hello topologia: [distribuire e gestire le topologie di Apache Storm in HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="9871f-157">Now that you have tested hello topology locally, discover how toodeploy hello topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="9871f-158">Può anche essere interessante hello seguenti Storm argomenti:</span><span class="sxs-lookup"><span data-stu-id="9871f-158">You may also be interested in hello following Storm topics:</span></span>

* [<span data-ttu-id="9871f-159">Sviluppare topologie Java per Storm in HDInsight con Maven</span><span class="sxs-lookup"><span data-stu-id="9871f-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="9871f-160">Sviluppare topologie C# per Storm in HDInsight con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9871f-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="9871f-161">Per altri esempi su Storm per HDinsight:</span><span class="sxs-lookup"><span data-stu-id="9871f-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="9871f-162">Topologie di esempio per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9871f-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

