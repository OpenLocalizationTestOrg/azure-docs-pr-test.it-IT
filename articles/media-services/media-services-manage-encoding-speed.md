---
title: "Gestire la velocità e la concorrenza della codifica con Servizi multimediali di Azure | Microsoft Docs"
description: "Questo articolo illustra brevemente la procedura per gestire la velocità e la concorrenza delle attività o dei processi di codifica con Servizi multimediali di Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 0463904fd9bf1138587d0d214e572ddd38cc2184
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="4973c-103">Gestire la velocità e la concorrenza della codifica</span><span class="sxs-lookup"><span data-stu-id="4973c-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="4973c-104">Questo articolo illustra brevemente la procedura per gestire la velocità e la concorrenza delle attività o dei processi di codifica.</span><span class="sxs-lookup"><span data-stu-id="4973c-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="4973c-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="4973c-105">Overview</span></span>

<span data-ttu-id="4973c-106">Nei Servizi multimediali, un **tipo di unità riservata** determina la velocità di elaborazione delle attività multimediali.</span><span class="sxs-lookup"><span data-stu-id="4973c-106">In Media Services, a **Reserved Unit Type** determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="4973c-107">È possibile scegliere uno dei seguenti tipi di unità riservata: **S1**, **S2** o **S3**.</span><span class="sxs-lookup"><span data-stu-id="4973c-107">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="4973c-108">Lo stesso processo di codifica viene eseguito più velocemente quando si usa ad esempio il tipo di unità riservata **S2** rispetto al tipo **S1**.</span><span class="sxs-lookup"><span data-stu-id="4973c-108">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span> <span data-ttu-id="4973c-109">L'argomento sulle [unità di codifica della scalabilità](media-services-scale-media-processing-overview.md) mostra una tabella che consente di scegliere tra diverse velocità di codifica.</span><span class="sxs-lookup"><span data-stu-id="4973c-109">The [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="4973c-110">Oltre al tipo di unità riservata, è possibile specificare il provisioning dell'account con le **unità riservate**.</span><span class="sxs-lookup"><span data-stu-id="4973c-110">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units**.</span></span> <span data-ttu-id="4973c-111">Il numero delle unità riservate sottoposte a provisioning determina il numero di attività multimediali che possono essere elaborate contemporaneamente in un determinato account.</span><span class="sxs-lookup"><span data-stu-id="4973c-111">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="4973c-112">Se, ad esempio, il proprio account dispone di cinque unità riservate, è possibile eseguire simultaneamente cinque attività multimediali, purché siano presenti attività da elaborare.</span><span class="sxs-lookup"><span data-stu-id="4973c-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks to be processed.</span></span> <span data-ttu-id="4973c-113">Le attività rimanenti verranno messe in coda e prelevate in sequenza per l'elaborazione quando un'attività in esecuzione viene completata.</span><span class="sxs-lookup"><span data-stu-id="4973c-113">The remaining tasks will wait in the queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="4973c-114">Se per un account non sono state fornite unità riservate, le attività verranno prelevate in sequenza.</span><span class="sxs-lookup"><span data-stu-id="4973c-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="4973c-115">In questo caso, il tempo di attesa tra il completamento di un'attività e l'avvio di quella successiva dipende dalle risorse disponibili nel sistema.</span><span class="sxs-lookup"><span data-stu-id="4973c-115">In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.</span></span>

<span data-ttu-id="4973c-116">Per informazioni dettagliate ed esempi che illustrano come ridimensionare le unità di codifica, vedere [questo](media-services-scale-media-processing-overview.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="4973c-116">For detailed information and examples that show how to scale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="4973c-117">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="4973c-117">Next step</span></span>

[<span data-ttu-id="4973c-118">Ridimensionare le unità di codifica</span><span class="sxs-lookup"><span data-stu-id="4973c-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="4973c-119">Percorsi di apprendimento di Media Services</span><span class="sxs-lookup"><span data-stu-id="4973c-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4973c-120">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="4973c-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

