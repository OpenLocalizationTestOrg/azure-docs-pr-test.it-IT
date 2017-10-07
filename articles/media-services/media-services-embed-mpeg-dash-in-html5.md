---
title: aaaEmbedding un MPEG-DASH Video con Streaming adattivo in un'applicazione HTML5 con DASH.js | Documenti Microsoft
description: Questo argomento viene illustrato come un MPEG-DASH Video con Streaming adattivo in un'applicazione HTML5 con DASH.js tooembed.
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
ms.openlocfilehash: a73713d20f95262654532b94576ae9669d829354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="1a401-103">Integrazione di uno streaming video adattivo MPEG-DASH in un'applicazione HTML5 con DASH.js</span><span class="sxs-lookup"><span data-stu-id="1a401-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="1a401-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1a401-104">Overview</span></span>
<span data-ttu-id="1a401-105">MPEG-DASH è uno standard ISO per il flusso adattivo di contenuto video, che offre vantaggi significativi per gli utenti che desiderano toodeliver adattivo di alta qualità dello streaming video output hello.</span><span class="sxs-lookup"><span data-stu-id="1a401-105">MPEG-DASH is an ISO standard for hello adaptive streaming of video content, which offers significant benefits for those who wish toodeliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="1a401-106">Con MPEG-DASH flusso video hello verrà eliminata automaticamente definizione inferiore tooa quando congestione rete hello.</span><span class="sxs-lookup"><span data-stu-id="1a401-106">With MPEG-DASH, hello video stream will automatically drop tooa lower definition when hello network becomes congested.</span></span> <span data-ttu-id="1a401-107">In questo modo si riduce la probabilità hello del Visualizzatore di hello visualizzare un video "sospeso" mentre player hello Scarica hello successivamente alcuni tooplay secondi (noto anche come memorizzazione nel buffer).</span><span class="sxs-lookup"><span data-stu-id="1a401-107">This reduces hello likelihood of hello viewer seeing a "paused" video while hello player downloads hello next few seconds tooplay (aka buffering).</span></span> <span data-ttu-id="1a401-108">Riduce la congestione della rete, lettore video hello restituirà a sua volta tooa il flusso di qualità superiore.</span><span class="sxs-lookup"><span data-stu-id="1a401-108">As network congestion reduces, hello video player will in turn return tooa higher quality stream.</span></span> <span data-ttu-id="1a401-109">Questa possibilità tooadapt hello larghezza di banda richiesta anche i risultati in un'ora di inizio più veloce per video.</span><span class="sxs-lookup"><span data-stu-id="1a401-109">This ability tooadapt hello bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="1a401-110">Che indica che alcuni secondi prima di hello possa essere riprodotto in un segmento di qualità inferiore fast per scaricare e quindi Esegui di qualità più elevata tooa dopo sufficiente contenuto memorizzato nel buffer.</span><span class="sxs-lookup"><span data-stu-id="1a401-110">That means that hello first few seconds can be played in a fast-to-download lower quality segment and then step up tooa higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="1a401-111">Dash.js è un lettore video MPEG-DASH open source scritto in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1a401-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="1a401-112">L'obiettivo è tooprovide un lettore affidabile, multipiattaforma da riusare liberamente in applicazioni che richiedono la riproduzione video.</span><span class="sxs-lookup"><span data-stu-id="1a401-112">Its goal is tooprovide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="1a401-113">Fornisce la riproduzione MPEG-DASH in qualsiasi browser che supporta hello W3C Media origine Extensions (MSE), ovvero oggi Chrome, Microsoft Edge e IE11 (altri browser hanno manifestato loro toosupport preventivo MSE).</span><span class="sxs-lookup"><span data-stu-id="1a401-113">It provides MPEG-DASH playback in any browser that supports hello W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent toosupport MSE).</span></span> <span data-ttu-id="1a401-114">Per ulteriori informazioni su DASH.js, js vedere repository dash.js GitHub di hello.</span><span class="sxs-lookup"><span data-stu-id="1a401-114">For more information about DASH.js, js see hello GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="1a401-115">Creazione di un lettore di streaming video basato su browser</span><span class="sxs-lookup"><span data-stu-id="1a401-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="1a401-116">toocreate una semplice pagina web che consente di visualizzare un lettore video con hello previsto controlla tali una riproduzione, pausa, riavvolgimento e così via, è necessario:</span><span class="sxs-lookup"><span data-stu-id="1a401-116">toocreate a simple web page that displays a video player with hello expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="1a401-117">Creare una pagina HTML</span><span class="sxs-lookup"><span data-stu-id="1a401-117">Create an HTML page</span></span>
2. <span data-ttu-id="1a401-118">Aggiungere tag video hello</span><span class="sxs-lookup"><span data-stu-id="1a401-118">Add hello video tag</span></span>
3. <span data-ttu-id="1a401-119">Aggiungere il giocatore dash.js hello</span><span class="sxs-lookup"><span data-stu-id="1a401-119">Add hello dash.js player</span></span>
4. <span data-ttu-id="1a401-120">Inizializzare il lettore hello</span><span class="sxs-lookup"><span data-stu-id="1a401-120">Initialize hello player</span></span>
5. <span data-ttu-id="1a401-121">Aggiungere lo stile CSS</span><span class="sxs-lookup"><span data-stu-id="1a401-121">Add some CSS style</span></span>
6. <span data-ttu-id="1a401-122">Visualizzare i risultati in un browser che implementa MSE hello</span><span class="sxs-lookup"><span data-stu-id="1a401-122">View hello results in a browser that implements MSE</span></span>

<span data-ttu-id="1a401-123">Inizializzazione player hello possono essere completate in un numero limitato di righe di codice JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1a401-123">Initializing hello player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="1a401-124">Utilizzando dash.js, è effettivamente tale video tooembed semplice MPEG-DASH nelle applicazioni basate su browser.</span><span class="sxs-lookup"><span data-stu-id="1a401-124">Using dash.js, it really is that simple tooembed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-hello-html-page"></a><span data-ttu-id="1a401-125">Creazione di hello pagina HTML</span><span class="sxs-lookup"><span data-stu-id="1a401-125">Creating hello HTML Page</span></span>
<span data-ttu-id="1a401-126">pagina HTML standard toocreate contenente hello, è innanzitutto Hello **video** elemento, salvare questo file come basicPlayer.html, come hello di esempio seguente viene illustrato:</span><span class="sxs-lookup"><span data-stu-id="1a401-126">hello first step is toocreate a standard HTML page containing hello **video** element, save this file as basicPlayer.html, as hello following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a><span data-ttu-id="1a401-127">Aggiunta di hello DASH.js Player</span><span class="sxs-lookup"><span data-stu-id="1a401-127">Adding hello DASH.js Player</span></span>
<span data-ttu-id="1a401-128">tooadd dash.js riferimento implementazione toohello applicazione hello, dovrai toograb hello dash.all.js file versione 1.0 di hello del progetto dash.js.</span><span class="sxs-lookup"><span data-stu-id="1a401-128">tooadd hello dash.js reference implementation toohello application, you’ll need toograb hello dash.all.js file from hello 1.0 release of dash.js project.</span></span> <span data-ttu-id="1a401-129">Questo deve essere salvato nella cartella JavaScript hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1a401-129">This should be saved in hello JavaScript folder of your application.</span></span> <span data-ttu-id="1a401-130">Questo file è un file di praticità mette insieme tutto il codice necessario dash.js hello in un singolo file.</span><span class="sxs-lookup"><span data-stu-id="1a401-130">This file is a convenience file that pulls together all hello necessary dash.js code into a single file.</span></span> <span data-ttu-id="1a401-131">Se si dispone di un aspetto intorno repository dash.js hello, verranno trovare hello singoli file, test di codice e così via, ma se si desidera toodo è usare dash.js, sarà file dash.all.js hello è necessario.</span><span class="sxs-lookup"><span data-stu-id="1a401-131">If you have a look around hello dash.js repository, you will find hello individual files, test code and much more, but if all you want toodo is use dash.js, then hello dash.all.js file is what you need.</span></span>

<span data-ttu-id="1a401-132">applicazioni di tooadd hello dash.js player tooyour, aggiungere una sezione head toohello al tag di script di basicPlayer.html:</span><span class="sxs-lookup"><span data-stu-id="1a401-132">tooadd hello dash.js player tooyour applications, add a script tag toohello head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="1a401-133">Successivamente, creare un lettore di hello tooinitialize funzione durante il caricamento pagina hello.</span><span class="sxs-lookup"><span data-stu-id="1a401-133">Next, create a function tooinitialize hello player when hello page loads.</span></span> <span data-ttu-id="1a401-134">Aggiungere lo script seguente dopo la riga hello in cui è stato caricato dash.all.js hello:</span><span class="sxs-lookup"><span data-stu-id="1a401-134">Add hello following script after hello line in which you load dash.all.js:</span></span>

    <script>
    // setup hello video element and attach it toohello Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="1a401-135">Questa funzione crea in primo luogo un elemento DashContext,</span><span class="sxs-lookup"><span data-stu-id="1a401-135">This function first creates a DashContext.</span></span> <span data-ttu-id="1a401-136">Si tratta di un'applicazione hello tooconfigure utilizzati per un ambiente di runtime specifica.</span><span class="sxs-lookup"><span data-stu-id="1a401-136">This is used tooconfigure hello application for a specific runtime environment.</span></span> <span data-ttu-id="1a401-137">Dal punto di vista tecnico, definisce le classi che hello framework injection dipendenza devono utilizzare durante la costruzione di un'applicazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="1a401-137">From a technical point of view, it defines hello classes that hello dependency injection framework should use when constructing hello application.</span></span> <span data-ttu-id="1a401-138">Nella maggior parte dei casi, si userà Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="1a401-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="1a401-139">Successivamente, creare un'istanza di classe primaria hello di framework dash.js hello, Media Player.</span><span class="sxs-lookup"><span data-stu-id="1a401-139">Next, instantiate hello primary class of hello dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="1a401-140">Questa classe contiene metodi, ad esempio necessari riprodurre e sospendere, gestisce la relazione hello con elemento video hello e gestiscono inoltre l'interpretazione di hello del file di supporto presentazione descrizione (MPD) hello che descrive toobe video di hello riprodotto base hello.</span><span class="sxs-lookup"><span data-stu-id="1a401-140">This class contains hello core methods needed such as play and pause, manages hello relationship with hello video element and also manages hello interpretation of hello Media Presentation Description (MPD) file which describes hello video toobe played.</span></span>

<span data-ttu-id="1a401-141">funzione Startup Hello di hello classe MediaPlayer viene chiamato tooensure tale lettore hello è pronto tooplay video.</span><span class="sxs-lookup"><span data-stu-id="1a401-141">hello startup() function of hello MediaPlayer class is called tooensure that hello player is ready tooplay video.</span></span> <span data-ttu-id="1a401-142">Tra l'altro questa funzione assicura che tutte le classi necessarie di hello (come definito dal contesto hello) sono state caricate.</span><span class="sxs-lookup"><span data-stu-id="1a401-142">Amongst other things this function ensures that all hello necessary classes (as defined by hello context) have been loaded.</span></span> <span data-ttu-id="1a401-143">Una volta player hello è pronto, è possibile collegare hello elemento video tooit funzione attachView() hello.</span><span class="sxs-lookup"><span data-stu-id="1a401-143">Once hello player is ready, you can attach hello video element tooit using hello attachView() function.</span></span> <span data-ttu-id="1a401-144">Questo consente di flusso video di hello MediaPlayer tooinject hello nell'elemento hello e inoltre controllare la riproduzione in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="1a401-144">This enables hello MediaPlayer tooinject hello video stream into hello element and also control playback as necessary.</span></span>

<span data-ttu-id="1a401-145">Passare l'URL di hello di hello MPD file toohello MediaPlayer in modo che conosce hello video è previsto tooplay.hello setupVideo() funzione appena creato sarà necessario toobe eseguiti pagina hello è completamente caricato.</span><span class="sxs-lookup"><span data-stu-id="1a401-145">Pass hello URL of hello MPD file toohello MediaPlayer so that it knows about hello video it is expected tooplay.hello setupVideo() function just created will need toobe executed once hello page has fully loaded.</span></span> <span data-ttu-id="1a401-146">Tale scopo utilizzare eventi onload hello hello dell'elemento del corpo.</span><span class="sxs-lookup"><span data-stu-id="1a401-146">Do this by using hello onload event of hello body element.</span></span> <span data-ttu-id="1a401-147">Modificare l'elemento <body> come segue:</span><span class="sxs-lookup"><span data-stu-id="1a401-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="1a401-148">Infine, impostare dimensioni hello hello video dell'elemento del CSS.</span><span class="sxs-lookup"><span data-stu-id="1a401-148">Finally, set hello size of hello video element using CSS.</span></span> <span data-ttu-id="1a401-149">In un ambiente di streaming adattivo, questo è particolarmente importante in quanto potrebbero cambiare dimensioni hello di hello video viene riprodotto durante la riproduzione adatta toochanging le condizioni della rete.</span><span class="sxs-lookup"><span data-stu-id="1a401-149">In an adaptive streaming environment, this is especially important because hello size of hello video being played may change as playback adapts toochanging network conditions.</span></span> <span data-ttu-id="1a401-150">In questa demo semplice semplicemente forzare hello elemento video toobe 80% della finestra del browser disponibili hello aggiungendo la seguente sezione di intestazione toohello CSS della pagina hello hello:</span><span class="sxs-lookup"><span data-stu-id="1a401-150">In this simple demo simply force hello video element toobe 80% of hello available browser window by adding hello following CSS toohello head section of hello page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="1a401-151">Riproduzione di un video</span><span class="sxs-lookup"><span data-stu-id="1a401-151">Playing a Video</span></span>
<span data-ttu-id="1a401-152">tooplay un video, il browser file basicPlayback.html hello e quindi la riproduzione su un lettore di hello visualizzato.</span><span class="sxs-lookup"><span data-stu-id="1a401-152">tooplay a video, point your browser at hello basicPlayback.html file and click play on hello video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="1a401-153">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="1a401-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1a401-154">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="1a401-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="1a401-155">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="1a401-155">See Also</span></span>
[<span data-ttu-id="1a401-156">Sviluppo di applicazioni di lettore video</span><span class="sxs-lookup"><span data-stu-id="1a401-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="1a401-157">Repository dash.js di GitHub</span><span class="sxs-lookup"><span data-stu-id="1a401-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

