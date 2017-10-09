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
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a>Creare un'app web in Azure che si connette tooMongoDB in esecuzione in una macchina virtuale
Usa Git, è possibile distribuire un tooAzure applicazione ASP.NET App del servizio Web App. In questa esercitazione si creerà un semplice front-end ASP.NET MVC applicazione elenco attività che si connette il database di MongoDB tooa in esecuzione in una macchina virtuale in Azure.  [MongoDB][MongoDB] è un diffuso database NoSQL open source a prestazioni elevate. Dopo l'esecuzione e test di un'applicazione ASP.NET hello nel computer di sviluppo, verrà caricato hello tooApp di applicazione del servizio Web App usando Git.

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="background-knowledge"></a>Informazioni di background
È utile conoscere seguente hello per questa esercitazione, tuttavia non è necessaria:

* driver Hello c# per MongoDB. Per ulteriori informazioni sullo sviluppo di applicazioni c# con MongoDB, vedere hello MongoDB [Center linguaggio CSharp][MongoC#LangCenter]. 
* framework di applicazioni web .NET ASP Hello. È possibile acquisire tutte le informazioni in hello [sito Web ASP.net][ASP.NET].
* framework di applicazioni web ASP .NET MVC Hello. È possibile acquisire tutte le informazioni in hello [sito Web di ASP.NET MVC][MVCWebSite].
* Azure. Per informazioni preliminari, vedere [Azure][WindowsAzure].

## <a name="prerequisites"></a>Prerequisiti
* [Visual Studio Express 2013 per Web][VSEWeb] o [Visual Studio 2013][VSUlt]
* [Azure SDK per .NET](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* Una sottoscrizione di Microsoft Azure

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a>Creare una macchina virtuale e installare MongoDB
In questa esercitazione si presuppone che l'utente abbia creato una macchina virtuale in Azure. Dopo aver creato una macchina virtuale hello occorre tooinstall MongoDB sulla macchina virtuale hello:

* toocreate una macchina virtuale di Windows e installare MongoDB, vedere [MongoDB installare in una macchina virtuale in esecuzione Windows Server in Azure][InstallMongoOnWindowsVM].

Dopo aver creato una macchina virtuale hello in Azure e installato MongoDB, essere certi tooremember hello nome DNS della macchina virtuale hello ("testlinuxvm.cloudapp.net", ad esempio) e la porta esterna hello MongoDB specificata nell'endpoint hello.  È necessario che queste informazioni in un secondo momento nell'esercitazione di hello.

<a id="createapp"></a>

## <a name="create-hello-application"></a>Creare un'applicazione hello
In questa sezione si crea un'applicazione ASP.NET denominata "Elenco di attività personali" usando Visual Studio ed eseguire un'App Web del servizio App di tooAzure distribuzione iniziale. Un'applicazione hello viene eseguito localmente, ma verrà tooyour di macchina virtuale in Azure di connettersi e utilizzare istanza MongoDB hello creato non esiste.

1. In Visual Studio, fare clic su **Nuovo progetto**.
   
    ![Pagina iniziale Nuovo progetto][StartPageNewProject]
2. In hello **nuovo progetto** finestra, nel riquadro sinistro hello, selezionare **Visual c#**, quindi selezionare **Web**. Nel riquadro centrale hello selezionare **applicazione Web ASP.NET**. Nella parte inferiore di hello, denominare il progetto "MyTaskListApp" e quindi fare clic su **OK**.
   
    ![Finestra di dialogo Nuovo progetto][NewProjectMyTaskListApp]
3. In hello **nuovo progetto ASP.NET** nella finestra di dialogo **MVC**, quindi fare clic su **OK**.
   
    ![Selezione di un template MVC][VS2013SelectMVCTemplate]
4. Se non è già stata effettuata in Microsoft Azure, sarà richiesta toosign in. Seguire toosign prompt hello in Azure.
5. Una volta che si sono connessi, è possibile avviare la configurazione dell'applicazione web servizio App. Specificare hello **nome dell'App Web**, **piano di servizio App**, **gruppo di risorse**, e **area**, quindi fare clic su **crea**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. Al termine della creazione del progetto hello, attendere hello web app toobe creato in Azure App Service come indicato nella hello **attività di servizio App di Azure** finestra. Quindi, fare clic su **toothis MyTaskListApp pubblicare App Web adesso**.
7. Fare clic su **Pubblica**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    L'applicazione ASP.NET predefinito, una volta pubblicato tooAzure App del servizio Web App, si verrà avviato nel browser hello.

## <a name="install-hello-mongodb-c-driver"></a>Installare hello MongoDB c# driver
MongoDB offre un supporto sul lato client per le applicazioni c# tramite un driver, che è necessario tooinstall nel computer di sviluppo locale. Hello c# driver è disponibile tramite NuGet.

hello tooinstall MongoDB c# driver:

1. In **Esplora**, hello rapida **MyTaskListApp** del progetto e selezionare **gestire NuGetPackages**.
   
    ![Manage NuGet Packages][VS2013ManageNuGetPackages]
2. In hello **Gestisci pacchetti NuGet** finestra, nel riquadro di sinistra hello, fare clic su **Online**. In hello **ricerca Online** su hello destra, digitare "mongodb.driver".  Fare clic su **installare** driver hello tooinstall.
   
    ![Ricerca del driver MongoDB C#][SearchforMongoDBCSharpDriver]
3. Fare clic su **accetto** tooaccept hello 10gen, Inc. delle condizioni di licenza.
4. Fare clic su **Chiudi** dopo che è installato il driver hello.
    ![Driver MongoDB C# installato][MongoDBCsharpDriverInstalled]

Hello driver MongoDB c# viene ora installato.  Riferimenti toohello **MongoDB.Bson**, **MongoDB.Driver**, e **MongoDB.Driver.Core** librerie sono stati aggiunti a un progetto toohello.

![Riferimenti al driver MongoDB C#][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a>Aggiunta di un modello
In **Esplora soluzioni**, hello rapida *modelli* cartella e **Aggiungi** un nuovo **classe** e denominarlo *TaskModel.cs* .  In *TaskModel.cs*, sostituire il codice esistente hello con hello seguente codice:

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

## <a name="add-hello-data-access-layer"></a>Aggiungere a livello di accesso ai dati hello
In **Esplora**, hello rapida *MyTaskListApp* progetto e **Aggiungi** un **nuova cartella** denominato *DAL*.  Pulsante destro del mouse hello *DAL* cartella e **Aggiungi** un nuovo **classe**. File di classe hello nome *Dal.cs*.  In *Dal.cs*, sostituire il codice esistente hello con hello seguente codice:

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

## <a name="add-a-controller"></a>Aggiunta di un controller
Aprire hello *controllers\homecontroller.cs.* file in **Esplora** e sostituire il codice esistente hello con hello seguente:

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

## <a name="set-up-hello-styles"></a>Impostare gli stili di hello
titolo hello toochange nella parte superiore di hello della pagina di hello, aprire hello *Views\Shared\\layout. cshtml* file in **Esplora** e sostituire "Nome applicazione" nell'intestazione di hello barra di spostamento con "My Task Applicazione elenco"in modo che risulti simile al seguente:

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

In ordine tooset menu elenco attività hello, aprire hello *\Views\Home\Index.cshtml* file e sostituire il codice esistente hello con hello seguente codice:

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


tooadd hello possibilità toocreate una nuova attività, fare doppio clic su hello *Views\Home\\*  cartella e **Aggiungi** un **vista**.  Nome vista hello *crea*. Sostituire il codice hello con codice hello seguente:

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

**Controllers\HomeController.cs** dovrebbe risultare simile al seguente:

![Esplora soluzioni][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a>Impostare la stringa di connessione di MongoDB hello
In **Esplora**aprire hello *DAL/Dal.cs* file. Trovare hello successiva riga di codice:

    private string connectionString = "mongodb://<vm-dns-name>";

Sostituire `<vm-dns-name>` con nome DNS hello hello macchina virtuale è stato creato in hello MongoDB [creare una macchina virtuale e installare MongoDB] [ Create a virtual machine and install MongoDB] passaggio di questa esercitazione.  nome DNS di hello toofind della macchina virtuale, passare il portale di Azure, selezionare toohello **macchine virtuali**e individuare **nome DNS**.

Se il nome DNS hello della macchina virtuale hello è "testlinuxvm.cloudapp.net" e MongoDB è in ascolto sulla porta predefinita hello 27017, hello connessione stringa riga di codice sarà simile:

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

Se l'endpoint della macchina virtuale hello specifica una porta esterna diversa per MongoDB, è possibile specificare la porta di hello nella stringa di connessione hello:

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

Per altre informazioni sulle stringhe di connessione di MongoDB, vedere [Connections][MongoConnectionStrings] (Connessioni).

## <a name="test-hello-local-deployment"></a>Testare la distribuzione locale di hello
Selezionare l'applicazione nel computer di sviluppo, toorun **Avvia debug** da hello **Debug** menu o premere **F5**. Avvio di IIS Express e un browser verrà visualizzata e viene avviata home page dell'applicazione hello.  È possibile aggiungere una nuova attività, che verrà aggiunto il database di MongoDB toohello in esecuzione sulla macchina virtuale in Azure.

![Applicazione My Task List][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a>Pubblicare App Web del servizio App tooAzure
In questa sezione verrà pubblicato il tooAzure modifiche App del servizio Web App.

1. In Esplora soluzioni, fare clic **MyTaskListApp** nuovamente e fare clic su **Pubblica**.
2. Fare clic su **Pubblica**.
   
    Dovrebbe essere l'app web in esecuzione in Azure App Service e l'accesso ai database di MongoDB hello in macchine virtuali di Azure.

## <a name="summary"></a>Riepilogo
Ora è stata distribuita la tooAzure applicazione ASP.NET App del servizio Web App. tooview hello web app:

1. Accedere al portale di Azure hello.
2. Fare clic su **App Web**. 
3. Selezionare l'applicazione web in hello **App Web** elenco.

Per altre informazioni sullo sviluppo di applicazioni C# con MongoDB, vedere [CSharp Language Center][MongoC#LangCenter] (Centro per il linguaggio CSharp). 

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
