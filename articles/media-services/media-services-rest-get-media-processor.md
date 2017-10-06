---
title: aaa come tooget un'istanza di processore di contenuti multimediali usando REST | Documenti Microsoft
description: Informazioni su come toocreate tooencode di componente processore una media, convertire il formato, crittografare o decrittografare il contenuto multimediale per servizi multimediali di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f9ff1997-0da6-4528-aaed-792837e5be41
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 9f423648ab73c90405c64895ce0f5b6a457862e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-a-media-processor-instance"></a>Come tooget un'istanza del processore di contenuti multimediali
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a>Overview
In Servizi multimediali un processore di contenuti multimediali è un componente che gestisce un'attività di elaborazione specifica, ad esempio la codifica, la conversione del formato, la crittografia o la decrittografia di contenuti multimediali. In genere creare un processore di contenuti multimediali quando si crea un'attività tooencode, crittografare o convertire il formato del contenuto multimediale hello.

## <a name="azure-media-processors"></a>Processori di contenuti multimediali di Azure 

Hello argomento fornisce elenchi di processori di contenuti multimediali:

* [Processori di contenuti multimediali di codifica](scenarios-and-availability.md#encoding-media-processors)
* [Processori di contenuti multimediali di analisi](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
>Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP. Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>Connessione dei servizi tooMedia

Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali. È necessario effettuare le chiamate successive toohello nuovo URI.

## <a name="get-a-media-processor"></a>Ottenere un processore di contenuti multimediali.

Hello chiamata REST seguente viene illustrato come istanza di un processore di contenuti multimediali tooget in base al nome (in questo caso, **Media Encoder Standard**). 

Richiesta:

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

Risposta:

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }


## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Passaggi successivi
Ora che è stato appreso come tooget un'istanza di processore di contenuti multimediali, andare toohello [come tooEncode un Asset](media-services-rest-get-started.md) argomento in cui è visualizzate come toouse hello Media Encoder Standard tooencode un asset.

