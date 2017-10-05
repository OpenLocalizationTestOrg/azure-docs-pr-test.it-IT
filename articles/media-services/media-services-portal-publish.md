---
title: "  Pubblicare contenuti con il portale di Azure | Microsoft Docs"
description: Questa esercitazione illustra i passaggi necessari per la pubblicazione di contenuti con il portale di Azure.
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
ms.openlocfilehash: 68a2fbdda0996cf4ba5ea3b09816bf845af756f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="publish-content-with-the-azure-portal"></a><span data-ttu-id="876ce-103">Pubblicare contenuti con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="876ce-103">Publish content with the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="876ce-104">Portale</span><span class="sxs-lookup"><span data-stu-id="876ce-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="876ce-105">.NET</span><span class="sxs-lookup"><span data-stu-id="876ce-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="876ce-106">REST</span><span class="sxs-lookup"><span data-stu-id="876ce-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="876ce-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="876ce-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="876ce-108">Per completare l'esercitazione, è necessario un account Azure.</span><span class="sxs-lookup"><span data-stu-id="876ce-108">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="876ce-109">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="876ce-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="876ce-110">Perché l'utente possa avere a disposizione un URL da usare per scaricare o riprodurre in streaming i contenuti, è prima necessario "pubblicare" un asset creando un localizzatore.</span><span class="sxs-lookup"><span data-stu-id="876ce-110">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span></span> <span data-ttu-id="876ce-111">I localizzatori forniscono l'accesso ai file contenuti nell'asset.</span><span class="sxs-lookup"><span data-stu-id="876ce-111">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="876ce-112">Servizi multimediali supporta due tipi di localizzatori:</span><span class="sxs-lookup"><span data-stu-id="876ce-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="876ce-113">Localizzatori di streaming (OnDemandOrigin) usati per lo streaming adattivo, ad esempio per riprodurre in streaming file MPEG DASH, HLS o Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="876ce-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="876ce-114">Per creare un localizzatore di streaming, l'asset deve contenere un file con estensione ISM.</span><span class="sxs-lookup"><span data-stu-id="876ce-114">To create a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="876ce-115">Localizzatori progressivi (SAS) usati per la distribuzione di video tramite download progressivo.</span><span class="sxs-lookup"><span data-stu-id="876ce-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="876ce-116">Un URL di streaming presenta il formato seguente e può essere usato per riprodurre asset Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="876ce-116">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="876ce-117">Per creare un URL di streaming HLS, aggiungere (format=m3u8-aapl) all'URL.</span><span class="sxs-lookup"><span data-stu-id="876ce-117">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="876ce-118">Per creare un URL di streaming MPEG DASH, aggiungere (format=mpd-time-csf) all'URL.</span><span class="sxs-lookup"><span data-stu-id="876ce-118">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="876ce-119">Un URL di firma di accesso condiviso ha il formato seguente.</span><span class="sxs-lookup"><span data-stu-id="876ce-119">A SAS URL has the following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="876ce-120">Per altre informazioni, vedere [Panoramica della distribuzione di contenuti](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="876ce-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="876ce-121">I localizzatori creati attraverso il portale prima del mese di marzo 2015 hanno una data di scadenza di due anni.</span><span class="sxs-lookup"><span data-stu-id="876ce-121">If you used the portal to create locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="876ce-122">Per aggiornare la data di scadenza di un localizzatore, è possibile usare le API [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) o [.NET](http://go.microsoft.com/fwlink/?LinkID=533259).</span><span class="sxs-lookup"><span data-stu-id="876ce-122">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="876ce-123">Si noti che quando si aggiorna la data di scadenza di un localizzatore di firma di accesso condiviso, l'URL viene modificato.</span><span class="sxs-lookup"><span data-stu-id="876ce-123">Note that when you update the expiration date of a SAS locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="876ce-124">Per usare il portale per la pubblicazione di un asset</span><span class="sxs-lookup"><span data-stu-id="876ce-124">To use the portal to publish an asset</span></span>
<span data-ttu-id="876ce-125">Per pubblicare un asset tramite il portale, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="876ce-125">To use the portal to publish an asset, do the following:</span></span>

1. <span data-ttu-id="876ce-126">Nel [portale di Azure ](https://portal.azure.com/) selezionare l'account Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="876ce-126">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="876ce-127">Selezionare **Impostazioni** > **Asset**.</span><span class="sxs-lookup"><span data-stu-id="876ce-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="876ce-128">Selezionare l'asset da pubblicare.</span><span class="sxs-lookup"><span data-stu-id="876ce-128">Select the asset that you want to publish.</span></span>
4. <span data-ttu-id="876ce-129">Fare clic sul pulsante **Pubblica** .</span><span class="sxs-lookup"><span data-stu-id="876ce-129">Click the **Publish** button.</span></span>
5. <span data-ttu-id="876ce-130">Selezionare il tipo di localizzatore.</span><span class="sxs-lookup"><span data-stu-id="876ce-130">Select the locator type.</span></span>
6. <span data-ttu-id="876ce-131">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="876ce-131">Press **Add**.</span></span>
   
    ![Pubblica](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="876ce-133">L'URL verrà aggiunto all'elenco di **URL pubblicati**.</span><span class="sxs-lookup"><span data-stu-id="876ce-133">The URL will be added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="876ce-134">Riprodurre contenuti dal portale</span><span class="sxs-lookup"><span data-stu-id="876ce-134">Play content from the portal</span></span>
<span data-ttu-id="876ce-135">Il portale di Azure fornisce un lettore di contenuti che può essere usato per testare il proprio video.</span><span class="sxs-lookup"><span data-stu-id="876ce-135">The Azure portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="876ce-136">Fare clic sul video richiesto e quindi sul pulsante **Riproduci** .</span><span class="sxs-lookup"><span data-stu-id="876ce-136">Click the desired video and then click the **Play** button.</span></span>

![Pubblica](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="876ce-138">Considerazioni applicabili:</span><span class="sxs-lookup"><span data-stu-id="876ce-138">Some considerations apply:</span></span>

* <span data-ttu-id="876ce-139">Verificare che il video sia stato pubblicato.</span><span class="sxs-lookup"><span data-stu-id="876ce-139">Make sure the video has been published.</span></span>
* <span data-ttu-id="876ce-140">**Media Player** esegue la riproduzione dall'endpoint di streaming predefinito.</span><span class="sxs-lookup"><span data-stu-id="876ce-140">This **Media player** plays from the default streaming endpoint.</span></span> <span data-ttu-id="876ce-141">Se si vuole eseguire la riproduzione da un endpoint di streaming diverso, fare clic per copiare l'URL e usare un altro lettore,</span><span class="sxs-lookup"><span data-stu-id="876ce-141">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span></span> <span data-ttu-id="876ce-142">ad esempio [Lettore di Servizi multimediali di Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="876ce-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="876ce-143">L'endpoint di streaming da cui si effettua lo streaming deve essere in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="876ce-143">The streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="876ce-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="876ce-144">Next steps</span></span>
<span data-ttu-id="876ce-145">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="876ce-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="876ce-146">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="876ce-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

