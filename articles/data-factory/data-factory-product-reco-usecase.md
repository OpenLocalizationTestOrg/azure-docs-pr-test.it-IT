---
title: aaaData caso d'uso Factory - consigli sui prodotti
description: Descrizione di un caso d'uso implementato usando Data factory di Azure e altri servizi.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6f1523c7-46c3-4b8d-9ed6-b847ae5ec4ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: d7912965fe4762d64e8ca3c28381ea6187f36631
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---product-recommendations"></a>Caso d'uso - Consigli sui prodotti
Data Factory di Azure è uno dei molti servizi utilizzati tooimplement hello Cortana Intelligence Suite di acceleratori.  Per i dettagli sulla suite, vedere la pagina [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics) . Questo documento descrive un caso d'uso comune risolto e implementato da alcuni utenti di Azure usando Azure Data Factory e altri servizi del componente Cortana Intelligence.

## <a name="scenario"></a>Scenario
Rivenditori online desidera comunemente tooentice toopurchase prodotti ai clienti con la visualizzazione con prodotti che sono probabilmente toobe interessati e toobuy pertanto più probabile. tooaccomplish, i rivenditori online necessitano toocustomize esperienza online dell'utente tramite consigli sui prodotti personalizzati per l'utente specifico. Questi consigli personalizzati sono toobe basarsi sui dati correnti e cronologici acquisti comportamento, informazioni sul prodotto, appena introdotti marchi e i dati di segmentazione tecnico e clienti.  Inoltre, possono fornire consigli sui prodotti utente hello basate sull'analisi del comportamento di utilizzo generale da tutti gli utenti combinati.

obiettivo di Hello di questi rivenditori è toooptimize per le conversioni di utente di fare clic su di vendita e ottenere maggiore dei ricavi delle vendite.  Per raggiungere questa conversione, forniscono consigli sui prodotti contestuali e basati sul comportamento, messi a punto a partire dagli interessi e dalle azioni dei clienti. In questo caso, utilizzare utilizziamo rivenditori online come esempio di aziende che desiderano toooptimize per i loro clienti. Tuttavia, tali principi applicano business tooany che desidera tooengage clienti intorno propri prodotti e servizi e migliorano l'esperienza di acquisto dei clienti con consigli sui prodotti personalizzati.

## <a name="challenges"></a>Problematiche
Esistono numerose problematiche che devono affrontare la distribuzione in linea durante il tentativo di questo tipo di caso d'uso tooimplement. 

In primo luogo, i dati di diverse dimensioni e le forme devono essere acquisiti da più origini dati, sia in locale e nel cloud hello. Questi dati includono dati di prodotto, dati sul comportamento di cliente cronologici e dati utente come utente di hello visita il sito di vendita al dettaglio online hello. 

In secondo luogo, devono elaborare e prevedere in modo ragionevole e accurato consigli personalizzati sui prodotti. Inoltre rivenditori online tooproduct, marchio e comportamento e i browser i dati dei clienti, nonché tooinclude suggerimenti dei clienti nei precedenti toofactor acquisti nella determinazione hello dei consigli sui prodotti migliori hello per utente hello. 

In terzo luogo, indicazioni hello devono essere immediatamente risultato finale toohello utente tooprovide un'esplorazione semplice ed esperienza di acquisto e fornire indicazioni più recenti e rilevanti di hello. 

Infine, i rivenditori necessario efficacia hello toomeasure dell'approccio rilevando incentivare complessivo cross-selling successi di vendita per fare clic su di conversione e regolare tootheir future indicazioni.

## <a name="solution-overview"></a>Panoramica della soluzione
Questo caso d'uso di esempio è stato risolto e implementato da utenti reali di Azure usando Azure Data Factory e altri servizi del componente Cortana Intelligence, tra cui [HDInsight](https://azure.microsoft.com/services/hdinsight/) e [Power BI](https://powerbi.microsoft.com/).

punto vendita online Hello utilizza un archivio Blob di Azure, un server SQL locale, database SQL di Azure e un data mart relazionale come le opzioni di archiviazione di dati nel corso del flusso di lavoro di hello.  archivio blob Hello contiene informazioni sul cliente, i dati sul comportamento di clienti e i dati di informazioni prodotto. informazioni sul prodotto Hello dati includono informazioni sul marchio di prodotto e un catalogo prodotti archiviata in locale in un data warehouse SQL. 

Tutti i dati di hello sono combinate e vengono inseriti in un prodotto raccomandazione sistema toodeliver personalizzati raccomandazioni in base agli interessi dei clienti e le azioni, mentre l'utente di hello Visualizza prodotti nel catalogo di hello nel sito Web di hello. i clienti Hello vedere anche i prodotti relativi prodotto toohello che quelli visualizzati in base ai modelli di utilizzo generale del sito Web che non sono correlati tooany un utente.

![diagramma caso d'uso](./media/data-factory-product-reco-usecase/diagram-1.png)

Gigabyte del file di log web non elaborati vengono generati ogni giorno dal sito Web del rivenditore online hello come file semistrutturati. Hello file di log web non elaborati e informazioni del catalogo hello customer e product vengono acquisite regolarmente in una risorsa di archiviazione Blob di Azure utilizzando lo spostamento dei dati distribuite globalmente della Factory di dati come servizio. file di registro non elaborati di Hello per giorno hello vengono partizionati (per anno e mese) nell'archiviazione blob per l'archiviazione a lungo termine.  [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) sono toopartition utilizzato i file di registro non elaborati hello in blob hello archivio e il processo log di hello caricamento su larga scala utilizzando gli script Hive e Pig. Hello registri web partizionata dati viene quindi elaborato tooextract hello necessari gli input per una macchina apprendimento consigli sui prodotti di raccomandazione sistema toogenerate hello personalizzato.

sistema di raccomandazione per hello machine learning in questo esempio Hello è un'origine aperto di machine learning piattaforma di raccomandazione [Mahout Apache](http://mahout.apache.org/).  Qualsiasi [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) o un modello personalizzato può essere applicato toohello scenario.  modello Mahout Hello è usato toopredict hello somiglianza tra gli elementi nel sito Web di hello in base ai modelli di utilizzo generale e consigli di toogenerate hello personalizzato in base a singoli utenti hello.

Infine, il set di risultati hello di consigli sui prodotti personalizzati è tooa spostato relazionale data mart per l'utilizzo da parte del sito Web rivenditore hello.  set di risultati Hello inoltre è stato possibile accedere direttamente dall'archiviazione blob da un'altra applicazione o spostate tooadditional archivi per altri consumer e casi d'uso.

## <a name="benefits"></a>Vantaggi
Ottimizzazione della propria strategia di raccomandazione di prodotto e allinearla agli obiettivi aziendali, soluzione hello soddisfatto merchandising del rivenditore online hello e gli obiettivi di marketing. Inoltre, cui è stata in grado di toooperationalize e gestire il flusso di lavoro di hello prodotto raccomandazione in modo efficiente, affidabile ed economico. approccio Hello ha semplificato li tooupdate loro del modello e a ottimizzare l'efficacia in base alle misure hello di esiti positivi per conversione immediata delle vendite. Usando Azure Data Factory, cui è stata tooabandon in grado di gestione di risorse cloud manuale dispersivo e costoso e spostare la gestione delle risorse cloud tooon richiesta. Pertanto, sono stati in grado di toosave tempo e denaro e ridurre la distribuzione di toosolution ora. Viste della derivazione dei dati e l'integrità operativa del servizio è diventato toovisualize semplice e risoluzione dei problemi con Data Factory intuitiva di hello monitoraggio e gestione dell'interfaccia utente disponibile dal portale di Azure hello. La soluzione può ora essere pianificata e gestita in modo che i dati terminati in modo affidabile generati e recapitati toousers e dati e le dipendenze di elaborazione vengono gestite automaticamente senza intervento umano.

Tramite questa esperienza di acquisto personalizzata, hello rivenditore online creato un cliente maggiore competitività, coinvolgere esperienza e pertanto di aumentare la soddisfazione dei clienti di vendite e generale.

