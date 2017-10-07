---
title: "velocità Gestisci aaa e la concorrenza della codifica con servizi multimediali di Azure | Documenti Microsoft"
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
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="83f25-103">Gestire la velocità e la concorrenza della codifica</span><span class="sxs-lookup"><span data-stu-id="83f25-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="83f25-104">Questo articolo illustra brevemente la procedura per gestire la velocità e la concorrenza delle attività o dei processi di codifica.</span><span class="sxs-lookup"><span data-stu-id="83f25-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="83f25-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="83f25-105">Overview</span></span>

<span data-ttu-id="83f25-106">In servizi multimediali un **il tipo di unità riservate** determina hello velocità con cui vengono elaborati i file multimediali l'elaborazione delle attività.</span><span class="sxs-lookup"><span data-stu-id="83f25-106">In Media Services, a **Reserved Unit Type** determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="83f25-107">È possibile scegliere tra segue hello i tipi di unità riservata: **S1**, **S2**, o **S3**.</span><span class="sxs-lookup"><span data-stu-id="83f25-107">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="83f25-108">Ad esempio, hello stesso processo di codifica viene eseguito più velocemente quando si utilizza hello **S2** toohello di confronto del tipo di unità riservata **S1** tipo.</span><span class="sxs-lookup"><span data-stu-id="83f25-108">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span> <span data-ttu-id="83f25-109">Hello [scalabilità unità di codifica](media-services-scale-media-processing-overview.md) argomento viene illustrata una tabella che consente di decidere quando si sceglie tra diverse velocità di codifica.</span><span class="sxs-lookup"><span data-stu-id="83f25-109">hello [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="83f25-110">Inoltre toospecifying hello riservati di tipo di unità, è possibile specificare l'account con tooprovision **unità riservate**.</span><span class="sxs-lookup"><span data-stu-id="83f25-110">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units**.</span></span> <span data-ttu-id="83f25-111">numero di Hello di unità riservate sottoposte a provisioning determina il numero di hello delle attività multimediali che possono essere elaborate contemporaneamente in un determinato account.</span><span class="sxs-lookup"><span data-stu-id="83f25-111">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="83f25-112">Ad esempio, se l'account dispone di 5 unità riservate, quindi verrà eseguita contemporaneamente a condizione attività cinque multimediali sono pari al numero di attività toobe elaborati.</span><span class="sxs-lookup"><span data-stu-id="83f25-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks toobe processed.</span></span> <span data-ttu-id="83f25-113">le attività rimanenti Hello rimarranno in attesa nella coda di hello e saranno prelevate per l'elaborazione in sequenza al termine di un'attività in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="83f25-113">hello remaining tasks will wait in hello queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="83f25-114">Se per un account non sono state fornite unità riservate, le attività verranno prelevate in sequenza.</span><span class="sxs-lookup"><span data-stu-id="83f25-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="83f25-115">In questo caso, hello tempo di attesa tra un completamento di attività e hello avvio della successiva dipenderà disponibilità hello delle risorse di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="83f25-115">In this case, hello wait time between one task finishing and hello next one starting will depend on hello availability of resources in hello system.</span></span>

<span data-ttu-id="83f25-116">Per informazioni dettagliate ed esempi che mostrano come unità di codifica tooscale, vedere [questo](media-services-scale-media-processing-overview.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="83f25-116">For detailed information and examples that show how tooscale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="83f25-117">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="83f25-117">Next step</span></span>

[<span data-ttu-id="83f25-118">Ridimensionare le unità di codifica</span><span class="sxs-lookup"><span data-stu-id="83f25-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="83f25-119">Percorsi di apprendimento di Media Services</span><span class="sxs-lookup"><span data-stu-id="83f25-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="83f25-120">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="83f25-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

