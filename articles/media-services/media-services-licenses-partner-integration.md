---
title: aaaUsing partner toodeliver Widevine licenze di servizi multimediali tooAzure | Documenti Microsoft
description: In questo articolo viene descritto come usare Azure Media Services (AMS) toodeliver un flusso che viene crittografato in modo dinamico dal sistema AMS con PlayReady e Widevine DRMs. la licenza PlayReady Hello proviene dal server licenze PlayReady di servizi multimediali e viene recapitata licenze Widevine dal server licenze castLabs.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5bcad5a4-c0bb-4871-9cce-808a913c53e6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 3c18a8a22ced239931dea5385020194bd6d83f28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-partners-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="54881-104">Con i partner toodeliver Widevine licenze tooAzure servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="54881-104">Using partners toodeliver Widevine licenses tooAzure Media Services</span></span>
## <a name="overview"></a><span data-ttu-id="54881-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="54881-105">Overview</span></span>
<span data-ttu-id="54881-106">Servizi multimediali di Microsoft Azure consente toodeliver CHE MPEG-DASH protetto con DRM Widevine, che vengono crittografati in base hello specifica CENC (Common Encryption).</span><span class="sxs-lookup"><span data-stu-id="54881-106">Microsoft Azure Media Services enables you toodeliver MPEG-DASH protected with Widevine DRM, which is encrypted per hello Common Encryption (CENC) specification.</span></span>

<span data-ttu-id="54881-107">A partire da Media Services .NET SDK versione 3.5.2 hello, servizi multimediali consente di tooconfigure Widevine modello di licenza e ottenere licenze Widevine.</span><span class="sxs-lookup"><span data-stu-id="54881-107">Starting with hello Media Services .NET SDK version 3.5.2, Media Services enables you tooconfigure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="54881-108">È inoltre possibile utilizzare hello seguente toohelp partner AMS di consegnare licenze Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="54881-108">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

## <a name="castlabs"></a><span data-ttu-id="54881-109">castLabs</span><span class="sxs-lookup"><span data-stu-id="54881-109">castLabs</span></span>
<span data-ttu-id="54881-110">È possibile utilizzare [castLabs](http://castlabs.com/company/partners/azure/) licenze Widevine toodeliver.</span><span class="sxs-lookup"><span data-stu-id="54881-110">You can use [castLabs](http://castlabs.com/company/partners/azure/) toodeliver Widevine licenses.</span></span> <span data-ttu-id="54881-111">Per ulteriori informazioni, vedere [utilizzando castLabs toodeliver DRM licenze di servizi multimediali tooAzure](media-services-castlabs-integration.md)</span><span class="sxs-lookup"><span data-stu-id="54881-111">For more information, see [Using castLabs toodeliver DRM licenses tooAzure Media Services](media-services-castlabs-integration.md)</span></span>

## <a name="axinom"></a><span data-ttu-id="54881-112">Axinom</span><span class="sxs-lookup"><span data-stu-id="54881-112">Axinom</span></span>
<span data-ttu-id="54881-113">È possibile utilizzare [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) licenze Widevine toodeliver.</span><span class="sxs-lookup"><span data-stu-id="54881-113">You can use [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) toodeliver Widevine licenses.</span></span> <span data-ttu-id="54881-114">Per ulteriori informazioni, vedere [toodeliver Axinom con DRM licenze di servizi multimediali tooAzure](media-services-axinom-integration.md)</span><span class="sxs-lookup"><span data-stu-id="54881-114">For more information, see [Using Axinom toodeliver DRM licenses tooAzure Media Services](media-services-axinom-integration.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="54881-115">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="54881-115">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="54881-116">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="54881-116">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="54881-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="54881-117">See also</span></span>
[<span data-ttu-id="54881-118">Uso della crittografia comune dinamica PlayReady e/o Widevine</span><span class="sxs-lookup"><span data-stu-id="54881-118">Using PlayReady and/or Widevine dynamic common encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="54881-119">Blog di Mingfei</span><span class="sxs-lookup"><span data-stu-id="54881-119">Mingfei’s blog</span></span>](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)

