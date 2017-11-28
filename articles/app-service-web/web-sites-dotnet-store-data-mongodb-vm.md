---
title: Creare un sito Web di Azure che si connette a MongoDB in esecuzione su una macchina virtuale in Azure
description: Un'esercitazione che illustra come usare Git per distribuire un'app ASP.NET in un sito Web di Azure connessa a MongoDB in una macchina virtuale.
tags: azure-portal
services: app-service\web, virtual-machines
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: adf7a472-ae00-45a8-aec4-06247e21318b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: cephalin
ms.openlocfilehash: a3f289ed9c764d0859573de4f834e042d0f103c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-in-azure-that-connects-to-mongodb-running-on-a-virtual-machine"></a><span data-ttu-id="d7be9-103">Creare un sito Web di Azure che si connette a MongoDB in esecuzione su una macchina virtuale in Azure</span><span class="sxs-lookup"><span data-stu-id="d7be9-103">Create a web app in Azure that connects to MongoDB running on a virtual machine</span></span>
<span data-ttu-id="d7be9-104">Utilizzando Git è possibile distribuire un'applicazione ASP.NET in un sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7be9-104">Using Git, you can deploy an ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="d7be9-105">In questa esercitazione verrà creata una semplice applicazione di elenco di attività ASP.NET MVC front-end che si connette a un database MongoDB in esecuzione in una macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="d7be9-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects to a MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="d7be9-106">[MongoDB][MongoDB] è un diffuso database NoSQL open source a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="d7be9-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="d7be9-107">Dopo aver eseguito e verificato l'applicazione ASP.NET sul computer di sviluppo, l'applicazione verrà caricata in un sito Web di Azure utilizzando Git.</span><span class="sxs-lookup"><span data-stu-id="d7be9-107">After running and testing the ASP.NET application on your development computer, you will upload the application to App Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="d7be9-108">Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="d7be9-108">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d7be9-109">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="d7be9-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="d7be9-110">Informazioni di background</span><span class="sxs-lookup"><span data-stu-id="d7be9-110">Background knowledge</span></span>
<span data-ttu-id="d7be9-111">Per questa esercitazione è utile, ma non obbligatorio, disporre di conoscenze sui seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="d7be9-111">Knowledge of the following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="d7be9-112">Driver C# per MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d7be9-112">The C# driver for MongoDB.</span></span> <span data-ttu-id="d7be9-113">Per altre informazioni sullo sviluppo di applicazioni C# con MongoDB, vedere [CSharp Language Center][MongoC#LangCenter] (Centro per il linguaggio CSharp) di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d7be9-113">For more information on developing C# applications against MongoDB, see the MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="d7be9-114">Framework applicazione Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d7be9-114">The ASP .NET web application framework.</span></span> <span data-ttu-id="d7be9-115">Per informazioni complete, vedere il [sito Web ASP.net][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="d7be9-115">You can learn all about it at the [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="d7be9-116">Framework applicazione Web ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="d7be9-116">The ASP .NET MVC web application framework.</span></span> <span data-ttu-id="d7be9-117">Per informazioni complete, vedere il [sito Web MVC ASP.NET][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="d7be9-117">You can learn all about it at the [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="d7be9-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="d7be9-118">Azure.</span></span> <span data-ttu-id="d7be9-119">Per informazioni preliminari, vedere [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="d7be9-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7be9-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d7be9-120">Prerequisites</span></span>
* <span data-ttu-id="d7be9-121">[Visual Studio Express 2013 per Web][VSEWeb] o [Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="d7be9-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="d7be9-122">Azure SDK per .NET</span><span class="sxs-lookup"><span data-stu-id="d7be9-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="d7be9-123">Una sottoscrizione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d7be9-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="d7be9-124">Creare una macchina virtuale e installare MongoDB</span><span class="sxs-lookup"><span data-stu-id="d7be9-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="d7be9-125">In questa esercitazione si presuppone che l'utente abbia creato una macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="d7be9-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="d7be9-126">Dopo aver creato la macchina virtuale è necessario installarvi MongoDB:</span><span class="sxs-lookup"><span data-stu-id="d7be9-126">After creating the virtual machine you need to install MongoDB on the virtual machine:</span></span>

* <span data-ttu-id="d7be9-127">Per creare una macchina virtuale di Windows e installare MongoDB, vedere [Installare MongoDB in una macchina virtuale che esegue Windows Server in Azure][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="d7be9-127">To create a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="d7be9-128">Dopo aver creato la macchina virtuale in Azure e installato MongoDB, prendere nota del nome DNS della macchina virtuale (ad esempio; "testlinuxvm.cloudapp.net") e della porta esterna per MongoDB specificata nell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="d7be9-128">After you have created the virtual machine in Azure and installed MongoDB, be sure to remember the DNS name of the virtual machine ("testlinuxvm.cloudapp.net", for example) and the external port for MongoDB that you specified in the endpoint.</span></span>  <span data-ttu-id="d7be9-129">Sarà necessario utilizzare queste informazioni più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d7be9-129">You will need this information later in the tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-the-application"></a><span data-ttu-id="d7be9-130">Creazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="d7be9-130">Create the application</span></span>
<span data-ttu-id="d7be9-131">In questa sezione verranno creare un'applicazione ASP.NET denominata "My Task List" utilizzando Visual Studio e verrà eseguita una distribuzione iniziale in Azure applicazione servizio Web Apps.</span><span class="sxs-lookup"><span data-stu-id="d7be9-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment to Azure App Service Web Apps.</span></span> <span data-ttu-id="d7be9-132">L'applicazione verrà eseguita localmente, ma si connetterà alla macchina virtuale in Azure e utilizzerà l'istanza MongoDB creata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d7be9-132">You will run the application locally, but it will connect to your virtual machine on Azure and use the MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="d7be9-133">In Visual Studio, fare clic su **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Pagina iniziale Nuovo progetto][StartPageNewProject]
2. <span data-ttu-id="d7be9-135">Nel riquadro sinistro della finestra **Nuovo progetto** selezionare **Visual C#**, quindi selezionare **Web**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-135">In the **New Project** window, in the left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="d7be9-136">Nel riquadro centrale selezionare **Applicazione Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-136">In the middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="d7be9-137">In basso, assegnare al progetto il nome "MyTaskListApp", quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-137">At the bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Finestra di dialogo Nuovo progetto][NewProjectMyTaskListApp]
3. <span data-ttu-id="d7be9-139">Nella finestra di dialogo **Nuovo progetto ASP.NET** selezionare **MVC**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-139">In the **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![Selezione di un template MVC][VS2013SelectMVCTemplate]
4. <span data-ttu-id="d7be9-141">Se non è già stata effettuata in Microsoft Azure, verrà richiesto di accedere.</span><span class="sxs-lookup"><span data-stu-id="d7be9-141">If you aren't already signed into Microsoft Azure, you will be prompted to sign in.</span></span> <span data-ttu-id="d7be9-142">Seguire le istruzioni per accedere a Azure.</span><span class="sxs-lookup"><span data-stu-id="d7be9-142">Follow the prompts to sign into Azure.</span></span>
5. <span data-ttu-id="d7be9-143">Una volta che si sono connessi, è possibile avviare la configurazione dell'applicazione web servizio App.</span><span class="sxs-lookup"><span data-stu-id="d7be9-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="d7be9-144">Specificare il **nome dell'app Web**, **piano di servizio App**, **gruppo di risorse** e **area**, quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-144">Specify the **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="d7be9-145">Al termine della creazione del progetto, di attesa per l'applicazione web da creare nel servizio App Azure come indicato nella **attività servizio App Azure** finestra.</span><span class="sxs-lookup"><span data-stu-id="d7be9-145">After the project creation completes, wait for the web app to be created in Azure App Service as indicated in the **Azure App Service Activity** window.</span></span> <span data-ttu-id="d7be9-146">Fare clic su **MyTaskListApp pubblica per questa applicazione Web ora**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-146">Then, click **Publish MyTaskListApp to this Web App now**.</span></span>
7. <span data-ttu-id="d7be9-147">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="d7be9-148">Una volta pubblicata l'applicazione ASP.NET predefinita in Azure applicazione servizio Web Apps, questa verrà avviata nel browser.</span><span class="sxs-lookup"><span data-stu-id="d7be9-148">Once your default ASP.NET application is published to Azure App Service Web Apps, it will be launched in the browser.</span></span>

## <a name="install-the-mongodb-c-driver"></a><span data-ttu-id="d7be9-149">Installazione del driver MongoDB C#</span><span class="sxs-lookup"><span data-stu-id="d7be9-149">Install the MongoDB C# driver</span></span>
<span data-ttu-id="d7be9-150">MongoDB offre il supporto lato client per le applicazioni C# tramite un driver, che è necessario installare nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="d7be9-150">MongoDB offers client-side support for C# applications through a driver, which you need to install on your local development computer.</span></span> <span data-ttu-id="d7be9-151">Il driver C# è disponibile tramite NuGet.</span><span class="sxs-lookup"><span data-stu-id="d7be9-151">The C# driver is available through NuGet.</span></span>

<span data-ttu-id="d7be9-152">Per installare il driver MongoDB C#:</span><span class="sxs-lookup"><span data-stu-id="d7be9-152">To install the MongoDB C# driver:</span></span>

1. <span data-ttu-id="d7be9-153">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **MyTaskListApp** e selezionare **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-153">In **Solution Explorer**, right-click the **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![Manage NuGet Packages][VS2013ManageNuGetPackages]
2. <span data-ttu-id="d7be9-155">Nel riquadro sinistro della finestra **Gestisci pacchetti NuGet** fare clic su **Online**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-155">In the **Manage NuGet Packages** window, in the left pane, click **Online**.</span></span> <span data-ttu-id="d7be9-156">Nella casella di **ricerca online** a destra, digitare "mongodb.driver".</span><span class="sxs-lookup"><span data-stu-id="d7be9-156">In the **Search Online** box on the right, type "mongodb.driver".</span></span>  <span data-ttu-id="d7be9-157">Fare clic su **Installa** per installare il driver.</span><span class="sxs-lookup"><span data-stu-id="d7be9-157">Click **Install** to install the driver.</span></span>
   
    ![Ricerca del driver MongoDB C#][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="d7be9-159">Fare clic su **Accetto** per accettare i termini di licenza di 10gen, Inc.</span><span class="sxs-lookup"><span data-stu-id="d7be9-159">Click **I Accept** to accept the 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="d7be9-160">Dopo aver installato il driver, fare clic su **Chiudi** .</span><span class="sxs-lookup"><span data-stu-id="d7be9-160">Click **Close** after the driver has installed.</span></span>
    <span data-ttu-id="d7be9-161">![Driver MongoDB C# installato][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="d7be9-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="d7be9-162">Il driver MongoDB C# è ora installato.</span><span class="sxs-lookup"><span data-stu-id="d7be9-162">The MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="d7be9-163">I riferimenti alle librerie **MongoDB.Bson**, **MongoDB.Driver** e **MongoDB.Driver.Core** sono stati aggiunti al progetto.</span><span class="sxs-lookup"><span data-stu-id="d7be9-163">References to the **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added to the project.</span></span>

![Riferimenti al driver MongoDB C#][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="d7be9-165">Aggiunta di un modello</span><span class="sxs-lookup"><span data-stu-id="d7be9-165">Add a model</span></span>
<span data-ttu-id="d7be9-166">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella *Modelli*, quindi scegliere **Aggiungi**, **Classe** per aggiungere una nuova classe e denominarla *TaskModel.cs*.</span><span class="sxs-lookup"><span data-stu-id="d7be9-166">In **Solution Explorer**, right-click the *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="d7be9-167">In *TaskModel.cs*, sostituire il codice esistente con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d7be9-167">In *TaskModel.cs*, replace the existing code with the following code:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MongoDB.Bson.Serialization.Attributes;
    using MongoDB.Bson.Serialization.IdGenerators;
    using MongoDB.Bson;

    namespace MyTaskListApp.Models
    {
        public class MyTask
        {
            [BsonId(IdGenerator = typeof(CombGuidGenerator))]
            public Guid Id { get; set; }

            [BsonElement("Name")]
            public string Name { get; set; }

            [BsonElement("Category")]
            public string Category { get; set; }

            [BsonElement("Date")]
            public DateTime Date { get; set; }

            [BsonElement("CreatedDate")]
            public DateTime CreatedDate { get; set; }

        }
    }

## <a name="add-the-data-access-layer"></a><span data-ttu-id="d7be9-168">Aggiunta di un livello di accesso ai dati</span><span class="sxs-lookup"><span data-stu-id="d7be9-168">Add the data access layer</span></span>
<span data-ttu-id="d7be9-169">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto *MyTaskListApp*, quindi scegliere **Aggiungi**, **Nuova cartella** e scegliere la cartella denominata *DAL*.</span><span class="sxs-lookup"><span data-stu-id="d7be9-169">In **Solution Explorer**, right-click the *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="d7be9-170">Fare clic con il pulsante destro del mouse sulla cartella *DAL* e scegliere **Aggiungi**, **Classe** per aggiungere una nuova classe.</span><span class="sxs-lookup"><span data-stu-id="d7be9-170">Right-click the *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="d7be9-171">Assegnare al file della classe il nome *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="d7be9-171">Name the class file *Dal.cs*.</span></span>  <span data-ttu-id="d7be9-172">In *Dal.cs*sostituire il codice esistente con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d7be9-172">In *Dal.cs*, replace the existing code with the following code:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;


    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            private MongoServer mongoServer = null;
            private bool disposed = false;

            // To do: update the connection string with the DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

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
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClient client = new MongoClient(connectionString);
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
                        if (mongoServer != null)
                        {
                            this.mongoServer.Disconnect();
                        }
                    }
                }

                this.disposed = true;
            }

            # endregion
        }
    }

## <a name="add-a-controller"></a><span data-ttu-id="d7be9-173">Aggiunta di un controller</span><span class="sxs-lookup"><span data-stu-id="d7be9-173">Add a controller</span></span>
<span data-ttu-id="d7be9-174">Aprire il file *Controllers\HomeController.cs* in **Esplora soluzioni** e sostituire il codice esistente con quello seguente:</span><span class="sxs-lookup"><span data-stu-id="d7be9-174">Open the *Controllers\HomeController.cs* file in **Solution Explorer** and replace the existing code with the following:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.Mvc;
    using MyTaskListApp.Models;
    using System.Configuration;

    namespace MyTaskListApp.Controllers
    {
        public class HomeController : Controller, IDisposable
        {
            private Dal dal = new Dal();
            private bool disposed = false;
            //
            // GET: /MyTask/

            public ActionResult Index()
            {
                return View(dal.GetAllTasks());
            }

            //
            // GET: /MyTask/Create

            public ActionResult Create()
            {
                return View();
            }

            //
            // POST: /MyTask/Create

            [HttpPost]
            public ActionResult Create(MyTask task)
            {
                try
                {
                    dal.CreateTask(task);
                    return RedirectToAction("Index");
                }
                catch
                {
                    return View();
                }
            }

            public ActionResult About()
            {
                return View();
            }

            # region IDisposable

            new protected void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            new protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        this.dal.Dispose();
                    }
                }

                this.disposed = true;
            }

            # endregion

        }
    }

## <a name="set-up-the-styles"></a><span data-ttu-id="d7be9-175">Impostare gli stili</span><span class="sxs-lookup"><span data-stu-id="d7be9-175">Set up the styles</span></span>
<span data-ttu-id="d7be9-176">Per modificare il titolo nella parte superiore della pagina, aprire il file *Views\Shared\\_Layout.cshtml* in **Esplora soluzioni** e sostituire "Application name" nell'intestazione della barra di navigazione con "My Task List Application" in modo che i risultati avranno un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d7be9-176">To change the title at the top of the page, open the *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in the navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="d7be9-177">Per impostare il menu Elenco attività, aprire il file *\Views\Home\Index.cshtml* e sostituire il codice esistente con il seguente codice:</span><span class="sxs-lookup"><span data-stu-id="d7be9-177">In order to set up the Task List menu, open the *\Views\Home\Index.cshtml* file and replace the existing code with the following code:</span></span>

    @model IEnumerable<MyTaskListApp.Models.MyTask>

    @{
        ViewBag.Title = "My Task List";
    }

    <h2>My Task List</h2>

    <table border="1">
        <tr>
            <th>Task</th>
            <th>Category</th>
            <th>Date</th>

        </tr>

    @foreach (var item in Model) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.Name)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Category)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Date)
            </td>

        </tr>
    }

    </table>
    <div>  @Html.Partial("Create", new MyTaskListApp.Models.MyTask())</div>


<span data-ttu-id="d7be9-178">Per aggiungere la possibilità di creare una nuova attività, fare clic con il pulsante destro del mouse sulla cartella *Views\Home\\\*, quindi scegliere **Aggiungi**, **Visualizzazione** per aggiungere una nuova visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="d7be9-178">To add the ability to create a new task, right-click the *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="d7be9-179">Assegnare alla visualizzazione il nome *Crea*.</span><span class="sxs-lookup"><span data-stu-id="d7be9-179">Name the view *Create*.</span></span> <span data-ttu-id="d7be9-180">Sostituire il codice con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d7be9-180">Replace the code with the following:</span></span>

    @model MyTaskListApp.Models.MyTask

    <script src="@Url.Content("~/Scripts/jquery-1.10.2.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.unobtrusive.min.js")" type="text/javascript"></script>

    @using (Html.BeginForm("Create", "Home")) {
        @Html.ValidationSummary(true)
        <fieldset>
            <legend>New Task</legend>

            <div class="editor-label">
                @Html.LabelFor(model => model.Name)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Name)
                @Html.ValidationMessageFor(model => model.Name)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Category)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Category)
                @Html.ValidationMessageFor(model => model.Category)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Date)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Date)
                @Html.ValidationMessageFor(model => model.Date)
            </div>

            <p>
                <input type="submit" value="Create" />
            </p>
        </fieldset>
    }

<span data-ttu-id="d7be9-181">**Controllers\HomeController.cs** dovrebbe risultare simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d7be9-181">**Solution Explorer** should look like this:</span></span>

![Controllers\HomeController.cs][SolutionExplorerMyTaskListApp]

## <a name="set-the-mongodb-connection-string"></a><span data-ttu-id="d7be9-183">Impostazione della stringa di connessione MongoDB</span><span class="sxs-lookup"><span data-stu-id="d7be9-183">Set the MongoDB connection string</span></span>
<span data-ttu-id="d7be9-184">In **Esplora soluzioni**aprire il file *DAL/Dal.cs* .</span><span class="sxs-lookup"><span data-stu-id="d7be9-184">In **Solution Explorer**, open the *DAL/Dal.cs* file.</span></span> <span data-ttu-id="d7be9-185">Individuare la riga di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d7be9-185">Find the following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="d7be9-186">Sostituire `<vm-dns-name>` con il nome DNS della macchina virtuale che esegue MongoDB creata nel passaggio [Creare una macchina virtuale e installare MongoDB][Create a virtual machine and install MongoDB] di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d7be9-186">Replace `<vm-dns-name>` with the DNS name of the virtual machine running MongoDB you created in the [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="d7be9-187">Per individuare il nome DNS della macchina virtuale, passare al portale di gestione di Azure, selezionare **Macchine virtuali** e individuare **Nome DN**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-187">To find the DNS name of your virtual machine, go to the Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="d7be9-188">Se il nome DNS della macchina virtuale è "testlinuxvm.cloudapp.net" e MongoDB è in ascolto sulla porta predefinita 27017, la riga di codice della stringa di connessione avrà il seguente aspetto:</span><span class="sxs-lookup"><span data-stu-id="d7be9-188">If the DNS name of the virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on the default port 27017, the connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="d7be9-189">Se l'endpoint della macchina virtuale specifica una porta esterna diversa per MongoDB, è possibile specificare la porta nella stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="d7be9-189">If the virtual machine endpoint specifies a different external port for MongoDB, you can specifiy the port in the connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="d7be9-190">Per altre informazioni sulle stringhe di connessione di MongoDB, vedere [Connections][MongoConnectionStrings] (Connessioni).</span><span class="sxs-lookup"><span data-stu-id="d7be9-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-the-local-deployment"></a><span data-ttu-id="d7be9-191">Test della distribuzione locale</span><span class="sxs-lookup"><span data-stu-id="d7be9-191">Test the local deployment</span></span>
<span data-ttu-id="d7be9-192">Per eseguire l'applicazione sul computer di sviluppo, selezionare **Avvia debug** dal menu **Debug** oppure premere **F5**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-192">To run your application on your development computer, select **Start Debugging** from the **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="d7be9-193">IIS Express viene avviato e nel browser viene avviata la home page dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d7be9-193">IIS Express starts and a browser opens and launches the application's home page.</span></span>  <span data-ttu-id="d7be9-194">È possibile aggiungere una nuova attività, che verrà aggiunta al database MongoDB in esecuzione sulla macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="d7be9-194">You can add a new task, which will be added to the MongoDB database running on your virtual machine in Azure.</span></span>

![Applicazione My Task List][TaskListAppBlank]

## <a name="publish-to-azure-app-service-web-apps"></a><span data-ttu-id="d7be9-196">Pubblicare nelle App Web di Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d7be9-196">Publish to Azure App Service Web Apps</span></span>
<span data-ttu-id="d7be9-197">In questa sezione verrà pubblicato le modifiche in Azure applicazione servizio Web Apps.</span><span class="sxs-lookup"><span data-stu-id="d7be9-197">In this section you will publish your changes to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="d7be9-198">In Esplora soluzioni, fare clic **MyTaskListApp** nuovamente e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="d7be9-199">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="d7be9-200">Si noterà ora l'applicazione web in esecuzione in Azure App servizio e l'accesso al database MongoDB in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7be9-200">You should now see your web app running in Azure App Service and accessing the MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="d7be9-201">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="d7be9-201">Summary</span></span>
<span data-ttu-id="d7be9-202">L'applicazione ASP.NET è stata correttamente distribuita in un sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7be9-202">You have now successfully deployed your ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="d7be9-203">Per visualizzare l'applicazione web:</span><span class="sxs-lookup"><span data-stu-id="d7be9-203">To view the web app:</span></span>

1. <span data-ttu-id="d7be9-204">Accedere al Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7be9-204">Log into the Azure Portal.</span></span>
2. <span data-ttu-id="d7be9-205">Fare clic su **App Web**.</span><span class="sxs-lookup"><span data-stu-id="d7be9-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="d7be9-206">Selezionare l'applicazione web nel **applicazioni Web** elenco.</span><span class="sxs-lookup"><span data-stu-id="d7be9-206">Select your web app in the **Web Apps** list.</span></span>

<span data-ttu-id="d7be9-207">Per altre informazioni sullo sviluppo di applicazioni C# con MongoDB, vedere [CSharp Language Center][MongoC#LangCenter] (Centro per il linguaggio CSharp).</span><span class="sxs-lookup"><span data-stu-id="d7be9-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- HYPERLINKS -->

[AzurePortal]: http://manage.windowsazure.com
[WindowsAzure]: http://www.windowsazure.com
[MongoC#LangCenter]: http://docs.mongodb.org/ecosystem/drivers/csharp/
[MVCWebSite]: http://www.asp.net/mvc
[ASP.NET]: http://www.asp.net/
[MongoConnectionStrings]: http://www.mongodb.org/display/DOCS/Connections
[MongoDB]: http://www.mongodb.org
[InstallMongoOnWindowsVM]:../virtual-machines/windows/classic/install-mongodb.md
[VSEWeb]: http://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express
[VSUlt]: http://www.microsoft.com/visualstudio/eng/2013-downloads

<!-- IMAGES -->


[StartPageNewProject]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProject.png
[NewProjectMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProjectMyTaskListApp.png
[VS2013SelectMVCTemplate]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013SelectMVCTemplate.png
[VS2013DefaultMVCApplication]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013DefaultMVCApplication.png
[VS2013ManageNuGetPackages]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013ManageNuGetPackages.png
[SearchforMongoDBCSharpDriver]: ./media/web-sites-dotnet-store-data-mongodb-vm/SearchforMongoDBCSharpDriver.png
[MongoDBCsharpDriverInstalled]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCsharpDriverInstalled.png
[MongoDBCSharpDriverReferences]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCSharpDriverReferences.png
[SolutionExplorerMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/SolutionExplorerMyTaskListApp.png
[TaskListAppBlank]: ./media/web-sites-dotnet-store-data-mongodb-vm/TaskListAppBlank.png
[WAWSCreateWebSite]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSCreateWebSite.png
[WAWSDashboardMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSDashboardMyTaskListApp.png
[Image9]: ./media/web-sites-dotnet-store-data-mongodb-vm/RepoReady.png
[Image10]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitInstructions.png
[Image11]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitDeploymentComplete.png

<!-- TOC BOOKMARKS -->
[Create a virtual machine and install MongoDB]: #virtualmachine
[Create and run the My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy the ASP.NET application to the web site using Git]: #deployapp
