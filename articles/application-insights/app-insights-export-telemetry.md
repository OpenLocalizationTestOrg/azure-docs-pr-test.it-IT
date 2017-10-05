---
title: Esportazione continua dei dati di telemetria da Application Insights | Microsoft Docs
description: "Esportare i dati di diagnostica e di uso nella risorsa di archiviazione in Microsoft Azure e scaricarli da lì."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: 6ac3bda5101593b5ca66b4c9035e2fdac9d1e833
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="9ec6f-103">Esportare i dati di telemetria da Application Insights</span><span class="sxs-lookup"><span data-stu-id="9ec6f-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="9ec6f-104">Si vogliono mantenere i dati di telemetria per un periodo più lungo del periodo di mantenimento standard</span><span class="sxs-lookup"><span data-stu-id="9ec6f-104">Want to keep your telemetry for longer than the standard retention period?</span></span> <span data-ttu-id="9ec6f-105">o elaborarli in un modo particolare?</span><span class="sxs-lookup"><span data-stu-id="9ec6f-105">Or process it in some specialized way?</span></span> <span data-ttu-id="9ec6f-106">A tale scopo, l'esportazione continua è ideale.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="9ec6f-107">Gli eventi visualizzati nel portale di Application Insights possono essere esportati nella risorsa di archiviazione di Microsoft Azure in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-107">The events you see in the Application Insights portal can be exported to storage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="9ec6f-108">Da qui è possibile scaricare i dati e scrivere qualsiasi tipo di codice necessario per elaborarli.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-108">From there you can download your data and write whatever code you need to process it.</span></span>  

<span data-ttu-id="9ec6f-109">L'uso dell'esportazione continua può comportare un costo aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="9ec6f-110">Controllare il [modello di prezzi](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="9ec6f-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="9ec6f-111">Prima di configurare l'esportazione continua, è necessario prendere in considerazione alcune alternative:</span><span class="sxs-lookup"><span data-stu-id="9ec6f-111">Before you set up continuous export, there are some alternatives you might want to consider:</span></span>

* <span data-ttu-id="9ec6f-112">Il pulsante Esporta nella parte superiore del pannello delle metriche o di ricerca consente di esportare tabelle e grafici in un foglio di calcolo di Excel.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-112">The Export button at the top of a metrics or search blade lets you transfer tables and charts to an Excel spreadsheet.</span></span>

* <span data-ttu-id="9ec6f-113">[Dati di analisi](app-insights-analytics.md) offre un linguaggio avanzato di query per la telemetria</span><span class="sxs-lookup"><span data-stu-id="9ec6f-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="9ec6f-114">che consente anche di esportare i risultati.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-114">It can also export results.</span></span>
* <span data-ttu-id="9ec6f-115">Se si vogliono [esplorare i dati in Power BI](app-insights-export-power-bi.md), non è necessario usare l'esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-115">If you're looking to [explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="9ec6f-116">L'[API REST di accesso ai dati](https://dev.applicationinsights.io/) consente di accedere ai dati di telemetria a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-116">The [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="9ec6f-117">Con l'esportazione continua i dati vengono copiati nella risorsa di archiviazione, in cui possono rimanere fino a quando si desidera, ma sono ancora disponibili in Application Insights per il [periodo di conservazione](app-insights-data-retention-privacy.md) usuale.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-117">After Continuous Export copies your data to storage (where it can stay for as long as you like), it's still available in Application Insights for the usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="9ec6f-118"><a name="setup"></a> Creare un'esportazione continua</span><span class="sxs-lookup"><span data-stu-id="9ec6f-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="9ec6f-119">Nella risorsa di Application Insights per l'app aprire Esportazione continua e scegliere **Aggiungi**:</span><span class="sxs-lookup"><span data-stu-id="9ec6f-119">In the Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Scorrere verso il basso e fare clic su Esportazione continua](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="9ec6f-121">Scegliere i tipi di dati di telemetria da esportare.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-121">Choose the telemetry data types you want to export.</span></span>

3. <span data-ttu-id="9ec6f-122">Creare o selezionare un [account di archiviazione di Azure](../storage/common/storage-introduction.md) in cui memorizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want to store the data.</span></span>

    > [!Warning]
    > <span data-ttu-id="9ec6f-123">Per impostazione predefinita, il percorso di archiviazione verrà impostato sulla stessa area geografica della risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-123">By default, the storage location will be set to the same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="9ec6f-124">Se si esegue l'archiviazione in un'area differente, è possibile che vengano applicati addebiti per il trasferimento.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Fare clic su Aggiungi, Destinazione di esportazione, Account di archiviazione e quindi creare un nuovo archivio o scegliere un archivio esistente](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="9ec6f-126">Creare o selezionare un contenitore nella risorsa di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="9ec6f-126">Create or select a container in the storage:</span></span>

    ![Fare clic su Scegli tipi di eventi](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="9ec6f-128">Dopo averla creata, l'esportazione viene avviata.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="9ec6f-129">Si ottengono solo i dati ricevuti dopo avere creato l'esportazione.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-129">You only get data that arrives after you create the export.</span></span>

<span data-ttu-id="9ec6f-130">Può verificarsi un ritardo di circa un'ora prima che i dati vengano visualizzati nella risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-130">There can be a delay of about an hour before data appears in the storage.</span></span>

### <a name="to-edit-continuous-export"></a><span data-ttu-id="9ec6f-131">Per modificare l'esportazione continua</span><span class="sxs-lookup"><span data-stu-id="9ec6f-131">To edit continuous export</span></span>

<span data-ttu-id="9ec6f-132">Se si vogliono modificare i tipi di eventi in un secondo momento, è sufficiente modificare l'esportazione:</span><span class="sxs-lookup"><span data-stu-id="9ec6f-132">If you want to change the event types later, just edit the export:</span></span>

![Fare clic su Scegli tipi di eventi](./media/app-insights-export-telemetry/05-edit.png)

### <a name="to-stop-continuous-export"></a><span data-ttu-id="9ec6f-134">Per interrompere l'esportazione continua</span><span class="sxs-lookup"><span data-stu-id="9ec6f-134">To stop continuous export</span></span>

<span data-ttu-id="9ec6f-135">Per interrompere l'esportazione, fare clic su Disabilita.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-135">To stop the export, click Disable.</span></span> <span data-ttu-id="9ec6f-136">Quando si fa clic di nuovo su Abilita, l'esportazione verrà riavviata con nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-136">When you click Enable again, the export will restart with new data.</span></span> <span data-ttu-id="9ec6f-137">Non si otterranno i dati che arrivano nel portale mentre l'esportazione è stata disabilitata.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-137">You won't get the data that arrived in the portal while export was disabled.</span></span>

<span data-ttu-id="9ec6f-138">Per interrompere l'esportazione in modo permanente, eliminare l'esportazione.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-138">To stop the export permanently, delete it.</span></span> <span data-ttu-id="9ec6f-139">Questa operazione non elimina i dati dalla risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="9ec6f-140">Non si riesce ad aggiungere o modificare un'esportazione?</span><span class="sxs-lookup"><span data-stu-id="9ec6f-140">Can't add or change an export?</span></span>
* <span data-ttu-id="9ec6f-141">Per aggiungere o modificare le esportazioni, è necessario avere i diritti di accesso proprietario, collaboratore o collaboratore di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-141">To add or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="9ec6f-142">[Informazioni sui ruoli][roles].</span><span class="sxs-lookup"><span data-stu-id="9ec6f-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="9ec6f-143"><a name="analyze"></a> Quali eventi si ottengono?</span><span class="sxs-lookup"><span data-stu-id="9ec6f-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="9ec6f-144">I dati esportati sono dati di telemetria non elaborati ricevuti dall'applicazione, tranne che per l'aggiunta di dati del percorso calcolati dall'indirizzo IP del client.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-144">The exported data is the raw telemetry we receive from your application, except that we add location data which we calculate from the client IP address.</span></span>

<span data-ttu-id="9ec6f-145">I dati che il [campionamento](app-insights-sampling.md) ha rimosso non sono inclusi nei dati esportati.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in the exported data.</span></span>

<span data-ttu-id="9ec6f-146">Le altre metriche calcolate non sono incluse.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="9ec6f-147">Ad esempio, non si procederà all'esportazione dell'uso medio della CPU, ma si procederà all'esportazione dei dati di telemetria non elaborati a partire dai quali viene calcolata la media.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-147">For example, we don't export average CPU utilisation, but we do export the raw telemetry from which the average is computed.</span></span>

<span data-ttu-id="9ec6f-148">I dati includono anche i risultati di ogni [test Web di disponibilità](app-insights-monitor-web-app-availability.md) impostato.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-148">The data also includes the results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="9ec6f-149">**Campionamento.**</span><span class="sxs-lookup"><span data-stu-id="9ec6f-149">**Sampling.**</span></span> <span data-ttu-id="9ec6f-150">Se l'applicazione invia una grande quantità di dati, la funzionalità di campionamento può intervenire e inviare solo una percentuale della telemetria generata.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-150">If your application sends a lot of data, the sampling feature may operate and send only a fraction of the generated telemetry.</span></span> [<span data-ttu-id="9ec6f-151">Altre informazioni sul campionamento.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="9ec6f-152"><a name="get"></a> Esaminare i dati</span><span class="sxs-lookup"><span data-stu-id="9ec6f-152"><a name="get"></a> Inspect the data</span></span>
<span data-ttu-id="9ec6f-153">È possibile esaminare lo spazio di archiviazione direttamente nel portale.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-153">You can inspect the storage directly in the portal.</span></span> <span data-ttu-id="9ec6f-154">Fare clic su **Sfoglia**, selezionare l'account di archiviazione e quindi aprire i **Contenitori**.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="9ec6f-155">Per esaminare l'archiviazione di Azure in Visual Studio, aprire **Visualizza**, **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-155">To inspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="9ec6f-156">(Se non si dispone di tale comando del menu, è necessario installare l’SDK di Azure: aprire la finestra di dialogo **Nuovo progetto**, espandere Visual C#/Cloud e scegliere **Ottieni Microsoft Azure SDK per .NET**).</span><span class="sxs-lookup"><span data-stu-id="9ec6f-156">(If you don't have that menu command, you need to install the Azure SDK: Open the **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="9ec6f-157">Quando si apre l'archivio BLOB, si noterà un contenitore con un set di file BLOB.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="9ec6f-158">L'URI di ogni file è derivato dal nome della risorsa di Application Insights, la relativa chiave di strumentazione e tipo/data/ora della telemetria.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-158">The URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="9ec6f-159">(Il nome della risorsa viene scritto in minuscolo e la chiave di strumentazione omette i trattini).</span><span class="sxs-lookup"><span data-stu-id="9ec6f-159">(The resource name is all lowercase, and the instrumentation key omits dashes.)</span></span>

![Controllare l'archivio BLOB con uno strumento adatto](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="9ec6f-161">La data e ora sono UTC e lo sono quando i dati di telemetria sono stati depositati nell'archivio, non l'ora in cui sono stati generati.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-161">The date and time are UTC and are when the telemetry was deposited in the store - not the time it was generated.</span></span> <span data-ttu-id="9ec6f-162">Di conseguenza, se si scrive codice per scaricare i dati, può spostarsi in modo lineare attraverso i dati.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-162">So if you write code to download the data, it can move linearly through the data.</span></span>

<span data-ttu-id="9ec6f-163">Di seguito è riportato il formato del percorso:</span><span class="sxs-lookup"><span data-stu-id="9ec6f-163">Here's the form of the path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="9ec6f-164">Where</span><span class="sxs-lookup"><span data-stu-id="9ec6f-164">Where</span></span>

* <span data-ttu-id="9ec6f-165">`blobCreationTimeUtc` è l'ora di creazione del BLOB nell'archivio di gestione temporanea interno</span><span class="sxs-lookup"><span data-stu-id="9ec6f-165">`blobCreationTimeUtc` is time when blob was created in the internal staging storage</span></span>
* <span data-ttu-id="9ec6f-166">`blobDeliveryTimeUtc` è l'ora in cui il BLOB viene copiato nell'archivio di destinazione dell'esportazione</span><span class="sxs-lookup"><span data-stu-id="9ec6f-166">`blobDeliveryTimeUtc` is the time when blob is copied to the export destination storage</span></span>

## <span data-ttu-id="9ec6f-167"><a name="format"></a> Formato dati</span><span class="sxs-lookup"><span data-stu-id="9ec6f-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="9ec6f-168">Ogni BLOB è un file di testo che contiene più righe separate da '\n'.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="9ec6f-169">Contiene i dati di telemetria elaborati in un periodo di tempo di circa mezzo minuto.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-169">It contains the telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="9ec6f-170">Ogni riga rappresenta un punto dati di telemetria, ad esempio una richiesta o una visualizzazione di pagina.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="9ec6f-171">Ogni riga è un documento JSON non formattato.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="9ec6f-172">Se si desidera sedersi a osservare, aprirlo in Visual Studio e scegliere Modifica, Avanzate, File di formato:</span><span class="sxs-lookup"><span data-stu-id="9ec6f-172">If you want to sit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![Visualizzare i dati di telemetria con uno strumento adatto](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="9ec6f-174">Gli intervalli di tempo sono espressi in tick, dove 10 000 tick = 1 ms.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="9ec6f-175">Questi valori, ad esempio, indicano un tempo di 1 ms per inviare una richiesta dal browser, 3 ms per riceverla e 1,8 s per elaborare la pagina nel browser:</span><span class="sxs-lookup"><span data-stu-id="9ec6f-175">For example, these values show a time of 1ms to send a request from the browser, 3ms to receive it, and 1.8s to process the page in the browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="9ec6f-176">Riferimento dettagliato al modello di dati per i valori e i tipi di proprietà.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-176">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-the-data"></a><span data-ttu-id="9ec6f-177">Elaborazione dei dati</span><span class="sxs-lookup"><span data-stu-id="9ec6f-177">Processing the data</span></span>
<span data-ttu-id="9ec6f-178">Su scala ridotta è possibile scrivere codice per separare i dati, leggerli in un foglio di calcolo e così via.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-178">On a small scale, you can write some code to pull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="9ec6f-179">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="9ec6f-179">For example:</span></span>

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

<span data-ttu-id="9ec6f-180">Per un esempio di codice più esaustivo, vedere l'articolo relativo all'[uso di un ruolo di lavoro][exportasa].</span><span class="sxs-lookup"><span data-stu-id="9ec6f-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="9ec6f-181"><a name="delete"></a>Eliminare i vecchi dati</span><span class="sxs-lookup"><span data-stu-id="9ec6f-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="9ec6f-182">Si noti che si è responsabili della gestione della capacità di archiviazione ed eliminazione di vecchi dati, se necessario.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-182">Please note that you are responsible for managing your storage capacity and deleting the old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="9ec6f-183">Se si rigenera la chiave di archiviazione...</span><span class="sxs-lookup"><span data-stu-id="9ec6f-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="9ec6f-184">Se si modifica la chiave per l'archiviazione, l'esportazione continua non funzionerà più.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-184">If you change the key to your storage, continuous export will stop working.</span></span> <span data-ttu-id="9ec6f-185">Verrà visualizzata una notifica nell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="9ec6f-186">Aprire il pannello Esportazione continua e modificare l'esportazione.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-186">Open the Continuous Export blade and edit your export.</span></span> <span data-ttu-id="9ec6f-187">Modificare la destinazione di esportazione, ma lasciare selezionata la stessa risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-187">Edit the Export Destination, but just leave the same storage selected.</span></span> <span data-ttu-id="9ec6f-188">Fare clic su OK per confermare.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-188">Click OK to confirm.</span></span>

![Modificare l'esportazione continua, aprire e chiudere tre destinazioni di esportazione.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="9ec6f-190">L'esportazione continua verrà riavviata.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-190">The continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="9ec6f-191">Esempi di esportazione</span><span class="sxs-lookup"><span data-stu-id="9ec6f-191">Export samples</span></span>

* <span data-ttu-id="9ec6f-192">[Eseguire l'esportazione in SQL usando l'analisi di flusso][exportasa]</span><span class="sxs-lookup"><span data-stu-id="9ec6f-192">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="9ec6f-193">Esempio di analisi di flusso 2</span><span class="sxs-lookup"><span data-stu-id="9ec6f-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="9ec6f-194">Su scala più estesa considerare la possibilità di usare cluster [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop nel cloud.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in the cloud.</span></span> <span data-ttu-id="9ec6f-195">HDInsight offre un'ampia gamma di tecnologie per la gestione e analisi dei Big Data e può essere usato per elaborare i dati esportati da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it to process data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="9ec6f-196">Domande e risposte</span><span class="sxs-lookup"><span data-stu-id="9ec6f-196">Q & A</span></span>
* <span data-ttu-id="9ec6f-197">*Si intende scaricare semplicemente un grafico.*</span><span class="sxs-lookup"><span data-stu-id="9ec6f-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="9ec6f-198">Questa operazione è consentita.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-198">Yes, you can do that.</span></span> <span data-ttu-id="9ec6f-199">Nella parte superiore del pannello fare clic sul **pulsante di esportazione dati**.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-199">At the top of the blade, click **Export Data**.</span></span>
* <span data-ttu-id="9ec6f-200">*È stata impostata un'esportazione, ma non sono presenti dati nell'archivio personale.*</span><span class="sxs-lookup"><span data-stu-id="9ec6f-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="9ec6f-201">Application Insights ha ricevuto eventuali dati di telemetria dall'app dal momento in cui si è impostata l'esportazione?</span><span class="sxs-lookup"><span data-stu-id="9ec6f-201">Did Application Insights receive any telemetry from your app since you set up the export?</span></span> <span data-ttu-id="9ec6f-202">Si riceveranno solo nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-202">You'll only receive new data.</span></span>
* <span data-ttu-id="9ec6f-203">*Si è tentato di impostare un'esportazione, ma è stato negato l'accesso*</span><span class="sxs-lookup"><span data-stu-id="9ec6f-203">*I tried to set up an export, but was denied access*</span></span>

    <span data-ttu-id="9ec6f-204">Se l'account è di proprietà dell'organizzazione, è necessario essere un membro del gruppo di proprietari o di collaboratori.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-204">If the account is owned by your organization, you have to be a member of the owners or contributors groups.</span></span>
* <span data-ttu-id="9ec6f-205">*È possibile eseguire un'esportazione direttamente al negozio locale?*</span><span class="sxs-lookup"><span data-stu-id="9ec6f-205">*Can I export straight to my own on-premises store?*</span></span>

    <span data-ttu-id="9ec6f-206">No.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-206">No, sorry.</span></span> <span data-ttu-id="9ec6f-207">Il motore di esportazione attualmente funziona solo con Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="9ec6f-208">*Esiste un limite alla quantità di dati da inserire nell'archivio personale?*</span><span class="sxs-lookup"><span data-stu-id="9ec6f-208">*Is there any limit to the amount of data you put in my store?*</span></span>

    <span data-ttu-id="9ec6f-209">No.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-209">No.</span></span> <span data-ttu-id="9ec6f-210">L'inserimento dei dati continuerà fino a quando non si elimina l'esportazione.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-210">We'll keep pushing data in until you delete the export.</span></span> <span data-ttu-id="9ec6f-211">Occorrerà fermarsi se i limiti esterni per l'archiviazione BLOB sono stati raggiunti, ma ciò è abbastanza difficile.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-211">We'll stop if we hit the outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="9ec6f-212">Spetta all'utente controllare quante risorse di archiviazione usare.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-212">It's up to you to control how much storage you use.</span></span>  
* <span data-ttu-id="9ec6f-213">*Quanti BLOB dovrebbero essere visualizzati nella risorsa di archiviazione?*</span><span class="sxs-lookup"><span data-stu-id="9ec6f-213">*How many blobs should I see in the storage?*</span></span>

  * <span data-ttu-id="9ec6f-214">Per ogni tipi di dati selezionato per l'esportazione, viene creato un nuovo BLOB ogni minuto, se sono disponibili dati.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-214">For every data type you selected to export, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="9ec6f-215">Per le applicazioni con traffico elevato, inoltre, vengono allocate unità di partizione aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="9ec6f-216">In questo caso ogni unità crea un BLOB ogni minuto.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="9ec6f-217">*La chiave per la risorsa di archiviazione è stata rigenerata o il nome del contenitore è stato modificato, ma l'esportazione non funziona.*</span><span class="sxs-lookup"><span data-stu-id="9ec6f-217">*I regenerated the key to my storage or changed the name of the container, and now the export doesn't work.*</span></span>

    <span data-ttu-id="9ec6f-218">Modificare l'esportazione e aprire il pannello di destinazione dell'esportazione.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-218">Edit the export and open the export destination blade.</span></span> <span data-ttu-id="9ec6f-219">Lasciare la stessa risorsa di archiviazione selezionata come in precedenza e fare clic su OK per confermare.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-219">Leave the same storage selected as before, and click OK to confirm.</span></span> <span data-ttu-id="9ec6f-220">L'esportazione verrà riavviata.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-220">Export will restart.</span></span> <span data-ttu-id="9ec6f-221">Se la modifica è stata eseguita negli ultimi giorni, non si perderanno i dati.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-221">If the change was within the past few days, you won't lose data.</span></span>
* <span data-ttu-id="9ec6f-222">*È possibile sospendere l'esportazione?*</span><span class="sxs-lookup"><span data-stu-id="9ec6f-222">*Can I pause the export?*</span></span>

    <span data-ttu-id="9ec6f-223">Sì.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-223">Yes.</span></span> <span data-ttu-id="9ec6f-224">Fare clic su Disabilita.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="9ec6f-225">Esempi di codice</span><span class="sxs-lookup"><span data-stu-id="9ec6f-225">Code samples</span></span>

* [<span data-ttu-id="9ec6f-226">Esempio di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="9ec6f-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="9ec6f-227">[Eseguire l'esportazione in SQL usando l'analisi di flusso][exportasa]</span><span class="sxs-lookup"><span data-stu-id="9ec6f-227">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="9ec6f-228">Riferimento dettagliato al modello di dati per i valori e i tipi di proprietà.</span><span class="sxs-lookup"><span data-stu-id="9ec6f-228">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
