---
title: aaaPerform avanzate codifica personalizzando MES predefiniti | Documenti Microsoft
description: "Questo argomento viene illustrato come tooperform avanzate codifica personalizzando Media Encoder Standard attività predefiniti."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a>Eseguire attività di codifica avanzata personalizzando i set di impostazioni di Media Encoder Standard 

## <a name="overview"></a>Panoramica

Questo argomento viene illustrato come toocustomize Media Encoder Standard predefiniti. Hello [codifica con Media Encoder Standard utilizzando predefiniti personalizzati](media-services-custom-mes-presets-with-dotnet.md) argomento viene illustrato come toouse .NET toocreate una codifica attività e un processo che esegue questa attività. Dopo aver personalizzato di un set di impostazioni attività codifica toohello alimentatore hello predefiniti personalizzati. 

>[!NOTE]
>Se si utilizza un set di impostazioni XML, creare che toopreserve hello ordine degli elementi, come illustrato negli esempi XML seguenti (durata di KeyFrameInterval, ad esempio, deve precedere SceneChangeDetection).
>

In questo argomento vengono illustrati predefiniti personalizzati hello che eseguono hello seguente attività di codifica.

## <a name="support-for-relative-sizes"></a>Supporto per le dimensioni relative

Durante la generazione di anteprime, non è necessario specificare di tooalways output larghezza e altezza in pixel. È possibile specificarle in percentuali nell'intervallo di hello [% 1, …, 100%].

### <a name="json-preset"></a>Set di impostazioni JSON
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a>Set di impostazioni XML
    <Width>100%</Width>
    <Height>100%</Height>

## <a id="thumbnails"></a>Generare anteprime

Questa sezione viene illustrato come toocustomize un set di impostazioni che genera le anteprime. Hello predefinito definito di seguito contiene informazioni su come si desidera tooencode il file, nonché le informazioni necessarie toogenerate anteprime. È possibile eseguire uno dei set di impostazioni MES hello documentato [questo](media-services-mes-presets-overview.md) sezione e aggiungere codice che genera le anteprime.  

> [!NOTE]
> Hello **SceneChangeDetection** impostazione hello seguente set di impostazioni può essere impostato solo tootrue se si esegue la codifica video con velocità in bit singola tooa. Se si esegue la codifica tooa più velocità in bit video e impostare **SceneChangeDetection** tootrue, il codificatore hello restituisce un errore.  
>
>

Per informazioni sullo schema, vedere [questo](media-services-mes-schema.md) argomento.

Verificare che hello tooreview [considerazioni](#considerations) sezione.

### <a id="json"></a>Set di impostazioni JSON
    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"

            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a id="xml"></a>Set di impostazioni XML
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a>Considerazioni

si applica Hello seguenti considerazioni:

* utilizzo di Hello del timestamp esplicito per Inizio passaggio/intervallo presuppone che tale origine di input hello è lungo almeno 1 minuto.
* Gli elementi Jpg/Png/BmpImage hanno gli attributi inizio, passaggio e intervallo della stringa, che possono essere interpretati come:

  * Se sono numeri interi non negativi, numero di frame, ad esempio "Start": "120",
  * Durata toosource relativo se espresso come presenta il suffisso %, ad esempio "Start": "% 15", o
  * Timestamp se espresso come HH:MM:SS come formato, ad esempio "Start": "00:01:00"

    È possibile combinare e associare le notazioni a piacimento.

    Inizio supporta inoltre anche una Macro speciale: {ottimale}, che tenta di toodetermine hello primo "interessante" frame di contenuto hello Nota: (passaggio e intervallo vengono ignorati quando l'avvio viene impostato troppo {migliore})
  * Impostazioni predefinite: Start: {Best}
* Formato di output deve toobe forniti in modo esplicito per ogni formato di immagine: Jpg o Png/BmpFormat. Se presente, MES corrisponde JpgVideo tooJpgFormat e così via. OutputFormat introduce una nuova immagine codec specifico (macro): {indice}, che richiede toobe presente (una volta e una sola volta) per formati di output di immagine.

## <a id="trim_video"></a>Tagliare un video (ritaglio)
Discussioni questa sezione sulla modifica del codificatore hello predefiniti tooclip o tagliare i video di input hello dove hello input è un file mezzanine cosiddetti o su richiesta. Hello codificatore può anche essere utilizzati tooclip o tagliare un asset, che viene acquisito o archiviato da un flusso in tempo reale: hello dettagli per questo sono disponibili nel [questo blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).

tootrim i video, può accettare qualsiasi hello MES predefiniti documentati [questo](media-services-mes-presets-overview.md) sezione e modificare hello **origini** elemento (come illustrato di seguito). il valore di Hello di StartTime deve toomatch hello i timestamp assoluto del video di input hello. Ad esempio, se hello primo frame del video di input hello ha un timestamp di 12:00:10.000 quindi StartTime deve essere almeno 12:00:10.000 e versioni successive. Nell'esempio hello seguente, si presuppone che l'input di hello video presenta un timestamp inizio pari a zero. **Origini** deve essere inserito all'inizio di hello di hello predefinito.

### <a id="json"></a>Set di impostazioni JSON
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="xml-preset"></a>Set di impostazioni XML
tootrim i video, può accettare qualsiasi hello MES predefiniti documentati [qui](media-services-mes-presets-overview.md) e modificare hello **origini** elemento (come illustrato di seguito).

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <a id="overlay"></a>Creare una sovrimpressione

Hello Media Encoder Standard consente toooverlay un'immagine in un video esistente. Attualmente, è supportato i seguenti formati hello: png, jpg, gif, bmp e. Hello predefinito definito di seguito è un esempio di base di un sovrimpressione video.

Inoltre toodefining un file predefinito, è inoltre servizi multimediali toolet sapere quali file di asset hello è l'immagine sovrapposta hello e il file di cui è in cui si desidera che toooverlay hello immagine video di origine di hello. file video Hello è hello toobe **primario** file.

Se si utilizza .NET, aggiungere hello seguenti due funzioni di esempio .NET toohello definito in [questo](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) argomento. Hello **UploadMediaFilesFromFolder** funzione carica i file da una cartella (ad esempio, BigBuckBunny.mp4 e Image001.png) e set hello mp4 file toobe hello file primario nel asset hello. Hello **EncodeWithOverlay** funzione utilizza hello personalizzato preimpostate che è stato passato tooit (ad esempio, hello preset che segue) toocreate hello attività di codifica.


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> Limitazioni correnti:
>
> impostazione di opacità Hello sovrapposizione non è supportata.
>
> Il file video di origine e di un file di immagine sovrapposta hello hanno toobe in hello stesso asset e hello file video esigenze toobe set come file primario hello questo asset.
>
>

### <a name="json-preset"></a>Set di impostazioni JSON
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a>Set di impostazioni XML
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <a id="silent_audio"></a>Inserire una traccia audio silenziosa quando l'input è privo di audio
Per impostazione predefinita, se si invia un codificatore toohello input che contiene solo i video e audio non hello asset di output contiene file che contengono dati solo video. Alcuni lettori potrebbero non essere possibile toohandle tali flussi di output. È possibile utilizzare questo tooadd di codificatore hello tooforce impostazione un output di traccia audio invisibile all'utente toohello in tale scenario.

tooforce hello codificatore tooproduce un asset che contenga una traccia audio invisibile all'utente quando l'input non dispone di alcun audio, specificare il valore di "InsertSilenceIfNoAudio" hello.

È possibile eseguire qualsiasi hello MES predefiniti documentati in [questo](media-services-mes-presets-overview.md) sezione e rendere hello seguente modifica:

### <a name="json-preset"></a>Set di impostazioni JSON
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a>Set di impostazioni XML
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <a id="deinterlacing"></a>Disabilitare il deinterlacciamento automatico
I clienti non devono toodo alcuna operazione se sono ad esempio hello interlacciata toobe contenuto automaticamente deallocare interlacciata. Una volta deinterlacciamento dei automatica hello in hello (impostazione predefinita) MES hello automaticamente il rilevamento di fotogrammi interlacciati e solo interlaces deallocare frame contrassegnati come interlacciata.

È possibile disattivare deinterlacciamento dei automatica hello. Questa opzione non è consigliata.

### <a name="json-preset"></a>Set di impostazioni JSON
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a>Set di impostazioni XML
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <a id="audio_only"></a>Impostazioni predefinite solo audio
In questa sezione vengono illustrate due impostazioni predefinite MES solo audio: Audio AAC e Audio AAC di buona qualità.

### <a name="aac-audio"></a>Audio ACC
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a>Audio AAC di buona qualità
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="concatenate"></a>Concatenare due o più file video

Hello seguente viene illustrato come è possibile generare un set di impostazioni tooconcatenate due o più file video. nello scenario più comune di Hello è quando si desidera tooadd un'intestazione o un video principale di toohello finale. Hello scopo viene utilizzato quando i file video hello in fase di modifica insieme condividono proprietà (risoluzione video, frequenza dei fotogrammi, conteggio traccia audio e così via). È necessario prestare attenzione non toomix video di frequenze diverse o con un numero diverso di tracce audio.

>[!NOTE]
>Hello struttura corrente della funzionalità di concatenazione hello prevede che hello input clip video sono coerenti in termini di risoluzione, frequenza dei fotogrammi e così via. 

### <a name="requirements-and-considerations"></a>Problemi e considerazioni

* I video di input devono contenere solo una traccia audio.
* Video di input devono tutti avere hello stessa frequenza dei fotogrammi.
* È necessario caricare i video in asset separati e impostare video hello come file primario hello ogni asset.
* È necessario durata hello tooknow dei video.
* Hello predefiniti negli esempi seguenti si presuppone che tutti i video di input hello inizino con un timestamp pari a zero. Sono necessari valori di StartTime hello toomodify se video hello con un timestamp di inizio diversi, come avviene in genere hello con gli archivi in tempo reale.
* Hello JSON predefinito rende i riferimenti espliciti toohello AssetID valori hello di asset di input.
* codice di esempio Hello si presuppone che hello che JSON predefinito è stato salvato come file locale tooa, ad esempio "C:\supportFiles\preset.json". Si presuppone inoltre che siano state create due asset caricando due file video, di cui si conosce hello valori AssetID risultanti.
* Hello frammento di codice e JSON predefinito viene illustrato un esempio della concatenazione di due file video. È possibile estenderlo toomore rispetto a due video da:

  1. Attività chiamata. InputAssets.Add() ripetutamente tooadd altri video, in ordine.
  2. Rendendo corrispondente Modifica elemento toohello "origini" hello JSON, dall'aggiunta di più voci, hello stesso ordine.

### <a name="net-code"></a>Codice .NET

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a>Set di impostazioni JSON

Aggiornare personalizzati predefiniti con gli ID degli asset hello che si desidera tooconcatenate e con intervallo di tempo appropriato hello per ogni video.

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="crop"></a>Ritagliare video con Media Encoder Standard
Vedere hello [ritagliare video con Media Encoder Standard](media-services-crop-video.md) argomento.

## <a id="no_video"></a>Inserire una traccia video quando l'input non ha video

Per impostazione predefinita, se si invia un codificatore toohello input che contiene solo audio e video non hello asset di output contiene file che contengono dati solo audio. Alcuni lettori, tra cui Azure Media Player (vedere [questo](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) potrebbe non essere in grado di toohandle questi flussi. È possibile utilizzare un output di traccia video monocromatica toohello tooadd di codificatore questa impostazione tooforce hello in tale scenario.

> [!NOTE]
> Una dimensione di hello aumenta traccia video output di hello forzando hello codificatore tooinsert Asset di output e hello in tal modo i costi sostenuti per attività di codifica hello. È consigliabile eseguire test tooverify questo aumento incide solo modesta sugli addebiti mensili.
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a>Inserimento di video a solo hello più bassa velocità in bit

Si supponga che si utilizza una velocità in bit più codifica predefinito, ad esempio ["H264 bitrate multiplo con risoluzione 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode all'intero catalogo per lo streaming, che contiene una combinazione di file solo audio e video di input. In questo scenario, quando l'input hello dispone di alcun monitor, è opportuno tooforce hello codificatore tooinsert un video monocromatico rilevare al solo hello più bassa velocità in bit, come tooinserting anziché video a velocità in bit ogni output. tooachieve, è necessario hello toouse **InsertBlackIfNoVideoBottomLayerOnly** flag.

È possibile eseguire qualsiasi hello MES predefiniti documentati in [questo](media-services-mes-presets-overview.md) sezione e rendere hello seguente modifica:

#### <a name="json-preset"></a>Set di impostazioni JSON
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>Set di impostazioni XML

Quando si utilizza XML, utilizzare una condizione = "InsertBlackIfNoVideoBottomLayerOnly" come un attributo di toohello **H264Video** elemento e condizione = "InsertSilenceIfNoAudio" come attributo troppo**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a>Inserimento di video a tutte le velocità in bit di output
Si supponga che si utilizza una velocità in bit più codifica predefinito, ad esempio ["H264 bitrate multiplo con risoluzione 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode all'intero catalogo per lo streaming, che contiene una combinazione di file solo audio e video di input. In questo scenario, quando l'input hello dispone di alcun monitor, è opportuno tooforce hello codificatore tooinsert tenere traccia di un video monocromatico a tutte le velocità di output di hello in. Ciò garantisce che l'output di attività sono tutte omogeneo con riguardo toonumber di tracce video e le tracce audio. tooachieve, è necessario toospecify hello flag "InsertBlackIfNoVideo".

È possibile eseguire qualsiasi hello MES predefiniti documentati in [questo](media-services-mes-presets-overview.md) sezione e rendere hello seguente modifica:

#### <a name="json-preset"></a>Set di impostazioni JSON
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>Set di impostazioni XML

Quando si utilizza XML, utilizzare una condizione = "InsertBlackIfNoVideo" come un attributo di toohello **H264Video** elemento e condizione = "InsertSilenceIfNoAudio" come attributo troppo**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <a id="rotate_video"></a>Ruotare un video
Hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supporta rotazione dagli angoli di utilizzabile come 0, 90, 180 o 270. comportamento predefinito di Hello è "Auto", in cui tenta toodetect hello rotazione metadati nel file video in ingresso hello e compensare relativo. Sono inclusi i seguenti hello **origini** tooone elemento hello predefiniti definiti in [questo](media-services-mes-presets-overview.md) sezione:

### <a name="json-preset"></a>Set di impostazioni JSON
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a>Set di impostazioni XML
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

Vedere anche [questo](media-services-mes-schema.md#PreserveResolutionAfterRotation) argomento per ulteriori informazioni sulla modalità di interpretazione delle impostazioni di larghezza e altezza hello in hello codificatore hello predefinito, quando viene attivato compensazione di rotazione.

È possibile utilizzare hello valore "0" tooindicate toohello codificatore tooignore rotazione dei metadati, se presente, nel video di input hello.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Vedere anche
[Panoramica sulla codifica dei servizi multimediali](media-services-encode-asset.md)
