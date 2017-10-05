---
title: Usare i lettori esistenti per la riproduzione dei contenuti - Azure | Documentazione Microsoft
description: "Questo argomento elenca i lettori esistenti che è possibile usare per la riproduzione dei propri contenuti."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 48f373b013b1192c353352b801876d706d91dd28
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="playing-your-content-with-existing-players"></a><span data-ttu-id="63c8f-103">Riproduzione di contenuti con i lettori esistenti</span><span class="sxs-lookup"><span data-stu-id="63c8f-103">Playing your content with existing players</span></span>
<span data-ttu-id="63c8f-104">Servizi multimediali di Azure supporta molti formati di streaming noti, ad esempio Smooth Streaming, HTTP Live Streaming (HLS) e MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="63c8f-104">Azure Media Services supports many popular streaming formats, such as Smooth Streaming, HTTP Live Streaming, and MPEG-Dash.</span></span> <span data-ttu-id="63c8f-105">Questo argomento descrive i lettori esistenti che possono essere usati per testare i propri flussi.</span><span class="sxs-lookup"><span data-stu-id="63c8f-105">This topic points you to existing players that you can use to test your streams.</span></span>

### <a name="the-azure-portal-media-services-content-player"></a><span data-ttu-id="63c8f-106">Lettore di contenuti di Servizi multimediali del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="63c8f-106">The Azure portal Media Services content player</span></span>
<span data-ttu-id="63c8f-107">Il portale di **Azure** fornisce un lettore di contenuti che può essere usato per testare il proprio video.</span><span class="sxs-lookup"><span data-stu-id="63c8f-107">The **Azure** portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="63c8f-108">Fare clic sul video desiderato (assicurarsi che sia stato [pubblicato](media-services-portal-publish.md)) e fare clic sul pulsante **Play** nella parte inferiore del portale.</span><span class="sxs-lookup"><span data-stu-id="63c8f-108">Click on the desired video (make sure it was [published](media-services-portal-publish.md)) and click the **Play** button at the bottom of the portal.</span></span>

<span data-ttu-id="63c8f-109">Considerazioni applicabili:</span><span class="sxs-lookup"><span data-stu-id="63c8f-109">Some considerations apply:</span></span>

* <span data-ttu-id="63c8f-110">Il **LETTORE DI CONTENUTI DI SERVIZI MULTIMEDIALI** esegue la riproduzione dall'endpoint di streaming predefinito.</span><span class="sxs-lookup"><span data-stu-id="63c8f-110">The **MEDIA SERVICES CONTENT PLAYER** plays from the default streaming endpoint.</span></span> <span data-ttu-id="63c8f-111">Se si vuole eseguire la riproduzione da un endpoint di streaming diverso, usare un altro lettore,</span><span class="sxs-lookup"><span data-stu-id="63c8f-111">If you want to play from a non-default streaming endpoint, use another player.</span></span> <span data-ttu-id="63c8f-112">ad esempio [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="63c8f-112">For example, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a><span data-ttu-id="63c8f-114">Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="63c8f-114">Azure Media Player</span></span>
<span data-ttu-id="63c8f-115">Usare il [lettore multimediale di Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html) per riprodurre i contenuti (in chiaro o protetti) in uno dei seguenti formati:</span><span class="sxs-lookup"><span data-stu-id="63c8f-115">Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to playback your content (clear or protected) in any of the following formats:</span></span>

* <span data-ttu-id="63c8f-116">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="63c8f-116">Smooth Streaming</span></span>
* <span data-ttu-id="63c8f-117">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="63c8f-117">MPEG DASH</span></span>
* <span data-ttu-id="63c8f-118">HLS</span><span class="sxs-lookup"><span data-stu-id="63c8f-118">HLS</span></span>
* <span data-ttu-id="63c8f-119">MP4 progressivo</span><span class="sxs-lookup"><span data-stu-id="63c8f-119">Progressive MP4</span></span>

### <a name="flash-player"></a><span data-ttu-id="63c8f-120">Flash Player</span><span class="sxs-lookup"><span data-stu-id="63c8f-120">Flash Player</span></span>
#### <a name="aes-encrypted-with-token"></a><span data-ttu-id="63c8f-121">Con crittografia AES con token</span><span class="sxs-lookup"><span data-stu-id="63c8f-121">AES-encrypted with Token</span></span>
[<span data-ttu-id="63c8f-122">http://aestoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="63c8f-122">http://aestoken.azurewebsites.net</span></span>](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a><span data-ttu-id="63c8f-123">Lettori Silverlight</span><span class="sxs-lookup"><span data-stu-id="63c8f-123">Silverlight Players</span></span>
#### <a name="monitoring"></a><span data-ttu-id="63c8f-124">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="63c8f-124">Monitoring</span></span>
[<span data-ttu-id="63c8f-125">http://smf.cloudapp.net/healthmonitor</span><span class="sxs-lookup"><span data-stu-id="63c8f-125">http://smf.cloudapp.net/healthmonitor</span></span>](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a><span data-ttu-id="63c8f-126">PlayReady con token</span><span class="sxs-lookup"><span data-stu-id="63c8f-126">PlayReady with Token</span></span>
[<span data-ttu-id="63c8f-127">http://sltoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="63c8f-127">http://sltoken.azurewebsites.net</span></span>](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a><span data-ttu-id="63c8f-128">Lettori DASH</span><span class="sxs-lookup"><span data-stu-id="63c8f-128">DASH Players</span></span>
[<span data-ttu-id="63c8f-129">http://dashplayer.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="63c8f-129">http://dashplayer.azurewebsites.net</span></span>](http://dashplayer.azurewebsites.net)

[<span data-ttu-id="63c8f-130">http://dashif.org</span><span class="sxs-lookup"><span data-stu-id="63c8f-130">http://dashif.org</span></span>](http://dashif.org)

### <a name="other"></a><span data-ttu-id="63c8f-131">Altri</span><span class="sxs-lookup"><span data-stu-id="63c8f-131">Other</span></span>
<span data-ttu-id="63c8f-132">Per testare gli URL HLS è inoltre possibile usare:</span><span class="sxs-lookup"><span data-stu-id="63c8f-132">To test HLS URLs you can also use:</span></span>

* <span data-ttu-id="63c8f-133">**Safari** in un dispositivo iOS o</span><span class="sxs-lookup"><span data-stu-id="63c8f-133">**Safari** on an iOS device or</span></span>
* <span data-ttu-id="63c8f-134">**Lettore HLS 3ivx** in un dispositivo Windows.</span><span class="sxs-lookup"><span data-stu-id="63c8f-134">**3ivx HLS Player** on Windows.</span></span>

## <a name="developing-video-players"></a><span data-ttu-id="63c8f-135">Sviluppo di lettori video</span><span class="sxs-lookup"><span data-stu-id="63c8f-135">Developing video players</span></span>
<span data-ttu-id="63c8f-136">Per informazioni su come sviluppare i propri lettori, vedere [Sviluppo di lettori di contenuti video](media-services-develop-video-players.md)</span><span class="sxs-lookup"><span data-stu-id="63c8f-136">For information about how to develop your own players, see [Developing video players](media-services-develop-video-players.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="63c8f-137">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="63c8f-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="63c8f-138">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="63c8f-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
