---
title: aaaGet avviato con ricerca di Azure in Node.js | Documenti Microsoft
description: Illustra la creazione di un'applicazione di ricerca in un servizio di ricerca cloud ospitato in Azure usando Node.js come linguaggio di programmazione.
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="e495c-103">Introduzione a Ricerca di Azure in Node.js</span><span class="sxs-lookup"><span data-stu-id="e495c-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e495c-104">Portale</span><span class="sxs-lookup"><span data-stu-id="e495c-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="e495c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="e495c-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="e495c-106">Informazioni su come toobuild un Node.js personalizzato ricerca applicazione che utilizza la ricerca di Azure per la sua esperienza di ricerca.</span><span class="sxs-lookup"><span data-stu-id="e495c-106">Learn how toobuild a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="e495c-107">Questa esercitazione viene utilizzato hello [API REST di Azure ricerca](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello oggetti e operazioni in questo esercizio.</span><span class="sxs-lookup"><span data-stu-id="e495c-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="e495c-108">È stato usato [Node.js](https://Nodejs.org) e NPM, [Sublime 3 testo](http://www.sublimetext.com/3)e Windows PowerShell in Windows 8.1 toodevelop e testare questo codice.</span><span class="sxs-lookup"><span data-stu-id="e495c-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 toodevelop and test this code.</span></span>

<span data-ttu-id="e495c-109">toorun in questo esempio, è necessario un servizio di ricerca di Azure, che è possibile iscriversi a in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e495c-109">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e495c-110">Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per istruzioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="e495c-110">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-hello-data"></a><span data-ttu-id="e495c-111">Informazioni sui dati hello</span><span class="sxs-lookup"><span data-stu-id="e495c-111">About hello data</span></span>
<span data-ttu-id="e495c-112">Questa applicazione di esempio utilizza i dati di hello [Italia geologiche servizi (USG)](http://geonames.usgs.gov/domestic/download_data.htm)filtro sulle dimensioni di hello lo stato di Rhode Island tooreduce hello set di dati.</span><span class="sxs-lookup"><span data-stu-id="e495c-112">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="e495c-113">Verrà utilizzata questa toobuild dati un'applicazione di ricerca che restituisce gli edifici punti di riferimento, ad esempio ospedale un numero e scuole, nonché funzionalità geologiche come flussi e laghi Summit.</span><span class="sxs-lookup"><span data-stu-id="e495c-113">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="e495c-114">In questa applicazione hello **DataIndexer** programma compila e carica hello indice utilizzando un [indicizzatore](https://msdn.microsoft.com/library/azure/dn798918.aspx) costrutto, recupero hello filtrati soltanto set di dati da un Database SQL di Azure pubblico.</span><span class="sxs-lookup"><span data-stu-id="e495c-114">In this application, hello **DataIndexer** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="e495c-115">Connessione e credenziali origine dati online toohello di informazioni viene fornita nel codice programma hello.</span><span class="sxs-lookup"><span data-stu-id="e495c-115">Credentials and connection information toohello online data source is provided in hello program code.</span></span> <span data-ttu-id="e495c-116">Non è necessaria ulteriore configurazione.</span><span class="sxs-lookup"><span data-stu-id="e495c-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="e495c-117">In questo set di dati toostay in limite dei documenti di hello disponibile a livello di prezzo 10.000 hello è stato applicato un filtro.</span><span class="sxs-lookup"><span data-stu-id="e495c-117">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="e495c-118">Se si utilizza il livello standard di hello, questo limite non si applica.</span><span class="sxs-lookup"><span data-stu-id="e495c-118">If you use hello standard tier, this limit does not apply.</span></span> <span data-ttu-id="e495c-119">Per altre informazioni sulla capacità per ogni piano tariffario, vedere [Limiti del servizio di ricerca](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="e495c-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="e495c-120">Trovare il nome del servizio hello e la chiave api del servizio di ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="e495c-120">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="e495c-121">Dopo aver creato il servizio di hello, restituire toohello tooget portale hello URL o `api-key`.</span><span class="sxs-lookup"><span data-stu-id="e495c-121">After you create hello service, return toohello portal tooget hello URL or `api-key`.</span></span> <span data-ttu-id="e495c-122">Connessioni tooyour servizio di ricerca, è necessario disporre sia URL hello e un `api-key` chiamata hello tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="e495c-122">Connections tooyour Search service require that you have both hello URL and an `api-key` tooauthenticate hello call.</span></span>

1. <span data-ttu-id="e495c-123">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e495c-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e495c-124">Nella barra di spostamento hello, fare clic su **servizio di ricerca** toolist il provisioning di tutti i servizi di ricerca di Azure per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="e495c-124">In hello jump bar, click **Search service** toolist all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="e495c-125">Selezionare servizio hello da toouse.</span><span class="sxs-lookup"><span data-stu-id="e495c-125">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="e495c-126">Nel dashboard del servizio hello, dovrebbe essere riquadri per informazioni essenziali, ad esempio di icona per l'accesso alle chiavi amministratore hello hello.</span><span class="sxs-lookup"><span data-stu-id="e495c-126">On hello service dashboard, you should see tiles for essential information, such as hello key icon for accessing hello admin keys.</span></span>
5. <span data-ttu-id="e495c-127">Copiare l'URL del servizio hello, una chiave amministratore e una chiave di query.</span><span class="sxs-lookup"><span data-stu-id="e495c-127">Copy hello service URL, an admin key, and a query key.</span></span> <span data-ttu-id="e495c-128">È necessario in seguito tutti e tre quando vengono aggiunte toohello config.js file.</span><span class="sxs-lookup"><span data-stu-id="e495c-128">You need all three later when you add them toohello config.js file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="e495c-129">Scaricare i file di esempio hello</span><span class="sxs-lookup"><span data-stu-id="e495c-129">Download hello sample files</span></span>
<span data-ttu-id="e495c-130">Utilizzare uno dei seguenti approcci toodownload hello-esempio hello.</span><span class="sxs-lookup"><span data-stu-id="e495c-130">Use either one of hello following approaches toodownload hello sample.</span></span>

1. <span data-ttu-id="e495c-131">Andare troppo[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="e495c-131">Go too[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="e495c-132">Fare clic su **ZIP di Download**, salvare file con estensione zip hello e quindi estrarre tutti i file hello in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="e495c-132">Click **Download ZIP**, save hello .zip file, and then extract all hello files it contains.</span></span>

<span data-ttu-id="e495c-133">Tutte le successive modifiche e le istruzioni di esecuzione vengono effettuate sui file in questa cartella.</span><span class="sxs-lookup"><span data-stu-id="e495c-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="e495c-134">Aggiornare config.js hello.</span><span class="sxs-lookup"><span data-stu-id="e495c-134">Update hello config.js.</span></span> <span data-ttu-id="e495c-135">con l'URL del servizio di ricerca e la chiave API</span><span class="sxs-lookup"><span data-stu-id="e495c-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="e495c-136">Utilizzando hello URL e la chiave api copiato in precedenza, specificare l'URL di hello, chiave di amministrazione e della chiave di query nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e495c-136">Using hello URL and api-key that you copied earlier, specify hello URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="e495c-137">Le chiavi di amministrazione forniscono il controllo completo sulle operazioni del servizio, incluse creazione ed eliminazione di un indice e caricamento di documenti.</span><span class="sxs-lookup"><span data-stu-id="e495c-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="e495c-138">Al contrario, le chiavi di query sono per le operazioni di sola lettura, in genere utilizzate dalle applicazioni client che si connettono tooAzure ricerca.</span><span class="sxs-lookup"><span data-stu-id="e495c-138">In contrast, query keys are for read-only operations, typically used by client applications that connect tooAzure Search.</span></span>

<span data-ttu-id="e495c-139">In questo esempio, si includono query hello toohelp chiave ribadire hello consigliata per l'utilizzo di una chiave di query hello nelle applicazioni client.</span><span class="sxs-lookup"><span data-stu-id="e495c-139">In this sample, we include hello query key toohelp reinforce hello best practice of using hello query key in client applications.</span></span>

<span data-ttu-id="e495c-140">Hello seguente schermata mostra **config.js** aperto in un editor di testo con hello rilevante movimenti delimitato in modo da poter visualizzare in file hello tooupdate con hello valori che è valido per il servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="e495c-140">hello following screenshot shows **config.js** open in a text editor, with hello relevant entries demarcated so that you can see where tooupdate hello file with hello values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a><span data-ttu-id="e495c-141">Host di un ambiente di runtime per l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="e495c-141">Host a runtime environment for hello sample</span></span>
<span data-ttu-id="e495c-142">esempio Hello richiede un server HTTP, che è possibile installare a livello globale tramite npm.</span><span class="sxs-lookup"><span data-stu-id="e495c-142">hello sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="e495c-143">Utilizzare una finestra di PowerShell per i seguenti comandi hello.</span><span class="sxs-lookup"><span data-stu-id="e495c-143">Use a PowerShell window for hello following commands.</span></span>

1. <span data-ttu-id="e495c-144">Esplorazione delle cartelle toohello contenente hello **package. JSON** file.</span><span class="sxs-lookup"><span data-stu-id="e495c-144">Navigate toohello folder that contains hello **package.json** file.</span></span>
2. <span data-ttu-id="e495c-145">Digitare `npm install`.</span><span class="sxs-lookup"><span data-stu-id="e495c-145">Type `npm install`.</span></span>
3. <span data-ttu-id="e495c-146">Digitare `npm install -g http-server`.</span><span class="sxs-lookup"><span data-stu-id="e495c-146">Type `npm install -g http-server`.</span></span>

## <a name="build-hello-index-and-run-hello-application"></a><span data-ttu-id="e495c-147">Compilare hello indice ed eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e495c-147">Build hello index and run hello application</span></span>
1. <span data-ttu-id="e495c-148">Digitare `npm run indexDocuments`.</span><span class="sxs-lookup"><span data-stu-id="e495c-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="e495c-149">Digitare `npm run build`.</span><span class="sxs-lookup"><span data-stu-id="e495c-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="e495c-150">Digitare `npm run start_server`.</span><span class="sxs-lookup"><span data-stu-id="e495c-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="e495c-151">Inserire nel browser l'indirizzo `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="e495c-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="e495c-152">Eseguire ricerche sui dati dei servizi geologici degli Stati Uniti</span><span class="sxs-lookup"><span data-stu-id="e495c-152">Search on USGS data</span></span>
<span data-ttu-id="e495c-153">Hello soltanto set di dati include i record che sono rilevante toohello lo stato di Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="e495c-153">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="e495c-154">Se si fa clic **ricerca** su una casella di ricerca vuoto, ottenere voci primi 50 hello, hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="e495c-154">If you click **Search** on an empty search box, you get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="e495c-155">Immettendo un termine di ricerca offre il motore di ricerca hello qualcosa toogo in.</span><span class="sxs-lookup"><span data-stu-id="e495c-155">Entering a search term gives hello search engine something toogo on.</span></span> <span data-ttu-id="e495c-156">Provare a immettere un nome locale.</span><span class="sxs-lookup"><span data-stu-id="e495c-156">Try entering a regional name.</span></span> <span data-ttu-id="e495c-157">"Roger Williams" è stato governor prima di hello del Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="e495c-157">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="e495c-158">Numerosi parchi, edifici e scuole prendono il suo nome.</span><span class="sxs-lookup"><span data-stu-id="e495c-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="e495c-159">È inoltre possibile tentare con uno dei termini seguenti:</span><span class="sxs-lookup"><span data-stu-id="e495c-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="e495c-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="e495c-160">Pawtucket</span></span>
* <span data-ttu-id="e495c-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="e495c-161">Pembroke</span></span>
* <span data-ttu-id="e495c-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="e495c-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="e495c-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e495c-163">Next steps</span></span>
<span data-ttu-id="e495c-164">Si tratta di hello prima esercitazione ricerca di Azure in base a Node.js e hello soltanto set di dati.</span><span class="sxs-lookup"><span data-stu-id="e495c-164">This is hello first Azure Search tutorial based on Node.js and hello USGS dataset.</span></span> <span data-ttu-id="e495c-165">Nel corso del tempo, toodemonstrate questa esercitazione verrà esteso le funzionalità di ricerca aggiuntive è toouse in soluzioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="e495c-165">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="e495c-166">Se si dispone già delle nozioni di base di Ricerca di Azure, è possibile usare questo esempio come base di prova per i suggerimenti di alternative (query di suggerimento per la digitazione e completamento automatico), filtri ed esplorazione basata su facet.</span><span class="sxs-lookup"><span data-stu-id="e495c-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="e495c-167">È inoltre possibile migliorare alla pagina dei risultati di ricerca hello aggiungendo i conteggi e l'invio in batch di documenti in modo che gli utenti possono spostarsi tra i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="e495c-167">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="e495c-168">TooAzure nuova ricerca?</span><span class="sxs-lookup"><span data-stu-id="e495c-168">New tooAzure Search?</span></span> <span data-ttu-id="e495c-169">È consigliabile tentare altri toodevelop esercitazioni la comprensione di ciò che è possibile creare.</span><span class="sxs-lookup"><span data-stu-id="e495c-169">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="e495c-170">Visitare il nostro [pagina della documentazione](https://azure.microsoft.com/documentation/services/search/) toofind più risorse.</span><span class="sxs-lookup"><span data-stu-id="e495c-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="e495c-171">È inoltre possibile visualizzare i collegamenti di hello nel nostro [elenco Video e un'esercitazione](search-video-demo-tutorial-list.md) tooaccess ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="e495c-171">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
