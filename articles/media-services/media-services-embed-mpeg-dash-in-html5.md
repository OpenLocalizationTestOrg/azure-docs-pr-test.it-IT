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
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a>Integrazione di uno streaming video adattivo MPEG-DASH in un'applicazione HTML5 con DASH.js
## <a name="overview"></a>Panoramica
MPEG-DASH è uno standard ISO per il flusso adattivo di contenuto video, che offre vantaggi significativi per gli utenti che desiderano toodeliver adattivo di alta qualità dello streaming video output hello. Con MPEG-DASH flusso video hello verrà eliminata automaticamente definizione inferiore tooa quando congestione rete hello. In questo modo si riduce la probabilità hello del Visualizzatore di hello visualizzare un video "sospeso" mentre player hello Scarica hello successivamente alcuni tooplay secondi (noto anche come memorizzazione nel buffer). Riduce la congestione della rete, lettore video hello restituirà a sua volta tooa il flusso di qualità superiore. Questa possibilità tooadapt hello larghezza di banda richiesta anche i risultati in un'ora di inizio più veloce per video. Che indica che alcuni secondi prima di hello possa essere riprodotto in un segmento di qualità inferiore fast per scaricare e quindi Esegui di qualità più elevata tooa dopo sufficiente contenuto memorizzato nel buffer.

Dash.js è un lettore video MPEG-DASH open source scritto in JavaScript. L'obiettivo è tooprovide un lettore affidabile, multipiattaforma da riusare liberamente in applicazioni che richiedono la riproduzione video. Fornisce la riproduzione MPEG-DASH in qualsiasi browser che supporta hello W3C Media origine Extensions (MSE), ovvero oggi Chrome, Microsoft Edge e IE11 (altri browser hanno manifestato loro toosupport preventivo MSE). Per ulteriori informazioni su DASH.js, js vedere repository dash.js GitHub di hello.

## <a name="creating-a-browser-based-streaming-video-player"></a>Creazione di un lettore di streaming video basato su browser
toocreate una semplice pagina web che consente di visualizzare un lettore video con hello previsto controlla tali una riproduzione, pausa, riavvolgimento e così via, è necessario:

1. Creare una pagina HTML
2. Aggiungere tag video hello
3. Aggiungere il giocatore dash.js hello
4. Inizializzare il lettore hello
5. Aggiungere lo stile CSS
6. Visualizzare i risultati in un browser che implementa MSE hello

Inizializzazione player hello possono essere completate in un numero limitato di righe di codice JavaScript. Utilizzando dash.js, è effettivamente tale video tooembed semplice MPEG-DASH nelle applicazioni basate su browser.

## <a name="creating-hello-html-page"></a>Creazione di hello pagina HTML
pagina HTML standard toocreate contenente hello, è innanzitutto Hello **video** elemento, salvare questo file come basicPlayer.html, come hello di esempio seguente viene illustrato:

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a>Aggiunta di hello DASH.js Player
tooadd dash.js riferimento implementazione toohello applicazione hello, dovrai toograb hello dash.all.js file versione 1.0 di hello del progetto dash.js. Questo deve essere salvato nella cartella JavaScript hello dell'applicazione. Questo file è un file di praticità mette insieme tutto il codice necessario dash.js hello in un singolo file. Se si dispone di un aspetto intorno repository dash.js hello, verranno trovare hello singoli file, test di codice e così via, ma se si desidera toodo è usare dash.js, sarà file dash.all.js hello è necessario.

applicazioni di tooadd hello dash.js player tooyour, aggiungere una sezione head toohello al tag di script di basicPlayer.html:

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


Successivamente, creare un lettore di hello tooinitialize funzione durante il caricamento pagina hello. Aggiungere lo script seguente dopo la riga hello in cui è stato caricato dash.all.js hello:

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

Questa funzione crea in primo luogo un elemento DashContext, Si tratta di un'applicazione hello tooconfigure utilizzati per un ambiente di runtime specifica. Dal punto di vista tecnico, definisce le classi che hello framework injection dipendenza devono utilizzare durante la costruzione di un'applicazione hello hello. Nella maggior parte dei casi, si userà Dash.di.DashContext.

Successivamente, creare un'istanza di classe primaria hello di framework dash.js hello, Media Player. Questa classe contiene metodi, ad esempio necessari riprodurre e sospendere, gestisce la relazione hello con elemento video hello e gestiscono inoltre l'interpretazione di hello del file di supporto presentazione descrizione (MPD) hello che descrive toobe video di hello riprodotto base hello.

funzione Startup Hello di hello classe MediaPlayer viene chiamato tooensure tale lettore hello è pronto tooplay video. Tra l'altro questa funzione assicura che tutte le classi necessarie di hello (come definito dal contesto hello) sono state caricate. Una volta player hello è pronto, è possibile collegare hello elemento video tooit funzione attachView() hello. Questo consente di flusso video di hello MediaPlayer tooinject hello nell'elemento hello e inoltre controllare la riproduzione in base alle esigenze.

Passare l'URL di hello di hello MPD file toohello MediaPlayer in modo che conosce hello video è previsto tooplay.hello setupVideo() funzione appena creato sarà necessario toobe eseguiti pagina hello è completamente caricato. Tale scopo utilizzare eventi onload hello hello dell'elemento del corpo. Modificare l'elemento <body> come segue:

    <body onload="setupVideo()">

Infine, impostare dimensioni hello hello video dell'elemento del CSS. In un ambiente di streaming adattivo, questo è particolarmente importante in quanto potrebbero cambiare dimensioni hello di hello video viene riprodotto durante la riproduzione adatta toochanging le condizioni della rete. In questa demo semplice semplicemente forzare hello elemento video toobe 80% della finestra del browser disponibili hello aggiungendo la seguente sezione di intestazione toohello CSS della pagina hello hello:

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a>Riproduzione di un video
tooplay un video, il browser file basicPlayback.html hello e quindi la riproduzione su un lettore di hello visualizzato.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Vedere anche
[Sviluppo di applicazioni di lettore video](media-services-develop-video-players.md)

[Repository dash.js di GitHub](https://github.com/Dash-Industry-Forum/dash.js) 

