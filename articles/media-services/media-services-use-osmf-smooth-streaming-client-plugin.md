---
title: plug-in Streaming per Open origine Media Framework hello aaaSmooth
description: Informazioni su come toouse hello Azure Media Services Smooth Streaming di plug-in per hello Adobe Apri origine Media Framework.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6068151f-b6b0-4507-9346-f03416d3d572
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 3cf8e4679279344cf79c3f0e5b28f63adf88179d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a><span data-ttu-id="edd8c-103">Come tooUse hello Microsoft Smooth Streaming plug-in per hello Adobe Apri origine Media Framework</span><span class="sxs-lookup"><span data-stu-id="edd8c-103">How tooUse hello Microsoft Smooth Streaming Plugin for hello Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="edd8c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="edd8c-104">Overview</span></span>
<span data-ttu-id="edd8c-105">Hello plug-in di Microsoft Smooth Streaming per Open Source Media Framework 2.0 (SS per OSMF) estende le funzionalità predefinite di hello di OSMF e aggiunge Microsoft Smooth Streaming toonew la riproduzione del contenuto e OSMF esistenti lettori.</span><span class="sxs-lookup"><span data-stu-id="edd8c-105">hello Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends hello default capabilities of OSMF and adds Microsoft Smooth Streaming content playback toonew and existing OSMF players.</span></span> <span data-ttu-id="edd8c-106">plug-in Hello aggiunge inoltre Smooth Streaming tooStrobe funzionalità riproduzione Media Playback (SMP).</span><span class="sxs-lookup"><span data-stu-id="edd8c-106">hello plugin also adds Smooth Streaming playback capabilities tooStrobe Media Playback (SMP).</span></span>

<span data-ttu-id="edd8c-107">In Smooth Streaming per OSMF sono incluse due versioni di plug-in:</span><span class="sxs-lookup"><span data-stu-id="edd8c-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="edd8c-108">Plug-in Static Smooth Streaming per OSMF (con estensione swc)</span><span class="sxs-lookup"><span data-stu-id="edd8c-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="edd8c-109">Plug-in Dynamic Smooth Streaming per OSMF (con estensione swf)</span><span class="sxs-lookup"><span data-stu-id="edd8c-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="edd8c-110">Questo documento si presuppone che il lettore di hello abbia una conoscenza generale di OSMF e OSMF plug-in. Per ulteriori informazioni su OSMF, vedere la documentazione di hello in hello [sito ufficiale di OSMF](http://osmf.org/).</span><span class="sxs-lookup"><span data-stu-id="edd8c-110">This document assumes that hello reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see hello documentation on hello [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="edd8c-111">Plug-in Smooth Streaming per OSMF 2.0</span><span class="sxs-lookup"><span data-stu-id="edd8c-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="edd8c-112">plug-in Hello supporta il caricamento e la riproduzione del contenuto Smooth Streaming su richiesta con hello seguenti caratteristiche:</span><span class="sxs-lookup"><span data-stu-id="edd8c-112">hello plugin supports loading and playback of on-demand Smooth Streaming content with hello following features:</span></span>

* <span data-ttu-id="edd8c-113">Riproduzione Smooth Streaming su richiesta (riproduzione, pausa, ricerca, arresto)</span><span class="sxs-lookup"><span data-stu-id="edd8c-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="edd8c-114">Riproduzione Smooth Streaming in diretta (riproduzione)</span><span class="sxs-lookup"><span data-stu-id="edd8c-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="edd8c-115">Funzioni DVR in diretta (pausa, ricerca, riproduzione DVR, modalità attiva)</span><span class="sxs-lookup"><span data-stu-id="edd8c-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="edd8c-116">Supporto per codec video: H.264</span><span class="sxs-lookup"><span data-stu-id="edd8c-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="edd8c-117">Supporto per codec audio: AAC</span><span class="sxs-lookup"><span data-stu-id="edd8c-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="edd8c-118">Commutazione tra più lingue per l'audio grazie alle API incorporate in OSMF</span><span class="sxs-lookup"><span data-stu-id="edd8c-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="edd8c-119">Selezione della qualità di riproduzione massima grazie alle API incorporate in OSMF</span><span class="sxs-lookup"><span data-stu-id="edd8c-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="edd8c-120">Sottotitoli collaterali con il plug-in per didascalie OSMF</span><span class="sxs-lookup"><span data-stu-id="edd8c-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="edd8c-121">Adobe&reg; Flash&reg; Player 11.4 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="edd8c-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="edd8c-122">In questa versione è supportato solo OSMF 2.0.</span><span class="sxs-lookup"><span data-stu-id="edd8c-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="edd8c-123">Funzionalità supportate e problemi noti</span><span class="sxs-lookup"><span data-stu-id="edd8c-123">Supported features and known issues</span></span>
<span data-ttu-id="edd8c-124">Per un elenco completo delle funzionalità supportate e problemi noti e funzionalità non supportate, vedere troppo[questo documento](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span><span class="sxs-lookup"><span data-stu-id="edd8c-124">For a full list of supported features, unsupported features and known issues, refer too[this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-hello-plugin"></a><span data-ttu-id="edd8c-125">Caricamento hello plug-in</span><span class="sxs-lookup"><span data-stu-id="edd8c-125">Loading hello Plugin</span></span>
<span data-ttu-id="edd8c-126">I plug-in OSMF possono essere caricati in modo statico (in fase di compilazione) o dinamico (in fase di esecuzione).</span><span class="sxs-lookup"><span data-stu-id="edd8c-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="edd8c-127">Hello Smooth Streaming plug-in per il download OSMF include versioni statiche e dinamiche.</span><span class="sxs-lookup"><span data-stu-id="edd8c-127">hello Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="edd8c-128">Caricamento statico: tooload in modo statico, un file di libreria statica (SWC) è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="edd8c-128">Static loading: tooload statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="edd8c-129">I plug-in statico vengono aggiunti come riferimento toohello progetti e unione all'interno di output finale hello file in fase di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="edd8c-129">Static plugins are added as a reference toohello projects and merge inside hello final output file at hello compile time.</span></span>
* <span data-ttu-id="edd8c-130">Caricamento dinamico: tooload in modo dinamico, precompilato (SWF) è richiesto un file.</span><span class="sxs-lookup"><span data-stu-id="edd8c-130">Dynamic loading: tooload dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="edd8c-131">I plug-in dinamico sono caricati in fase di esecuzione hello e non incluso nell'output di progetto hello.</span><span class="sxs-lookup"><span data-stu-id="edd8c-131">Dynamic plugins are loaded in hello runtime and not included in hello project output.</span></span> <span data-ttu-id="edd8c-132">(Output compilato) I plug-in dinamici possono essere caricati tramite i protocolli HTTP e FILE.</span><span class="sxs-lookup"><span data-stu-id="edd8c-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="edd8c-133">Per ulteriori informazioni sul caricamento statico e dinamico, vedere ufficiale hello [pagina plug-in OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="edd8c-133">For more information on static and dynamic loading, see hello official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="edd8c-134">Caricamento statico di Smooth Streaming per OSMF</span><span class="sxs-lookup"><span data-stu-id="edd8c-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="edd8c-135">frammento di codice Hello seguente viene illustrato come tooload hello SS di plug-in per OSMF in modo statico e riproduce un video di base utilizzando la classe MediaFactory OSMF.</span><span class="sxs-lookup"><span data-stu-id="edd8c-135">hello code snippet below shows how tooload hello SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="edd8c-136">Prima di includere hello SS per il codice OSMF, verificare che il riferimento di progetto hello include plug-in statico hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc".</span><span class="sxs-lookup"><span data-stu-id="edd8c-136">Before including hello SS for OSMF code, please ensure that hello project reference includes hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

```
package 
{

    import com.microsoft.azure.media.AdaptiveStreamingPluginInfo;

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;



    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;

            initMediaPlayer();

        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;

            pluginResource = new PluginInfoResource(new AdaptiveStreamingPluginInfo( )); 
            _mediaFactory.loadPlugin( pluginResource ); 
        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.
            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="edd8c-137">Caricamento dinamico di Smooth Streaming per OSMF</span><span class="sxs-lookup"><span data-stu-id="edd8c-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="edd8c-138">frammento di codice Hello seguente viene illustrato come tooload hello SS di plug-in per OSMF in modo dinamico e riproduce un video di base utilizzando una classe OSMF MediaFactory hello.</span><span class="sxs-lookup"><span data-stu-id="edd8c-138">hello code snippet below shows how tooload hello SS plugin for OSMF dynamically and play a basic video using hello OSMF MediaFactory class.</span></span> <span data-ttu-id="edd8c-139">Prima di includere hello SS per il codice OSMF, copiare la cartella del progetto hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" plug-in dinamico toohello se si desidera tooload utilizzando il protocollo FILE oppure copiare in un server web per il carico HTTP.</span><span class="sxs-lookup"><span data-stu-id="edd8c-139">Before including hello SS for OSMF code, copy hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin toohello project folder if you want tooload using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="edd8c-140">Non sussiste alcun tooinclude necessità "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" nei riferimenti al progetto hello.</span><span class="sxs-lookup"><span data-stu-id="edd8c-140">There is no need tooinclude "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in hello project references.</span></span>

<span data-ttu-id="edd8c-141">pacchetto {</span><span class="sxs-lookup"><span data-stu-id="edd8c-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets hello size of hello SWF

    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;
            initMediaPlayer();
        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs toohost a valid crossdomain.xml file tooallow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.

            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="edd8c-142">}</span><span class="sxs-lookup"><span data-stu-id="edd8c-142">}</span></span>

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a><span data-ttu-id="edd8c-143">Strobe Media Playback con hello plug-in dinamico ODMF SS</span><span class="sxs-lookup"><span data-stu-id="edd8c-143">Strobe Media  Playback with hello SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="edd8c-144">è compatibile con Hello Smooth Streaming per OSMF dinamica plugin [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span><span class="sxs-lookup"><span data-stu-id="edd8c-144">hello Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="edd8c-145">È possibile utilizzare hello SS per OSMF tooSMP la riproduzione del contenuto di Smooth Streaming tooadd di plug-in.</span><span class="sxs-lookup"><span data-stu-id="edd8c-145">You can use hello SS for OSMF plugin tooadd Smooth Streaming content playback tooSMP.</span></span> <span data-ttu-id="edd8c-146">toodo, questa copia "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" in un server web per il carico HTTP utilizzando hello seguendo i passaggi:</span><span class="sxs-lookup"><span data-stu-id="edd8c-146">toodo this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using hello following steps:</span></span>

1. <span data-ttu-id="edd8c-147">Sfoglia hello [pagina Installazione Strobe Media Playback](http://osmf.org/dev/2.0gm/setup.html).</span><span class="sxs-lookup"><span data-stu-id="edd8c-147">Browse hello [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="edd8c-148">Consente di impostare hello src tooa Smooth Streaming origine, (ad esempio http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span><span class="sxs-lookup"><span data-stu-id="edd8c-148">Set hello src tooa Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="edd8c-149">Apportare modifiche alla configurazione di hello desiderato e fare clic su Anteprima e aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="edd8c-149">Make hello desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="edd8c-150">**Nota** Per il server Web del contenuto deve essere presente un file crossdomain.xml valido.</span><span class="sxs-lookup"><span data-stu-id="edd8c-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="edd8c-151">Copiare e incollare hello codice tooa semplice pagina HTML utilizzando un editor di testo, come nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="edd8c-151">Copy and paste hello code tooa simple HTML page using your favorite text editor, such as in hello following example:</span></span>

        <html>
        <body>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest &autoPlay=true"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars=" src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true">
        </embed>
        </object>
        </body>
        </html>



1. <span data-ttu-id="edd8c-152">Aggiungere toohello plug-in Smooth Streaming per OSMF codice di incorporamento e salvare.</span><span class="sxs-lookup"><span data-stu-id="edd8c-152">Add Smooth Streaming OSMF plugin toohello embed code and save.</span></span>
   
        <html>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10">
        </embed>
        </object>
        </html>
2. <span data-ttu-id="edd8c-153">Salvare una pagina HTML e pubblicare tooa web server.</span><span class="sxs-lookup"><span data-stu-id="edd8c-153">Save your HTML page and publish tooa web server.</span></span> <span data-ttu-id="edd8c-154">Sfoglia toohello pubblicati pagina web mediante i Preferiti Flash&reg; Player abilitato browser Internet (Internet Explorer, Chrome, Firefox, così via).</span><span class="sxs-lookup"><span data-stu-id="edd8c-154">Browse toohello published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="edd8c-155">Riprodurre il contenuto Smooth Streaming in Adobe&reg; Flash&reg; Player.</span><span class="sxs-lookup"><span data-stu-id="edd8c-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="edd8c-156">Per ulteriori informazioni sullo sviluppo di OSMF generale, vedere ufficiale hello [pagina sviluppo OSMF](http://osmf.org/resources.html).</span><span class="sxs-lookup"><span data-stu-id="edd8c-156">For more information on general OSMF development, please see hello official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="edd8c-157">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="edd8c-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="edd8c-158">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="edd8c-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="edd8c-159">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="edd8c-159">See Also</span></span>
[<span data-ttu-id="edd8c-160">Plug-in di streaming adattivo Microsoft per aggiornamento OSMF</span><span class="sxs-lookup"><span data-stu-id="edd8c-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

