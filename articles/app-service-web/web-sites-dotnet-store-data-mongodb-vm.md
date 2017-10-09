---
title: aaaCreate un'app web in Azure che si connette tooMongoDB in esecuzione in una macchina virtuale
description: "Un'esercitazione che illustra la modalità di connessione un tooAzure app ASP.NET servizio App, di toouse Git toodeploy tooMongoDB in una macchina virtuale di Azure."
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
ms.openlocfilehash: 1f5f42c28c3c294d92c9ebf1499374931d47c010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a><span data-ttu-id="00890-103">Creare un'app web in Azure che si connette tooMongoDB in esecuzione in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="00890-103">Create a web app in Azure that connects tooMongoDB running on a virtual machine</span></span>
<span data-ttu-id="00890-104">Usa Git, è possibile distribuire un tooAzure applicazione ASP.NET App del servizio Web App.</span><span class="sxs-lookup"><span data-stu-id="00890-104">Using Git, you can deploy an ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="00890-105">In questa esercitazione si creerà un semplice front-end ASP.NET MVC applicazione elenco attività che si connette il database di MongoDB tooa in esecuzione in una macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="00890-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects tooa MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="00890-106">[MongoDB][MongoDB] è un diffuso database NoSQL open source a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="00890-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="00890-107">Dopo l'esecuzione e test di un'applicazione ASP.NET hello nel computer di sviluppo, verrà caricato hello tooApp di applicazione del servizio Web App usando Git.</span><span class="sxs-lookup"><span data-stu-id="00890-107">After running and testing hello ASP.NET application on your development computer, you will upload hello application tooApp Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="00890-108">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="00890-108">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="00890-109">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="00890-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="00890-110">Informazioni di background</span><span class="sxs-lookup"><span data-stu-id="00890-110">Background knowledge</span></span>
<span data-ttu-id="00890-111">È utile conoscere seguente hello per questa esercitazione, tuttavia non è necessaria:</span><span class="sxs-lookup"><span data-stu-id="00890-111">Knowledge of hello following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="00890-112">driver Hello c# per MongoDB.</span><span class="sxs-lookup"><span data-stu-id="00890-112">hello C# driver for MongoDB.</span></span> <span data-ttu-id="00890-113">Per ulteriori informazioni sullo sviluppo di applicazioni c# con MongoDB, vedere hello MongoDB [Center linguaggio CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="00890-113">For more information on developing C# applications against MongoDB, see hello MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="00890-114">framework di applicazioni web .NET ASP Hello.</span><span class="sxs-lookup"><span data-stu-id="00890-114">hello ASP .NET web application framework.</span></span> <span data-ttu-id="00890-115">È possibile acquisire tutte le informazioni in hello [sito Web ASP.net][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="00890-115">You can learn all about it at hello [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="00890-116">framework di applicazioni web ASP .NET MVC Hello.</span><span class="sxs-lookup"><span data-stu-id="00890-116">hello ASP .NET MVC web application framework.</span></span> <span data-ttu-id="00890-117">È possibile acquisire tutte le informazioni in hello [sito Web di ASP.NET MVC][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="00890-117">You can learn all about it at hello [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="00890-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="00890-118">Azure.</span></span> <span data-ttu-id="00890-119">Per informazioni preliminari, vedere [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="00890-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00890-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="00890-120">Prerequisites</span></span>
* <span data-ttu-id="00890-121">[Visual Studio Express 2013 per Web][VSEWeb] o [Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="00890-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="00890-122">Azure SDK per .NET</span><span class="sxs-lookup"><span data-stu-id="00890-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="00890-123">Una sottoscrizione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="00890-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="00890-124">Creare una macchina virtuale e installare MongoDB</span><span class="sxs-lookup"><span data-stu-id="00890-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="00890-125">In questa esercitazione si presuppone che l'utente abbia creato una macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="00890-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="00890-126">Dopo aver creato una macchina virtuale hello occorre tooinstall MongoDB sulla macchina virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="00890-126">After creating hello virtual machine you need tooinstall MongoDB on hello virtual machine:</span></span>

* <span data-ttu-id="00890-127">toocreate una macchina virtuale di Windows e installare MongoDB, vedere [MongoDB installare in una macchina virtuale in esecuzione Windows Server in Azure][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="00890-127">toocreate a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="00890-128">Dopo aver creato una macchina virtuale hello in Azure e installato MongoDB, essere certi tooremember hello nome DNS della macchina virtuale hello ("testlinuxvm.cloudapp.net", ad esempio) e la porta esterna hello MongoDB specificata nell'endpoint hello.</span><span class="sxs-lookup"><span data-stu-id="00890-128">After you have created hello virtual machine in Azure and installed MongoDB, be sure tooremember hello DNS name of hello virtual machine ("testlinuxvm.cloudapp.net", for example) and hello external port for MongoDB that you specified in hello endpoint.</span></span>  <span data-ttu-id="00890-129">È necessario che queste informazioni in un secondo momento nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="00890-129">You will need this information later in hello tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-hello-application"></a><span data-ttu-id="00890-130">Creare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="00890-130">Create hello application</span></span>
<span data-ttu-id="00890-131">In questa sezione si crea un'applicazione ASP.NET denominata "Elenco di attività personali" usando Visual Studio ed eseguire un'App Web del servizio App di tooAzure distribuzione iniziale.</span><span class="sxs-lookup"><span data-stu-id="00890-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment tooAzure App Service Web Apps.</span></span> <span data-ttu-id="00890-132">Un'applicazione hello viene eseguito localmente, ma verrà tooyour di macchina virtuale in Azure di connettersi e utilizzare istanza MongoDB hello creato non esiste.</span><span class="sxs-lookup"><span data-stu-id="00890-132">You will run hello application locally, but it will connect tooyour virtual machine on Azure and use hello MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="00890-133">In Visual Studio, fare clic su **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="00890-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Pagina iniziale Nuovo progetto][StartPageNewProject]
2. <span data-ttu-id="00890-135">In hello **nuovo progetto** finestra, nel riquadro sinistro hello, selezionare **Visual c#**, quindi selezionare **Web**.</span><span class="sxs-lookup"><span data-stu-id="00890-135">In hello **New Project** window, in hello left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="00890-136">Nel riquadro centrale hello selezionare **applicazione Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="00890-136">In hello middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="00890-137">Nella parte inferiore di hello, denominare il progetto "MyTaskListApp" e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="00890-137">At hello bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Finestra di dialogo Nuovo progetto][NewProjectMyTaskListApp]
3. <span data-ttu-id="00890-139">In hello **nuovo progetto ASP.NET** nella finestra di dialogo **MVC**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="00890-139">In hello **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![Selezione di un template MVC][VS2013SelectMVCTemplate]
4. <span data-ttu-id="00890-141">Se non è già stata effettuata in Microsoft Azure, sarà richiesta toosign in.</span><span class="sxs-lookup"><span data-stu-id="00890-141">If you aren't already signed into Microsoft Azure, you will be prompted toosign in.</span></span> <span data-ttu-id="00890-142">Seguire toosign prompt hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="00890-142">Follow hello prompts toosign into Azure.</span></span>
5. <span data-ttu-id="00890-143">Una volta che si sono connessi, è possibile avviare la configurazione dell'applicazione web servizio App.</span><span class="sxs-lookup"><span data-stu-id="00890-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="00890-144">Specificare hello **nome dell'App Web**, **piano di servizio App**, **gruppo di risorse**, e **area**, quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="00890-144">Specify hello **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="00890-145">Al termine della creazione del progetto hello, attendere hello web app toobe creato in Azure App Service come indicato nella hello **attività di servizio App di Azure** finestra.</span><span class="sxs-lookup"><span data-stu-id="00890-145">After hello project creation completes, wait for hello web app toobe created in Azure App Service as indicated in hello **Azure App Service Activity** window.</span></span> <span data-ttu-id="00890-146">Quindi, fare clic su **toothis MyTaskListApp pubblicare App Web adesso**.</span><span class="sxs-lookup"><span data-stu-id="00890-146">Then, click **Publish MyTaskListApp toothis Web App now**.</span></span>
7. <span data-ttu-id="00890-147">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="00890-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="00890-148">L'applicazione ASP.NET predefinito, una volta pubblicato tooAzure App del servizio Web App, si verrà avviato nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="00890-148">Once your default ASP.NET application is published tooAzure App Service Web Apps, it will be launched in hello browser.</span></span>

## <a name="install-hello-mongodb-c-driver"></a><span data-ttu-id="00890-149">Installare hello MongoDB c# driver</span><span class="sxs-lookup"><span data-stu-id="00890-149">Install hello MongoDB C# driver</span></span>
<span data-ttu-id="00890-150">MongoDB offre un supporto sul lato client per le applicazioni c# tramite un driver, che è necessario tooinstall nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="00890-150">MongoDB offers client-side support for C# applications through a driver, which you need tooinstall on your local development computer.</span></span> <span data-ttu-id="00890-151">Hello c# driver è disponibile tramite NuGet.</span><span class="sxs-lookup"><span data-stu-id="00890-151">hello C# driver is available through NuGet.</span></span>

<span data-ttu-id="00890-152">hello tooinstall MongoDB c# driver:</span><span class="sxs-lookup"><span data-stu-id="00890-152">tooinstall hello MongoDB C# driver:</span></span>

1. <span data-ttu-id="00890-153">In **Esplora**, hello rapida **MyTaskListApp** del progetto e selezionare **gestire NuGetPackages**.</span><span class="sxs-lookup"><span data-stu-id="00890-153">In **Solution Explorer**, right-click hello **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![Manage NuGet Packages][VS2013ManageNuGetPackages]
2. <span data-ttu-id="00890-155">In hello **Gestisci pacchetti NuGet** finestra, nel riquadro di sinistra hello, fare clic su **Online**.</span><span class="sxs-lookup"><span data-stu-id="00890-155">In hello **Manage NuGet Packages** window, in hello left pane, click **Online**.</span></span> <span data-ttu-id="00890-156">In hello **ricerca Online** su hello destra, digitare "mongodb.driver".</span><span class="sxs-lookup"><span data-stu-id="00890-156">In hello **Search Online** box on hello right, type "mongodb.driver".</span></span>  <span data-ttu-id="00890-157">Fare clic su **installare** driver hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="00890-157">Click **Install** tooinstall hello driver.</span></span>
   
    ![Ricerca del driver MongoDB C#][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="00890-159">Fare clic su **accetto** tooaccept hello 10gen, Inc. delle condizioni di licenza.</span><span class="sxs-lookup"><span data-stu-id="00890-159">Click **I Accept** tooaccept hello 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="00890-160">Fare clic su **Chiudi** dopo che è installato il driver hello.</span><span class="sxs-lookup"><span data-stu-id="00890-160">Click **Close** after hello driver has installed.</span></span>
    <span data-ttu-id="00890-161">![Driver MongoDB C# installato][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="00890-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="00890-162">Hello driver MongoDB c# viene ora installato.</span><span class="sxs-lookup"><span data-stu-id="00890-162">hello MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="00890-163">Riferimenti toohello **MongoDB.Bson**, **MongoDB.Driver**, e **MongoDB.Driver.Core** librerie sono stati aggiunti a un progetto toohello.</span><span class="sxs-lookup"><span data-stu-id="00890-163">References toohello **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added toohello project.</span></span>

![Riferimenti al driver MongoDB C#][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="00890-165">Aggiunta di un modello</span><span class="sxs-lookup"><span data-stu-id="00890-165">Add a model</span></span>
<span data-ttu-id="00890-166">In **Esplora soluzioni**, hello rapida *modelli* cartella e **Aggiungi** un nuovo **classe** e denominarlo *TaskModel.cs* .</span><span class="sxs-lookup"><span data-stu-id="00890-166">In **Solution Explorer**, right-click hello *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="00890-167">In *TaskModel.cs*, sostituire il codice esistente hello con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="00890-167">In *TaskModel.cs*, replace hello existing code with hello following code:</span></span>

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

## <a name="add-hello-data-access-layer"></a><span data-ttu-id="00890-168">Aggiungere a livello di accesso ai dati hello</span><span class="sxs-lookup"><span data-stu-id="00890-168">Add hello data access layer</span></span>
<span data-ttu-id="00890-169">In **Esplora**, hello rapida *MyTaskListApp* progetto e **Aggiungi** un **nuova cartella** denominato *DAL*.</span><span class="sxs-lookup"><span data-stu-id="00890-169">In **Solution Explorer**, right-click hello *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="00890-170">Pulsante destro del mouse hello *DAL* cartella e **Aggiungi** un nuovo **classe**.</span><span class="sxs-lookup"><span data-stu-id="00890-170">Right-click hello *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="00890-171">File di classe hello nome *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="00890-171">Name hello class file *Dal.cs*.</span></span>  <span data-ttu-id="00890-172">In *Dal.cs*, sostituire il codice esistente hello con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="00890-172">In *Dal.cs*, replace hello existing code with hello following code:</span></span>

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

            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

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

## <a name="add-a-controller"></a><span data-ttu-id="00890-173">Aggiunta di un controller</span><span class="sxs-lookup"><span data-stu-id="00890-173">Add a controller</span></span>
<span data-ttu-id="00890-174">Aprire hello *controllers\homecontroller.cs.* file in **Esplora** e sostituire il codice esistente hello con hello seguente:</span><span class="sxs-lookup"><span data-stu-id="00890-174">Open hello *Controllers\HomeController.cs* file in **Solution Explorer** and replace hello existing code with hello following:</span></span>

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

## <a name="set-up-hello-styles"></a><span data-ttu-id="00890-175">Impostare gli stili di hello</span><span class="sxs-lookup"><span data-stu-id="00890-175">Set up hello styles</span></span>
<span data-ttu-id="00890-176">titolo hello toochange nella parte superiore di hello della pagina di hello, aprire hello *Views\Shared\\layout. cshtml* file in **Esplora** e sostituire "Nome applicazione" nell'intestazione di hello barra di spostamento con "My Task Applicazione elenco"in modo che risulti simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="00890-176">toochange hello title at hello top of hello page, open hello *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in hello navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="00890-177">In ordine tooset menu elenco attività hello, aprire hello *\Views\Home\Index.cshtml* file e sostituire il codice esistente hello con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="00890-177">In order tooset up hello Task List menu, open hello *\Views\Home\Index.cshtml* file and replace hello existing code with hello following code:</span></span>

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


<span data-ttu-id="00890-178">tooadd hello possibilità toocreate una nuova attività, fare doppio clic su hello *Views\Home\\*  cartella e **Aggiungi** un **vista**.</span><span class="sxs-lookup"><span data-stu-id="00890-178">tooadd hello ability toocreate a new task, right-click hello *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="00890-179">Nome vista hello *crea*.</span><span class="sxs-lookup"><span data-stu-id="00890-179">Name hello view *Create*.</span></span> <span data-ttu-id="00890-180">Sostituire il codice hello con codice hello seguente:</span><span class="sxs-lookup"><span data-stu-id="00890-180">Replace hello code with hello following:</span></span>

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

<span data-ttu-id="00890-181">**Controllers\HomeController.cs** dovrebbe risultare simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="00890-181">**Solution Explorer** should look like this:</span></span>

![Esplora soluzioni][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a><span data-ttu-id="00890-183">Impostare la stringa di connessione di MongoDB hello</span><span class="sxs-lookup"><span data-stu-id="00890-183">Set hello MongoDB connection string</span></span>
<span data-ttu-id="00890-184">In **Esplora**aprire hello *DAL/Dal.cs* file.</span><span class="sxs-lookup"><span data-stu-id="00890-184">In **Solution Explorer**, open hello *DAL/Dal.cs* file.</span></span> <span data-ttu-id="00890-185">Trovare hello successiva riga di codice:</span><span class="sxs-lookup"><span data-stu-id="00890-185">Find hello following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="00890-186">Sostituire `<vm-dns-name>` con nome DNS hello hello macchina virtuale è stato creato in hello MongoDB [creare una macchina virtuale e installare MongoDB] [ Create a virtual machine and install MongoDB] passaggio di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="00890-186">Replace `<vm-dns-name>` with hello DNS name of hello virtual machine running MongoDB you created in hello [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="00890-187">nome DNS di hello toofind della macchina virtuale, passare il portale di Azure, selezionare toohello **macchine virtuali**e individuare **nome DNS**.</span><span class="sxs-lookup"><span data-stu-id="00890-187">toofind hello DNS name of your virtual machine, go toohello Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="00890-188">Se il nome DNS hello della macchina virtuale hello è "testlinuxvm.cloudapp.net" e MongoDB è in ascolto sulla porta predefinita hello 27017, hello connessione stringa riga di codice sarà simile:</span><span class="sxs-lookup"><span data-stu-id="00890-188">If hello DNS name of hello virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on hello default port 27017, hello connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="00890-189">Se l'endpoint della macchina virtuale hello specifica una porta esterna diversa per MongoDB, è possibile specificare la porta di hello nella stringa di connessione hello:</span><span class="sxs-lookup"><span data-stu-id="00890-189">If hello virtual machine endpoint specifies a different external port for MongoDB, you can specifiy hello port in hello connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="00890-190">Per altre informazioni sulle stringhe di connessione di MongoDB, vedere [Connections][MongoConnectionStrings] (Connessioni).</span><span class="sxs-lookup"><span data-stu-id="00890-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-hello-local-deployment"></a><span data-ttu-id="00890-191">Testare la distribuzione locale di hello</span><span class="sxs-lookup"><span data-stu-id="00890-191">Test hello local deployment</span></span>
<span data-ttu-id="00890-192">Selezionare l'applicazione nel computer di sviluppo, toorun **Avvia debug** da hello **Debug** menu o premere **F5**.</span><span class="sxs-lookup"><span data-stu-id="00890-192">toorun your application on your development computer, select **Start Debugging** from hello **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="00890-193">Avvio di IIS Express e un browser verrà visualizzata e viene avviata home page dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="00890-193">IIS Express starts and a browser opens and launches hello application's home page.</span></span>  <span data-ttu-id="00890-194">È possibile aggiungere una nuova attività, che verrà aggiunto il database di MongoDB toohello in esecuzione sulla macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="00890-194">You can add a new task, which will be added toohello MongoDB database running on your virtual machine in Azure.</span></span>

![Applicazione My Task List][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a><span data-ttu-id="00890-196">Pubblicare App Web del servizio App tooAzure</span><span class="sxs-lookup"><span data-stu-id="00890-196">Publish tooAzure App Service Web Apps</span></span>
<span data-ttu-id="00890-197">In questa sezione verrà pubblicato il tooAzure modifiche App del servizio Web App.</span><span class="sxs-lookup"><span data-stu-id="00890-197">In this section you will publish your changes tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="00890-198">In Esplora soluzioni, fare clic **MyTaskListApp** nuovamente e fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="00890-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="00890-199">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="00890-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="00890-200">Dovrebbe essere l'app web in esecuzione in Azure App Service e l'accesso ai database di MongoDB hello in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="00890-200">You should now see your web app running in Azure App Service and accessing hello MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="00890-201">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="00890-201">Summary</span></span>
<span data-ttu-id="00890-202">Ora è stata distribuita la tooAzure applicazione ASP.NET App del servizio Web App.</span><span class="sxs-lookup"><span data-stu-id="00890-202">You have now successfully deployed your ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="00890-203">tooview hello web app:</span><span class="sxs-lookup"><span data-stu-id="00890-203">tooview hello web app:</span></span>

1. <span data-ttu-id="00890-204">Accedere al portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="00890-204">Log into hello Azure Portal.</span></span>
2. <span data-ttu-id="00890-205">Fare clic su **App Web**.</span><span class="sxs-lookup"><span data-stu-id="00890-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="00890-206">Selezionare l'applicazione web in hello **App Web** elenco.</span><span class="sxs-lookup"><span data-stu-id="00890-206">Select your web app in hello **Web Apps** list.</span></span>

<span data-ttu-id="00890-207">Per altre informazioni sullo sviluppo di applicazioni C# con MongoDB, vedere [CSharp Language Center][MongoC#LangCenter] (Centro per il linguaggio CSharp).</span><span class="sxs-lookup"><span data-stu-id="00890-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

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
[Create and run hello My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy hello ASP.NET application toohello web site using Git]: #deployapp
