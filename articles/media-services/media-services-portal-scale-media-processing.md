---
title: Ridimensionare l'elaborazione di contenuti mediante il portale di Azure | Microsoft Docs
description: Questa esercitazione descrive i passaggi per ridimensionare l'elaborazione multimediale mediante il portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 46ca29d3e66701f2abcb185791089e94761984e8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="change-the-reserved-unit-type"></a><span data-ttu-id="48207-103">Modificare il tipo di unità riservata</span><span class="sxs-lookup"><span data-stu-id="48207-103">Change the reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="48207-104">.NET</span><span class="sxs-lookup"><span data-stu-id="48207-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="48207-105">Portale</span><span class="sxs-lookup"><span data-stu-id="48207-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="48207-106">REST</span><span class="sxs-lookup"><span data-stu-id="48207-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="48207-107">Java</span><span class="sxs-lookup"><span data-stu-id="48207-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="48207-108">PHP</span><span class="sxs-lookup"><span data-stu-id="48207-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="48207-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="48207-109">Overview</span></span>

<span data-ttu-id="48207-110">Un account di Servizi multimediali è associato a un tipo di unità riservata che determina la velocità dei processi di elaborazione dei multimedia.</span><span class="sxs-lookup"><span data-stu-id="48207-110">A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="48207-111">È possibile scegliere uno dei seguenti tipi di unità riservata: **S1**, **S2** o **S3**.</span><span class="sxs-lookup"><span data-stu-id="48207-111">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="48207-112">Lo stesso processo di codifica viene eseguito più velocemente quando si usa ad esempio il tipo di unità riservata **S2** rispetto al tipo **S1**.</span><span class="sxs-lookup"><span data-stu-id="48207-112">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span>

<span data-ttu-id="48207-113">Oltre al tipo di unità riservata, è possibile specificare il provisioning dell'account con **Unità riservate** (UR).</span><span class="sxs-lookup"><span data-stu-id="48207-113">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="48207-114">Il numero delle UR sottoposte a provisioning determina il numero di attività multimediali che possono essere elaborate contemporaneamente in un determinato account.</span><span class="sxs-lookup"><span data-stu-id="48207-114">The number of provisioned RUs determines the number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="48207-115">UR di lavoro per la parallelizzazione di tutta l'elaborazione di supporti di memorizzazione, tra cui l'indicizzazione di processi tramite Azure Media Indexer.</span><span class="sxs-lookup"><span data-stu-id="48207-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="48207-116">Tuttavia, a differenza della codifica, l'indicizzazione di processi non viene elaborata più velocemente con unità riservate più veloci.</span><span class="sxs-lookup"><span data-stu-id="48207-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48207-117">Per altre informazioni sul ridimensionamento dell'elaborazione multimediale, vedere questo argomento di [panoramica](media-services-scale-media-processing-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="48207-117">Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="48207-118">Ridimensionare l'elaborazione di contenuti multimediali</span><span class="sxs-lookup"><span data-stu-id="48207-118">Scale media processing</span></span>
<span data-ttu-id="48207-119">Per modificare il tipo di unità riservata e il numero di unità riservate, effettuare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="48207-119">To change the reserved unit type and the number of reserved units, do the following:</span></span>

1. <span data-ttu-id="48207-120">Nel [portale di Azure ](https://portal.azure.com/) selezionare l'account Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="48207-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="48207-121">Nella finestra **Impostazioni** selezionare **Media Reserved Unit**.</span><span class="sxs-lookup"><span data-stu-id="48207-121">In the **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="48207-122">Per cambiare il numero di unità riservate per il tipo selezionato, usare il dispositivo di scorrimento **Media Served Units** .</span><span class="sxs-lookup"><span data-stu-id="48207-122">To change the number of reserved units for the selected reserved unit type, use the **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="48207-123">Per cambiare il **TIPO DI UNITÀ RISERVATA**, scegliere S1, S2 o S3.</span><span class="sxs-lookup"><span data-stu-id="48207-123">To change the **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![Pagina relativa ai processori](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="48207-125">Fare clic sul pulsante SAVE per salvare le modifiche apportate.</span><span class="sxs-lookup"><span data-stu-id="48207-125">Press the SAVE button to save your changes.</span></span>
   
    <span data-ttu-id="48207-126">Le nuove unità riservate vengono allocate quando si fa clic su SALVA.</span><span class="sxs-lookup"><span data-stu-id="48207-126">The new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48207-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="48207-127">Next steps</span></span>
<span data-ttu-id="48207-128">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="48207-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="48207-129">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="48207-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

