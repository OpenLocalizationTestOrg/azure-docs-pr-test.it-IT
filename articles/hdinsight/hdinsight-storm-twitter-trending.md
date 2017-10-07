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
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a>Determinare i temi di tendenza Twitter con Apache Storm in HDInsight

Informazioni su come toouse Trident toocreate una topologia di Storm che determina analisi delle tendenze di argomenti (tag hash) su Twitter.

Trident è un'astrazione generale che fornisce strumenti quali join, aggregazioni, raggruppamento, funzioni e filtri. Trident fornisce inoltre primitive per l'elaborazione incrementale e con informazioni sullo stato. esempio Hello utilizzato in questo documento è una topologia Trident con un beccuccio personalizzato e una funzione. Vengono inoltre usate diverse funzioni predefinite offerte da Trident.

## <a name="requirements"></a>Requisiti

* <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java e hello 1.8 JDK</a>

* <a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a>

* <a href="http://git-scm.com/" target="_blank">Git</a>

* Un account sviluppatore Twitter

## <a name="download-hello-project"></a>Scaricare il progetto hello

Utilizzare hello seguente progetto hello tooclone di codice in locale.

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a>Informazioni sulla topologia di hello

esempio Hello diagramma mostra il flusso dei dati tramite questa topologia:

![Topologia](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> Questo diagramma è una visualizzazione semplificata della topologia hello. Più istanze dei componenti di hello vengono distribuite tra i nodi nel cluster hello hello.


Hello codice Trident che implementa la topologia hello è indicato di seguito:

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

Questo codice vengono eseguite hello seguenti azioni:

1. Crea un flusso da beccuccio hello. beccuccio Hello recupera TWEET da Twitter e consente di filtrare per parole chiave specifiche (piace, musica e caffè in questo esempio).

2. HashtagExtractor, una funzione personalizzata, è tag hash tooextract utilizzati da ogni tweet. i tag di hash Hello sono flusso toohello generato.

3. flusso Hello è raggruppato mediante tag di hash e passato tooan aggregator. L'aggregatore crea un conteggio delle occorrenze di ciascun hashtag, informazione che viene mantenuta in memoria. Infine, viene generato un nuovo flusso che contiene tag hash hello e conteggio hello.

4. Hello **FirstN** assembly viene applicato tooreturn solo hello primi 10 valori in base a campo del conteggio hello.

> [!NOTE]
> Per ulteriori informazioni sull'uso di Trident, vedere hello [panoramica dell'API Trident](http://storm.apache.org/releases/current/Trident-API-Overview.html) documento.

### <a name="hello-spout"></a>beccuccio Hello

beccuccio Hello, **TwitterSpout**, Usa [Twitter4j](http://twitter4j.org/en/) tweets tooretrieve da Twitter. Viene creato un filtro le parole hello __AMO__, **musica**, e **coffee**. TWEET in ingresso (stato) che corrispondono al filtro hello vengono archiviati in una coda di blocco collegata. Infine, gli elementi vengono estratti dalla coda hello e generato toohello topologia.

### <a name="hello-hashtagextractor"></a>Hello HashtagExtractor

tag di hash tooextract, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) è tooretrieve utilizzati tutti i tag contenuti in tweet hello hash. Questi sono quindi flusso toohello generato.

## <a name="configure-twitter"></a>Configurare Twitter

Utilizzare i seguenti passaggi tooregister una nuova applicazione Twitter hello e ottenere hello consumer e l'accesso tooread di informazioni sul token necessite da Twitter:

1. Andare troppo[Twitter app](https://apps.twitter.com) e fare clic su hello **Crea nuova applicazione** pulsante. Durante la compilazione nel modulo hello, lasciare hello **URL Callback** campo vuoto.

2. Quando viene creato l'applicazione hello, fare clic su hello **chiavi e i token di accesso** scheda.

3. Hello copia **chiave Consumer** e **segreto del cliente** informazioni.

4. Nella parte inferiore di hello della pagina hello, selezionare **creare il token di accesso** se è presente alcun token. Quando sono stati creati i token hello, hello copia **Token di accesso** e **segreto del Token di accesso** informazioni.

5. In hello **TwitterSpoutTopology** progetto hello clonato in precedenza, aprire **resources/twitter4j.properties** file, aggiungere informazioni hello raccolte nei passaggi precedenti hello e quindi salvare il file hello .

## <a name="build-hello-topology"></a>Creare una topologia di hello

Utilizzare hello progetto hello toobuild di codice seguente:

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a>Topologia hello test

Utilizzare hello localmente topologia di hello tootest comando seguente:

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

Dopo l'avvio della topologia di hello, si noterà informazioni di debug che contiene l'hash hello tag e conta generate dalla topologia hello. output di Hello risulterà simile toohello seguente testo:

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a>Passaggi successivi

Ora che il test di topologia hello localmente, individuare la modalità toodeploy hello topologia: [distribuire e gestire le topologie di Apache Storm in HDInsight](hdinsight-storm-deploy-monitor-topology.md).

Può anche essere interessante hello seguenti Storm argomenti:

* [Sviluppare topologie Java per Storm in HDInsight con Maven](hdinsight-storm-develop-java-topology.md)
* [Sviluppare topologie C# per Storm in HDInsight con Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Per altri esempi su Storm per HDinsight:

* [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md)

