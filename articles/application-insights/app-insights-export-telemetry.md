---
title: esportazione di aaaContinuous di telemetria da Application Insights | Documenti Microsoft
description: Esportare toostorage di dati di diagnostica e utilizzo in Microsoft Azure e scaricarlo da qui.
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
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="1b4e5-103">Esportare i dati di telemetria da Application Insights</span><span class="sxs-lookup"><span data-stu-id="1b4e5-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="1b4e5-104">Desidera tookeep dati di telemetria per oltre il periodo di memorizzazione standard di hello?</span><span class="sxs-lookup"><span data-stu-id="1b4e5-104">Want tookeep your telemetry for longer than hello standard retention period?</span></span> <span data-ttu-id="1b4e5-105">o elaborarli in un modo particolare?</span><span class="sxs-lookup"><span data-stu-id="1b4e5-105">Or process it in some specialized way?</span></span> <span data-ttu-id="1b4e5-106">A tale scopo, l'esportazione continua è ideale.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="1b4e5-107">gli eventi di Hello che viene visualizzato nel portale Application Insights hello possono essere esportati toostorage in Microsoft Azure in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-107">hello events you see in hello Application Insights portal can be exported toostorage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="1b4e5-108">Da qui è possibile scaricare i dati e scrivere qualsiasi tipo di codice è necessario tooprocess è.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-108">From there you can download your data and write whatever code you need tooprocess it.</span></span>  

<span data-ttu-id="1b4e5-109">L'uso dell'esportazione continua può comportare un costo aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="1b4e5-110">Controllare il [modello di prezzi](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="1b4e5-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="1b4e5-111">Prima di configurare l'esportazione continua, sono disponibili alcune alternative tooconsider potrebbe essere necessario:</span><span class="sxs-lookup"><span data-stu-id="1b4e5-111">Before you set up continuous export, there are some alternatives you might want tooconsider:</span></span>

* <span data-ttu-id="1b4e5-112">pulsante Esporta Hello nella parte superiore di hello di blade metriche o ricerca consente di trasferire le tabelle e grafici tooan foglio di calcolo Excel.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-112">hello Export button at hello top of a metrics or search blade lets you transfer tables and charts tooan Excel spreadsheet.</span></span>

* <span data-ttu-id="1b4e5-113">[Dati di analisi](app-insights-analytics.md) offre un linguaggio avanzato di query per la telemetria</span><span class="sxs-lookup"><span data-stu-id="1b4e5-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="1b4e5-114">che consente anche di esportare i risultati.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-114">It can also export results.</span></span>
* <span data-ttu-id="1b4e5-115">Se si sta cercando troppo[esplorare i dati in Power BI](app-insights-export-power-bi.md), è possibile farlo senza utilizzare l'esportazione continua.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-115">If you're looking too[explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="1b4e5-116">Hello [API REST di accesso ai dati](https://dev.applicationinsights.io/) consente di accedere ai dati di telemetria a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-116">hello [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="1b4e5-117">Dopo l'esportazione continua copia toostorage i dati (in cui possibile abilitarlo per fino a quando si desidera), è ancora disponibile in Application Insights per hello consueta [periodo di memorizzazione](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="1b4e5-117">After Continuous Export copies your data toostorage (where it can stay for as long as you like), it's still available in Application Insights for hello usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="1b4e5-118"><a name="setup"></a> Creare un'esportazione continua</span><span class="sxs-lookup"><span data-stu-id="1b4e5-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="1b4e5-119">Nella risorsa di Application Insights per l'applicazione hello, aprire l'esportazione continua e scegliere **Aggiungi**:</span><span class="sxs-lookup"><span data-stu-id="1b4e5-119">In hello Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Scorrere verso il basso e fare clic su Esportazione continua](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="1b4e5-121">Scegliere i tipi di dati di telemetria hello desiderato tooexport.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-121">Choose hello telemetry data types you want tooexport.</span></span>

3. <span data-ttu-id="1b4e5-122">Creare o selezionare un [account di archiviazione Azure](../storage/common/storage-introduction.md) in cui si desidera dati hello toostore.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want toostore hello data.</span></span>

    > [!Warning]
    > <span data-ttu-id="1b4e5-123">Per impostazione predefinita, il percorso di archiviazione hello verrà impostato toohello stessa area geografica della risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-123">By default, hello storage location will be set toohello same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="1b4e5-124">Se si esegue l'archiviazione in un'area differente, è possibile che vengano applicati addebiti per il trasferimento.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Fare clic su Aggiungi, Destinazione di esportazione, Account di archiviazione e quindi creare un nuovo archivio o scegliere un archivio esistente](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="1b4e5-126">Creare o selezionare un contenitore nell'archiviazione hello:</span><span class="sxs-lookup"><span data-stu-id="1b4e5-126">Create or select a container in hello storage:</span></span>

    ![Fare clic su Scegli tipi di eventi](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="1b4e5-128">Dopo averla creata, l'esportazione viene avviata.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="1b4e5-129">Si ottengono solo i dati in arrivo dopo la creazione di esportazione hello.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-129">You only get data that arrives after you create hello export.</span></span>

<span data-ttu-id="1b4e5-130">Può esistere un ritardo di circa un'ora prima che i dati vengono visualizzati nel servizio di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-130">There can be a delay of about an hour before data appears in hello storage.</span></span>

### <a name="tooedit-continuous-export"></a><span data-ttu-id="1b4e5-131">esportazione continua tooedit</span><span class="sxs-lookup"><span data-stu-id="1b4e5-131">tooedit continuous export</span></span>

<span data-ttu-id="1b4e5-132">Se si desidera che i tipi di evento hello toochange in un secondo momento, è sufficiente modificare esportazione hello:</span><span class="sxs-lookup"><span data-stu-id="1b4e5-132">If you want toochange hello event types later, just edit hello export:</span></span>

![Fare clic su Scegli tipi di eventi](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a><span data-ttu-id="1b4e5-134">esportazione continua toostop</span><span class="sxs-lookup"><span data-stu-id="1b4e5-134">toostop continuous export</span></span>

<span data-ttu-id="1b4e5-135">esportazione di hello toostop, fare clic su Disattiva.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-135">toostop hello export, click Disable.</span></span> <span data-ttu-id="1b4e5-136">Quando si sceglie abilita nuovamente, esportazione hello verrà riavviato con nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-136">When you click Enable again, hello export will restart with new data.</span></span> <span data-ttu-id="1b4e5-137">Si otterranno dati hello ricevuti nel portale di hello durante l'esportazione è stata disabilitata.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-137">You won't get hello data that arrived in hello portal while export was disabled.</span></span>

<span data-ttu-id="1b4e5-138">esportazione di hello toostop, l'eliminazione definitiva.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-138">toostop hello export permanently, delete it.</span></span> <span data-ttu-id="1b4e5-139">Questa operazione non elimina i dati dalla risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="1b4e5-140">Non si riesce ad aggiungere o modificare un'esportazione?</span><span class="sxs-lookup"><span data-stu-id="1b4e5-140">Can't add or change an export?</span></span>
* <span data-ttu-id="1b4e5-141">esportazioni tooadd o modifica, sono necessari i diritti di accesso proprietario, collaboratore o collaboratore di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-141">tooadd or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="1b4e5-142">[Informazioni sui ruoli][roles].</span><span class="sxs-lookup"><span data-stu-id="1b4e5-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="1b4e5-143"><a name="analyze"></a> Quali eventi si ottengono?</span><span class="sxs-lookup"><span data-stu-id="1b4e5-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="1b4e5-144">Hello dati esportati sono telemetria di hello non elaborati ricevuti dall'applicazione, ma è aggiungere dati di percorso che si calcolano dall'indirizzo IP del client hello.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-144">hello exported data is hello raw telemetry we receive from your application, except that we add location data which we calculate from hello client IP address.</span></span>

<span data-ttu-id="1b4e5-145">Dati che sono stati eliminati da [campionamento](app-insights-sampling.md) non è incluso nei dati hello esportata.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in hello exported data.</span></span>

<span data-ttu-id="1b4e5-146">Le altre metriche calcolate non sono incluse.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="1b4e5-147">Ad esempio, non esportazione medio utilizzo della CPU, ma si procederà all'esportazione di telemetria non elaborati di hello da cui viene calcolata la media hello.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-147">For example, we don't export average CPU utilisation, but we do export hello raw telemetry from which hello average is computed.</span></span>

<span data-ttu-id="1b4e5-148">Hello dati includono anche risultati hello di qualsiasi [test web disponibilità](app-insights-monitor-web-app-availability.md) che è stato impostato.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-148">hello data also includes hello results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="1b4e5-149">**Campionamento.**</span><span class="sxs-lookup"><span data-stu-id="1b4e5-149">**Sampling.**</span></span> <span data-ttu-id="1b4e5-150">Se l'applicazione invia una grande quantità di dati, funzionalità di campionamento hello possono operare e inviare solo una frazione di telemetria hello generato.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-150">If your application sends a lot of data, hello sampling feature may operate and send only a fraction of hello generated telemetry.</span></span> [<span data-ttu-id="1b4e5-151">Altre informazioni sul campionamento.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="1b4e5-152"><a name="get"></a>Controllare i dati di hello</span><span class="sxs-lookup"><span data-stu-id="1b4e5-152"><a name="get"></a> Inspect hello data</span></span>
<span data-ttu-id="1b4e5-153">È possibile esaminare archiviazione hello direttamente nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-153">You can inspect hello storage directly in hello portal.</span></span> <span data-ttu-id="1b4e5-154">Fare clic su **Sfoglia**, selezionare l'account di archiviazione e quindi aprire i **Contenitori**.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="1b4e5-155">tooinspect archiviazione di Azure in Visual Studio, aprire **vista**, **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-155">tooinspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="1b4e5-156">(Se non si dispone di tale comando di menu, è necessario tooinstall hello Azure SDK: hello aprire **nuovo progetto** finestra di dialogo espandere Visual c# del cloud e scegliere **ottenere Microsoft Azure SDK per .NET**.)</span><span class="sxs-lookup"><span data-stu-id="1b4e5-156">(If you don't have that menu command, you need tooinstall hello Azure SDK: Open hello **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="1b4e5-157">Quando si apre l'archivio BLOB, si noterà un contenitore con un set di file BLOB.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="1b4e5-158">URI di ogni file Hello derivato dal nome di risorsa di Application Insights, la chiave di strumentazione, tipo di dati di telemetria/data/ora.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-158">hello URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="1b4e5-159">(nome della risorsa hello è tutti in lettere minuscole, e la chiave di strumentazione hello omette trattini).</span><span class="sxs-lookup"><span data-stu-id="1b4e5-159">(hello resource name is all lowercase, and hello instrumentation key omits dashes.)</span></span>

![Controllare l'archivio di blob hello con uno strumento appropriato](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="1b4e5-161">hello data e ora siano UTC e quando è stato depositato telemetria hello nell'archivio di hello - tempo di hello non è stato generato.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-161">hello date and time are UTC and are when hello telemetry was deposited in hello store - not hello time it was generated.</span></span> <span data-ttu-id="1b4e5-162">Pertanto, se si scrivono dati di code toodownload hello, è possibile spostarsi in modo lineare dati hello.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-162">So if you write code toodownload hello data, it can move linearly through hello data.</span></span>

<span data-ttu-id="1b4e5-163">Di seguito è il formato di hello di hello percorso:</span><span class="sxs-lookup"><span data-stu-id="1b4e5-163">Here's hello form of hello path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="1b4e5-164">Where</span><span class="sxs-lookup"><span data-stu-id="1b4e5-164">Where</span></span>

* <span data-ttu-id="1b4e5-165">`blobCreationTimeUtc`è ora di creazione blob in hello interno gestione temporanea di archiviazione</span><span class="sxs-lookup"><span data-stu-id="1b4e5-165">`blobCreationTimeUtc` is time when blob was created in hello internal staging storage</span></span>
* <span data-ttu-id="1b4e5-166">`blobDeliveryTimeUtc`è il momento di hello è copiato toohello esportazione destinazione archiviazione blob</span><span class="sxs-lookup"><span data-stu-id="1b4e5-166">`blobDeliveryTimeUtc` is hello time when blob is copied toohello export destination storage</span></span>

## <span data-ttu-id="1b4e5-167"><a name="format"></a> Formato dati</span><span class="sxs-lookup"><span data-stu-id="1b4e5-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="1b4e5-168">Ogni BLOB è un file di testo che contiene più righe separate da '\n'.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="1b4e5-169">Contiene dati di telemetria hello elaborati in un periodo di tempo di circa metà un minuto.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-169">It contains hello telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="1b4e5-170">Ogni riga rappresenta un punto dati di telemetria, ad esempio una richiesta o una visualizzazione di pagina.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="1b4e5-171">Ogni riga è un documento JSON non formattato.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="1b4e5-172">Se desidera toosit comincerà, aprirlo in Visual Studio e scegliere Modifica, avanzate, File di formato:</span><span class="sxs-lookup"><span data-stu-id="1b4e5-172">If you want toosit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![Visualizza dati di telemetria hello con uno strumento appropriato](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="1b4e5-174">Gli intervalli di tempo sono espressi in tick, dove 10 000 tick = 1 ms.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="1b4e5-175">Ad esempio, questi valori vengono visualizzate un tempo pari a 1 ms toosend una richiesta da browser hello, 3 MS tooreceive e 1.8s tooprocess hello pagina nel browser hello:</span><span class="sxs-lookup"><span data-stu-id="1b4e5-175">For example, these values show a time of 1ms toosend a request from hello browser, 3ms tooreceive it, and 1.8s tooprocess hello page in hello browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="1b4e5-176">Riferimento per i tipi di proprietà hello e i valori del modello di dati dettagliati.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-176">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a><span data-ttu-id="1b4e5-177">L'elaborazione dei dati hello</span><span class="sxs-lookup"><span data-stu-id="1b4e5-177">Processing hello data</span></span>
<span data-ttu-id="1b4e5-178">Su una scala di piccole dimensioni, è possibile scrivere i dati di alcuni toopull codice divide in due, leggerlo in un foglio di calcolo e così via.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-178">On a small scale, you can write some code toopull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="1b4e5-179">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1b4e5-179">For example:</span></span>

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

<span data-ttu-id="1b4e5-180">Per un esempio di codice più esaustivo, vedere l'articolo relativo all'[uso di un ruolo di lavoro][exportasa].</span><span class="sxs-lookup"><span data-stu-id="1b4e5-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="1b4e5-181"><a name="delete"></a>Eliminare i vecchi dati</span><span class="sxs-lookup"><span data-stu-id="1b4e5-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="1b4e5-182">Si noti che è responsabile per la gestione della capacità di archiviazione e l'eliminazione dei dati precedente hello se necessario.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-182">Please note that you are responsible for managing your storage capacity and deleting hello old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="1b4e5-183">Se si rigenera la chiave di archiviazione...</span><span class="sxs-lookup"><span data-stu-id="1b4e5-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="1b4e5-184">Se si modifica l'archiviazione di chiavi tooyour hello, l'esportazione continua smetteranno di funzionare.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-184">If you change hello key tooyour storage, continuous export will stop working.</span></span> <span data-ttu-id="1b4e5-185">Verrà visualizzata una notifica nell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="1b4e5-186">Aprire il pannello di esportazione continua hello e modificare l'esportazione.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-186">Open hello Continuous Export blade and edit your export.</span></span> <span data-ttu-id="1b4e5-187">Modifica hello esportare destinazione, ma lasciare hello stessa risorsa di archiviazione selezionato.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-187">Edit hello Export Destination, but just leave hello same storage selected.</span></span> <span data-ttu-id="1b4e5-188">Fare clic su OK tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-188">Click OK tooconfirm.</span></span>

![Modifica hello continua esportare, aprire e chiudere tre destinazione dell'esportazione.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="1b4e5-190">l'esportazione continua Hello verrà riavviato.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-190">hello continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="1b4e5-191">Esempi di esportazione</span><span class="sxs-lookup"><span data-stu-id="1b4e5-191">Export samples</span></span>

* <span data-ttu-id="1b4e5-192">[Esportare tooSQL tramite flusso Analitica][exportasa]</span><span class="sxs-lookup"><span data-stu-id="1b4e5-192">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="1b4e5-193">Esempio di analisi di flusso 2</span><span class="sxs-lookup"><span data-stu-id="1b4e5-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="1b4e5-194">In scale di dimensioni maggiori, prendere in considerazione [HDInsight](https://azure.microsoft.com/services/hdinsight/) -cluster Hadoop in cloud hello.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in hello cloud.</span></span> <span data-ttu-id="1b4e5-195">HDInsight offre un'ampia gamma di tecnologie per la gestione e analisi dei dati di grandi dimensioni e, è possibile utilizzare dati tooprocess che sono stati esportati da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it tooprocess data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="1b4e5-196">Domande e risposte</span><span class="sxs-lookup"><span data-stu-id="1b4e5-196">Q & A</span></span>
* <span data-ttu-id="1b4e5-197">*Si intende scaricare semplicemente un grafico.*</span><span class="sxs-lookup"><span data-stu-id="1b4e5-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="1b4e5-198">Questa operazione è consentita.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-198">Yes, you can do that.</span></span> <span data-ttu-id="1b4e5-199">Nella parte superiore di hello del Pannello di hello, fare clic su **Esporta dati**.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-199">At hello top of hello blade, click **Export Data**.</span></span>
* <span data-ttu-id="1b4e5-200">*È stata impostata un'esportazione, ma non sono presenti dati nell'archivio personale.*</span><span class="sxs-lookup"><span data-stu-id="1b4e5-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="1b4e5-201">Application Insights ricevuto eventuali dati di telemetria dall'app perché è impostare esportazione hello?</span><span class="sxs-lookup"><span data-stu-id="1b4e5-201">Did Application Insights receive any telemetry from your app since you set up hello export?</span></span> <span data-ttu-id="1b4e5-202">Si riceveranno solo nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-202">You'll only receive new data.</span></span>
* <span data-ttu-id="1b4e5-203">*Tentato tooset backup un'esportazione, ma è stato negato l'accesso*</span><span class="sxs-lookup"><span data-stu-id="1b4e5-203">*I tried tooset up an export, but was denied access*</span></span>

    <span data-ttu-id="1b4e5-204">Se l'organizzazione account hello è di proprietà, è necessario toobe un membro dei gruppi di collaboratori o i proprietari di hello.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-204">If hello account is owned by your organization, you have toobe a member of hello owners or contributors groups.</span></span>
* <span data-ttu-id="1b4e5-205">*È possibile esportare toomy retta locale proprio archivio?*</span><span class="sxs-lookup"><span data-stu-id="1b4e5-205">*Can I export straight toomy own on-premises store?*</span></span>

    <span data-ttu-id="1b4e5-206">No.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-206">No, sorry.</span></span> <span data-ttu-id="1b4e5-207">Il motore di esportazione attualmente funziona solo con Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="1b4e5-208">*C'è alcun limite di toohello di dati inseriti nell'archivio personale?*</span><span class="sxs-lookup"><span data-stu-id="1b4e5-208">*Is there any limit toohello amount of data you put in my store?*</span></span>

    <span data-ttu-id="1b4e5-209">No.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-209">No.</span></span> <span data-ttu-id="1b4e5-210">Si saranno mantenere il push dei dati fino a quando non si elimina l'esportazione di hello.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-210">We'll keep pushing data in until you delete hello export.</span></span> <span data-ttu-id="1b4e5-211">Verrà interrotta se viene raggiunto i limiti di hello esterno per l'archiviazione blob, ma che è notevole.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-211">We'll stop if we hit hello outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="1b4e5-212">È attivo tooyou toocontrol si utilizza lo spazio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-212">It's up tooyou toocontrol how much storage you use.</span></span>  
* <span data-ttu-id="1b4e5-213">*Il numero di BLOB è consigliabile vedere nel servizio di archiviazione hello*</span><span class="sxs-lookup"><span data-stu-id="1b4e5-213">*How many blobs should I see in hello storage?*</span></span>

  * <span data-ttu-id="1b4e5-214">Per ogni tipo di dati di tipo è tooexport selezionato, un nuovo blob viene creato ogni minuto (se sono disponibili dati).</span><span class="sxs-lookup"><span data-stu-id="1b4e5-214">For every data type you selected tooexport, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="1b4e5-215">Per le applicazioni con traffico elevato, inoltre, vengono allocate unità di partizione aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="1b4e5-216">In questo caso ogni unità crea un BLOB ogni minuto.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="1b4e5-217">*Non è hello toomy chiave archiviazione rigenerate o nome hello del contenitore hello modificato, ed esportazione hello non funziona.*</span><span class="sxs-lookup"><span data-stu-id="1b4e5-217">*I regenerated hello key toomy storage or changed hello name of hello container, and now hello export doesn't work.*</span></span>

    <span data-ttu-id="1b4e5-218">Modificare l'esportazione di hello e aprire Pannello di destinazione di esportazione hello.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-218">Edit hello export and open hello export destination blade.</span></span> <span data-ttu-id="1b4e5-219">Lasciare hello stessa risorsa di archiviazione selezionato in precedenza e fare clic su OK tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-219">Leave hello same storage selected as before, and click OK tooconfirm.</span></span> <span data-ttu-id="1b4e5-220">L'esportazione verrà riavviata.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-220">Export will restart.</span></span> <span data-ttu-id="1b4e5-221">Se è stata modifica hello all'interno di hello dopo alcuni giorni, dei dati andrà perso.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-221">If hello change was within hello past few days, you won't lose data.</span></span>
* <span data-ttu-id="1b4e5-222">*È possibile sospendere l'esportazione di hello?*</span><span class="sxs-lookup"><span data-stu-id="1b4e5-222">*Can I pause hello export?*</span></span>

    <span data-ttu-id="1b4e5-223">Sì.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-223">Yes.</span></span> <span data-ttu-id="1b4e5-224">Fare clic su Disabilita.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="1b4e5-225">Esempi di codice</span><span class="sxs-lookup"><span data-stu-id="1b4e5-225">Code samples</span></span>

* [<span data-ttu-id="1b4e5-226">Esempio di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="1b4e5-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="1b4e5-227">[Esportare tooSQL tramite flusso Analitica][exportasa]</span><span class="sxs-lookup"><span data-stu-id="1b4e5-227">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="1b4e5-228">Riferimento per i tipi di proprietà hello e i valori del modello di dati dettagliati.</span><span class="sxs-lookup"><span data-stu-id="1b4e5-228">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
