---
title: Considerazioni sulle prestazioni e ottimizzazione ricerca aaaAzure | Documenti Microsoft
description: "Ottimizzare le prestazioni di Ricerca di Azure e configurare una scalabilità ottimale"
services: search
documentationcenter: 
author: LiamCavanagh
manager: pablocas
editor: 
ms.assetid: 4d3cd864-29d2-4921-be0d-a3f1a819de46
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: 725149ba32773ab6b4c9d4b441424aba78db7c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-performance-and-optimization-considerations"></a>Considerazioni sulle prestazioni e sull'ottimizzazione di Ricerca di Azure
Un'esperienza ottimale di ricerca è una chiave toosuccess per molti dispositivi mobili e le applicazioni web. Da immobiliare, cataloghi di tooonline tooused car Marketplace, ricerca veloce e i risultati pertinenti avrà effetto su Analisi utilizzo software hello. Questo documento è toohelp previsto individuare le procedure consigliate per la modalità hello tooget meglio la ricerca di Azure, in particolare per scenari avanzati con sofisticate requisiti per la scalabilità, supporto multilingue o classificazione personalizzata.  Questo documento illustra anche i meccanismi interni e descrive gli approcci efficienti per le applicazioni reali dei clienti.

## <a name="performance-and-scale-tuning-for-search-services"></a>Prestazioni e pianificazione della scalabilità per i servizi di Ricerca
È in tutti i motori toosearch utilizzato, ad esempio Bing e Google e hello ad alte prestazioni che offrono.  Di conseguenza, quando i clienti usano applicazioni mobili o Web abilitate per la ricerca, si aspettano prestazioni simili.  Per l'ottimizzazione delle prestazioni di ricerca, uno degli approcci migliori hello è toofocus sulla latenza, ovvero hello tempo una query toocomplete e restituire risultati.  Durante l'ottimizzazione della latenza della ricerca, è importante:

1. Selezionare una latenza prevista (o la quantità massima di tempo) che una richiesta di ricerca tipiche dovrà essere toocomplete.
2. Creare e testare un carico di lavoro reale per il servizio di ricerca con un set di dati realistico di toomeasure i tassi di latenza.
3. Iniziare con un numero ridotto di query al secondo variano e continuare il numero di hello tooincrease eseguito in test hello fino al query hello latenza scende di sotto di hello definito latenza.  Si tratta di un toohelp benchmark importante che pianificare per la scala, man mano che aumenta l'applicazione in uso.
4. Se possibile, riusare le connessioni HTTP.  Se si utilizza hello Azure Search .NET SDK, ciò significa che è necessario riutilizzare un'istanza o [SearchIndexClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchindexclient) istanza e, se si utilizza hello API REST, è necessario riutilizzare HttpClient singolo.

Durante la creazione di questi test i carichi di lavoro, esistono alcune caratteristiche di ricerca di Azure tookeep presente:

1. È possibile toopush moltissimi ricerca eseguita una query in una sola volta, che sarà possibile sovraccaricate risorse hello disponibili nel servizio di ricerca di Azure.  In questo caso, vengono visualizzati i codici di risposta HTTP 503.  Per questo motivo, è migliore toostart con vari intervalli di ricerca richieste toosee hello differenze in periodi di latenza quando si aggiungono più richieste di ricerca.
2. Caricamento di contenuto tooAzure ricerca avrà un impatto sulle prestazioni complessive di hello e latenza di hello del servizio di ricerca di Azure.  Se si prevedono di toosend dati mentre gli utenti eseguono ricerche, è importante tootake questo carico di lavoro nell'account di test.
3. Non tutte le query di ricerca verrà eseguita in hello stessi livelli di prestazioni.  Ad esempio, la visualizzazione di un documento o un consiglio sulla ricerca viene generalmente eseguito più velocemente rispetto a una query con un numero significativo di facet e filtri.  È migliore hello tootake varie query in che previsti toosee considerazione durante la compilazione di test.  
4. Variazione delle richieste di ricerca è importante perché se si esegue continuamente hello stesso richieste di ricerca, la memorizzazione nella cache dei dati delle prestazioni di avvio toomake sarà meglio potrebbe con una query più diverso impostata.

> [!NOTE]
> [Test di carico di Visual Studio](https://www.visualstudio.com/docs/test/performance-testing/run-performance-tests-app-before-release) è un tooperform realmente efficace il benchmark testa in quanto consente le richieste HTTP tooexecute che sarebbero necessari per l'esecuzione di query su ricerca di Azure e consente la parallelizzazione delle richieste.
> 
> 

## <a name="scaling-azure-search-for-high-query-rates-and-throttled-requests"></a>Ridimensionamento di Ricerca di Azure per tassi elevati di query e richieste limitate
Quando si ricevono troppi le richieste limitate o superano le tariffe di latenza di destinazione da un carico maggiore di query, è possibile esaminare i tassi di latenza toodecrease in uno dei due modi:

1. **Aumento delle repliche:** una replica è una copia dei dati che consente di più copie di ricerca di Azure tooload bilanciamento delle richieste su hello.  Tutto il bilanciamento del carico e la replica dei dati tra le repliche è gestita da ricerca di Azure è possibile modificare il numero di hello di repliche allocata per il servizio in qualsiasi momento.  È possibile allocare backup too12 le repliche di un servizio di ricerca Standard e 3 repliche in un servizio di ricerca. Le repliche possono essere modificate da hello [portale di Azure](search-create-service-portal.md) o [PowerShell](search-manage-powershell.md).
2. **Aumentare il livello di Ricerca:** sono disponibili [diversi livelli](https://azure.microsoft.com/pricing/details/search/) per Ricerca di Azure, ognuno dei quali offre diversi livelli di prestazioni.  In alcuni casi, potrebbe essere così tante query trovano in tale livello di hello non può fornire tariffe sufficientemente bassa latenza, anche quando si raggiunge il limite massimo delle repliche.  In questo caso, è consigliabile tooconsider utilizzando uno dei piani ricerca superiori hello, ad esempio livello di hello S3 di ricerca di Azure che è particolarmente adatto per scenari con un numero elevato di documenti e i carichi di lavoro di query estremamente elevate.

## <a name="scaling-azure-search-for-slow-individual-queries"></a>Ridimensionamento di Ricerca di Azure per le singole query lente
Un altro motivo, perché può essere lente periodi di latenza è da una singola query tenendo toocomplete troppo lungo.  In questo caso, l'aggiunta di repliche non migliorerà il tasso di latenza.  In questo caso sono disponibili due opzioni:

1. **Aumentare le partizioni**: una partizione è un meccanismo per la suddivisione dei dati tra le risorse aggiuntive.  Per questo motivo, quando si aggiunge una seconda partizione, si ottengono dati divisi in due parti.  Una terza partizione suddivide l'indice in tre parti e così via.  Questo ha inoltre effetto di hello che in alcuni casi, le query lente eseguirà più velocemente a causa di parallelizzazione toohello di calcolo.  Sono disponibili alcuni esempi dell'efficienza della parallelizzazione con query che dispongono di query a selettività ridotta.  Si tratta di una query che soddisfano molti documenti o quando è necessario facet tooprovide conta su un numero elevato di documenti.  Poiché non esiste che una grande quantità di calcolo necessarie rilevanza hello tooscore di documenti hello o numeri di hello toocount dei documenti, aggiunta di partizioni aggiuntive consentono di calcolo aggiuntive tooprovide.  
   
   Può esistere un massimo di 12 partizioni nel servizio di ricerca Standard e la 1 partizione nel servizio di ricerca basic hello.  Le partizioni possono essere modificate da hello [portale di Azure](search-create-service-portal.md) o [PowerShell](search-manage-powershell.md).
2. **Campi di cardinalità elevata limite:** un campo di cardinalità elevata è costituito da un facetable o filtrabile campo che dispone di un numero significativo di valori univoci e di conseguenza, assume una grande quantità di risorse toocompute risultati.   Ad esempio, l'impostazione di un campo ID prodotto o la descrizione come filtrabile/facetable renderebbe per cardinalità elevata poiché la maggior parte dei valori hello toodocument documento sono univoca. Laddove possibile, limitare il numero di hello di campi di cardinalità elevata.
3. **Aumento del livello di ricerca:** spostando verso l'alto tooa maggiore livello di ricerca di Azure può essere un altro modo tooimprove le prestazioni delle query lente.  Ogni livello superiore fornisce CPU più veloce e memoria più ampia, elementi che possono avere un impatto positivo sulle prestazioni delle query.

## <a name="scaling-for-availability"></a>Ridimensionamento per la disponibilità
Le repliche non solo consentono di ridurre la latenza delle query ma possono anche favorire una disponibilità elevata.  Con una singola replica, è possibile aspettarsi periodica tempi di inattività a causa di riavvii tooserver dopo gli aggiornamenti software o per altri eventi di manutenzione che si verificheranno.  Di conseguenza, è importante tooconsider se l'applicazione richiede la disponibilità elevata di ricerche, le query, nonché operazioni di scrittura (eventi di indicizzazione).  Ricerca di Azure offre opzioni di contratto di servizio su tutti hello offerte a pagamento di ricerca con hello gli attributi seguenti:

* 2 repliche per la disponibilità elevata dei carichi di lavoro di sola lettura (query)
* 3 o più repliche per la disponibilità elevata dei carichi di lavoro di lettura/scrittura (query e indicizzazione)

Per ulteriori informazioni, visitare hello [contratto del servizio di ricerca di Azure](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

Poiché le repliche sono copie dei dati, con più repliche consente il riavvio di ricerca di Azure toodo macchina e manutenzione su una replica in un momento, consentendo query toobe toocontinue eseguite hello altre repliche.  Per questo motivo, è necessario anche tooconsider questo periodo di inattività possibile impatto query hello in cui sono stati toobe eseguite una minore copia dei dati di hello.

## <a name="scaling-geo-distributed-workloads-and-provide-geo-redundancy"></a>Ridimensionamento dei carichi di lavoro distribuiti geograficamente e ridondanza geografica
Per carichi di lavoro distribuita geograficamente, si noterà che gli utenti trovano lontano dal centro dati hello in cui è ospitato il servizio di ricerca di Azure avrà la velocità di latenza.  Per questo motivo, è spesso importante toohave ricerca più servizi in aree che sono in più vicino agli utenti di toothese prossimità.  Ricerca di Azure attualmente non offre un metodo automatizzato di replica geografica indici di ricerca di Azure tra le aree, ma esistono alcune tecniche che consentono di che possono rendere questo tooimplement semplice processo e gestire. Queste vengono illustrate in hello prossime sezioni.

obiettivo di un set geograficamente distribuite di servizi di ricerca Hello è toohave due o più indici disponibili in due o più aree in cui un utente sarà indirizzato toohello del servizio di ricerca di Azure che fornisce la latenza più bassa di hello, come illustrato in questo esempio:

   ![Incrocio dei servizi per area][1]

### <a name="keeping-data-in-sync-across-multiple-azure-search-services"></a>Mantenere sincronizzati i dati tra più servizi di Ricerca di Azure
Sono disponibili due opzioni per mantenere i servizi di ricerca distribuita sincronizzati tramite composti da hello [indicizzatore di ricerca di Azure](search-indexer-overview.md) o hello API Push (definita anche hello tooas [API REST di ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/)).  

### <a name="azure-search-indexers"></a>Indicizzatori di Ricerca di Azure
Se si utilizza hello indicizzatore di ricerca di Azure, già importate le modifiche ai dati da un archivio dati centrale, ad esempio database SQL di Azure o Azure Cosmos DB. Quando si crea una nuova ricerca del servizio, è sufficiente anche creare un nuovo indicizzatore di ricerca di Azure per il servizio che toothis punti stesso archivio dati. In questo modo, ogni volta che le nuove modifiche diventano hello archivio dati, si dovessero poi rendere indicizzato da hello diversi indicizzatori.  

Di seguito è riportato un esempio dell'aspetto dell'architettura.

   ![Singola origine dati con indicizzatore distribuito e combinazioni di servizio][2]

### <a name="push-api"></a>API Push
Se si utilizza hello API Push ricerca di Azure troppo[aggiornare il contenuto in un indice di ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/update-index), è possibile mantenere sincronizzati i vari servizi di ricerca mediante il push dei servizi di ricerca tooall modifiche ogni volta che è necessario un aggiornamento.  In tal caso è importante toomake che toohandle casi in cui un servizio di ricerca tooone aggiornamento ha esito negativo e l'esito positivo di uno o più aggiornamenti.

## <a name="leveraging-azure-traffic-manager"></a>Uso di Gestione traffico di Azure
[Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) consente tooroute richieste toomultiple posizionati geograficamente i siti Web che vengono quindi supportato da più servizi di ricerca di Azure.  Uno dei vantaggi di gestione traffico hello è che può probe tooensure di ricerca di Azure che sia disponibile e distribuire servizi di ricerca di utenti tooalternate nell'evento hello del tempo di inattività.  Inoltre, se si esegue il routing delle richieste di ricerca tramite siti Web di Azure, Azure Traffic Manager consente tooload saldo casi in cui sito Web di hello backup ma non ricerca di Azure.  Di seguito è riportato un esempio di architettura hello che sfrutta Traffic Manager.

   ![Incrocio dei servizi per area con Gestione traffico centrale][3]

## <a name="monitoring-performance"></a>Monitoraggio delle prestazioni
Ricerca di Azure offre hello possibilità tooanalyze e monitoraggio hello prestazioni del servizio tramite [ricerca traffico Analitica (STA)](search-traffic-analytics.md). Tramite STA, è facoltativamente possibile registrare le operazioni di ricerca individuali hello, nonché account di archiviazione Azure tooan le metriche di aggregazione che possono essere elaborati per l'analisi o visualizzati in Power BI.  Con le metriche STA, è possibile esaminare le statistiche sulle prestazioni, ad esempio il numero medio delle query o i tempi di risposta alle query.  Inoltre, la registrazione di operazioni hello consente toodrill in dettagli delle operazioni di ricerca specifico.

STA rappresenta una velocità di latenza strumento prezioso toounderstand dal punto di vista che ricerca di Azure.  Poiché le metriche delle prestazioni di query hello registrate sono basate su tempo hello una query richiede toobe completamente elaborati nella ricerca di Azure (da ora hello è toowhen richiesto che venga inviato), si è in grado di toouse questo toodetermine se problemi di latenza da hello del servizio di ricerca di Azure sul lato o all'esterno di hello service, ad esempio dalla latenza di rete.  

## <a name="next-steps"></a>Passaggi successivi
vedere toolearn ulteriori informazioni sui prezzi di livelli e i limiti di servizi per ognuno di essi, hello [limiti in ricerca di Azure del servizio](search-limits-quotas-capacity.md).

Visitare [la pianificazione della capacità](search-capacity-planning.md) toolearn ulteriori informazioni sulle combinazioni di partizione e di replica.

Per ulteriori drill-down sulle prestazioni e toosee alcune dimostrazioni della modalità tooimplement hello ottimizzazioni descritti in questo articolo, eseguire il controllo hello video seguente:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<!--Image references-->
[1]: ./media/search-performance-optimization/geo-redundancy.png
[2]: ./media/search-performance-optimization/scale-indexers.png
[3]: ./media/search-performance-optimization/geo-search-traffic-mgr.png
