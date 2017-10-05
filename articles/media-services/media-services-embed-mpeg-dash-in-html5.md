---
title: Integrazione di uno streaming video adattivo MPEG-DASH in un'applicazione HTML5 con DASH.js | Microsoft Docs
description: Questo argomento illustra come integrare un video in streaming adattivo MPEG-DASH in un'applicazione HTML5 con DASH.js.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 5aa0e7b6-f5c3-4cc1-aa33-ed16ea4780c2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 27ce6325773ba1f9fd9cd9ab9e07ea9f5e2488ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="3be68-103">Integrazione di uno streaming video adattivo MPEG-DASH in un'applicazione HTML5 con DASH.js</span><span class="sxs-lookup"><span data-stu-id="3be68-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="3be68-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="3be68-104">Overview</span></span>
<span data-ttu-id="3be68-105">MPEG-DASH è uno standard ISO per lo streaming adattivo di contenuti video che offre vantaggi significativi agli utenti che desiderano distribuire output di streaming video adattivo di alta qualità.</span><span class="sxs-lookup"><span data-stu-id="3be68-105">MPEG-DASH is an ISO standard for the adaptive streaming of video content, which offers significant benefits for those who wish to deliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="3be68-106">Con MPEG-DASH il flusso video viene automaticamente impostato a una definizione inferiore quando si verificano situazioni di congestione sulla rete.</span><span class="sxs-lookup"><span data-stu-id="3be68-106">With MPEG-DASH, the video stream will automatically drop to a lower definition when the network becomes congested.</span></span> <span data-ttu-id="3be68-107">Questo riduce il rischio che il video si interrompa mentre il lettore scarica i secondi successivi da riprodurre (noto anche come buffering).</span><span class="sxs-lookup"><span data-stu-id="3be68-107">This reduces the likelihood of the viewer seeing a "paused" video while the player downloads the next few seconds to play (aka buffering).</span></span> <span data-ttu-id="3be68-108">Man mano che la congestione sulla rete si riduce, il lettore video torna a un flusso di qualità elevata.</span><span class="sxs-lookup"><span data-stu-id="3be68-108">As network congestion reduces, the video player will in turn return to a higher quality stream.</span></span> <span data-ttu-id="3be68-109">La possibilità di adattare la larghezza di banda richiesta riduce anche i tempi di avvio del video.</span><span class="sxs-lookup"><span data-stu-id="3be68-109">This ability to adapt the bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="3be68-110">I primi secondi, ad esempio, possono essere riprodotti con una qualità inferiore, rapida da scaricare, per poi passare a una qualità superiore nel momento in cui nel buffer è stato memorizzato contenuto sufficiente.</span><span class="sxs-lookup"><span data-stu-id="3be68-110">That means that the first few seconds can be played in a fast-to-download lower quality segment and then step up to a higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="3be68-111">Dash.js è un lettore video MPEG-DASH open source scritto in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3be68-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="3be68-112">È stato sviluppato per offrire un affidabile lettore multipiattaforma che possa essere liberamente riusato in applicazioni che richiedono la riproduzione video.</span><span class="sxs-lookup"><span data-stu-id="3be68-112">Its goal is to provide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="3be68-113">Offre funzionalità di riproduzione MPEG-DASH in qualsiasi browser che supportalo standard W3C Media Source Extensions (MSE), ovvero Chrome,  Microsoft Edge e IE11 (altri browser hanno manifestato l'intenzione di supportare MSE).</span><span class="sxs-lookup"><span data-stu-id="3be68-113">It provides MPEG-DASH playback in any browser that supports the W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent to support MSE).</span></span> <span data-ttu-id="3be68-114">Per altre informazioni su DASH.js, vedere la pagina relativa al repository dash.js di GitHub.</span><span class="sxs-lookup"><span data-stu-id="3be68-114">For more information about DASH.js, js see the GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="3be68-115">Creazione di un lettore di streaming video basato su browser</span><span class="sxs-lookup"><span data-stu-id="3be68-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="3be68-116">Per creare una pagina Web semplice che visualizzi un lettore video con i controlli previsti, quali riproduzione, pausa, riavvolgimento e così via, sarà necessario:</span><span class="sxs-lookup"><span data-stu-id="3be68-116">To create a simple web page that displays a video player with the expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="3be68-117">Creare una pagina HTML</span><span class="sxs-lookup"><span data-stu-id="3be68-117">Create an HTML page</span></span>
2. <span data-ttu-id="3be68-118">Aggiungere un tag video</span><span class="sxs-lookup"><span data-stu-id="3be68-118">Add the video tag</span></span>
3. <span data-ttu-id="3be68-119">Aggiungere il lettore dash.js</span><span class="sxs-lookup"><span data-stu-id="3be68-119">Add the dash.js player</span></span>
4. <span data-ttu-id="3be68-120">Inizializzare il lettore</span><span class="sxs-lookup"><span data-stu-id="3be68-120">Initialize the player</span></span>
5. <span data-ttu-id="3be68-121">Aggiungere lo stile CSS</span><span class="sxs-lookup"><span data-stu-id="3be68-121">Add some CSS style</span></span>
6. <span data-ttu-id="3be68-122">Visualizzare i risultati in un browser che implementa MSE</span><span class="sxs-lookup"><span data-stu-id="3be68-122">View the results in a browser that implements MSE</span></span>

<span data-ttu-id="3be68-123">L'inizializzazione del lettore può essere eseguita con poche righe di codice JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3be68-123">Initializing the player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="3be68-124">Usando dash.js, integrare video MPEG-DASH in applicazioni basate su browser è davvero molto semplice.</span><span class="sxs-lookup"><span data-stu-id="3be68-124">Using dash.js, it really is that simple to embed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-the-html-page"></a><span data-ttu-id="3be68-125">Creazione della pagina HTML</span><span class="sxs-lookup"><span data-stu-id="3be68-125">Creating the HTML Page</span></span>
<span data-ttu-id="3be68-126">Il primo passaggio consiste nel creare una pagina HTML standard contenente l'elemento **video** e salvare il file come basicPlayer.html, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="3be68-126">The first step is to create a standard HTML page containing the **video** element, save this file as basicPlayer.html, as the following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-the-dashjs-player"></a><span data-ttu-id="3be68-127">Aggiunta del lettore DASH.js</span><span class="sxs-lookup"><span data-stu-id="3be68-127">Adding the DASH.js Player</span></span>
<span data-ttu-id="3be68-128">Per aggiungere l'implementazione di riferimento dash.js all'applicazione, è necessario recuperare il file dash.all.js dalla versione 1.0 del progetto dash.js.</span><span class="sxs-lookup"><span data-stu-id="3be68-128">To add the dash.js reference implementation to the application, you’ll need to grab the dash.all.js file from the 1.0 release of dash.js project.</span></span> <span data-ttu-id="3be68-129">Il file deve essere quindi salvato nella cartella JavaScript dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3be68-129">This should be saved in the JavaScript folder of your application.</span></span> <span data-ttu-id="3be68-130">Si tratta di un file di riferimento che raccoglie tutto il codice dash.js necessario in un unico file.</span><span class="sxs-lookup"><span data-stu-id="3be68-130">This file is a convenience file that pulls together all the necessary dash.js code into a single file.</span></span> <span data-ttu-id="3be68-131">Esaminando l'archivio dash.js si potrà identificare i singoli file, il codice di test e molto altro, ma se si deve solo usare il file dash.js, questo sarà l'unico elemento effettivamente necessario.</span><span class="sxs-lookup"><span data-stu-id="3be68-131">If you have a look around the dash.js repository, you will find the individual files, test code and much more, but if all you want to do is use dash.js, then the dash.all.js file is what you need.</span></span>

<span data-ttu-id="3be68-132">Per aggiungere il lettore dash.js a un'applicazione, aggiungere un tag di script alla sezione di intestazione del file basicPlayer.html:</span><span class="sxs-lookup"><span data-stu-id="3be68-132">To add the dash.js player to your applications, add a script tag to the head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="3be68-133">Successivamente, creare una funzione per inizializzare il lettore al caricamento della pagina.</span><span class="sxs-lookup"><span data-stu-id="3be68-133">Next, create a function to initialize the player when the page loads.</span></span> <span data-ttu-id="3be68-134">Aggiungere lo script seguente dopo la riga in cui si carica dash.all.js:</span><span class="sxs-lookup"><span data-stu-id="3be68-134">Add the following script after the line in which you load dash.all.js:</span></span>

    <script>
    // setup the video element and attach it to the Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="3be68-135">Questa funzione crea in primo luogo un elemento DashContext,</span><span class="sxs-lookup"><span data-stu-id="3be68-135">This function first creates a DashContext.</span></span> <span data-ttu-id="3be68-136">che consente di configurare l'applicazione per un ambiente di runtime specifico.</span><span class="sxs-lookup"><span data-stu-id="3be68-136">This is used to configure the application for a specific runtime environment.</span></span> <span data-ttu-id="3be68-137">Da un punto di vista tecnico, definisce le classi che il framework di inserimento delle dipendenze dovrà usare durante la creazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3be68-137">From a technical point of view, it defines the classes that the dependency injection framework should use when constructing the application.</span></span> <span data-ttu-id="3be68-138">Nella maggior parte dei casi, si userà Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="3be68-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="3be68-139">Successivamente, inizializza la classe primaria del framework dash.js, MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="3be68-139">Next, instantiate the primary class of the dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="3be68-140">Questa classe contiene i principali metodi necessari, ad esempio riproduzione e pausa, e gestisce sia la relazione con l'elemento video sia l'interpretazione del file Media Presentation Description (MPD) che descrive il video da riprodurre.</span><span class="sxs-lookup"><span data-stu-id="3be68-140">This class contains the core methods needed such as play and pause, manages the relationship with the video element and also manages the interpretation of the Media Presentation Description (MPD) file which describes the video to be played.</span></span>

<span data-ttu-id="3be68-141">Per verificare che il lettore sia pronto per la riproduzione del video, viene chiamata la funzione startup() della classe MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="3be68-141">The startup() function of the MediaPlayer class is called to ensure that the player is ready to play video.</span></span> <span data-ttu-id="3be68-142">Tra le altre cose, questa funzione controlla anche che siano state caricate tutte le classi necessarie (come definito dal contesto).</span><span class="sxs-lookup"><span data-stu-id="3be68-142">Amongst other things this function ensures that all the necessary classes (as defined by the context) have been loaded.</span></span> <span data-ttu-id="3be68-143">Quando il lettore è pronto, è possibile collegare l'elemento video mediante la funzione attachView().</span><span class="sxs-lookup"><span data-stu-id="3be68-143">Once the player is ready, you can attach the video element to it using the attachView() function.</span></span> <span data-ttu-id="3be68-144">In questo modo, MediaPlayer può inserire il flusso video nell'elemento e, se necessario, controllare la riproduzione.</span><span class="sxs-lookup"><span data-stu-id="3be68-144">This enables the MediaPlayer to inject the video stream into the element and also control playback as necessary.</span></span>

<span data-ttu-id="3be68-145">Passare l'URL del file MPD a MediaPlayer in modo che riconosca il video previsto per la riproduzione. Quando la pagina risulterà completamente caricata, sarà necessario eseguire la funzione setupVideo() appena creata.</span><span class="sxs-lookup"><span data-stu-id="3be68-145">Pass the URL of the MPD file to the MediaPlayer so that it knows about the video it is expected to play.The setupVideo() function just created will need to be executed once the page has fully loaded.</span></span> <span data-ttu-id="3be68-146">A questo scopo, è possibile usare l'evento onload dell'elemento del corpo.</span><span class="sxs-lookup"><span data-stu-id="3be68-146">Do this by using the onload event of the body element.</span></span> <span data-ttu-id="3be68-147">Modificare l'elemento <body> come segue:</span><span class="sxs-lookup"><span data-stu-id="3be68-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="3be68-148">Infine, imposta la dimensione dell'elemento video usando lo stile CSS.</span><span class="sxs-lookup"><span data-stu-id="3be68-148">Finally, set the size of the video element using CSS.</span></span> <span data-ttu-id="3be68-149">In un ambiente di streaming adattivo, questo passaggio è particolarmente importante poiché le dimensioni del video riprodotto possono variare mentre la riproduzione si adatta alle mutevoli condizioni di rete.</span><span class="sxs-lookup"><span data-stu-id="3be68-149">In an adaptive streaming environment, this is especially important because the size of the video being played may change as playback adapts to changing network conditions.</span></span> <span data-ttu-id="3be68-150">Questo semplice esempio forza l'elemento video all'80% della finestra del browser disponibile aggiungendo lo stile CSS seguente alla sezione di intestazione della pagina:</span><span class="sxs-lookup"><span data-stu-id="3be68-150">In this simple demo simply force the video element to be 80% of the available browser window by adding the following CSS to the head section of the page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="3be68-151">Riproduzione di un video</span><span class="sxs-lookup"><span data-stu-id="3be68-151">Playing a Video</span></span>
<span data-ttu-id="3be68-152">Per riprodurre un video, passare nel browser al file basicPlayback.html e fare clic sul pulsante di riproduzione sul lettore video visualizzato.</span><span class="sxs-lookup"><span data-stu-id="3be68-152">To play a video, point your browser at the basicPlayback.html file and click play on the video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="3be68-153">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="3be68-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3be68-154">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="3be68-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="3be68-155">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="3be68-155">See Also</span></span>
[<span data-ttu-id="3be68-156">Sviluppo di applicazioni di lettore video</span><span class="sxs-lookup"><span data-stu-id="3be68-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="3be68-157">Repository dash.js di GitHub</span><span class="sxs-lookup"><span data-stu-id="3be68-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

