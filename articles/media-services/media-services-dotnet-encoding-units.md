---
title: "supporto aaaScale elaborazione mediante l'aggiunta di unità di codifica - Azure |  Documenti Microsoft"
description: "Informazioni su come unità di codifica tooadd toohow con .NET"
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
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a><span data-ttu-id="5e53a-103">Come tooscale codifica con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5e53a-103">How tooscale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e53a-104">Portale</span><span class="sxs-lookup"><span data-stu-id="5e53a-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="5e53a-105">.NET</span><span class="sxs-lookup"><span data-stu-id="5e53a-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="5e53a-106">REST</span><span class="sxs-lookup"><span data-stu-id="5e53a-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="5e53a-107">Java</span><span class="sxs-lookup"><span data-stu-id="5e53a-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="5e53a-108">PHP</span><span class="sxs-lookup"><span data-stu-id="5e53a-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="5e53a-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5e53a-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5e53a-110">Verificare che hello tooreview [Panoramica](media-services-scale-media-processing-overview.md) tooget argomento ulteriori informazioni sulla scalabilità supporti l'elaborazione di argomento.</span><span class="sxs-lookup"><span data-stu-id="5e53a-110">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="5e53a-111">hello toochange hello riservato hello tipo e il numero di unità mediante .NET SDK, di unità riservate di codifica seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e53a-111">toochange hello reserved unit type and hello number of encoding reserved units using .NET SDK, do hello following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="5e53a-112">Apertura di un ticket di supporto</span><span class="sxs-lookup"><span data-stu-id="5e53a-112">Opening a Support Ticket</span></span>
<span data-ttu-id="5e53a-113">Per impostazione predefinita, ogni account di servizi multimediali possono essere ridimensionati tooup too25 5 e codifica su richiesta unità riservate di Streaming.</span><span class="sxs-lookup"><span data-stu-id="5e53a-113">By default every Media Services account can scale tooup too25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="5e53a-114">È possibile richiedere l'applicazione di un limite superiore mediante l'apertura di un ticket di supporto.</span><span class="sxs-lookup"><span data-stu-id="5e53a-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="5e53a-115">Aprire un ticket di supporto</span><span class="sxs-lookup"><span data-stu-id="5e53a-115">Open a support ticket</span></span>
<span data-ttu-id="5e53a-116">hello tooopen un ticket di supporto seguenti:</span><span class="sxs-lookup"><span data-stu-id="5e53a-116">tooopen a support ticket do hello following:</span></span>

1. <span data-ttu-id="5e53a-117">Fare clic su [Ottieni supporto](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="5e53a-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="5e53a-118">Se non si è connessi, è necessario essere tooenter richieste le credenziali.</span><span class="sxs-lookup"><span data-stu-id="5e53a-118">If you are not logged in, you will be prompted tooenter your credentials.</span></span>
2. <span data-ttu-id="5e53a-119">Selezionare la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5e53a-119">Select your subscription.</span></span>
3. <span data-ttu-id="5e53a-120">Come tipo di supporto, selezionare "Tecnico".</span><span class="sxs-lookup"><span data-stu-id="5e53a-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="5e53a-121">Fare clic su "Create Ticket".</span><span class="sxs-lookup"><span data-stu-id="5e53a-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="5e53a-122">Selezionare "Servizi multimediali di Azure" nell'elenco di prodotti hello presentate nella pagina successiva di hello.</span><span class="sxs-lookup"><span data-stu-id="5e53a-122">Select "Azure Media Services" in hello product list presented on hello next page.</span></span>
6. <span data-ttu-id="5e53a-123">Selezionare un tipo di problema appropriato per la situazione specifica.</span><span class="sxs-lookup"><span data-stu-id="5e53a-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="5e53a-124">Fare clic su Continue.</span><span class="sxs-lookup"><span data-stu-id="5e53a-124">Click Continue.</span></span>
8. <span data-ttu-id="5e53a-125">Seguire le istruzioni nella pagina successiva e quindi immettere i dettagli relativi al problema.</span><span class="sxs-lookup"><span data-stu-id="5e53a-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="5e53a-126">Fare clic su Invia il ticket hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="5e53a-126">Click submit tooopen hello ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="5e53a-127">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="5e53a-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5e53a-128">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="5e53a-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

