---
title: aaaHow toocrop video con Media Encoder Standard - Azure | Documenti Microsoft
description: Questo articolo viene illustrato come video toocrop con Media Encoder Standard.
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 7628f674-2005-4531-8b61-d7a4f53e46ba
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/09/2017
ms.author: anilmur;juliako;
ms.openlocfilehash: 2b4ac3d96228b93c890a38c57c4913988de1e8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a>Ritagliare video con Media Encoder Standard
È possibile utilizzare supporti codificatore Standard (MES) toocrop il video di input. Il ritaglio è il processo di hello di selezione di una finestra rettangolare all'interno di fotogrammi video hello e codifica solo i pixel hello all'interno di tale finestra. Consente di illustrare il processo di hello Hello seguente diagramma.

![Ritagliare un video](./media/media-services-crop-video/media-services-crop-video01.png)

Si supponga di che avere come input un video con risoluzione di 1920x1080 pixel (proporzioni 16:9), ma ha nere (pillar caselle) hello sinistro e destro, in modo che solo una finestra di 4:3 o 1440 x 1080 pixel contiene video attivo. È possibile utilizzare MES toocrop o modificare le barre di hello nero e codificare area 1440 x 1080 hello.

Ritaglio in MES è una fase di pre-elaborazione, pertanto i parametri di ritaglio hello in set di impostazioni di codifica hello applicano toohello video di input originale. La codifica è una fase successiva, e le impostazioni di larghezza/altezza hello applicano toohello *pre-elaborato* video e non i video originale toohello. Quando si progetta il set di impostazioni è necessario seguente hello toodo: (a) selezionare i parametri di ritaglio hello in base a video di input originale hello e (b) il codificare le impostazioni in base hello ritagliata video. Se non corrispondono il codificare toohello impostazioni ritagliata video, l'output di hello non sarà come previsto.

Hello [seguente](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) argomento viene illustrato come un processo di codifica con MES toocreate e come toospecify personalizzato preimpostato per hello attività di codifica. 

## <a name="creating-a-custom-preset"></a>Creazione di un set di impostazioni personalizzato
Nell'esempio hello illustrato nel diagramma hello:

1. L'input originale è 1920x1080
2. È necessario toobe ritagliata output tooan di 1440 x 1080, viene centrata nel frame input hello
3. Ciò equivale a un offset X (1920 - 1440)/2 = 240 e un offset Y pari a zero
4. Hello larghezza e altezza del rettangolo di ritaglio hello sono rispettivamente 1440 e 1080,
5. In hello fase codifica, hello chiedere tooproduce tre livelli, sono rispettivamente risoluzioni 1440 x 1080, 960 x 720 e 480 x 360

### <a name="json-preset"></a>Set di impostazioni JSON
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "Crop": {
                "X": 240,
                "Y": 0,
                "Width": 1440,
                "Height": 1080
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
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1440,
              "Height": 1080,
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
              "Bitrate": 1250,
              "MaxBitrate": 1250,
              "BufferWindow": "00:00:05",
              "Width": 480,
              "Height": 360,
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


## <a name="restrictions-on-cropping"></a>Restrizioni relative al ritaglio
Hello ritaglio funzionalità deve essere toobe manuale. È necessario tooload l'input video in uno strumento di modificando appropriato che consente di selezionare i frame di interesse, posizionare hello cursore toodetermine offset per il rettangolo di ritaglio hello, toodetermine hello set di impostazioni di codifica che è ottimizzato per quel particolare video, e così via. Questa funzionalità non è stata progettata tooenable ad esempio: rilevamento automatico e la rimozione dei bordi neri letterbox/formato pillarbox nell'input video.

I vincoli seguenti si applicano toohello ritaglio funzionalità. Se questi non vengono soddisfatte, hello codificare attività può non riuscire o produrre un output imprevisto.

1. salve le coordinate e le dimensioni del rettangolo di ritaglio hello hanno toofit all'interno di video di input hello
2. Come indicato in precedenza, hello larghezza e altezza in hello alle impostazioni di codifica sono toohello toocorrespond ritagliata video
3. Ritaglio applica toovideos acquisiti in modalità orizzontale (ovvero non applicabile toovideos registrate con uno smartphone contenute in verticale o in modalità verticale)
4. Il ritaglio funziona in modo ottimale con video progressivo acquisito con pixel quadrati

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Passaggio successivo
Apprendimento toohelp percorsi di che conoscere funzionalità eccellenti offerta dal sistema AMS servizi multimediali di Azure, vedere.  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
