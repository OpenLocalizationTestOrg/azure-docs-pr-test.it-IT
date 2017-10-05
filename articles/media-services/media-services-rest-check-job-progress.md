---
title: Come controllare lo stato dei processi mediante l'API REST | Microsoft Docs
description: Informazioni su come tenere traccia dello stato dei processi.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a1a1f956-c035-448a-af9c-5ac15fcce9dd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: fea4383e81f3ca21955252cf1d573f1b347b5a38
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-check-job-progress"></a><span data-ttu-id="cc3b6-103">Procedura: Controllare lo stato dei processi</span><span class="sxs-lookup"><span data-stu-id="cc3b6-103">How to: check job progress</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc3b6-104">Portale</span><span class="sxs-lookup"><span data-stu-id="cc3b6-104">Portal</span></span>](media-services-portal-check-job-progress.md)
> * [<span data-ttu-id="cc3b6-105">.NET</span><span class="sxs-lookup"><span data-stu-id="cc3b6-105">.NET</span></span>](media-services-check-job-progress.md)
> * [<span data-ttu-id="cc3b6-106">REST</span><span class="sxs-lookup"><span data-stu-id="cc3b6-106">REST</span></span>](media-services-rest-check-job-progress.md)
> 
> 

<span data-ttu-id="cc3b6-107">Quando si esegue un processo, spesso è necessario monitorarne l'avanzamento.</span><span class="sxs-lookup"><span data-stu-id="cc3b6-107">When you run jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="cc3b6-108">È possibile trovare lo stato dell'entità Job mediante la relativa proprietà State.</span><span class="sxs-lookup"><span data-stu-id="cc3b6-108">You can find out the Job status by using the Job's State property.</span></span> <span data-ttu-id="cc3b6-109">Per altre informazioni sulla proprietà State, vedere [Proprietà dell'entità Job](https://docs.microsoft.com/rest/api/media/operations/job#job_entity_properties).</span><span class="sxs-lookup"><span data-stu-id="cc3b6-109">For more information on the State property, see [Job Entity Properties](https://docs.microsoft.com/rest/api/media/operations/job#job_entity_properties).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="cc3b6-110">Connettersi a Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="cc3b6-110">Connect to Media Services</span></span>

<span data-ttu-id="cc3b6-111">Per informazioni su come connettersi all'API AMS, vedere [Accedere all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="cc3b6-111">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="cc3b6-112">Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="cc3b6-112">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="cc3b6-113">Le chiamate successive dovranno essere effettuate al nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="cc3b6-113">You must make subsequent calls to the new URI.</span></span>

## <a name="check-job-progress"></a><span data-ttu-id="cc3b6-114">Controllare lo stato dei processi</span><span class="sxs-lookup"><span data-stu-id="cc3b6-114">Check job progress</span></span>

<span data-ttu-id="cc3b6-115">Richiesta:</span><span class="sxs-lookup"><span data-stu-id="cc3b6-115">Request:</span></span>

    GET https://media.windows.net/api/Jobs()?$filter=Id%20eq%20'nb%3Ajid%3AUUID%3Af3c43f94-327f-2347-90bb-3bf79f8559f1'&$top=1 HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423640758&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=z5yFIG%2bk8Z2G2aXABqM60P9smHNKD7P4BfSxXanwKFc%3d
    x-ms-version: 2.11
    Host: media.windows.net



<span data-ttu-id="cc3b6-116">Risposta:</span><span class="sxs-lookup"><span data-stu-id="cc3b6-116">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 450
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d9b83c57-e26c-4d10-a20b-2be634c4b6a8
    request-id: 91d2be35-20ed-4e1c-a147-e82cd000c193
    x-ms-request-id: 91d2be35-20ed-4e1c-a147-e82cd000c193
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains

    {"odata.metadata":"https://media.windows.net/api/$metadata#Jobs","value":[{"Id":"nb:jid:UUID:f3c43f94-327f-2347-90bb-3bf79f8559f1","Name":"Encoding BigBuckBunny into to H264 Adaptive Bitrate MP4 Set 720p","Created":"2015-02-11T01:46:08.897","LastModified":"2015-02-11T01:46:08.897","EndTime":null,"Priority":0,"RunningDuration":0.0,"StartTime":"2015-02-11T01:46:16.58","State":2,"TemplateId":null,"JobNotificationSubscriptions":[]}]} 


## <a name="media-services-learning-paths"></a><span data-ttu-id="cc3b6-117">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="cc3b6-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cc3b6-118">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="cc3b6-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="cc3b6-119">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="cc3b6-119">See also</span></span>

[<span data-ttu-id="cc3b6-120">Informazioni generali sull'API REST di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="cc3b6-120">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)
