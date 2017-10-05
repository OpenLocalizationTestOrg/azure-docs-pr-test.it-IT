---
title: Esempio introduttivo
description: Power BI Embedded - Uso di SDK per aggiungere report di Power BI interattivi nell'applicazione di Business Intelligence
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
ms.openlocfilehash: c3cb1763f807220a4a829f410d7eb77974b25776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="097dd-103">Introduzione all'esempio di Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="097dd-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="097dd-104">**Microsoft Power BI Embedded**consente di integrare i report di Power BI direttamente nelle applicazioni Web o per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="097dd-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="097dd-105">In questo articolo verrà presentato l'esempio introduttivo per **Power BI Embedded** .</span><span class="sxs-lookup"><span data-stu-id="097dd-105">In this article, we'll introduce you to the **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="097dd-106">Prima di continuare, è consigliabile salvare le risorse seguenti,</span><span class="sxs-lookup"><span data-stu-id="097dd-106">Before we go any further, you'll probably want to save the following resources.</span></span> <span data-ttu-id="097dd-107">che risulteranno utili durante l'integrazione dei report di Power BI nell'app di esempio e nelle app personalizzate.</span><span class="sxs-lookup"><span data-stu-id="097dd-107">They'll help you when integrating Power BI reports into the sample app and your own apps too.</span></span>

* [<span data-ttu-id="097dd-108">App Web di esempio per l'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="097dd-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="097dd-109">Riferimento all'API di Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="097dd-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="097dd-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (disponibile tramite NuGet)</span><span class="sxs-lookup"><span data-stu-id="097dd-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="097dd-111">Esempio per incorporare il report di JavaScript</span><span class="sxs-lookup"><span data-stu-id="097dd-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="097dd-112">Prima di poter configurare ed eseguire l'esempio d'introduzione a Power BI Embedded, è necessario creare almeno una **raccolta di aree di lavoro** nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="097dd-112">Before you can configure and run the Power BI Embedded get started sample, you need to create at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="097dd-113">Per informazioni su come creare una **Raccolta di aree di lavoro** nel portale di Azure, vedere [Introduzione a Microsoft Power BI Embedded - Anteprima](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="097dd-113">To learn how to create a **Workspace Collection** in the Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-the-sample-app"></a><span data-ttu-id="097dd-114">Configurare l'app di esempio</span><span class="sxs-lookup"><span data-stu-id="097dd-114">Configure the sample app</span></span>

<span data-ttu-id="097dd-115">La procedura dettagliata seguente illustra la configurazione dell'ambiente di sviluppo di Visual Studio per l'accesso ai componenti necessari per eseguire l'app di esempio.</span><span class="sxs-lookup"><span data-stu-id="097dd-115">Let's walk through setting up your Visual Studio development environment to access the  components needed to run the sample app.</span></span>

1. <span data-ttu-id="097dd-116">Scaricare e decomprimere l'esempio [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="097dd-116">Download and unzip the [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="097dd-117">Aprire il file **PowerBI embedded.sln** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="097dd-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="097dd-118">Potrebbe essere necessario eseguire il comando **Update-Package** nella Console di gestione pacchetti NuGET per aggiornare i pacchetti utilizzati in questa soluzione.</span><span class="sxs-lookup"><span data-stu-id="097dd-118">You may need to execute the **Update-Package** command in the NuGET Package Manager Console in order to update the packages used in this solution.</span></span>
3. <span data-ttu-id="097dd-119">Compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="097dd-119">Build the solution.</span></span>
4. <span data-ttu-id="097dd-120">Eseguire l'applicazione console **ProvisionSample** .</span><span class="sxs-lookup"><span data-stu-id="097dd-120">Run the **ProvisionSample** console app.</span></span> <span data-ttu-id="097dd-121">Nell'applicazione console di esempio, effettuare il provisioning di un'area di lavoro e importare un file PBIX.</span><span class="sxs-lookup"><span data-stu-id="097dd-121">In the sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="097dd-122">Per effettuare il provisioning di una nuova **area di lavoro**, selezionare l'opzione 1 **Collection management** (Gestione raccolte) e quindi selezionare l'opzione 6 **Provision a new Workspace** (Effettua il provisioning di una nuova area di lavoro).</span><span class="sxs-lookup"><span data-stu-id="097dd-122">To provision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="097dd-123">Per importare un nuovo **report**, selezionare l'opzione 2 **Report management** (Gestione report) e quindi selezionare l'opzione 3 **Import PBIX Desktop file into a workspace** (Importa file di PBIX Desktop in un'area di lavoro).</span><span class="sxs-lookup"><span data-stu-id="097dd-123">To import a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="097dd-124">Immettere il **nome della raccolta di aree di lavoro** e la **chiave di accesso**.</span><span class="sxs-lookup"><span data-stu-id="097dd-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="097dd-125">È possibile ottenere questi dati nel **portale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="097dd-125">You can get these in the **Azure Portal**.</span></span> <span data-ttu-id="097dd-126">Per altre informazioni su come ottenere la **Chiave di accesso**, vedere [Visualizzare le chiavi di accesso all'API Power BI](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) nell'introduzione a Microsoft Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="097dd-126">To learn more about how to get your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="097dd-127">Copiare e salvare l' **ID area di lavoro** appena creato per poterlo usare successivamente.</span><span class="sxs-lookup"><span data-stu-id="097dd-127">Copy and save the newly created **Workspace ID** to use later in this article.</span></span> <span data-ttu-id="097dd-128">Dopo aver creato l'**ID area di lavoro**, è possibile trovarlo nel **portale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="097dd-128">After the **Workspace ID** is created, you can find it the **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="097dd-129">Per importare un file PBIX nell'**area di lavoro**, selezionare l'opzione **6. Import PBIX Desktop file into an existing workspace**.</span><span class="sxs-lookup"><span data-stu-id="097dd-129">To import a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="097dd-130">In mancanza di un file PBIX adatto, è possibile scaricare l'esempio [Retail Analysis PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="097dd-130">If you don't have a PBIX file handy, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="097dd-131">Se richiesto, immettere un nome descrittivo per il **set di dati**.</span><span class="sxs-lookup"><span data-stu-id="097dd-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="097dd-132">Verrà visualizzata una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="097dd-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="097dd-133">Se il file PBIX contiene connessioni tramite query diretta, eseguire l'opzione 7 per aggiornare le stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="097dd-133">If your PBIX file contains any direct query connections, run option 7 to update the connection strings.</span></span>

<span data-ttu-id="097dd-134">A questo punto il report di Power BI in formato PBIX è stato importato nell'**area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="097dd-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="097dd-135">Viene ora illustrato come eseguire l'applicazione Web dell'esempio introduttivo di **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="097dd-135">Now, let's look at how to run the **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-the-sample-web-app"></a><span data-ttu-id="097dd-136">Eseguire l'app Web di esempio</span><span class="sxs-lookup"><span data-stu-id="097dd-136">Run the sample web app</span></span>
<span data-ttu-id="097dd-137">L'app Web di esempio è un'applicazione di esempio che esegue il rendering dei report importati nell'**area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="097dd-137">The web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="097dd-138">Di seguito viene spiegato come configurare l'app Web di esempio.</span><span class="sxs-lookup"><span data-stu-id="097dd-138">Here's how to configure the web app sample.</span></span>

1. <span data-ttu-id="097dd-139">Nella soluzione **PowerBI Embedded** in Visual Studio fare clic con il pulsante destro del mouse sull'applicazione Web **EmbedSample** e scegliere **Imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="097dd-139">In the **PowerBI-embedded** Visual Studio solution, right click the **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="097dd-140">In **web.config**, nell'applicazione Web **EmbedSample** modificare il nome **appSettings**: **AccessKey**, **WorkspaceCollection** e **WorkspaceId**.</span><span class="sxs-lookup"><span data-stu-id="097dd-140">In **web.config**, in the **EmbedSample** web application, edit the **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="097dd-141">Eseguire l'applicazione Web **EmbedSample**.</span><span class="sxs-lookup"><span data-stu-id="097dd-141">Run the **EmbedSample** web application.</span></span>

<span data-ttu-id="097dd-142">Dopo aver eseguito l'applicazione Web **EmbedSample**, il pannello di spostamento a sinistra conterrà un menu **Reports** (Report).</span><span class="sxs-lookup"><span data-stu-id="097dd-142">Once you run the **EmbedSample** web application, the left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="097dd-143">Per visualizzare il report che è stato importato, espandere il menu **Reports** (Report) e fare clic su un report.</span><span class="sxs-lookup"><span data-stu-id="097dd-143">To view the report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="097dd-144">Se è stato importato l'[esempio Analyzing Sales Data PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), l'applicazione Web sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="097dd-144">If you imported the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="097dd-145">Dopo aver selezionato un report, l'applicazione Web **EmbedSample** sarà simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="097dd-145">After you click a report, the **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-the-sample-code"></a><span data-ttu-id="097dd-146">Esplorare il codice di esempio</span><span class="sxs-lookup"><span data-stu-id="097dd-146">Explore the sample code</span></span>

<span data-ttu-id="097dd-147">L'esempio di **Microsoft Power BI Embedded** è un'app Web che illustra come integrare report di **Power BI** nella propria app.</span><span class="sxs-lookup"><span data-stu-id="097dd-147">The **Microsoft Power BI Embedded** sample is an example web app that shows you how to integrate **Power BI** reports into your app.</span></span> <span data-ttu-id="097dd-148">Usa un modello di progettazione MVC (Model-View-Controller) per illustrare le procedure consigliate.</span><span class="sxs-lookup"><span data-stu-id="097dd-148">It uses a Model-View-Controller (MVC) design pattern to demonstrate best practices.</span></span> <span data-ttu-id="097dd-149">Questa sezione evidenzia parti del codice di esempio che è possibile esplorare nella soluzione di applicazione Web di **PowerBI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="097dd-149">This section highlights parts of the sample code that you can explore within the **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="097dd-150">Il modello MVC separa la modellazione del dominio, la presentazione e le azioni in base all'input dell'utente in tre classi distinte, ovvero modellazione, visualizzazione e controller.</span><span class="sxs-lookup"><span data-stu-id="097dd-150">The Model-View-Controller (MVC) pattern separates the modeling of the domain, the presentation, and the actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="097dd-151">Per altre informazioni sul modello MVC, vedere [Learn About ASP.NET](http://www.asp.net/mvc) (Informazioni su ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="097dd-151">To learn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="097dd-152">Il codice di esempio di **Microsoft Power BI Embedded** è suddiviso come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="097dd-152">The **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="097dd-153">Ogni sezione contiene il nome del file nella soluzione PowerBI-embedded.sln in modo che sia possibile trovare facilmente il codice nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="097dd-153">Each section includes the file name in the PowerBI-embedded.sln solution so that you can easily find the code in the sample.</span></span>

> [!NOTE]
> <span data-ttu-id="097dd-154">Questa sezione è un riepilogo del codice di esempio e illustra in che modo è stato scritto.</span><span class="sxs-lookup"><span data-stu-id="097dd-154">This section is a summary of the sample code that shows how the code was written.</span></span> <span data-ttu-id="097dd-155">Per visualizzare l'esempio completo, caricare la soluzione PowerBI-embedded.sln in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="097dd-155">To view the complete sample, please load the PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="097dd-156">Modello</span><span class="sxs-lookup"><span data-stu-id="097dd-156">Model</span></span>

<span data-ttu-id="097dd-157">L'esempio è composto da **ReportsViewModel** e **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="097dd-157">The sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="097dd-158">**ReportsViewModel.cs**: rappresenta i report di Power BI.</span><span class="sxs-lookup"><span data-stu-id="097dd-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="097dd-159">**ReportViewModel.cs**: rappresenta un report di Power BI.</span><span class="sxs-lookup"><span data-stu-id="097dd-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="097dd-160">Stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="097dd-160">Connection string</span></span>

<span data-ttu-id="097dd-161">La stringa di connessione deve essere nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="097dd-161">The connection string must be in the following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="097dd-162">L'uso di attributi comuni di server e database avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="097dd-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="097dd-163">Ad esempio: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="097dd-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="097dd-164">Visualizza</span><span class="sxs-lookup"><span data-stu-id="097dd-164">View</span></span>

<span data-ttu-id="097dd-165">**Visualizza** gestisce la visualizzazione di più **report** di Power BI e di un **report** di Power BI.</span><span class="sxs-lookup"><span data-stu-id="097dd-165">The **View** manages the display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="097dd-166">**Reports.cshtml**: esegue l'iterazione di **Model.Reports** per creare un elemento **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="097dd-166">**Reports.cshtml**: Iterate over **Model.Reports** to create an **ActionLink**.</span></span> <span data-ttu-id="097dd-167">L'elemento **ActionLink** è costituito da:</span><span class="sxs-lookup"><span data-stu-id="097dd-167">The **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="097dd-168">Parte:</span><span class="sxs-lookup"><span data-stu-id="097dd-168">Part</span></span> | <span data-ttu-id="097dd-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="097dd-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="097dd-170">Titolo</span><span class="sxs-lookup"><span data-stu-id="097dd-170">Title</span></span> |<span data-ttu-id="097dd-171">Nome del report.</span><span class="sxs-lookup"><span data-stu-id="097dd-171">Name of the Report.</span></span> |
| <span data-ttu-id="097dd-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="097dd-172">QueryString</span></span> |<span data-ttu-id="097dd-173">Collegamento al l'ID report.</span><span class="sxs-lookup"><span data-stu-id="097dd-173">A link to the Report ID.</span></span> |

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

<span data-ttu-id="097dd-174">Report.cshtml: imposta **Model.AccessToken** e l'espressione Lambda per **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="097dd-174">Report.cshtml: Set the **Model.AccessToken**, and the Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="097dd-175">Controller</span><span class="sxs-lookup"><span data-stu-id="097dd-175">Controller</span></span>

<span data-ttu-id="097dd-176">**DashboardController.cs**: crea un'istanza di PowerBIClient per il passaggio di un **token dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="097dd-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="097dd-177">Dalla **Chiave di firma** viene generato un token JSON Web (JWT) per ottenere le **Credenziali**.</span><span class="sxs-lookup"><span data-stu-id="097dd-177">A JSON Web Token (JWT) is generated from the **Signing Key** to get the **Credentials**.</span></span> <span data-ttu-id="097dd-178">Le **Credenziali** servono per creare un'istanza di **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="097dd-178">The **Credentials** are used to create an instance of **PowerBIClient**.</span></span> <span data-ttu-id="097dd-179">Dopo aver creato un'istanza di **PowerBIClient**, è possibile chiamare i metodi GetReports() e GetReportsAsync().</span><span class="sxs-lookup"><span data-stu-id="097dd-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="097dd-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="097dd-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="097dd-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="097dd-181">ActionResult Reports()</span></span>

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


<span data-ttu-id="097dd-182">Task<ActionResult> Report(string reportId)</span><span class="sxs-lookup"><span data-stu-id="097dd-182">Task<ActionResult> Report(string reportId)</span></span>

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

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="097dd-183">Integrare un report nell'app</span><span class="sxs-lookup"><span data-stu-id="097dd-183">Integrate a report into your app</span></span>

<span data-ttu-id="097dd-184">Dopo aver creato un **report**, usare un **iFrame** per incorporare il **report** di Power BI.</span><span class="sxs-lookup"><span data-stu-id="097dd-184">Once you have a **Report**, you use an **IFrame** to embed the Power BI **Report**.</span></span> <span data-ttu-id="097dd-185">Ecco un frammento di codice da powerbi.js nell'esempio di **Microsoft Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="097dd-185">Here is a code snippet from  powerbi.js in the **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="097dd-186">Filtrare i report incorporati nell'applicazione</span><span class="sxs-lookup"><span data-stu-id="097dd-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="097dd-187">È possibile filtrare un report incorporato tramite una sintassi dell'URL.</span><span class="sxs-lookup"><span data-stu-id="097dd-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="097dd-188">A questo scopo aggiungere un parametro della stringa di query **$filter** con un operatore **eq** all'URL iFrame src specificando il filtro.</span><span class="sxs-lookup"><span data-stu-id="097dd-188">To do this, you add a **$filter** query string parameter with an **eq** operator to your iFrame src url with the filter specified.</span></span> <span data-ttu-id="097dd-189">Di seguito è riportata la sintassi della query del filtro:</span><span class="sxs-lookup"><span data-stu-id="097dd-189">Here is the filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="097dd-190">{tableName/fieldName} non può includere spazi o caratteri speciali.</span><span class="sxs-lookup"><span data-stu-id="097dd-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="097dd-191">{fieldValue} accetta un singolo valore categorico.</span><span class="sxs-lookup"><span data-stu-id="097dd-191">The {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="097dd-192">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="097dd-192">See also</span></span>

[<span data-ttu-id="097dd-193">Scenari comuni di Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="097dd-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="097dd-194">Autenticazione e autorizzazione con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="097dd-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="097dd-195">Incorporare un report</span><span class="sxs-lookup"><span data-stu-id="097dd-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="097dd-196">Creare un nuovo report da un set di dati</span><span class="sxs-lookup"><span data-stu-id="097dd-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="097dd-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="097dd-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="097dd-198">Esempio di incorporamento con JavaScript</span><span class="sxs-lookup"><span data-stu-id="097dd-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="097dd-199">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="097dd-199">More questions?</span></span> [<span data-ttu-id="097dd-200">Contattare la community di Power BI</span><span class="sxs-lookup"><span data-stu-id="097dd-200">Try the Power BI Community</span></span>](http://community.powerbi.com/)
