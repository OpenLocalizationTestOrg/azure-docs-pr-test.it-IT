---
title: aaaAzure telemetria di servizi multimediali | Documenti Microsoft
description: Questo articolo offre una panoramica sulla telemetria di Servizi multimediali di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95c20ec4-c782-4063-8042-b79f95741d28
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 659e1c947a77aad0e4acacb541d95714da4775ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-telemetry"></a>Telemetria di Servizi multimediali di Azure

Azure Media Services (AMS) permette di dati di telemetria/metrica tooaccess per i propri servizi. versione corrente di Hello del sistema AMS consente di raccogliere in tempo reale dati di telemetria per **canale**, **StreamingEndpoint**e in tempo reale **archivio** entità. 

Dati di telemetria è scritto tooa tabella di archiviazione in un account di archiviazione di Azure specificato (in genere, utilizzare account di archiviazione hello associato all'account di sistema AMS). 

sistema di telemetria Hello non gestisce la conservazione dei dati. È possibile rimuovere i vecchi dati di telemetria hello mediante l'eliminazione di tabelle di archiviazione hello.

Questo argomento viene illustrato come tooconfigure e utilizzare dati di telemetria hello AMS.

## <a name="configuring-telemetry"></a>Configurare la telemetria

È possibile configurare i dati di telemetria con granularità a livello di componente. Esistono due livelli di dettaglio: "Normal" e "Verbose". Attualmente, entrambi i livelli di restituiscono hello stesse informazioni. È consigliabile toouse "normale. 

Hello seguente mostra gli argomenti come dati di telemetria tooenable:

[Abilitare la telemetria con .NET](media-services-dotnet-telemetry.md) 

[Abilitare la telemetria con REST](media-services-rest-telemetry.md)

## <a name="consuming-telemetry-information"></a>Uso delle informazioni di telemetria

Dati di telemetria viene scritto tooan tabella di archiviazione di Azure nell'account di archiviazione hello specificato durante la configurazione di telemetria per hello account di servizi multimediali. Questa sezione vengono descritte le tabelle di archiviazione hello per le metriche di hello.

È possibile utilizzare i dati di telemetria in uno dei seguenti modi hello:

- Leggere i dati direttamente da Archiviazione tabelle di Azure (ad esempio tramite hello Azure Storage SDK). Per una descrizione di hello di tabelle di archiviazione di dati di telemetria, vedere hello **utilizzo delle informazioni di telemetria** in [questo](https://msdn.microsoft.com/library/mt742089.aspx) argomento.

Or

- Usare il supporto di hello hello Media Services .NET SDK per la lettura dei dati di archiviazione, come descritto in [questo](media-services-dotnet-telemetry.md) argomento. 


schema di dati di telemetria Hello descritto di seguito è progettato toogive buone prestazioni entro i limiti di hello tabella di archiviazione di Azure:

- I dati sono partizionati dall'account ID e l'ID del servizio dati di telemetria tooallow da ogni toobe servizio eseguire una query in modo indipendente.
- Le partizioni contenere hello data toogive un ragionevole limite superiore per la dimensione della partizione hello.
- Nella fase inversa ordine tooallow hello più recente telemetria elementi toobe chiavi di riga vengono interrogate per un determinato servizio.

In questo modo molti toobe query comuni hello efficiente:

- Download parallelo e indipendente dei dati da destinare ad altri servizi.
- Recupero di tutti i dati relativi a un servizio in un certo intervallo di date.
- Il recupero dei dati più recenti di hello per un servizio.

### <a name="telemetry-table-storage-output-schema"></a>Schema di output dell'archiviazione tabelle di telemetria

Dati di telemetria vengono archiviati nella funzione di aggregazione in una tabella, "TelemetryMetrics20160321" dove "20160321" è data della tabella hello creato. Il sistema di telemetria crea una nuova tabella per ogni giornata alle ore 00:00 UTC. viene utilizzata la tabella Hello valori ricorrenti toostore di inserimento, ad esempio velocità in bit a un determinato intervallo di tempo byte inviati, e così via. 

Proprietà|Valore|Esempi/note
---|---|---
PartitionKey|{ID account}_{ID entità}|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66<br/<br/>Hello account ID è incluso in hello partizione toosimplify chiave dei flussi di lavoro in più account di servizi multimediali scrive toohello stesso account di archiviazione.
RowKey|{secondi toomidnight} _ {valore casuale}|01688_00199<br/><br/>chiave di riga Hello inizia con il numero di hello di secondi toomidnight tooallow top n le query all'interno di una partizione. Per altre informazioni, vedere [questo](../cosmos-db/table-storage-design-guide.md#log-tail-pattern) articolo. 
Timestamp|Data/ora|Auto timestamp da tabelle di Azure 2016 hello-09-09T22:43:42.241Z
Tipo|tipo di Hello di entità che hello fornisce i dati di telemetria|Channel/StreamingEndpoint/Archive<br/><br/>Il tipo di evento è semplicemente un valore stringa.
Nome|nome di Hello dell'evento di telemetria hello|ChannelHeartbeat/StreamingEndpointRequestLog
ObservedTime|si è verificato Hello ora hello telemetria evento (UTC)|2016-09-09T22:42:36.924Z<br/><br/>Hello osservata l'ora viene fornita dalla telemetria hello entità mittente hello (ad esempio un canale). Poiché possono esserci problemi di sincronizzazione tra i componenti, questo valore è approssimativo
ServiceID|{ID servizio}|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
Proprietà specifiche di entità|Come definito dall'evento hello|NomeFlusso: flusso1, bitrate 10123, ...<br/><br/>proprietà rimanenti Hello vengono definite per il tipo di evento specificato hello. Il contenuto della tabella di Azure corrisponde a coppie valore-chiave.  (ovvero, diverse righe di tabella hello hanno diversi set di proprietà).

### <a name="entity-specific-schema"></a>Schema specifico di entità

Esistono tre tipi specifici di entità telemetric di voci di dati che ogni inseriti con hello seguente frequenza:

- Endpoint di streaming: ogni 30 secondi
- Canali live: ogni minuto
- Archivio live: ogni minuto

**Endpoint di streaming**

Proprietà|Valore|esempi
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Timestamp automatico della tabella di Azure 2016-09-09T22:43:42.241Z
Tipo|Tipo|StreamingEndpoint
Nome|Nome|StreamingEndpointRequestLog
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|ID del servizio|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
HostName|Nome host dell'endpoint hello|builddemoserver.Origin.mediaservices.Windows.NET
StatusCode|Stato dei record HTTP|200
ResultCode|Dettagli del codice risultato|S_OK
RequestCount|Totale richieste nell'aggregazione hello|3
BytesSent|Insieme dei byte inviati|2987358
ServerLatency|Latenza media del server (inclusa l'archiviazione)|129
E2ELatency|Latenza end-to-end media|250

**Canale live**

Proprietà|Valore|Esempi/note
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Auto timestamp da tabelle di Azure 2016 hello-09-09T22:43:42.241Z
Tipo|Tipo|canale
Nome|Nome|ChannelHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|ID del servizio|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
TrackType|Tipo di testo traccia di testo/video/audio|video/audio
TrackName|Nome della traccia hello|video/audio_1
Bitrate|Velocità in bit della traccia|785000
CustomAttributes||   
IncomingBitrate|Velocità in bit in ingresso effettiva|784548
OverlapCount|Inserimento di sovrapposizione hello|0
DiscontinuityCount|Discontinuità di traccia|0
LastTimestamp|Timestamp degli ultimi dati inseriti|1800488800
NonincreasingCount|Numero di frammenti scartati a causa l'aumento toonon timestamp|2
UnalignedKeyFrames|Eventuali frammenti (con vari livelli di qualità) ricevuti con fotogrammi chiave non allineati |True
UnalignedPresentationTime|Eventuali frammenti (con vari livelli/tracce di qualità) ricevuti con l'ora di presentazione non allineata|True
UnexpectedBitrate|True, se la frequenza in bit audio/video calcolata/effettiva è > 40.000 bps e IncomingBitrate è = = 0 O i valori IncomingBitrate e actualBitrate sono diversi del 50% |True
Healthy|True, se <br/>overlapCount, <br/>DiscontinuityCount, <br/>NonIncreasingCount, <br/>UnalignedKeyFrames, <br/>UnalignedPresentationTime, <br/>UnexpectedBitrate<br/> sono tutti pari a 0|True <br/><br/>Integro è una funzione composita che restituisce false quando una delle seguenti condizioni attesa hello:<br/><br/>- OverlapCount > 0<br/>- DiscontinuityCount > 0<br/>- NonincreasingCount > 0<br/>- UnalignedKeyFrames == True<br/>- UnalignedPresentationTime == True<br/>- UnexpectedBitrate == True

**Archivio live**

Proprietà|Valore|Esempi/note
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Auto timestamp da tabelle di Azure 2016 hello-09-09T22:43:42.241Z
Tipo|Tipo|Archiviazione
Nome|Nome|ArchiveHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|ID del servizio|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
ManifestName|URL del programma|asset-eb149703-ed0a-483c-91c4-e4066e72cce3/a0a5cfbf-71ec-4bd2-8c01-a92a2b38c9ba.ism
TrackName|Nome della traccia hello|audio_1
TrackType|Tipo di traccia hello|Audio/video
CustomAttribute|Stringa esadecimale che opera la distinzione fra tracce diverse con lo stesso nome e la stessa velocità in bit (diverse angolazioni)|
Bitrate|Velocità in bit della traccia|785000
Healthy|True, se FragmentDiscardedCount == 0 e ArchiveAcquisitionError == False|True (questi due valori non sono presenti nella metrica hello ma sono presenti nell'evento di origine hello)<br/><br/>Integro è una funzione composita che restituisce false quando una delle seguenti condizioni attesa hello:<br/><br/>- FragmentDiscardedCount > 0<br/>- ArchiveAcquisitionError == True

## <a name="general-qa"></a>Domande generali

### <a name="how-tooconsume-metrics-data"></a>Come dati di metrica tooconsume?

Dati di metrica vengono archiviati come una serie di tabelle di Azure nell'account di archiviazione del cliente hello. Questi dati possono essere utilizzati con hello seguenti strumenti:

- SDK DI AMS
- Microsoft Azure Storage Explorer (supporta il formato di esportazione toocomma delimitati da virgole e trasformati in Excel)
- API REST

### <a name="how-toofind-average-bandwidth-consumption"></a>Come toofind medio di larghezza di banda?

il consumo di larghezza di banda media Hello è Media hello di BytesSent un intervallo di tempo.

### <a name="how-toodefine-streaming-unit-count"></a>Come numero di unità di streaming toodefine?

numero di unità di streaming Hello può essere definita come velocità effettiva di picco hello dall'endpoint di streaming del servizio hello diviso velocità effettiva di picco hello di un endpoint di streaming. Hello utilizzabile velocità effettiva di picco di un endpoint di streaming è 160 Mbps.
Si supponga, ad esempio, velocità effettiva di picco hello dal servizio di un cliente è 40 MBps (hello massimo valore BytesSent in un intervallo di tempo). Quindi, numero di unità di streaming hello è uguale too(40 MBps) * /(160 Mbps) (8 bit/byte) = 2 unità di streaming.

### <a name="how-toofind-average-requestssecond"></a>Come toofind Media richieste al secondo?

numero medio di hello toofind di richieste al secondo, calcola il numero medio di hello delle richieste (RequestCount) in un intervallo di tempo.

### <a name="how-toodefine-channel-health"></a>Come toodefine canale integrità?

Integrità del canale può essere definita come un funzione booleana composito in modo che sia false quando una delle seguenti condizioni hello:

- OverlapCount > 0
- DiscontinuityCount > 0
- NonincreasingCount > 0
- UnalignedKeyFrames == True 
- UnalignedPresentationTime == True 
- UnexpectedBitrate == True


### <a name="how-toodetect-discontinuities"></a>La modalità delle discontinuità toodetect?

discontinuità toodetect, trovare tutte le voci di dati di canale in cui DiscontinuityCount > 0. Hello corrispondente ObservedTime timestamp indica le ore hello in corrispondenza del quale si è verificato discontinuità hello.

### <a name="how-toodetect-timestamp-overlaps"></a>Come si sovrappone toodetect timestamp?

sovrapposizioni di timestamp toodetect, trovare tutte le voci di dati di canale in cui OverlapCount > 0. Hello corrispondente ObservedTime timestamp indica hello volte in cui hello si sovrappone timestamp si è verificati.

### <a name="how-toofind-streaming-request-failures-and-reasons"></a>Streaming toofind richiesta come errori e motivi?

toofind flusso degli errori delle richieste e motivi, trovare tutte le voci di dati di Endpoint di Streaming in cui ResultCode non è uguale tooS_OK. campo StatusCode corrispondente Hello indica hello causa un errore di richiesta di hello.

### <a name="how-tooconsume-data-with-external-tools"></a>Come dati tooconsume con strumenti esterni?

Dati telemetric possono essere elaborati e visualizzati con i seguenti strumenti hello:

- PowerBI
- Application Insights
- Monitoraggio di Azure (in precedenza Shoebox)
- Dashboard in tempo reale di AMS
- Portale di Azure (in attesa di rilascio)

### <a name="how-toomanage-data-retention"></a>La conservazione dei dati toomanage?

sistema di telemetria Hello non fornisce gestione della conservazione dei dati o l'eliminazione automatica dei vecchi record. Pertanto, è necessario toomanage ed eliminare manualmente i record obsoleti dalla tabella di archiviazione hello. È possibile fare riferimento a SDK toostorage come toodo è.

## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
