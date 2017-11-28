---
title: aaaHow toouse Fiddler tooevaluate e testare le API REST di ricerca di Azure | Documenti Microsoft
description: "Usare Fiddler per la disponibilità di ricerca di Azure un approccio senza codice tooverifying e provare hello API REST."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="bfc97-103">Usare Fiddler tooevaluate e testare le API REST di ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="bfc97-103">Use Fiddler tooevaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="bfc97-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="bfc97-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="bfc97-105">Esplora ricerche</span><span class="sxs-lookup"><span data-stu-id="bfc97-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="bfc97-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="bfc97-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="bfc97-107">.NET</span><span class="sxs-lookup"><span data-stu-id="bfc97-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="bfc97-108">REST</span><span class="sxs-lookup"><span data-stu-id="bfc97-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="bfc97-109">Questo articolo viene illustrato come toouse Fiddler, disponibile come una [download gratuito di telerik](http://www.telerik.com/fiddler), utilizzando hello API REST di ricerca di Azure, senza la necessità di qualsiasi codice toowrite tooissue HTTP richieste tooand Visualizza risposte.</span><span class="sxs-lookup"><span data-stu-id="bfc97-109">This article explains how toouse Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), tooissue HTTP requests tooand view responses using hello Azure Search REST API, without having toowrite any code.</span></span> <span data-ttu-id="bfc97-110">Ricerca di Azure è un servizio di ricerca cloud ospitato in Microsoft Azure e completamente gestito, facilmente programmabile con le API REST e .NET.</span><span class="sxs-lookup"><span data-stu-id="bfc97-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="bfc97-111">API REST sono documentate nel servizio di ricerca di Azure Hello [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span><span class="sxs-lookup"><span data-stu-id="bfc97-111">hello Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="bfc97-112">In hello alla procedura seguente, si sarà creare un indice, caricare documenti, indice hello query e query sul sistema hello per informazioni sul servizio.</span><span class="sxs-lookup"><span data-stu-id="bfc97-112">In hello following steps, you'll create an index, upload documents, query hello index, and then query hello system for service information.</span></span>

<span data-ttu-id="bfc97-113">toocomplete questi passaggi, sarà necessario un servizio di ricerca di Azure e `api-key`.</span><span class="sxs-lookup"><span data-stu-id="bfc97-113">toocomplete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="bfc97-114">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per istruzioni sulla modalità di avvio tooget.</span><span class="sxs-lookup"><span data-stu-id="bfc97-114">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for instructions on how tooget started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="bfc97-115">Creare un indice</span><span class="sxs-lookup"><span data-stu-id="bfc97-115">Create an index</span></span>
1. <span data-ttu-id="bfc97-116">Avviare Fiddler</span><span class="sxs-lookup"><span data-stu-id="bfc97-116">Start Fiddler.</span></span> <span data-ttu-id="bfc97-117">In hello **File** menu, disattivare **acquisire il traffico** toohide estranei HTTP attività non correlate toohello dell'attività corrente.</span><span class="sxs-lookup"><span data-stu-id="bfc97-117">On hello **File** menu, turn off **Capture Traffic** toohide extraneous HTTP activity that is unrelated toohello current task.</span></span>
2. <span data-ttu-id="bfc97-118">In hello **Composer** scheda sarà di formulare una richiesta simile al seguente cattura di schermata hello.</span><span class="sxs-lookup"><span data-stu-id="bfc97-118">On hello **Composer** tab, you'll formulate a request that looks like hello following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="bfc97-119">Selezionare **PUT**.</span><span class="sxs-lookup"><span data-stu-id="bfc97-119">Select **PUT**.</span></span>
4. <span data-ttu-id="bfc97-120">Immettere un URL che specifica l'URL del servizio hello, attributi della richiesta e hello. api-version.</span><span class="sxs-lookup"><span data-stu-id="bfc97-120">Enter a URL that specifies hello service URL, request attributes, and hello api-version.</span></span> <span data-ttu-id="bfc97-121">Alcuni tookeep di puntatori in considerazione:</span><span class="sxs-lookup"><span data-stu-id="bfc97-121">A few pointers tookeep in mind:</span></span>

   * <span data-ttu-id="bfc97-122">Utilizzo di HTTPS come prefisso hello.</span><span class="sxs-lookup"><span data-stu-id="bfc97-122">Use HTTPS as hello prefix.</span></span>
   * <span data-ttu-id="bfc97-123">L'attributo della richiesta è "/indexes/hotels".</span><span class="sxs-lookup"><span data-stu-id="bfc97-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="bfc97-124">In questo modo toocreate di ricerca di un indice denominato 'hotel'.</span><span class="sxs-lookup"><span data-stu-id="bfc97-124">This tells Search toocreate an index named 'hotels'.</span></span>
   * <span data-ttu-id="bfc97-125">La versione API è specificata in lettere minuscole come "?api-version=2016-09-01".</span><span class="sxs-lookup"><span data-stu-id="bfc97-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="bfc97-126">Le versioni API sono importanti perché Ricerca di Azure distribuisce aggiornamenti su base regolare.</span><span class="sxs-lookup"><span data-stu-id="bfc97-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="bfc97-127">In rari casi, un aggiornamento del servizio può introdurre un toohello di modifica di rilievo API.</span><span class="sxs-lookup"><span data-stu-id="bfc97-127">On rare occasions, a service update may introduce a breaking change toohello API.</span></span> <span data-ttu-id="bfc97-128">Per questo motivo, Ricerca di Azure richiede la versione dell'API in ogni richiesta per garantire il controllo completo sulla versione usata.</span><span class="sxs-lookup"><span data-stu-id="bfc97-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="bfc97-129">URL completo di Hello dovrebbe essere simile toohello esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="bfc97-129">hello full URL should look similar toohello following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="bfc97-130">Specificare l'intestazione della richiesta hello, sostituendo host hello e la chiave api con i valori validi per il servizio.</span><span class="sxs-lookup"><span data-stu-id="bfc97-130">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="bfc97-131">Nel corpo della richiesta, incollare i campi di hello che costituiscono la definizione di indice hello.</span><span class="sxs-lookup"><span data-stu-id="bfc97-131">In Request Body, paste in hello fields that make up hello index definition.</span></span>

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. <span data-ttu-id="bfc97-132">Fare clic su **Execute**.</span><span class="sxs-lookup"><span data-stu-id="bfc97-132">Click **Execute**.</span></span>

<span data-ttu-id="bfc97-133">In pochi secondi, verrà visualizzata una risposta HTTP 201 nell'elenco delle sessioni hello, indice hello che indica che è stato creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="bfc97-133">In a few seconds, you should see an HTTP 201 response in hello session list, indicating hello index was created successfully.</span></span>

<span data-ttu-id="bfc97-134">Se si verificano HTTP 504, verificare il che URL hello specifichi HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bfc97-134">If you get HTTP 504, verify hello URL specifies HTTPS.</span></span> <span data-ttu-id="bfc97-135">Se viene visualizzato HTTP 400 o 404, tooverify corpo di controllo hello richiesta si sono verificati errori di copia e Incolla.</span><span class="sxs-lookup"><span data-stu-id="bfc97-135">If you see HTTP 400 or 404, check hello request body tooverify there were no copy-paste errors.</span></span> <span data-ttu-id="bfc97-136">Un HTTP 403 indica in genere un problema con hello chiave api (una chiave non valida o un problema di sintassi di specifica la chiave api hello).</span><span class="sxs-lookup"><span data-stu-id="bfc97-136">An HTTP 403 typically indicates a problem with hello api-key (either an invalid key or a syntax problem with how hello api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="bfc97-137">Caricare i documenti</span><span class="sxs-lookup"><span data-stu-id="bfc97-137">Load documents</span></span>
<span data-ttu-id="bfc97-138">In hello **Composer** scheda documenti toopost richiesta avrà un aspetto simile al seguente hello.</span><span class="sxs-lookup"><span data-stu-id="bfc97-138">On hello **Composer** tab, your request toopost documents will look like hello following.</span></span> <span data-ttu-id="bfc97-139">il corpo di Hello di hello richiesta contiene dati di ricerca hello per 4 hotel.</span><span class="sxs-lookup"><span data-stu-id="bfc97-139">hello body of hello request contains hello search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="bfc97-140">Selezionare **POST**.</span><span class="sxs-lookup"><span data-stu-id="bfc97-140">Select **POST**.</span></span>
2. <span data-ttu-id="bfc97-141">Immettere un URL che inizia con HTTPS, seguito dall'URL del servizio e quindi da "/indexes/<'nomeindice'>/docs/index?api-version=2016-09-01".</span><span class="sxs-lookup"><span data-stu-id="bfc97-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="bfc97-142">URL completo di Hello dovrebbe essere simile toohello esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="bfc97-142">hello full URL should look similar toohello following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="bfc97-143">Intestazione della richiesta deve essere hello stesso come in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bfc97-143">Request Header should be hello same as before.</span></span> <span data-ttu-id="bfc97-144">Tenere presente che è stato sostituito host hello e la chiave api con i valori validi per il servizio.</span><span class="sxs-lookup"><span data-stu-id="bfc97-144">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="bfc97-145">Hello corpo della richiesta contiene quattro hotel indice con documenti toobe toohello aggiunto.</span><span class="sxs-lookup"><span data-stu-id="bfc97-145">hello Request Body contains four documents toobe added toohello hotels index.</span></span>

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
             "hotelName": "Fancy Stay",
             "category": "Luxury",
             "tags": ["pool", "view", "wifi", "concierge"],
             "parkingIncluded": false,
             "smokingAllowed": false,
             "lastRenovationDate": "2010-06-27T00:00:00Z",
             "rating": 5,
             "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "2",
             "baseRate": 79.99,
             "description": "Cheapest hotel in town",
             "hotelName": "Roach Motel",
             "category": "Budget",
             "tags": ["motel", "budget"],
             "parkingIncluded": true,
             "smokingAllowed": true,
             "lastRenovationDate": "1982-04-28T00:00:00Z",
             "rating": 1,
             "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. <span data-ttu-id="bfc97-146">Fare clic su **Execute**.</span><span class="sxs-lookup"><span data-stu-id="bfc97-146">Click **Execute**.</span></span>

<span data-ttu-id="bfc97-147">In pochi secondi, verrà visualizzata una risposta HTTP 200 nell'elenco delle sessioni hello.</span><span class="sxs-lookup"><span data-stu-id="bfc97-147">In a few seconds, you should see an HTTP 200 response in hello session list.</span></span> <span data-ttu-id="bfc97-148">Ciò indica hello documenti sono stati creati correttamente.</span><span class="sxs-lookup"><span data-stu-id="bfc97-148">This indicates hello documents were created successfully.</span></span> <span data-ttu-id="bfc97-149">Se viene visualizzato un 207, almeno un documento non è stato possibile tooupload.</span><span class="sxs-lookup"><span data-stu-id="bfc97-149">If you get a 207, at least one document failed tooupload.</span></span> <span data-ttu-id="bfc97-150">Se si verifica un errore 404, si verifica un errore di sintassi nell'intestazione di hello o corpo della richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="bfc97-150">If you get a 404, you have a syntax error in either hello header or body of hello request.</span></span>

## <a name="query-hello-index"></a><span data-ttu-id="bfc97-151">Indice di query hello</span><span class="sxs-lookup"><span data-stu-id="bfc97-151">Query hello index</span></span>
<span data-ttu-id="bfc97-152">Ora che l'indice e i documenti sono stati caricati, è possibile eseguire query su di essi.</span><span class="sxs-lookup"><span data-stu-id="bfc97-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="bfc97-153">In hello **Composer** scheda, un **ottenere** comando che esegue una query del servizio avrà un aspetto simile toohello seguente cattura di schermata.</span><span class="sxs-lookup"><span data-stu-id="bfc97-153">On hello **Composer** tab, a **GET** command that queries your service will look similar toohello following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="bfc97-154">Selezionare **GET**.</span><span class="sxs-lookup"><span data-stu-id="bfc97-154">Select **GET**.</span></span>
2. <span data-ttu-id="bfc97-155">Immettere un URL che inizia con HTTPS, seguito dall'URL del servizio, seguito da "/indexes/<'nome indice'>/docs?", seguito dai parametri di query.</span><span class="sxs-lookup"><span data-stu-id="bfc97-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="bfc97-156">A titolo esemplificativo, utilizzare hello URL seguente, sostituendo il nome di host di esempio hello con uno valido per il servizio.</span><span class="sxs-lookup"><span data-stu-id="bfc97-156">By way of example, use hello following URL, replacing hello sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="bfc97-157">Questa query cerca hello termine "motel" e recupera le categorie di facet per classificazioni.</span><span class="sxs-lookup"><span data-stu-id="bfc97-157">This query searches on hello term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="bfc97-158">Intestazione della richiesta deve essere hello stesso come in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bfc97-158">Request Header should be hello same as before.</span></span> <span data-ttu-id="bfc97-159">Tenere presente che è stato sostituito host hello e la chiave api con i valori validi per il servizio.</span><span class="sxs-lookup"><span data-stu-id="bfc97-159">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="bfc97-160">codice di risposta Hello deve essere di 200 e output di risposta di hello dovrebbe essere simile toohello seguente cattura di schermata.</span><span class="sxs-lookup"><span data-stu-id="bfc97-160">hello response code should be 200, and hello response output should look similar toohello following screen shot.</span></span>

   ![][4]

<span data-ttu-id="bfc97-161">Hello query di esempio seguente è tratto dall'hello [operazione di indice di ricerca (API di ricerca di Azure)](http://msdn.microsoft.com/library/dn798927.aspx) su MSDN.</span><span class="sxs-lookup"><span data-stu-id="bfc97-161">hello following example query is from hello [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="bfc97-162">Molte delle query di esempio hello in questo argomento include spazi, che non sono consentiti in Fiddler.</span><span class="sxs-lookup"><span data-stu-id="bfc97-162">Many of hello example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="bfc97-163">Sostituire ogni spazio con il carattere + prima di incollare in hello stringa di query prima di tentare di query hello in Fiddler.</span><span class="sxs-lookup"><span data-stu-id="bfc97-163">Replace each space with a + character before pasting in hello query string before attempting hello query in Fiddler.</span></span>

<span data-ttu-id="bfc97-164">**Prima della sostituzione degli spazi:**</span><span class="sxs-lookup"><span data-stu-id="bfc97-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="bfc97-165">**Dopo la sostituzione degli spazi con il carattere +:**</span><span class="sxs-lookup"><span data-stu-id="bfc97-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a><span data-ttu-id="bfc97-166">query sul sistema hello</span><span class="sxs-lookup"><span data-stu-id="bfc97-166">Query hello system</span></span>
<span data-ttu-id="bfc97-167">È anche possibile eseguire una query hello sistema tooget conteggi e archiviazione uso del documento.</span><span class="sxs-lookup"><span data-stu-id="bfc97-167">You can also query hello system tooget document counts and storage consumption.</span></span> <span data-ttu-id="bfc97-168">In hello **Composer** , avrà un aspetto simile toohello seguente la richiesta e risposta hello verrà restituito un conteggio hello numero di documenti e lo spazio utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bfc97-168">On hello **Composer** tab, your request will look similar toohello following, and hello response will return a count for hello number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="bfc97-169">Selezionare **GET**.</span><span class="sxs-lookup"><span data-stu-id="bfc97-169">Select **GET**.</span></span>
2. <span data-ttu-id="bfc97-170">Immettere un URL che include l'URL del servizio, seguito da "/indexes/hotels/stats?api-version=2016-09-01":</span><span class="sxs-lookup"><span data-stu-id="bfc97-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="bfc97-171">Specificare l'intestazione della richiesta hello, sostituendo host hello e la chiave api con i valori validi per il servizio.</span><span class="sxs-lookup"><span data-stu-id="bfc97-171">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="bfc97-172">Lasciare vuoto il corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="bfc97-172">Leave hello request body empty.</span></span>
5. <span data-ttu-id="bfc97-173">Fare clic su **Execute**.</span><span class="sxs-lookup"><span data-stu-id="bfc97-173">Click **Execute**.</span></span> <span data-ttu-id="bfc97-174">Verrà visualizzato un codice di stato HTTP 200 nell'elenco delle sessioni hello.</span><span class="sxs-lookup"><span data-stu-id="bfc97-174">You should see an HTTP 200 status code in hello session list.</span></span> <span data-ttu-id="bfc97-175">Selezionare il movimento di hello registrato per il comando.</span><span class="sxs-lookup"><span data-stu-id="bfc97-175">Select hello entry posted for your command.</span></span>
6. <span data-ttu-id="bfc97-176">Fare clic su hello **controlli** scheda, fare clic su hello **intestazioni** scheda e quindi selezionare hello JSON formato.</span><span class="sxs-lookup"><span data-stu-id="bfc97-176">Click hello **Inspectors** tab, click hello **Headers** tab, and then select hello JSON format.</span></span> <span data-ttu-id="bfc97-177">Dovrebbe essere hello documento numero e dimensioni di archiviazione (in KB).</span><span class="sxs-lookup"><span data-stu-id="bfc97-177">You should see hello document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfc97-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bfc97-178">Next steps</span></span>
<span data-ttu-id="bfc97-179">Vedere [gestire il servizio di ricerca in Azure](search-manage.md) per toomanaging un approccio senza codice e l'utilizzo di ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfc97-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach toomanaging and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
