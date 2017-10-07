---
title: "aaaRequest unità di misura e stima della velocità effettiva - DB Cosmos Azure | Documenti Microsoft"
description: "Informazioni su come specificare toounderstand e stimare i requisiti dell'unità richiesta nel database di Azure Cosmos."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a>Unità richiesta in Azure Cosmos DB
Ora disponibile: [calcolatore di unità richiesta](https://www.documentdb.com/capacityplanner) di Azure Cosmos DB. Per altre informazioni, vedere [Stima delle esigenze di velocità effettiva](request-units.md#estimating-throughput-needs).

![Calcolatore della velocità effettiva][5]

## <a name="introduction"></a>Introduzione
[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) è il database multimodello distribuito a livello globale di Microsoft. Con Azure Cosmos DB, non dispone di macchine virtuali toorent, distribuire il software o monitorare i database. Azure DB Cosmos è gestito e monitorato costantemente da Microsoft tecnici superiore toodeliver world classe disponibilità, prestazioni e protezione dei dati. Permette di accedere ai dati usando le API preferite, perché supporta in modalità nativa [SQL di DocumentDB](documentdb-sql-query.md) (documenti), MongoDB (documenti), [Archiviazione tabelle di Azure](https://azure.microsoft.com/services/storage/tables/) (chiave-valore) e [Gremlin](https://tinkerpop.apache.org/gremlin.html) (grafi). valuta Hello del database di Azure Cosmos è hello unità richiesta (RU). Con unità riservate, non è necessaria capacità di lettura/scrittura tooreserve o eseguire il provisioning della CPU, memoria e IOPS.

DB Cosmos Azure supporta una serie di API con diverse operazioni che vanno da semplici operazioni di lettura e scrittura toocomplex query grafico. Poiché non tutte le richieste sono uguali, viene loro assegnata una quantità normalizzata **unità richieste** in base all'ammontare hello della richiesta di calcolo necessarie tooserve hello. numero di unità di richiesta per un'operazione di Hello è deterministica ed è possibile monitorare il numero di hello di unità di richiesta utilizzati da qualsiasi operazione nel database di Azure Cosmos tramite un'intestazione di risposta. 

tooprovide prestazioni prevedibili, è necessario tooreserve velocità effettiva in unità di 100 UR/sec. 

Dopo aver letto questo articolo, sarà in grado di tooanswer hello seguenti domande:  

* Cosa sono le unità richiesta e gli addebiti richiesta?
* Come è possibile specificare la capacità delle unità richiesta per una raccolta?
* Come si possono stimare le esigenze relative alle unità richiesta per l'applicazione?
* Cosa accade se si supera la capacità delle unità richiesta per una raccolta?

Come Azure Cosmos DB è un database di più modello, è importante toonote che si farà riferimento tooa insieme o documento per un documento di API, un nodo o un grafico per un grafico di API e una tabella o entità per la tabella API. Velocità effettiva di questo documento generalizzeremo toohello concetti/elemento contenitore.

## <a name="request-units-and-request-charges"></a>Unità richiesta e addebiti richiesta
DB Cosmos Azure offre prestazioni rapida e prevedibile da *riservare* toosatisfy risorse esigenze di velocità effettiva dell'applicazione.  Perché l'applicazione carica e modifica di modelli nel corso del tempo di accesso, Azure Cosmos DB consente tooeasily aumentare o diminuire hello dell'applicazione disponibili tooyour velocità effettiva riservati.

Con Azure Cosmos DB, la velocità effettiva riservata è specificata in termini di unità richiesta elaborate al secondo. È possibile considerare di unità di richiesta come valuta di velocità effettiva, in base al quale si *riservare* garantito che una quantità di unità di richiesta applicazione tooyour disponibili in base al secondo.  Ogni operazione in Azure Cosmos DB, ovvero scrittura di un documento, esecuzione di una query, aggiornamento di un documento, utilizza CPU, memoria e operazioni di I/O al secondo.  In altre parole, ogni operazione comporta un *addebito richiesta* espresso in *unità richiesta*.  I fattori che influiscono sulle spese di unità di richiesta, insieme ai requisiti di velocità effettiva dell'applicazione, hello conoscendo toorun è l'applicazione come costi in modo efficace possibile. Esplora query Hello è anche un'eccellente strumento tootest hello di base di una query.

Si consiglia di iniziare, è possibile guardare hello seguente video, in cui Aravind Ramachandran illustra l'unità di richiesta e prestazioni prevedibili con Azure Cosmos DB.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a>Specifica della capacità in unità richiesta in Azure Cosmos DB
Quando si avvia una nuova raccolta, tabella o grafico, specificare il numero di hello di unità di richiesta al secondo (UR al secondo) si desidera riservato. In base alla velocità effettiva di provisioning hello, Azure Cosmos DB alloca la raccolta di partizioni fisiche toohost e divisioni/rebalances dati tra partizioni di si sviluppa.

DB Cosmos Azure richiede che un toobe chiave di partizione specificato quando una raccolta è stato eseguito il provisioning con 2.500 unità di richiesta o una versione successiva. Una chiave di partizione è anche necessario tooscale la velocità effettiva della raccolta oltre 2.500 unità di richiesta in futuro hello. Pertanto, è consigliabile tooconfigure un [chiave di partizione](partition-data.md) quando si crea un contenitore indipendentemente dal fatto la velocità effettiva di iniziale. Poiché i dati potrebbero contenere toobe suddiviso tra più partizioni, è necessario toopick una chiave di partizione che ha una cardinalità elevata (100 toomillions di valori distinct) in modo che la raccolta/tabella o grafico e le richieste possono essere ridimensionate in modo uniforme da Azure Cosmos DB. 

> [!NOTE]
> Una chiave di partizione è un limite logico, non un limite fisico. Pertanto, non è necessario numero hello toolimit partizione distinta dei valori di chiave. In realtà è migliore toohave più distinta partizionare i valori di chiave inferiore rispetto a come Azure Cosmos DB con le opzioni di bilanciamento del carico di ulteriori.

Ecco un frammento di codice per la creazione di una raccolta con 3.000 richiesta unità al secondo utilizzando hello .NET SDK:

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

Azure Cosmos DB usa un modello di prenotazione per la velocità effettiva, Ovvero, vengono fatturati quantità hello di velocità effettiva *riservato*, indipendentemente da quanta parte di tale velocità effettiva è attivamente *utilizzato*. Come carico, dati e utilizzo dei modelli modifica dell'applicazione è possibile ridimensionare su e giù hello quantità di RUs riservato tramite SDK o l'utilizzo di hello [portale Azure](https://portal.azure.com).

Viene eseguito il mapping di ogni raccolta, tabella o grafico tooan `Offer` risorse in Azure Cosmos DB, che contiene i metadati relativi a velocità effettiva di provisioning hello. È possibile modificare la velocità effettiva hello allocato, la ricerca di risorsa offerta corrispondente hello per un contenitore, quindi aggiornarla con il nuovo valore di velocità effettiva hello. Ecco un frammento di codice per la modifica di velocità effettiva di hello di una raccolta di too5, 000 unità di richiesta al secondo utilizzando hello .NET SDK:

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

Quando si modifica la velocità effettiva hello non è disponibilità toohello impatto del contenitore. Velocità effettiva riservate hello è in genere efficace entro pochi secondi sull'applicazione di velocità effettiva di nuovo hello.

## <a name="request-unit-considerations"></a>Considerazioni sulle unità richiesta
Quando si stima il numero di hello di tooreserve unità di richiesta per il contenitore di Azure Cosmos DB, è importante tootake hello seguenti variabili in considerazione:

* **Dimensioni dell'elemento**. Come dimensioni aumentano hello unità utilizzate tooread o scrittura dei dati hello comporterà un aumento.
* **Numero di proprietà dell'elemento**. Presupponendo che l'impostazione predefinita l'indicizzazione di tutte le proprietà, hello unità utilizzate toowrite un documento, nodo/ntity aumenterà man mano che aumenta di hello proprietà count.
* **Coerenza dei dati**. Quando si utilizzano livelli di coerenza dei dati di sicuro o con obsolescenza associata, unità aggiuntive saranno elementi tooread utilizzato.
* **Proprietà indicizzate**. I criteri di indicizzazione in ogni contenitore determinano le proprietà che vengono indicizzate per impostazione predefinita. È possibile ridurre il consumo di unità di richiesta, limitando il numero di hello di proprietà indicizzate o abilitare questo tipo di indicizzazione.
* **Indicizzazione del documento**. Per impostazione predefinita, che ogni elemento viene automaticamente indicizzato, si utilizzerà un minor numero di unità di richiesta se si sceglie non tooindex alcuni degli elementi.
* **Modelli di query**. complessità Hello di una query ha un impatto quante unità di richiesta vengono utilizzate per un'operazione. numero di Hello di predicati, natura dei predicati hello, proiezioni, numero di funzioni definite dall'utente e dimensioni di hello del set di dati di origine hello tutti influenzare il costo di hello di operazioni di query.
* **Utilizzo di script**.  Come con le query, stored procedure e trigger utilizzano unità di richiesta in base hello complessità delle operazioni di hello in corso. Quando si sviluppa l'applicazione, controllare i costi richiesta hello toobetter intestazione comprendere come ogni operazione sta consumando capacità dell'unità richiesta.

## <a name="estimating-throughput-needs"></a>Stima delle esigenze di velocità effettiva
Un'unità di richiesta è una misura normalizzata del costo di elaborazione della richiesta. Un'unità singola richiesta rappresenta tooread di capacità necessaria elaborazione hello (tramite collegamento self link o id) di un singolo 1KB elemento costituito da 10 valori di proprietà univoco (escluse le proprietà di sistema). Un toocreate richiesta (insert), sostituire o eliminare hello stesso elemento utilizzerà ulteriore elaborazione dal servizio hello e in tal modo unità più richieste.   

> [!NOTE]
> linea di base di Hello dell'unità di 1 richiesta di un 1KB corrisponde elemento tooa semplice ottenere collegamento self link o id dell'elemento hello.
> 
> 

Ad esempio, ecco una tabella che mostra il numero di richieste tooprovision unità a tre dimensioni di elemento diverso (64KB, 1KB e 4KB) e a due diversi livelli di prestazioni (500 letture al secondo 100 scritture al secondo e 500 letture al secondo + 500 scritture al secondo). è stata configurata la coerenza dei dati Hello nella sessione e criteri di indicizzazione hello è stato impostato tooNone.

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Dimensioni dell'elemento</strong></p></td>
            <td valign="top"><p><strong>Letture al secondo</strong></p></td>
            <td valign="top"><p><strong>Scritture al secondo</strong></p></td>
            <td valign="top"><p><strong>Unità richiesta</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1) + (100 * 5) = 1.000 UR/sec</p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1) + (500 * 5) = 3.000 UR/sec</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1,3) + (100 * 7) = 1.350 UR/sec</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1,3) + (500 * 7) = 4.150 UR/sec</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 10) + (100 * 48) = 9.800 UR/sec</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 10) + (500 * 48) = 29.000 UR/sec</p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a>Calcolatore unità richiesta hello
i clienti toohelp fini di ottimizzare le stime di velocità effettiva, non vi è un sito web basato [calcolatrice unità richiesta](https://www.documentdb.com/capacityplanner) toohelp stima hello richiesta i requisiti dell'unità per le normali operazioni, tra cui:

* Creazione di elementi (scrittura)
* Lettura di elementi
* Eliminazione di elementi
* Aggiornamento di elementi

strumento Hello include inoltre il supporto per la stima delle esigenze di archiviazione dei dati in base agli elementi di esempio hello che è fornire.

Utilizzo dello strumento di hello è semplice:

1. Caricare uno o più elementi rappresentativi.
   
    ![Caricare calcolatrice unità richiesta toohello di elementi][2]
2. requisiti di archiviazione dati tooestimate, immettere il numero totale di hello degli elementi previsti toostore.
3. Immettere numero hello di elementi di creare, leggere, aggiornare ed eliminare le operazioni desiderate (in base al secondo). gli addebiti unità di richiesta di tooestimate hello elemento operazioni di aggiornamento, caricare una copia dell'elemento di esempio hello dal passaggio 1 sopra che include aggiornamenti del campo tipico.  Ad esempio, se gli aggiornamenti degli elementi in genere modificare due proprietà denominate lastLogin e userVisits, copiare semplicemente l'elemento di esempio hello, aggiornare i valori hello per queste due proprietà e carica elemento hello copiato.
   
    ![Immettere i requisiti di velocità effettiva della calcolatrice unità di richiesta hello][3]
4. Fare clic su calcolare ed esaminare i risultati di hello.
   
    ![Risultati del calcolatore di unità richiesta][4]

> [!NOTE]
> Se si dispone di tipi di elemento che variano notevolmente in termini di dimensioni e hello il numero di proprietà indicizzate, quindi caricare un esempio di ogni *tipo* di toohello tipico elemento strumento e quindi calcolare i risultati di hello.
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a>Utilizzare l'intestazione della risposta addebito hello Azure Cosmos DB richiesta
Ogni risposta dal servizio Azure Cosmos DB hello include un'intestazione personalizzata (`x-ms-request-charge`) che contiene l'unità di richiesta hello utilizzata per la richiesta di hello. Questa intestazione è anche possibile accedere tramite hello Azure Cosmos DB SDK. In .NET SDK hello, RequestCharge è una proprietà dell'oggetto ResourceResponse hello.  Per le query, hello Azure Cosmos DB Query Esplora in hello portale di Azure fornisce informazioni di addebito richiesta per le query eseguite.

![Esaminare gli addebiti RU in hello Esplora Query][1]

A tal fine, un metodo per la stima delle quantità hello di velocità effettiva riservati richiesta dall'applicazione è l'addebito di toorecord hello richiesta unità associata a eseguire le operazioni tipiche di un elemento rappresentativo utilizzato dall'applicazione e quindi stima hello numero di operazioni prevede l'esecuzione di ogni secondo.  Toomeasure assicurarsi di essere e includono query tipiche e uso degli script di Azure Cosmos DB anche.

> [!NOTE]
> Se si dispone di tipi di elemento che variano notevolmente in termini di dimensioni e hello il numero di proprietà indicizzate, quindi registrare addebito di hello operazione applicabile richiesta unità associata a ogni *tipo* dell'elemento tipico.
> 
> 

ad esempio:

1. Registrare l'addebito di unità hello richiesta di creazione (inserimento) un tipico elemento. 
2. Addebito di unità hello record richiesta di lettura di un tipico elemento.
3. Addebito di unità hello record richiesta di aggiornamento di un tipico elemento.
4. Addebito di unità hello record richiesta di query comuni, tipico elemento.
5. Record hello richiesta unità delle spese di tutti gli script personalizzati (stored procedure, trigger, funzioni definite dall'utente) utilizzata da un'applicazione hello
6. Calcolare richiesta necessarie di hello unità hello stimato un numero di operazioni che si prevede toorun ogni secondo.

### <a id="GetLastRequestStatistics"></a>Usare il comando dell'API per MongoDB
API per MongoDB supporta un comando personalizzato, *getLastRequestStatistics*, per il recupero dei costi richiesta hello per le operazioni specificate.

Ad esempio, nella Shell di Mongo hello, eseguire hello operazione tooverify hello richiesta gratuito.
```
> db.sample.find()
```

Successivamente, eseguire il comando hello *getLastRequestStatistics*.
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

A tal fine, un metodo per la stima delle quantità hello di velocità effettiva riservati richiesta dall'applicazione è l'addebito di toorecord hello richiesta unità associata a eseguire le operazioni tipiche di un elemento rappresentativo utilizzato dall'applicazione e quindi stima hello numero di operazioni prevede l'esecuzione di ogni secondo.

> [!NOTE]
> Se si dispone di tipi di elemento che variano notevolmente in termini di dimensioni e hello il numero di proprietà indicizzate, quindi registrare addebito di hello operazione applicabile richiesta unità associata a ogni *tipo* dell'elemento tipico.
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a>Usare le metriche del portale dell'API per MongoDB
Hello più semplice tooget modo una buona stima dell'unità richiesta gli addebiti per l'API per i database di MongoDB è hello toouse [portale di Azure](https://portal.azure.com) metriche. Con hello *numero di richieste* e *richiesta addebito* grafici, è possibile ottenere una stima il numero di unità di richiesta ogni operazione è il numero di unità di richiesta e un notevole utilizzano relativo tooone un altro.

![Metriche del portale dell'API per MongoDB][6]

## <a name="a-request-unit-estimation-example"></a>Esempio di stima delle unità richiesta
Prendere in considerazione hello ~ 1KB documento seguenti:

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> I documenti sono minimizzare in Azure Cosmos DB, in modo che il sistema hello calcolato dimensioni del documento hello sopra sono leggermente inferiore a 1KB.
> 
> 

Hello nella tabella seguente mostra approssimativo richiesta gli addebiti di unità per le operazioni tipiche di questo elemento (hello richiesta approssimativo unità addebito si presuppone che a livello di coerenza hello account sia stato impostato troppo "Sessione" e che tutti gli elementi vengono indicizzati automaticamente):

| Operazione | Addebito delle unità richiesta |
| --- | --- |
| Creare elemento |~15 unità richiesta |
| Leggere l'elemento |~1 unità richiesta |
| Eseguire query sull'elemento in base all'ID |~2,5 unità richiesta |

Inoltre, gli addebiti di unità per le query tipiche utilizzato in un'applicazione hello questa tabella mostra approssimativo richiesta:

| Query | Addebito delle unità richiesta | Numero di elementi restituiti |
| --- | --- | --- |
| Selezionare alimenti in base all'ID |~2,5 unità richiesta |1 |
| Selezionare alimenti in base al produttore |~7 unità richiesta |7 |
| Selezionare per gruppo di alimenti e ordinare in base al peso |~70 unità richiesta |100 |
| Selezionare i primi 10 alimenti in un gruppo di alimenti |~10 unità richiesta |10 |

> [!NOTE]
> Gli addebiti RU variano in base numero hello di elementi restituiti.
> 
> 

Con queste informazioni, è possibile stimare i requisiti di RU hello per questo numero di hello applicazione data di operazioni e le query che si prevede che al secondo:

| Operazione/query | Numero stimato al secondo | Unità richiesta necessarie |
| --- | --- | --- |
| Creare elemento |10 |150 |
| Leggere l'elemento |100 |100 |
| Selezionare alimenti in base al produttore |25 |175 |
| Selezionare per gruppo di alimenti |10 |700 |
| Selezionare i primi 10 |15 |Totale 150 |

In questo caso, è previsto un requisito di velocità effettiva medio di 1.275 unità richiesta/secondo.  Arrotondamento per eccesso toohello più vicino al 100, è necessario eseguire il provisioning 1.300 UR/sec per la raccolta di questa applicazione.

## <a id="RequestRateTooLarge"></a> Superamento dei limiti della velocità effettiva riservata in Azure Cosmos DB
Tenere presente che il consumo di unità di richiesta viene valutato come una velocità al secondo se budget hello è vuoto. Per le applicazioni che superano hello richiesta provisioning unità per un contenitore, richieste verrà limitata toothat raccolta fino a quando il tasso di hello scende di sotto di livello hello riservato. Quando si verifica una limitazione, server hello modalità preemptive terminerà richiesta hello con RequestRateTooLargeException (codice di stato HTTP 429) e indicando l'intestazione x-ms-nuovo tentativo-dopo-ms hello restituito hello tempo totale, espresso in millisecondi, che hello utente deve attendere prima di Ritentare la richiesta hello.

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

Se si utilizza le query LINQ e .NET Client SDK di hello, quindi la maggior parte del tempo di hello non è mai necessario toodeal con questa eccezione, come versione corrente di hello del Client .NET SDK hello memorizza nella cache in modo implicito la risposta, equivalenti hello specificata dal server intestazione retry-after, e richiesta di hello tentativi. A meno che non si accede all'account contemporaneamente da più client, il successivo tentativo di hello avrà esito positivo.

Se si dispone di più di un client in modo cumulativo operativo sopra il numero di richieste di hello, hello comportamento tentativi predefinito potrebbe non essere sufficiente e client hello genererà un DocumentClientException con applicazione toohello 429 in codice stato. In casi come questo, è possibile considerare la gestione di comportamento del nuovo tentativo e logica di errore dell'applicazione, la gestione di routine o aumentando la velocità effettiva riservati hello per contenitore hello.

## <a id="RequestRateTooLargeAPIforMongoDB"></a> Superamento dei limiti della velocità effettiva riservata nell'API per MongoDB
Le applicazioni che superano l'unità di richiesta hello il provisioning per una raccolta verranno limitate fino a quando il tasso di hello scende di sotto di livello hello riservato. Quando si verifica una limitazione, back-end hello terminerà modalità preemptive richiesta hello con un *16500* codice di errore - *troppo numerose richieste*. Per impostazione predefinita, l'API per MongoDB tenterà automaticamente di ripetere too10 ore prima della restituzione di un *troppo numerose richieste* codice di errore. Se si ricevono numerosi *troppo numerose richieste* codici di errore, è possibile considerare un comportamento del nuovo tentativo aggiunta nella routine di gestione degli errori dell'applicazione o [aumentando la velocità effettiva riservati hello per raccolta hello](set-throughput.md).

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni sulla velocità effettiva riservati con i database di Azure Cosmos DB, è esplorare queste risorse:

* [Prezzi di Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [Partizionamento dei dati in Azure Cosmos DB](partition-data.md)

toolearn ulteriori informazioni su Azure Cosmos DB, vedere hello Azure Cosmos DB [documentazione](https://azure.microsoft.com/documentation/services/cosmos-db/). 

tooget avviato con scala e test delle prestazioni con Azure Cosmos DB, vedere [test delle prestazioni e scalabilità con Azure Cosmos DB](performance-testing.md).

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
