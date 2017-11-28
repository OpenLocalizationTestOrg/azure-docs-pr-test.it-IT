---
title: Esportare tooSQL da Azure Application Insights | Documenti Microsoft
description: Esportare in modo continuo tooSQL di dati di Application Insights con flusso Analitica.
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
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="3db32-103">Procedura dettagliata: Esportare tooSQL da Application Insights con flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="3db32-103">Walkthrough: Export tooSQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="3db32-104">Questo articolo viene illustrato come toomove i dati di telemetria da [Azure Application Insights] [ start] in un database SQL di Azure tramite [esportazione continua] [ export] e [Analitica di flusso di Azure](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="3db32-104">This article shows how toomove your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="3db32-105">L'esportazione continua sposta i dati di telemetria in Archiviazione di Azure in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="3db32-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="3db32-106">Viene l'analisi degli oggetti JSON hello utilizzando Azure flusso Analitica e creare le righe in una tabella di database.</span><span class="sxs-lookup"><span data-stu-id="3db32-106">We'll parse hello JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="3db32-107">(Più in generale, l'esportazione continua è hello modo toodo la propria analisi dei dati di telemetria hello App Insights tooApplication di trasmissione.</span><span class="sxs-lookup"><span data-stu-id="3db32-107">(More generally, Continuous Export is hello way toodo your own analysis of hello telemetry your apps send tooApplication Insights.</span></span> <span data-ttu-id="3db32-108">È possibile adattare questa toodo di esempio di codice altre operazioni con i dati di telemetria hello esportata, ad esempio aggregazione dei dati.)</span><span class="sxs-lookup"><span data-stu-id="3db32-108">You could adapt this code sample toodo other things with hello exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="3db32-109">Si inizierà con il presupposto hello che si disponga già di app hello da toomonitor.</span><span class="sxs-lookup"><span data-stu-id="3db32-109">We'll start with hello assumption that you already have hello app you want toomonitor.</span></span>

<span data-ttu-id="3db32-110">In questo esempio, si utilizzerà dati della visualizzazione pagina hello, ma hello stesso modello può essere estesa facilmente tooother i tipi di dati, ad esempio gli eventi personalizzati e le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="3db32-110">In this example, we will be using hello page view data, but hello same pattern can easily be extended tooother data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-tooyour-application"></a><span data-ttu-id="3db32-111">Aggiungere l'applicazione tooyour Application Insights</span><span class="sxs-lookup"><span data-stu-id="3db32-111">Add Application Insights tooyour application</span></span>
<span data-ttu-id="3db32-112">tooget avviato:</span><span class="sxs-lookup"><span data-stu-id="3db32-112">tooget started:</span></span>

1. <span data-ttu-id="3db32-113">[Installare Application Insights per le pagine Web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="3db32-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="3db32-114">(In questo esempio sarà dedicata all'elaborazione di dati della visualizzazione pagina dal browser client hello, ma è anche possibile configurare Application Insights per hello sul lato server il [Java](app-insights-java-get-started.md) o [ASP.NET](app-insights-asp-net.md) app e processo di richiesta dipendenze e altri dati di telemetria di server.)</span><span class="sxs-lookup"><span data-stu-id="3db32-114">(In this example, we'll focus on processing page view data from hello client browsers, but you could also set up Application Insights for hello server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="3db32-115">Pubblicare l'app e controllare i dati di telemetria visualizzati nella risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3db32-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="3db32-116">Creare l'archivio in Azure</span><span class="sxs-lookup"><span data-stu-id="3db32-116">Create storage in Azure</span></span>
<span data-ttu-id="3db32-117">L'esportazione continua restituisce sempre l'account di archiviazione Azure tooan di dati, pertanto è necessario innanzitutto archiviazione hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="3db32-117">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="3db32-118">Creare un account di archiviazione nella sottoscrizione in hello [portale di Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="3db32-118">Create a storage account in your subscription in hello [Azure portal][portal].</span></span>
   
    ![Nel portale di Azure scegliere Nuovo, Dati, Archiviazione](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="3db32-122">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="3db32-122">Create a container</span></span>
   
    ![In hello nuova risorsa di archiviazione, selezionare i contenitori, fare clic su riquadro contenitori hello, quindi su Aggiungi](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="3db32-124">Chiave di accesso di archiviazione hello copia</span><span class="sxs-lookup"><span data-stu-id="3db32-124">Copy hello storage access key</span></span>
   
    <span data-ttu-id="3db32-125">È necessario prima tooset hello toohello input flusso analitica servizio.</span><span class="sxs-lookup"><span data-stu-id="3db32-125">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![Nel servizio di archiviazione hello, aprire le impostazioni, chiavi e richiedere una copia della chiave di accesso primaria hello](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="3db32-127">Avviare l'esportazione continua tooAzure archiviazione</span><span class="sxs-lookup"><span data-stu-id="3db32-127">Start continuous export tooAzure storage</span></span>
1. <span data-ttu-id="3db32-128">Nel portale di Azure hello, Sfoglia risorsa di Application Insights toohello creata per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3db32-128">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Scegliere Sfoglia, Application Insights e quindi l'applicazione](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="3db32-130">Creare un'esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="3db32-130">Create a continuous export.</span></span>
   
    ![Scegliere Impostazioni, Esportazione continua, Aggiungi](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="3db32-132">Selezionare l'account di archiviazione hello creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="3db32-132">Select hello storage account you created earlier:</span></span>

    ![Set di destinazione dell'esportazione hello](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="3db32-134">Impostare i tipi di evento hello da toosee:</span><span class="sxs-lookup"><span data-stu-id="3db32-134">Set hello event types you want toosee:</span></span>

    ![Scegliere i tipi di eventi](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="3db32-136">Lasciare che alcuni dati si accumulino.</span><span class="sxs-lookup"><span data-stu-id="3db32-136">Let some data accumulate.</span></span> <span data-ttu-id="3db32-137">Attendere che gli utenti usino l'applicazione per qualche tempo.</span><span class="sxs-lookup"><span data-stu-id="3db32-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="3db32-138">Verranno restituiti i dati di telemetria e sarà possibile esaminare i grafici statistici in [Esplora metriche](app-insights-metrics-explorer.md) e i singoli eventi in [Ricerca diagnostica](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="3db32-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="3db32-139">E inoltre dati hello esporterà tooyour archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3db32-139">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="3db32-140">Controllare i dati di hello esportata, nel portale di hello - Scegli **Sfoglia**, selezionare l'account di archiviazione, quindi **contenitori** - o in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3db32-140">Inspect hello exported data, either in hello portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="3db32-141">In Visual Studio, scegliere **Visualizza/Cloud Explorer**e aprire Azure/Archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3db32-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="3db32-142">(Se non si dispone di questa opzione, è necessario tooinstall hello Azure SDK: aprire finestra di dialogo Nuovo progetto hello e Visual c# / Cloud / ottenere Microsoft Azure SDK per .NET.)</span><span class="sxs-lookup"><span data-stu-id="3db32-142">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![In Visual Studio aprire Esplora server, Azure, Archiviazione](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="3db32-144">Prendere nota di parte in comune hello del nome di percorso hello, che viene derivato dalla chiave di nome e la strumentazione dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3db32-144">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="3db32-145">gli eventi di Hello vengono scritti i file tooblob in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="3db32-145">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="3db32-146">Ogni file può contenere uno o più eventi.</span><span class="sxs-lookup"><span data-stu-id="3db32-146">Each file may contain one or more events.</span></span> <span data-ttu-id="3db32-147">In modo desideriamo tooread hello dati dell'evento e filtro campi hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="3db32-147">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="3db32-148">Sono disponibili tutti i tipi di operazioni che è possibile farlo con dati hello, ma il piano è oggi database SQL toouse flusso Analitica toomove hello dati tooa.</span><span class="sxs-lookup"><span data-stu-id="3db32-148">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toomove hello data tooa SQL database.</span></span> <span data-ttu-id="3db32-149">In questo modo sarà facile toorun moltissimi interessanti di query.</span><span class="sxs-lookup"><span data-stu-id="3db32-149">That will make it easy toorun lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="3db32-150">Creare un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="3db32-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="3db32-151">Ancora una volta a partire dalla sottoscrizione in [portale di Azure][portal], creare database hello (e un nuovo server, a meno che non si dispone già uno) toowhich si scriverà dati hello.</span><span class="sxs-lookup"><span data-stu-id="3db32-151">Once again starting from your subscription in [Azure portal][portal], create hello database (and a new server, unless you've already got one) toowhich you'll write hello data.</span></span>

![Nuovo, Dati, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="3db32-153">Verificare che il server di database hello consente l'accesso tooAzure servizi:</span><span class="sxs-lookup"><span data-stu-id="3db32-153">Make sure that hello database server allows access tooAzure services:</span></span>

![Sfoglia, server, il server, le impostazioni, Firewall, consentire l'accesso a tooAzure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="3db32-155">Creare una tabella nel database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="3db32-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="3db32-156">La connessione a database toohello creato nella sezione precedente di hello con lo strumento di gestione preferiti.</span><span class="sxs-lookup"><span data-stu-id="3db32-156">Connect toohello database created in hello previous section with your preferred management tool.</span></span> <span data-ttu-id="3db32-157">In questa procedura dettagliata verranno usati gli [strumenti di gestione di SQL Server](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="3db32-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="3db32-158">Creare una nuova query ed eseguire hello T-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="3db32-158">Create a new query, and execute hello following T-SQL:</span></span>

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

<span data-ttu-id="3db32-159">In questo esempio vengono usati i dati delle visualizzazioni pagina.</span><span class="sxs-lookup"><span data-stu-id="3db32-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="3db32-160">toosee hello altri dati disponibili, esaminare l'output JSON e vedere hello [Esporta modello di dati](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="3db32-160">toosee hello other data available, inspect your JSON output, and see hello [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="3db32-161">Creare un'istanza di analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="3db32-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="3db32-162">Da hello [portale di Azure classico](https://manage.windowsazure.com/), selezionare il servizio di Azure flusso Analitica hello e creare un nuovo processo di flusso Analitica:</span><span class="sxs-lookup"><span data-stu-id="3db32-162">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="3db32-163">Quando viene creato il nuovo processo di hello, espandere i dettagli:</span><span class="sxs-lookup"><span data-stu-id="3db32-163">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="3db32-164">Impostare il percorso BLOB</span><span class="sxs-lookup"><span data-stu-id="3db32-164">Set blob location</span></span>
<span data-ttu-id="3db32-165">Impostarlo input tootake dal blob di esportazione continua:</span><span class="sxs-lookup"><span data-stu-id="3db32-165">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="3db32-166">A questo punto è necessario hello chiave di accesso primaria dall'Account di archiviazione, annotati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3db32-166">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="3db32-167">Impostare come hello chiave Account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3db32-167">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="3db32-168">Impostare lo schema prefisso percorso</span><span class="sxs-lookup"><span data-stu-id="3db32-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="3db32-169">È troppo hello tooset che il formato di data**AAAA-MM-GG** (con **trattini**).</span><span class="sxs-lookup"><span data-stu-id="3db32-169">Be sure tooset hello Date Format too**YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="3db32-170">Hello modello prefisso del percorso specifica come flusso Analitica Trova file di input hello nel servizio di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="3db32-170">hello Path Prefix Pattern specifies how Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="3db32-171">È necessario tooset è toohow toocorrespond esportazione continua archivia dati hello.</span><span class="sxs-lookup"><span data-stu-id="3db32-171">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="3db32-172">Impostarlo come segue:</span><span class="sxs-lookup"><span data-stu-id="3db32-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="3db32-173">Esempio:</span><span class="sxs-lookup"><span data-stu-id="3db32-173">In this example:</span></span>

* <span data-ttu-id="3db32-174">`webapplication27`è il nome di hello della risorsa di Application Insights, hello **tutti in lettere minuscole**.</span><span class="sxs-lookup"><span data-stu-id="3db32-174">`webapplication27` is hello name of hello Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="3db32-175">`1234...`è la chiave di strumentazione hello di hello risorsa di Application Insights **con rimossi trattini**.</span><span class="sxs-lookup"><span data-stu-id="3db32-175">`1234...` is hello instrumentation key of hello Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="3db32-176">`PageViews`hello tipo di dati desiderato tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="3db32-176">`PageViews` is hello type of data we want tooanalyze.</span></span> <span data-ttu-id="3db32-177">tipi di Hello disponibili dipendono dal filtro hello impostato nell'esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="3db32-177">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="3db32-178">Esaminare altri tipi disponibili di hello toosee di dati esportati hello e vedere hello [Esporta modello di dati](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="3db32-178">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="3db32-179">`/{date}/{time}` è uno schema scritto letteralmente.</span><span class="sxs-lookup"><span data-stu-id="3db32-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="3db32-180">nome hello tooget iKey della risorsa di Application Insights, aprire Essentials nella relativa pagina di panoramica e aprire le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="3db32-180">tooget hello name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="3db32-181">Completare l'installazione iniziale</span><span class="sxs-lookup"><span data-stu-id="3db32-181">Finish initial setup</span></span>
<span data-ttu-id="3db32-182">Verificare il formato di serializzazione hello:</span><span class="sxs-lookup"><span data-stu-id="3db32-182">Confirm hello serialization format:</span></span>

![Confermare e chiudere la procedura guidata](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="3db32-184">Chiudere la procedura guidata hello e attendere hello toocomplete di programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="3db32-184">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="3db32-185">Utilizzare toocheck funzione di esempio hello che hello percorso di input è stato impostato correttamente.</span><span class="sxs-lookup"><span data-stu-id="3db32-185">Use hello Sample function toocheck that you have set hello input path correctly.</span></span> <span data-ttu-id="3db32-186">In caso di errore: verifica della presenza dei dati nel servizio di archiviazione per l'intervallo di tempo esempio hello scelto hello.</span><span class="sxs-lookup"><span data-stu-id="3db32-186">If it fails: Check that there is data in hello storage for hello sample time range you chose.</span></span> <span data-ttu-id="3db32-187">Modifica definizione input hello e controllare impostare account di archiviazione hello, prefisso di percorso e Data formato correttamente.</span><span class="sxs-lookup"><span data-stu-id="3db32-187">Edit hello input definition and check you set hello storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="3db32-188">Impostare la query</span><span class="sxs-lookup"><span data-stu-id="3db32-188">Set query</span></span>
<span data-ttu-id="3db32-189">Aprire sezione query hello:</span><span class="sxs-lookup"><span data-stu-id="3db32-189">Open hello query section:</span></span>

![In Analisi di flusso selezionare Query](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="3db32-191">Sostituire query predefinita hello con:</span><span class="sxs-lookup"><span data-stu-id="3db32-191">Replace hello default query with:</span></span>

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

<span data-ttu-id="3db32-192">Si noti che innanzitutto hello alcune proprietà sono specifiche toopage visualizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="3db32-192">Notice that hello first few properties are specific toopage view data.</span></span> <span data-ttu-id="3db32-193">Le esportazioni di altri tipi di dati di telemetria avranno proprietà diverse.</span><span class="sxs-lookup"><span data-stu-id="3db32-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="3db32-194">Vedere hello [dettagliate di riferimento del modello di dati per i tipi di proprietà hello e valori.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="3db32-194">See hello [detailed data model reference for hello property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-toodatabase"></a><span data-ttu-id="3db32-195">Impostare toodatabase di output</span><span class="sxs-lookup"><span data-stu-id="3db32-195">Set up output toodatabase</span></span>
<span data-ttu-id="3db32-196">Selezionare SQL come output di hello.</span><span class="sxs-lookup"><span data-stu-id="3db32-196">Select SQL as hello output.</span></span>

![In Analisi di flusso selezionare Output](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="3db32-198">Specificare il database SQL di hello.</span><span class="sxs-lookup"><span data-stu-id="3db32-198">Specify hello SQL database.</span></span>

![Specificare dettagli hello del database](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="3db32-200">Chiudere la procedura guidata hello e attende una notifica che l'output di hello è stata impostata.</span><span class="sxs-lookup"><span data-stu-id="3db32-200">Close hello wizard and wait for a notification that hello output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="3db32-201">Avviare l'elaborazione</span><span class="sxs-lookup"><span data-stu-id="3db32-201">Start processing</span></span>
<span data-ttu-id="3db32-202">Avviare il processo di hello dalla barra delle azioni hello:</span><span class="sxs-lookup"><span data-stu-id="3db32-202">Start hello job from hello action bar:</span></span>

![In Analisi di flusso fare clic su Avvia.](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="3db32-204">È possibile scegliere se l'elaborazione di toostart hello dati a partire da ora o toostart con i dati precedenti.</span><span class="sxs-lookup"><span data-stu-id="3db32-204">You can choose whether toostart processing hello data starting from now, or toostart with earlier data.</span></span> <span data-ttu-id="3db32-205">Hello quest'ultimo è utile se si è avuto l'esportazione continua è già in esecuzione per un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="3db32-205">hello latter is useful if you have had Continuous Export already running for a while.</span></span>

![In Analisi di flusso fare clic su Avvia.](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="3db32-207">Dopo alcuni minuti, tornare indietro tooSQL strumenti di gestione di Server e guardare hello i dati trasmessi.</span><span class="sxs-lookup"><span data-stu-id="3db32-207">After a few minutes, go back tooSQL Server Management Tools and watch hello data flowing in.</span></span> <span data-ttu-id="3db32-208">Usare ad esempio una query simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="3db32-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="3db32-209">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="3db32-209">Related articles</span></span>
* [<span data-ttu-id="3db32-210">Esportare tooPowerBI tramite flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="3db32-210">Export tooPowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="3db32-211">Riferimento per i tipi di proprietà hello e i valori del modello di dati dettagliati.</span><span class="sxs-lookup"><span data-stu-id="3db32-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="3db32-212">Esportazione continua in Application Insights</span><span class="sxs-lookup"><span data-stu-id="3db32-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="3db32-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="3db32-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

