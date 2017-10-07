---
title: architetture del database master di aaaMulti con Azure Cosmos DB | Documenti Microsoft
description: "Informazioni su come toodesign architetture di applicazioni con locale legge e scrive in più aree geografiche con Azure Cosmos DB."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 706ced74-ea67-45dd-a7de-666c3c893687
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3269c8405afe16f75db69b42e576fe76e00a8e16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a>Architetture di database multimaster replicate a livello globale con Cosmos DB
DB Cosmos Azure supporta pronti per l'uso [replica globale](distribute-data-globally.md), che consente le aree con accesso a bassa latenza in qualsiasi parte del carico di lavoro hello toomultiple dati toodistribute. Questo modello viene usato in genere per carichi di lavoro di pubblicazione/consumer in cui è presente un writer in una singola area geografica e con lettori distribuiti a livello globale in altre aree (lettura). 

È inoltre possibile utilizzare globale supporto toobuild le applicazioni di replica Azure Cosmos DB in cui i writer e lettori sono globalmente distribuiti. Questo documento illustra un modello che consente di ottenere l'accesso in scrittura e lettura locale per i writer distribuiti mediante Azure Cosmos DB.

## <a id="ExampleScenario"></a>Pubblicazione del contenuto: scenario di esempio
Esaminiamo un toodescribe di uno scenario reale come è possibile utilizzare i modelli distribuiti in modo globale più region/multi-master lettura/scrittura con Azure Cosmos DB. Esaminare una piattaforma di pubblicazione di contenuti creata in Cosmos DB. Ecco alcuni requisiti che devono essere rispettati da questa piattaforma per offrire un'esperienza utente ottimale per server di pubblicazione e consumer.

* Sia gli autori e i sottoscrittori vengono distribuiti in HelloWorld 
* Gli autori devono pubblicare (scrittura) articoli tootheir locale (il più vicino) area
* Gli autori hanno lettori/tutti i sottoscrittori di loro articoli che vengono distribuiti tra globo hello. 
* I sottoscrittori ricevono una notifica quando vengono pubblicati nuovi articoli.
* I sottoscrittori devono essere in grado di tooread articoli da loro area locale. Dovrebbero inoltre essere in grado di tooadd revisioni toothese articoli. 
* Tutti gli utenti, tra cui autore hello degli articoli hello deve essere in grado di visualizzare che tutti hello revisioni tooarticles collegati da un'area locale. 

Supponendo che milioni di utenti e i server di pubblicazione con miliardi di articoli, non appena si riscontrano tooconfront hello della scala insieme a garantire la località di accesso. Come con la maggior parte dei problemi di scalabilità, la soluzione hello si trova in una buona strategia di partizionamento. Successivamente, si esaminerà come articoli toomodel, esaminare e notifiche come documenti, configurano gli account di Azure Cosmos DB e implementare un livello di accesso ai dati. 

Se si desidera toolearn informazioni sul partizionamento e le chiavi di partizione, vedere [partizionamento e la scalabilità in Azure Cosmos DB](partition-data.md).

## <a id="ModelingNotifications"></a>Modellazione delle notifiche
Le notifiche sono utente tooa specifico di feed di dati. Pertanto, i modelli di accesso hello per i documenti le notifiche sono sempre nel contesto di hello del singolo utente. Ad esempio, si sarebbe "post a un utente tooa notifica" o "recuperare tutte le notifiche per un determinato utente". In tal caso, hello ottimale della chiave di partizionamento per questo tipo `UserId`.

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // hello user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // hello partition Key for hello resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of hello notification. 
        public string ArticleId { get; set; } 
    }

## <a id="ModelingSubscriptions"></a>Modellazione delle sottoscrizioni
Le sottoscrizioni possono essere create per diversi criteri, ad esempio per una categoria di articoli rilevanti o un server di pubblicazione specifico. Di conseguenza hello `SubscriptionFilter` è una buona scelta per la chiave di partizione.

    class Subscriptions 
    { 
        // Unique ID for Subscription 
        public string Id { get; set; }

        // Subscription source. Could be Author | Category etc. 
        public string SubscriptionFilter { get; set; }

        // subscribing User. 
        public string UserId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.SubscriptionFilter; 
            } 
        } 
    }

## <a id="ModelingArticles"></a>Modellazione degli articoli
Una volta identificato un articolo tramite le notifiche, le query successive sono solitamente basate sul hello `Article.Id`. Scelta di `Article.Id` come partizione chiave hello fornisce pertanto distribuzione migliore di hello per l'archiviazione di articoli all'interno di una raccolta di Azure Cosmos DB. 

    class Article 
    { 
        // Unique ID for Article 
        public string Id { get; set; }
        
        public string PartitionKey 
        { 
            get 
            { 
                return this.Id; 
            } 
        }
        
        // Author of hello article
        public string Author { get; set; }

        // Category/genre of hello article
        public string Category { get; set; }

        // Tags associated with hello article
        public string[] Tags { get; set; }

        // Title of hello article
        public string Title { get; set; }
        
        //... 
    }

## <a id="ModelingReviews"></a>Modellazione delle revisioni
Come articoli, revisioni sono principalmente scritte e letti nel contesto di hello dell'articolo. Scegliendo `ArticleId` come chiave di partizione si ottiene quindi la distribuzione ottimale e l'accesso più efficiente per le revisioni associate all'articolo. 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of hello review 
        public string ArticleId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.ArticleId; 
            } 
        }
        
        //Reviewer Id 
        public string UserId { get; set; }
        public string ReviewText { get; set; }
        
        public int Rating { get; set; } }
    }

## <a id="DataAccessMethods"></a>Metodi per i livelli di accesso ai dati
Ora esaminiamo dati principale hello dobbiamo tooimplement dei metodi di accesso. Ecco hello elenco di metodi che hello `ContentPublishDatabase` deve:

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <a id="Architecture"></a>Configurazione dell'account Azure Cosmos DB
tooguarantee locale legge e scrive, è necessario partizionare i dati non solo sulla chiave di partizione, ma anche in base allo schema di accesso geografica hello in aree. modello di Hello si basa sulla disponibilità di un account del database di Azure Cosmos DB replica geografica per ogni area. Ad esempio, con due aree si può ottenere uno scenario come il seguente per le operazioni di scrittura in più aree:

| Nome account | Area di scrittura | Area di lettura |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

Hello diagramma seguente viene illustrato come vengono eseguite le letture e scritture in una tipica applicazione con il programma di installazione:

![Architettura multimaster di Azure Cosmos DB](./media/multi-region-writers/multi-master.png)

Ecco un frammento di codice che illustra come tooinitialize hello client a in esecuzione in hello `West US` area.
    
    ConnectionPolicy writeClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    writeClientPolicy.PreferredLocations.Add(LocationNames.WestUS);
    writeClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

    DocumentClient writeClient = new DocumentClient(
        new Uri("https://contentpubdatabase-usa.documents.azure.com"), 
        writeRegionAuthKey,
        writeClientPolicy);

    ConnectionPolicy readClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    readClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);
    readClientPolicy.PreferredLocations.Add(LocationNames.WestUS);

    DocumentClient readClient = new DocumentClient(
        new Uri("https://contentpubdatabase-europe.documents.azure.com"),
        readRegionAuthKey,
        readClientPolicy);

Con hello che precede il programma di installazione, livello di accesso ai dati hello può inoltrare tutte le operazioni di scrittura toohello account locale in base a cui viene distribuito. Letture vengono eseguite mediante la lettura da entrambi visualizzazione globale di hello tooget gli account dei dati. Questo approccio può essere estesa tooas molte aree in base alle esigenze. Ad esempio, ecco una configurazione con tre aree geografiche:

| Nome account | Area di scrittura | Area di lettura 1 | Area di lettura 2 |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <a id="DataAccessImplementation"></a>Implementazione del livello di accesso ai dati
Ora esaminiamo implementazione hello di hello livello di accesso ai dati (DAL) per un'applicazione con due aree modificabili. Hello DAL deve implementare hello alla procedura seguente:

* Creare più istanze di `DocumentClient` per ogni account. Con due aree, ogni istanza del livello di accesso ai dati ha un valore `writeClient` e un valore `readClient`. 
* Basato sull'area di hello distribuito dell'applicazione hello, configurare gli endpoint di hello per `writeclient` e `readClient`. Ad esempio, hello DAL distribuiti `West US` utilizza `contentpubdatabase-usa.documents.azure.com` per l'esecuzione di operazioni di scrittura. Hello DAL distribuito in `NorthEurope` utilizza `contentpubdatabase-europ.documents.azure.com` per operazioni di scrittura.

Con hello che precede il programma di installazione, è possibile implementare i metodi di accesso ai dati hello. Scrivere operazioni inoltrare hello scrittura toohello corrispondente `writeClient`.

    public async Task CreateSubscriptionAsync(string userId, string category)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Subscriptions
        {
            UserId = userId,
            SubscriptionFilter = category
        });
    }

    public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Review
        {
            UserId = userId,
            ArticleId = articleId,
            ReviewText = reviewText,
            Rating = rating
        });
    }

Per la lettura delle notifiche e revisioni, è necessario leggere le aree e i risultati di unione hello come illustrato nel seguente frammento di codice hello:

    public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId)
    {
        IDocumentQuery<Notification> writeAccountNotification = (
            from notification in this.writeClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();
        
        IDocumentQuery<Notification> readAccountNotification = (
            from notification in this.readClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();

        List<Notification> notifications = new List<Notification>();

        while (writeAccountNotification.HasMoreResults || readAccountNotification.HasMoreResults)
        {
            IList<Task<FeedResponse<Notification>>> results = new List<Task<FeedResponse<Notification>>>();

            if (writeAccountNotification.HasMoreResults)
            {
                results.Add(writeAccountNotification.ExecuteNextAsync<Notification>());
            }

            if (readAccountNotification.HasMoreResults)
            {
                results.Add(readAccountNotification.ExecuteNextAsync<Notification>());
            }

            IList<FeedResponse<Notification>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Notification> feed in notificationFeedResult)
            {
                notifications.AddRange(feed);
            }
        }
        return notifications;
    }

    public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId)
    {
        IDocumentQuery<Review> writeAccountReviews = (
            from review in this.writeClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();
        
        IDocumentQuery<Review> readAccountReviews = (
            from review in this.readClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();

        List<Review> reviews = new List<Review>();
        
        while (writeAccountReviews.HasMoreResults || readAccountReviews.HasMoreResults)
        {
            IList<Task<FeedResponse<Review>>> results = new List<Task<FeedResponse<Review>>>();

            if (writeAccountReviews.HasMoreResults)
            {
                results.Add(writeAccountReviews.ExecuteNextAsync<Review>());
            }

            if (readAccountReviews.HasMoreResults)
            {
                results.Add(readAccountReviews.ExecuteNextAsync<Review>());
            }

            IList<FeedResponse<Review>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Review> feed in notificationFeedResult)
            {
                reviews.AddRange(feed);
            }
        }

        return reviews;
    }

Se si sceglie una chiave di partizione ottimale e un partizionamento basato su account statici, è possibile ottenere operazioni di scrittura e lettura locali in più aree usando Azure Cosmos DB.

## <a id="NextSteps"></a>Passaggi successivi
In questo articolo è stato illustrato come è possibile usare modelli di lettura e scrittura in più aree con distribuzione globale con Cosmos DB usando la pubblicazione di contenuti come scenario di esempio.

* Altre informazioni sul modo in cui Cosmos DB supporta la [distribuzione globale](distribute-data-globally.md)
* Altre informazioni sui [failover automatici o manuali in Azure Cosmos DB](regional-failover.md)
* Informazioni sulla [coerenza globale con Azure Cosmos DB](consistency-levels.md)
* Sviluppo con più aree tramite hello [Azure Cosmos DB - API DocumentDB](tutorial-global-distribution-documentdb.md)
* Sviluppo con più aree tramite hello [Azure Cosmos DB - API MongoDB](tutorial-global-distribution-MongoDB.md)
* Sviluppo con più aree tramite hello [Azure Cosmos DB - API di tabella](tutorial-global-distribution-table.md)
