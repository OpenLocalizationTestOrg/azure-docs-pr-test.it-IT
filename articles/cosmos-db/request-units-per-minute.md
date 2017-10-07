---
title: "Azure CosmosDB: unità richiesta al minuto (UR/m) | Microsoft Docs"
description: "Informazioni su come costo tooreduce utilizzando richieste unità al minuto."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a>Unità richiesta al minuto in Azure Cosmos DB

Azure DB Cosmos è progettato toohelp è ottenere un rapido e prevedibile prestazioni e scalabilità senza problemi con l'aumento delle dimensioni dell'applicazione. È possibile effettuare il provisioning della velocità effettiva in un contenitore Cosmos DB sia con la granularità al secondo che con la granularità al minuto (UR/m). velocità effettiva di provisioning con granularità al minuto Hello è usato toomanage imprevisti picchi di carico di lavoro hello che si verificano con una granularità al secondo. 

In questo articolo viene fornita una panoramica del funzionamento di hello provisioning di unità di richiesta al minuto (UR/m). obiettivo di Hello presente con il provisioning di UR/m è tooprovide un prestazioni prevedibili intorno esigenze imprevisti (in particolare se è necessario toorun analitica nella parte superiore in base ai dati) e i carichi di lavoro problemi. Si vuole che i clienti utilizzano una velocità effettiva maggiore hello, che il provisioning in modo possibile scalare rapidamente con tranquillità toohave.

Dopo aver letto questo articolo, sarà in grado di tooanswer hello seguenti domande:

* Come funziona un'unità richiesta al minuto?
* Qual è la differenza hello tra unità di richiesta al minuto e richieste al secondo?
* Come tooprovision UR/m?
* In quale scenario è opportuno considerare il provisioning di unità richiesta al minuto?
* Come toouse hello toooptimize portale metriche personali costi e prestazioni?
* Quale tipo di richiesta può utilizzare il budget UR/m?

## <a name="provisioning-request-units-per-minute-rum"></a>Provisioning di unità richiesta al minuto (UR/m)

Quando si esegue il provisioning di Azure Cosmos DB granularità hello secondo (UR/sec), si ottiene garanzia hello che la richiesta ha esito positivo in una bassa latenza se la velocità effettiva non ha superato la capacità di hello provisioning all'interno di tale secondo. Con UR/m, granularità hello è minuto hello con garanzia hello che la richiesta ha esito positivo all'interno di tale minuto. Confronto toobursting sistemi, occorre assicurarsi prestazioni hello ottenuto sono prevedibile che è possibile pianificare su di esso.

Hello al minuto provisioning works è semplice:

* UR/m viene addebitata ogni ora e in aggiunta tooRU/s. Per altre informazioni, vedere la [pagina dei prezzi](https://aka.ms/acdbpricing) di Azure Cosmos DB.
* Le UR/m possono essere abilitate a livello di raccolta, Ciò può essere eseguito tramite hello SDK (Node.js, Java o .net) o tramite il portale di hello (includono anche i carichi di lavoro di MongoDB API)
* Quando è abilitata UR/m, per ogni 100 UR/sec provisioning, è anche possibile ottenere 1.000 UR/m provisioning (rapporto hello è 10 x)
* In un determinato secondo, un'unità richiesta utilizza il provisioning di UR/m solo se durante tale secondo è stato superato il provisioning al secondo
* Una volta hello termina il periodo di 60 secondi (UTC), viene riempito hello per ogni minuto provisioning
* Le UR/m possono essere abilitate solo per le raccolte con un provisioning massimo di 5.000 UR/s per partizione. Se le esigenze di velocità effettiva aumentano e si ha un livello di provisioning per partizione così elevato, si riceverà un messaggio di avviso

Segue un esempio concreto, in cui un cliente può effettuare il provisioning di 10.000 UR/s con 100.000 UR/m, risparmiando il 73% sui costi rispetto al provisioning per picco (a 50.000 UR/sec) in un periodo di 90 secondi in una raccolta con un provisioning di 10.000 UR/s e 100.000 UR/m:

* 1 secondo: budget UR/m hello è impostato su 100.000
* secondo 3a: durante la seconda hello consumo dell'unità richiesta è stata 11,010 russo, 1,010 RUs sopra il provisioning di hello UR/sec. Quindi, 1,010 russo è detratto budget UR/m hello. 98,990 RUs sono disponibili per hello prossimi secondi 57 budget UR/m hello
* secondo 29: durante il secondo, si è verificato un picco di grandi dimensioni (> 4 volte superiore rispetto al secondo di provisioning) e il consumo di hello dell'unità richiesta è stata 46,920 russo. 36,920 RUs vengono dedotti dal budget UR/m hello di eliminazione da 92,323 too55 RUs (secondo 28), 403 russo (29 secondi)
* secondo 61st: budget UR/m viene ripristinata too100, russo 000.
 
![Grafico che mostra il consumo di hello e il provisioning di Azure Cosmos DB](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a>Specifica della capacità delle unità richiesta con UR/M

Quando si crea una raccolta di Azure Cosmos DB, specificare il numero di hello di unità di richiesta al secondo (UR al secondo) si desidera riservato per l'insieme di hello. È inoltre possibile decidere se si desidera RU tooadd al minuto. Questa operazione può essere eseguita tramite hello portale o hello SDK. 

### <a name="through-hello-portal"></a>Tramite hello portale

Per abilitare o disabilitare UR al minuto, è sufficiente un clic durante il provisioning di una raccolta. 

 ![Screenshot che mostra come tooset UR/m in hello portale di Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a>Tramite hello SDK
In primo luogo, è importante toonote che UR/m è disponibile solo per hello seguenti SDK:

* .Net 1.14.0
* Java 1.11.0
* Node.js 1.12.0
* Python 2.2.0

Di seguito è riportato un frammento di codice per la creazione di una raccolta con 3.000 unità di richiesta per ogni unità di secondo e 30.000 richiesta al minuto utilizzando hello .NET SDK:

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

Ecco un frammento di codice per la modifica di velocità effettiva di hello di una raccolta di too5, 000 unità di richiesta al secondo senza provisioning RU al minuto utilizzando hello .NET SDK:

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a>Scenari ideali

In questa sezione è disponibile una panoramica degli scenari ideali per abilitare le unità richiesta al minuto.

**Ambiente di sviluppo e test:** ideale. Durante la fase di sviluppo hello, se si sta testando l'applicazione con diversi carichi di lavoro, UR/m possono offrire flessibilità hello in questa fase. Durante la hello [emulatore](local-emulator.md) è tootest un ottimo strumento gratuito Azure Cosmos DB. Tuttavia se si desidera toostart in un ambiente cloud, si avrà una grande flessibilità con UR/m alle proprie esigenze di prestazioni ad hoc. Sarà possibile dedicare più tempo allo sviluppo, non essendo più necessario preoccuparsi in primo luogo delle prestazioni. È consigliabile iniziare con provisioning hello minimo UR/sec e abilitare UR/m.

**Esigenze di granularità al minuto non prevedibili e di picco:** ideale. Risparmio: dal 25 al 75%. Grazie alle UR/m sono stati osservati notevoli miglioramenti per la maggior parte degli scenari di produzione. Se si dispone di un carico di lavoro IoT è picco più volte in un minuto, nel caso di query in esecuzione quando il sistema effettua massa inserire in hello stesso tempo, è necessario capacità aggiuntiva per esigenze di handeling problemi. È consigliabile ottimizzare le esigenze delle risorse applicando l'approccio graduale indicato più avanti.

 ![Grafico che illustra il consumo di richieste con una granularità di 5 minuti](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 *Figura: benchmark del consumo di UR*

**Massima tranquillità:** ideale. Risparmio: dal 10 al 20%. In alcuni casi, si desidera toohave tranquillità e non preoccuparsi picchi possibili e la limitazione delle richieste. Questa funzionalità è hello right, uno per l'utente. In questo caso, è consigliabile abilitare RU/m e ridurre leggermente il provisioning al secondo. In questo caso è diverso da hello sopra come non si tenterà di toooptimize rapidamente il provisioning. Non si tratta solo di eliminare le limitazioni.

Le operazioni critiche con esigenze ad hoc: in alcuni casi, è consigliabile tooonly consentire operazioni critiche accesso UR/m budget in modo da non ottenere budget hello consumare da ad hoc o meno operazioni importanti. Che può essere facilmente definite nella sezione hello riportata di seguito.

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a>Utilizzo di hello metriche portale toooptimize costi e prestazioni

**Nelle prossime settimane hello, si svilupperà ulteriormente il contenuto di hello intorno monitoraggio RUs consumo minuto toooptimize che richiede la velocità effettiva.**

Tramite le metriche del portale di hello, è possibile visualizzare la quantità di secondi di RU regolare utilizzi e RU minuti. Il monitoraggio di queste metriche consente di ottimizzare il provisioning. 

È consigliabile un approccio dettagliate su come toouse vantaggio tooyour UR/m. Per ogni passaggio, è necessario avere una panoramica del consumo di hello RU che rappresenta un ciclo completo del carico di lavoro (potrebbe essere ore, giorni, o persino settimane) e ottenere informazioni dettagliate sull'utilizzo di hello di il provisioning.

principio Hello dietro questo approccio è toomake il provisioning di velocità effettiva come chiudere come possibili tooa di provisioning che corrispondono ai criteri delle prestazioni seguenti. 

![Grafico che illustra il consumo di richieste con una granularità di 5 minuti](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
toounderstand hello ottimale provisioning punto per il carico di lavoro, è necessario toounderstand:

* Modelli di consumo: spike prolungati, sporadici o inesistenti? Spike di dimensioni piccole (2 volte la media), medie o grandi (più di 10 volte la media)?
* Percentuale di richieste limitate: la presenza di qualche limitazione è accettabile? Se sì, in quale percentuale? 

Dopo aver individuato gli obiettivi sono, sarà in grado di tooget più vicino toohello ottimale di provisioning.

tooassist, desideriamo tooprovide un istruzioni generali sulle modalità toooptimize il provisioning in base all'utilizzo registrato UR/m. Questa Guida non applica il tipo di tooall dei carichi di lavoro, ma si basa sulla conoscenza anteprima privata hello. Tali linee guida potrebbero cambiare nel corso del tempo:

|% utilizzo UR/m|Grado di utilizzo di UR/m|Azioni consigliate per il provisioning|
|---|---|---|
|0-1%|Sottoutilizzo|Abbassare di ulteriori UR/m tooconsume UR/sec|
|1-10%|Uso appropriato|Mantenere hello stesso provisioning livello|
|Più del 10%|Sovrautilizzo|Aumentare meno UR/m toorely UR/sec|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a>Selezionare le operazioni che possono utilizzare budget UR/m hello

A livello di richiesta, è possibile anche abilitare/disabilitare UR/m tooserve hello preventivo indipendentemente dal tipo di operazione. Se viene utilizzato regolare budget RUs/sec provisioning e richiesta hello non può utilizzare budget UR/m hello, verrà limitata la richiesta. Per impostazione predefinita, qualsiasi richiesta viene gestita dal budget per le UR/m se il budget per la velocità effettiva di UR/m è attivato. 

Di seguito è riportato un frammento di codice per la disabilitazione di budget UR/m utilizzando l'API DocumentDB hello per le operazioni CRUD e query.

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a>Passaggi successivi

Questo articolo descrive come funziona il partizionamento in Azure Cosmos DB, come creare raccolte partizionate e come scegliere una chiave di partizione efficace per l'applicazione.

* Eseguire il test delle prestazioni e della scalabilità con Azure Cosmos DB. Per un esempio, vedere [Test delle prestazioni e della scalabilità con Azure Cosmos DB](performance-testing.md).
* Iniziare a scrivere codice con hello [SDK](documentdb-sdk-dotnet.md) o hello [API REST](/rest/api/documentdb/).
* Informazioni sulla [velocità effettiva di provisioning in Azure Cosmos DB](request-units.md). 

