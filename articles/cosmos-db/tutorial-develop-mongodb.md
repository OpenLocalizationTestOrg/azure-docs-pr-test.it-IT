---
title: Usare l'API di Azure Cosmos DB per MongoDB per creare un'app Web | Microsoft Docs
description: Esercitazione di Azure Cosmos DB per creare un'app Web di database online usando l'API per MongoDB.
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
ms.openlocfilehash: ff277c7f88359cd977424f2e0958c69e2547a2af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-connect-to-a-mongodb-app-using-net"></a><span data-ttu-id="7ec20-104">Azure Cosmos DB: Connettersi a un'app MongoDB usando .NET</span><span class="sxs-lookup"><span data-stu-id="7ec20-104">Azure Cosmos DB: Connect to a MongoDB app using .NET</span></span>

<span data-ttu-id="7ec20-105">Azure Cosmos DB è il servizio di database di Microsoft multimodello distribuito a livello globale.</span><span class="sxs-lookup"><span data-stu-id="7ec20-105">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="7ec20-106">È possibile creare ed eseguire rapidamente query su database di documenti, coppie chiave-valore e grafi, sfruttando in ognuno dei casi i vantaggi offerti dalle funzionalità di scalabilità orizzontale e distribuzione globale alla base di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7ec20-106">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="7ec20-107">Questa esercitazione illustra come creare un account Azure Cosmos DB usando il portale di Azure e come creare un database e una raccolta per l'archiviazione di dati usando l'[API per MongoDB](mongodb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7ec20-107">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal, and how to create a database and collection to store data using the [MongoDB API](mongodb-introduction.md).</span></span> 

<span data-ttu-id="7ec20-108">Questa esercitazione illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="7ec20-108">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7ec20-109">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7ec20-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="7ec20-110">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="7ec20-110">Update your connection string</span></span>
> * <span data-ttu-id="7ec20-111">Creare un'app MongoDB in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7ec20-111">Create a MongoDB app on a virtual machine</span></span> 


## <a name="create-a-database-account"></a><span data-ttu-id="7ec20-112">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="7ec20-112">Create a database account</span></span>

<span data-ttu-id="7ec20-113">Si inizia creando un account Azure Cosmos DB nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7ec20-113">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="7ec20-114">È stato già creato un account Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="7ec20-114">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="7ec20-115">In questo caso passare a [Configurare la soluzione di Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="7ec20-115">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="7ec20-116">Si dispone di un account Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="7ec20-116">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="7ec20-117">In questo caso l'account è ora un account Azure Cosmos DB ed è possibile passare a [Configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="7ec20-117">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="7ec20-118">Se si usa l'emulatore Azure Cosmos DB, seguire i passaggi descritti nell'articolo [Azure Cosmos DB Emulator](local-emulator.md) (Emulatore Azure Cosmos DB) per configurare l'emulatore e proseguire con il passaggio [Configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="7ec20-118">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a><span data-ttu-id="7ec20-119">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="7ec20-119">Update your connection string</span></span>

1. <span data-ttu-id="7ec20-120">Nella pagina **Azure Cosmos DB** del portale di Azure selezionare l'account dell'API per MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7ec20-120">In the Azure portal, in the **Azure Cosmos DB** page, select the API for MongoDB account.</span></span> 
2. <span data-ttu-id="7ec20-121">Nella barra a sinistra del pannello Account fare clic su **Avvio rapido**.</span><span class="sxs-lookup"><span data-stu-id="7ec20-121">In the left bar of the account blade, click **Quick start**.</span></span> 
3. <span data-ttu-id="7ec20-122">Scegliere la piattaforma (*driver .NET*, *driver Node.js*, *MongoDB Shell*, *driver Java*, *driver Python*).</span><span class="sxs-lookup"><span data-stu-id="7ec20-122">Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*).</span></span> <span data-ttu-id="7ec20-123">Se il driver o lo strumento non è visualizzato nell'elenco, tenere presente che altri frammenti di codice di connessione vengono continuamente documentati.</span><span class="sxs-lookup"><span data-stu-id="7ec20-123">If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets.</span></span> 
4. <span data-ttu-id="7ec20-124">Copiare e incollare il frammento di codice nell'app MongoDB per iniziare.</span><span class="sxs-lookup"><span data-stu-id="7ec20-124">Copy and paste the code snippet into your MongoDB app, and you are ready to go.</span></span>

## <a name="set-up-your-mongodb-app"></a><span data-ttu-id="7ec20-125">Configurare l'app MongoDB</span><span class="sxs-lookup"><span data-stu-id="7ec20-125">Set up your MongoDB app</span></span>

<span data-ttu-id="7ec20-126">È possibile usare l'esercitazione [Creare un'app Web di Azure che si connette a MongoDB in esecuzione su una macchina virtuale](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md), con modifiche minime, per configurare rapidamente un'applicazione MongoDB, in locale o pubblicata in un'app Web di Azure, che si connette a un account dell'API per MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7ec20-126">You can use the [Create a web app in Azure that connects to MongoDB running on a virtual machine](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial, with minimal modification, to quickly setup a MongoDB application (either locally or published to an Azure web app) that connects to an API for MongoDB account.</span></span>  

1. <span data-ttu-id="7ec20-127">Seguire l'esercitazione, con una modifica.</span><span class="sxs-lookup"><span data-stu-id="7ec20-127">Follow the tutorial, with one modification.</span></span>  <span data-ttu-id="7ec20-128">Sostituire il codice del file Dal.cs con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="7ec20-128">Replace the Dal.cs code with this:</span></span>

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
   
            // To do: update the connection string with the DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net
            private string connectionString = "mongodb://localhost:27017";
            private string userName = "<your user name>";
            private string host = "<your host>";
            private string password = "<your password>";
   
            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  The database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";
   
            // Default constructor.        
            public Dal()
            {
            }
   
            // Gets all Task items from the MongoDB server.        
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
   
            // Creates a Task and inserts it into the collection in MongoDB.
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

2. <span data-ttu-id="7ec20-129">Modificare le variabili seguenti nel file Dal.cs in base alle impostazioni dell'account nella pagina Chiavi del portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="7ec20-129">Modify the following variables in the Dal.cs file per your account settings from the Keys page in the Azure portal:</span></span>

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. <span data-ttu-id="7ec20-130">Usare l'app.</span><span class="sxs-lookup"><span data-stu-id="7ec20-130">Use the app!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="7ec20-131">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="7ec20-131">Clean up resources</span></span>

<span data-ttu-id="7ec20-132">Se non si prevede di continuare a usare questa app, seguire questa procedura per eliminare tutte le risorse create da questa esercitazione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7ec20-132">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span> 

1. <span data-ttu-id="7ec20-133">Scegliere **Gruppi di risorse** dal menu a sinistra del portale di Azure e quindi fare clic sul nome della risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="7ec20-133">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="7ec20-134">Nella pagina del gruppo di risorse fare clic su **Elimina**, digitare il nome della risorsa da eliminare nella casella di testo e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="7ec20-134">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ec20-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7ec20-135">Next steps</span></span>

<span data-ttu-id="7ec20-136">In questa esercitazione sono state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7ec20-136">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7ec20-137">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7ec20-137">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="7ec20-138">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="7ec20-138">Update your connection string</span></span>
> * <span data-ttu-id="7ec20-139">Creare un'app MongoDB in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7ec20-139">Create a MongoDB app on a virtual machine</span></span>

<span data-ttu-id="7ec20-140">È possibile passare all'esercitazione successiva e importare i dati di MongoDB in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7ec20-140">You can proceed to the next tutorial and import your MongoDB data to Azure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ec20-141">Importare i dati di MongoDB in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7ec20-141">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)

