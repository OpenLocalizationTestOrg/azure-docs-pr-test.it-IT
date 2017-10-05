---
title: "Ridimensionare l'elaborazione multimediale aggiungendo unità di codifica - Azure | Documentazione Microsoft"
description: "Informazioni su come aggiungere unità di codifica mediante .NET"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: 72a8729d22a9e76c8076d7a3347619a2163e4f09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-scale-encoding-with-net-sdk"></a><span data-ttu-id="b0075-103">Come scalare la codifica con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b0075-103">How to scale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0075-104">Portale</span><span class="sxs-lookup"><span data-stu-id="b0075-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="b0075-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b0075-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="b0075-106">REST</span><span class="sxs-lookup"><span data-stu-id="b0075-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="b0075-107">Java</span><span class="sxs-lookup"><span data-stu-id="b0075-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="b0075-108">PHP</span><span class="sxs-lookup"><span data-stu-id="b0075-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="b0075-109">Overview</span><span class="sxs-lookup"><span data-stu-id="b0075-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b0075-110">Per altre informazioni sul ridimensionamento dell'elaborazione multimediale, vedere questo argomento di [panoramica](media-services-scale-media-processing-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="b0075-110">Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="b0075-111">Per cambiare il tipo di unità riservata e il numero di unità riservate di codifica mediante l'SDK per .NET, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b0075-111">To change the reserved unit type and the number of encoding reserved units using .NET SDK, do the following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds to S1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="b0075-112">Apertura di un ticket di supporto</span><span class="sxs-lookup"><span data-stu-id="b0075-112">Opening a Support Ticket</span></span>
<span data-ttu-id="b0075-113">Per impostazione predefinita, ogni account di Media Services può includere fino a 25 unità di codifica riservate e cinque unità riservate di streaming on demand.</span><span class="sxs-lookup"><span data-stu-id="b0075-113">By default every Media Services account can scale to up to 25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="b0075-114">È possibile richiedere l'applicazione di un limite superiore mediante l'apertura di un ticket di supporto.</span><span class="sxs-lookup"><span data-stu-id="b0075-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="b0075-115">Aprire un ticket di supporto</span><span class="sxs-lookup"><span data-stu-id="b0075-115">Open a support ticket</span></span>
<span data-ttu-id="b0075-116">Per aprire un ticket di supporto, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b0075-116">To open a support ticket do the following:</span></span>

1. <span data-ttu-id="b0075-117">Fare clic su [Ottieni supporto](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="b0075-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="b0075-118">Se non si è ancora connessi, verrà richiesto di immettere le credenziali.</span><span class="sxs-lookup"><span data-stu-id="b0075-118">If you are not logged in, you will be prompted to enter your credentials.</span></span>
2. <span data-ttu-id="b0075-119">Selezionare la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b0075-119">Select your subscription.</span></span>
3. <span data-ttu-id="b0075-120">Come tipo di supporto, selezionare "Tecnico".</span><span class="sxs-lookup"><span data-stu-id="b0075-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="b0075-121">Fare clic su "Create Ticket".</span><span class="sxs-lookup"><span data-stu-id="b0075-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="b0075-122">Selezionare "Servizi multimediali di Azure" dall'elenco dei prodotti visualizzato nella pagina successiva.</span><span class="sxs-lookup"><span data-stu-id="b0075-122">Select "Azure Media Services" in the product list presented on the next page.</span></span>
6. <span data-ttu-id="b0075-123">Selezionare un tipo di problema appropriato per la situazione specifica.</span><span class="sxs-lookup"><span data-stu-id="b0075-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="b0075-124">Fare clic su Continue.</span><span class="sxs-lookup"><span data-stu-id="b0075-124">Click Continue.</span></span>
8. <span data-ttu-id="b0075-125">Seguire le istruzioni nella pagina successiva e quindi immettere i dettagli relativi al problema.</span><span class="sxs-lookup"><span data-stu-id="b0075-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="b0075-126">Fare clic su Invia per aprire il ticket.</span><span class="sxs-lookup"><span data-stu-id="b0075-126">Click submit to open the ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="b0075-127">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="b0075-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b0075-128">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="b0075-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

