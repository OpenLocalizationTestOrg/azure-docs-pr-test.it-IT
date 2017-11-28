---
title: aaaGet avviato con un esempio
description: Power BI incorporato, utilizzare il SDK tooadd report interattivi di Power BI in un'applicazione di business intelligence
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: d8a9ef78-ad4e-4bc7-9711-89172dc5c548
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/02/2017
ms.author: asaxton
ms.openlocfilehash: 1fef9dd8e0f734b748b930d3f85ad4b517d9661e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="51bda-103">Introduzione all'esempio di Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="51bda-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="51bda-104">**Microsoft Power BI Embedded**consente di integrare i report di Power BI direttamente nelle applicazioni Web o per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="51bda-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="51bda-105">In questo articolo verranno introdotti è toohello **Power BI Embedded** get di esempio avviata.</span><span class="sxs-lookup"><span data-stu-id="51bda-105">In this article, we'll introduce you toohello **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="51bda-106">Prima di continuare, è opportuno hello toosave seguenti risorse.</span><span class="sxs-lookup"><span data-stu-id="51bda-106">Before we go any further, you'll probably want toosave hello following resources.</span></span> <span data-ttu-id="51bda-107">Verrà consentono per l'integrazione di report di Power BI in app di esempio hello e la propria App troppo.</span><span class="sxs-lookup"><span data-stu-id="51bda-107">They'll help you when integrating Power BI reports into hello sample app and your own apps too.</span></span>

* [<span data-ttu-id="51bda-108">App Web di esempio per l'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="51bda-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="51bda-109">Riferimento all'API di Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="51bda-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="51bda-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (disponibile tramite NuGet)</span><span class="sxs-lookup"><span data-stu-id="51bda-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="51bda-111">Esempio per incorporare il report di JavaScript</span><span class="sxs-lookup"><span data-stu-id="51bda-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="51bda-112">Prima di è possibile configurare e l'esecuzione hello ottenere Power BI Embedded avvio esempio, è necessario toocreate almeno **dell'area di lavoro raccolta** nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="51bda-112">Before you can configure and run hello Power BI Embedded get started sample, you need toocreate at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="51bda-113">toolearn come toocreate un **dell'area di lavoro raccolta** nel portale di Azure hello vedere [Introduzione a Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="51bda-113">toolearn how toocreate a **Workspace Collection** in hello Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-hello-sample-app"></a><span data-ttu-id="51bda-114">Configurare l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="51bda-114">Configure hello sample app</span></span>

<span data-ttu-id="51bda-115">Si analizzerà l'impostazione di Visual Studio development ambiente tooaccess hello componenti necessari toorun hello esempio app.</span><span class="sxs-lookup"><span data-stu-id="51bda-115">Let's walk through setting up your Visual Studio development environment tooaccess hello  components needed toorun hello sample app.</span></span>

1. <span data-ttu-id="51bda-116">Scaricare e decomprimere hello [Power BI Embedded - integrare un report in un'app web](http://go.microsoft.com/fwlink/?LinkId=761493) sample su GitHub.</span><span class="sxs-lookup"><span data-stu-id="51bda-116">Download and unzip hello [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="51bda-117">Aprire il file **PowerBI embedded.sln** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="51bda-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="51bda-118">Potrebbe essere necessario hello tooexecute **pacchetto di aggiornamento** comando hello Console di gestione pacchetti NuGET in pacchetti di hello tooupdate ordine utilizzato in questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="51bda-118">You may need tooexecute hello **Update-Package** command in hello NuGET Package Manager Console in order tooupdate hello packages used in this solution.</span></span>
3. <span data-ttu-id="51bda-119">Compilare la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="51bda-119">Build hello solution.</span></span>
4. <span data-ttu-id="51bda-120">Eseguire hello **ProvisionSample** applicazione console.</span><span class="sxs-lookup"><span data-stu-id="51bda-120">Run hello **ProvisionSample** console app.</span></span> <span data-ttu-id="51bda-121">Nell'applicazione console di esempio hello, eseguire il provisioning di un'area di lavoro e importare un file PBIX.</span><span class="sxs-lookup"><span data-stu-id="51bda-121">In hello sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="51bda-122">tooprovision un nuovo **dell'area di lavoro**, selezionare l'opzione 1, **gestione raccolta**, quindi selezionare l'opzione 6, **il provisioning di una nuova area di lavoro**</span><span class="sxs-lookup"><span data-stu-id="51bda-122">tooprovision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="51bda-123">tooimport un nuovo **Report**, selezionare l'opzione 2, **Report gestione**, quindi selezionare l'opzione 3, **file di importazione PBIX Desktop in un'area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="51bda-123">tooimport a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="51bda-124">Immettere il **nome della raccolta di aree di lavoro** e la **chiave di accesso**.</span><span class="sxs-lookup"><span data-stu-id="51bda-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="51bda-125">È possibile ottenere questi in hello **portale Azure**.</span><span class="sxs-lookup"><span data-stu-id="51bda-125">You can get these in hello **Azure Portal**.</span></span> <span data-ttu-id="51bda-126">toolearn altre informazioni su come tooget il **chiave di accesso**, vedere [Visualizza chiavi di accesso API di Power BI](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Introduzione a Microsoft Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="51bda-126">toolearn more about how tooget your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="51bda-127">Copiare e salvare hello appena creato **ID area di lavoro** toouse più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="51bda-127">Copy and save hello newly created **Workspace ID** toouse later in this article.</span></span> <span data-ttu-id="51bda-128">Dopo aver hello **ID area di lavoro** viene creato, sarà possibile trovarlo hello **portale Azure**.</span><span class="sxs-lookup"><span data-stu-id="51bda-128">After hello **Workspace ID** is created, you can find it hello **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="51bda-129">del file in un file PBIX tooimport il **dell'area di lavoro**, selezionare l'opzione **6. Import PBIX Desktop file into an existing workspace**.</span><span class="sxs-lookup"><span data-stu-id="51bda-129">tooimport a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="51bda-130">Se non è un file PBIX file utile, è possibile scaricare hello [PBIX di esempio di analisi delle vendite al dettaglio](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="51bda-130">If you don't have a PBIX file handy, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="51bda-131">Se richiesto, immettere un nome descrittivo per il **set di dati**.</span><span class="sxs-lookup"><span data-stu-id="51bda-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="51bda-132">Verrà visualizzata una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="51bda-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="51bda-133">Se il file PBIX contiene tutte le connessioni DirectQuery, eseguire le stringhe di connessione hello opzione tooupdate 7.</span><span class="sxs-lookup"><span data-stu-id="51bda-133">If your PBIX file contains any direct query connections, run option 7 tooupdate hello connection strings.</span></span>

<span data-ttu-id="51bda-134">A questo punto il report di Power BI in formato PBIX è stato importato nell'**area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="51bda-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="51bda-135">A questo punto, vediamo come hello toorun **Power BI Embedded** ottenere app web di esempio avviata.</span><span class="sxs-lookup"><span data-stu-id="51bda-135">Now, let's look at how toorun hello **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-hello-sample-web-app"></a><span data-ttu-id="51bda-136">Eseguire app web di esempio hello</span><span class="sxs-lookup"><span data-stu-id="51bda-136">Run hello sample web app</span></span>
<span data-ttu-id="51bda-137">esempio di app web Hello è un'applicazione di esempio che il rendering dei report importati i **dell'area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="51bda-137">hello web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="51bda-138">Ecco come tooconfigure hello esempio di app web.</span><span class="sxs-lookup"><span data-stu-id="51bda-138">Here's how tooconfigure hello web app sample.</span></span>

1. <span data-ttu-id="51bda-139">In hello **incorporato PowerBI** soluzione di Visual Studio, destro, fare clic su hello **EmbedSample** applicazione web e scegliere **imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="51bda-139">In hello **PowerBI-embedded** Visual Studio solution, right click hello **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="51bda-140">In **Web. config**, in hello **EmbedSample** applicazione web, modificare hello **appSettings**: **AccessKey**,  **WorkspaceCollection** nome, e **Idareadilavoro**.</span><span class="sxs-lookup"><span data-stu-id="51bda-140">In **web.config**, in hello **EmbedSample** web application, edit hello **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="51bda-141">Eseguire hello **EmbedSample** applicazione web.</span><span class="sxs-lookup"><span data-stu-id="51bda-141">Run hello **EmbedSample** web application.</span></span>

<span data-ttu-id="51bda-142">Dopo aver eseguito hello **EmbedSample** applicazione web, il pannello di navigazione a sinistra di hello deve contenere un **report** menu.</span><span class="sxs-lookup"><span data-stu-id="51bda-142">Once you run hello **EmbedSample** web application, hello left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="51bda-143">report di hello tooview è stato importato, espandere **report**, fare clic su un report.</span><span class="sxs-lookup"><span data-stu-id="51bda-143">tooview hello report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="51bda-144">Se è stata importata hello [PBIX di esempio di analisi delle vendite al dettaglio](http://go.microsoft.com/fwlink/?LinkID=780547), app web di esempio hello è analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="51bda-144">If you imported hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="51bda-145">Dopo aver selezionato un report, hello **EmbedSample** applicazione web dovrebbe apparire questo:</span><span class="sxs-lookup"><span data-stu-id="51bda-145">After you click a report, hello **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a><span data-ttu-id="51bda-146">Esplorare il codice di esempio hello</span><span class="sxs-lookup"><span data-stu-id="51bda-146">Explore hello sample code</span></span>

<span data-ttu-id="51bda-147">Hello **Microsoft Power BI Embedded** esempio è un'app web di esempio che illustra come toointegrate **Power BI** report nell'app.</span><span class="sxs-lookup"><span data-stu-id="51bda-147">hello **Microsoft Power BI Embedded** sample is an example web app that shows you how toointegrate **Power BI** reports into your app.</span></span> <span data-ttu-id="51bda-148">Model-View-Controller (MVC) usa le procedure consigliate toodemonstrate modello di progettazione.</span><span class="sxs-lookup"><span data-stu-id="51bda-148">It uses a Model-View-Controller (MVC) design pattern toodemonstrate best practices.</span></span> <span data-ttu-id="51bda-149">In questa sezione evidenzia le parti del codice di esempio hello che è possibile esplorare all'interno di hello **incorporato PowerBI** soluzione dell'app web.</span><span class="sxs-lookup"><span data-stu-id="51bda-149">This section highlights parts of hello sample code that you can explore within hello **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="51bda-150">modello Model-View-Controller (MVC) Hello separa la modellazione hello di dominio di hello, presentazione hello e azioni hello basate sull'input dell'utente in tre classi separate: modello, visualizzazione e controllo.</span><span class="sxs-lookup"><span data-stu-id="51bda-150">hello Model-View-Controller (MVC) pattern separates hello modeling of hello domain, hello presentation, and hello actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="51bda-151">toolearn ulteriori informazioni su MVC, vedere [informazioni su ASP.NET](http://www.asp.net/mvc).</span><span class="sxs-lookup"><span data-stu-id="51bda-151">toolearn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="51bda-152">Hello **Microsoft Power BI Embedded** codice di esempio è separato come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="51bda-152">hello **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="51bda-153">Ogni sezione include il nome di file hello nella soluzione di Power BI embedded.sln hello in modo che è possibile trovare codice hello: esempio hello.</span><span class="sxs-lookup"><span data-stu-id="51bda-153">Each section includes hello file name in hello PowerBI-embedded.sln solution so that you can easily find hello code in hello sample.</span></span>

> [!NOTE]
> <span data-ttu-id="51bda-154">In questa sezione è riportato un riepilogo hello del codice di esempio che illustra il modo in cui è stato scritto codice di hello.</span><span class="sxs-lookup"><span data-stu-id="51bda-154">This section is a summary of hello sample code that shows how hello code was written.</span></span> <span data-ttu-id="51bda-155">hello tooview completo di esempio, caricare la soluzione hello embedded.sln di Power BI in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="51bda-155">tooview hello complete sample, please load hello PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="51bda-156">Modello</span><span class="sxs-lookup"><span data-stu-id="51bda-156">Model</span></span>

<span data-ttu-id="51bda-157">esempio Hello ha un **ReportsViewModel** e **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="51bda-157">hello sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="51bda-158">**ReportsViewModel.cs**: rappresenta i report di Power BI.</span><span class="sxs-lookup"><span data-stu-id="51bda-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="51bda-159">**ReportViewModel.cs**: rappresenta un report di Power BI.</span><span class="sxs-lookup"><span data-stu-id="51bda-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="51bda-160">Stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="51bda-160">Connection string</span></span>

<span data-ttu-id="51bda-161">stringa di connessione Hello deve essere nel seguente formato hello:</span><span class="sxs-lookup"><span data-stu-id="51bda-161">hello connection string must be in hello following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="51bda-162">L'uso di attributi comuni di server e database avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="51bda-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="51bda-163">Ad esempio: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="51bda-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="51bda-164">Visualizza</span><span class="sxs-lookup"><span data-stu-id="51bda-164">View</span></span>

<span data-ttu-id="51bda-165">Hello **vista** gestisce visualizzazione hello di Power BI **report** di Power BI e **Report**.</span><span class="sxs-lookup"><span data-stu-id="51bda-165">hello **View** manages hello display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="51bda-166">**Reports.cshtml**: eseguire l'iterazione su **Model.Reports** toocreate un **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="51bda-166">**Reports.cshtml**: Iterate over **Model.Reports** toocreate an **ActionLink**.</span></span> <span data-ttu-id="51bda-167">Hello **ActionLink** è composta da come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="51bda-167">hello **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="51bda-168">Parte:</span><span class="sxs-lookup"><span data-stu-id="51bda-168">Part</span></span> | <span data-ttu-id="51bda-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="51bda-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="51bda-170">Titolo</span><span class="sxs-lookup"><span data-stu-id="51bda-170">Title</span></span> |<span data-ttu-id="51bda-171">Nome del Report hello.</span><span class="sxs-lookup"><span data-stu-id="51bda-171">Name of hello Report.</span></span> |
| <span data-ttu-id="51bda-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="51bda-172">QueryString</span></span> |<span data-ttu-id="51bda-173">Toohello un collegamento ID del Report.</span><span class="sxs-lookup"><span data-stu-id="51bda-173">A link toohello Report ID.</span></span> |

    <div id="reports-nav" class="panel-collapse collapse">
        <div class="panel-body">
            <ul class="nav navbar-nav">
                @foreach (var report in Model.Reports)
                {
                    var reportClass = Request.QueryString["reportId"] == report.Id ? "active" : "";
                    <li class="@reportClass">
                        @Html.ActionLink(report.Name, "Report", new { reportId = report.Id })
                    </li>
                }
            </ul>
        </div>
    </div>

<span data-ttu-id="51bda-174">Report.cshtml: Impostare hello **Model.AccessToken**, e l'espressione Lambda per hello **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="51bda-174">Report.cshtml: Set hello **Model.AccessToken**, and hello Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="51bda-175">Controller</span><span class="sxs-lookup"><span data-stu-id="51bda-175">Controller</span></span>

<span data-ttu-id="51bda-176">**DashboardController.cs**: crea un'istanza di PowerBIClient per il passaggio di un **token dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="51bda-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="51bda-177">Viene generato un JSON Web Token JWT () da hello **chiave per la firma** tooget hello **credenziali**.</span><span class="sxs-lookup"><span data-stu-id="51bda-177">A JSON Web Token (JWT) is generated from hello **Signing Key** tooget hello **Credentials**.</span></span> <span data-ttu-id="51bda-178">Hello **credenziali** è toocreate utilizzata un'istanza di **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="51bda-178">hello **Credentials** are used toocreate an instance of **PowerBIClient**.</span></span> <span data-ttu-id="51bda-179">Dopo aver creato un'istanza di **PowerBIClient**, è possibile chiamare i metodi GetReports() e GetReportsAsync().</span><span class="sxs-lookup"><span data-stu-id="51bda-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="51bda-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="51bda-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="51bda-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="51bda-181">ActionResult Reports()</span></span>

    public ActionResult Reports()
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = client.Reports.GetReports(this.workspaceCollection, this.workspaceId);

            var viewModel = new ReportsViewModel
            {
                Reports = reportsResponse.Value.ToList()
            };

            return PartialView(viewModel);
        }
    }


<span data-ttu-id="51bda-182">Task<ActionResult> Report(string reportId)</span><span class="sxs-lookup"><span data-stu-id="51bda-182">Task<ActionResult> Report(string reportId)</span></span>

    public async Task<ActionResult> Report(string reportId)
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = await client.Reports.GetReportsAsync(this.workspaceCollection, this.workspaceId);
            var report = reportsResponse.Value.FirstOrDefault(r => r.Id == reportId);
            var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

            var viewModel = new ReportViewModel
            {
                Report = report,
                AccessToken = embedToken.Generate(this.accessKey)
            };

            return View(viewModel);
        }
    }

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="51bda-183">Integrare un report nell'app</span><span class="sxs-lookup"><span data-stu-id="51bda-183">Integrate a report into your app</span></span>

<span data-ttu-id="51bda-184">Dopo aver creato un **Report**, si utilizza un **IFrame** tooembed hello Power BI **Report**.</span><span class="sxs-lookup"><span data-stu-id="51bda-184">Once you have a **Report**, you use an **IFrame** tooembed hello Power BI **Report**.</span></span> <span data-ttu-id="51bda-185">Ecco un frammento di codice da powerbi.js in hello **Microsoft Power BI Embedded** esempio.</span><span class="sxs-lookup"><span data-stu-id="51bda-185">Here is a code snippet from  powerbi.js in hello **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="51bda-186">Filtrare i report incorporati nell'applicazione</span><span class="sxs-lookup"><span data-stu-id="51bda-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="51bda-187">È possibile filtrare un report incorporato tramite una sintassi dell'URL.</span><span class="sxs-lookup"><span data-stu-id="51bda-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="51bda-188">toodo, si aggiunge un **$filter** con parametro della stringa di query un **eq** operatore tooyour iFrame src url con hello filtro specificato.</span><span class="sxs-lookup"><span data-stu-id="51bda-188">toodo this, you add a **$filter** query string parameter with an **eq** operator tooyour iFrame src url with hello filter specified.</span></span> <span data-ttu-id="51bda-189">Di seguito è riportata la sintassi di query filtro hello:</span><span class="sxs-lookup"><span data-stu-id="51bda-189">Here is hello filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="51bda-190">{tableName/fieldName} non può includere spazi o caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="51bda-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="51bda-191">Hello {fieldValue} accetta un singolo valore categorico.</span><span class="sxs-lookup"><span data-stu-id="51bda-191">hello {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="51bda-192">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="51bda-192">See also</span></span>

[<span data-ttu-id="51bda-193">Scenari comuni di Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="51bda-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="51bda-194">Autenticazione e autorizzazione con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="51bda-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="51bda-195">Incorporare un report</span><span class="sxs-lookup"><span data-stu-id="51bda-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="51bda-196">Creare un nuovo report da un set di dati</span><span class="sxs-lookup"><span data-stu-id="51bda-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="51bda-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="51bda-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="51bda-198">Esempio di incorporamento con JavaScript</span><span class="sxs-lookup"><span data-stu-id="51bda-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="51bda-199">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="51bda-199">More questions?</span></span> [<span data-ttu-id="51bda-200">Provare a hello Community di Power BI</span><span class="sxs-lookup"><span data-stu-id="51bda-200">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
