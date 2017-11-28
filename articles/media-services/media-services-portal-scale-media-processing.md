---
title: supporto aaaScale elaborazione utilizzando hello portale di Azure | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello di scala media elaborazione utilizzando hello portale di Azure.
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
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a><span data-ttu-id="cb248-103">Tipo di unità di modifica hello riservato</span><span class="sxs-lookup"><span data-stu-id="cb248-103">Change hello reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb248-104">.NET</span><span class="sxs-lookup"><span data-stu-id="cb248-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="cb248-105">Portale</span><span class="sxs-lookup"><span data-stu-id="cb248-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="cb248-106">REST</span><span class="sxs-lookup"><span data-stu-id="cb248-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="cb248-107">Java</span><span class="sxs-lookup"><span data-stu-id="cb248-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="cb248-108">PHP</span><span class="sxs-lookup"><span data-stu-id="cb248-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="cb248-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="cb248-109">Overview</span></span>

<span data-ttu-id="cb248-110">Un account di servizi multimediali è associato a un tipo di unità riservate, che determina la velocità di hello con cui vengono elaborati i file multimediali l'elaborazione delle attività.</span><span class="sxs-lookup"><span data-stu-id="cb248-110">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="cb248-111">È possibile scegliere tra segue hello i tipi di unità riservata: **S1**, **S2**, o **S3**.</span><span class="sxs-lookup"><span data-stu-id="cb248-111">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="cb248-112">Ad esempio, hello stesso processo di codifica viene eseguito più velocemente quando si utilizza hello **S2** toohello di confronto del tipo di unità riservata **S1** tipo.</span><span class="sxs-lookup"><span data-stu-id="cb248-112">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span>

<span data-ttu-id="cb248-113">Inoltre toospecifying hello riservati di tipo di unità, è possibile specificare l'account con tooprovision **unità riservate** (RUs).</span><span class="sxs-lookup"><span data-stu-id="cb248-113">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="cb248-114">numero di Hello di provisioning RUs determina il numero di hello delle attività multimediali che possono essere elaborate contemporaneamente in un determinato account.</span><span class="sxs-lookup"><span data-stu-id="cb248-114">hello number of provisioned RUs determines hello number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="cb248-115">UR di lavoro per la parallelizzazione di tutta l'elaborazione di supporti di memorizzazione, tra cui l'indicizzazione di processi tramite Azure Media Indexer.</span><span class="sxs-lookup"><span data-stu-id="cb248-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="cb248-116">Tuttavia, a differenza della codifica, l'indicizzazione di processi non viene elaborata più velocemente con unità riservate più veloci.</span><span class="sxs-lookup"><span data-stu-id="cb248-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cb248-117">Verificare che hello tooreview [Panoramica](media-services-scale-media-processing-overview.md) tooget argomento ulteriori informazioni sulla scalabilità supporti l'elaborazione di argomento.</span><span class="sxs-lookup"><span data-stu-id="cb248-117">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="cb248-118">Ridimensionare l'elaborazione di contenuti multimediali</span><span class="sxs-lookup"><span data-stu-id="cb248-118">Scale media processing</span></span>
<span data-ttu-id="cb248-119">toochange hello riservato unità hello tipo e il numero di unità riservate, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb248-119">toochange hello reserved unit type and hello number of reserved units, do hello following:</span></span>

1. <span data-ttu-id="cb248-120">In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb248-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="cb248-121">In hello **impostazioni** selezionare **supporto di unità riservate**.</span><span class="sxs-lookup"><span data-stu-id="cb248-121">In hello **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="cb248-122">numero di hello toochange di unità riservate per hello selezionato il tipo di unità riservata, utilizzare hello **Media servita unità** dispositivo di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="cb248-122">toochange hello number of reserved units for hello selected reserved unit type, use hello **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="cb248-123">hello toochange **il tipo di unità riservate**, premere S1, S2 o S3.</span><span class="sxs-lookup"><span data-stu-id="cb248-123">toochange hello **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![Pagina relativa ai processori](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="cb248-125">Hello premere salvare toosave pulsante le modifiche.</span><span class="sxs-lookup"><span data-stu-id="cb248-125">Press hello SAVE button toosave your changes.</span></span>
   
    <span data-ttu-id="cb248-126">Quando si preme di salvataggio, vengono allocate nuove unità riservate di Hello.</span><span class="sxs-lookup"><span data-stu-id="cb248-126">hello new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb248-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cb248-127">Next steps</span></span>
<span data-ttu-id="cb248-128">Analizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="cb248-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cb248-129">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="cb248-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

