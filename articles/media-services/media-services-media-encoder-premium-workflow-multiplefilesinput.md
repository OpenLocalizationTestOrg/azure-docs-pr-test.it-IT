---
title: "aaaMultiple input i file e le proprietà del componente con il codificatore Premium, Azure | Documenti Microsoft"
description: "In questo argomento viene illustrato toouse setRuntimeProperties toouse input più file e passare processore di contenuti multimediali di flusso di lavoro Premium del codificatore multimediale toohello dati personalizzati."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: 7fb35bdd-9891-4401-a65b-ef3cc8190e8a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: xpouyat;anilmur;juliako
ms.openlocfilehash: e14d10fbf9669e0b88e5ba1c519f1ba5e0bafdd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a>Uso di più file di input e proprietà del componente con il codificatore Premium
## <a name="overview"></a>Panoramica
Esistono scenari in cui le proprietà del componente toocustomize, potrebbe essere necessario specificare Clip elenco XML contenuto oppure inviare più file di input quando si invia un'attività con hello **flusso di lavoro Premium del codificatore multimediale** processore di contenuti multimediali. Di seguito sono riportati alcuni esempi:

* La sovrapposizione di testo nel video e impostando il valore di testo hello (ad esempio, Buongiorno data corrente) in fase di esecuzione per ogni video di input.
* Personalizzazione hello Clip elenco XML (toospecify uno o più file, con o senza l'eliminazione e così via di origine).
* La sovrapposizione di un'immagine del logo nel video di input hello mentre video hello è codificato.
* Codifica di più lingue per l'audio.

hello toolet **flusso di lavoro Premium del codificatore multimediale** che si modificano alcune proprietà nel flusso di lavoro hello quando si creano attività hello o inviano più file di input, si dispone di toouse una stringa di configurazione che contiene  **setRuntimeProperties** e/o **transcodeSource**. Questo argomento viene illustrato come toouse li.

## <a name="configuration-string-syntax"></a>Sintassi della stringa di configurazione
tooset di stringa di configurazione di Hello in hello codifica attività utilizza un documento XML simile al seguente:

```xml
<?xml version="1.0" encoding="utf-8"?>
<transcodeRequest>
  <transcodeSource>
  </transcodeSource>
  <setRuntimeProperties>
    <property propertyPath="Media File Input/filename" value="VideoFileName.mp4" />
  </setRuntimeProperties>
</transcodeRequest>
```

di seguito Hello è codice hello c# che consente di leggere da un file di configurazione XML hello, aggiornarlo con hello filename destra video e la passa toohello attività in un processo:

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass tooit hello name of hello 
// processor toouse for hello specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with hello encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify hello input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset toocontain hello results of hello job. 
// This output is specified as AssetCreationOptions.None, which 
// means hello output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a>Personalizzazione delle proprietà del componente
### <a name="property-with-a-simple-value"></a>Proprietà con un valore semplice
In alcuni casi, è utile toocustomize una proprietà del componente con i file di flusso di lavoro hello che verrà eseguito dal flusso di lavoro Premium del codificatore multimediale toobe.

Si supponga che è progettato un flusso di lavoro che il testo sovrapposizioni sui video e testo hello (ad esempio, Buongiorno data corrente) si suppone che il set di toobe in fase di esecuzione. È possibile farlo inviando toobe testo hello configurare come nuovo valore per la proprietà text hello del componente di sovrapposizione hello di hello hello attività di codifica. È possibile utilizzare questo meccanismo toochange altre proprietà di un componente nel flusso di lavoro di hello (ad esempio hello posizione o colore della sovrimpressione hello, velocità in bit hello del codificatore hello AVC, ecc.).

**setRuntimeProperties** è toooverride utilizzata una proprietà nei componenti hello del flusso di lavoro hello.

Esempio:

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text tooImage Converter/text" value="Today is Friday hello 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a>Proprietà con un valore XML
incapsulare una proprietà che prevede un valore XML, tooset utilizzando `<![CDATA[ and ]]>`.

Esempio:

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

> [!NOTE]
> Assicurarsi che non tooput di ritorno a capo restituiscono subito dopo `<![CDATA[`.

### <a name="propertypath-value"></a>Valore di propertyPath
Negli esempi precedenti hello, stato hello propertyPath "file di supporto/nome al file di Input" o "/ inactiveTimeout" o "clipListXml".
Si tratta in genere, nome hello del componente di hello, il nome di hello di proprietà hello. Hello percorso può essere maggiore o minore di livelli, ad esempio "/ primarySourceFile" (poiché la proprietà hello è alla radice di hello del flusso di lavoro hello) o "/ Video opacità di elaborazione grafica sovrapposizione /" (poiché hello sovrapposta è un gruppo).    

toocheck hello percorso e la proprietà nome, utilizzare hello azione pulsante immediatamente accanto a ogni proprietà. È possibile fare clic su questo pulsante di azione e selezionare **Modifica**. Verranno visualizzati hello effettivo nome di proprietà hello e immediatamente sopra di esso, hello dello spazio dei nomi.

![Azione/modifica](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Proprietà](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a>Più file di input
Ogni attività che si presentino toohello **flusso di lavoro Premium del codificatore multimediale** richiede due risorse:

* Hello prima uno è un *del flusso di lavoro Asset* che contiene un file di flusso di lavoro. È possibile progettare i file del flusso di lavoro utilizzando hello [Progettazione flussi di lavoro](media-services-workflow-designer.md).
* Hello secondo è un *Asset multimediali* che contiene i file di supporto hello che si desidera tooencode.

Quando si invia più supporti file toohello **flusso di lavoro Premium del codificatore multimediale** codificatore, hello seguenti vincoli applica:

* Tutti i supporti di hello file devono trovarsi nel hello stesso *Asset multimediali*. L'uso di più asset multimediali non è supportato.
* È necessario impostare file primario hello in questo Asset multimediali (idealmente, si tratta di hello file video principale che hello codificatore viene chiesto tooprocess).
* È necessario toopass i dati di configurazione che include hello **setRuntimeProperties** e/o **transcodeSource** processore toohello elemento.
  * **setRuntimeProperties** è di proprietà filename di hello toooverride usato o un'altra proprietà nei componenti di hello del flusso di lavoro hello.
  * **transcodeSource** è usato toospecify hello contenuto Clip elenco XML.

Connessioni nel flusso di lavoro hello:

* Se si utilizza uno o più componenti di Input di File multimediali e pianificare toouse **setRuntimeProperties** toospecify hello Nome file, quindi non si connettono hello file primario componente pin toothem. Assicurarsi che non vi sia alcuna connessione tra l'oggetto file primario hello e hello uno o più File di supporto di input.
* Se si preferisce toouse Clip elenco XML e un componente di origine multimediale, quindi è possibile connettere entrambi.

![Nessuna connessione da File di origine primario tooMedia File di Input](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

*Se si usa proprietà filename di setRuntimeProperties tooset hello non è nessuna connessione dal file primario di hello tooMedia componenti di Input del File.*

![Connessione da Clip elenco XML tooClip elenco origine](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

*È possibile connettersi tooMedia Clip elenco XML origine e utilizzare transcodeSource.*

### <a name="clip-list-xml-customization"></a>Personalizzazione di Clip List XML
È possibile specificare hello Clip elenco XML nel flusso di lavoro hello in fase di esecuzione utilizzando **transcodeSource** in configurazione hello stringa XML. È necessario hello Clip elenco XML pin toobe connesso toohello origine multimediale componente nel flusso di lavoro hello.

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <transcodeSource>
      <clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
      </clipList>
    </transcodeSource>
    <setRuntimeProperties>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Se si desidera toospecify /primarySourceFile toouse file di output di hello tooname questa proprietà tramite 'Expressions', si consiglia di passando hello Clip elenco XML come una proprietà *dopo* proprietà /primarySourceFile hello, tooavoid con hello elenco Clip essere sottoposto a override dall'impostazione /primarySourceFile hello.

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="c:\temp\start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Con altro trimming preciso al fotogramma:

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a>Esempio 1: Sovrapposizione un'immagine di sopra hello video

### <a name="presentation"></a>Presentazione
Si consideri un esempio in cui si desidera toooverlay un'immagine del logo nel video di input hello mentre video hello è codificato. In questo esempio, i video di input hello è denominato "Microsoft_HoloLens_Possibilities_816p24.mp4" e il logo di hello "logo.png". È consigliabile eseguire hello alla procedura seguente:

* Creare un Asset del flusso di lavoro con i file di flusso di lavoro hello (vedere il seguente esempio hello).
* Creare una risorsa multimediale, che contiene due file: MyInputVideo.mp4 come hello file primario e MyLogo.png.
* Inviare un supporto di flusso di lavoro Premium del codificatore multimediale di toohello attività asset processore con hello precedente di input e specificare hello seguente stringa di configurazione.

Configurazione:

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Nell'esempio hello sopra, il nome di hello di file video hello viene inviato proprietà primarySourceFile componente e hello toohello Input File multimediali. nome di Hello del file di logo hello viene inviato tooanother Input del File di supporto che è connesso toohello sovrimpressione grafica componente.

> [!NOTE]
> nome di file video Hello viene inviato toohello primarySourceFile proprietà. motivo di Hello è toouse nel flusso di lavoro di hello per la generazione del nome file di output corretto hello utilizzando espressioni, ad esempio questa proprietà.

### <a name="step-by-step-workflow-creation"></a>Procedura dettagliata di creazione del flusso di lavoro
Di seguito è hello passaggi toocreate un flusso di lavoro viene considerato come input due file: un video e un'immagine. Sovrapporrà immagine hello di sopra hello video.

Aprire **Progettazione flussi di lavoro** e selezionare **File** > **New Workspace (Nuova area di lavoro)** > **Transcode Blueprint**.

nuovo flusso di lavoro Hello mostra tre elementi:

* Primary Source File
* Clip List XML
* Output File/Asset  

![Nuovo flusso di lavoro della codifica](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

*Nuovo flusso di lavoro della codifica*

Nel file multimediale di input di ordinamento tooaccept hello, iniziare con l'aggiunta di un componente di Input di File multimediali. tooadd un componente toohello del flusso di lavoro, cercare nella casella di ricerca Repository hello e trascinare la voce hello desiderato nel riquadro della finestra di progettazione di hello.

Successivamente, aggiungere hello file video toobe utilizzato per la progettazione del flusso di lavoro. toodo in tal caso, fare clic su riquadro sfondo hello nella finestra di progettazione del flusso di lavoro e cercare proprietà File di origine primario hello nel riquadro di destra proprietà hello. Fare clic sull'icona di cartella hello e selezionare i file video appropriato hello.

![File di origine primario](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

*File di origine primario*

Successivamente, è possibile specificare file video hello nel componente di Input di File multimediali hello.   

![Origine Media File Input](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

*Origine Media File Input*

Non appena questa operazione viene eseguita, hello Input File multimediali componente esaminare il file hello e popolare il PIN tooreflect hello file di output controllato.

passaggio successivo Hello è tooadd un tooRec.709 spazio colore di "Aggiornamento di tipo dati Video" toospecify hello. Aggiungere un convertitore di formato Video"" che è impostato il tipo di Layout/Layout tooData = configurabile planare. Questo verrà convertito formato tooa di flusso video hello che può essere eseguita come origine del componente di sovrapposizione hello.

![Strumento di aggiornamento tipo dati video e Convertitore formato video](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

*Strumento di aggiornamento tipo dati video e Convertitore formato video*

![Layout type = Configurable Planar (Tipo layout = Planare configurabile)](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

*Il tipo di layout è Planare configurabile*

Successivamente, aggiungere un componente sovrimpressione Video e connessione hello pin video (non compressa) toohello (non compressa) video del pin di input del file di supporto hello.

Aggiungere un altro Input del File di supporto (file del logo tooload hello) fare clic su questo componente e rinominarlo troppo "Supporto di File di Input Logo" e selezionare un'immagine (file con estensione png, ad esempio) nella proprietà di file hello. Connettersi hello immagine non compressi toohello immagine non compressi spina della sovrimpressione hello.

![Componente della sovrimpressione e origine del file di immagine](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

*Componente della sovrimpressione e origine del file di immagine*

Se si desidera toomodify hello posizione del logo hello nel video hello (ad esempio, è possibile tooposition al 10% di fuori di inizio hello era angolo del video hello), deselezionare la casella di controllo "Input manuale" hello. È possibile farlo perché si sta usando un componente di sovrapposizione di Input di File multimediali tooprovide hello logo file toohello.

![Posizione della sovrimpressione](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

*Posizione della sovrimpressione*

tooencode hello tooH.264 flusso video, aggiungere hello codificatore Video AVC e l'area della finestra di progettazione toohello AAC codificatore componenti. Connettere i pin hello.
Impostare codificatore AAC hello e selezionare conversione formato Audio/impostazione predefinita: 2.0 (L, R).

![Codificatori audio e video](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

*Codificatori audio e video*

A questo punto aggiungere hello **ISO Mpeg-4 Multiplexer** e **File di Output** componenti e connessione pin hello, come illustrato.

![Multiplexer MP4 e file di output](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

*Multiplexer MP4 e file di output*

È necessario tooset hello nome per il file di output di hello. Fare clic su hello **File di Output** componente e Modifica espressione hello per file hello:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Nome file di output](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

*Nome file di output*

È possibile eseguire i flussi di lavoro hello localmente toocheck che venga eseguito correttamente.

Al termine, è possibile eseguire il flusso di lavoro in Servizi multimediali di Azure.

Innanzitutto, preparare un asset in servizi multimediali di Azure con due file: file video hello e logo hello. È possibile farlo tramite hello .NET o API REST. È anche possibile farlo tramite hello portale di Azure o [Esplora servizi multimediali di Azure](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).

In questa esercitazione illustra come asset toomanage con AMSE. Esistono due tooan asset di modi tooadd file:

* Creare una cartella locale, copiare i file hello due e trascinamento della selezione hello cartella toohello **Asset** scheda.
* Caricare file video di hello come asset, visualizzare le informazioni di asset hello, andare toohello file scheda e caricare un file aggiuntivo (logo).

> [!NOTE]
> Verificare che tooset un file primario nel asset hello (hello video file principale).

![File di asset nello strumento di esplorazione di Servizi multimediali di Azure](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

*File di asset nello strumento di esplorazione di Servizi multimediali di Azure*

Selezionare asset hello e scegliere tooencode con codificatore Premium. Caricamento del flusso di lavoro hello e selezionarlo.

Fare clic su hello pulsante toopass dati toohello processore e aggiungere le proprietà di runtime XML tooset hello seguenti hello:

![Codificatore Premium nello strumento di esplorazione di Servizi multimediali di Azure](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

*Codificatore Premium nello strumento di esplorazione di Servizi multimediali di Azure*

Quindi, incollare hello segue i dati XML. È necessario il nome hello toospecify di file video hello per hello Input del File di supporto e primarySourceFile. Specificare il nome di hello hello del file del logo hello troppo.

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

![setRuntimeProperties](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture20_amsexmldata.png)

*setRuntimeProperties*

Se si utilizza toocreate .NET SDK hello e attività hello, passato come stringa di configurazione hello toobe questi dati XML.

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

Dopo aver completato il processo di hello, file MP4 hello in hello output asset Visualizza sovrapposizione hello!

![Sovrapporre su hello video](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

*Sovrapporre su hello video*

È possibile scaricare il flusso di lavoro di hello esempio da [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).

## <a name="example-2--multiple-audio-language-encoding"></a>Esempio 2: Codifica di più lingue per l'audio

Un esempio di flusso di lavoro per la codifica di più lingue per l'audio è disponibile in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).

Questa cartella contiene un flusso di lavoro di esempio che può essere utilizzato tooencode un asset di file MXF file tooa più file MP4 con più tracce audio.

Questo flusso di lavoro presuppone che Hello MXF contenente una traccia audio; tracce audio aggiuntive Hello devono essere passate come file audio (WAV o MP4...).

tooencode, effettuare le seguenti operazioni:

* Creare un asset di servizi multimediali con hello e file MXF hello Audio (file 0 too18 audio).
* Verificare che il file MXF hello è impostato come un file primario.
* Creare un processo e un'attività con il processore di codificatore del flusso di lavoro Premium hello. Utilizzo del flusso di lavoro hello fornito (MultiMP4 1080p-19audio v1.workflow).
* Passare l'attività di hello setruntime.xml dati toohello (se si utilizza Esplora servizi multimediali di Azure, utilizzare hello "pass flusso di lavoro toohello dati xml" pulsante).
  * Aggiornare hello dati toospecify hello file corretto linguaggi e i nomi di tag XML.
  * flusso di lavoro Hello include componenti audio denominati 1 Audio tooAudio 18.
  * RFC5646 è supportata per il tag di linguaggio hello.

```xml
<?xml version="1.0" encoding="utf-16"?>
<transcodeRequest>
  <setRuntimeProperties>
    <property propertyPath="Media File Input Video/filename" value="MainVideo.mxf" />
    <property propertyPath="Language/language_code" value="en" />
    <property propertyPath="/primarySourceFile" value="MainVideo.mxf" />
    <property propertyPath="Audio 1/Media File Input/filename" value="french-audio.wav" />
    <property propertyPath="Audio 1/Language/language_code" value="fr" />
    <property propertyPath="Audio 2/Media File Input/filename" value="german-audio.wav" />
    <property propertyPath="Audio 2/Language/language_code" value="de" />
    <property propertyPath="Audio 3/Media File Input/filename" value="japanese-audio.wav" />
    <property propertyPath="Audio 3/Language/language_code" value="ja" />
  </setRuntimeProperties>
</transcodeRequest>
```

* asset codificato Hello conterrà più tracce audio di linguaggio e queste tracce devono essere selezionabile in Azure Media Player.

## <a name="see-also"></a>Vedere anche
* [Introduzione alla codifica Premium in Servizi multimediali di Azure](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [Come toouse codifica Premium in servizi multimediali di Azure](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [Codifica di contenuti su richiesta con Servizi multimediali di Azure](media-services-encode-asset.md#media-encoder-premium-workflow)
* [Codec e formati del flusso di lavoro Premium del codificatore multimediale](media-services-premium-workflow-encoder-formats.md)
* [File del flusso di lavoro di esempio](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [Strumento di esplorazione di Servizi multimediali di Azure](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
