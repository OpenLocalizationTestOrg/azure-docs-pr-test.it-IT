---
title: Creare un'API REST in Azure con ASP.NET e database SQL | Documentazione Microsoft
description: Un'esercitazione che illustra come distribuire un'app che usa l'API Web ASP.NET in un'app Web di Azure tramite Visual Studio.
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 64c18f2cfabbb7af6ffd89b4c2a9095fca1cf799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="0d7e7-103">Creare un servizio REST con l'API Web ASP.NET e il database SQL in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="0d7e7-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="0d7e7-104">Questa esercitazione illustra come distribuire un'app Web ASP.NET in un [Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) usando la procedura guidata Pubblica sul Web in Visual Studio 2013 o Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-104">This tutorial shows how to deploy an ASP.NET web app to an [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using the Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="0d7e7-105">È possibile aprire gratuitamente un account Azure e, se non si dispone già di Visual Studio 2013, con l'SDK verrà installato automaticamente Visual Studio Express 2013 per il Web.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, the SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="0d7e7-106">Sarà quindi possibile iniziare a sviluppare per Azure del tutto gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="0d7e7-107">In questa esercitazione si presuppone che l'utente non abbia mai utilizzato Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="0d7e7-108">Al termine dell'esercitazione, si disporrà di un'app Web semplice in esecuzione nel cloud.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-108">On completing this tutorial, you'll have a simple web app up and running in the cloud.</span></span>

<span data-ttu-id="0d7e7-109">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="0d7e7-109">You'll learn:</span></span>

* <span data-ttu-id="0d7e7-110">Abilitare il sistema per lo sviluppo in Azure installando Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-110">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="0d7e7-111">Creare un progetto ASP.NET MVC 5 di Visual Studio e pubblicarlo in un'app di Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-111">How to create a Visual Studio ASP.NET MVC 5 project and publish it to an Azure app.</span></span>
* <span data-ttu-id="0d7e7-112">Creare l'API Web ASP.NET per consentire chiamate all'API RESTful.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-112">How to use the ASP.NET Web API to enable Restful API calls.</span></span>
* <span data-ttu-id="0d7e7-113">Utilizzare un database SQL per l'archiviazione di dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-113">How to use a SQL database to store data in Azure.</span></span>
* <span data-ttu-id="0d7e7-114">Pubblicare aggiornamenti dell'applicazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-114">How to publish application updates to Azure.</span></span>

<span data-ttu-id="0d7e7-115">Verrà creata una semplice applicazione Web di elenco contatti basata su ASP.NET MVC 5 che utilizza ADO.NET Entity Framework per l'accesso al database.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses the ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="0d7e7-116">Nella figura seguente è illustrata l'applicazione completata:</span><span class="sxs-lookup"><span data-stu-id="0d7e7-116">The following illustration shows the completed application:</span></span>

![schermata del sito web][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-the-project"></a><span data-ttu-id="0d7e7-118">Creare il progetto</span><span class="sxs-lookup"><span data-stu-id="0d7e7-118">Create the project</span></span>
1. <span data-ttu-id="0d7e7-119">Avviare Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="0d7e7-120">Scegliere **Nuovo progetto** dal menu **File**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-120">From the **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="0d7e7-121">Nella finestra di dialogo **Nuovo progetto** espandere **Visual C#** e selezionare **Web**, quindi selezionare **Applicazione Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-121">In the **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="0d7e7-122">Assegnare all'applicazione il nome **ContactManager** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-122">Name the application **ContactManager** and click **OK**.</span></span>
   
    ![Finestra di dialogo Nuovo progetto](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="0d7e7-124">Nella finestra di dialogo **Nuovo progetto ASP.NET** selezionare il modello **MVC**, selezionare **API Web**, quindi fare clic su **Modifica autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-124">In the **New ASP.NET Project** dialog box, select the **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="0d7e7-125">Nella finestra di dialogo **Modifica autenticazione** fare clic su **Nessuna autenticazione**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-125">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![No Authentication](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="0d7e7-127">L'applicazione di esempio che si sta creando non includerà funzionalità che richiedono l'accesso agli utenti.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-127">The sample application you're creating won't have features that require users to log in.</span></span> <span data-ttu-id="0d7e7-128">Per informazioni su come implementare le funzionalità di autenticazione e autorizzazione, vedere la sezione [Passaggi successivi](#nextsteps) alla fine di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-128">For information about how to implement authentication and authorization features, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
6. <span data-ttu-id="0d7e7-129">Nella finestra di dialogo **Nuovo progetto ASP.NET** verificare che **Ospita nel cloud** sia selezionato e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-129">In the **New ASP.NET Project** dialog box, make sure the **Host in the Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="0d7e7-130">Se non è già stato effettuato l'accesso ad Azure, verrà richiesto di accedervi.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-130">If you have not previously signed in to Azure, you will be prompted to sign in.</span></span>

1. <span data-ttu-id="0d7e7-131">La configurazione guidata suggerirà un nome univoco basato su *ContactManager* , come mostrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-131">The configuration wizard will suggest a unique name based on *ContactManager* (see the image below).</span></span> <span data-ttu-id="0d7e7-132">Selezionare un'area nelle vicinanze.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-132">Select a region near you.</span></span> <span data-ttu-id="0d7e7-133">È possibile usare [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") per trovare il data center a latenza più bassa.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") to find the lowest latency data center.</span></span> 
2. <span data-ttu-id="0d7e7-134">Se non è stato creato un server di database, selezionare **Crea nuovo server**e immettere un nome utente e una password per il database.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Configurare il sito Web di Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="0d7e7-136">Se si dispone di un server di database, usarlo per creare un nuovo database.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-136">If you have a database server, use that to create a new database.</span></span> <span data-ttu-id="0d7e7-137">I server di database sono una risorsa preziosa e in genere è utile creare più database nello stesso server per attività di test e sviluppo anziché creare un server di database per ogni database.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-137">Database servers are a precious resource, and you generally want to create multiple databases on the same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="0d7e7-138">Assicurarsi che il sito Web e il database si trovino nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-138">Make sure your web site and database are in the same region.</span></span>

![Configurare il sito Web di Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-the-page-header-and-footer"></a><span data-ttu-id="0d7e7-140">Impostare intestazione e piè di pagina</span><span class="sxs-lookup"><span data-stu-id="0d7e7-140">Set the page header and footer</span></span>
1. <span data-ttu-id="0d7e7-141">In **Esplora soluzioni** espandere la cartella *Views\Shared* e aprire il file *_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-141">In **Solution Explorer**, expand the *Views\Shared* folder and open the *_Layout.cshtml* file.</span></span>
   
    ![File _Layout.cshtml in Esplora soluzioni][newapp004]
2. <span data-ttu-id="0d7e7-143">Sostituire il contenuto del file *Views\Shared_Layout.cshtml* con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="0d7e7-143">Replace the contents of the *Views\Shared_Layout.cshtml* file with the following code:</span></span>

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

<span data-ttu-id="0d7e7-144">Il markup precedente cambia il nome dell'app da "My ASP.NET App" a "Contact Manager" e rimuove i collegamenti a **Home**, **About** e **Contact**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-144">The markup above changes the app name from "My ASP.NET App" to "Contact Manager", and it removes the links to **Home**, **About** and **Contact**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="0d7e7-145">Eseguire l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="0d7e7-145">Run the application locally</span></span>
1. <span data-ttu-id="0d7e7-146">Premere CTRL+F5 per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-146">Press CTRL+F5 to run the application.</span></span>
   <span data-ttu-id="0d7e7-147">La home page dell'applicazione verrà visualizzata nel browser predefinito.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-147">The application home page appears in the default browser.</span></span>
    <span data-ttu-id="0d7e7-148">![Home page Elenco azioni](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="0d7e7-148">![To Do List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="0d7e7-149">Non è necessario eseguire per il momento altre operazioni per creare l'applicazione che verrà distribuita in Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-149">This is all you need to do for now to create the application that you'll deploy to Azure.</span></span> <span data-ttu-id="0d7e7-150">La funzionalità di database verrà aggiunta in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-150">Later you'll add database functionality.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="0d7e7-151">Distribuzione dell'applicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="0d7e7-151">Deploy the application to Azure</span></span>
1. <span data-ttu-id="0d7e7-152">In Visual Studio fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere **Pubblica** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-152">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
   
    ![Opzione Pubblica nel menu di scelta rapida del progetto][PublishVSSolution]
   
    <span data-ttu-id="0d7e7-154">Viene visualizzata la procedura guidata **Pubblica sito Web** .</span><span class="sxs-lookup"><span data-stu-id="0d7e7-154">The **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="0d7e7-155">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-155">Click **Publish**.</span></span>

![Scheda Settings](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="0d7e7-157">In Visual Studio verrà avviato il processo di copia dei file nel server Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-157">Visual Studio begins the process of copying the files to the Azure server.</span></span> <span data-ttu-id="0d7e7-158">Nella finestra **Output** vengono indicate le azioni di distribuzione effettuate e viene segnalato il corretto completamento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-158">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span>

1. <span data-ttu-id="0d7e7-159">Nel browser predefinito verrà automaticamente aperto l'URL del sito distribuito.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-159">The default browser automatically opens to the URL of the deployed site.</span></span>
   
   <span data-ttu-id="0d7e7-160">L'applicazione creata verrà ora eseguita nel cloud.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-160">The application you created is now running in the cloud.</span></span>
   
   ![Pagina iniziale Elenco azioni in esecuzione in Azure][rxz2]

## <a name="add-a-database-to-the-application"></a><span data-ttu-id="0d7e7-162">Aggiungere un database all'applicazione</span><span class="sxs-lookup"><span data-stu-id="0d7e7-162">Add a database to the application</span></span>
<span data-ttu-id="0d7e7-163">A questo punto si passa all'aggiornamento dell'applicazione MVC, in modo da aggiungere la possibilità di visualizzare e aggiornare i contatti e di archiviare i dati in un database.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-163">Next, you'll update the MVC application to add the ability to display and update contacts and store the data in a database.</span></span> <span data-ttu-id="0d7e7-164">L'applicazione utilizzerà Entity Framework per creare il database e per leggere e aggiornare i dati nel database.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-164">The application will use the Entity Framework to create the database and to read and update data in the database.</span></span>

### <a name="add-data-model-classes-for-the-contacts"></a><span data-ttu-id="0d7e7-165">Aggiungere classi del modello di dati per i contatti</span><span class="sxs-lookup"><span data-stu-id="0d7e7-165">Add data model classes for the contacts</span></span>
<span data-ttu-id="0d7e7-166">Creare innanzitutto un semplice modello di dati nel codice.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="0d7e7-167">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella Modelli, quindi scegliere **Aggiungi** e infine **Classe**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-167">In **Solution Explorer**, right-click the Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Aggiungi classe nel menu di scelta rapida della cartella Modelli][adddb001]
2. <span data-ttu-id="0d7e7-169">Nella finestra di dialogo **Aggiungi nuovo elemento** assegnare al nuovo file di classe il nome *Contact.cs*, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-169">In the **Add New Item** dialog box, name the new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Finestra di dialogo Aggiungi nuovo elemento][adddb002]
3. <span data-ttu-id="0d7e7-171">Sostituire il contenuto del file Contacts.cs con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-171">Replace the contents of the Contacts.cs file with the following code.</span></span>
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

<span data-ttu-id="0d7e7-172">La classe **Contact** definisce i dati che verranno archiviati per ogni contatto, oltre a una chiave primaria, ContactID, necessaria per il database.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-172">The **Contact** class defines the data that you will store for each contact, plus a primary key, ContactID, that is needed by the database.</span></span> <span data-ttu-id="0d7e7-173">Per ulteriori informazioni, vedere la sezione [Passaggi successivi](#nextsteps) alla fine di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-173">You can get more information about data models in the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-to-work-with-the-contacts"></a><span data-ttu-id="0d7e7-174">Creare pagine Web che consentono agli utenti dell'app di utilizzare i contatti</span><span class="sxs-lookup"><span data-stu-id="0d7e7-174">Create web pages that enable app users to work with the contacts</span></span>
<span data-ttu-id="0d7e7-175">La funzionalità di scaffolding di ASP.NET MVC consente di generare automaticamente codice per l'esecuzione di azioni di creazione, lettura, aggiornamento ed eliminazione (CRUD, Create, Read, Update, Delete).</span><span class="sxs-lookup"><span data-stu-id="0d7e7-175">The ASP.NET MVC the scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-the-data"></a><span data-ttu-id="0d7e7-176">Aggiungere un controller e una visualizzazione per i dati</span><span class="sxs-lookup"><span data-stu-id="0d7e7-176">Add a Controller and a view for the data</span></span>
1. <span data-ttu-id="0d7e7-177">In **Esplora soluzioni**espandere la cartella Controllers.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-177">In **Solution Explorer**, expand the Controllers folder.</span></span>
2. <span data-ttu-id="0d7e7-178">Creare il progetto **(CTRL+MAIUSC+B)**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-178">Build the project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="0d7e7-179">Per utilizzare il meccanismo scaffolding, è innanzitutto necessario creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-179">(You must build the project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="0d7e7-180">Fare clic con il pulsante destro del mouse sulla cartella Controllers, quindi scegliere **Aggiungi** e infine **Controller**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-180">Right-click the Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Opzione Aggiungi controller nel menu di scelta rapida della cartella Controllers][addcode001]
4. <span data-ttu-id="0d7e7-182">Nella finestra di dialogo **Add Scaffold** selezionare **MVC Controller with views, using Entity Framework**, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-182">In the **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Aggiungi controller](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="0d7e7-184">Impostare il nome del controller su **HomeController**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-184">Set the controller name to **HomeController**.</span></span> <span data-ttu-id="0d7e7-185">Selezionare **Contact** come classe del modello.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="0d7e7-186">Fare clic sul pulsante **Nuovo contesto dati** e accettare il contesto predefinito "ContactManager.Models.ContactManagerContext" per **Nuovo tipo di contesto dati**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-186">Click the **New data context** button and accept the default "ContactManager.Models.ContactManagerContext" for the **New data context type**.</span></span> <span data-ttu-id="0d7e7-187">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-187">Click **Add**.</span></span>

    <span data-ttu-id="0d7e7-188">Nella finestra di dialogo chiederà: "un file con nome HomeController esiste già.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-188">A dialog box will prompt you: "A file with the name HomeController already exits.</span></span> <span data-ttu-id="0d7e7-189">Sostituirlo?"</span><span class="sxs-lookup"><span data-stu-id="0d7e7-189">Do you want to replace it?".</span></span> <span data-ttu-id="0d7e7-190">Fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-190">Click **Yes**.</span></span> <span data-ttu-id="0d7e7-191">Il file HomeController creato con il nuovo progetto verrà sovrascritto.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-191">We are overwriting the Home Controller that was created with the new project.</span></span> <span data-ttu-id="0d7e7-192">Per l'elenco dei contatti, verrà utilizzato il nuovo file HomeController.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-192">We will use the new Home Controller for our contact list.</span></span>

    <span data-ttu-id="0d7e7-193">In Visual Studio verranno creati metodi e visualizzazioni di un controller per operazioni CRUD di database per oggetti **Contact** .</span><span class="sxs-lookup"><span data-stu-id="0d7e7-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-the-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="0d7e7-194">Abilitazione delle migrazioni, creazione del database, aggiunta di dati di esempio e di un inizializzatore di dati</span><span class="sxs-lookup"><span data-stu-id="0d7e7-194">Enable Migrations, create the database, add sample data and a data initializer</span></span>
<span data-ttu-id="0d7e7-195">L'attività successiva consiste nell'abilitare la caratteristica [Migrazioni Code First](http://curah.microsoft.com/55220) , in modo da creare il database basato sul modello di dati creato.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-195">The next task is to enable the [Code First Migrations](http://curah.microsoft.com/55220) feature in order to create the database based on the data model you created.</span></span>

1. <span data-ttu-id="0d7e7-196">Scegliere **Gestione pacchetti libreria** dal menu **Strumenti**, quindi fare clic su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-196">In the **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Console di Gestione pacchetti nel menu Strumenti][addcode008]
2. <span data-ttu-id="0d7e7-198">Nella finestra **Console di Gestione pacchetti** immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d7e7-198">In the **Package Manager Console** window, enter the following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="0d7e7-199">Il comando **enable-migrations** consente di creare una cartella *Migrations* e di inserire in tale tabella il file *Configuration.cs*, che può essere modificato per configurare le migrazioni.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-199">The **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit to configure Migrations.</span></span> 
3. <span data-ttu-id="0d7e7-200">Nella finestra **Console di Gestione pacchetti** immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d7e7-200">In the **Package Manager Console** window, enter the following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="0d7e7-201">Il comando **add-migration Initial** consente di generare una classe denominata **&lt;timbro_data&gt;Initial** che crea il database.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-201">The **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates the database.</span></span> <span data-ttu-id="0d7e7-202">Il primo parametro *(Initial)* è arbitrario e viene utilizzato per creare il nome del file.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-202">The first parameter ( *Initial* ) is arbitrary and used to create the name of the file.</span></span> <span data-ttu-id="0d7e7-203">È possibile visualizzare i nuovi file di classe in **Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-203">You can see the new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="0d7e7-204">Nella classe **Initial** il metodo **Up** consente di creare la cartella Contacts e il metodo **Down**, usato quando si vuole tornare allo stato precedente, consente di rimuoverla.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-204">In the **Initial** class, the **Up** method creates the Contacts table, and the **Down** method (used when you want to return to the previous state) drops it.</span></span>
4. <span data-ttu-id="0d7e7-205">Aprire il file *Migrations\Configuration.cs*.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-205">Open the *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="0d7e7-206">Aggiungere gli spazi dei nomi seguenti.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-206">Add the following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="0d7e7-207">Sostituire il metodo *Seed* con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="0d7e7-207">Replace the *Seed* method with the following code:</span></span>
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    <span data-ttu-id="0d7e7-208">Il codice precedente consente di inizializzare il database con le informazioni sui contatti.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-208">This code above will initialize the database with the contact information.</span></span> <span data-ttu-id="0d7e7-209">Per ulteriori informazioni sul seeding del database, vedere la pagina relativa al [debug di database di Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d7e7-209">For more information on seeding the database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="0d7e7-210">In **Console di Gestione pacchetti** immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0d7e7-210">In the **Package Manager Console** enter the command:</span></span>
   
        update-database
   
    ![Comandi di Console di Gestione pacchetti][addcode009]
   
    <span data-ttu-id="0d7e7-212">Il comando **update-database** consente di eseguire la prima migrazione al fine di creare il database.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-212">The **update-database** runs the first migration which creates the database.</span></span> <span data-ttu-id="0d7e7-213">Per impostazione predefinita, il database viene creato come database LocalDB SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-213">By default, the database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="0d7e7-214">Premere CTRL+F5 per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-214">Press CTRL+F5 to run the application.</span></span> 

<span data-ttu-id="0d7e7-215">Nell'applicazione vengono mostrati i dati di seeding e sono disponibili collegamenti per la modifica, i dettagli e l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-215">The application shows the seed data and provides edit, details and delete links.</span></span>

![Visualizzazione MVC dei dati][rxz3]

## <a name="edit-the-view"></a><span data-ttu-id="0d7e7-217">Modificare la visualizzazione</span><span class="sxs-lookup"><span data-stu-id="0d7e7-217">Edit the View</span></span>
1. <span data-ttu-id="0d7e7-218">Aprire il file *Views\Home\Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-218">Open the *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="0d7e7-219">Nel passaggio successivo, il markup generato verrà sostituito con codice che usa [jQuery](http://jquery.com/) e [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="0d7e7-219">In the next step, we will replace the generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="0d7e7-220">Questo nuovo codice recupera l'elenco dei contatti con l'API Web e JSON e quindi associa i dati dei contatti all'interfaccia utente usando knockout.js.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-220">This new code retrieves the list of contacts from using web API and JSON and then binds the contact data to the UI using knockout.js.</span></span> <span data-ttu-id="0d7e7-221">Per altre informazioni, vedere la sezione [Passaggi successivi](#nextsteps) alla fine di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-221">For more information, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
2. <span data-ttu-id="0d7e7-222">Sostituire il contenuto del file con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-222">Replace the contents of the file with the following code.</span></span>
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. <span data-ttu-id="0d7e7-223">Fare clic con il pulsante destro del mouse sulla cartella Content, scegliere **Aggiungi**, quindi fare clic su **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-223">Right-click the Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Opzione Aggiungi foglio di stile nel menu di scelta rapida della cartella Content][addcode005]
4. <span data-ttu-id="0d7e7-225">Nella finestra di dialogo **Aggiungi nuovo elemento** immettere **Stile** nella casella di ricerca in alto a destra e quindi selezionare **Foglio di stile**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-225">In the **Add New Item** dialog box, enter **Style** in the upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="0d7e7-226">![Finestra di dialogo Aggiungi nuovo elemento][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="0d7e7-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="0d7e7-227">Assegnare al file il nome *Contacts.css* e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-227">Name the file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="0d7e7-228">Sostituire il contenuto del file con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-228">Replace the contents of the file with the following code.</span></span>
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    <span data-ttu-id="0d7e7-229">Questo foglio di stile verrà utilizzato per il layout, i colori e gli stili nell'app Contact Manager.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-229">We will use this style sheet for the layout, colors and styles used in the contact manager app.</span></span>
6. <span data-ttu-id="0d7e7-230">Aprire il file *App_Start\BundleConfig.cs*.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-230">Open the *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="0d7e7-231">Aggiungere il codice seguente per registrare il plug-in [Knockout](http://knockoutjs.com/index.html "KO") .</span><span class="sxs-lookup"><span data-stu-id="0d7e7-231">Add the following code to register the [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="0d7e7-232">In questo esempio viene utilizzato il plug-in Knockout per semplificare il codice JavaScript dinamico che gestisce i modelli delle schermate.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-232">This sample using knockout to simplify dynamic JavaScript code that handles the screen templates.</span></span>
8. <span data-ttu-id="0d7e7-233">Modificare la voce contents/css per registrare il foglio di stile *contacts.css* .</span><span class="sxs-lookup"><span data-stu-id="0d7e7-233">Modify the contents/css entry to register the *contacts.css* style sheet.</span></span> <span data-ttu-id="0d7e7-234">Sostituire la riga seguente:</span><span class="sxs-lookup"><span data-stu-id="0d7e7-234">Change the following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="0d7e7-235">Con:</span><span class="sxs-lookup"><span data-stu-id="0d7e7-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="0d7e7-236">Nella Console di Gestione pacchetti eseguire il comando seguente per installare Knockout.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-236">In the Package Manager Console, run the following command to install Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-the-web-api-restful-interface"></a><span data-ttu-id="0d7e7-237">Aggiungere un controller per l'interfaccia dell'API Web RESTful</span><span class="sxs-lookup"><span data-stu-id="0d7e7-237">Add a controller for the Web API Restful interface</span></span>
1. <span data-ttu-id="0d7e7-238">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella Controllers, quindi scegliere **Aggiungi** e infine **Controller**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="0d7e7-239">Nella finestra di dialogo **Add Scaffold** immettere **Web API 2 Controller with actions, using Entity Framework**, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-239">In the **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![Aggiunta di un controller per l'API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="0d7e7-241">Nella finestra di dialogo **Aggiungi controller** immettere "ContactsController" come nome del controller.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-241">In the **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="0d7e7-242">In **Classe modello**selezionare "Contact (ContactManager.Models)".</span><span class="sxs-lookup"><span data-stu-id="0d7e7-242">Select "Contact (ContactManager.Models)" for the **Model class**.</span></span>  <span data-ttu-id="0d7e7-243">Mantenere il valore predefinito per **Classe contesto dei dati**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-243">Keep the default value for the **Data context class**.</span></span> 
4. <span data-ttu-id="0d7e7-244">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-244">Click **Add**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="0d7e7-245">Eseguire l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="0d7e7-245">Run the application locally</span></span>
1. <span data-ttu-id="0d7e7-246">Premere CTRL+F5 per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-246">Press CTRL+F5 to run the application.</span></span>
   
    ![Pagina di indice][intro001]
2. <span data-ttu-id="0d7e7-248">Immettere un contatto e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="0d7e7-249">L'app torna alla pagina iniziale e visualizza il contatto immesso</span><span class="sxs-lookup"><span data-stu-id="0d7e7-249">The app returns to the home page and displays the contact you entered.</span></span>
   
    ![Pagina di indice con elementi dell'elenco azioni][addwebapi004]
3. <span data-ttu-id="0d7e7-251">Nel browser aggiungere **/api/contacts** all'URL.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-251">In the browser, append **/api/contacts** to the URL.</span></span>
   
    <span data-ttu-id="0d7e7-252">L'URL risultante sarà simile a http://localhost:1234/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-252">The resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="0d7e7-253">L'API Web RESTful aggiunta restituirà i contatti archiviati.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-253">The RESTful web API you added returns the stored contacts.</span></span> <span data-ttu-id="0d7e7-254">In Firefox e Chrome i dati saranno visualizzati in formato XML.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-254">Firefox and Chrome will display the data in XML format.</span></span>
   
    ![Pagina di indice con elementi dell'elenco azioni][rxFFchrome]

    <span data-ttu-id="0d7e7-256">In Internet Explorer verrà visualizzato un messaggio in cui viene chiesto se si desidera aprire o salvare i contatti.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-256">IE will prompt you to open or save the contacts.</span></span>

    ![Finestra di dialogo Salva dell'API Web][addwebapi006]


    <span data-ttu-id="0d7e7-258">È possibile aprire i contatti restituiti in Blocco note o in un browser.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-258">You can open the returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="0d7e7-259">Questo output può essere utilizzato da altre applicazioni, ad esempio una pagina Web o un'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Finestra di dialogo Salva dell'API Web][addwebapi007]

    <span data-ttu-id="0d7e7-261">**Avviso di sicurezza**: a questo punto, l'applicazione non è sicura ed è vulnerabile agli attacchi di richiesta intersito falsa (Cross-Site Request Forgery, CSRF).</span><span class="sxs-lookup"><span data-stu-id="0d7e7-261">**Security Warning**: At this point, your application is insecure and vulnerable to CSRF attack.</span></span> <span data-ttu-id="0d7e7-262">Questa vulnerabilità verrà rimossa più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-262">Later in the tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="0d7e7-263">Per altre informazioni, vedere l'articolo relativo alla [prevenzione delle richieste intersito false (CSRF)][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="0d7e7-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="0d7e7-264">Aggiunta della protezione XSRF</span><span class="sxs-lookup"><span data-stu-id="0d7e7-264">Add XSRF Protection</span></span>
<span data-ttu-id="0d7e7-265">La richiesta intersito falsa (nota anche come XSRF o CSRF) è un attacco contro applicazioni ospitate sul Web in base al quale un sito Web dannoso può influenzare l'interazione tra un browser client e un sito Web considerato attendibile da tale browser.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence the interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="0d7e7-266">Questi attacchi sono possibili in quanto i Web browser inviano automaticamente token di autenticazione con ogni richiesta a un sito Web.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request to a website.</span></span> <span data-ttu-id="0d7e7-267">Un classico esempio è un cookie di autenticazione, ad esempio un ticket di autenticazione basata su form di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-267">The canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="0d7e7-268">Tuttavia, i siti Web che usano un meccanismo di autenticazione persistente, ad esempio Autenticazione di Windows, autenticazione di base e così via, possono essere presi di mira da questi attacchi.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="0d7e7-269">Un attacco XSRF è diverso da un attacco di phishing.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="0d7e7-270">Gli attacchi di phishing richiedono un'interazione da parte della vittima.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-270">Phishing attacks require interaction from the victim.</span></span> <span data-ttu-id="0d7e7-271">In un attacco di phishing, un sito Web dannoso imita il sito Web di destinazione e la vittima viene indotta a fornire informazioni sensibili all'autore dell'attacco.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-271">In a phishing attack, a malicious website will mimic the target website, and the victim is fooled into providing sensitive information to the attacker.</span></span> <span data-ttu-id="0d7e7-272">In un attacco XSRF spesso non è necessaria alcuna interazione da parte della vittima.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-272">In an XSRF attack, there is often no interaction necessary from the victim.</span></span> <span data-ttu-id="0d7e7-273">Al contrario, l'attacco non fa che attendere che il browser invii automaticamente tutti i cookie pertinenti al sito Web di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-273">Rather, the attacker is relying on the browser automatically sending all relevant cookies to the destination website.</span></span>

<span data-ttu-id="0d7e7-274">Per altre informazioni, vedere il sito Web relativo all'[Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="0d7e7-274">For more information, see the [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="0d7e7-275">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **ContactManager**, scegliere **Aggiungi** e quindi fare clic su **Classe**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="0d7e7-276">Assegnare al file il nome *ValidateHttpAntiForgeryTokenAttribute.cs* e aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="0d7e7-276">Name the file *ValidateHttpAntiForgeryTokenAttribute.cs* and add the following code:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. <span data-ttu-id="0d7e7-277">Aggiungere l'istruzione *using* seguente al controller dei contratti in modo da poter accedere all'attributo **[ValidateHttpAntiForgeryToken]** .</span><span class="sxs-lookup"><span data-stu-id="0d7e7-277">Add the following *using* statement to the contracts controller so you have access to the **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="0d7e7-278">Aggiungere l'attributo **[ValidateHttpAntiForgeryToken]** ai metodi POST di **ContactsController** per proteggerlo dalle minacce XSRF.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-278">Add the **[ValidateHttpAntiForgeryToken]** attribute to the Post methods of the **ContactsController** to protect it from XSRF threats.</span></span> <span data-ttu-id="0d7e7-279">Sarà necessario aggiungerlo ai metodi di azione "PutContact", "PostContact" e **DeleteContact**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-279">You will add it to the "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="0d7e7-280">Aggiornare la sezione *Scripts* del file *Views\Home\Index.cshtml* in modo da includere il codice per recuperare i token XSRF.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-280">Update the *Scripts* section of the *Views\Home\Index.cshtml* file to include code to get the XSRF tokens.</span></span>
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-the-application-update-to-azure-and-sql-database"></a><span data-ttu-id="0d7e7-281">Pubblicare l'aggiornamento dell'applicazione in Azure e nel database SQL</span><span class="sxs-lookup"><span data-stu-id="0d7e7-281">Publish the application update to Azure and SQL Database</span></span>
<span data-ttu-id="0d7e7-282">Per pubblicare l'applicazione, ripetere la procedura seguita in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-282">To publish the application, you repeat the procedure you followed earlier.</span></span>

1. <span data-ttu-id="0d7e7-283">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-283">In **Solution Explorer**, right click the project and select **Publish**.</span></span>
   
    ![Pubblica][rxP]
2. <span data-ttu-id="0d7e7-285">Fare clic sulla scheda **Impostazioni** .</span><span class="sxs-lookup"><span data-stu-id="0d7e7-285">Click the **Settings** tab.</span></span>
3. <span data-ttu-id="0d7e7-286">In **ContactsManagerContext(ContactsManagerContext)** fare clic sull'icona **v** per sostituire la *Stringa di connessione remota* con la stringa di connessione per il database dei contatti.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-286">Under **ContactsManagerContext(ContactsManagerContext)**, click the **v** icon to change *Remote connection string* to the connection string for the contact database.</span></span> <span data-ttu-id="0d7e7-287">Fare clic su **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-287">Click **ContactDB**.</span></span>
   
    ![Impostazioni](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="0d7e7-289">Selezionare la casella per **Esegui Migrazioni Code First (esecuzione all'avvio dell'applicazione)**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-289">Check the box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="0d7e7-290">Fare clic su **Avanti** e quindi su **Anteprima**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="0d7e7-291">In Visual Studio verrà visualizzato un elenco dei file che verranno aggiunti o aggiornati.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-291">Visual Studio displays a list of the files that will be added or updated.</span></span>
6. <span data-ttu-id="0d7e7-292">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-292">Click **Publish**.</span></span>
   <span data-ttu-id="0d7e7-293">Al termine della distribuzione, nel browser verrà aperta la pagina iniziale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-293">After the deployment completes, the browser opens to the home page of the application.</span></span>
   
    ![Pagina di indice senza contatti][intro001]
   
    <span data-ttu-id="0d7e7-295">Il processo di pubblicazione di Visual Studio ha automaticamente configurato la stringa di connessione nel file *Web.config* distribuito affinché faccia riferimento al database SQL.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-295">The Visual Studio publish process automatically configured the connection string in the deployed *Web.config* file to point to the SQL database.</span></span> <span data-ttu-id="0d7e7-296">Ha inoltre configurato le migrazioni Code First affinché aggiornino automaticamente il database alla versione più recente la prima volta che l'applicazione accede al database dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-296">It also configured Code First Migrations to automatically upgrade the database to the latest version the first time the application accesses the database after deployment.</span></span>
   
    <span data-ttu-id="0d7e7-297">Grazie a questa configurazione, Code First ha creato il database tramite l'esecuzione del codice nella classe **Initial** creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-297">As a result of this configuration, Code First created the database by running the code in the **Initial** class that you created earlier.</span></span> <span data-ttu-id="0d7e7-298">Questa operazione è stata eseguita la prima volta che l'applicazione ha tentato di accedere al database dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-298">It did this the first time the application tried to access the database after deployment.</span></span>
7. <span data-ttu-id="0d7e7-299">Immettere un contatto come se l'app fosse eseguita localmente per verificare che la distribuzione del database abbia avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-299">Enter a contact as you did when you ran the app locally, to verify that database deployment succeeded.</span></span>

<span data-ttu-id="0d7e7-300">Se la voce immessa viene salvata e quindi visualizzata nella pagina di Contact Manager, significa che è stata archiviata nel database.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-300">When you see that the item you enter is saved and appears on the contact manager page, you know that it has been stored in the database.</span></span>

![Pagina di indice con contatti][addwebapi004]

<span data-ttu-id="0d7e7-302">L'applicazione è ora in esecuzione nel cloud e utilizza il database SQL per archiviare i relativi dati.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-302">The application is now running in the cloud, using SQL Database to store its data.</span></span> <span data-ttu-id="0d7e7-303">Al termine del test dell'applicazione in Azure, eliminarla.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-303">After you finish testing the application in Azure, delete it.</span></span> <span data-ttu-id="0d7e7-304">L'applicazione è pubblica e non dispone di un meccanismo per limitare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-304">The application is public and doesn't have a mechanism to limit access.</span></span>

> [!NOTE]
> <span data-ttu-id="0d7e7-305">Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-305">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="0d7e7-306">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0d7e7-307">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d7e7-307">Next Steps</span></span>
<span data-ttu-id="0d7e7-308">Un altro modo per archiviare i dati in un'applicazione di Azure consiste nell'utilizzare Archiviazione di Azure, che offre un servizio di archiviazione di dati non relazionali sotto forma di BLOB e tabelle.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-308">Another way to store data in an Azure application is to use Azure storage, which provide non-relational data storage in the form of blobs and tables.</span></span> <span data-ttu-id="0d7e7-309">Per ulteriori informazioni sull'API Web, su ASP.NET MVC e Azure, vedere i collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-309">The following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="0d7e7-310">[Introduzione a Entity Framework con MVC][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="0d7e7-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="0d7e7-311">Introduzione ad ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="0d7e7-311">Intro to ASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="0d7e7-312">Creare la prima API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0d7e7-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="0d7e7-313">Debug di WAWS</span><span class="sxs-lookup"><span data-stu-id="0d7e7-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="0d7e7-314">Questa esercitazione e l'applicazione di esempio sono state scritte da [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) con il supporto di Tom Dykstra e Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="0d7e7-314">This tutorial and the sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="0d7e7-315">Se lo si desidera, inviare commenti e suggerimenti sugli aspetti ritenuti utili e su eventuali miglioramenti da apportare, non solo in merito all'esercitazione ma anche ai prodotti illustrati nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-315">Please leave feedback on what you liked or what you would like to see improved, not only about the tutorial itself but also about the products that it demonstrates.</span></span> <span data-ttu-id="0d7e7-316">I commenti e suggerimenti saranno utili per definire la priorità dei miglioramenti da apportare.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="0d7e7-317">In particolare, saranno apprezzati i commenti relativi all'interesse in merito a un'ulteriore automazione per il processo di configurazione e distribuzione del database di appartenenza.</span><span class="sxs-lookup"><span data-stu-id="0d7e7-317">We are especially interested in finding out how much interest there is in more automation for the process of configuring and deploying the membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="0d7e7-318">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="0d7e7-318">What's changed</span></span>
* <span data-ttu-id="0d7e7-319">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="0d7e7-319">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles to the Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update the Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

