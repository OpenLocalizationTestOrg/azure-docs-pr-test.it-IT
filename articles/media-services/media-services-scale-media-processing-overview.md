---
title: Panoramica di elaborazione multimediale aaaScaling | Documenti Microsoft
description: Questo argomento presenta una panoramica del ridimensionamento dell'elaborazione multimediale con Servizi multimediali di Azure.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 780ef5c2-3bd6-4261-8540-6dee77041387
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: d17531f79d4c1e0d0fa544c4fb5c083684e706fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-media-processing-overview"></a>Panoramica del ridimensionamento dell'elaborazione multimediale
Questa pagina viene fornita una panoramica di come e perché l'elaborazione di tooscale media. 

## <a name="overview"></a>Panoramica
Un account di servizi multimediali è associato a un tipo di unità riservate, che determina la velocità di hello con cui vengono elaborati i file multimediali l'elaborazione delle attività. È possibile scegliere tra segue hello i tipi di unità riservata: **S1**, **S2**, o **S3**. Ad esempio, hello stesso processo di codifica viene eseguito più velocemente quando si utilizza hello **S2** toohello di confronto del tipo di unità riservata **S1** tipo. Per ulteriori informazioni, vedere hello [tipi di unità riservate](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/).

Inoltre toospecifying hello riservati di tipo di unità, è possibile specificare l'account tooprovision con unità riservate. numero di Hello di unità riservate sottoposte a provisioning determina il numero di hello delle attività multimediali che possono essere elaborate contemporaneamente in un determinato account. Ad esempio, se l'account dispone di 5 unità riservate, quindi verrà eseguita contemporaneamente a condizione attività cinque multimediali sono pari al numero di attività toobe elaborati. le attività rimanenti Hello rimarranno in attesa nella coda di hello e saranno prelevate per l'elaborazione in sequenza al termine di un'attività in esecuzione. Se per un account non sono state fornite unità riservate, le attività verranno prelevate in sequenza. In questo caso, hello tempo di attesa tra un completamento di attività e hello avvio della successiva dipenderà disponibilità hello delle risorse di sistema hello.

## <a name="choosing-between-different-reserved-unit-types"></a>Scelta tra i tipi diversi di unità riservata
Hello nella tabella seguente consente di decidere quando si sceglie tra diverse velocità di codifica. Inoltre, fornisce alcuni casi benchmark e vengono forniti gli URL di firma di accesso condiviso che è possibile utilizzare i video toodownload in cui è possibile eseguire dei test personali:

| Scenari | **S1** | **S2** | **S3** |
| --- | --- | --- | --- |
| Caso d'uso previsto |Codifica con velocità in bit singola. <br/>File SD o con risoluzione inferiore, non dipendenti dall'ora, a basso costo. |Codifica con velocità in bit singola e multipla.<br/>Uso normale per la codifica SD e HD. |Codifica con velocità in bit singola e multipla.<br/>Video Full HD e con risoluzione 4K. Codifica dipendente dall'ora con completamento più rapido. |
| Benchmark |[File di input: della durata di 5 minuti, con risoluzione 640x360p, a 29,97 fotogrammi al secondo](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_360p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).<br/><br/>File MP4 a velocità in bit singola tooa, codifica in hello stessa risoluzione, richiede circa 11 minuti. |[File di input: della durata di 5 minuti, con risoluzione 1280 x 720p, a 29,97 fotogrammi al secondo](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_720p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).<br/><br/>La codifica con set di impostazioni "Codec video H264 a bitrate singolo con risoluzione 720p" richiede circa 5 minuti.<br/><br/>La codifica con set di impostazioni "Codec video H.264 a bitrate multipli con risoluzione 720p" richiede circa 11,5 minuti. |[File di input: della durata di 5 minuti, con risoluzione 1920x1080p, a 29,97 fotogrammi al secondo](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_1080p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D). <br/><br/>La codifica con set di impostazioni "Codec video H264 a bitrate singolo con risoluzione 1080p" richiede circa 2,7 minuti.<br/><br/>La codifica con "Codec video H.264 a bitrate multiplo con risoluzione 1080p" preconfigurato richiede circa 5,7 minuti. |

## <a name="considerations"></a>Considerazioni
> [!IMPORTANT]
> Vedere le considerazioni descritte in questa sezione.  
> 
> 

* Unità riservate di lavoro per la parallelizzazione di tutta l'elaborazione di supporti di memorizzazione, tra cui l'indicizzazione di processi tramite Azure Media Indexer.  Tuttavia, a differenza della codifica, l'indicizzazione di processi non viene elaborata più velocemente con unità riservate più veloci.
* Se si utilizza hello condiviso pool, vale a dire, senza alcuna unità riservate, quindi le attività di codifica sono hello stesse prestazioni come in russo S1. Tuttavia, non sono previsti tempi toohello limite superiore destinare le attività nello stato in coda, e in qualsiasi momento, verrà eseguito al massimo una sola attività.
* Hello seguendo i data Center non offra hello **S2** tipo di unità riservata: Brasile meridionale e India occidentale.
* Hello centro dati seguente non offre hello **S3** tipo di unità riservata: India ovest.

## <a name="billing"></a>Fatturazione

Vengono addebitati i minuti di uso effettivo di Media Reserved Unit. Per informazioni dettagliate, vedere la sezione Domande frequenti su hello di hello [dei prezzi di servizi multimediali](https://azure.microsoft.com/pricing/details/media-services/) pagina.   

## <a name="quotas-and-limitations"></a>Quote e limitazioni
Per informazioni su quote e limitazioni e tooopen un ticket di supporto, vedere [quote e limitazioni](media-services-quotas-and-limitations.md).

## <a name="next-step"></a>Passaggio successivo
È possibile ottenere scalabilità supporti l'elaborazione dell'attività con una di queste tecnologie hello: 

> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portale](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

