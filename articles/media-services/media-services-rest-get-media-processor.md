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
# <a name="how-tooget-a-media-processor-instance"></a><span data-ttu-id="60209-103">Come tooget un'istanza del processore di contenuti multimediali</span><span class="sxs-lookup"><span data-stu-id="60209-103">How tooget a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="60209-104">.NET</span><span class="sxs-lookup"><span data-stu-id="60209-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="60209-105">REST</span><span class="sxs-lookup"><span data-stu-id="60209-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="60209-106">Overview</span><span class="sxs-lookup"><span data-stu-id="60209-106">Overview</span></span>
<span data-ttu-id="60209-107">In Servizi multimediali un processore di contenuti multimediali è un componente che gestisce un'attività di elaborazione specifica, ad esempio la codifica, la conversione del formato, la crittografia o la decrittografia di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="60209-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="60209-108">In genere creare un processore di contenuti multimediali quando si crea un'attività tooencode, crittografare o convertire il formato del contenuto multimediale hello.</span><span class="sxs-lookup"><span data-stu-id="60209-108">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="60209-109">Processori di contenuti multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="60209-109">Azure media processors</span></span> 

<span data-ttu-id="60209-110">Hello argomento fornisce elenchi di processori di contenuti multimediali:</span><span class="sxs-lookup"><span data-stu-id="60209-110">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="60209-111">Processori di contenuti multimediali di codifica</span><span class="sxs-lookup"><span data-stu-id="60209-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="60209-112">Processori di contenuti multimediali di analisi</span><span class="sxs-lookup"><span data-stu-id="60209-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="60209-113">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="60209-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="60209-114">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="60209-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="60209-115">Connessione dei servizi tooMedia</span><span class="sxs-lookup"><span data-stu-id="60209-115">Connect tooMedia Services</span></span>

<span data-ttu-id="60209-116">Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="60209-116">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="60209-117">Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="60209-117">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="60209-118">È necessario effettuare le chiamate successive toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="60209-118">You must make subsequent calls toohello new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="60209-119">Ottenere un processore di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="60209-119">Get a media processor</span></span>

<span data-ttu-id="60209-120">Hello chiamata REST seguente viene illustrato come istanza di un processore di contenuti multimediali tooget in base al nome (in questo caso, **Media Encoder Standard**).</span><span class="sxs-lookup"><span data-stu-id="60209-120">hello following REST call shows how tooget a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="60209-121">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="60209-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="60209-122">Risposta:</span><span class="sxs-lookup"><span data-stu-id="60209-122">Response:</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="60209-123">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="60209-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="60209-124">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="60209-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="60209-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="60209-125">Next Steps</span></span>
<span data-ttu-id="60209-126">Ora che è stato appreso come tooget un'istanza di processore di contenuti multimediali, andare toohello [come tooEncode un Asset](media-services-rest-get-started.md) argomento in cui è visualizzate come toouse hello Media Encoder Standard tooencode un asset.</span><span class="sxs-lookup"><span data-stu-id="60209-126">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-rest-get-started.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

