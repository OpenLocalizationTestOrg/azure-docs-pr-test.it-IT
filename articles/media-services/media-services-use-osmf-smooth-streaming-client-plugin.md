---
title: Plug-in Smooth Streaming per Open Source Media Framework
description: Informazioni su come usare il plug-in Smooth Streaming di Servizi multimediali di Azure per Adobe Open Source Media Framework.
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
ms.openlocfilehash: 9c764f176ae75085320882de3fb26d8e7d52daaf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-the-microsoft-smooth-streaming-plugin-for-the-adobe-open-source-media-framework"></a><span data-ttu-id="c6984-103">Come usare il plug-in Microsoft Smooth Streaming per Adobe Open Source Media Framework</span><span class="sxs-lookup"><span data-stu-id="c6984-103">How to Use the Microsoft Smooth Streaming Plugin for the Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="c6984-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c6984-104">Overview</span></span>
<span data-ttu-id="c6984-105">Il plug-in Microsoft Smooth Streaming per Open Source Media Framework 2.0 (SS per OSMF) estende le funzionalità predefinite di OSMF e aggiunge la funzionalità di riproduzione del contenuto Smooth Streaming ai lettori OSMF nuovi ed esistenti.</span><span class="sxs-lookup"><span data-stu-id="c6984-105">The Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends the default capabilities of OSMF and adds Microsoft Smooth Streaming content playback to new and existing OSMF players.</span></span> <span data-ttu-id="c6984-106">Il plug-in aggiunge inoltre funzionalità di riproduzione Smooth Streaming a Strobe Media Playback (SMP).</span><span class="sxs-lookup"><span data-stu-id="c6984-106">The plugin also adds Smooth Streaming playback capabilities to Strobe Media Playback (SMP).</span></span>

<span data-ttu-id="c6984-107">In Smooth Streaming per OSMF sono incluse due versioni di plug-in:</span><span class="sxs-lookup"><span data-stu-id="c6984-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="c6984-108">Plug-in Static Smooth Streaming per OSMF (con estensione swc)</span><span class="sxs-lookup"><span data-stu-id="c6984-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="c6984-109">Plug-in Dynamic Smooth Streaming per OSMF (con estensione swf)</span><span class="sxs-lookup"><span data-stu-id="c6984-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="c6984-110">In questo documento si presuppone che il lettore disponga già di conoscenze tecniche generali relative a OSMF e ai plug-in per OSMF. Per altre informazioni su OSMF, consultare la documentazione sul [sito Web ufficiale di OSMF](http://osmf.org/).</span><span class="sxs-lookup"><span data-stu-id="c6984-110">This document assumes that the reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see the documentation on the [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="c6984-111">Plug-in Smooth Streaming per OSMF 2.0</span><span class="sxs-lookup"><span data-stu-id="c6984-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="c6984-112">Il plug-in supporta il caricamento e la riproduzione di contenuto Smooth Streaming su richiesta con le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="c6984-112">The plugin supports loading and playback of on-demand Smooth Streaming content with the following features:</span></span>

* <span data-ttu-id="c6984-113">Riproduzione Smooth Streaming su richiesta (riproduzione, pausa, ricerca, arresto)</span><span class="sxs-lookup"><span data-stu-id="c6984-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="c6984-114">Riproduzione Smooth Streaming in diretta (riproduzione)</span><span class="sxs-lookup"><span data-stu-id="c6984-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="c6984-115">Funzioni DVR in diretta (pausa, ricerca, riproduzione DVR, modalità attiva)</span><span class="sxs-lookup"><span data-stu-id="c6984-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="c6984-116">Supporto per codec video: H.264</span><span class="sxs-lookup"><span data-stu-id="c6984-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="c6984-117">Supporto per codec audio: AAC</span><span class="sxs-lookup"><span data-stu-id="c6984-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="c6984-118">Commutazione tra più lingue per l'audio grazie alle API incorporate in OSMF</span><span class="sxs-lookup"><span data-stu-id="c6984-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="c6984-119">Selezione della qualità di riproduzione massima grazie alle API incorporate in OSMF</span><span class="sxs-lookup"><span data-stu-id="c6984-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="c6984-120">Sottotitoli collaterali con il plug-in per didascalie OSMF</span><span class="sxs-lookup"><span data-stu-id="c6984-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="c6984-121">Adobe&reg; Flash&reg; Player 11.4 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="c6984-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="c6984-122">In questa versione è supportato solo OSMF 2.0.</span><span class="sxs-lookup"><span data-stu-id="c6984-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="c6984-123">Funzionalità supportate e problemi noti</span><span class="sxs-lookup"><span data-stu-id="c6984-123">Supported features and known issues</span></span>
<span data-ttu-id="c6984-124">Per un elenco completo di funzionalità supportate, funzionalità non supportate e problemi noti, fare riferimento a [questo documento](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span><span class="sxs-lookup"><span data-stu-id="c6984-124">For a full list of supported features, unsupported features and known issues, refer to [this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-the-plugin"></a><span data-ttu-id="c6984-125">Caricamento del plug-in</span><span class="sxs-lookup"><span data-stu-id="c6984-125">Loading the Plugin</span></span>
<span data-ttu-id="c6984-126">I plug-in OSMF possono essere caricati in modo statico (in fase di compilazione) o dinamico (in fase di esecuzione).</span><span class="sxs-lookup"><span data-stu-id="c6984-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="c6984-127">Nel download del plug-in Smooth Streaming per OSMF sono incluse entrambe le versioni statica e dinamica.</span><span class="sxs-lookup"><span data-stu-id="c6984-127">The Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="c6984-128">Caricamento statico: per eseguire il caricamento in modo statico, è necessario un file di libreria statica (SWC).</span><span class="sxs-lookup"><span data-stu-id="c6984-128">Static loading: To load statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="c6984-129">I plug-in statici vengono aggiunti come riferimento ai progetti e vengono uniti all'interno del file di output finale in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="c6984-129">Static plugins are added as a reference to the projects and merge inside the final output file at the compile time.</span></span>
* <span data-ttu-id="c6984-130">Caricamento dinamico: per eseguire il caricamento dinamico, è necessario un file precompilato (SWF).</span><span class="sxs-lookup"><span data-stu-id="c6984-130">Dynamic loading: To load dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="c6984-131">I plug-in dinamici vengono caricati in fase di esecuzione e non sono inclusi nell'output del progetto.</span><span class="sxs-lookup"><span data-stu-id="c6984-131">Dynamic plugins are loaded in the runtime and not included in the project output.</span></span> <span data-ttu-id="c6984-132">(Output compilato) I plug-in dinamici possono essere caricati tramite i protocolli HTTP e FILE.</span><span class="sxs-lookup"><span data-stu-id="c6984-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="c6984-133">Per altre informazioni sul caricamento statico e dinamico, vedere la [pagina ufficiale del plug-in OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="c6984-133">For more information on static and dynamic loading, see the official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="c6984-134">Caricamento statico di Smooth Streaming per OSMF</span><span class="sxs-lookup"><span data-stu-id="c6984-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="c6984-135">Nel frammento di codice seguente viene illustrato come caricare il plug-in Smooth Streaming per OSMF in modo statico e riprodurre un video di base usando la classe MediaFactory di OSMF.</span><span class="sxs-lookup"><span data-stu-id="c6984-135">The code snippet below shows how to load the SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="c6984-136">Prima di includere il codice di Smooth Streaming per OSMF, verificare che nei riferimenti del progetto sia incluso il plug-in statico "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc".</span><span class="sxs-lookup"><span data-stu-id="c6984-136">Before including the SS for OSMF code, please ensure that the project reference includes the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

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

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
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
            // The plugin is loaded successfully.
            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="c6984-137">Caricamento dinamico di Smooth Streaming per OSMF</span><span class="sxs-lookup"><span data-stu-id="c6984-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="c6984-138">Nel frammento di codice seguente viene illustrato come caricare il plug-in Smooth Streaming per OSMF in modo dinamico e riprodurre un video di base usando la classe MediaFactory di OSMF.</span><span class="sxs-lookup"><span data-stu-id="c6984-138">The code snippet below shows how to load the SS plugin for OSMF dynamically and play a basic video using the OSMF MediaFactory class.</span></span> <span data-ttu-id="c6984-139">Prima di includere il codice di Smooth Streaming per OSMF, copiare il plug-in dinamico "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" nella cartella del progetto se si desidera eseguire il caricamento tramite il protocollo FILE o copiarlo in un server Web per il caricamento tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="c6984-139">Before including the SS for OSMF code, copy the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin to the project folder if you want to load using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="c6984-140">Non è necessario includere il file "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" nei riferimenti del progetto.</span><span class="sxs-lookup"><span data-stu-id="c6984-140">There is no need to include "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in the project references.</span></span>

<span data-ttu-id="c6984-141">pacchetto {</span><span class="sxs-lookup"><span data-stu-id="c6984-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets the size of the SWF

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

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs to host a valid crossdomain.xml file to allow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // The plugin is loaded successfully.

            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="c6984-142">}</span><span class="sxs-lookup"><span data-stu-id="c6984-142">}</span></span>

## <a name="strobe-media--playback-with-the-ss-odmf-dynamic-plugin"></a><span data-ttu-id="c6984-143">Strobe Media Playback con plug-in dinamico SS per OSMF</span><span class="sxs-lookup"><span data-stu-id="c6984-143">Strobe Media  Playback with the SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="c6984-144">Il plug-in dinamico Smooth Streaming per OSMF è compatibile con [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span><span class="sxs-lookup"><span data-stu-id="c6984-144">The Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="c6984-145">È possibile utilizzare il plug-in SS per OSMF per aggiungere la riproduzione di contenuti Smooth Streaming a SMP.</span><span class="sxs-lookup"><span data-stu-id="c6984-145">You can use the SS for OSMF plugin to add Smooth Streaming content playback to SMP.</span></span> <span data-ttu-id="c6984-146">A questo scopo, copiare il plug-in "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" in un server Web per il caricamento tramite HTTP attenendosi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="c6984-146">To do this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using the following steps:</span></span>

1. <span data-ttu-id="c6984-147">Passare alla [pagina di installazione di Strobe Media Playback](http://osmf.org/dev/2.0gm/setup.html).</span><span class="sxs-lookup"><span data-stu-id="c6984-147">Browse the [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="c6984-148">Impostare l'elemento src su un'origine Smooth Streaming, ad esempio http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest.</span><span class="sxs-lookup"><span data-stu-id="c6984-148">Set the src to a Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="c6984-149">Apportare le modifiche di configurazione desiderate e fare clic su Preview and Update.</span><span class="sxs-lookup"><span data-stu-id="c6984-149">Make the desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="c6984-150">**Nota** Per il server Web del contenuto deve essere presente un file crossdomain.xml valido.</span><span class="sxs-lookup"><span data-stu-id="c6984-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="c6984-151">Copiare e incollare il codice in una pagina HTML semplice utilizzando l'editor di testo desiderato, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c6984-151">Copy and paste the code to a simple HTML page using your favorite text editor, such as in the following example:</span></span>

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



1. <span data-ttu-id="c6984-152">Aggiungere il plug-in Smooth Streaming per OSMF al codice incorporato e salvare.</span><span class="sxs-lookup"><span data-stu-id="c6984-152">Add Smooth Streaming OSMF plugin to the embed code and save.</span></span>
   
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
2. <span data-ttu-id="c6984-153">Salvare la pagina HTML e pubblicarla in un server Web.</span><span class="sxs-lookup"><span data-stu-id="c6984-153">Save your HTML page and publish to a web server.</span></span> <span data-ttu-id="c6984-154">Passare alla pagina Web pubblicata usando un browser Internet compatibile con Flash&reg; Player, ad esempio Internet Explorer, Chrome, Firefox e così via.</span><span class="sxs-lookup"><span data-stu-id="c6984-154">Browse to the published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="c6984-155">Riprodurre il contenuto Smooth Streaming in Adobe&reg; Flash&reg; Player.</span><span class="sxs-lookup"><span data-stu-id="c6984-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="c6984-156">Per ulteriori informazioni sullo sviluppo generale per OSMF, consultare la [pagina ufficiale per lo sviluppo di OSMF](http://osmf.org/resources.html).</span><span class="sxs-lookup"><span data-stu-id="c6984-156">For more information on general OSMF development, please see the official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c6984-157">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="c6984-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c6984-158">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="c6984-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="c6984-159">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c6984-159">See Also</span></span>
[<span data-ttu-id="c6984-160">Plug-in di streaming adattivo Microsoft per aggiornamento OSMF</span><span class="sxs-lookup"><span data-stu-id="c6984-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

