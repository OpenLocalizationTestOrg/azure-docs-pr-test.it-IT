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
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="3b780-103">Architetture di database multimaster replicate a livello globale con Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3b780-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="3b780-104">DB Cosmos Azure supporta pronti per l'uso [replica globale](distribute-data-globally.md), che consente le aree con accesso a bassa latenza in qualsiasi parte del carico di lavoro hello toomultiple dati toodistribute.</span><span class="sxs-lookup"><span data-stu-id="3b780-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you toodistribute data toomultiple regions with low latency access anywhere in hello workload.</span></span> <span data-ttu-id="3b780-105">Questo modello viene usato in genere per carichi di lavoro di pubblicazione/consumer in cui è presente un writer in una singola area geografica e con lettori distribuiti a livello globale in altre aree (lettura).</span><span class="sxs-lookup"><span data-stu-id="3b780-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="3b780-106">È inoltre possibile utilizzare globale supporto toobuild le applicazioni di replica Azure Cosmos DB in cui i writer e lettori sono globalmente distribuiti.</span><span class="sxs-lookup"><span data-stu-id="3b780-106">You can also use Azure Cosmos DB's global replication support toobuild applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="3b780-107">Questo documento illustra un modello che consente di ottenere l'accesso in scrittura e lettura locale per i writer distribuiti mediante Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3b780-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="3b780-108"><a id="ExampleScenario"></a>Pubblicazione del contenuto: scenario di esempio</span><span class="sxs-lookup"><span data-stu-id="3b780-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="3b780-109">Esaminiamo un toodescribe di uno scenario reale come è possibile utilizzare i modelli distribuiti in modo globale più region/multi-master lettura/scrittura con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3b780-109">Let's look at a real world scenario toodescribe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="3b780-110">Esaminare una piattaforma di pubblicazione di contenuti creata in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3b780-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="3b780-111">Ecco alcuni requisiti che devono essere rispettati da questa piattaforma per offrire un'esperienza utente ottimale per server di pubblicazione e consumer.</span><span class="sxs-lookup"><span data-stu-id="3b780-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="3b780-112">Sia gli autori e i sottoscrittori vengono distribuiti in HelloWorld</span><span class="sxs-lookup"><span data-stu-id="3b780-112">Both authors and subscribers are spread over hello world</span></span> 
* <span data-ttu-id="3b780-113">Gli autori devono pubblicare (scrittura) articoli tootheir locale (il più vicino) area</span><span class="sxs-lookup"><span data-stu-id="3b780-113">Authors must publish (write) articles tootheir local (closest) region</span></span>
* <span data-ttu-id="3b780-114">Gli autori hanno lettori/tutti i sottoscrittori di loro articoli che vengono distribuiti tra globo hello.</span><span class="sxs-lookup"><span data-stu-id="3b780-114">Authors have readers/subscribers of their articles who are distributed across hello globe.</span></span> 
* <span data-ttu-id="3b780-115">I sottoscrittori ricevono una notifica quando vengono pubblicati nuovi articoli.</span><span class="sxs-lookup"><span data-stu-id="3b780-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="3b780-116">I sottoscrittori devono essere in grado di tooread articoli da loro area locale.</span><span class="sxs-lookup"><span data-stu-id="3b780-116">Subscribers must be able tooread articles from their local region.</span></span> <span data-ttu-id="3b780-117">Dovrebbero inoltre essere in grado di tooadd revisioni toothese articoli.</span><span class="sxs-lookup"><span data-stu-id="3b780-117">They should also be able tooadd reviews toothese articles.</span></span> 
* <span data-ttu-id="3b780-118">Tutti gli utenti, tra cui autore hello degli articoli hello deve essere in grado di visualizzare che tutti hello revisioni tooarticles collegati da un'area locale.</span><span class="sxs-lookup"><span data-stu-id="3b780-118">Anyone including hello author of hello articles should be able view all hello reviews attached tooarticles from a local region.</span></span> 

<span data-ttu-id="3b780-119">Supponendo che milioni di utenti e i server di pubblicazione con miliardi di articoli, non appena si riscontrano tooconfront hello della scala insieme a garantire la località di accesso.</span><span class="sxs-lookup"><span data-stu-id="3b780-119">Assuming millions of consumers and publishers with billions of articles, soon we have tooconfront hello problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="3b780-120">Come con la maggior parte dei problemi di scalabilità, la soluzione hello si trova in una buona strategia di partizionamento.</span><span class="sxs-lookup"><span data-stu-id="3b780-120">As with most scalability problems, hello solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="3b780-121">Successivamente, si esaminerà come articoli toomodel, esaminare e notifiche come documenti, configurano gli account di Azure Cosmos DB e implementare un livello di accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="3b780-121">Next, let's look at how toomodel articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="3b780-122">Se si desidera toolearn informazioni sul partizionamento e le chiavi di partizione, vedere [partizionamento e la scalabilità in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="3b780-122">If you would like toolearn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="3b780-123"><a id="ModelingNotifications"></a>Modellazione delle notifiche</span><span class="sxs-lookup"><span data-stu-id="3b780-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="3b780-124">Le notifiche sono utente tooa specifico di feed di dati.</span><span class="sxs-lookup"><span data-stu-id="3b780-124">Notifications are data feeds specific tooa user.</span></span> <span data-ttu-id="3b780-125">Pertanto, i modelli di accesso hello per i documenti le notifiche sono sempre nel contesto di hello del singolo utente.</span><span class="sxs-lookup"><span data-stu-id="3b780-125">Therefore, hello access patterns for notifications documents are always in hello context of single user.</span></span> <span data-ttu-id="3b780-126">Ad esempio, si sarebbe "post a un utente tooa notifica" o "recuperare tutte le notifiche per un determinato utente".</span><span class="sxs-lookup"><span data-stu-id="3b780-126">For example, you would "post a notification tooa user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="3b780-127">In tal caso, hello ottimale della chiave di partizionamento per questo tipo `UserId`.</span><span class="sxs-lookup"><span data-stu-id="3b780-127">So, hello optimal choice of partitioning key for this type would be `UserId`.</span></span>

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

## <span data-ttu-id="3b780-128"><a id="ModelingSubscriptions"></a>Modellazione delle sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="3b780-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="3b780-129">Le sottoscrizioni possono essere create per diversi criteri, ad esempio per una categoria di articoli rilevanti o un server di pubblicazione specifico.</span><span class="sxs-lookup"><span data-stu-id="3b780-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="3b780-130">Di conseguenza hello `SubscriptionFilter` è una buona scelta per la chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="3b780-130">Hence hello `SubscriptionFilter` is a good choice for partition key.</span></span>

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

## <span data-ttu-id="3b780-131"><a id="ModelingArticles"></a>Modellazione degli articoli</span><span class="sxs-lookup"><span data-stu-id="3b780-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="3b780-132">Una volta identificato un articolo tramite le notifiche, le query successive sono solitamente basate sul hello `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="3b780-132">Once an article is identified through notifications, subsequent queries are typically based on hello `Article.Id`.</span></span> <span data-ttu-id="3b780-133">Scelta di `Article.Id` come partizione chiave hello fornisce pertanto distribuzione migliore di hello per l'archiviazione di articoli all'interno di una raccolta di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3b780-133">Choosing `Article.Id` as partition hello key thus provides hello best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

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

## <span data-ttu-id="3b780-134"><a id="ModelingReviews"></a>Modellazione delle revisioni</span><span class="sxs-lookup"><span data-stu-id="3b780-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="3b780-135">Come articoli, revisioni sono principalmente scritte e letti nel contesto di hello dell'articolo.</span><span class="sxs-lookup"><span data-stu-id="3b780-135">Like articles, reviews are mostly written and read in hello context of article.</span></span> <span data-ttu-id="3b780-136">Scegliendo `ArticleId` come chiave di partizione si ottiene quindi la distribuzione ottimale e l'accesso più efficiente per le revisioni associate all'articolo.</span><span class="sxs-lookup"><span data-stu-id="3b780-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

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

## <span data-ttu-id="3b780-137"><a id="DataAccessMethods"></a>Metodi per i livelli di accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="3b780-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="3b780-138">Ora esaminiamo dati principale hello dobbiamo tooimplement dei metodi di accesso.</span><span class="sxs-lookup"><span data-stu-id="3b780-138">Now let's look at hello main data access methods we need tooimplement.</span></span> <span data-ttu-id="3b780-139">Ecco hello elenco di metodi che hello `ContentPublishDatabase` deve:</span><span class="sxs-lookup"><span data-stu-id="3b780-139">Here's hello list of methods that hello `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="3b780-140"><a id="Architecture"></a>Configurazione dell'account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3b780-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="3b780-141">tooguarantee locale legge e scrive, è necessario partizionare i dati non solo sulla chiave di partizione, ma anche in base allo schema di accesso geografica hello in aree.</span><span class="sxs-lookup"><span data-stu-id="3b780-141">tooguarantee local reads and writes, we must partition data not just on partition key, but also based on hello geographical access pattern into regions.</span></span> <span data-ttu-id="3b780-142">modello di Hello si basa sulla disponibilità di un account del database di Azure Cosmos DB replica geografica per ogni area.</span><span class="sxs-lookup"><span data-stu-id="3b780-142">hello model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="3b780-143">Ad esempio, con due aree si può ottenere uno scenario come il seguente per le operazioni di scrittura in più aree:</span><span class="sxs-lookup"><span data-stu-id="3b780-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="3b780-144">Nome account</span><span class="sxs-lookup"><span data-stu-id="3b780-144">Account Name</span></span> | <span data-ttu-id="3b780-145">Area di scrittura</span><span class="sxs-lookup"><span data-stu-id="3b780-145">Write Region</span></span> | <span data-ttu-id="3b780-146">Area di lettura</span><span class="sxs-lookup"><span data-stu-id="3b780-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="3b780-147">Hello diagramma seguente viene illustrato come vengono eseguite le letture e scritture in una tipica applicazione con il programma di installazione:</span><span class="sxs-lookup"><span data-stu-id="3b780-147">hello following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Architettura multimaster di Azure Cosmos DB](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="3b780-149">Ecco un frammento di codice che illustra come tooinitialize hello client a in esecuzione in hello `West US` area.</span><span class="sxs-lookup"><span data-stu-id="3b780-149">Here is a code snippet showing how tooinitialize hello clients in a DAL running in hello `West US` region.</span></span>
    
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

<span data-ttu-id="3b780-150">Con hello che precede il programma di installazione, livello di accesso ai dati hello può inoltrare tutte le operazioni di scrittura toohello account locale in base a cui viene distribuito.</span><span class="sxs-lookup"><span data-stu-id="3b780-150">With hello preceding setup, hello data access layer can forward all writes toohello local account based on where it is deployed.</span></span> <span data-ttu-id="3b780-151">Letture vengono eseguite mediante la lettura da entrambi visualizzazione globale di hello tooget gli account dei dati.</span><span class="sxs-lookup"><span data-stu-id="3b780-151">Reads are performed by reading from both accounts tooget hello global view of data.</span></span> <span data-ttu-id="3b780-152">Questo approccio può essere estesa tooas molte aree in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="3b780-152">This approach can be extended tooas many regions as required.</span></span> <span data-ttu-id="3b780-153">Ad esempio, ecco una configurazione con tre aree geografiche:</span><span class="sxs-lookup"><span data-stu-id="3b780-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="3b780-154">Nome account</span><span class="sxs-lookup"><span data-stu-id="3b780-154">Account Name</span></span> | <span data-ttu-id="3b780-155">Area di scrittura</span><span class="sxs-lookup"><span data-stu-id="3b780-155">Write Region</span></span> | <span data-ttu-id="3b780-156">Area di lettura 1</span><span class="sxs-lookup"><span data-stu-id="3b780-156">Read Region 1</span></span> | <span data-ttu-id="3b780-157">Area di lettura 2</span><span class="sxs-lookup"><span data-stu-id="3b780-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="3b780-158"><a id="DataAccessImplementation"></a>Implementazione del livello di accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="3b780-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="3b780-159">Ora esaminiamo implementazione hello di hello livello di accesso ai dati (DAL) per un'applicazione con due aree modificabili.</span><span class="sxs-lookup"><span data-stu-id="3b780-159">Now let's look at hello implementation of hello data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="3b780-160">Hello DAL deve implementare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3b780-160">hello DAL must implement hello following steps:</span></span>

* <span data-ttu-id="3b780-161">Creare più istanze di `DocumentClient` per ogni account.</span><span class="sxs-lookup"><span data-stu-id="3b780-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="3b780-162">Con due aree, ogni istanza del livello di accesso ai dati ha un valore `writeClient` e un valore `readClient`.</span><span class="sxs-lookup"><span data-stu-id="3b780-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="3b780-163">Basato sull'area di hello distribuito dell'applicazione hello, configurare gli endpoint di hello per `writeclient` e `readClient`.</span><span class="sxs-lookup"><span data-stu-id="3b780-163">Based on hello deployed region of hello application, configure hello endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="3b780-164">Ad esempio, hello DAL distribuiti `West US` utilizza `contentpubdatabase-usa.documents.azure.com` per l'esecuzione di operazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="3b780-164">For example, hello DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="3b780-165">Hello DAL distribuito in `NorthEurope` utilizza `contentpubdatabase-europ.documents.azure.com` per operazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="3b780-165">hello DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="3b780-166">Con hello che precede il programma di installazione, è possibile implementare i metodi di accesso ai dati hello.</span><span class="sxs-lookup"><span data-stu-id="3b780-166">With hello preceding setup, hello data access methods can be implemented.</span></span> <span data-ttu-id="3b780-167">Scrivere operazioni inoltrare hello scrittura toohello corrispondente `writeClient`.</span><span class="sxs-lookup"><span data-stu-id="3b780-167">Write operations forward hello write toohello corresponding `writeClient`.</span></span>

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

<span data-ttu-id="3b780-168">Per la lettura delle notifiche e revisioni, è necessario leggere le aree e i risultati di unione hello come illustrato nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="3b780-168">For reading notifications and reviews, you must read from both regions and union hello results as shown in hello following snippet:</span></span>

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

<span data-ttu-id="3b780-169">Se si sceglie una chiave di partizione ottimale e un partizionamento basato su account statici, è possibile ottenere operazioni di scrittura e lettura locali in più aree usando Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3b780-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="3b780-170"><a id="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3b780-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="3b780-171">In questo articolo è stato illustrato come è possibile usare modelli di lettura e scrittura in più aree con distribuzione globale con Cosmos DB usando la pubblicazione di contenuti come scenario di esempio.</span><span class="sxs-lookup"><span data-stu-id="3b780-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="3b780-172">Altre informazioni sul modo in cui Cosmos DB supporta la [distribuzione globale](distribute-data-globally.md)</span><span class="sxs-lookup"><span data-stu-id="3b780-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="3b780-173">Altre informazioni sui [failover automatici o manuali in Azure Cosmos DB](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="3b780-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="3b780-174">Informazioni sulla [coerenza globale con Azure Cosmos DB](consistency-levels.md)</span><span class="sxs-lookup"><span data-stu-id="3b780-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="3b780-175">Sviluppo con più aree tramite hello [Azure Cosmos DB - API DocumentDB](tutorial-global-distribution-documentdb.md)</span><span class="sxs-lookup"><span data-stu-id="3b780-175">Develop with multiple regions using hello [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="3b780-176">Sviluppo con più aree tramite hello [Azure Cosmos DB - API MongoDB](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="3b780-176">Develop with multiple regions using hello [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="3b780-177">Sviluppo con più aree tramite hello [Azure Cosmos DB - API di tabella](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="3b780-177">Develop with multiple regions using hello [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>
