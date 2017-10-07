---
title: aaa"pubblicare il contenuto con hello portale di Azure | Documenti di Microsoft"
description: In questa esercitazione vengono illustrati i passaggi hello della pubblicazione del contenuto con hello portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a><span data-ttu-id="95708-103">Pubblicare il contenuto con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="95708-103">Publish content with hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95708-104">Portale</span><span class="sxs-lookup"><span data-stu-id="95708-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="95708-105">.NET</span><span class="sxs-lookup"><span data-stu-id="95708-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="95708-106">REST</span><span class="sxs-lookup"><span data-stu-id="95708-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="95708-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="95708-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="95708-108">toocomplete questa esercitazione, è necessario un account di Azure.</span><span class="sxs-lookup"><span data-stu-id="95708-108">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="95708-109">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95708-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="95708-110">tooprovide l'utente con un URL che possa essere utilizzati toostream o scaricare il contenuto, è innanzitutto necessario troppo "pubblica" l'asset creando un localizzatore.</span><span class="sxs-lookup"><span data-stu-id="95708-110">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="95708-111">I localizzatori forniscono accesso toofiles contenuti in hello asset.</span><span class="sxs-lookup"><span data-stu-id="95708-111">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="95708-112">Servizi multimediali supporta due tipi di localizzatori:</span><span class="sxs-lookup"><span data-stu-id="95708-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="95708-113">Streaming localizzatori (OnDemandOrigin) usati per streaming adattivo (ad esempio, toostream MPEG DASH, HLS o Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="95708-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="95708-114">toocreate un localizzatore di streaming dell'asset deve contenere un file con estensione ISM.</span><span class="sxs-lookup"><span data-stu-id="95708-114">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="95708-115">Localizzatori progressivi (SAS) usati per la distribuzione di video tramite download progressivo.</span><span class="sxs-lookup"><span data-stu-id="95708-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="95708-116">È possibile utilizzare asset Smooth Streaming tooplay un URL di streaming ha hello seguente formato.</span><span class="sxs-lookup"><span data-stu-id="95708-116">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="95708-117">aggiungere toobuild un URL di streaming HLS (formato = m3u8-aapl) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="95708-117">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="95708-118">aggiungere toobuild un URL di streaming di contenuto MPEG DASH (formato = mpd-tempo-csf) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="95708-118">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="95708-119">Un URL SAS è hello seguente formato.</span><span class="sxs-lookup"><span data-stu-id="95708-119">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="95708-120">Per altre informazioni, vedere [Panoramica della distribuzione di contenuti](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="95708-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="95708-121">Se si utilizza i localizzatori toocreate portale hello prima marzo 2015, sono stati creati con una data di scadenza per anno a due indicatori di posizione.</span><span class="sxs-lookup"><span data-stu-id="95708-121">If you used hello portal toocreate locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="95708-122">tooupdate data di scadenza su un indicatore di posizione, utilizzare [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) o [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API.</span><span class="sxs-lookup"><span data-stu-id="95708-122">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="95708-123">Si noti che quando si aggiorna la data di scadenza hello di un localizzatore SAS, hello URL viene modificato.</span><span class="sxs-lookup"><span data-stu-id="95708-123">Note that when you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="95708-124">toouse hello portale toopublish un asset</span><span class="sxs-lookup"><span data-stu-id="95708-124">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="95708-125">toouse hello portale toopublish un asset, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="95708-125">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="95708-126">In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="95708-126">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="95708-127">Selezionare **Impostazioni** > **Asset**.</span><span class="sxs-lookup"><span data-stu-id="95708-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="95708-128">Selezionare asset hello che si desidera toopublish.</span><span class="sxs-lookup"><span data-stu-id="95708-128">Select hello asset that you want toopublish.</span></span>
4. <span data-ttu-id="95708-129">Fare clic su hello **pubblica** pulsante.</span><span class="sxs-lookup"><span data-stu-id="95708-129">Click hello **Publish** button.</span></span>
5. <span data-ttu-id="95708-130">Selezionare il tipo di localizzatore hello.</span><span class="sxs-lookup"><span data-stu-id="95708-130">Select hello locator type.</span></span>
6. <span data-ttu-id="95708-131">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="95708-131">Press **Add**.</span></span>
   
    ![Pubblica](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="95708-133">Hello URL verrà aggiunto l'elenco toohello di **URL pubblicato**.</span><span class="sxs-lookup"><span data-stu-id="95708-133">hello URL will be added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="95708-134">Riprodurre il contenuto dal portale hello</span><span class="sxs-lookup"><span data-stu-id="95708-134">Play content from hello portal</span></span>
<span data-ttu-id="95708-135">portale di Azure Hello fornisce un lettore di contenuti che è possibile utilizzare tootest video.</span><span class="sxs-lookup"><span data-stu-id="95708-135">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="95708-136">Fare clic su video hello desiderato e quindi fare clic su hello **riprodurre** pulsante.</span><span class="sxs-lookup"><span data-stu-id="95708-136">Click hello desired video and then click hello **Play** button.</span></span>

![Pubblica](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="95708-138">Considerazioni applicabili:</span><span class="sxs-lookup"><span data-stu-id="95708-138">Some considerations apply:</span></span>

* <span data-ttu-id="95708-139">Verificare che sia stato pubblicato hello video.</span><span class="sxs-lookup"><span data-stu-id="95708-139">Make sure hello video has been published.</span></span>
* <span data-ttu-id="95708-140">Questo **Media player** riprodotto dal valore predefinito di hello endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="95708-140">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="95708-141">Se si desidera tooplay da un valore non predefinito, endpoint di streaming fare clic su URL hello toocopy e usare un altro lettore.</span><span class="sxs-lookup"><span data-stu-id="95708-141">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="95708-142">ad esempio [Lettore di Servizi multimediali di Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="95708-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="95708-143">Hello da cui si utilizza il flusso di endpoint di streaming deve essere in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="95708-143">hello streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="95708-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="95708-144">Next steps</span></span>
<span data-ttu-id="95708-145">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="95708-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="95708-146">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="95708-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

