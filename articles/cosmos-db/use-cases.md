---
title: aaaCommon casi di utilizzo e scenari per Azure Cosmos DB | Documenti Microsoft
description: 'Informazioni sulla parte superiore di hello cinque casi di utilizzo per Azure Cosmos DB: generato dall''utente contenuto, la registrazione degli eventi, dati del catalogo, i dati di preferenze utente e Internet delle cose (IoT).'
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: eca68a58-1a8c-4851-8cf8-6e4d2b889905
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: mimig
ms.openlocfilehash: 115a418e7b18d5033c4d7e64591bf302aea0190b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="common-azure-cosmos-db-use-cases"></a>Casi d'uso comuni di Azure Cosmos DB
Questo articolo fornisce una panoramica di diversi casi d'uso comuni per Azure Cosmos DB.  indicazioni Hello in questo articolo fungono da un punto di partenza quando si sviluppa l'applicazione con DB Cosmos.   

Dopo aver letto questo articolo, sarà in grado di tooanswer hello seguenti domande: 

* Quali sono i casi di utilizzo per Azure Cosmos DB comuni hello?
* Quali sono i vantaggi hello utilizzando Azure Cosmos DB per le applicazioni di vendita al dettaglio?
* Quali sono hello vantaggi derivanti dall'utilizzo DB Cosmos Azure come archivio dati per i sistemi di Internet delle cose (IoT)?
* Quali sono hello vantaggi dell'utilizzo di database di Azure Cosmos per web e applicazioni per dispositivi mobili?

## <a name="introduction"></a>Introduzione
[Azure Cosmos DB](../cosmos-db/introduction.md) è il servizio di database di Microsoft distribuito a livello globale. servizio Hello è progettato tooallow tooelastically di clienti (e in modo indipendente) scala velocità effettiva e l'archiviazione per un numero qualsiasi di aree geografiche. Azure DB Cosmos è hello primo servizio di database distribuita a livello globale in hello mercato oggi toooffer completa [contratti di servizi](https://azure.microsoft.com/support/legal/sla/cosmos-db/) comprendente velocità effettiva, latenza, disponibilità e la coerenza. 

progetto di database di Azure Cosmos Hello avviato nel 2011 come "progetto denominato Florence" tooaddress developer-i punti deboli riscontrati da applicazioni di grandi dimensioni su scala Internet all'interno di Microsoft. Osservare che questi problemi non sono applicazioni di tooMicrosoft univoco, si è deciso di toomake Azure Cosmos DB tooexternal generalmente disponibili sviluppatori in 2015 nel formato hello [Azure DocumentDB](https://azure.microsoft.com/blog/documentdb-moving-to-general-availability/). servizio Hello è usato ampliamente internamente all'interno di Microsoft, è uno dei servizi più rapida crescita di hello utilizzati dagli sviluppatori di Azure esternamente. 

Azure Cosmos DB è un database multimodello distribuito a livello globale che viene usato in un'ampia gamma di applicazioni e casi di utilizzo. È una buona scelta per qualsiasi [senza](http://azure.com/serverless) applicazione che richiede tempi di risposta dell'ordine-millisecondo bassa e deve tooscale rapidamente e a livello globale. Supporta diversi modelli di dati (chiave-valore, documenti, diagrammi e grafici a colonne) oltre a molte API per l'accesso ai dati, tra cui [MongoDB](mongodb-introduction.md), [DocumentDB SQL](documentdb-introduction.md), [Gremlin](graph-introduction.md) e [tabelle di Azure ](table-introduction.md), in modo nativo ed estendibile. 

Hello seguito sono riportati alcuni attributi di Azure Cosmos DB che lo rendono ideale per applicazioni ad alte prestazioni con ambizioni globale.

* Azure Cosmos DB partiziona in modo nativo i dati per la disponibilità e la scalabilità elevate. Azure Cosmos DB offre garanzie del 99,99% per disponibilità, velocità effettiva, bassa latenza e coerenza.
* Azure Cosmos DB ha una risorsa di archiviazione basata su SSD con tempi di risposta a bassa latenza nell'ordine di millisecondi.
* Il supporto di Azure Cosmos DB per i livelli di coerenza di tipo eventuale, prefisso coerente, sessione e con obsolescenza associata consente una flessibilità completa e un basso rapporto costo-prestazioni. Nessun servizio di database offre una flessibilità maggiore di Azure Cosmos DB in termini di coerenza dei livelli. 
* Azure Cosmos DB ha un modello di determinazione dei prezzi flessibile e semplice da usare che calcola in modo indipendente lo spazio di archiviazione e la velocità effettiva.
* Modello di velocità effettiva riservati Azure Cosmos DB consente toothink in termini di numero di letture/scritture anziché memoria/CPU/IOPs di hello hardware sottostante.
* Consente di progettazione di Azure Cosmos DB ridimensionate volumi richiesta toomassive in hello ordine di trilioni di richieste al giorno.

Questi attributi sono utili in web, mobili, giochi e applicazioni IoT che necessitano di tempi di risposta bassa e che richiedono toohandle grandi quantità di letture e scritture.

## <a name="iot-and-telematics"></a>IoT e dati telematici
I casi di utilizzo IoT condividono di solito alcuni modelli di inserimento, elaborazione e archiviazione dei dati.  In primo luogo, questi sistemi devono tooingest picchi di dati da sensori dispositivo delle impostazioni locali diverse. Successivamente, questi sistemi elaborano e analizzare i flussi di informazioni in tempo reale dati di tooderive. dati Hello viene quindi archiviato archiviazione toocold per analitica batch. Microsoft Azure offre servizi avanzati che possono essere applicati per i casi d'uso di IoT, inclusi Azure Cosmos DB, Hub eventi di Azure, analisi di flusso di Azure, Hub di notifica di Azure, Azure Machine Learning, Azure HDInsight e PowerBI. 

![Architettura di riferimento di IoT per Azure Cosmos DB](./media/use-cases/iot.png)

Grandi quantità di dati possono essere acquisite da Hub eventi di Azure che consente di inserire i dati con una velocità effettiva elevata e una bassa latenza. Caricamento dei dati che devono essere elaborati toobe per una visione in tempo reale possono essere funneled tooAzure flusso Analitica per analitica in tempo reale. I dati possono essere caricati in Azure Cosmos DB per l'esecuzione di query ad hoc. Una volta caricati i dati di hello in Azure Cosmos DB, dati hello sono pronto toobe eseguire una query. Inoltre, nuovi dati e le modifiche tooexisting dati possono essere letti nel feed di modifica. Feed di modifica è permanente, aggiungere solo i log che Archivia modifiche tooCosmos DB raccolte in ordine sequenziale. Hello che tutti i dati o solo le modifiche toodata nel database di Azure Cosmos può essere utilizzato come dati di riferimento come parte di analitica in tempo reale. Inoltre, dati possono ulteriormente essere perfezionati ed elaborati da connessione tooHDInsight di dati DB Cosmos Azure per i processi MapReduce, Hive o Pig.  Dati ottimizzato viene quindi caricati tooAzure indietro Cosmos DB per i report.   

Per una soluzione di esempio IoT utilizzando Azure Cosmos DB, EventHubs e Storm, vedere hello [repository di esempi di storm hdinsight su GitHub](https://github.com/hdinsight/hdinsight-storm-examples/).

Per ulteriori informazioni sulle offerte di Azure per IoT, vedere [crea hello Internet of Things Your](http://www.microsoft.com/server-cloud/internet-of-things.aspx). 

## <a name="retail-and-marketing"></a>Vendite e marketing
Azure DB Cosmos viene spesso utilizzato nelle piattaforme di e-commerce di Microsoft, che eseguono Windows hello Store e XBox Live. Si utilizza anche nel settore al dettaglio hello per l'archiviazione dei dati del catalogo e per l'evento di acquisti nella pipeline di elaborazione degli ordini.

Gli scenari di utilizzo dei dati di un catalogo includono l'archiviazione e l'esecuzione di query di un set di attributi per entità come persone, luoghi e prodotti. Gli account utente, i cataloghi di prodotti, i registri di dispositivi IoT e i sistemi di distinta base sono alcuni esempi di dati di catalogo. Attributi per questo tipo di dati possono variare e potrebbero cambiare nel requisiti dell'applicazione toofit ora.

Considerare l'esempio di un catalogo di prodotti per un fornitore di parti di ricambio per automobili. Ogni parte può avere i propri attributi in aggiunta toohello attributi comuni che condividono tutte le parti. Inoltre, gli attributi per una parte specifica è possono modificare hello successivo quando viene rilasciato un nuovo modello. Azure Cosmos DB supporta schemi flessibili e dati gerarchici ed è pertanto adatto per l'archiviazione dei dati di un catalogo di prodotti.

![Architettura di riferimento per un catalogo di vendita al dettaglio per Azure Cosmos DB](./media/use-cases/product-catalog.png)

Azure DB Cosmos viene spesso utilizzato per l'evento sourcing architetture basato sugli eventi toopower utilizzando il relativo [modificare feed](change-feed.md) funzionalità. Hello modifica feed fornisce microservizi downstream hello tooreliably possibilità e in modo incrementale lettura inserisce e (ad esempio, gli eventi di un ordine) gli aggiornamenti tooan Azure Cosmos DB. Questa funzionalità può essere sfruttate tooprovide archiviare un evento persistente come broker di messaggi per gli eventi di modifica di stato e unità ordine l'elaborazione del flusso di lavoro tra molti microservizi (che può essere implementata come [senzalefunzionidiAzure](http://azure.com/serverless)).

![Architettura di riferimento per la pipeline degli ordini di Azure Cosmos DB](./media/use-cases/event-sourcing.png)

I dati archiviati in Azure Cosmos DB possono inoltre essere integrati con HDInsight per analisi di Big Data tramite processi Apache Spark. Per informazioni dettagliate su hello connettore Spark per Azure Cosmos DB, vedere [eseguire un processo di Spark con DB Cosmos e HDInsight](spark-connector.md).

## <a name="gaming"></a>Giochi
livello di database Hello è un componente fondamentale di applicazioni di gioco. Giochi moderni elaborazione grafica client mobile/console, ma si basano su hello cloud toodeliver personalizzato e contenuto personalizzato come statistiche di gioco, integrazione social media e classifiche punteggi. Giochi spesso richiedono le latenze singolo millisecondi per le letture e scrive tooprovide un'esperienza di gioco accattivante. Un database di gioco deve toobe veloce e sarà in grado di toohandle massive picchi di frequenza richieste per il lancio di gioco nuovi e aggiornamenti delle funzionalità.

Azure Cosmos DB viene utilizzato da giochi come [hello esame messaggi non recapitabili: terreni dell'uomo No](https://azure.microsoft.com/blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/) da [giochi Avanti](http://www.nextgames.com/), e [alone 5: tutori](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/). DB Cosmos Azure fornisce agli sviluppatori toogame i vantaggi seguenti hello:

* Azure DB Cosmos consente prestazioni toobe ridimensionato verso l'alto o verso il basso elastico. In questo modo toohandle giochi aggiornamento profilo e le statistiche da decine toomillions dei giocatori simultanei da eseguire una singola chiamata API.
* Azure supporta Cosmos DB millisecondo legge e scrive toohelp evitare eventuali ritardi durante il gioco.
* L'indicizzazione automatica di Azure Cosmos DB consente di filtrare in base a più proprietà in tempo reale, ad esempio per individuare il giocatore in base al suo ID interno o all'ID di GameCenter, Facebook o Google o per eseguire query in base all'appartenenza del giocatore a una gilda. Questa operazione può essere eseguita senza compilare indicizzazioni complesse o infrastrutture di partizionamento orizzontale.
* Funzionalità di social networking inclusi i messaggi di chat di gioco, le appartenenze di Guida di Windows Media player, sfide completate, classifiche punteggi e grafici sociali sono tooimplement più semplice con uno schema flessibile.
* Azure DB Cosmos come un gestito platform-as-a-service (PaaS) configurazione minima e gestione lavoro tooallow necessari per l'iterazione rapido e ridurre il tempo toomarket.

![Architettura di riferimento per giochi per Azure Cosmos DB](./media/use-cases/gaming.png)

## <a name="web-and-mobile-applications"></a>Applicazioni Web e per dispositivi mobili
Azure Cosmos DB viene comunemente usato all'interno di applicazioni Web e per dispositivi mobili ed è particolarmente adatto alla creazione di modelli di interazione social, all'integrazione con servizi di terze parti e all'ottimizzazione delle esperienze personalizzate. Hello Cosmos DB SDK può essere utilizzato compilazione rich applicazioni iOS e Android utilizzando hello più diffuso [Xamarin framework](mobile-apps-with-xamarin.md).  

### <a name="social-applications"></a>Applicazioni social
Un caso di utilizzo comune per Azure Cosmos DB è toostore e query contenuto generato dall'utente (UGC) per il web, applicazioni per dispositivi mobili e social media. Alcuni esempi di UGC includono sessioni di chat, tweet, post di blog, classificazioni e commenti. Spesso, hello UGC nelle applicazioni di social media è una combinazione di testo in formato libero, le proprietà, tag e le relazioni che non sono limitate dalla struttura rigida. Contenuto, ad esempio chat, forum, commenti e post possono essere archiviati in DB Cosmos senza trasformazioni oggetto complesso toorelational i livelli di mapping.  Proprietà dei dati possono essere aggiunti o modificati facilmente toomatch requisiti come gli sviluppatori di scorrere il codice dell'applicazione hello, pertanto innalzamento di livello rapido sviluppo.  

Applicazioni che si integrano con i social network di terze parti devono rispondere toochanging schemi da tali reti. Come i dati vengono indicizzati automaticamente per impostazione predefinita in DB Cosmos, i dati sono pronti toobe sottoposti a query in qualsiasi momento. Di conseguenza, queste applicazioni sono proiezioni tooretrieve flessibilità di hello in base alle rispettive esigenze.

Molte applicazioni social hello eseguire su scala globale e può presentare i modelli di utilizzo imprevisti. Flessibilità nell'archivio dati hello la scalabilità è fondamentale poiché il livello di applicazione hello Ridimensiona toomatch richieste di utilizzo.  È possibile scalare orizzontalmente aggiungendo altre partizioni di dati con un account Cosmos DB.  Si possono anche creare altri account Cosmos DB in più aree. Per la disponibilità delle aree del servizio Cosmos DB, vedere [Aree di Azure](https://azure.microsoft.com/regions/#services).

![Architettura di riferimento per app Web per Azure Cosmos DB](./media/use-cases/apps-with-global-reach.png)

### <a name="personalization"></a>Personalizzazione
Oggi le applicazioni moderne sono caratterizzate da esperienze e visualizzazioni complesse, Questi sono in genere dinamici, ristorazione toouser preferenze o espressione e di branding esigenze. Di conseguenza, le applicazioni devono toobe in grado di tooretrieve personalizzate impostazioni in modo efficace gli elementi dell'interfaccia utente di toorender ed esperienze rapidamente. 

JSON, un formato supportato da Cosmos DB, è un formato efficace toorepresent UI layout dati come non solo è semplice, ma può essere facilmente interpretato da JavaScript. Cosmos DB offre livelli di coerenza regolabili che consentono letture veloci con scritture a bassa latenza. Di conseguenza, l'archiviazione di dati di layout dell'interfaccia utente tra le impostazioni personalizzate dei documenti JSON in DB Cosmos può essere un tooget efficace questi dati in transito hello.

![Architettura di riferimento per app Web per Azure Cosmos DB](./media/use-cases/personalization.png)

## <a name="next-steps"></a>Passaggi successivi
tooget introduttiva DB Cosmos Azure, seguire il nostro [introduttive](create-documentdb-dotnet.md), che consentono di eseguire la creazione di un account e iniziare a utilizzare DB Cosmos. 

In alternativa, se si desidera approfondire i clienti che usano DB Cosmos tooread, hello study seguenti sono disponibili:

* [Jet.com](https://jet.com). E-commerce antagonista occhi hello primo posto, viene eseguito nel cloud di Microsoft hello, sfrutta Cosmos DB in una scala globale.
* [Asos.com](http://www.asos.com/). Asos.com è una società inglese che opera online nel settore della moda e della bellezza. Rivolta principalmente al segmento giovani-adulti, Asos commercializza più di 850 marchi, oltre a una propria linea di abbigliamento e accessori.
* [Toyota](https://www.toyota.com/). Toyota Motor Corporation è un produttore giapponese di automobili. Toyota ha utilizzato Cosmos DB per un'app IoT globale.
* [Citrix](https://customers.microsoft.com/story/citrix). Citrix sviluppa una soluzione single sign-on con Azure Service Fabric e Azure Cosmos DB
* [TEXA](https://customers.microsoft.com/story/texaspa) La rivoluzionarie soluzione IoT di TEXA rivolta ai proprietari di veicoli consente di risparmiare tempo, denaro, carburante e, cosa più importante, vite umane.
* [Domino's Pizza](https://www.dominos.com). Domino's Pizza Inc. è una catena statunitense di pizzerie.
* [Johnson Controls](http://www.johnsoncontrols.com). Johnson Controls è una società leader a livello globale che usa tecnologie diversificate e opera in diversi settori gestendo un'ampia gamma di clienti in oltre 150 paesi.
* [Microsoft Windows, Universal Store, Hub IoT di Azure, Xbox Live e altri servizi Internet](https://azure.microsoft.com/blog/how-azure-documentdb-planet-scale-nosql-helps-run-microsoft-s-own-businesses/). Come Microsoft integra servizi altamente scalabili usando Azure Cosmos DB.
* [Team Dati e analisi di Microsoft](https://customers.microsoft.com/story/microsoftdataandanalytics). Grazie a Cosmos DB, il team Dati e analisi di Microsoft gestisce raccolte di Big Data su scala planetaria
* [Sulekha.com](https://customers.microsoft.com/story/sulekha-uses-azure-documentdb-to-connect-customers-and-businesses-across-india). Sulekha Usa Azure Cosmos DB tooconnect clienti e aziende su India.
* [NewOrbit](https://customers.microsoft.com/story/neworbit-takes-flight-with-azure-documentdb). NewOrbit decolla con Azure Cosmos DB.
* [Affinio](https://customers.microsoft.com/doclink/affinio-switches-from-aws-to-azure-documentdb-to-harness-social-data-at-scale). Affinio passa dalla AWS tooAzure dati di social networking tooharness DB Cosmos su larga scala.
* [Next Games](https://azure.microsoft.com//blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/). Hello Walking inattivi: No Man della terra giochi esponenzialmente troppo #1 supportato da Azure Cosmos DB.
* [Halo](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/). Come è stato usato Azure Cosmos DB per implementare un'esperienza di gioco social in Halo 5.
* [Cortana Analytics Gallery](https://azure.microsoft.com/blog/cortana-analytics-gallery-a-scalable-community-site-built-on-azure-documentdb/). Cortana Analytics Gallery: un sito di community scalabile basato su Azure Cosmos DB.
* [Breeze](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18602). L'integratore leader di settore offre alle multinazionali una visione globale in pochi minuti con tecnologie cloud flessibili.
* [News Republic](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18639). Aggiunta di intelligence toohello notizie tooprovide informazioni con scopo per cittadini coinvolti. 
* [SGS International](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18653). Per i colori coerenti in tutto mondo hello, marchi principali attivato tooSGS. E consente di SGS tooAzure.
* [Telenor](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18608). Leader globale Telenor utilizza hello cloud toomove con velocità hello di avvio. 
* [XOMNI](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18667). archivio Hello delle esecuzioni future hello in rapida la ricerca e hello flusso di dati.
* [Nucleo](https://customers.microsoft.com/story/azure-based-software-platform-breaks-down-barriers-bet). Piattaforma software basata su Azure che rompe le barriere tra clienti e aziende
* [Weka](https://customers.microsoft.com/story/weka-smart-fridge-improves-vaccine-management-so-more-people-can-be-protected-against-diseases). Smart Fridge di Weka migliora la gestione dei vaccini, per offrire una protezione dalle malattie a un maggior numero di persone
* [Orange Tribes](https://customers.microsoft.com/story/theres-more-to-that-food-app-than-meets-the-eye-or-the-mouth). Non sussiste più app di alimenti toothat che soddisfi gli occhi hello o bocca hello.
* [Real Madrid](https://customers.microsoft.com/story/real-madrid-brings-the-stadium-closer-to-450-million-f). Madrid reale offre hello stadio più vicino too450 milioni ventole mondo hello hello Cloud Microsoft.
* [Tuku](https://customers.microsoft.com/story/tuku-makes-car-buying-fun-with-help-from-azure-services). TUKU rende l'acquisto di un'auto un'esperienza divertente grazie al supporto dei servizi di Azure
