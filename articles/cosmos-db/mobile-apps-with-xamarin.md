---
title: applicazioni per dispositivi mobili con Xamarin e Azure Cosmos DB aaaBuild | Documenti Microsoft
description: "Esercitazione in cui si crea un'applicazione Xamarin iOS, Android o Forms usando Azure Cosmos DB. Azure Cosmos DB è un database su cloud per dispositivi mobili veloce e dotato di copertura globale."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: monicar
editor: 
ms.assetid: ff97881a-b41a-499d-b7ab-4f394df0e153
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: arramac
ms.openlocfilehash: 362a0e239a61e1309e1cf720c23151760952cf69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-mobile-applications-with-xamarin-and-azure-cosmos-db"></a>Creare applicazioni per dispositivi mobili con Xamarin e Azure Cosmos DB
App per più dispositivi mobili è necessario toostore dati nel cloud hello e Azure Cosmos DB è un database di cloud App per dispositivi mobili. Include tutto ciò di cui uno sviluppatore per dispositivi mobili ha bisogno. È un database completamente gestito come un servizio che offre scalabilità su richiesta. È possibile attivare l'applicazione di tooyour di dati in modo trasparente, ogni volta che si trovano gli utenti in tutto il mondo hello. Utilizzando hello [Azure Cosmos DB .NET Core SDK](documentdb-sdk-dotnet-core.md), è possibile abilitare Xamarin App per dispositivi mobili toointeract direttamente con Azure Cosmos DB, senza un livello intermedio.

Questo articolo contiene un'esercitazione per la creazione di app per dispositivi mobili con Xamarin e Azure Cosmos DB. È possibile trovare codice sorgente completo hello per esercitazione hello [DB Cosmos Azure su GitHub e Xamarin](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin), compresa la modalità toomanage utenti e autorizzazioni.

## <a name="azure-cosmos-db-capabilities-for-mobile-apps"></a>Capacità di Azure Cosmos DB per le app per dispositivi mobili
DB Cosmos Azure fornisce hello seguenti funzionalità principali per gli sviluppatori di app per dispositivi mobili:

![Capacità di Azure Cosmos DB per le app per dispositivi mobili](media/mobile-apps-with-xamarin/documentdb-for-mobile.png)

* Query avanzate su dati senza schema. Azure Cosmos DB archivia i dati come documenti JSON senza schema in insiemi eterogenei. Offre [query avanzate e veloce](documentdb-sql-query.md) senza hello necessario tooworry su schemi o indici.
* Alta velocità effettiva. Richiede solo pochi millisecondi tooread e scrittura documenti con Azure Cosmos DB. Gli sviluppatori possono specificare la velocità effettiva hello che devono e Azure Cosmos DB viene eseguito con i contratti di servizio 99,99%.
* Scalabilità senza limiti. Gli insiemi di Azure Cosmos DB [crescono al crescere dell'app](partition-data.md). È possibile iniziare con dati di piccole dimensioni e velocità effettiva di centinaia di richieste al secondo. Le raccolte possono crescere toopetabytes di dati e la velocità effettiva arbitrariamente grandi dimensione con centinaia di milioni di richieste al secondo.
* Distribuzione a livello globale. App per dispositivi mobili, gli utenti sono in hello attraversano, spesso HelloWorld. Azure Cosmos DB è un [database distribuito a livello globale](distribute-data-globally.md). Fare clic su hello mappa toomake agli utenti di tooyour accessibile di dati.
* Autorizzazioni avanzate integrate. Con Azure Cosmos DB è possibile implementare facilmente modelli diffusi come i [dati per utente](https://aka.ms/documentdb-xamarin-todouser) o i dati condivisi fra più utenti senza codice di autorizzazione personalizzato complesso.
* Query geospaziali. Molte app per dispositivi mobili offrono oggi un'esperienza geografica contestuale. Con supporto di livello superiore per [tipi geospaziali](geospatial.md), Azure Cosmos DB rende la creazione di questi tooaccomplish facile esperienze.
* Allegati binari. I dati dell'app includono spesso BLOB binari. Supporto nativo per gli allegati rende più semplice toouse DB Cosmos Azure come un accesso centralizzato per i dati dell'applicazione.

## <a name="azure-cosmos-db-and-xamarin-tutorial"></a>Esercitazione su Azure Cosmos DB e Xamarin
Hello successivo dell'esercitazione viene illustrato come un'applicazione per dispositivi mobili con Xamarin e Azure Cosmos DB toobuild. È possibile trovare codice sorgente completo hello per esercitazione hello [DB Cosmos Azure su GitHub e Xamarin](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).

### <a name="get-started"></a>Attività iniziali
È facile tooget avviato con Azure Cosmos DB. Passare toohello portale di Azure e creare un nuovo account di Azure Cosmos DB. Fare clic su hello **introduttiva** scheda. Download hello Xamarin Forms attività elenco sample che è già connesso account Azure Cosmos DB tooyour. 

![Avvio rapido di Azure Cosmos DB per le app per dispositivi mobili](media/mobile-apps-with-xamarin/cosmos-db-quickstart.png)

O se si dispone di un'app Xamarin esistente, è possibile aggiungere hello [pacchetto NuGet di Azure Cosmos DB](documentdb-sdk-dotnet-core.md). Azure Cosmos DB supporta le librerie condivise Xamarin.IOS, Xamarin.Android e Xamarin Forms.

### <a name="work-with-data"></a>Usare i dati
I record di dati vengono archiviati in Azure Cosmos DB come documenti JSON senza schema in insiemi eterogenei. È possibile archiviare documenti con strutture diverse in hello stessa raccolta:

```cs
    var result = await client.CreateDocumentAsync(collectionLink, todoItem);
```

Nei progetti Xamarin è possibile usare Language Integrated Query su dati senza schema:

```cs
    var query = await client.CreateDocumentQuery<ToDoItem>(collectionLink)
                    .Where(todoItem => todoItem.Complete == false)
                    .AsDocumentQuery();

    Items = new List<TodoItem>();
    while (query.HasMoreResults) {
        Items.AddRange(await query.ExecuteNextAsync<TodoItem>());
    }
```
### <a name="add-users"></a>Aggiungi utenti
Come molti ottenere esempi di avviati, è stato scaricato: esempio hello Azure Cosmos DB autentica il servizio di toohello utilizzando una chiave master di hardcoded nel codice dell'applicazione hello. Questa impostazione predefinita non è consigliabile per un'app che si intenda toorun in un punto qualsiasi tranne l'emulatore locale. Se un utente non autorizzato ottenuto una chiave master di hello, tutti i dati per l'account di Azure Cosmos DB hello potrebbe essere compromessa. Si desidera invece che tooaccess l'applicazione hello solo i record per l'utente connesso di hello. Azure DB Cosmos consente agli sviluppatori dell'applicazione toogrant lettura o lettura/scrittura insieme tooa di autorizzazione, set di documenti raggruppati in base a una chiave di partizione o un documento specifico. 

Seguire questi passaggi toomodify hello attività app tooa multiutente attività elenco app dell'elenco: 

  1. Aggiungere account di accesso tooyour app con Facebook, Active Directory o qualsiasi altro provider.

  2. Creare una raccolta di Azure Cosmos DB UserItems con **/userId** come chiave di partizione hello. Specifica la chiave di partizione hello per la raccolta consente Azure Cosmos DB tooscale all'infinito come numero hello di agli utenti di app aumenta, pur continuando toooffer rapido query.

  3. Aggiungere il broker dei token delle risorse di Azure Cosmos DB. Questa API Web semplice autentica gli utenti e rilascia i token di breve durata toosigned-gli utenti con accesso documenti toohello solo all'interno di relativa partizione. In questo esempio si ospita Resource Token Broker nel servizio app.

  4. Modificare hello app tooauthenticate tooResource Broker Token con Facebook e richiedere il token di risorsa hello per hello Facebook utenti connessi. Quindi, è possibile accedere ai dati di hello UserItems insieme.  

È possibile trovare un esempio di codice completo di questo modello in [Resource Token Broker su Github](http://aka.ms/documentdb-xamarin-todouser). Questo diagramma vengono illustrate soluzioni hello:

![Utenti di Azure Cosmos DB e broker delle autorizzazioni](media/mobile-apps-with-xamarin/documentdb-resource-token-broker.png)

Se si desidera che i due utenti toohave accesso toohello stesso elenco di attività, è possibile aggiungere i token di accesso toohello autorizzazioni aggiuntive nel gestore di Token di risorsa.

### <a name="scale-on-demand"></a>Scalabilità su richiesta
Azure Cosmos DB è un database distribuito come servizio. Man mano che aumenta la base di utenti, è necessario tooworry sul provisioning di macchine virtuali o ad aumentare Core. È sufficiente tootell DB Cosmos Azure è necessario il numero di operazioni al secondo (produttività) dell'app. È possibile specificare la velocità effettiva hello tramite hello **scala** scheda con una misura della velocità effettiva di chiamata di richiesta di unità (RUs) al secondo. Ad esempio un'operazione di lettura su un documento da 1 KB richiede 1 UR. È inoltre possibile aggiungere gli avvisi toohello **velocità effettiva** toomonitor metrica hello dell'aumento del traffico e modificare a livello di programmazione di velocità effettiva di hello come avvisi attivati.

![Scalabilità della velocità effettiva su richiesta di Azure Cosmos DB](media/mobile-apps-with-xamarin/cosmos-db-xamarin-scale.png)

### <a name="go-planet-scale"></a>Passare alla scala globale
Come si diffonde l'app, si potrebbero ottenere utenti tutto il mondo hello. O forse si desidera toobe preparata per eventi imprevisti. Andare toohello portale di Azure e aprire l'account di Azure Cosmos DB. Fare clic su hello mappa toomake il numero di tooany continuamente replicare dati di aree del mondo hello. Questa funzionalità rende disponibili i dati, indipendentemente dalla posizione dell'utente. È anche possibile aggiungere toobe di criteri di failover preparata per contingenze.

![Scalabilità fra aree geografiche di Azure Cosmos DB](media/mobile-apps-with-xamarin/cosmos-db-xamarin-replicate.png)

A questo punto Si conclude soluzione hello e di un'app per dispositivi mobili con Xamarin e Azure Cosmos DB. Seguire le app Cordova di toobuild simile passaggi tramite hello Azure Cosmos DB SDK per JavaScript e App native per iOS/Android con le API REST di Azure Cosmos DB.

## <a name="next-steps"></a>Passaggi successivi
* Visualizzare il codice sorgente hello per [DB Cosmos Azure su GitHub e Xamarin](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).
* Scaricare hello [Azure Cosmos DB .NET Core SDK](documentdb-sdk-dotnet-core.md).
* Trovare altri esempi di codice per [applicazioni .NET](documentdb-dotnet-samples.md).
* Informazioni sulle [funzionalità di query avanzate di Azure Cosmos DB](documentdb-sql-query.md).
* Informazioni sul [supporto geospaziale in Azure Cosmos DB](geospatial.md).



