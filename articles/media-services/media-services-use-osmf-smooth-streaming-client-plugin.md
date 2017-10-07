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
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a>Come tooUse hello Microsoft Smooth Streaming plug-in per hello Adobe Apri origine Media Framework
## <a name="overview"></a>Panoramica
Hello plug-in di Microsoft Smooth Streaming per Open Source Media Framework 2.0 (SS per OSMF) estende le funzionalità predefinite di hello di OSMF e aggiunge Microsoft Smooth Streaming toonew la riproduzione del contenuto e OSMF esistenti lettori. plug-in Hello aggiunge inoltre Smooth Streaming tooStrobe funzionalità riproduzione Media Playback (SMP).

In Smooth Streaming per OSMF sono incluse due versioni di plug-in:

* Plug-in Static Smooth Streaming per OSMF (con estensione swc)
* Plug-in Dynamic Smooth Streaming per OSMF (con estensione swf)

Questo documento si presuppone che il lettore di hello abbia una conoscenza generale di OSMF e OSMF plug-in. Per ulteriori informazioni su OSMF, vedere la documentazione di hello in hello [sito ufficiale di OSMF](http://osmf.org/).

### <a name="smooth-streaming-plugin-for-osmf-20"></a>Plug-in Smooth Streaming per OSMF 2.0
plug-in Hello supporta il caricamento e la riproduzione del contenuto Smooth Streaming su richiesta con hello seguenti caratteristiche:

* Riproduzione Smooth Streaming su richiesta (riproduzione, pausa, ricerca, arresto)
* Riproduzione Smooth Streaming in diretta (riproduzione)
* Funzioni DVR in diretta (pausa, ricerca, riproduzione DVR, modalità attiva)
* Supporto per codec video: H.264
* Supporto per codec audio: AAC
* Commutazione tra più lingue per l'audio grazie alle API incorporate in OSMF
* Selezione della qualità di riproduzione massima grazie alle API incorporate in OSMF
* Sottotitoli collaterali con il plug-in per didascalie OSMF
* Adobe&reg; Flash&reg; Player 11.4 o versione successiva.
* In questa versione è supportato solo OSMF 2.0.

## <a name="supported-features-and-known-issues"></a>Funzionalità supportate e problemi noti
Per un elenco completo delle funzionalità supportate e problemi noti e funzionalità non supportate, vedere troppo[questo documento](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).

## <a name="loading-hello-plugin"></a>Caricamento hello plug-in
I plug-in OSMF possono essere caricati in modo statico (in fase di compilazione) o dinamico (in fase di esecuzione). Hello Smooth Streaming plug-in per il download OSMF include versioni statiche e dinamiche.

* Caricamento statico: tooload in modo statico, un file di libreria statica (SWC) è obbligatorio. I plug-in statico vengono aggiunti come riferimento toohello progetti e unione all'interno di output finale hello file in fase di compilazione hello.
* Caricamento dinamico: tooload in modo dinamico, precompilato (SWF) è richiesto un file. I plug-in dinamico sono caricati in fase di esecuzione hello e non incluso nell'output di progetto hello. (Output compilato) I plug-in dinamici possono essere caricati tramite i protocolli HTTP e FILE.

Per ulteriori informazioni sul caricamento statico e dinamico, vedere ufficiale hello [pagina plug-in OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).

### <a name="ss-for-osmf-static-loading"></a>Caricamento statico di Smooth Streaming per OSMF
frammento di codice Hello seguente viene illustrato come tooload hello SS di plug-in per OSMF in modo statico e riproduce un video di base utilizzando la classe MediaFactory OSMF. Prima di includere hello SS per il codice OSMF, verificare che il riferimento di progetto hello include plug-in statico hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc".

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


### <a name="ss-for-osmf-dynamic-loading"></a>Caricamento dinamico di Smooth Streaming per OSMF
frammento di codice Hello seguente viene illustrato come tooload hello SS di plug-in per OSMF in modo dinamico e riproduce un video di base utilizzando una classe OSMF MediaFactory hello. Prima di includere hello SS per il codice OSMF, copiare la cartella del progetto hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" plug-in dinamico toohello se si desidera tooload utilizzando il protocollo FILE oppure copiare in un server web per il carico HTTP. Non sussiste alcun tooinclude necessità "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" nei riferimenti al progetto hello.

pacchetto {

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
}

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a>Strobe Media Playback con hello plug-in dinamico ODMF SS
è compatibile con Hello Smooth Streaming per OSMF dinamica plugin [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html). È possibile utilizzare hello SS per OSMF tooSMP la riproduzione del contenuto di Smooth Streaming tooadd di plug-in. toodo, questa copia "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" in un server web per il carico HTTP utilizzando hello seguendo i passaggi:

1. Sfoglia hello [pagina Installazione Strobe Media Playback](http://osmf.org/dev/2.0gm/setup.html). 
2. Consente di impostare hello src tooa Smooth Streaming origine, (ad esempio http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest) 
3. Apportare modifiche alla configurazione di hello desiderato e fare clic su Anteprima e aggiornamento.
   
   **Nota** Per il server Web del contenuto deve essere presente un file crossdomain.xml valido. 
4. Copiare e incollare hello codice tooa semplice pagina HTML utilizzando un editor di testo, come nel seguente esempio hello:

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



1. Aggiungere toohello plug-in Smooth Streaming per OSMF codice di incorporamento e salvare.
   
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
2. Salvare una pagina HTML e pubblicare tooa web server. Sfoglia toohello pubblicati pagina web mediante i Preferiti Flash&reg; Player abilitato browser Internet (Internet Explorer, Chrome, Firefox, così via).
3. Riprodurre il contenuto Smooth Streaming in Adobe&reg; Flash&reg; Player.

Per ulteriori informazioni sullo sviluppo di OSMF generale, vedere ufficiale hello [pagina sviluppo OSMF](http://osmf.org/resources.html).

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Vedere anche
[Plug-in di streaming adattivo Microsoft per aggiornamento OSMF](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

