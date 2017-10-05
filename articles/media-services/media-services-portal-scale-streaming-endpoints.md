---
title: Ridimensionare gli endpoint di streaming con il portale di Azure | Microsoft Docs
description: Questa esercitazione descrive i passaggi per ridimensionare gli endpoint di streaming mediante il portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 4bb891371e3fc802fa667688a88878db18e32422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="scale-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="77c84-103">Ridimensionare gli endpoint di streaming con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="77c84-103">Scale streaming endpoints with the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="77c84-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="77c84-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="77c84-105">Per completare l'esercitazione, è necessario un account Azure.</span><span class="sxs-lookup"><span data-stu-id="77c84-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="77c84-106">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77c84-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="77c84-107">Gli endpoint di streaming **Premium** sono ideali per i carichi di lavoro avanzati, in quanto offrono una capacità di larghezza di banda dedicata e scalabile.</span><span class="sxs-lookup"><span data-stu-id="77c84-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="77c84-108">Per impostazione predefinita, i clienti con un endpoint di streaming **Premium** ottengono un'unità di streaming.</span><span class="sxs-lookup"><span data-stu-id="77c84-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="77c84-109">L'endpoint di streaming può essere ridimensionato aggiungendo unità di streaming.</span><span class="sxs-lookup"><span data-stu-id="77c84-109">The streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="77c84-110">Ogni unità di streaming fornisce all'applicazione capacità di larghezza di banda aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="77c84-110">Each SU provides additional bandwidth capacity to the application.</span></span> <span data-ttu-id="77c84-111">Per altre informazioni sui tipi di endpoint di streaming e la configurazione della rete CDN, vedere l'argomento [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) (Panoramica sugli endpoint di streaming).</span><span class="sxs-lookup"><span data-stu-id="77c84-111">For more information about streaming endpoint types and CDN configuration, see the [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="77c84-112">Questo argomento illustra come ridimensionare un endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="77c84-112">This topic shows how to scale a streaming endpoint.</span></span>

<span data-ttu-id="77c84-113">Per informazioni sui prezzi, vedere [Dettagli prezzi di Servizi multimediali](http://go.microsoft.com/fwlink/?LinkId=275107).</span><span class="sxs-lookup"><span data-stu-id="77c84-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="77c84-114">Ridimensionare gli endpoint di streaming</span><span class="sxs-lookup"><span data-stu-id="77c84-114">Scale streaming endpoints</span></span>

<span data-ttu-id="77c84-115">Per modificare il numero di unità di streaming, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="77c84-115">To change the number of streaming units, do the following:</span></span>

1. <span data-ttu-id="77c84-116">Nel [portale di Azure ](https://portal.azure.com/) selezionare l'account Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="77c84-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="77c84-117">Nella finestra **Impostazioni** selezionare **Endpoint di streaming**.</span><span class="sxs-lookup"><span data-stu-id="77c84-117">In the **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="77c84-118">Fare clic sull'endpoint di streaming da ridimensionare.</span><span class="sxs-lookup"><span data-stu-id="77c84-118">Click on the streaming endpoint that you want to scale.</span></span> 

    [!NOTE] <span data-ttu-id="77c84-119">È possibile ridimensionare solo endpoint di streaming **Premium**.</span><span class="sxs-lookup"><span data-stu-id="77c84-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="77c84-120">Spostare il dispositivo di scorrimento per specificare il numero di unità di streaming.</span><span class="sxs-lookup"><span data-stu-id="77c84-120">Move the slider to specify the number of streaming units.</span></span>

    ![endpoint di streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="77c84-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77c84-122">Next steps</span></span>
<span data-ttu-id="77c84-123">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="77c84-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="77c84-124">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="77c84-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

