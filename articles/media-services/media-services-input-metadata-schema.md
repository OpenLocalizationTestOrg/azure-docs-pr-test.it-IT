---
title: schema dei metadati di input di servizi multimediali aaaAzure | Documenti Microsoft
description: Hello argomento viene fornita una panoramica dello schema dei metadati di input di servizi multimediali di Azure.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a>Metadati di input
Un processo di codifica è associato a un asset di input (o attività) in cui si desidera tooperform alcune attività di codifica.  Al termine di un'attività, viene generato un asset di output.  asset di output di hello e così via. contiene inoltre un file con i metadati sull'asset di input hello Hello output contenente video, audio, le anteprime, il manifesto. nome del file XML dei metadati di hello Hello ha hello seguente formato: &lt;asset_id&gt;<id_asset>_metadata.XML (ad esempio, d 57-8 41114ad3 eb5e - 4c 92-5354e2b7d4a4_metadata.xml), in cui &lt;asset_id&gt; è hello AssetId valore dell'asset di input hello.  

Se si desidera tooexamine hello metadati file, è possibile creare un **SAS** download e l'indicatore di posizione hello computer locale tooyour di file. È possibile trovare un esempio su come toocreate un localizzatore SAS e scaricare un file [utilizzando hello Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).  

Questo argomento vengono elementi hello e tipi di schema XML hello per metadati di input quali hello (&lt;asset_id&gt;<asset_id>_metadata.XML) è basato.  Per informazioni sul file hello che contiene i metadati sull'asset di output di hello, vedere [Output metadati](media-services-output-metadata-schema.md).  

> [!NOTE]
> È possibile trovare hello [codice Schema](media-services-input-metadata-schema.md#code) un [file XML di esempio](media-services-input-metadata-schema.md#xml) alla fine di hello di questo argomento.  
> 
> 

## <a name="AssetFiles"></a> Elemento radice AssetFile
Contiene una raccolta di [elemento AssetFile](media-services-input-metadata-schema.md#AssetFile)s per il processo di codifica hello.  

Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).  

| Nome | Descrizione |
| --- | --- |
| **AssetFile**<br /><br /> minOccurs="1" maxOccurs="unbounded" |Un singolo elemento figlio. Per altre informazioni, vedere [Elemento AssetFile](media-services-input-metadata-schema.md#AssetFile). |

## <a name="AssetFile"></a> Elemento AssetFile
 Contiene gli attributi e gli elementi che descrivono un file di asset.  

 Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Nome**<br /><br /> Obbligatorio |**xs:string** |Nome del file di asset |
| **Dimensione**<br /><br /> Obbligatorio |**xs:long** |Dimensioni del file di asset hello in byte. |
| **Duration**<br /><br /> Obbligatorio |**xs:duration** |Durata della riproduzione del contenuto. Esempio: Duration="PT25M37.757S". |
| **NumberOfStreams**<br /><br /> Obbligatorio |**xs:int** |Numero di flussi nel file di asset hello. |
| **FormatNames**<br /><br /> Obbligatorio |**xs:string** |Nomi del formato. |
| **FormatVerboseNames**<br /><br /> Obbligatorio |**xs:string** |Nomi dettagliati del formato. |
| **StartTime** |**xs:duration** |Ora di inizio del contenuto. Esempio: StartTime="PT2.669S". |
| **OverallBitRate** |**xs:int** |Velocità in bit media del file di asset hello in kbps. |

> [!NOTE]
> Hello 4 elementi figlio seguenti deve apparire in una sequenza.  
> 
> 

### <a name="child-elements"></a>Elementi figlio
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Programs**<br /><br /> minOccurs="0" | |Raccolta di tutti [elemento Programs](media-services-input-metadata-schema.md#Programs) quando il file di asset hello è in formato MPEG-TS. |
| **VideoTracks**<br /><br /> minOccurs="0" | |Ogni file di asset fisico può contenere da zero a più tracce video con interfoliazione in un formato contenitore appropriato. Questo elemento contiene una raccolta di tutti [elemento VideoTracks](media-services-input-metadata-schema.md#VideoTracks) che fanno parte del file di asset hello. |
| **AudioTrack**<br /><br /> minOccurs="0" | |Ogni file di asset fisico può contenere da zero a più tracce audio con interfoliazione in un formato contenitore appropriato. Questo elemento contiene una raccolta di tutti [elemento AudioTracks](media-services-input-metadata-schema.md#AudioTracks) che fanno parte del file di asset hello. |
| **Metadata**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |Metadati del file di asset rappresentati come stringhe chiave-valore. ad esempio:<br /><br /> **&lt;Metadata key="language" value="eng" /&gt;** |

## <a name="TrackType"></a> TrackType
Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Id**<br /><br /> Obbligatorio |**xs:int** |Indice in base zero della traccia audio o video.<br /><br /> Non è necessariamente tale hello TrackID usato in un file MP4. |
| **Codec** |**xs:string** |Stringa del codec della traccia video. |
| **CodecLongName** |**xs:string** |Nome lungo del codec della traccia audio o video. |
| **TimeBase**<br /><br /> Obbligatorio |**xs:string** |Tempo base. Esempio: TimeBase="1/48000" |
| **NumberOfFrames** |**xs:int** |Numero di frame (presenti per le tracce video). |
| **StartTime** |**xs:duration** |Ora di inizio della traccia. Esempio: StartTime="PT2.669S" |
| **Duration** |**xs:duration** |Durata della traccia. Esempio: Duration="PTSampleFormat M37.757S". |

> [!NOTE]
> Hello 2 elementi figlio seguenti deve apparire in una sequenza.  
> 
> 

### <a name="child-elements"></a>Elementi figlio
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Disposition**<br /><br /> minOccurs="0" maxOccurs="1" |[StreamDispositionType](media-services-input-metadata-schema.md#StreamDispositionType) |Contiene informazioni di presentazione (ad esempio, se una determinata traccia audio è per utenti con problemi di vista). |
| **Metadata**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |Stringhe chiave/valore generiche che possono essere utilizzati toohold un'ampia gamma di informazioni. Esempio, key="language" e value="eng". |

## <a name="AudioTrackType"></a> AudioTrackType (eredita da TrackType)
 **AudioTrackType** è un tipo globale complesso che eredita da [TrackType](media-services-input-metadata-schema.md#TrackType).  

 tipo di Hello rappresenta una specifica traccia audio nel file di asset hello.  

 Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **SampleFormat** |**xs:string** |Formato del campione. |
| **ChannelLayout** |**xs:string** |Layout del canale. |
| **Channels**<br /><br /> Obbligatorio |**xs:int** |Numero di canali audio (da 0 in su). |
| **SamplingRate**<br /><br /> Obbligatorio |**xs:int** |Frequenza di campionamento dell'audio in campioni/sec o Hz. |
| **Bitrate** |**xs:int** |Velocità in bit audio Media in bit al secondo, calcolata dal file di asset hello. Viene contato solo payload del flusso elementare hello e overhead di creazione di pacchetti hello non è incluso in questo conteggio. |
| **BitsPerSample** |**xs:int** |Bit per campione per formato wFormatTag hello digitare. |

## <a name="VideoTrackType"></a> VideoTrackType (eredita da TrackType)
**AudioTrackType** è un tipo globale complesso che eredita da [TrackType](media-services-input-metadata-schema.md#TrackType).  

tipo di Hello rappresenta una specifica traccia video nel file di asset hello.  

Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **FourCC**<br /><br /> Obbligatorio |**xs:string** |Codice FourCC del codec video. |
| **Profilo** |**xs:string** |Profilo della traccia video. |
| **Level** |**xs:string** |Livello della traccia video. |
| **PixelFormat** |**xs:string** |Formato pixel della traccia video. |
| **Width**<br /><br /> Obbligatorio |**xs:int** |Larghezza del video codificata in pixel. |
| **Height**<br /><br /> Obbligatorio |**xs:int** |Altezza del video codificata in pixel. |
| **DisplayAspectRatioNumerator**<br /><br /> Obbligatorio |**xs:double** |Numeratore delle proporzioni della visualizzazione video. |
| **DisplayAspectRatioDenominator**<br /><br /> Obbligatorio |**xs:double** |Denominatore delle proporzioni della visualizzazione video. |
| **DisplayAspectRatioDenominator**<br /><br /> Obbligatorio |**xs:double** |Numeratore delle proporzioni del campione video. |
| **SampleAspectRatioNumerator** |**xs:double** |Numeratore delle proporzioni del campione video. |
| **SampleAspectRatioNumerator** |**xs:double** |Denominatore delle proporzioni del campione video. |
| **FrameRate**<br /><br /> Obbligatorio |**xs: decimal** |Frequenza dei frame misurata in formato .3F. |
| **Bitrate** |**xs:int** |Velocità in bit video Media in kilobit al secondo, calcolata dal file di asset hello. Viene contato solo payload del flusso elementare hello e overhead di creazione di pacchetti hello non è incluso. |
| **MaxGOPBitrate** |**xs:int** |Velocità media in bit Max GOP per la traccia video, in kilobit al secondo. |
| **HasBFrames** |**xs:int** |Numero di traccia video dei fotogrammi B. |

## <a name="MetadataType"></a> MetadataType
**MetadataType** è un tipo globale complesso che descrive i metadati di un file di asset come stringhe chiave-valore. Esempio, key="language" e value="eng".  

Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **key**<br /><br /> Obbligatorio |**xs:string** |chiave di Hello nella coppia chiave/valore hello. |
| **value**<br /><br /> Obbligatorio |**xs:string** |valore di Hello nella coppia chiave/valore hello. |

## <a name="ProgramType"></a> ProgramType
**ProgramType** è un tipo globale complesso che descrive un programma.  

### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **ProgramId**<br /><br /> Obbligatorio |**xs:int** |ID programma |
| **NumberOfPrograms**<br /><br /> Obbligatorio |**xs:int** |Numero di programmi. |
| **PmtPid**<br /><br /> Obbligatorio |**xs:int** |Tabelle di mappa dei programmi (PMT) che contengono informazioni sui programmi.  Per altre informazioni, vedere [PMT](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT). |
| **PcrPid**<br /><br /> Obbligatorio |**xs:int** |Usato dal decodificatore. Per altre informazioni, vedere [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR). |
| **StartPTS** |**xs: long** |Timestamp di avvio della presentazione. |
| **EndPTS** |**xs: long** |Timestamp di fine della presentazione. |

## <a name="StreamDispositionType"></a> StreamDispositionType
**StreamDispositionType** è un tipo globale complesso che descrive il flusso di hello.  

Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Attributi
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Default**<br /><br /> Obbligatorio |**xs:int** |Impostare questo tooindicate too1 attributo di che si tratta presentazione predefinita hello. |
| **Dub**<br /><br /> Obbligatorio |**xs:int** |Impostare questa proprietà tooindicate di too1 questo attributo è hello riregistrare presentazione. |
| **Original**<br /><br /> Obbligatorio |**xs:int** |Impostare questo tooindicate too1 attributo di che si tratta presentazione originale hello. |
| **Comment**<br /><br /> Obbligatorio |**xs:int** |Impostare questo tooindicate too1 attributo questa traccia contiene dei commenti. |
| **Lyrics**<br /><br /> Obbligatorio |**xs:int** |Impostare questo tooindicate too1 attributo questa traccia contiene del testo. |
| **Karaoke**<br /><br /> Obbligatorio |**xs:int** |Impostare questo tooindicate too1 attributo rappresenta hello traccia karaoke (musica di sottofondo, senza canto). |
| **Forced**<br /><br /> Obbligatorio |**xs:int** |Impostare questo tooindicate too1 attributo di che si tratta presentazione di hello forzato. |
| **HearingImpaired**<br /><br /> Obbligatorio |**xs:int** |Impostare questo tooindicate too1 attributo che questa traccia è per udenti hello. |
| **VisualImpaired**<br /><br /> Obbligatorio |**xs:int** |Impostare questo tooindicate too1 attributo che questa traccia è per hello vedenti. |
| **CleanEffects**<br /><br /> Obbligatorio |**xs:int** |Impostare questo tooindicate too1 attributo che questa traccia contiene effetti di trasparenza. |
| **AttachedPic**<br /><br /> Obbligatorio |**xs:int** |Impostare questo tooindicate too1 attributo che questa traccia contiene immagini. |

## <a name="Programs"></a> Elemento Programs
Elemento wrapper contenente più elementi **Program**.  

### <a name="child-elements"></a>Elementi figlio
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **Program**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[ProgramType](media-services-input-metadata-schema.md#ProgramType) |Per i file di asset in formato MPEG-TS, contiene informazioni sui programmi nel file di asset hello. |

## <a name="VideoTracks"></a> Elemento VideoTracks
 Elemento wrapper contenente più elementi **VideoTrack**.  

 Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).  

### <a name="child-elements"></a>Elementi figlio
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **VideoTrack**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[VideoTrackType (eredita da TrackType)](media-services-input-metadata-schema.md#VideoTrackType) |Contiene informazioni su tracce video presenti nel file di asset hello. |

## <a name="AudioTracks"></a> Elemento AudioTrack
 Elemento wrapper contenente più elementi **AudioTrack**.  

 Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).  

### <a name="elements"></a>Elementi figlio
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **AudioTrack**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[AudioTrackType (eredita da TrackType)](media-services-input-metadata-schema.md#AudioTrackType) |Contiene informazioni su tracce audio presenti nel file di asset hello. |

## <a name="code"></a> Codice schema
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>hello media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <a name="xml"></a> Esempio XML
Hello Ecco un esempio di file di metadati di Input hello.  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

