---
title: gli endpoint con hello portale di Azure di streaming aaaScale | Documenti Microsoft
description: "In questa esercitazione vengono illustrati i passaggi hello di scalabilità di endpoint di streaming con hello portale di Azure."
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
ms.openlocfilehash: e466edf9232558b9e270f54ee2849cd9b22ad121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="c3909-103">Ridimensionare l'endpoint di streaming con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c3909-103">Scale streaming endpoints with hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="c3909-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c3909-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="c3909-105">toocomplete questa esercitazione, è necessario un account di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3909-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="c3909-106">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3909-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="c3909-107">Gli endpoint di streaming **Premium** sono ideali per i carichi di lavoro avanzati, in quanto offrono una capacità di larghezza di banda dedicata e scalabile.</span><span class="sxs-lookup"><span data-stu-id="c3909-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="c3909-108">Per impostazione predefinita, i clienti con un endpoint di streaming **Premium** ottengono un'unità di streaming.</span><span class="sxs-lookup"><span data-stu-id="c3909-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="c3909-109">è possibile scalare aggiungendo SUs Hello endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="c3909-109">hello streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="c3909-110">Ogni SU fornisce applicazione toohello capacità di larghezza di banda aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="c3909-110">Each SU provides additional bandwidth capacity toohello application.</span></span> <span data-ttu-id="c3909-111">Per ulteriori informazioni sul flusso di tipi di endpoint e la configurazione della rete CDN, vedere hello [Panoramica Endpoint di Streaming](media-services-portal-manage-streaming-endpoints.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="c3909-111">For more information about streaming endpoint types and CDN configuration, see hello [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="c3909-112">Questo argomento viene illustrato come tooscale un endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="c3909-112">This topic shows how tooscale a streaming endpoint.</span></span>

<span data-ttu-id="c3909-113">Per informazioni sui prezzi, vedere [Dettagli prezzi di Servizi multimediali](http://go.microsoft.com/fwlink/?LinkId=275107).</span><span class="sxs-lookup"><span data-stu-id="c3909-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="c3909-114">Ridimensionare gli endpoint di streaming</span><span class="sxs-lookup"><span data-stu-id="c3909-114">Scale streaming endpoints</span></span>

<span data-ttu-id="c3909-115">numero di hello toochange di unità di streaming, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c3909-115">toochange hello number of streaming units, do hello following:</span></span>

1. <span data-ttu-id="c3909-116">In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c3909-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="c3909-117">In hello **impostazioni** selezionare **gli endpoint di Streaming**.</span><span class="sxs-lookup"><span data-stu-id="c3909-117">In hello **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="c3909-118">Fare clic sull'endpoint di streaming hello che si desidera tooscale.</span><span class="sxs-lookup"><span data-stu-id="c3909-118">Click on hello streaming endpoint that you want tooscale.</span></span> 

    [!NOTE] <span data-ttu-id="c3909-119">È possibile ridimensionare solo endpoint di streaming **Premium**.</span><span class="sxs-lookup"><span data-stu-id="c3909-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="c3909-120">Spostare hello dispositivo di scorrimento toospecify hello diverse unità di streaming.</span><span class="sxs-lookup"><span data-stu-id="c3909-120">Move hello slider toospecify hello number of streaming units.</span></span>

    ![endpoint di streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="c3909-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c3909-122">Next steps</span></span>
<span data-ttu-id="c3909-123">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="c3909-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c3909-124">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="c3909-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

