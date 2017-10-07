---
title: schema di codificatore Standard aaaMedia | Documenti Microsoft
description: argomento Hello viene fornita una panoramica dello schema Standard di codificatore multimediale di hello.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 4c060062-8ef2-41d9-834e-e81e8eafcf2e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 82bad27b9546f75557ac691ff148b46990647632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-schema"></a>Schema di Media Encoder Standard
In questo argomento vengono descritti alcuni degli elementi di hello e tipi di schema XML hello in cui [predefiniti Media Encoder Standard](media-services-mes-presets-overview.md) si basano. argomento Hello spiegazione degli elementi e i relativi valori validi. schema completo Hello verrà pubblicato in un secondo momento.  

## <a name="Preset"></a> Set di impostazioni (elemento radice)
Definisce un set di impostazioni per la codifica.  

### <a name="elements"></a>Elementi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Encoding** |[Codifica](media-services-mes-schema.md#Encoding) |Elemento radice, indica che le origini di input hello toobe codificato. |
| **Outputs** |[Outputs](media-services-mes-schema.md#Output) |Raccolta dei file dell'output desiderato. |

### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Versione**<br/><br/> Obbligatorio |**xs: decimal** |versione del set di impostazioni Hello. salve le seguenti limitazioni: valore xs:fractionDigits = valore "1" e xs:minInclusive = "1", ad esempio, **versione = "1.0"**. |

## <a name="Encoding"></a> Encoding
Contiene una sequenza di hello seguenti elementi.  

### <a name="elements"></a>Elementi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **H264Video** |[H264Video](media-services-mes-schema.md#H264Video) |Impostazioni per la codifica video H.264. |
| **AACAudio** |[AACAudio](media-services-mes-schema.md#AACAudio) |Impostazioni per la codifica audio AAC. |
| **BmpImage** |[BmpImage](media-services-mes-schema.md#BmpImage) |Impostazioni per le immagini .bmp. |
| **PngImage** |[PngImage](media-services-mes-schema.md#PngImage) |Impostazioni per le immagini .png. |
| **JpgImage** |[JpgImage](media-services-mes-schema.md#JpgImage) |Impostazioni per le immagini .jpg. |

## <a name="H264Video"></a> H264Video
### <a name="elements"></a>Elementi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **TwoPass**<br/><br/> minOccurs="0" |**xs:boolean** |Al momento è supportata solo la codifica in un passaggio. |
| **KeyFrameInterval**<br/><br/> minOccurs="0"<br/><br/> **default="00:00:02"** |**xs:time** |Determina la spaziatura tra le unità di secondi frame IDR hello fissata. Definito anche durata GOP di hello tooas. Vedere **SceneChangeDetection** (sotto) per controllare se hello codificatore può deviare da questo valore. |
| **SceneChangeDetection**<br/><br/> minOccurs="0"<br/><br/> default="false" |**xs:boolean** |Se set tootrue, tentativi di codificatore scena toodetect modificare video hello e inserisce una cornice IDR. |
| **Complexity**<br/><br/> minOccurs="0"<br/><br/> default="Balanced" |**xs:string** |Controlli hello compromesso tra velocità e video di qualità la codifica. Potrebbe essere uno dei seguenti valori hello: **velocità**, **bilanciato**, o **qualità**<br/><br/> Valore predefinito: **Balanced** |
| **SyncMode**<br/><br/> minOccurs="0" | |La funzionalità sarà disponibile in una delle prossime versioni. |
| **H264Layers**<br/><br/> minOccurs="0" |[H264Layers](media-services-mes-schema.md#H264Layers) |Raccolta di livelli video di output. |

### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Condition** |**xs:string** | Quando l'input hello dispone di alcun monitor, è opportuno tooforce hello codificatore tooinsert una traccia video monocromatica. toodo utilizzati, condizione = "InsertBlackIfNoVideoBottomLayerOnly" (tooinsert un video con solo hello più bassa velocità in bit) o una condizione = "InsertBlackIfNoVideo" (tooinsert un video con velocità in bit output tutti). Per altre informazioni, vedere [questo](media-services-advanced-encoding-with-mes.md#no_video) argomento.|

## <a name="H264Layers"></a> H264Layers

Per impostazione predefinita, se si invia un codificatore toohello input che contiene solo audio e video non hello asset di output conterrà i file audio soltanto i dati. Alcuni lettori potrebbero non essere possibile toohandle tali flussi di output. È possibile utilizzare hello del H264Video **InsertBlackIfNoVideo** attributo l'impostazione di un output di traccia video toohello tooforce hello codificatore tooadd in tale scenario. Per altre informazioni, vedere [questo](media-services-advanced-encoding-with-mes.md#no_video) argomento.
              
### <a name="elements"></a>Elementi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **H264Layer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[H264Layer](media-services-mes-schema.md#H264Layer) |Raccolta di livelli H264. |

## <a name="H264Layer"></a> H264Layer
> [!NOTE]
> Limiti video si basano sui valori hello descritti in hello [livelli H264](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Levels) tabella.  
> 
> 

### <a name="elements"></a>Elementi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Profilo**<br/><br/> minOccurs="0"<br/><br/> default="Auto" |**xs:string** |Potrebbe essere uno dei seguenti hello **xs: String** valori: **Auto**, **della linea di base**, **Main**, **elevata**. |
| **Level**<br/><br/> minOccurs="0"<br/><br/> default="Auto" |**xs:string** | |
| **Bitrate**<br/><br/> minOccurs="0" |**xs:int** |velocità in bit Hello usata per questo livello video, specificato in kbps. |
| **MaxBitrate**<br/><br/> minOccurs="0" |**xs:int** |Hello massima velocità in bit usata per questo livello video, specificato in kbps. |
| **BufferWindow**<br/><br/> minOccurs="0"<br/><br/> default="00:00:05" |**xs:time** |Lunghezza del buffer video hello. |
| **Width**<br/><br/> minOccurs="0" |**xs:int** |Larghezza del frame di output video hello, in pixel.<br/><br/> Al momento è necessario specificare entrambi i valori di larghezza e altezza, è necessario numeri pari toobe Hello larghezza e altezza. |
| **Height**<br/><br/> minOccurs="0" |**xs:int** |Altezza del frame di output video hello, in pixel.<br/><br/> Al momento è necessario specificare entrambi i valori di larghezza e altezza, è necessario numeri pari toobe Hello larghezza e altezza.|
| **BFrames**<br/><br/> minOccurs="0" |**xs:int** |Numero di fotogrammi B tra frame di riferimento. |
| **ReferenceFrames**<br/><br/> minOccurs="0"<br/><br/> default=”3” |**xs:int** |Numero di frame di riferimento in un GOP. |
| **EntropyMode**<br/><br/> minOccurs="0"<br/><br/> default="Cabac" |**xs:string** |Potrebbe essere uno dei seguenti valori hello: **Cabac** e **Cavlc**. |
| **FrameRate**<br/><br/> minOccurs="0" |numero razionale |Determina frequenza dei fotogrammi hello dell'output di hello video. Utilizzare l'impostazione predefinita di hello "1/0" toolet hello codificatore utilizzo della frequenza fotogrammi stesso come hello input video. I valori consentiti sono previsti toobe frequenze di fotogrammi video comuni, come illustrato di seguito. Tuttavia, è consentito qualunque numero razionale. Ad esempio 1/1 corrisponderebbe a 1 fps e sarebbe valido.<br/><br/> - 12/1 (12 fps)<br/><br/> - 15/1 (15 fps)<br/><br/> - 24/1 (24 fps)<br/><br/> - 24.000/1.001 (23,976 fps)<br/><br/> - 25/1 (25 fps)<br/><br/>  - 30/1 (30 fps)<br/><br/> - 30.000/1.001 (29,97 fps) <br/> <br/>**Nota** se si sta creando un predefinito per la codifica più velocità in bit personalizzato, tutti i livelli di hello preimpostato **deve** utilizzare hello stesso valore della frequenza dei fotogrammi.|
| **AdaptiveBFrame**<br/><br/> minOccurs="0" |**xs:boolean** |Copiare da Azure Media Encoder |
| **Slices**<br/><br/> minOccurs="0"<br/><br/> default="0" |**xs:int** |Stabilisce il numero di sezioni in cui è suddiviso un frame. È consigliabile usare il valore predefinito. |

## <a name="AACAudio"></a> AACAudio
 Contiene una sequenza di hello segue gli elementi e gruppi.  

 Per altre informazioni su AAC, vedere [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding).  

### <a name="elements"></a>Elementi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Profilo**<br/><br/> minOccurs="0 "<br/><br/> default="AACLC" |**xs:string** |Potrebbe essere uno dei seguenti valori hello: **AACLC**, **HEAACV1**, o **HEAACV2**. |

### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Condition** |**xs:string** |tooforce hello codificatore tooproduce un asset che contenga una traccia audio invisibile all'utente quando l'input non dispone di alcun audio, specificare il valore di "InsertSilenceIfNoAudio" hello.<br/><br/> Per impostazione predefinita, se si invia un codificatore toohello input che contiene solo i video e audio non quindi hello asset di output conterrà i file che contengono dati solo video. Alcuni lettori potrebbero non essere possibile toohandle tali flussi di output. È possibile utilizzare questo tooadd di codificatore hello tooforce impostazione un output di traccia audio invisibile all'utente toohello in tale scenario. |

### <a name="groups"></a>Gruppi
| riferimento | Descrizione |
| --- | --- |
| [AudioGroup](media-services-mes-schema.md#AudioGroup)<br/><br/> minOccurs="0" |Vedere la descrizione di [AudioGroup](media-services-mes-schema.md#AudioGroup) tooknow hello numero appropriato di canali, frequenza di campionamento e velocità in bit che può essere impostato per ogni profilo. |

## <a name="AudioGroup"></a> AudioGroup
Per informazioni dettagliate su quali sono i valori validi per ogni profilo, vedere tabella "Dettagli codec Audio" hello che segue.  

### <a name="elements"></a>Elementi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Channels**<br/><br/> minOccurs="0" |**xs:int** |numero di Hello di canali audio codificati. di seguito Hello sono opzioni valide: 1, 2, 5, 6 e 8.<br/><br/> Valore predefinito: 2. |
| **SamplingRate**<br/><br/> minOccurs="0" |**xs:int** |frequenza di campionamento audio Hello, specificato in Hz. |
| **Bitrate**<br/><br/> minOccurs="0" |**xs:int** |velocità in bit Hello utilizzato quando la codifica audio hello, specificata in kbps. |

### <a name="audio-codec-details"></a>Dettagli sui codec audio
Codec audio|Dettagli  
-----------------|---  
**AACLC**|1:<br/><br/> - 11025 : 8 &lt;= bitrate &lt; 16<br/><br/> - 12000 : 8 &lt;= bitrate &lt; 16<br/><br/> - 16000 : 8 &lt;= bitrate &lt;32<br/><br/>- 22050 : 24 &lt;= bitrate &lt; 32<br/><br/> - 24000 : 24 &lt;= bitrate &lt; 32<br/><br/> - 32000 : 32 &lt;= bitrate &lt;= 192<br/><br/> - 44100 : 56 &lt;= bitrate &lt;= 288<br/><br/> - 48000 : 56 &lt;= bitrate &lt;= 288<br/><br/> - 88200 : 128 &lt;= bitrate &lt;= 288<br/><br/> - 96000 : 128 &lt;= bitrate &lt;= 288<br/><br/> 2:<br/><br/> - 11025 : 16 &lt;= bitrate &lt; 24<br/><br/> - 12000 : 16 &lt;= bitrate &lt; 24<br/><br/> - 16000 : 16 &lt;= bitrate &lt; 40<br/><br/> - 22050 : 32 &lt;= bitrate &lt; 40<br/><br/> - 24000 : 32 &lt;= bitrate &lt; 40<br/><br/> - 32000 : 40 &lt;= bitrate &lt;= 384<br/><br/> - 44100 : 96 &lt;= bitrate &lt;= 576<br/><br/> - 48000 : 96 &lt;= bitrate &lt;= 576<br/><br/> - 88200 : 256 &lt;= bitrate &lt;= 576<br/><br/> - 96000 : 256 &lt;= bitrate &lt;= 576<br/><br/> 5/6:<br/><br/> - 32000 : 160 &lt;= bitrate &lt;= 896<br/><br/> - 44100 : 240 &lt;= bitrate &lt;= 1024<br/><br/> - 48000 : 240 &lt;= bitrate &lt;= 1024<br/><br/> - 88200 : 640 &lt;= bitrate &lt;= 1024<br/><br/> - 96000 : 640 &lt;= bitrate &lt;= 1024<br/><br/> 8:<br/><br/> - 32000 : 224 &lt;= bitrate &lt;= 1024<br/><br/> - 44100 : 384 &lt;= bitrate &lt;= 1024<br/><br/> - 48000 : 384 &lt;= bitrate &lt;= 1024<br/><br/> - 88200 : 896 &lt;= bitrate &lt;= 1024<br/><br/> - 96000 : 896 &lt;= bitrate &lt;= 1024  
**HEAACV1**|1:<br/><br/> - 22050 : bitrate = 8<br/><br/> - 24000 : 8 &lt;= bitrate &lt;= 10<br/><br/> - 32000 : 12 &lt;= bitrate &lt;= 64<br/><br/> - 44100 : 20 &lt;= bitrate &lt;= 64<br/><br/> - 48000 : 20 &lt;= bitrate &lt;= 64<br/><br/> - 88200 : bitrate = 64<br/><br/> 2:<br/><br/> - 32000 : 16 &lt;= bitrate &lt;= 128<br/><br/> - 44100 : 16 &lt;= bitrate &lt;= 128<br/><br/> - 48000 : 16 &lt;= bitrate &lt;= 128<br/><br/> - 88200 : 96 &lt;= bitrate &lt;= 128<br/><br/> - 96000 : 96 &lt;= bitrate &lt;= 128<br/><br/> 5/6:<br/><br/> - 32000 : 64 &lt;= bitrate &lt;= 320<br/><br/> - 44100 : 64 &lt;= bitrate &lt;= 320<br/><br/> - 48000 : 64 &lt;= bitrate &lt;= 320<br/><br/> - 88200 : 256 &lt;= bitrate &lt;= 320<br/><br/> - 96000 : 256 &lt;= bitrate &lt;= 320<br/><br/> 8:<br/><br/> - 32000 : 96 &lt;= bitrate &lt;= 448<br/><br/> - 44100 : 96 &lt;= bitrate &lt;= 448<br/><br/> - 48000 : 96 &lt;= bitrate &lt;= 448<br/><br/> - 88200 : 384 &lt;= bitrate &lt;= 448<br/><br/> - 96000 : 384 &lt;= bitrate &lt;= 448  
**HEAACV2**|2:<br/><br/> - 22050 : 8 &lt;= bitrate &lt;= 10<br/><br/> - 24000 : 8 &lt;= bitrate &lt;= 10<br/><br/> - 32000 : 12 &lt;= bitrate &lt;= 64<br/><br/> - 44100 : 20 &lt;= bitrate &lt;= 64<br/><br/> - 48000 : 20 &lt;= bitrate &lt;= 64<br/><br/> - 88200 : 64 &lt;= bitrate &lt;= 64  
  

## <a name="Clip"></a> Clip
### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **StartTime** |**xs:duration** |Specifica l'ora di inizio hello di una presentazione. il valore di Hello di StartTime deve toomatch hello i timestamp assoluto del video di input hello. Ad esempio, se hello primo frame del video di input hello ha un timestamp di 12:00:10.000 quindi StartTime deve essere almeno 12:00:10.000 o versione successiva. |
| **Duration** |**xs:duration** |Specifica la durata di hello di una presentazione (ad esempio, aspetto della sovrimpressione video hello). |

## <a name="Output"></a> Output
### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **FileName** |**xs:string** |nome Hello hello del file di output.<br/><br/> È possibile utilizzare le macro descritte nella seguente di nomi di file di output di tabella toobuild hello hello. ad esempio:<br/><br/> **"Outputs": [      {       "FileName": "{Basename}*{Resolution}*{Bitrate}.mp4",       "Format": {         "Type": "MP4Format"       }     }   ]** |

### <a name="macros"></a>Macro
| Macro | Descrizione |
| --- | --- |
| **{Basename}** |Se si esegue la codifica VoD, hello {nome} è hello primi 32 caratteri della proprietà di AssetFile.Name hello del file primario di hello hello asset di input.<br/><br/> Se l'asset di input hello è un archivio in tempo reale, quindi hello {nome} è derivato da attributi trackName hello nel manifesto server hello. Se si inviano un processo di secondaria utilizzando hello TopBitrate, come in: "< VideoStream\>TopBitrate < / VideoStream\>", il file di output di hello contiene video, quindi hello {nome} è hello primi 32 caratteri del trackName hello di hello livello video con velocità in bit più elevata hello.<br/><br/> Se invece si inviano un processo secondaria usando tutte di hello input velocità in bit, ad esempio "< VideoStream\>* < / VideoStream\>", il file di output di hello contiene video, quindi {nome} è hello primi 32 caratteri del trackName hello di livello video Hello corrispondente. |
| **{Codec}** |Esegue il mapping troppo "H264" per video e "AAC" per l'audio. |
| **{Bitrate}** |Hello destinazione velocità in bit video se il file di output di hello contenente video e audio o velocità in bit audio di destinazione se il file di output di hello solo audio. il valore di Hello utilizzato è velocità in bit hello in kbps. |
| **{Channel}** |Numero di canali audio se il file hello contiene audio. |
| **{Width}** |Larghezza del video, in pixel, nel file di output di hello, se il file hello contiene video hello. |
| **{Height}** |Altezza del video, in pixel, nel file di output di hello, se il file hello contiene video hello. |
| **{Extension}** |Eredita la proprietà "Type" per il file di output di hello hello. nome del file di output di Hello avrà un'estensione che è uno di: "mp4", "Servizi terminal", "jpg", "png" o "bmp". |
| **{Index}** |Obbligatorio per l'anteprima. Deve essere presente solo una volta. |

## <a name="Video"></a> Video (il tipo complesso eredita da Codec)
### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Inizia** |**xs:string** | |
| **Step** |**xs:string** | |
| **Range** |**xs:string** | |
| **PreserveResolutionAfterRotation** |**xs:boolean** |Per informazioni dettagliate, vedere hello seguente sezione: [PreserveResolutionAfterRotation](media-services-mes-schema.md#PreserveResolutionAfterRotation) |

### <a name="PreserveResolutionAfterRotation"></a> PreserveResolutionAfterRotation
Si consiglia di flag di PreserveResolutionAfterRotation toouse hello in combinazione con la risoluzione dei valori espressi in termini di percentuale (Width = "100%" Height = "100%").  

Per impostazione predefinita, hello codificare le impostazioni di risoluzione (larghezza, altezza) in hello supporti codificatore Standard (MES) predefiniti sono orientati ai video con grado 0 rotazione. Ad esempio, se il video di input è 1280x720 con rotazione zero gradi, quindi predefiniti hello assicurarsi che l'output di hello disponga hello stessa risoluzione. Vedere la figura seguente.  

![MESRoation1](./media/media-services-shemas/media-services-mes-roation1.png) 

Tuttavia, ciò significa che se i video di input hello è stato acquisito con rotazione diverso da zero (ad es. un tablet o smartphone tenuto verticalmente), quindi MES per impostazione predefinita verrà applicata hello codificare risoluzione video di input toohello impostazioni (larghezza, altezza) e quindi compensare rotazione hello. Ad esempio, vedere l'immagine di hello riportato di seguito. Hello predefinito Usa la larghezza = "100%" Height = "100%", MES interpreta come richiedere hello output toobe 1280 pixel e 720 pixel in altezza. Dopo la rotazione video hello, quindi riduce toofit immagine hello in tale finestra, iniziali aree toopillar-box in hello sinistro e destro.  

![MESRoation2](./media/media-services-shemas/media-services-mes-roation2.png) 

Se hello precedente non è il comportamento di hello desiderato, è quindi possibile creare di hello PreserveResolutionAfterRotation flag e impostarla troppo "true" (valore predefinito è "false"). Pertanto se il set di impostazioni ha larghezza = "100%" Height = "100%" e impostare troppo "true", un video di input che è 1280 pixel e 720 pixel in altezza con rotazione di 90 gradi produrrà un output con rotazione zero gradi, ma pari a 720 pixel di larghezza e 1280 PreserveResolutionAfterRotation pixel in altezza. Vedere hello immagine riportata di seguito.  

![MESRoation3](./media/media-services-shemas/media-services-mes-roation3.png) 

## <a name="FormatGroup"></a> FormatGroup (gruppo)
### <a name="elements"></a>Elementi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **BmpFormat** |**BmpFormat** | |
| **PngFormat** |**PngFormat** | |
| **JpgFormat** |**JpgFormat** | |

## <a name="BmpLayer"></a> BmpLayer
### <a name="element"></a>Elemento
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |

### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="PngLayer"></a> PngLayer
### <a name="element"></a>Elemento
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |

### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="JpgLayer"></a> JpgLayer
### <a name="element"></a>Elemento
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |
| **Quality**<br/><br/> minOccurs="0" |**xs:int** |I valori validi sono 1(worst)-100(best) |

### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="PngLayers"></a> PngLayers
### <a name="elements"></a>Elementi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **PngLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[PngLayer](media-services-mes-schema.md#PngLayer) | |

## <a name="BmpLayers"></a> BmpLayers
### <a name="elements"></a>Elementi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **BmpLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[BmpLayer](media-services-mes-schema.md#BmpLayer) | |

## <a name="JpgLayers"></a> JpgLayers
### <a name="elements"></a>Elementi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **JpgLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[JpgLayer](media-services-mes-schema.md#JpgLayer) | |

## <a name="BmpImage"></a> BmpImage (il tipo complesso eredita da Video)
### <a name="elements"></a>Elementi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Png layers |

## <a name="JpgImage"></a> JpgImage (il tipo complesso eredita da Video)
### <a name="elements"></a>Elementi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Png layers |

## <a name="PngImage"></a> PngImage (il tipo complesso eredita da Video)
### <a name="elements"></a>Elementi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Png layers |

## <a name="examples"></a>esempi
Per osservare esempi di set di impostazioni XML compilati in base a questo schema, vedere [Task Presets for MES (Media Encoder Standard)](media-services-mes-presets-overview.md) (Set di impostazioni delle attività di MES (Media Encoder Standard)).

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

