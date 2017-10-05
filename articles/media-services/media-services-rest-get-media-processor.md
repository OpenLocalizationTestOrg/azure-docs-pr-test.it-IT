---
title: Come creare un'istanza del processore di contenuti multimediali usando REST | Microsoft Docs
description: Informazioni su come creare un componente del processore di contenuti multimediali per codificare, decodificare, convertire il formato, crittografare o decrittografare contenuti multimediali per Servizi multimediali di Azure.
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
ms.openlocfilehash: 4ad90ad979c5bd74fc55155098c88d5c13cb12e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="bf059-103">Come ottenere un'istanza del processore di contenuti multimediali</span><span class="sxs-lookup"><span data-stu-id="bf059-103">How to get a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf059-104">.NET</span><span class="sxs-lookup"><span data-stu-id="bf059-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="bf059-105">REST</span><span class="sxs-lookup"><span data-stu-id="bf059-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="bf059-106">Overview</span><span class="sxs-lookup"><span data-stu-id="bf059-106">Overview</span></span>
<span data-ttu-id="bf059-107">In Servizi multimediali un processore di contenuti multimediali è un componente che gestisce un'attività di elaborazione specifica, ad esempio la codifica, la conversione del formato, la crittografia o la decrittografia di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="bf059-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="bf059-108">Un processore multimediale viene generalmente creato durante la creazione di un'attività per la codifica, la crittografia o la conversione di formato di contenuto multimediale.</span><span class="sxs-lookup"><span data-stu-id="bf059-108">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="bf059-109">Processori di contenuti multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="bf059-109">Azure media processors</span></span> 

<span data-ttu-id="bf059-110">L'argomento seguente fornisce elenchi di processori di contenuti multimediali:</span><span class="sxs-lookup"><span data-stu-id="bf059-110">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="bf059-111">Processori di contenuti multimediali di codifica</span><span class="sxs-lookup"><span data-stu-id="bf059-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="bf059-112">Processori di contenuti multimediali di analisi</span><span class="sxs-lookup"><span data-stu-id="bf059-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="bf059-113">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="bf059-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="bf059-114">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="bf059-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="bf059-115">Connettersi a Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="bf059-115">Connect to Media Services</span></span>

<span data-ttu-id="bf059-116">Per informazioni su come connettersi all'API AMS, vedere [Accedere all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="bf059-116">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="bf059-117">Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="bf059-117">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="bf059-118">Le chiamate successive dovranno essere effettuate al nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="bf059-118">You must make subsequent calls to the new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="bf059-119">Ottenere un processore di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="bf059-119">Get a media processor</span></span>

<span data-ttu-id="bf059-120">La chiamata REST seguente mostra come ottenere un'istanza del processore di contenuti multimediali per nome, in questo caso **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="bf059-120">The following REST call shows how to get a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="bf059-121">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="bf059-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="bf059-122">Risposta:</span><span class="sxs-lookup"><span data-stu-id="bf059-122">Response:</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="bf059-123">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="bf059-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bf059-124">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="bf059-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="bf059-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bf059-125">Next Steps</span></span>
<span data-ttu-id="bf059-126">Dopo avere ottenuto un'istanza del processore di contenuti multimediali, passare all'argomento [Come codificare un asset](media-services-rest-get-started.md) che illustra come usare Media Encoder Standard per codificare un asset.</span><span class="sxs-lookup"><span data-stu-id="bf059-126">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-rest-get-started.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

