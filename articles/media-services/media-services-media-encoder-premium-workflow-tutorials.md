---
title: esercitazioni di flusso di lavoro Premium del codificatore multimediale aaaAvanced
description: "Questo documento contiene procedure dettagliate che illustrano come tooperform avanzate attività con flusso di lavoro Premium del codificatore multimediale e anche come toocreate flussi di lavoro complessi con Progettazione flussi di lavoro."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a>Esercitazioni avanzate del flusso di lavoro Premium del codificatore multimediale
## <a name="overview"></a>Panoramica
Questo documento contiene procedure dettagliate che illustrano come flussi di lavoro toocustomize con **Progettazione flussi di lavoro**. È possibile trovare i file del flusso di lavoro effettivo hello [qui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).  

## <a name="toc"></a>Sommario
viene trattato i seguenti argomenti Hello:

* [Codifica di un file MXF in un MP4 a velocità in bit singola](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [Avvio di un nuovo flusso di lavoro](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [Utilizzo di hello Input del File di supporto](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [Analisi di flussi multimediali](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [Aggiunta di un codificatore video per la generazione di file MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [Flusso audio di codifica hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [Multiplexing di flussi audio e video in un contenitore MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [Scrittura di file MP4 hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [Creazione di un Asset di servizi multimediali dal file di output di hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [Hello test completato del flusso di lavoro locale](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [Codifica di un file MXF in MP4 a velocità in bit multipla - Creazione dinamica dei pacchetti abilitata](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [Aggiunta di uno o più output MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [Output nomi file di configurazione hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [Aggiunta di una traccia audio separata](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [Aggiunta di hello. File SMIL ISM](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [Codifica di un file MXF in un MP4 a velocità in bit multipla - Progetto avanzato](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [Flusso di lavoro Panoramica tooenhance](#workflow-overview-to-enhance)
  * [Convenzioni di denominazione dei file](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [La pubblicazione delle proprietà del componente nella radice del flusso di lavoro hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [Fare in modo che i nomi file di output generati si basino sui valori delle proprietà pubblicati](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [Aggiunta dell'output di anteprime toomultibitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [Flusso di lavoro Panoramica tooadd anteprime](#workflow-overview-to-add-thumbnails-to)
  * [Aggiunta della codifica JPG](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [Gestione della conversione dello spazio colore](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [Anteprime di hello scrittura](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [Rilevamento di errori in un flusso di lavoro](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [Flusso di lavoro completato](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [Taglio basato sull'ora dell'output MP4 a velocità in bit multipla](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [Flusso di lavoro Panoramica toostart aggiunta di taglio per](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [Utilizzo di hello compensatore di flusso](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [Flusso di lavoro completato](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [Introduzione a hello componente script](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [Scripting in un flusso di lavoro: hello world](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [Taglio basato sul fotogramma dell'output MP4 a velocità in bit multipla](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [Cianografia toostart Panoramica aggiunta la rimozione di](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [Utilizzo di hello Clip elenco XML](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [Modifica elenco di clip hello da un componente script](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [Aggiunta di una pratica proprietà ClippingEnabled](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <a id="MXF_to_MP4"></a>Codifica di un file MXF in un MP4 a velocità in bit singola
In questa procedura dettagliata verrà creato un file MP4 a velocità in bit singola con audio con codifica AAC-HE da un file di input MXF.

### <a id="MXF_to_MP4_start_new"></a>Avvio di un nuovo flusso di lavoro
Aprire Progettazione flussi di lavoro e selezionare "File" - "New Workspace" - "Transcode Blueprint"

nuovo flusso di lavoro Hello visualizzerà 3 elementi:

* Primary Source File
* Clip List XML
* Output File/Asset  

![Nuovo flusso di lavoro della codifica](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

*Nuovo flusso di lavoro della codifica*

### <a id="MXF_to_MP4_with_file_input"></a>Utilizzo di hello Input del File di supporto
In ordine tooaccept il file multimediale di input, uno inizia con l'aggiunta di un componente di Input di File multimediali. tooadd un componente toohello del flusso di lavoro, cercare nella casella di ricerca Repository hello e trascinare la voce hello desiderato nel riquadro della finestra di progettazione di hello. Eseguire questa operazione per l'Input di File multimediali hello e connettersi hello File di origine primario componente toohello Filename pin di input da hello supporti File di Input.

![Media File Input connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

*Media File Input connesso*

Prima di effettuare molte altre operazioni, è prima necessario Progettazione flussi di lavoro di tooindicate toohello il file di esempio desideriamo toouse toodesign con il flusso di lavoro. toodo in tal caso, fare clic sullo sfondo della finestra di progettazione riquadro hello e cercare proprietà File di origine primario hello nel riquadro di destra proprietà hello. Fare clic sull'icona di cartella hello e selezionare hello desiderato file tootest hello flusso di lavoro con. Non appena questa operazione viene eseguita, hello Input File multimediali componente esaminare il file hello e popolare il file di hello tooreflect pin di output che controllato.

![Media File Input popolato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

*Media File Input popolato*

Mentre con il tipo di input che desideriamo toowork con specifica, non ti dirà ancora in output di hello con codificata da utilizzare. Simile hello toohow File di origine primario è stato configurato, configurare proprietà della variabile di cartella di Output, solo di sotto di hello.

![Proprietà di input e output configurate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

*Proprietà di input e output configurate*

### <a id="MXF_to_MP4_streams"></a>Analisi di flussi multimediali
Spesso è preferibile tooknow aspetto di questo flusso hello sono illustrate le fasi del flusso di lavoro di hello. solo tooinspect un flusso in qualsiasi punto del flusso di lavoro di hello, fare clic su un output o il pin di input in uno qualsiasi dei componenti di hello. In questo caso, provare a fare clic sul pin di output di hello Video non compressi dall'Input del File di supporto. Verrà aperta una finestra di dialogo che consente tooinspect hello in uscita video.

![Esame pin di output di hello Video non compresso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

*Esame pin di output di hello Video non compresso*

In questo caso, ad esempio, indica che si ha a che fare con un input 1920x1080 a 24 fotogrammi al secondo nel campionamento 4:2:2 per un video di almeno 2 minuti.

### <a id="MXF_to_MP4_file_generation"></a>Aggiunta di un codificatore video per la generazione di file MP4
Si noti che ora in Media File Input sono disponibili per l'uso un pin Uncompressed Video e più pin di output Uncompressed Audio. In ordine tooencode hello video in ingresso, è necessario un componente di codifica, in questo caso per la generazione. File MP4.

tooencode hello tooH.264 flusso video, aggiungere l'area della finestra di progettazione toohello hello codificatore Video AVC dei componenti. Questo componente accetta un flusso video non compresso e genera un flusso video compresso AVC nel pin di output.

![Codificatore AVC non connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

*Codificatore AVC non connesso*

Le proprietà determinano come codifica hello esattamente avviene. Di seguito sono descritte alcune di hello impostazioni più importanti:

* Larghezza di output e l'altezza di Output: consentono di determinare la risoluzione di hello del video codificato hello. In questo caso, si usa 640x360.
* Frequenza dei fotogrammi: quando toopassthrough set verranno semplicemente adottano frequenza dei fotogrammi hello origine, è possibile toooverride questo tuttavia. Si noti che tale conversione della frequenza dei fotogrammi non è compensata dal movimento.
* Profilo e il livello: consentono di determinare il profilo di hello AVC e il livello. tooconveniently ottenere ulteriori informazioni su livelli diversi di hello e profili, fare clic sull'icona di punto interrogativo hello sul componente codificatore Video AVC hello e pagina della Guida hello verrà visualizzati ulteriori informazioni su ciascuno dei livelli di hello. Per l'esempio Proviamo il profilo principale a livello 3.2 (impostazione predefinita hello).
* Rate Control Mode e Bitrate (kbps): in questo scenario viene usato un output con velocità in bit costante (CBR) a 1200 kbps
* Formato video: questo argomento vengono descritti hello VUI (Video di usabilità Information) che vengono scritte nel flusso di hello h. 264 (le informazioni sul lato che potrebbero essere utilizzate da un decodificatore tooenhance hello visualizzazione, ma non è essenziale toocorrectly decodificare):
* NTSC (tipico per Stati Uniti o Giappone, usa 30 fps)
* PAL (tipico per l'Europa, usa 25 fps)
* GOP Size Mode: in questo caso, verrà configurata una dimensione GOP fissa con un intervallo chiave di 2 secondi con GOP chiusi. Ciò garantisce la compatibilità con hello che fornisce servizi multimediali di Azure di creazione dinamica dei pacchetti.

toofeed il codificatore AVC, connettersi pin di output di hello Video non compressi da hello supporti File componente toohello Video non compressi input pin di Input dal codificatore hello AVC.

![Codificatore AVC connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

*Codificatore principale AVC connesso*

### <a id="MXF_to_MP4_audio"></a>Flusso audio di codifica hello
A questo punto, è stato codificato video ma hello flusso di audio non compresso originale deve comunque toobe compressi. Per questo verranno prese con AAC codifica hello componente codificatore AAC (Dolby). Aggiungerlo toohello del flusso di lavoro.

![Codificatore AVC non connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

*Codificatore AAC non connesso*

Ora è presente un problema di incompatibilità: è presente solo un singolo non compresso audio pin di input dal codificatore AAC hello mentre più probabile hello supporti File di Input avranno due diversi non compressi flusso audio disponibile: uno per hello canale audio e uno per hello a sinistra Ok. Se si usa un sistema audio di tipo surround, i canali saranno addirittura 6. Pertanto non è possibile toodirectly collegare audio hello dall'origine di Input di File multimediali hello codifica audio AAC di hello. componente AAC Hello prevede un flusso audio "interleaved" cosiddetto: un singolo flusso che contiene sia hello canali destra a sinistra e hello interlacciati tra loro. Una volta acquisite da questo file di origine le tracce audio la posizione nell'origine hello, è possibile generare tali interleaved flusso audio con hello correttamente assegnati posizioni degli altoparlanti per left e right.

Prima di tutto uno desidererà toogenerated un flusso di interfoliazione da canali audio sorgente hello necessario. componente Interleaver flusso Audio Hello questo gestirà automaticamente. Aggiungerlo toohello del flusso di lavoro e la connessione di output audio hello da hello Input del File di supporto al suo interno.

![Audio Stream Interleaver connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

*Audio Stream Interleaver connesso*

Ora che è disponibile un flusso audio interleaved, è ancora non sono state specificate in altoparlante sinistro o destro di hello tooassign posiziona per. In ordine toospecify questo, è possibile sfruttare tutte hello chi assegna posizione degli altoparlanti.

![Aggiunta di Speaker Position Assigner](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

*Aggiunta di Speaker Position Assigner*

Configurare hello chi assegna posizione altoparlante per l'utilizzo con un flusso di input stereo tramite un filtro di set di impostazioni del codificatore "Custom" e hello canale predefinito denominato "2.0 (L, R)". (Questo assegnerà hello altoparlante sinistro posizione toochannel 1 e hello altoparlante destro posizione toochannel 2.)

Connettere l'output di hello dell'input di toohello chi assegna posizione altoparlante hello di hello AAC codificatore. Specificare quindi la hello AAC codificatore toowork con una "2.0 (L, R)" canale predefinito, indicargli toodeal con audio stereo come input.

### <a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing di flussi audio e video in un contenitore MP4
È possibile acquisire sia il flusso video con codifica AVC che il flusso audio con codifica AAC in un contenitore MP4. il processo di Hello di combinazione di flussi diversi in un unico viene chiamato "multiplexing" (o "muxing"). In questo caso ci stiamo interfoliazione hello flussi audio e hello video in una singola coerente. Pacchetto di file MP4. componente Hello che coordina per un. Contenitore MP4 viene chiamato hello Multiplexer ISO MPEG-4. Aggiungere un'area di progettazione toohello e connettere hello codificatore Video AVC sia gli input di tooits AAC codificatore hello.

![MPEG4 Multiplexer connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

*MPEG4 Multiplexer connesso*

### <a id="MXF_to_MP4_writing_mp4"></a>Scrittura di file MP4 hello
Quando si scrive un file di output, viene utilizzato il componente di Output del File hello. È possibile connettersi a questo output toohello di hello multiplexer ISO MPEG-4, in modo che l'output viene scritto toodisk. toodo, connettersi hello contenitore (MPEG-4) pin toohello scrittura input pin di output di hello File di Output.

![File Output connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

*File Output connesso*

filename Hello che verrà utilizzato è determinato dalla proprietà del File hello. Tale proprietà può essere hardcoded tooa dato valore, più probabilmente una desidererà tooset tramite un'espressione invece.

flusso di lavoro hello toohave determinare automaticamente l'output di hello da un'espressione di proprietà del nome di File, scegliere il nome del File hello pulsante successivo toohello (icona di cartella toohello Avanti). Da hello menu a discesa, quindi selezionare "Espressione". Verrà visualizzata editor espressioni hello. Cancella contenuto hello dell'editor di hello prima.

![Expression Editor vuoto](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

*Expression Editor vuoto*

editor di espressioni Hello consente tooenter qualsiasi valore letterale, combinato con una o più variabili. Le variabili iniziano con un simbolo di dollaro. Quando si premere il tasto di $ hello, dell'editor di hello verrà visualizzata una casella a discesa con una scelta delle variabili disponibili. In questo caso si userà una combinazione di variabile di directory di output di hello e variabile di nome file di input base hello:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Expression Editor compilato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

*Expression Editor compilato*

> [!NOTE]
> In ordine toosee visualizzare un file di output del processo di codifica in Azure, è necessario fornire un valore nell'editor di espressioni hello.
>
>

Quando si conferma espressione hello facendo clic su ok, finestra Proprietà hello verrà visualizzate in anteprima toowhat valore hello File proprietà risolve in questo momento.

![L'espressione File risolve la directory di output](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

*L'espressione File risolve la directory di output*

### <a id="MXF_to_MP4_asset_from_output"></a>Creazione di un Asset di servizi multimediali dal file di output di hello
Anche se è stato scritto un file di output MP4, è comunque necessario tooindicate che il file appartiene toohello output asset di servizi multimediali di cui verranno generato in seguito all'esecuzione del flusso di lavoro. fine toothis, nodo di File/Asset di Output di hello nell'area di disegno del flusso di lavoro hello viene utilizzato. Tutti i file in arrivo in questo nodo renderà parte dell'asset di servizi multimediali di Azure risultante hello.

Connettersi hello Output File componente toohello Asset di Output File/componente toofinish hello del flusso di lavoro.

![Flusso di lavoro completato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

*Flusso di lavoro completato*

### <a id="MXF_to_MP4_test"></a>Hello test completato del flusso di lavoro locale
tootest hello flusso di lavoro in locale, ha raggiunto il pulsante play hello nella barra degli strumenti hello nella parte superiore di hello. Quando il flusso di lavoro hello terminato l'esecuzione, esaminare l'output di hello generato nella cartella di output di hello configurato. Si noterà hello completato MP4 i file di output che è stato codificato dal file di origine di input MXF hello.

## <a id="MXF_to_MP4_with_dyn_packaging"></a>Codifica di un file MXF in MP4 - Creazione dinamica dei pacchetti a velocità in bit multipla abilitata
In questa procedura dettagliata verrà creato un set di file MP4 a velocità in bit multipla con audio con codifica AAC da un solo file di input MXF.

Quando un output di asset con più velocità in bit desiderato per l'utilizzo in combinazione con le funzionalità di creazione dinamica dei pacchetti hello offerte da servizi multimediali di Azure, più file MP4 allineati GOP di ogni una velocità in bit diverse e una risoluzione sarà necessario toobe generato. hello in tal caso, toodo [MXF codifica in un file MP4 velocità in bit singola](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) procedura dettagliata ci offre un buon punto di partenza.

![Flusso di lavoro iniziale](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

*Flusso di lavoro iniziale*

### <a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Aggiunta di uno o più output MP4
Ogni file MP4 nell'asset di Servizi multimediali di Azure risultante supporterà una velocità in bit e una risoluzione diversa. Aggiungere uno o più file MP4 output file toohello del flusso di lavoro.

toomake che hanno tutti i codificatori video creati con le stesse impostazioni di hello, è più pratico tooduplicate hello codificatore di Video AVC già esistente e configurare un'altra combinazione di risoluzione e velocità in bit (aggiungere uno dei 960x540 25 fotogrammi al secondo 2,5 Mbps). codificatore esistente hello tooduplicate, copia incollarlo nell'area di progettazione hello.

Connettersi hello del pin di output di hello Input File multimediali in questo nuovo componente AVC Video non compressi.

![Secondo codificatore AVC connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

*Secondo codificatore AVC connesso*

Ora adattare configurazione hello per il nostro toooutput di codificatore AVC di nuovo 960x540 2,5 Mbps. usando le proprietà "Output width", "Output height" e "Bitrate (kbps)".

Dato vogliamo asset risultante di hello toouse con creazione dinamica dei pacchetti servizi multimediali di Azure, hello endpoint di streaming deve toobe in grado di generare da tali file MP4 frammenti MP4/DASH HLS/frammentato esattamente allineato tooeach altri in modo che i client che passa diverse velocità in bit ottengano un singolo smooth continua audio e video. toomake che si verificano, dobbiamo tooensure nelle proprietà hello di entrambi i codificatori AVC hello dimensioni GOP ("group of pictures") per entrambi i file MP4 è impostato too2 secondi, che possono essere eseguite da:

* impostazione delle dimensioni di GOP tooFixed modalità di ridimensionamento GOP hello e
* secondi di tootwo Hello intervallo dei fotogrammi chiave.
* inoltre impostare hello GOP IDR controllo tooClosed GOP tooensure tutti GOP sono permanente per i propri senza dipendenze

toomake nostri toounderstand pratico del flusso di lavoro, rinominare troppo codificatore AVC prima hello "codificatore Video AVC 640x360 kbps 1200" e hello secondo codificatore AVC "codificatore Video AVC 960x540 kbps 2500".

Ora aggiungere un secondo componente ISO MPEG-4 Multiplexer e un secondo componente File Output. Connettersi hello multiplexer toohello nuovo AVC codificatore e verificare che il relativo output viene indirizzato in File di Output di hello. Connettiti a nuovo toohello output codifica audio AAC hello input di multiplexer. File di Output di Hello, a sua volta, può quindi essere connesso toohello Asset di Output File/nodo tooadd è toohello Asset di servizi multimediali che verrà creato.

![Secondo muxer e File Output connessi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

*Secondo muxer e File Output connessi*

Per compatibilità con creazione dinamica dei pacchetti servizi multimediali di Azure, configurare conteggio tooGOP di hello della multiplexer, modalità di blocco o la durata e impostare hello GOP per ogni blocco too1. (Deve essere predefinito hello).

![Modalità blocco del muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

*Modalità blocco del muxer*

Nota: è consigliabile toorepeat questo processo per qualsiasi altro velocità in bit e la risoluzione combinazioni desiderato toohave aggiunto output asset toohello.

### <a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Output nomi file di configurazione hello
Sono presenti più di un asset di output toohello singolo file aggiunto. In questo modo un necessità toomake che hello nomi di file per ogni hello output file sono diversi tra loro e forse anche applicano una convenzione di denominazione dei file in modo che diventi non crittografato hello nome del file si vuole eseguire.

È possibile controllare la denominazione di file di output tramite espressioni nella finestra di progettazione hello. Aprire il riquadro Proprietà hello per uno dei componenti di File di Output di hello e aprire l'editor di espressioni hello per proprietà File hello. Il primo file di output è stato configurato tramite l'espressione seguente hello (vedere l'esercitazione hello per spostarsi da [MXF tooa velocità in bit singola output MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

Ciò significa che il nome del file è determinato da due variabili: hello di output directory toowrite hello e nel nome di base del file di origine. ex Hello viene esposto come una proprietà a livello radice del flusso di lavoro hello e hello quest'ultimo è determinato dal file di hello in arrivo. Si noti che directory di output di hello è ciò che si usa per test locale; per questa proprietà verrà sottoposto a override dal motore del flusso di lavoro hello quando il flusso di lavoro hello viene eseguito dal processore di contenuti multimediali basata su cloud hello in servizi multimediali di Azure.
toogive sia l'output file una denominazione coerente output, hello modifica file prima denominazione espressione per:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

e hello in secondo luogo per:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

Eseguire un test intermedio eseguire toomake che entrambi i file di output MP4 generati correttamente.

### <a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Aggiunta di una traccia audio separata
Come si vedrà in un secondo momento quando si genera un toogo di file con estensione ISM con i file di output MP4, si richiede inoltre un file MP4 solo audio come traccia audio hello per il flusso adattivo. toocreate questo file, aggiungere ulteriori muxer toohello flusso di lavoro (Multiplexer ISO-MPEG-4) e connettersi pin di output del codificatore AAC hello con il proprio pin di input per la traccia 1.

![Muxer audio aggiunto](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

*Muxer audio aggiunto*

Il nome di un terzo File componente toooutput hello in uscita flusso di Output di hello muxer e configurare l'espressione di denominazione file hello come:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Creazione di File Output con il muxer audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

*Creazione di File Output con il muxer audio*

### <a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Aggiunta di hello. File SMIL ISM
Per toowork creazione dinamica dei pacchetti hello in combinazione con entrambi MP4 i file (e hello MP4 solo audio) nell'asset di servizi multimediali, è necessario anche un file manifesto (denominato anche "SMIL" file: Synchronized Multimedia Integration Language). Questo file indica a servizi multimediali tooAzure quali file MP4 sono disponibili per la creazione dinamica dei pacchetti e quali di questi tooconsider per i flussi audio hello. Un file manifesto tipico per un set di MP4 con un solo flusso audio sarà simile al seguente:

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

file con estensione ISM Hello contiene all'interno di un'istruzione switch, tooeach un riferimento di file video MP4 singoli hello e inoltre tooan MP4 contenente solo audio hello fa riferimento a file audio toothose anche uno (o più).

Generazione del file manifesto hello per il set di MP4 possono essere eseguita tramite un componente denominato "AMS manifesto Writer" hello. toouse, trascinarlo sull'area hello e connettersi pin di output "Scrittura completa" hello da hello tre File di Output componenti toohello Writer AMS manifesto di input. Verificare quindi che output di hello tooconnect di hello AMS manifesto Writer toohello/Asset di File di Output.

Come con il nostro altri componenti output file, configurare il nome output del file con estensione ISM hello con un'espressione:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

Il flusso di lavoro terminato l'aspetto hello riportato di seguito:

![Flusso di file MP4 toomultibitrate MXF completata](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

*Flusso di file MP4 toomultibitrate MXF completata*

## <a id="MXF_to__multibitrate_MP4"></a>Codifica di un file MXF in un MP4 a velocità in bit multipla - Progetto avanzato
In hello [procedura dettagliata precedente del flusso di lavoro](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) abbiamo visto come un singolo asset di input MXF può essere convertito in un asset di output con file MP4 a più velocità in bit, un file MP4 solo audio e un file manifesto da utilizzare in combinazione con il supporto di Azure I servizi di creazione dinamica dei pacchetti.

Questa procedura dettagliata verrà illustrano come alcuni degli aspetti hello possibile avanzato e apportate più semplice.

### <a id="MXF_to_multibitrate_MP4_overview"></a>Flusso di lavoro Panoramica tooenhance
![Multibitrate MP4 tooenhance di flusso di lavoro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

*Multibitrate MP4 tooenhance di flusso di lavoro*

### <a id="MXF_to__multibitrate_MP4_file_naming"></a>Convenzioni di denominazione dei file
Nel flusso di lavoro precedente hello è specificata un'espressione semplice come base di hello per la generazione di nomi file di output. Abbiamo anche se alcuni duplicazione: tutti i componenti di file singolo output di hello hello specificata espressione di questo tipo.

Ad esempio, il componente di output file per file video prima hello è configurato con questa espressione:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

Mentre hello secondo output video, può essere un'espressione simile:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

Non sarebbe più lineare, meno soggetto a errori e più pratico, se fosse possibile rimuovere alcune duplicazioni e rendere il tutto più facilmente configurabile? Fortunatamente, è possibile: le funzioni di espressioni della finestra di progettazione di hello in combinazione con le proprietà personalizzate di hello possibilità toocreate per la radice del flusso di lavoro ci consentirà di ottenere un ulteriore livello di praticità.

Si supponga che si sarà unità configurazione filename da hello di singoli file hello. MP4 velocità in bit. Le velocità in bit verrà siamo tooconfigure in un centro posizionare (su hello radice il grafico), da dove saranno usati tooconfigure e unità di generazione del nome file. toodo, iniziamo pubblicando proprietà velocità in bit hello entrambi radice AVC codificatori toohello il flusso di lavoro, in modo che diventi accessibile da entrambi radice hello anche da codificatori hello AVC. Anche se visualizzata in due punti diversi, esiste un solo valore sottostante.

### <a id="MXF_to__multibitrate_MP4_publishing"></a>La pubblicazione delle proprietà del componente nella radice del flusso di lavoro hello
Aprire codificatore AVC prima hello, passare a proprietà velocità in bit (kbps) toohello e dall'elenco a discesa hello scegliere pubblica.

![Proprietà della pubblicazione hello velocità in bit](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

*Proprietà della pubblicazione hello velocità in bit*

Configurare hello pubblicare finestra di dialogo toopublish toohello radice il grafico del flusso di lavoro, con un nome pubblicato di "video1bitrate" e un nome leggibile di "Velocità in bit Video 1". Configurare un nome gruppo denominato "Streaming Bitrates" e fare clic su Publish.

![Proprietà della pubblicazione hello velocità in bit](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

*Finestra di dialogo di pubblicazione per la proprietà della velocità in bit*

Ripetizione hello stesso per la proprietà di velocità in bit hello di hello secondo codificatore AVC e denominarla "video2bitrate" con un nome visualizzato di "Velocità in bit Video 2", in hello stessa personalizzato di raggruppamento "Streaming velocità in bit".

È ora possibile controllare le proprietà di radice di hello del flusso di lavoro, vedremo il gruppo personalizzato con hello visualizzati due proprietà pubblicata. Entrambi sono che riflette il valore di hello del loro rispettivi AVC codificatore a velocità in bit.

![Proprietà della velocità in bit pubblicate nella radice del flusso di lavoro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

Ogni volta che si desidera tooaccess queste proprietà dal codice o da un'espressione, è possibile farlo simile al seguente:

* dal codice inline da un componente sotto la radice hello: node.getPropertyAsString('.. / video1bitrate', null)
* in un'espressione: ${ROOT_video1bitrate}

Ora è necessario completare gruppo "Streaming velocità in bit" hello pubblicando nonché la velocità di traccia audio su di esso. All'interno delle proprietà di hello di hello codificatore AAC, cercare l'impostazione di velocità in bit hello e selezionare pubblica tooit avanti di hello elenco a discesa. Pubblicare toohello radice del grafico hello con nome "audio1bitrate" e il nome "Velocità in bit Audio 1" all'interno di questo gruppo personalizzato "Streaming velocità in bit" visualizzato.

![Finestra di dialogo di pubblicazione per la velocità in bit audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

*Finestra di dialogo di pubblicazione per la velocità in bit audio*

![Proprietà video e audio risultanti nella radice](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

*Proprietà video e audio risultanti nella radice*

Si noti che la modifica di una di queste tre valori anche riconfigura e modifiche hello valori su cui sono collegate con in base ai rispettivi componenti hello (e in cui è pubblicato da).

### <a id="MXF_to__multibitrate_MP4_output_files"></a>Fare in modo che i nomi file di output generati si basino sui valori delle proprietà pubblicati
Anziché a livello di codice ai nomi file generato, è possibile ora modificare l'espressione di nome file in ogni toorely componenti File di Output di hello sulle proprietà di velocità in bit hello che è appena pubblicati a livello di radice grafico hello. A partire da questo primo output del file, trovare la proprietà di File hello e modificare l'espressione hello simile al seguente:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

siano accessibili e immessi facendo clic sul segno di dollaro hello tastiera hello nella finestra espressione di hello diversi parametri di Hello in questa espressione. Uno dei parametri disponibili hello è la proprietà video1bitrate è pubblicate in precedenza.

![Accesso ai parametri in un'espressione](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

*Accesso ai parametri in un'espressione*

Hello lo stesso per hello file di output per il secondo video:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

e per l'output di hello file solo audio:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

Se si modifica ora velocità in bit hello per le hello file video o audio, verrà riconfigurato codificatore rispettivi hello e convenzione di denominazione di file in base a velocità in bit hello verrà rispettata completamente automatico.

## <a id="thumbnails_to__multibitrate_MP4"></a>Aggiunta dell'output di anteprime toomultibitrate MP4
A partire da un flusso di lavoro che genera l'errore [un output più file MP4 da un input di MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), ora esamineremo nell'aggiunta dell'output toohello anteprime.

### <a id="thumbnails_to__multibitrate_MP4_overview"></a>Flusso di lavoro Panoramica tooadd anteprime
![Multibitrate MP4 toostart di flusso di lavoro da](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

*Multibitrate MP4 toostart di flusso di lavoro da*

### <a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Aggiunta della codifica JPG
cuore Hello del nostro generazione anteprima sarà componente codificatore JPG hello, in grado di toooutput JPG (file).

![JPG Encoder](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

*JPG Encoder*

Connessione non è tuttavia direttamente il flusso Video non compressi da hello Input File multimediali in codificatore JPG hello. In alternativa, è previsto che toobe passato singoli frame. Questa operazione, è possibile eseguire questa operazione tramite il componente di controllo Frame Video hello.

![La connessione a un codificatore di frame gate toohello JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

*La connessione a un codificatore di frame gate toohello JPG*

controllo frame Hello dopo ogni moltissimi secondi o frame consente un toopass fotogrammi video. Hello intervallo e hello differenza di orario con cui in questo caso è possibile configurare nelle proprietà hello.

![Proprietà di Video Frame Gate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

*Proprietà di Video Frame Gate*

Si crea un'immagine di anteprima ogni minuto impostando tooTime modalità hello (secondi) e hello too60 intervallo.

### <a id="thumbnails_to__multibitrate_MP4_color_space"></a>Gestione della conversione dello spazio colore
Anche se potrebbe sembrare logico sia PIN Video non compressi di controllo frame hello e hello Input del File di supporto può ora essere connesso, si otterrebbe un avviso se è necessario farlo.

![Errore relativo allo spazio color di input](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

*Errore relativo allo spazio color di input*

In questo modo hello quali colori informazioni vengono rappresentate nel nostro originale non elaborato non compresso flusso video, provenienti dal nostro MXF, è diverso da quali hello prevede che il codificatore JPG. Più in particolare, una cosiddetta "spazio colore" di "RGB" o "Grigio" è previsto tooflow in. Ciò significa che flusso video in ingresso che hello Video Frame Gate necessario toohave una conversione riguardanti lo spazio colore applicata per primo.

Trascinare hello del flusso di lavoro hello convertitore spazio colore - Intel e connetterla tooour gate di frame.

![Connessione di un convertitore dello spazio colore](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

*Connessione di un convertitore dello spazio colore*

Nella finestra Proprietà hello, selezionare la voce hello BGR 24 dall'elenco predefinito di hello.

### <a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Anteprime di hello scrittura
Diverso da nel video di MP4, hello codificatore JPG componente l'output contiene più di un file. In ordine toodeal con questo oggetto, è possibile utilizzare un componente Writer di File JPG Ricerca scena: verrà richiedere anteprime di hello in arrivo JPG e scriverli out, ogni nome di file viene preceduto da un numero diverso. (hello numero in genere hello del secondi/unità nel flusso di hello hello anteprima è stato creato da).

![Introduzione a hello Writer di File JPG Ricerca scena](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

*Introduzione a hello Writer di File JPG Ricerca scena*

Configurare proprietà percorso di cartella di Output di hello con espressione hello: ${ROOT_outputWriteDirectory}

e la proprietà con il prefisso del nome file hello:

    ${ROOT_sourceFileBaseName}_thumb_

prefisso Hello determinerà come file di anteprima hello sono denominati. Essi verrà aggiunto un suffisso con la posizione di un numero che indica hello della casella di scorrimento nel flusso hello.

![Proprietà di Scene Search JPG File Writer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

*Proprietà di Scene Search JPG File Writer*

Connettere hello Writer di File JPG Ricerca scena toohello Asset di Output File/nodo.

### <a id="thumbnails_to__multibitrate_MP4_errors"></a>Rilevamento di errori in un flusso di lavoro
Connettere l'input hello di hello colore spazio convertitore toohello non elaborato non compresso output video. A questo punto, eseguire un test locale per flusso di lavoro hello. È presente un flusso di lavoro hello buone probabilità verrà improvvisamente arrestare l'esecuzione e indicare con un contorno rosso sul componente hello che si è verificato un errore:

![Errore di Color Space Converter](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

*Errore di Color Space Converter*

Fare clic sull'icona "E" hello leggermente rosso hello angolo superiore destro di hello convertitore spazio colore componente toosee qual è il motivo di hello hello codifica non è riuscito.

![Finestra di dialogo dell'errore di Color Space Converter](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

*Finestra di dialogo dell'errore di Color Space Converter*

Si scopre, come si può notare che hello in arrivo spazio colore standard per convertitore di spazio colori hello è rec601 toobe per la conversione di tooRGB YUV richiesta. Sembra che il flusso non indichi rec601. Rec 601 è uno standard per la codifica dei segnali video analogici interlacciati nel formato video digitale. Specifica un'area attiva che copre 720 campioni di luminanza e 360 campioni di crominanza per linea. sistema di codifica dei colori di Hello sono noto come allineamento 4:2:2.)

toofix, si verrà indicano i metadati di hello del nostro flusso ci stiamo occupa rec601 contenuto. toodo utilizzeremo un componente di aggiornamento di tipo di dati Video, che è stato verrà inserito tra il nostro raw origine e hello colore spazio componente per la conversione. L'aggiornamento di tipo di dati consente l'aggiornamento manuale di hello di determinati dati video le proprietà del tipo. Configurarlo tooindicate uno spazio colore Standard di "Rec 601". In questo modo flusso hello tootag Updater tipo di dati Video di hello con spazio di colore "Rec 601" hello, se si è verificato alcun spazio colore ancora definito. (Non sostituisce eventuali metadati esistenti, a meno che non è stata selezionata la casella di controllo Override hello.)

![Aggiornamento Standard di spazio colore in hello Updater tipo di dati](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

*Aggiornamento Standard di spazio colore in hello Updater tipo di dati*

### <a id="thumbnails_to__multibitrate_MP4_finish"></a>Flusso di lavoro completato
Ora che il nostro il flusso di lavoro viene terminato, eseguire un altro toosee esecuzione dei test vengano superati.

![Flusso di lavoro completato per l'output di più MP4 con anteprime](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

*Flusso di lavoro completato per l'output di più MP4 con anteprime*

## <a id="time_based_trim"></a>Taglio basato sull'ora dell'output MP4 a velocità in bit multipla
A partire da un flusso di lavoro che genera l'errore [un output più file MP4 da un input di MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), ora esamineremo in trimming video di origine hello in base a un timestamp.

### <a id="time_based_trim_start"></a>Flusso di lavoro Panoramica toostart aggiunta di taglio per
![Avvio rimozione tooadd del flusso di lavoro a](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

*Avvio rimozione tooadd del flusso di lavoro a*

### <a id="time_based_trim_use_stream_trimmer"></a>Utilizzo di hello compensatore di flusso
componente flusso compensatore Hello consente tootrim hello inizio e alla fine di un flusso di input basata sulle informazioni di intervallo (secondi, minuti,...). compensatore Hello non supporta la rimozione di basati su frame.

![Stream Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

*Stream Trimmer*

Anziché direttamente il collegamento codificatori hello AVC e degli altoparlanti posizione chi assegna toohello Input del File di supporto, si verrà inserita tra tali compensatore flusso hello. (Uno per il segnale video hello e uno per hello interleaved segnali audio).

![Inserire Stream Trimmer in mezzo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

*Inserire Stream Trimmer in mezzo*

Configurazione compensatore hello in modo che verranno elaborati solo video e audio compreso tra 15 e 60 secondi in video hello.

Passare la proprietà toohello di hello compensatore flusso Video e configurare l'ora di inizio (15s) sia le proprietà dell'ora di fine (60 s). toomake che sia il compensatore audio e video siano sempre configurata toohello stesso iniziare e terminare i valori, verranno pubblicate tali radice toohello del flusso di lavoro hello.

![Pubblicare la proprietà Start Time da Stream Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

*Pubblicare la proprietà Start Time da Stream Trimmer*

![Finestra di dialogo Publish Property per Start Time](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

*Finestra di dialogo Publish Property per Start Time*

![Finestra di dialogo Publish Property per End Time](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

*Finestra di dialogo Publish Property per End Time*

Se è ora possibile esaminare radice hello il flusso di lavoro, entrambe le proprietà sarà perfettamente configurabile e visualizzati da qui.

![Proprietà pubblicate disponibili nella radice](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

*Proprietà pubblicate disponibili nella radice*

Ora aprire le proprietà di taglio hello da compensatore audio hello e configurare i tempi di inizio e di fine con un'espressione che fa riferimento toohello pubblicato le proprietà nella directory principale di hello di questo flusso di lavoro.

Ora di inizio rimozione audio per hello:

    ${ROOT_TrimmingStartTime}

e per l'ora di fine:

    ${ROOT_TrimmingEndTime}

### <a id="time_based_trim_finish"></a>Flusso di lavoro completato
![Flusso di lavoro completato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

*Flusso di lavoro completato*

## <a id="scripting"></a>Introduzione a hello componente script
Componenti di script possono essere eseguiti gli script arbitrari durante le fasi di esecuzione hello del nostro del flusso di lavoro. Sono disponibili quattro diversi script che può essere eseguito, ognuna con caratteristiche specifiche e luogo nel ciclo di vita di hello del flusso di lavoro:

* **commandScript**
* **realizeScript**
* **processInputScript**
* **lifeCycleScript**

Hello inserire la documentazione di hello componente script in modo più dettagliato per ogni hello precedente. In [hello seguente sezione](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** componente script è tooconstruct utilizzato un file xml di cliplist volo hello all'avvio di flusso di lavoro hello. Questo script viene chiamato durante l'installazione di componenti hello, che si verifica una sola volta nel relativo ciclo di vita.

### <a id="scripting_hello_world"></a>Scripting in un flusso di lavoro: hello world
Trascinare un componente script nell'area di progettazione hello e rinominarlo (ad esempio, "SetClipListXML").

![Aggiunta di un componente con script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Aggiunta di un componente con script*

Quando si esaminano le proprietà di hello di hello componente script, hello verranno visualizzati quattro tipi di script diverso, ogni script diverso tooa configurabile.

![Proprietà del componente con script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Proprietà del componente con script*

Deselezionare hello processInputScript e aprire l'editor di hello per realizeScript hello. È ora completato la configurazione e pronto toostart scripting.

Gli script vengono scritti in Groovy, un linguaggio di scripting compilato in modo dinamico per la piattaforma Java hello che mantiene la compatibilità con Java. La maggior parte del codice Java è effettivamente codice Groovy valido.

Di seguito scrivere uno script di semplice hello world groovy nel contesto di hello del nostro realizeScript. Immettere il seguente hello nell'editor di hello:

    node.log("hello world");

Ora effettuare un'esecuzione di test locale. Dopo l'esecuzione, controllare (tramite scheda sistema hello nel componente script hello) hello proprietà log.

![Output di log hello world](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

*Output di log hello world*

oggetto del nodo Hello viene chiamato il metodo di log hello, fa riferimento tooour corrente "nodo" o un componente di hello ci stiamo l'esecuzione degli script. Di conseguenza, ogni componente ha hello possibilità toooutput la registrazione dati, disponibili tramite la scheda di sistema hello. In questo caso, è output hello stringa letterale "hello world". Qui toounderstand importante è che ciò può rivelarsi toobe uno strumento estremamente utile di debug, visualizzando le informazioni dettagliate su quali script hello è in esecuzione.

Da in ambiente di scripting, è necessario anche accesso tooproperties su altri componenti. Provare a eseguire quanto segue:

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

La finestra del log mostrerà hello seguenti:

![Output dei log per l'accesso ai percorsi dei nodi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

*Output dei log per l'accesso ai percorsi dei nodi*

## <a id="frame_based_trim"></a>Taglio basato sul fotogramma dell'output MP4 a velocità in bit multipla
A partire da un flusso di lavoro che genera l'errore [un output più file MP4 da un input di MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), ora esamineremo in trimming video di origine hello in base al conteggio dei frame.

### <a id="frame_based_trim_start"></a>Cianografia toostart Panoramica aggiunta la rimozione di
![Aggiunta di taglio per toostart di flusso di lavoro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

*Aggiunta di taglio per toostart di flusso di lavoro*

### <a id="frame_based_trim_clip_list"></a>Utilizzo di hello Clip elenco XML
In tutte le esercitazioni del flusso di lavoro precedente, abbiamo utilizzato componente di Input di File di supporto hello come l'origine video di input. Per questo scenario specifico, tuttavia, verrà usato il componente di origine dell'elenco Clip hello invece. Si noti che questo non deve essere hello preferito modo di lavorare; utilizzare solo hello Clip elenco origine quando esiste un toodo motivo effettivo così (come in hello sotto i casi in cui rendiamo utilizzo delle funzionalità di taglio hello clip elenco).

tooswitch dal nostro toohello di Input di File multimediali Clip elenco origine, trascinare il componente di origine dell'elenco Clip hello nell'area di progettazione hello e connettersi hello Clip elenco XML pin toohello Clip elenco il nodo XML di progettazione del flusso di lavoro hello. Questo deve popolare hello Clip elenco origine con il PIN di output, in base tooour video di input. Connettersi a questo punto i pin non compresso Audio e Video non compresso hello da hello hello Clip elenco origine toohello rispettivi AVC codificatori e Interleaver flusso Audio. Rimuovere hello Input del File di supporto.

![Sostituito hello Input File multimediali con hello Clip elenco origine](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

*Sostituito hello Input File multimediali con hello Clip elenco origine*

componente di origine dell'elenco Clip Hello accetta come input un "Clip elenco XML". Selezionando tootest di file di origine hello con localmente, questo elenco di ritaglio codice xml viene popolato automaticamente per l'utente.

![Proprietà Clip List XML popolata automaticamente](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

*Proprietà Clip List XML popolata automaticamente*

Esaminando un bit più vicino toohello xml, ecco come appare come:

![Finestra di dialogo di modifica dell'elenco di clip](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

*Finestra di dialogo di modifica dell'elenco di clip*

Questo tuttavia non riflette le funzionalità di hello di hello clip elenco xml. Abbiamo è tooadd un elemento "Trim" hello audio e video origine audio, simile al seguente:

![Aggiunta di un elenco di ritaglio di elemento trim toohello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

*Aggiunta di un elenco di ritaglio di elemento trim toohello*

Se si modifica hello clip elenco xml simile al seguente di sopra e si esegue un'esecuzione dei test locali, si noterà video hello correttamente stato tagliati compreso tra 10 e 20 secondi in video hello.

Toowhat contrarie si verifica quando si esegue un'esecuzione locale, tuttavia, questa stessa xml cliplist non avrebbero hello lo stesso effetto di quando applicato in un flusso di lavoro in esecuzione in servizi multimediali di Azure. Quando viene avviato codificatore Premium di Azure, hello cliplist xml viene generato ogni volta che, in base alle hello file di input hello codifica processo è stato specificato. Ciò significa che tutte le modifiche facciamo su xml hello verrebbero Purtroppo eseguito l'override.

toocounter hello cliplist xml venga cancellato quando viene avviato un processo di codifica, è possibile generare di nuovo il volo hello subito dopo l'inizio di hello il flusso di lavoro. Tali azioni personalizzate possono essere eseguite con un cosiddetto "componente con script". Per ulteriori informazioni, vedere [Introducing hello componente script](media-services-media-encoder-premium-workflow-tutorials.md#scripting).

Trascinare un componente script nell'area di progettazione hello e rinominarlo troppo "SetClipListXML".

![Aggiunta di un componente con script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Aggiunta di un componente con script*

Quando si esaminano le proprietà di hello di hello componente script, hello verranno visualizzati quattro tipi di script diverso, ogni script diverso tooa configurabile.

![Proprietà del componente con script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Proprietà del componente con script*

### <a id="frame_based_trim_modify_clip_list"></a>Modifica elenco di clip hello da un componente script
È possibile scrivere nuovamente hello cliplist xml che viene generato durante l'avvio del flusso di lavoro, è necessario contenuto e la proprietà xml toohave accesso toohello cliplist. A questo scopo, è possibile usare il codice seguente:

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Elenco di clip in entrata da registrare](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

*Elenco di clip in entrata da registrare*

È necessario un modo toodetermine da che punto fino a quel punto si desidera tootrim hello video. pubblicare questo utente meno tecniche toohello pratico di flusso di lavoro hello toomake radice toohello due proprietà del grafico hello. toodo, fare clic con il pulsante destro progettazione hello e selezionare "Aggiungi proprietà":

* Prima proprietà: "ClippingTimeStart" di tipo: "TIMECODE"
* Seconda proprietà: "ClippingTimeEnd" di tipo: "TIMECODE"

![Finestra di dialogo Add Property per l'ora di inizio del ritaglio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

*Finestra di dialogo Add Property per l'ora di inizio del ritaglio*

![Proprietà degli orari di ritaglio pubblicate nella radice del flusso di lavoro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

*Proprietà degli orari di ritaglio pubblicate nella radice del flusso di lavoro*

Configurare entrambi valore di proprietà tooa appropriato:

![Configurare hello ritaglio proprietà start ed end](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

*Configurare hello ritaglio proprietà start ed end*

Ora dallo script è possibile accedere a entrambe le proprietà, in questo modo:

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Finestra dei log che mostra l'inizio e la fine del ritaglio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

*Finestra dei log che mostra l'inizio e la fine del ritaglio*

Di seguito è possibile analizzare le stringhe di timecode hello in un form toouse più semplice, usando un'espressione regolare semplice:

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Finestra dei log con l'output del time code analizzato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

*Finestra dei log con l'output del time code analizzato*

Con queste informazioni in questione, è possibile ora modificare hello cliplist xml tooreflect hello e l'ora di fine per hello desiderato ritaglio ad alta precisione del filmato hello.

![Elementi di taglio tooadd codice di script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

*Elementi di taglio tooadd codice di script*

Queste modifiche sono state apportate con normali operazioni di manipolazione delle stringhe. codice xml risultante ClipArt modificata elenco Hello vengono riscritti toohello clipListXML proprietà a livello radice del flusso di lavoro hello tramite il metodo "setProperty" hello. finestra log Hello dopo l'esecuzione di un altro test sarebbe mostrano hello seguenti:

![Registrazione elenco clip risultante hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

*Registrazione elenco clip risultante hello*

Eseguire un toosee di esecuzione dei test come sono stati ritagliati flussi audio e video hello. Come verranno eseguite più di una esecuzione dei test con valori diversi per i punti di taglio hello, si noterà che quelli non accederà conto tuttavia! motivo Hello è tale finestra di progettazione di hello, a differenza di hello runtime di Azure, non non override hello cliplist xml ogni esecuzione. Ciò significa che solo hello attutire impostate hello i punti, causerà hello xml tootransform, tutti hello altre volte, la clausola guard (se (clipListXML.indexOf ("<trim>") = = -1)), non potrà del flusso di lavoro hello aggiungerne un altro trim elemento quando è già presente.

toomake il flusso di lavoro pratico tootest in locale, è migliore aggiungere il codice di parti di riferimento che controlla se un elemento trim è già presente. In questo caso, è possibile rimuoverlo prima di continuare modificando hello xml con i nuovi valori hello. Anziché utilizzare stringhe normale, è probabilmente sicura toodo tramite l'oggetto xml reale durante l'analisi del modello.

Tuttavia, è possibile aggiungere tale codice, è necessario tooadd che un numero di istruzioni import in hello iniziare prima dello script:

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

Successivamente, è possibile aggiungere hello necessaria la pulizia di codice:

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

Questo codice viene inserito sopra il punto di hello in corrispondenza del quale è aggiungere hello elementi trim toohello cliplist xml.

A questo punto, è possibile eseguire e modificare il flusso di lavoro come determinante dal momento che durante le modifiche apportate hello applicato mai ora.    

### <a id="frame_based_trim_clippingenabled_prop"></a>Aggiunta di una pratica proprietà ClippingEnabled
Poiché non è sempre consigliabile toohappen taglio, completare disattivare il flusso di lavoro tramite l'aggiunta di un semplice flag booleano che indica se si vuole tooenable trimming / ritaglio.

Proprio come prima, pubblicare una nuova proprietà toohello directory principale di questo flusso di lavoro denominato "ClippingEnabled" di tipo "BOOLEAN".

![Pubblicare una proprietà per l'abilitazione del ritaglio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

*Pubblicare una proprietà per l'abilitazione del ritaglio*

Con hello seguito clausola guard semplice, è possibile controllare se è necessaria la rimozione e decidere se l'elenco di ritaglio deve pertanto toobe modificato o meno.

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <a id="code"></a>Codice completo
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a>Vedere anche
[Introduzione alla codifica Premium in Servizi multimediali di Azure](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[Come tooUse codifica Premium in servizi multimediali di Azure](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[Codifica di contenuti su richiesta con Servizi multimediali di Azure](media-services-encode-asset.md#media-encoder-premium-workflow)

[Codec e formati del flusso di lavoro Premium del codificatore multimediale](media-services-premium-workflow-encoder-formats.md)

[File del flusso di lavoro di esempio](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[Strumento di esplorazione di Servizi multimediali di Azure](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
