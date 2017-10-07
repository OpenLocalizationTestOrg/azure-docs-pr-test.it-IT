---
title: "aaaWhat è ricerca di Azure | Documenti Microsoft"
description: "Ricerca di Azure è un servizio di ricerca interamente ospitato sul cloud. In questa panoramica delle funzionalità sono fornite ulteriori informazioni sul servizio."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 50bed849-b716-4cc9-bbbc-b5b34e2c6153
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/26/2017
ms.author: ashmaka
ms.openlocfilehash: b38a7e93a7f0e0d5f8a3779858032271b3883778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-search"></a>Che cos'è la Ricerca di Azure?
Ricerca di Azure è una soluzione cloud di ricerca distribuita come servizio che offre agli sviluppatori le API e gli strumenti per ottenere un'esperienza di ricerca avanzata tra i dati nelle applicazioni Web, per dispositivi mobili ed enterprise.

Funzionalità viene esposta tramite una semplice [API REST](/rest/api/searchservice/) o [.NET SDK](search-howto-dotnet-sdk.md) che maschera la complessità intrinseca hello della tecnologia di ricerca. In aggiunta tooAPIs, hello portale di Azure consente l'amministrazione e supporto per la creazione di prototipi. La disponibilità e l'infrastruttura sono gestiti da Microsoft.

<a name="feature-drilldown"></a>

## <a name="feature-summary"></a>Riepilogo delle funzionalità

| Categoria | Funzionalità |
|----------|----------|
|Ricerca full-text e analisi del testo | [**Ricerca full-text**](search-lucene-query-architecture.md) è un caso di uso principale per la maggior parte delle app basate sulla ricerca. È possibile formulare query servendosi di una sintassi supportata: <br/><br/>[**Semplice sintassi di query**](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search), in grado di offrire operatori logici, operatori di ricerca di una frase, operatori di suffisso, operatori di precedenza.<br/><br/>[**Sintassi di query Lucene**](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) offre tutto il supporto delle query semplici oltre a ricerca fuzzy, ricerca per prossimità, aumento della priorità dei termini ed espressioni regolari.| 
| Integrazione dei dati | Gli indici di Ricerca di Azure accettano i dati provenienti da qualsiasi origine, purché vengano inviati come struttura di dati JSON. <br/><br/> Facoltativamente, per le origini dati supportate in Azure, è possibile utilizzare [ **indicizzatori** ](search-indexer-overview.md) ricerca per indicizzazione tooautomatically [Database SQL di Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md), [Azure Cosmos DB](search-howto-index-documentdb.md), o [archiviazione Blob di Azure](search-howto-indexing-azure-blob-storage.md) toosync l'indice di ricerca del contenuto con l'archivio dati primario. Gli indicizzatori BLOB di Azure possono eseguire la *decifrazione del documento* per [indicizzare i principali formati di file](search-howto-indexing-azure-blob-storage.md) inclusi documenti Microsoft Office, PDF e HTML. |
| Analisi di ricerca | [**Gli analizzatori lessicali personalizzati**](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) sono disponibili per le query di ricerca complesse che usano la corrispondenza fonetica e le espressioni regolari. |
| Supporto per le lingue | [**Gli analizzatori del linguaggio** ](https://docs.microsoft.com/rest/api/searchservice/language-support) Lucene, come Microsoft del linguaggio naturale di processori disponibili in lingue specifiche della lingua di lingue diverse 56 toointelligently handle compresi tempi dei verbi, sesso, al plurale irregolare nomi (ad esempio, ' mouse' e 'mice'), word deallocazione di composizione, ritorno a capo (per le lingue senza spazi) e altro ancora. |
| Ricerca geografica | La Ricerca di Azure elabora, filtra e visualizza le posizioni geografiche in modo intelligente. Consente agli utenti dati tooexplore basati su prossimità hello della posizione fisica tooa risultati ricerca. [Guardare questo video](https://channel9.msdn.com/Shows/Data-Exposed/Azure-Search-and-Geospatial-Data) o [rivedere in questo esempio](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs) toolearn altre. |
| Funzioni per l'esperienza utente | I [**suggerimenti per la ricerca**](https://docs.microsoft.com/rest/api/searchservice/suggesters) possono essere abilitati per le query di digitazione in una barra di ricerca. I documenti presenti nell'indice sono suggeriti come input di ricerca parziale inserita dagli utenti. <br/><br/>L'[**Esplorazione in base a facet**](https://docs.microsoft.com/azure/search/search-faceted-navigation) viene abilitata tramite un singolo parametro di query. Ricerca di Azure restituisce una struttura di navigazione con facet, che è possibile utilizzare come codice hello dietro a un elenco di categorie, per il filtro automatico diretto (ad esempio, toofilter gli elementi del catalogo da intervalli di prezzo o una marca). <br/><br/> [**I filtri** ](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) può essere utilizzato tooincorporate navigazione con facet nell'interfaccia utente dell'applicazione, migliorare la formulazione di query e filtro in base ai criteri specificati dall'utente o developer. Creare filtri utilizzando la sintassi di OData hello.<br/><br/> [**Evidenziazione dei** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) Applica formato visivo atting tooa corrispondente parola chiave nei risultati della ricerca. È possibile scegliere i campi che devono restituire i frammenti evidenziati.<br/><br/>[**Ordinamento** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) è disponibile per più campi tramite dello schema di indice hello e quindi attivare/disattivare in fase di query con un solo parametro di ricerca.<br/><br/> [**Paging** ](search-pagination-page-layout.md) e la limitazione delle richieste i risultati della ricerca è molto semplice con controllo hello ottimizzati in modo che ricerca di Azure sono disponibili tramite i risultati della ricerca.  
| Pertinenza | La [**semplicità di assegnazione dei punteggi**](/rest/api/searchservice/add-scoring-profiles-to-a-search-index) è un vantaggio chiave di Ricerca di Azure. I profili di punteggio sono pertinenti di toomodel utilizzato come una funzione di valori in hello documenti stessi. Ad esempio, si potrebbe essere necessario i prodotti più recenti o sconti per i prodotti tooappear maggiore nei risultati della ricerca hello. È inoltre possibile compilare profili di puntaggio utilizzando tag per il punteggio personalizzati in base alle preferenze di ricerca cliente che sono stati rilevati e archiviati separatamente. |
| Monitoraggio e reporting | [**Ricerca analitica traffico** ](search-traffic-analytics.md) sono le informazioni vengono raccolte e analizzate toounlock dai quali utenti sono digitare nella casella di ricerca hello. <br/><br/>Le metriche sulle query al secondo, sulla latenza e sulla limitazione vengono acquisite e inserite in report nelle pagine del portale, senza necessità di configurazioni aggiuntive. È anche possibile monitorare con facilita i conteggi di indici e documenti in modo da regolare la capacità in base alle necessità. Per altre informazioni, vedere [Amministrazione del servizio](search-manage.md) |
| Strumenti per la creazione di prototipi e l'ispezione | Nel portale di hello, è possibile utilizzare hello [ **importazione guidata dati** ](search-import-data-portal.md) tooconfigure indicizzatori, indice toostand della finestra di progettazione di un indice, e [ **Esplora ricerche** ](search-explorer.md) tootest esegue una query e perfezionare i profili di punteggio. È inoltre possibile aprire qualsiasi tooview indice relativo schema. |
| Infrastruttura | Hello **a disponibilità elevata piattaforma** garantisce un'esperienza di servizio di ricerca estremamente affidabili. Se si applica una scala corretta, [Ricerca di Azure offre un contratto di servizio con disponibilità del 99,9%](https://azure.microsoft.com/support/legal/sla/search/v1_0/).<br/><br/> **Gestione completa e scalabile** come soluzione end-to-end, Ricerca di Azure non richiede assolutamente alcun tipo di gestione dell'infrastruttura. Il servizio può essere personalizzata tooyour esigenze scalando in due dimensioni toohandle ulteriore spazio di archiviazione di documenti, più carichi di query o entrambi.

## <a name="how-it-works"></a>Funzionamento
### <a name="step-1-provision-service"></a>Passaggio 1: Effettuare il provisioning del servizio
È possibile creare rapidamente un servizio di ricerca di Azure in hello [portale di Azure](https://portal.azure.com/) o tramite hello [API di gestione risorse di Azure](/rest/api/searchmanagement/). È possibile scegliere un servizio gratuito hello condiviso con altri sottoscrittori, o un [a livello di pagamento](https://azure.microsoft.com/pricing/details/search/) che dedica le risorse usate solo dal servizio. Per i livelli a pagamento, è possibile scalare il servizio in due dimensioni: 

- Aggiungere repliche toogrow che carica il capacità toohandle elevato di query.   
- Aggiungere spazio di archiviazione di partizioni toogrow per più documenti. 

Tramite la gestione separata della risorsa di archiviazione del documento e della velocità effettiva della query, è possibile calibrare le risorse in base ai requisiti di produzione.

### <a name="step-2-create-index"></a>Passaggio 2: Creare un indice
Per poter caricare il contenuto ricercabile, è innanzitutto necessario definire un indice di Ricerca di Azure. Un indice è simile a una tabella di database che contiene i dati e può accettare query di ricerca. Per definire hello indice schema toomap tooreflect hello struttura dei documenti hello desiderato toosearch, toofields simili in un database.

È possibile creare uno schema in hello Azure hello portale o a livello di programmazione tramita [.NET SDK](search-howto-dotnet-sdk.md) o [API REST](/rest/api/searchservice/).

### <a name="step-3-index-data"></a>Passaggio 3: Indicizzare i dati
Dopo aver definito un indice, sei contenuto tooupload pronto. È possibile usare un modello push o pull.

modello pull Hello recupera dati da origini dati esterne. È supportato tramite *indicizzatori* che semplificano e automatizzano degli aspetti dell'operazione di inserimento di dati, ad esempio la connessione, la lettura e la serializzazione dei dati. Gli [indicizzatori](/rest/api/searchservice/Indexer-operations) sono disponibili per Azure Cosmos DB, Database SQL di Azure, Archiviazione BLOB di Azure e SQL Server ospitato in una macchina virtuale di Azure. È possibile configurare un indicizzatore per l'aggiornamento dati su richiesta o pianificato.

modello push Hello viene fornito tramite hello SDK o le API REST, utilizzato per l'invio di indice tooan documenti aggiornati. È possibile effettuare il push dei dati da qualsiasi set di dati utilizzando il formato JSON hello. Vedere [Add, update o delete documenti](/rest/api/searchservice/addupdate-or-delete-documents) o [come toouse hello .NET SDK)](search-howto-dotnet-sdk.md) per istruzioni sul caricamento dei dati.

### <a name="step-4-search"></a>Passaggio 4: Eseguire la ricerca
Dopo la compilazione di un indice, è possibile [eseguire query di ricerca](/rest/api/searchservice/Search-Documents) tooyour endpoint del servizio utilizzando HTTP semplice le richieste con l'API REST o hello .NET SDK.

## <a name="how-it-compares"></a>Confronto

I clienti spesso chiedono com'è la [ricerca full-text in Ricerca di Azure](search-lucene-query-architecture.md) in confronto alla [ricerca full-text](https://en.wikipedia.org/wiki/Full_text_search) nel loro prodotto database. La risposta è che le funzionalità del linguaggio di ricerca di Azure sono avanzati e più flessibile, con supporto per le query di Lucene, gli analizzatori del linguaggio di Lucene e Microsoft, analizzatori personalizzati per fonetico o di altri input specializzato e hello possibilità toomerge dati da più origini nell'indice di ricerca hello. 

Un altro punto di flesso è che una soluzione di ricerca indirizzi esperienza di ricerca completa hello. Ad esempio, si può volere un punteggio personalizzato dei risultati, un'esplorazione in base a facet per i filtri autoindirizzati, un'evidenziazione dei risultati e suggerimenti di query typeahead. 

Gli strumenti per il monitoraggio e la comprensione delle attività di query possono anche fattorizzarsi in una decisione di soluzione della ricerca. Ad esempio, Ricerca di Azure supporta l'[Analisi del traffico di ricerca](search-traffic-analytics.md) per la metrica sul tasso di click-through, le ricerche più frequenti, le ricerche senza clic e così via. Nei prodotti in cui ricerca è un componente aggiuntivo, si è toofind improbabile che queste funzionalità.

L'uso delle risorse è un'altra considerazione. La ricerca del linguaggio naturale è spesso impegnativa da un punto di vista computazionale. Alcuni dei nostri clienti scaricate le operazioni di ricerca tooAzure ricerca come risorse del computer toopreserve un modo per l'elaborazione delle transazioni. Per l'esternalizzazione di ricerca, è possibile modificare facilmente scala toomatch grandi volumi di query.

Dopo aver deciso toogo con servizio di ricerca dedicato, la decisione successiva è compreso tra un servizio cloud o un server locale. Se si desidera un servizio cloud è la scelta giusta hello un [soluzione chiavi in mano con un overhead minimo e di manutenzione e scala regolabile](#cloud-service-advantage).

All'interno di paradigma cloud hello, diversi provider offrono le funzionalità di base comparabile, con la ricerca full-text e ricerca geografica hello possibilità toohandle un certo livello di ambiguità nell'input di ricerca. In genere, è un [funzionalità specializzate](#feature-drilldown), o la facilità di hello e complessiva semplicità di gestione che determina l'adattamento migliore hello, strumenti e API.

Tra i provider di cloud, Ricerca di Azure offre le migliori prestazioni nei carichi di lavoro con ricerca full-text in archivi di contenuti e database in Azure, per le app che fanno principalmente affidamento sulla ricerca per il recupero delle informazioni e l'esplorazione dei contenuti. Ecco i principali vantaggi:

+ Integrazione di dati di Azure (crawler) a livello di indicizzazione hello
+ Portale di Azure per la gestione centralizzata
+ Scalabilità, affidabilità e massima disponibilità proprie di Azure
+ Analisi linguistica e personalizzata, con analizzatori per una robusta ricerca full-text in 56 lingue
+ [Le applicazioni basate su toosearch comuni delle funzionalità principali](#feature-drilldown): assegnazione dei punteggi, facet, suggerimenti, sinonimi, geo-ricerca e molto altro.

> [!Note]
> le origini dati non crittografato, non Azure toobe sono completamente supportate, ma si basano su una metodologia di push più dispendiose in termini di codice, anziché gli indicizzatori. Utilizzando le API, è possibile inviare tramite pipe qualsiasi indice di ricerca di Azure tooan raccolta documento di JSON.

Tra i clienti, tali tooleverage in grado di hello più vasta gamma di funzionalità di ricerca di Azure includono cataloghi online, applicazioni line-of-business e applicazioni di individuazione di documento.

## <a name="rest-api--net-sdk"></a>API REST | .NET SDK

Mentre molte attività possono essere eseguite nel portale di hello, ricerca di Azure è destinata agli sviluppatori che desiderano funzionalità di ricerca toointegrate nelle applicazioni esistenti. Hello segue le interfacce di programmazione sono disponibile.

|Piattaforma |Descrizione |
|-----|------------|
|[REST](/rest/api/searchservice/) | Comandi HTTP supportati da qualsiasi piattaforma e linguaggio di programmazione, inclusi Xamarin, Java e JavaScript|
|[.NET SDK](search-howto-dotnet-sdk.md) | Wrapper .NET per l'API REST hello offre efficiente di codifica in c# e altri linguaggi di codice gestito per hello .NET Framework |

## <a name="free-trial"></a>Versione di prova gratuita
I sottoscrittori di Azure possono [il provisioning di un servizio di livello gratuito hello](search-create-service-portal.md).

Se non si è abbonati, è possibile [aprire un account Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F). Si riceveranno crediti per provare i servizi di Azure a pagamento. Dopo il loro uso, è possibile tenere conto di hello e usare [libero di servizi di Azure](https://azure.microsoft.com/free/). Carta di credito non viene addebitata mai a meno che non modificare le impostazioni in modo esplicito e chiedere toobe addebitati.

In alternativa, è possibile [attivare i benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): con la sottoscrizione MSDN ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento. 

## <a name="how-tooget-started"></a>La modalità di avvio tooget

1. Creare un servizio in hello [livello gratuito](search-create-service-portal.md).

2. Eseguire una o più delle seguenti esercitazioni hello. 

  + [Come toouse hello .NET SDK](search-howto-dotnet-sdk.md) illustra i passaggi principale hello in codice gestito.  
  + [Introduzione a hello API REST](https://github.com/Azure-Samples/search-rest-api-getting-started) Mostra hello stessi passaggi utilizzando l'API REST hello.  
  + [Creare il primo indice nel portale di hello](search-get-started-portal.md) dimostrazione delle funzionalità di indicizzazione e prototipo incorporata del portale hello.   

Motori di ricerca sono fattori comuni hello il recupero di informazioni in App per dispositivi mobili, sito Web hello e negli archivi di dati aziendali. Ricerca di Azure offre gli strumenti per la creazione di un'esperienza di ricerca simili toothose su siti web commerciale di grandi dimensioni.

In questo video di 9 minuti prodotto dal program manager Liam Cavanagh, sono presenti informazioni su come l'app possa trarre vantaggio dall'integrazione di un motore di ricerca. Brevi demo riguardano le funzionalità principali in Ricerca di Azure e l'aspetto di un tipico flusso di lavoro. 

>[!VIDEO https://channel9.msdn.com/Events/Connect/2016/138/player]
 
+ Da 0 a 3 minuti: funzionalità chiave e casi d'uso.
+ Da 3 a 4 minuti: provisioning del servizio. 
+ 4-6 minuti copre toocreate guidata utilizzata l'importazione dei dati di un indice utilizzando i set di dati incorporato immobiliare hello.
+ Da 6 a 9 minuti: Esplora ricerche e varie query.


