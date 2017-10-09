---
title: un'API REST in Azure con ASP.NET e database SQL aaaCreate | Documenti Microsoft
description: Un'esercitazione che illustra come un'applicazione che utilizza toodeploy hello tooan ASP.NET Web API app web di Azure tramite Visual Studio.
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
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="8c47c-103">Creare un servizio REST con l'API Web ASP.NET e il database SQL in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="8c47c-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="8c47c-104">Questa esercitazione viene illustrato come toodeploy ASP.NET web app tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) utilizzando la procedura guidata Pubblica sito Web hello in Visual Studio 2013 o Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="8c47c-104">This tutorial shows how toodeploy an ASP.NET web app tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using hello Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="8c47c-105">È possibile aprire un account Azure, gratuitamente, e se si dispone già di Visual Studio 2013, hello SDK installa automaticamente Visual Studio 2013 per Web.</span><span class="sxs-lookup"><span data-stu-id="8c47c-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, hello SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="8c47c-106">Sarà quindi possibile iniziare a sviluppare per Azure del tutto gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="8c47c-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="8c47c-107">In questa esercitazione si presuppone che l'utente non abbia mai utilizzato Azure.</span><span class="sxs-lookup"><span data-stu-id="8c47c-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="8c47c-108">Dopo aver completato questa esercitazione, è necessario un'app web semplici backup e in esecuzione nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-108">On completing this tutorial, you'll have a simple web app up and running in hello cloud.</span></span>

<span data-ttu-id="8c47c-109">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="8c47c-109">You'll learn:</span></span>

* <span data-ttu-id="8c47c-110">Come tooenable il computer per lo sviluppo di Azure installando hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="8c47c-110">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="8c47c-111">Come toocreate un Visual Studio ASP.NET MVC 5 del progetto e pubblicarlo tooan app di Azure.</span><span class="sxs-lookup"><span data-stu-id="8c47c-111">How toocreate a Visual Studio ASP.NET MVC 5 project and publish it tooan Azure app.</span></span>
* <span data-ttu-id="8c47c-112">Come toouse hello tooenable ASP.NET Web API chiamate all'API REST.</span><span class="sxs-lookup"><span data-stu-id="8c47c-112">How toouse hello ASP.NET Web API tooenable Restful API calls.</span></span>
* <span data-ttu-id="8c47c-113">Come toouse un SQL database toostore dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="8c47c-113">How toouse a SQL database toostore data in Azure.</span></span>
* <span data-ttu-id="8c47c-114">Come applicazione toopublish Aggiorna tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8c47c-114">How toopublish application updates tooAzure.</span></span>

<span data-ttu-id="8c47c-115">Compilerai un'applicazione web semplice elenco di contatti che si basa su ASP.NET MVC 5 e utilizza hello ADO.NET Entity Framework per l'accesso al database.</span><span class="sxs-lookup"><span data-stu-id="8c47c-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses hello ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="8c47c-116">completa l'applicazione Hello hello illustrato nella figura riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="8c47c-116">hello following illustration shows hello completed application:</span></span>

![schermata del sito web][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a><span data-ttu-id="8c47c-118">Creare il progetto hello</span><span class="sxs-lookup"><span data-stu-id="8c47c-118">Create hello project</span></span>
1. <span data-ttu-id="8c47c-119">Avviare Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="8c47c-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="8c47c-120">Da hello **File** dal menu **nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-120">From hello **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="8c47c-121">In hello **nuovo progetto** finestra di dialogo espandere **Visual c#** e selezionare **Web** e quindi selezionare **applicazione Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-121">In hello **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="8c47c-122">Nome di un'applicazione hello **ContactManager** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-122">Name hello application **ContactManager** and click **OK**.</span></span>
   
    ![Finestra di dialogo Nuovo progetto](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="8c47c-124">In hello **nuovo progetto ASP.NET** la finestra di dialogo, seleziona hello **MVC** modello di controllo **API Web** e quindi fare clic su **Modifica autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-124">In hello **New ASP.NET Project** dialog box, select hello **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="8c47c-125">In hello **Modifica autenticazione** la finestra di dialogo, fare clic su **Nessuna autenticazione**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-125">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![No Authentication](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="8c47c-127">si sta creando un'applicazione Hello esempio non disporrà di funzionalità che richiedono toolog gli utenti in.</span><span class="sxs-lookup"><span data-stu-id="8c47c-127">hello sample application you're creating won't have features that require users toolog in.</span></span> <span data-ttu-id="8c47c-128">Per informazioni sulla funzionalità di autenticazione e autorizzazione tooimplement, vedere hello [passaggi successivi](#nextsteps) sezione alla fine di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8c47c-128">For information about how tooimplement authentication and authorization features, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
6. <span data-ttu-id="8c47c-129">In hello **nuovo progetto ASP.NET** la finestra di dialogo, verificare che hello **Host nel Cloud hello** è selezionata e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-129">In hello **New ASP.NET Project** dialog box, make sure hello **Host in hello Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="8c47c-130">Se non è stato precedentemente firmato in tooAzure, sarà richiesta toosign in.</span><span class="sxs-lookup"><span data-stu-id="8c47c-130">If you have not previously signed in tooAzure, you will be prompted toosign in.</span></span>

1. <span data-ttu-id="8c47c-131">procedura guidata di configurazione Hello suggerirà un nome univoco basato sul *ContactManager* (vedere l'immagine di hello riportata di seguito).</span><span class="sxs-lookup"><span data-stu-id="8c47c-131">hello configuration wizard will suggest a unique name based on *ContactManager* (see hello image below).</span></span> <span data-ttu-id="8c47c-132">Selezionare un'area nelle vicinanze.</span><span class="sxs-lookup"><span data-stu-id="8c47c-132">Select a region near you.</span></span> <span data-ttu-id="8c47c-133">È possibile utilizzare [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello più bassa latenza datacenter.</span><span class="sxs-lookup"><span data-stu-id="8c47c-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello lowest latency data center.</span></span> 
2. <span data-ttu-id="8c47c-134">Se non è stato creato un server di database, selezionare **Crea nuovo server**e immettere un nome utente e una password per il database.</span><span class="sxs-lookup"><span data-stu-id="8c47c-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Configurare il sito Web di Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="8c47c-136">Se si dispone di un server di database, utilizzare tale toocreate un nuovo database.</span><span class="sxs-lookup"><span data-stu-id="8c47c-136">If you have a database server, use that toocreate a new database.</span></span> <span data-ttu-id="8c47c-137">Server di database sono una risorsa preziosa, e in genere si desidera toocreate più database nella hello stesso server per il test e sviluppo anziché creare un server di database per ogni database.</span><span class="sxs-lookup"><span data-stu-id="8c47c-137">Database servers are a precious resource, and you generally want toocreate multiple databases on hello same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="8c47c-138">Verificare che il sito web e il database siano in hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="8c47c-138">Make sure your web site and database are in hello same region.</span></span>

![Configurare il sito Web di Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a><span data-ttu-id="8c47c-140">Impostare l'intestazione di pagina hello e piè di pagina</span><span class="sxs-lookup"><span data-stu-id="8c47c-140">Set hello page header and footer</span></span>
1. <span data-ttu-id="8c47c-141">In **Esplora**, espandere hello *Views\Shared* cartella e aprire hello *layout. cshtml* file.</span><span class="sxs-lookup"><span data-stu-id="8c47c-141">In **Solution Explorer**, expand hello *Views\Shared* folder and open hello *_Layout.cshtml* file.</span></span>
   
    ![File _Layout.cshtml in Esplora soluzioni][newapp004]
2. <span data-ttu-id="8c47c-143">Sostituire il contenuto di hello di hello *Views\Shared_Layout.cshtml* file con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="8c47c-143">Replace hello contents of hello *Views\Shared_Layout.cshtml* file with hello following code:</span></span>

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

<span data-ttu-id="8c47c-144">markup Hello sopra al nome app hello modifiche da "My App ASP.NET" troppo "contatto Manager" che rimuove i collegamenti di hello troppo**Home**, **su** e **contatto**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-144">hello markup above changes hello app name from "My ASP.NET App" too"Contact Manager", and it removes hello links too**Home**, **About** and **Contact**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="8c47c-145">Eseguire un'applicazione hello in locale</span><span class="sxs-lookup"><span data-stu-id="8c47c-145">Run hello application locally</span></span>
1. <span data-ttu-id="8c47c-146">Premere CTRL + F5 toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-146">Press CTRL+F5 toorun hello application.</span></span>
   <span data-ttu-id="8c47c-147">home page dell'applicazione Hello viene visualizzato nel browser predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-147">hello application home page appears in hello default browser.</span></span>
    <span data-ttu-id="8c47c-148">![home page di tooDo elenco](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="8c47c-148">![tooDo List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="8c47c-149">Questo è tutto ciò che serve toodo si distribuiranno tooAzure un'applicazione hello toocreate ora.</span><span class="sxs-lookup"><span data-stu-id="8c47c-149">This is all you need toodo for now toocreate hello application that you'll deploy tooAzure.</span></span> <span data-ttu-id="8c47c-150">La funzionalità di database verrà aggiunta in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="8c47c-150">Later you'll add database functionality.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="8c47c-151">Distribuire tooAzure applicazione hello</span><span class="sxs-lookup"><span data-stu-id="8c47c-151">Deploy hello application tooAzure</span></span>
1. <span data-ttu-id="8c47c-152">In Visual Studio, fare clic sul progetto hello in **Esplora** e selezionare **pubblica** dal menu di scelta rapida hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-152">In Visual Studio, right-click hello project in **Solution Explorer** and select **Publish** from hello context menu.</span></span>
   
    ![Opzione Pubblica nel menu di scelta rapida del progetto][PublishVSSolution]
   
    <span data-ttu-id="8c47c-154">Hello **pubblica sul Web** apre la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="8c47c-154">hello **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="8c47c-155">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-155">Click **Publish**.</span></span>

![Scheda Settings](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="8c47c-157">Visual Studio avvia il processo di hello di copia hello toohello di file server di Azure.</span><span class="sxs-lookup"><span data-stu-id="8c47c-157">Visual Studio begins hello process of copying hello files toohello Azure server.</span></span> <span data-ttu-id="8c47c-158">Hello **Output** finestra Mostra intraprese le azioni di distribuzione e segnala il completamento corretto della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-158">hello **Output** window shows what deployment actions were taken and reports successful completion of hello deployment.</span></span>

1. <span data-ttu-id="8c47c-159">browser predefinito Hello verrà aperta automaticamente toohello URL del sito hello distribuito.</span><span class="sxs-lookup"><span data-stu-id="8c47c-159">hello default browser automatically opens toohello URL of hello deployed site.</span></span>
   
   <span data-ttu-id="8c47c-160">un'applicazione Hello creato è in esecuzione nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-160">hello application you created is now running in hello cloud.</span></span>
   
   ![pagina iniziale di elenco tooDo in esecuzione in Azure][rxz2]

## <a name="add-a-database-toohello-application"></a><span data-ttu-id="8c47c-162">Aggiungere un'applicazione di database toohello</span><span class="sxs-lookup"><span data-stu-id="8c47c-162">Add a database toohello application</span></span>
<span data-ttu-id="8c47c-163">Successivamente, verrà aggiornare hello MVC applicazione tooadd hello possibilità toodisplay e aggiornare i contatti e archiviare dati hello in un database.</span><span class="sxs-lookup"><span data-stu-id="8c47c-163">Next, you'll update hello MVC application tooadd hello ability toodisplay and update contacts and store hello data in a database.</span></span> <span data-ttu-id="8c47c-164">applicazione Hello tooread e il database di hello Entity Framework toocreate hello e aggiornare i dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-164">hello application will use hello Entity Framework toocreate hello database and tooread and update data in hello database.</span></span>

### <a name="add-data-model-classes-for-hello-contacts"></a><span data-ttu-id="8c47c-165">Aggiungere le classi di modello di dati per i contatti hello</span><span class="sxs-lookup"><span data-stu-id="8c47c-165">Add data model classes for hello contacts</span></span>
<span data-ttu-id="8c47c-166">Creare innanzitutto un semplice modello di dati nel codice.</span><span class="sxs-lookup"><span data-stu-id="8c47c-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="8c47c-167">In **Esplora**, fare clic sulla cartella Modelli hello, fare clic su **Aggiungi**e quindi **classe**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-167">In **Solution Explorer**, right-click hello Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Aggiungi classe nel menu di scelta rapida della cartella Modelli][adddb001]
2. <span data-ttu-id="8c47c-169">In hello **Aggiungi nuovo elemento** della finestra di dialogo Nome hello nuovo file di classe *Contact.cs*, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-169">In hello **Add New Item** dialog box, name hello new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Finestra di dialogo Aggiungi nuovo elemento][adddb002]
3. <span data-ttu-id="8c47c-171">Sostituire il contenuto di hello del file Contacts.cs hello con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="8c47c-171">Replace hello contents of hello Contacts.cs file with hello following code.</span></span>
   
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

<span data-ttu-id="8c47c-172">Hello **contattare** classe definisce i dati di hello che verranno archiviati per ogni contatto, oltre a una chiave primaria, ContactID, richiesto dal database hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-172">hello **Contact** class defines hello data that you will store for each contact, plus a primary key, ContactID, that is needed by hello database.</span></span> <span data-ttu-id="8c47c-173">È possibile ottenere ulteriori informazioni sui modelli di dati in hello [passaggi successivi](#nextsteps) sezione alla fine di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8c47c-173">You can get more information about data models in hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a><span data-ttu-id="8c47c-174">Creare pagine web che consentono di toowork agli utenti di app con i contatti hello</span><span class="sxs-lookup"><span data-stu-id="8c47c-174">Create web pages that enable app users toowork with hello contacts</span></span>
<span data-ttu-id="8c47c-175">Hello funzionalità di scaffolding di ASP.NET MVC hello può generare automaticamente il codice che esegue creare, leggere, aggiornare ed eliminare azioni (CRUD).</span><span class="sxs-lookup"><span data-stu-id="8c47c-175">hello ASP.NET MVC hello scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-hello-data"></a><span data-ttu-id="8c47c-176">Aggiungere un Controller e una visualizzazione per i dati di hello</span><span class="sxs-lookup"><span data-stu-id="8c47c-176">Add a Controller and a view for hello data</span></span>
1. <span data-ttu-id="8c47c-177">In **Esplora**, espandere cartella Controllers hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-177">In **Solution Explorer**, expand hello Controllers folder.</span></span>
2. <span data-ttu-id="8c47c-178">Compilare il progetto hello **(Ctrl + MAIUSC + B)**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-178">Build hello project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="8c47c-179">(È necessario compilare il progetto hello prima di utilizzare il meccanismo di scaffolding).</span><span class="sxs-lookup"><span data-stu-id="8c47c-179">(You must build hello project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="8c47c-180">Fare clic sulla cartella controller hello e fare clic su **Aggiungi**, quindi fare clic su **Controller**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-180">Right-click hello Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Opzione Aggiungi controller nel menu di scelta rapida della cartella Controllers][addcode001]
4. <span data-ttu-id="8c47c-182">In hello **aggiungere lo scaffolding** nella finestra di dialogo **Controller MVC con visualizzazioni, mediante Entity Framework** e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-182">In hello **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Aggiungi controller](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="8c47c-184">Impostare il nome di controller hello troppo**HomeController**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-184">Set hello controller name too**HomeController**.</span></span> <span data-ttu-id="8c47c-185">Selezionare **Contact** come classe del modello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="8c47c-186">Fare clic su hello **nuovo contesto dati** pulsante e accettare hello predefinito "ContactManager.Models.ContactManagerContext" hello **nuovo tipo di contesto dati**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-186">Click hello **New data context** button and accept hello default "ContactManager.Models.ContactManagerContext" for hello **New data context type**.</span></span> <span data-ttu-id="8c47c-187">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-187">Click **Add**.</span></span>

    <span data-ttu-id="8c47c-188">Una finestra di dialogo verrà chiesto: "un file con nome hello HomeController esiste già.</span><span class="sxs-lookup"><span data-stu-id="8c47c-188">A dialog box will prompt you: "A file with hello name HomeController already exits.</span></span> <span data-ttu-id="8c47c-189">Si desidera tooreplace è? ".</span><span class="sxs-lookup"><span data-stu-id="8c47c-189">Do you want tooreplace it?".</span></span> <span data-ttu-id="8c47c-190">Fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-190">Click **Yes**.</span></span> <span data-ttu-id="8c47c-191">Si sta sovrascrivendo hello Home Controller che è stato creato con il nuovo progetto di hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-191">We are overwriting hello Home Controller that was created with hello new project.</span></span> <span data-ttu-id="8c47c-192">Si utilizzerà hello nuovo Home Controller per l'elenco di contatti.</span><span class="sxs-lookup"><span data-stu-id="8c47c-192">We will use hello new Home Controller for our contact list.</span></span>

    <span data-ttu-id="8c47c-193">In Visual Studio verranno creati metodi e visualizzazioni di un controller per operazioni CRUD di database per oggetti **Contact** .</span><span class="sxs-lookup"><span data-stu-id="8c47c-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="8c47c-194">Abilitare le migrazioni, creare database hello, aggiungere dati di esempio e un inizializzatore di dati</span><span class="sxs-lookup"><span data-stu-id="8c47c-194">Enable Migrations, create hello database, add sample data and a data initializer</span></span>
<span data-ttu-id="8c47c-195">attività successiva Hello è hello tooenable [migrazioni Code First](http://curah.microsoft.com/55220) funzionalità nel database di hello toocreate ordine basato sul modello di dati hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="8c47c-195">hello next task is tooenable hello [Code First Migrations](http://curah.microsoft.com/55220) feature in order toocreate hello database based on hello data model you created.</span></span>

1. <span data-ttu-id="8c47c-196">In hello **strumenti** dal menu **Gestione pacchetti libreria** e quindi **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-196">In hello **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Console di Gestione pacchetti nel menu Strumenti][addcode008]
2. <span data-ttu-id="8c47c-198">In hello **Package Manager Console** finestra immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8c47c-198">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="8c47c-199">Hello **enable-migrations** comando crea un *migrazioni* cartella e lo inserisce in questa cartella un *Configuration.cs* file che è possibile modificare le migrazioni tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="8c47c-199">hello **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit tooconfigure Migrations.</span></span> 
3. <span data-ttu-id="8c47c-200">In hello **Package Manager Console** finestra immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8c47c-200">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="8c47c-201">Hello **iniziale migrazione aggiungere** comando genera una classe denominata  **&lt;date_stamp&gt;iniziale** che crea database hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-201">hello **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates hello database.</span></span> <span data-ttu-id="8c47c-202">primo parametro Hello ( *iniziale* ) è arbitrario e utilizzati toocreate hello nome del file hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-202">hello first parameter ( *Initial* ) is arbitrary and used toocreate hello name of hello file.</span></span> <span data-ttu-id="8c47c-203">È possibile visualizzare hello nuovi file di classe in **Esplora**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-203">You can see hello new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="8c47c-204">In hello **iniziale** classe hello **backup** metodo crea tabella Contacts hello e hello **verso il basso** rilascia metodo (utilizzato quando si desidera che lo stato precedente di tooreturn toohello).</span><span class="sxs-lookup"><span data-stu-id="8c47c-204">In hello **Initial** class, hello **Up** method creates hello Contacts table, and hello **Down** method (used when you want tooreturn toohello previous state) drops it.</span></span>
4. <span data-ttu-id="8c47c-205">Aprire hello *Migrations\Configuration.cs* file.</span><span class="sxs-lookup"><span data-stu-id="8c47c-205">Open hello *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="8c47c-206">Aggiungere i seguenti spazi dei nomi hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-206">Add hello following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="8c47c-207">Sostituire hello *valore di inizializzazione* metodo con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="8c47c-207">Replace hello *Seed* method with hello following code:</span></span>
   
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
   
    <span data-ttu-id="8c47c-208">Questo codice precedente verrà inizializzato database hello con le informazioni di contatto hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-208">This code above will initialize hello database with hello contact information.</span></span> <span data-ttu-id="8c47c-209">Per ulteriori informazioni sui database hello il seeding, vedere [il debug di Entity Framework (EF) database](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c47c-209">For more information on seeding hello database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="8c47c-210">In hello **Package Manager Console** immettere il comando hello:</span><span class="sxs-lookup"><span data-stu-id="8c47c-210">In hello **Package Manager Console** enter hello command:</span></span>
   
        update-database
   
    ![Comandi di Console di Gestione pacchetti][addcode009]
   
    <span data-ttu-id="8c47c-212">Hello **aggiornamento database** esecuzioni hello migrazione prima che crea database hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-212">hello **update-database** runs hello first migration which creates hello database.</span></span> <span data-ttu-id="8c47c-213">Per impostazione predefinita, il database di hello viene creato come database di SQL Server Express LocalDB.</span><span class="sxs-lookup"><span data-stu-id="8c47c-213">By default, hello database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="8c47c-214">Premere CTRL + F5 toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-214">Press CTRL+F5 toorun hello application.</span></span> 

<span data-ttu-id="8c47c-215">un'applicazione Hello Mostra dati di inizializzazione hello e consente di modificare i dettagli e collegamenti Elimina.</span><span class="sxs-lookup"><span data-stu-id="8c47c-215">hello application shows hello seed data and provides edit, details and delete links.</span></span>

![Visualizzazione MVC dei dati][rxz3]

## <a name="edit-hello-view"></a><span data-ttu-id="8c47c-217">Modifica vista hello</span><span class="sxs-lookup"><span data-stu-id="8c47c-217">Edit hello View</span></span>
1. <span data-ttu-id="8c47c-218">Aprire hello *Views\Home\Index.cshtml* file.</span><span class="sxs-lookup"><span data-stu-id="8c47c-218">Open hello *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="8c47c-219">Nel passaggio successivo hello, si sostituirà markup hello generato con il codice che usa [jQuery](http://jquery.com/) e [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="8c47c-219">In hello next step, we will replace hello generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="8c47c-220">Questo codice recupera l'elenco di hello di contatti da mediante API web e JSON e quindi associa hello contattare toohello dati dell'interfaccia utente utilizzando knockout.js.</span><span class="sxs-lookup"><span data-stu-id="8c47c-220">This new code retrieves hello list of contacts from using web API and JSON and then binds hello contact data toohello UI using knockout.js.</span></span> <span data-ttu-id="8c47c-221">Per ulteriori informazioni, vedere hello [passaggi successivi](#nextsteps) sezione alla fine di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8c47c-221">For more information, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
2. <span data-ttu-id="8c47c-222">Sostituire il contenuto di hello del file hello con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="8c47c-222">Replace hello contents of hello file with hello following code.</span></span>
   
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
3. <span data-ttu-id="8c47c-223">Fare clic sulla cartella del contenuto hello e fare clic su **Aggiungi**, quindi fare clic su **nuovo elemento...** .</span><span class="sxs-lookup"><span data-stu-id="8c47c-223">Right-click hello Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Opzione Aggiungi foglio di stile nel menu di scelta rapida della cartella Content][addcode005]
4. <span data-ttu-id="8c47c-225">In hello **Aggiungi nuovo elemento** finestra di dialogo immettere **stile** nella casella di ricerca a destra superiore hello e quindi selezionare **foglio di stile**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-225">In hello **Add New Item** dialog box, enter **Style** in hello upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="8c47c-226">![Finestra di dialogo Aggiungi nuovo elemento][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="8c47c-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="8c47c-227">File con nome hello *Contacts.css* e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-227">Name hello file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="8c47c-228">Sostituire il contenuto di hello del file hello con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="8c47c-228">Replace hello contents of hello file with hello following code.</span></span>
   
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
   
    <span data-ttu-id="8c47c-229">Si utilizzerà questo foglio di stile per il layout di hello, colori e stili utilizzati nell'applicazione Gestione contatti hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-229">We will use this style sheet for hello layout, colors and styles used in hello contact manager app.</span></span>
6. <span data-ttu-id="8c47c-230">Aprire hello *App_Start\BundleConfig.cs* file.</span><span class="sxs-lookup"><span data-stu-id="8c47c-230">Open hello *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="8c47c-231">Aggiungere i seguenti hello tooregister codice hello [Knockout](http://knockoutjs.com/index.html "KO") plug-in.</span><span class="sxs-lookup"><span data-stu-id="8c47c-231">Add hello following code tooregister hello [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="8c47c-232">In questo esempio utilizzando knockout toosimplify dinamico il codice JavaScript che gestisce i modelli di schermata hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-232">This sample using knockout toosimplify dynamic JavaScript code that handles hello screen templates.</span></span>
8. <span data-ttu-id="8c47c-233">Modificare hello di hello contenuto/css voce tooregister *contacts.css* foglio di stile.</span><span class="sxs-lookup"><span data-stu-id="8c47c-233">Modify hello contents/css entry tooregister hello *contacts.css* style sheet.</span></span> <span data-ttu-id="8c47c-234">Modificare hello seguente riga:</span><span class="sxs-lookup"><span data-stu-id="8c47c-234">Change hello following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="8c47c-235">Con:</span><span class="sxs-lookup"><span data-stu-id="8c47c-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="8c47c-236">Nella Console di gestione pacchetti hello, eseguire hello successivo comando tooinstall Knockout.</span><span class="sxs-lookup"><span data-stu-id="8c47c-236">In hello Package Manager Console, run hello following command tooinstall Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a><span data-ttu-id="8c47c-237">Aggiungere un controller per l'interfaccia Web API Restful hello</span><span class="sxs-lookup"><span data-stu-id="8c47c-237">Add a controller for hello Web API Restful interface</span></span>
1. <span data-ttu-id="8c47c-238">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla cartella Controllers, quindi scegliere **Aggiungi** e infine **Controller**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="8c47c-239">In hello **aggiungere lo scaffolding** finestra di dialogo immettere **Web 2 Controller API con azioni, mediante Entity Framework** e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-239">In hello **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![Aggiunta di un controller per l'API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="8c47c-241">In hello **Aggiungi Controller** finestra di dialogo immettere "ContactsController" come nome del controller.</span><span class="sxs-lookup"><span data-stu-id="8c47c-241">In hello **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="8c47c-242">Selezionare "Contact (ContactManager.Models)" per hello **classe modello**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-242">Select "Contact (ContactManager.Models)" for hello **Model class**.</span></span>  <span data-ttu-id="8c47c-243">Mantenere il valore predefinito hello per hello **classe contesto dati**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-243">Keep hello default value for hello **Data context class**.</span></span> 
4. <span data-ttu-id="8c47c-244">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-244">Click **Add**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="8c47c-245">Eseguire un'applicazione hello in locale</span><span class="sxs-lookup"><span data-stu-id="8c47c-245">Run hello application locally</span></span>
1. <span data-ttu-id="8c47c-246">Premere CTRL + F5 toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-246">Press CTRL+F5 toorun hello application.</span></span>
   
    ![Pagina di indice][intro001]
2. <span data-ttu-id="8c47c-248">Immettere un contatto e fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="8c47c-249">app Hello restituisce toohello homepage e contatto hello immesso viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="8c47c-249">hello app returns toohello home page and displays hello contact you entered.</span></span>
   
    ![Pagina di indice con elementi dell'elenco azioni][addwebapi004]
3. <span data-ttu-id="8c47c-251">In browser hello, aggiungere **/api/contatti** toohello URL.</span><span class="sxs-lookup"><span data-stu-id="8c47c-251">In hello browser, append **/api/contacts** toohello URL.</span></span>
   
    <span data-ttu-id="8c47c-252">URL di Hello risultante sarà simile a http://localhost:1234/api/contatti.</span><span class="sxs-lookup"><span data-stu-id="8c47c-252">hello resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="8c47c-253">API è stato aggiunto a web RESTful Hello restituisce contatti hello archiviato.</span><span class="sxs-lookup"><span data-stu-id="8c47c-253">hello RESTful web API you added returns hello stored contacts.</span></span> <span data-ttu-id="8c47c-254">Firefox e Chrome verranno visualizzati i dati di hello in formato XML.</span><span class="sxs-lookup"><span data-stu-id="8c47c-254">Firefox and Chrome will display hello data in XML format.</span></span>
   
    ![Pagina di indice con elementi dell'elenco azioni][rxFFchrome]

    <span data-ttu-id="8c47c-256">Internet Explorer verrà chiesto tooopen o salvare i contatti hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-256">IE will prompt you tooopen or save hello contacts.</span></span>

    ![Finestra di dialogo Salva dell'API Web][addwebapi006]


    <span data-ttu-id="8c47c-258">È possibile aprire hello restituito contatti in blocco note o un browser.</span><span class="sxs-lookup"><span data-stu-id="8c47c-258">You can open hello returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="8c47c-259">Questo output può essere utilizzato da altre applicazioni, ad esempio una pagina Web o un'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8c47c-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Finestra di dialogo Salva dell'API Web][addwebapi007]

    <span data-ttu-id="8c47c-261">**Avviso di sicurezza**: A questo punto, l'applicazione è attacco tooCSRF vulnerabile e non protetti.</span><span class="sxs-lookup"><span data-stu-id="8c47c-261">**Security Warning**: At this point, your application is insecure and vulnerable tooCSRF attack.</span></span> <span data-ttu-id="8c47c-262">Più avanti nell'esercitazione di hello verrà rimossa questa vulnerabilità.</span><span class="sxs-lookup"><span data-stu-id="8c47c-262">Later in hello tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="8c47c-263">Per altre informazioni, vedere l'articolo relativo alla [prevenzione delle richieste intersito false (CSRF)][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="8c47c-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="8c47c-264">Aggiunta della protezione XSRF</span><span class="sxs-lookup"><span data-stu-id="8c47c-264">Add XSRF Protection</span></span>
<span data-ttu-id="8c47c-265">Falsificazione della richiesta tra siti tra (noto anche come XSRF o CSRF) è un attacco contro applicazioni ospitate da web in base al quale un sito Web dannoso può influenzare l'interazione di hello tra un browser del client e un sito Web considerato attendibile da tale browser.</span><span class="sxs-lookup"><span data-stu-id="8c47c-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence hello interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="8c47c-266">Questi attacchi sono possibili perché browser invierà i token di autenticazione automaticamente con ogni sito Web tooa richiesta.</span><span class="sxs-lookup"><span data-stu-id="8c47c-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request tooa website.</span></span> <span data-ttu-id="8c47c-267">esempio canonico Hello è un cookie di autenticazione, ad esempio, ASP. Ticket di autenticazione basata su form della rete.</span><span class="sxs-lookup"><span data-stu-id="8c47c-267">hello canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="8c47c-268">Tuttavia, i siti Web che usano un meccanismo di autenticazione persistente, ad esempio Autenticazione di Windows, autenticazione di base e così via, possono essere presi di mira da questi attacchi.</span><span class="sxs-lookup"><span data-stu-id="8c47c-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="8c47c-269">Un attacco XSRF è diverso da un attacco di phishing.</span><span class="sxs-lookup"><span data-stu-id="8c47c-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="8c47c-270">Attacchi di phishing richiedono l'interazione da vittima hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-270">Phishing attacks require interaction from hello victim.</span></span> <span data-ttu-id="8c47c-271">In un attacco di phishing, un sito Web dannoso imitino sito Web di destinazione hello e vittima hello è significativo a fornire l'autore dell'attacco toohello informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="8c47c-271">In a phishing attack, a malicious website will mimic hello target website, and hello victim is fooled into providing sensitive information toohello attacker.</span></span> <span data-ttu-id="8c47c-272">In un attacco XSRF, non vi è spesso alcuna interazione necessari da vittima hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-272">In an XSRF attack, there is often no interaction necessary from hello victim.</span></span> <span data-ttu-id="8c47c-273">Piuttosto, autore dell'attacco hello si basa su browser hello automaticamente l'invio del sito Web di tutti i cookie rilevanti toohello destinazione.</span><span class="sxs-lookup"><span data-stu-id="8c47c-273">Rather, hello attacker is relying on hello browser automatically sending all relevant cookies toohello destination website.</span></span>

<span data-ttu-id="8c47c-274">Per ulteriori informazioni, vedere hello [Apri progetto di sicurezza dell'applicazione Web](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="8c47c-274">For more information, see hello [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="8c47c-275">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **ContactManager**, scegliere **Aggiungi** e quindi fare clic su **Classe**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="8c47c-276">File con nome hello *ValidateHttpAntiForgeryTokenAttribute.cs* e aggiungere hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="8c47c-276">Name hello file *ValidateHttpAntiForgeryTokenAttribute.cs* and add hello following code:</span></span>
   
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
3. <span data-ttu-id="8c47c-277">Aggiungere il seguente hello *utilizzando* toohello istruzione contratti controller in modo che sia accesso toohello **[ValidateHttpAntiForgeryToken]** attributo.</span><span class="sxs-lookup"><span data-stu-id="8c47c-277">Add hello following *using* statement toohello contracts controller so you have access toohello **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="8c47c-278">Aggiungere hello **[ValidateHttpAntiForgeryToken]** attributo metodi Post toohello di hello **ContactsController** tooprotect da minacce XSRF.</span><span class="sxs-lookup"><span data-stu-id="8c47c-278">Add hello **[ValidateHttpAntiForgeryToken]** attribute toohello Post methods of hello **ContactsController** tooprotect it from XSRF threats.</span></span> <span data-ttu-id="8c47c-279">Si aggiungerà toohello "PutContact", "PostContact" e **DeleteContact** metodi di azione.</span><span class="sxs-lookup"><span data-stu-id="8c47c-279">You will add it toohello "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="8c47c-280">Hello aggiornamento *script* sezione di hello *Views\Home\Index.cshtml* i token XSRF tooinclude codice tooget hello del file.</span><span class="sxs-lookup"><span data-stu-id="8c47c-280">Update hello *Scripts* section of hello *Views\Home\Index.cshtml* file tooinclude code tooget hello XSRF tokens.</span></span>
   
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

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a><span data-ttu-id="8c47c-281">Pubblicare tooAzure di aggiornamento dell'applicazione hello e Database SQL</span><span class="sxs-lookup"><span data-stu-id="8c47c-281">Publish hello application update tooAzure and SQL Database</span></span>
<span data-ttu-id="8c47c-282">un'applicazione hello toopublish, ripetere procedura hello che è eseguita in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8c47c-282">toopublish hello application, you repeat hello procedure you followed earlier.</span></span>

1. <span data-ttu-id="8c47c-283">In **Esplora**, fare clic con il pulsante destro progetto hello e selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-283">In **Solution Explorer**, right click hello project and select **Publish**.</span></span>
   
    ![Pubblica][rxP]
2. <span data-ttu-id="8c47c-285">Fare clic su hello **impostazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="8c47c-285">Click hello **Settings** tab.</span></span>
3. <span data-ttu-id="8c47c-286">In **ContactsManagerContext(ContactsManagerContext)**, fare clic su hello **v** icona toochange *stringa di connessione remota* toohello stringa di connessione per il contatto hello database.</span><span class="sxs-lookup"><span data-stu-id="8c47c-286">Under **ContactsManagerContext(ContactsManagerContext)**, click hello **v** icon toochange *Remote connection string* toohello connection string for hello contact database.</span></span> <span data-ttu-id="8c47c-287">Fare clic su **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-287">Click **ContactDB**.</span></span>
   
    ![Impostazioni](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="8c47c-289">Casella hello per **eseguire migrazioni Code First (esecuzione all'avvio dell'applicazione)**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-289">Check hello box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="8c47c-290">Fare clic su **Avanti** e quindi su **Anteprima**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="8c47c-291">Visual Studio visualizza un elenco di file hello che verranno aggiunti o aggiornati.</span><span class="sxs-lookup"><span data-stu-id="8c47c-291">Visual Studio displays a list of hello files that will be added or updated.</span></span>
6. <span data-ttu-id="8c47c-292">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="8c47c-292">Click **Publish**.</span></span>
   <span data-ttu-id="8c47c-293">Al termine della distribuzione di hello, browser hello apre toohello home page dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-293">After hello deployment completes, hello browser opens toohello home page of hello application.</span></span>
   
    ![Pagina di indice senza contatti][intro001]
   
    <span data-ttu-id="8c47c-295">Visual Studio Hello pubblicare stringa di connessione hello processo configurato automaticamente in hello distribuito *Web. config* database SQL toohello toopoint del file.</span><span class="sxs-lookup"><span data-stu-id="8c47c-295">hello Visual Studio publish process automatically configured hello connection string in hello deployed *Web.config* file toopoint toohello SQL database.</span></span> <span data-ttu-id="8c47c-296">È anche possibile configurarlo migrazioni Code First tooautomatically hello aggiornamento database toohello versione più recente hello prima hello applicazione accede a database hello dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8c47c-296">It also configured Code First Migrations tooautomatically upgrade hello database toohello latest version hello first time hello application accesses hello database after deployment.</span></span>
   
    <span data-ttu-id="8c47c-297">In seguito a questa configurazione, il primo codice creato hello database eseguendo il codice hello in hello **iniziale** classe creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8c47c-297">As a result of this configuration, Code First created hello database by running hello code in hello **Initial** class that you created earlier.</span></span> <span data-ttu-id="8c47c-298">Era hello prima ora hello tentato tooaccess hello database dell'applicazione dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8c47c-298">It did this hello first time hello application tried tooaccess hello database after deployment.</span></span>
7. <span data-ttu-id="8c47c-299">Quando è stato eseguito localmente, app hello tooverify che ha avuto esito positivo di distribuzione del database, immettere un contatto.</span><span class="sxs-lookup"><span data-stu-id="8c47c-299">Enter a contact as you did when you ran hello app locally, tooverify that database deployment succeeded.</span></span>

<span data-ttu-id="8c47c-300">Quando viene visualizzata tale elemento hello che immesso viene salvato e visualizzato nella pagina di gestione contatto hello, si sa che è stato archiviato nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-300">When you see that hello item you enter is saved and appears on hello contact manager page, you know that it has been stored in hello database.</span></span>

![Pagina di indice con contatti][addwebapi004]

<span data-ttu-id="8c47c-302">un'applicazione Hello è in esecuzione nel cloud hello, utilizzando il Database SQL toostore i dati.</span><span class="sxs-lookup"><span data-stu-id="8c47c-302">hello application is now running in hello cloud, using SQL Database toostore its data.</span></span> <span data-ttu-id="8c47c-303">Dopo aver completato il test di un'applicazione hello in Azure, è necessario eliminarla.</span><span class="sxs-lookup"><span data-stu-id="8c47c-303">After you finish testing hello application in Azure, delete it.</span></span> <span data-ttu-id="8c47c-304">un'applicazione Hello è pubblica e non dispone dell'accesso toolimit un meccanismo.</span><span class="sxs-lookup"><span data-stu-id="8c47c-304">hello application is public and doesn't have a mechanism toolimit access.</span></span>

> [!NOTE]
> <span data-ttu-id="8c47c-305">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="8c47c-305">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8c47c-306">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="8c47c-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8c47c-307">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c47c-307">Next Steps</span></span>
<span data-ttu-id="8c47c-308">Un altro modo toostore dati in un'applicazione Azure sono toouse archiviazione di Azure, che forniscono l'archiviazione dei dati non relazionali in formato hello di BLOB e tabelle.</span><span class="sxs-lookup"><span data-stu-id="8c47c-308">Another way toostore data in an Azure application is toouse Azure storage, which provide non-relational data storage in hello form of blobs and tables.</span></span> <span data-ttu-id="8c47c-309">Hello seguenti collegamenti fornisce informazioni su API Web, ASP.NET MVC e Azure.</span><span class="sxs-lookup"><span data-stu-id="8c47c-309">hello following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="8c47c-310">[Introduzione a Entity Framework con MVC][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="8c47c-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="8c47c-311">Introduzione tooASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="8c47c-311">Intro tooASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="8c47c-312">Creare la prima API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8c47c-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="8c47c-313">Debug di WAWS</span><span class="sxs-lookup"><span data-stu-id="8c47c-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="8c47c-314">Questa applicazione di esempio di esercitazione e hello è stato scritto dal [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) con l'assistenza da Tom Dykstra e Barry Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="8c47c-314">This tutorial and hello sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="8c47c-315">Lasciare commenti e suggerimenti su cosa piace o ciò che si vuole toosee migliorata, non solo informazioni sull'esercitazione hello stesso, ma anche sui prodotti hello che viene illustrato come.</span><span class="sxs-lookup"><span data-stu-id="8c47c-315">Please leave feedback on what you liked or what you would like toosee improved, not only about hello tutorial itself but also about hello products that it demonstrates.</span></span> <span data-ttu-id="8c47c-316">I commenti e suggerimenti saranno utili per definire la priorità dei miglioramenti da apportare.</span><span class="sxs-lookup"><span data-stu-id="8c47c-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="8c47c-317">Siamo interessati soprattutto individuare il quanta interesse esiste in più di automazione per il processo di hello di configurazione e distribuzione di database delle appartenenze hello.</span><span class="sxs-lookup"><span data-stu-id="8c47c-317">We are especially interested in finding out how much interest there is in more automation for hello process of configuring and deploying hello membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="8c47c-318">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="8c47c-318">What's changed</span></span>
* <span data-ttu-id="8c47c-319">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="8c47c-319">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
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

