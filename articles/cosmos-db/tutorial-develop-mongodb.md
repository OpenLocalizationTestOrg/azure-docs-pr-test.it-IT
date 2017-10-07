---
title: API del database di aaaUse Azure Cosmos per MongoDB toobuild un'app web | Documenti Microsoft
description: Un'esercitazione DB Cosmos Azure che crea un'app web di database online tramite API di hello per MongoDB.
keywords: esempi di mongodb
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 61a2ab3a-2fc3-4d49-a263-ed87c66628f6
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 6dfa7fef49fc53ea2fcfcfbad3b3fcf97ac18e94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a><span data-ttu-id="fbb51-104">Azure Cosmos DB: Connettersi tooa MongoDB app con .NET</span><span class="sxs-lookup"><span data-stu-id="fbb51-104">Azure Cosmos DB: Connect tooa MongoDB app using .NET</span></span>

<span data-ttu-id="fbb51-105">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fbb51-105">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="fbb51-106">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="fbb51-106">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="fbb51-107">Questa esercitazione viene illustrato come toocreate un account Azure Cosmos DB usando hello portale di Azure e come toocreate un database e dati toostore insieme utilizzando hello [MongoDB API](mongodb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fbb51-107">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and how toocreate a database and collection toostore data using hello [MongoDB API](mongodb-introduction.md).</span></span> 

<span data-ttu-id="fbb51-108">Questa esercitazione sono trattati hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="fbb51-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fbb51-109">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fbb51-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="fbb51-110">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="fbb51-110">Update your connection string</span></span>
> * <span data-ttu-id="fbb51-111">Creare un'app MongoDB in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fbb51-111">Create a MongoDB app on a virtual machine</span></span> 


## <a name="create-a-database-account"></a><span data-ttu-id="fbb51-112">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="fbb51-112">Create a database account</span></span>

<span data-ttu-id="fbb51-113">Iniziamo mediante la creazione di un account Azure Cosmos DB in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fbb51-113">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="fbb51-114">È stato già creato un account Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="fbb51-114">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="fbb51-115">In caso affermativo, andare troppo[configurazione della soluzione di Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="fbb51-115">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="fbb51-116">Si dispone di un account Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="fbb51-116">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="fbb51-117">Se in tal caso, l'account è un account Azure Cosmos DB ed è possibile andare troppo[configurazione della soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="fbb51-117">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="fbb51-118">Se si utilizza hello Azure Cosmos DB emulatore, eseguire le operazioni di hello in [emulatore di Azure Cosmos DB](local-emulator.md) toosetup hello emulatore e andare troppo[configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="fbb51-118">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a><span data-ttu-id="fbb51-119">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="fbb51-119">Update your connection string</span></span>

1. <span data-ttu-id="fbb51-120">Nel portale di Azure in hello hello **Azure Cosmos DB** selezionare hello API per conto di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fbb51-120">In hello Azure portal, in hello **Azure Cosmos DB** page, select hello API for MongoDB account.</span></span> 
2. <span data-ttu-id="fbb51-121">Nella barra sinistra di hello del Pannello di hello account, fare clic su **avvio rapido**.</span><span class="sxs-lookup"><span data-stu-id="fbb51-121">In hello left bar of hello account blade, click **Quick start**.</span></span> 
3. <span data-ttu-id="fbb51-122">Scegliere la piattaforma (*driver .NET*, *driver Node.js*, *MongoDB Shell*, *driver Java*, *driver Python*).</span><span class="sxs-lookup"><span data-stu-id="fbb51-122">Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*).</span></span> <span data-ttu-id="fbb51-123">Se il driver o lo strumento non è visualizzato nell'elenco, tenere presente che altri frammenti di codice di connessione vengono continuamente documentati.</span><span class="sxs-lookup"><span data-stu-id="fbb51-123">If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets.</span></span> 
4. <span data-ttu-id="fbb51-124">Copiare e incollare il frammento di codice hello app MongoDB, e si è pronto toogo.</span><span class="sxs-lookup"><span data-stu-id="fbb51-124">Copy and paste hello code snippet into your MongoDB app, and you are ready toogo.</span></span>

## <a name="set-up-your-mongodb-app"></a><span data-ttu-id="fbb51-125">Configurare l'app MongoDB</span><span class="sxs-lookup"><span data-stu-id="fbb51-125">Set up your MongoDB app</span></span>

<span data-ttu-id="fbb51-126">È possibile utilizzare hello [creare un'app web in Azure che si connette in esecuzione in una macchina virtuale tooMongoDB](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) dell'esercitazione, con modifiche minime, tooquickly programma di installazione di un'applicazione di MongoDB (sia localmente o un'app web di Azure pubblicata tooan) che si connette tooan API per conto di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fbb51-126">You can use hello [Create a web app in Azure that connects tooMongoDB running on a virtual machine](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial, with minimal modification, tooquickly setup a MongoDB application (either locally or published tooan Azure web app) that connects tooan API for MongoDB account.</span></span>  

1. <span data-ttu-id="fbb51-127">Seguire l'esercitazione di hello, con una modifica.</span><span class="sxs-lookup"><span data-stu-id="fbb51-127">Follow hello tutorial, with one modification.</span></span>  <span data-ttu-id="fbb51-128">Sostituire il codice di Dal.cs hello con questo:</span><span class="sxs-lookup"><span data-stu-id="fbb51-128">Replace hello Dal.cs code with this:</span></span>

    ```csharp   
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;
    using System.Security.Authentication;
   
    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            //private MongoServer mongoServer = null;
            private bool disposed = false;
   
            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net
            private string connectionString = "mongodb://localhost:27017";
            private string userName = "<your user name>";
            private string host = "<your host>";
            private string password = "<your password>";
   
            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";
   
            // Default constructor.        
            public Dal()
            {
            }
   
            // Gets all Task items from hello MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }
   
            // Creates a Task and inserts it into hello collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }
   
            private IMongoCollection<MyTask> GetTasksCollection()
            {
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
   
                MongoClient client = new MongoClient(settings);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
                MongoClient client = new MongoClient(settings);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            # region IDisposable
   
            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }
   
            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                    }
                }
   
                this.disposed = true;
            }
   
            # endregion
        }
    }
    ```

2. <span data-ttu-id="fbb51-129">Modificare hello seguendo le variabili nel file Dal.cs hello per le impostazioni dell'account dalla pagina chiavi hello hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="fbb51-129">Modify hello following variables in hello Dal.cs file per your account settings from hello Keys page in hello Azure portal:</span></span>

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. <span data-ttu-id="fbb51-130">Utilizzare l'applicazione hello!</span><span class="sxs-lookup"><span data-stu-id="fbb51-130">Use hello app!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="fbb51-131">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="fbb51-131">Clean up resources</span></span>

<span data-ttu-id="fbb51-132">Se non si ha intenzione toocontinue toouse questa app, utilizzare hello seguendo i passaggi toodelete tutte le risorse create da questa esercitazione in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fbb51-132">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span> 

1. <span data-ttu-id="fbb51-133">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="fbb51-133">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="fbb51-134">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="fbb51-134">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbb51-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fbb51-135">Next steps</span></span>

<span data-ttu-id="fbb51-136">In questa esercitazione, effettuata seguente hello:</span><span class="sxs-lookup"><span data-stu-id="fbb51-136">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fbb51-137">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fbb51-137">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="fbb51-138">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="fbb51-138">Update your connection string</span></span>
> * <span data-ttu-id="fbb51-139">Creare un'app MongoDB in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fbb51-139">Create a MongoDB app on a virtual machine</span></span>

<span data-ttu-id="fbb51-140">È possibile continuare l'esercitazione successiva toohello e importare il tooAzure dati MongoDB DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="fbb51-140">You can proceed toohello next tutorial and import your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="fbb51-141">Importare i dati di MongoDB in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fbb51-141">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)

