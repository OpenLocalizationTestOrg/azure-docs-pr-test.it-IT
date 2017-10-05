---
title: Esportare in SQL da Azure Application Insights | Documentazione Microsoft
description: Eseguire l'esportazione continua dei dati Application Insights in SQL tramite l'analisi di flusso.
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: d51e80509ffb63cef0d01133a2295d58757d5b1a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-export-to-sql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="e2a30-103">Procedura dettagliata: Eseguire l'esportazione in SQL da Application Insights tramite l'analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="e2a30-103">Walkthrough: Export to SQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="e2a30-104">Questo articolo illustra come spostare i dati di telemetria da [Azure Application Insights][start] in un database SQL di Azure usando l'[esportazione continua][export] e l'[analisi di flusso di Azure](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="e2a30-104">This article shows how to move your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="e2a30-105">L'esportazione continua sposta i dati di telemetria in Archiviazione di Azure in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="e2a30-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="e2a30-106">Gli oggetti JSON verranno analizzati con l'analisi di flusso di Azure e verranno create righe in una tabella di database.</span><span class="sxs-lookup"><span data-stu-id="e2a30-106">We'll parse the JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="e2a30-107">Più in generale, l'esportazione continua consente di eseguire la propria analisi dei dati di telemetria che le app inviano ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e2a30-107">(More generally, Continuous Export is the way to do your own analysis of the telemetry your apps send to Application Insights.</span></span> <span data-ttu-id="e2a30-108">È possibile adattare questo esempio di codice per eseguire altre operazioni con i dati di telemetria esportati, come l’aggregazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="e2a30-108">You could adapt this code sample to do other things with the exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="e2a30-109">Si inizierà dal presupposto che si abbia già l'app che si vuole monitorare.</span><span class="sxs-lookup"><span data-stu-id="e2a30-109">We'll start with the assumption that you already have the app you want to monitor.</span></span>

<span data-ttu-id="e2a30-110">In questo esempio verranno usati i dati relativi alle visualizzazioni pagina, ma gli stessi criteri possono essere estesi facilmente ad altri tipi di dati, ad esempio eccezioni ed eventi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="e2a30-110">In this example, we will be using the page view data, but the same pattern can easily be extended to other data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-to-your-application"></a><span data-ttu-id="e2a30-111">Aggiunta di Application Insights all'applicazione</span><span class="sxs-lookup"><span data-stu-id="e2a30-111">Add Application Insights to your application</span></span>
<span data-ttu-id="e2a30-112">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="e2a30-112">To get started:</span></span>

1. <span data-ttu-id="e2a30-113">[Installare Application Insights per le pagine Web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="e2a30-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="e2a30-114">In questo esempio viene considerata l'elaborazione dei dati di visualizzazione della pagina dai browser client, ma è possibile anche impostare Application Insights per il lato server dell'app [Java](app-insights-java-get-started.md) o [ASP.NET](app-insights-asp-net.md) ed elaborare la richiesta, la dipendenza e altri dati di telemetria del server.</span><span class="sxs-lookup"><span data-stu-id="e2a30-114">(In this example, we'll focus on processing page view data from the client browsers, but you could also set up Application Insights for the server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="e2a30-115">Pubblicare l'app e controllare i dati di telemetria visualizzati nella risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e2a30-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="e2a30-116">Creare l'archivio in Azure</span><span class="sxs-lookup"><span data-stu-id="e2a30-116">Create storage in Azure</span></span>
<span data-ttu-id="e2a30-117">L'esportazione continua invia sempre i dati a un account di Archiviazione di Azure, pertanto è prima necessario creare l'archivio.</span><span class="sxs-lookup"><span data-stu-id="e2a30-117">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="e2a30-118">Creare un account di archiviazione per la sottoscrizione nel [portale di Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="e2a30-118">Create a storage account in your subscription in the [Azure portal][portal].</span></span>
   
    ![Nel portale di Azure scegliere Nuovo, Dati, Archiviazione](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="e2a30-122">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="e2a30-122">Create a container</span></span>
   
    ![Nel nuovo archivio selezionare Contenitori, fare clic sul riquadro Contenitori e quindi su Aggiungi](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="e2a30-124">Copiare la chiave di accesso alle risorse di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e2a30-124">Copy the storage access key</span></span>
   
    <span data-ttu-id="e2a30-125">Sarà presto necessaria per configurare l'input per il servizio di analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="e2a30-125">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![Nella risorsa di archiviazione aprire Impostazioni, Chiavi ed eseguire una copia della chiave di accesso primaria](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="e2a30-127">Avviare l'esportazione continua nell'archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e2a30-127">Start continuous export to Azure storage</span></span>
1. <span data-ttu-id="e2a30-128">Nel portale di Azure passare alla risorsa di Application Insights creata per la propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="e2a30-128">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Scegliere Sfoglia, Application Insights e quindi l'applicazione](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="e2a30-130">Creare un'esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="e2a30-130">Create a continuous export.</span></span>
   
    ![Scegliere Impostazioni, Esportazione continua, Aggiungi](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="e2a30-132">Selezionare l'account di archiviazione creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="e2a30-132">Select the storage account you created earlier:</span></span>

    ![Impostare la destinazione di esportazione](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="e2a30-134">Impostare i tipi di eventi da visualizzare:</span><span class="sxs-lookup"><span data-stu-id="e2a30-134">Set the event types you want to see:</span></span>

    ![Scegliere i tipi di eventi](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="e2a30-136">Lasciare che alcuni dati si accumulino.</span><span class="sxs-lookup"><span data-stu-id="e2a30-136">Let some data accumulate.</span></span> <span data-ttu-id="e2a30-137">Attendere che gli utenti usino l'applicazione per qualche tempo.</span><span class="sxs-lookup"><span data-stu-id="e2a30-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="e2a30-138">Verranno restituiti i dati di telemetria e sarà possibile esaminare i grafici statistici in [Esplora metriche](app-insights-metrics-explorer.md) e i singoli eventi in [Ricerca diagnostica](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="e2a30-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="e2a30-139">I dati verranno inoltre esportati nell'archivio.</span><span class="sxs-lookup"><span data-stu-id="e2a30-139">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="e2a30-140">Esaminare i dati esportati, nel portale (scegliere **Esplora**, selezionare l'account di archiviazione, quindi **Contenitori**) o in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2a30-140">Inspect the exported data, either in the portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="e2a30-141">In Visual Studio, scegliere **Visualizza/Cloud Explorer**e aprire Azure/Archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e2a30-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="e2a30-142">(Se non si dispone di tale opzione del menu, è necessario installare l’SDK di Azure: aprire la finestra di dialogo Nuovo progetto, aprire Visual C#/Cloud/Ottieni Microsoft Azure SDK per .NET).</span><span class="sxs-lookup"><span data-stu-id="e2a30-142">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![In Visual Studio aprire Esplora server, Azure, Archiviazione](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="e2a30-144">Prendere nota della parte comune del nome del percorso, derivata dal nome dell’applicazione e dalla chiave di strumentazione.</span><span class="sxs-lookup"><span data-stu-id="e2a30-144">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="e2a30-145">Gli eventi vengono scritti nei file BLOB in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="e2a30-145">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="e2a30-146">Ogni file può contenere uno o più eventi.</span><span class="sxs-lookup"><span data-stu-id="e2a30-146">Each file may contain one or more events.</span></span> <span data-ttu-id="e2a30-147">A questo punto sarà possibile leggere i dati degli eventi e filtrare i campi preferiti.</span><span class="sxs-lookup"><span data-stu-id="e2a30-147">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="e2a30-148">È possibile eseguire una serie di operazioni sui dati, ma lo scopo di questo articolo è usare l'analisi di flusso per spostare i dati in un database SQL.</span><span class="sxs-lookup"><span data-stu-id="e2a30-148">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to move the data to a SQL database.</span></span> <span data-ttu-id="e2a30-149">Sarà quindi più semplice eseguire molte query interessanti.</span><span class="sxs-lookup"><span data-stu-id="e2a30-149">That will make it easy to run lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="e2a30-150">Creare un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="e2a30-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="e2a30-151">Iniziando di nuovo dalla sottoscrizione nel [portale di Azure][portal], creare il database (e un nuovo server, se necessario) in cui si scriveranno i dati.</span><span class="sxs-lookup"><span data-stu-id="e2a30-151">Once again starting from your subscription in [Azure portal][portal], create the database (and a new server, unless you've already got one) to which you'll write the data.</span></span>

![Nuovo, Dati, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="e2a30-153">Assicurarsi che il server di database consenta di accedere ai servizi di Azure:</span><span class="sxs-lookup"><span data-stu-id="e2a30-153">Make sure that the database server allows access to Azure services:</span></span>

![Sfoglia, Server, il proprio server, Impostazioni, Firewall, Consenti l'accesso a Servizi di Azure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="e2a30-155">Creare una tabella nel database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="e2a30-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="e2a30-156">Connettersi al database creato nella sezione precedente con lo strumento di gestione preferito.</span><span class="sxs-lookup"><span data-stu-id="e2a30-156">Connect to the database created in the previous section with your preferred management tool.</span></span> <span data-ttu-id="e2a30-157">In questa procedura dettagliata verranno usati gli [strumenti di gestione di SQL Server](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="e2a30-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="e2a30-158">Creare una nuova query ed eseguire il codice T-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="e2a30-158">Create a new query, and execute the following T-SQL:</span></span>

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

<span data-ttu-id="e2a30-159">In questo esempio vengono usati i dati delle visualizzazioni pagina.</span><span class="sxs-lookup"><span data-stu-id="e2a30-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="e2a30-160">Per visualizzare gli altri dati disponibili, esaminare l'output JSON e vedere il [modello di dati di esportazione](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="e2a30-160">To see the other data available, inspect your JSON output, and see the [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="e2a30-161">Creare un'istanza di analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="e2a30-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="e2a30-162">Nel [portale di Azure classico](https://manage.windowsazure.com/)selezionare il servizio di analisi di flusso di Azure e creare un nuovo processo di analisi di flusso:</span><span class="sxs-lookup"><span data-stu-id="e2a30-162">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="e2a30-163">Quando viene creato il nuovo processo, espanderne i dettagli:</span><span class="sxs-lookup"><span data-stu-id="e2a30-163">When the new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="e2a30-164">Impostare il percorso BLOB</span><span class="sxs-lookup"><span data-stu-id="e2a30-164">Set blob location</span></span>
<span data-ttu-id="e2a30-165">Impostarlo in modo da accettare l'input dal BLOB di esportazione continua:</span><span class="sxs-lookup"><span data-stu-id="e2a30-165">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="e2a30-166">A questo punto è necessaria la chiave di accesso primaria dell'account di archiviazione, di cui si è preso nota in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e2a30-166">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="e2a30-167">Impostarla come chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e2a30-167">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="e2a30-168">Impostare lo schema prefisso percorso</span><span class="sxs-lookup"><span data-stu-id="e2a30-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="e2a30-169">Assicurarsi di impostare il formato della data su **AAAA-MM-GG** (con i **trattini**).</span><span class="sxs-lookup"><span data-stu-id="e2a30-169">Be sure to set the Date Format to **YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="e2a30-170">Lo schema prefisso percorso specifica il modo in cui l'analisi di flusso trova i file di input nell'archivio.</span><span class="sxs-lookup"><span data-stu-id="e2a30-170">The Path Prefix Pattern specifies how Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="e2a30-171">È necessario configurarlo in modo che corrisponda alla modalità di archiviazione dei dati dell'esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="e2a30-171">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="e2a30-172">Impostarlo come segue:</span><span class="sxs-lookup"><span data-stu-id="e2a30-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="e2a30-173">Esempio:</span><span class="sxs-lookup"><span data-stu-id="e2a30-173">In this example:</span></span>

* <span data-ttu-id="e2a30-174">`webapplication27` è il nome della risorsa di Application Insights, **tutto minuscolo**.</span><span class="sxs-lookup"><span data-stu-id="e2a30-174">`webapplication27` is the name of the Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="e2a30-175">`1234...` è la chiave di strumentazione della risorsa di Application Insights **con i trattini rimossi**.</span><span class="sxs-lookup"><span data-stu-id="e2a30-175">`1234...` is the instrumentation key of the Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="e2a30-176">`PageViews` è il tipo di dati da analizzare.</span><span class="sxs-lookup"><span data-stu-id="e2a30-176">`PageViews` is the type of data we want to analyze.</span></span> <span data-ttu-id="e2a30-177">I tipi disponibili dipendono dal filtro impostato nell'esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="e2a30-177">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="e2a30-178">Esaminare i dati esportati per vedere gli altri tipi disponibili e vedere il [modello di dati di esportazione](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="e2a30-178">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="e2a30-179">`/{date}/{time}` è uno schema scritto letteralmente.</span><span class="sxs-lookup"><span data-stu-id="e2a30-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="e2a30-180">Per ottenere il nome e la chiave di strumentazione (iKey) della risorsa di Application Insights, aprire Essentials nella relativa pagina di panoramica o aprire le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="e2a30-180">To get the name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="e2a30-181">Completare l'installazione iniziale</span><span class="sxs-lookup"><span data-stu-id="e2a30-181">Finish initial setup</span></span>
<span data-ttu-id="e2a30-182">Verificare il formato di serializzazione:</span><span class="sxs-lookup"><span data-stu-id="e2a30-182">Confirm the serialization format:</span></span>

![Confermare e chiudere la procedura guidata](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="e2a30-184">Chiudere la procedura guidata e attendere il completamento dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="e2a30-184">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="e2a30-185">Utilizzare la funzione di esempio per verificare di aver impostato correttamente il percorso di input.</span><span class="sxs-lookup"><span data-stu-id="e2a30-185">Use the Sample function to check that you have set the input path correctly.</span></span> <span data-ttu-id="e2a30-186">In caso di errore: verificare che ci siano dati nell’archiviazione per l’intervallo di tempo esemplificativo che si seleziona.</span><span class="sxs-lookup"><span data-stu-id="e2a30-186">If it fails: Check that there is data in the storage for the sample time range you chose.</span></span> <span data-ttu-id="e2a30-187">Modificare la definizione di input e controllare di impostare l'account di archiviazione, il prefisso del percorso e il formato di data corretto.</span><span class="sxs-lookup"><span data-stu-id="e2a30-187">Edit the input definition and check you set the storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="e2a30-188">Impostare la query</span><span class="sxs-lookup"><span data-stu-id="e2a30-188">Set query</span></span>
<span data-ttu-id="e2a30-189">Aprire la sezione delle query:</span><span class="sxs-lookup"><span data-stu-id="e2a30-189">Open the query section:</span></span>

![In Analisi di flusso selezionare Query](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="e2a30-191">Sostituire la query predefinita con:</span><span class="sxs-lookup"><span data-stu-id="e2a30-191">Replace the default query with:</span></span>

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

<span data-ttu-id="e2a30-192">Tenere presente che le prime proprietà sono specifiche dei dati relativi alle visualizzazioni pagina.</span><span class="sxs-lookup"><span data-stu-id="e2a30-192">Notice that the first few properties are specific to page view data.</span></span> <span data-ttu-id="e2a30-193">Le esportazioni di altri tipi di dati di telemetria avranno proprietà diverse.</span><span class="sxs-lookup"><span data-stu-id="e2a30-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="e2a30-194">Vedere il [Riferimento dettagliato al modello di dati per i valori e i tipi di proprietà](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="e2a30-194">See the [detailed data model reference for the property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-to-database"></a><span data-ttu-id="e2a30-195">Configurare l'output nel database</span><span class="sxs-lookup"><span data-stu-id="e2a30-195">Set up output to database</span></span>
<span data-ttu-id="e2a30-196">Selezionare SQL come output.</span><span class="sxs-lookup"><span data-stu-id="e2a30-196">Select SQL as the output.</span></span>

![In Analisi di flusso selezionare Output](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="e2a30-198">Specificare il database SQL.</span><span class="sxs-lookup"><span data-stu-id="e2a30-198">Specify the SQL database.</span></span>

![Inserire i dettagli del database](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="e2a30-200">Chiudere la procedura guidata e attendere la notifica di configurazione dell'output.</span><span class="sxs-lookup"><span data-stu-id="e2a30-200">Close the wizard and wait for a notification that the output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="e2a30-201">Avviare l'elaborazione</span><span class="sxs-lookup"><span data-stu-id="e2a30-201">Start processing</span></span>
<span data-ttu-id="e2a30-202">Avviare il processo dalla barra delle azioni:</span><span class="sxs-lookup"><span data-stu-id="e2a30-202">Start the job from the action bar:</span></span>

![In Analisi di flusso fare clic su Avvia.](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="e2a30-204">È possibile scegliere se avviare l'elaborazione dei dati a partire dai dati correnti o se includere i dati precedenti.</span><span class="sxs-lookup"><span data-stu-id="e2a30-204">You can choose whether to start processing the data starting from now, or to start with earlier data.</span></span> <span data-ttu-id="e2a30-205">La seconda opzione è utile se l'esportazione continua è già stata eseguita per un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="e2a30-205">The latter is useful if you have had Continuous Export already running for a while.</span></span>

![In Analisi di flusso fare clic su Avvia.](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="e2a30-207">Dopo alcuni minuti, tornare agli strumenti di gestione di SQL Server e controllare il flusso dei dati.</span><span class="sxs-lookup"><span data-stu-id="e2a30-207">After a few minutes, go back to SQL Server Management Tools and watch the data flowing in.</span></span> <span data-ttu-id="e2a30-208">Usare ad esempio una query simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="e2a30-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="e2a30-209">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="e2a30-209">Related articles</span></span>
* [<span data-ttu-id="e2a30-210">Esportare in PowerBI usando l'analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="e2a30-210">Export to PowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="e2a30-211">Riferimento dettagliato al modello di dati per i valori e i tipi di proprietà.</span><span class="sxs-lookup"><span data-stu-id="e2a30-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="e2a30-212">Esportazione continua in Application Insights</span><span class="sxs-lookup"><span data-stu-id="e2a30-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="e2a30-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="e2a30-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

