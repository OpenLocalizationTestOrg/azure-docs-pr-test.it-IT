---
title: trigger di ricorrenza aaaAdd hello in App per la logica | Documenti Microsoft
description: Panoramica del trigger di ricorrenza hello e come toouse con un'app per la logica di Azure.
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a><span data-ttu-id="fd6b3-103">Introduzione a trigger ricorrenza hello</span><span class="sxs-lookup"><span data-stu-id="fd6b3-103">Get started with hello recurrence trigger</span></span>
<span data-ttu-id="fd6b3-104">Tramite il trigger di ricorrenza hello, è possibile creare potenti flussi di lavoro nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="fd6b3-104">By using hello recurrence trigger, you can create powerful workflows in hello cloud.</span></span>

<span data-ttu-id="fd6b3-105">Ad esempio, è possibile:</span><span class="sxs-lookup"><span data-stu-id="fd6b3-105">For example, you can:</span></span>

* <span data-ttu-id="fd6b3-106">Pianificare un toorun del flusso di lavoro una stored procedure SQL ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="fd6b3-106">Schedule a workflow toorun a SQL stored procedure every day.</span></span>
* <span data-ttu-id="fd6b3-107">Un riepilogo di tutti i TWEET all'interno di hello ultima settimana su un determinato hashtag di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="fd6b3-107">Email a summary of all tweets within hello last week about a certain hashtag.</span></span>

<span data-ttu-id="fd6b3-108">tooget avviato tramite trigger ricorrenza hello in un'app di logica, vedere [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="fd6b3-108">tooget started using hello recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="fd6b3-109">Usare un trigger di ricorrenza</span><span class="sxs-lookup"><span data-stu-id="fd6b3-109">Use a recurrence trigger</span></span>
<span data-ttu-id="fd6b3-110">Un trigger è un evento che può essere utilizzato toostart hello flusso di lavoro che è definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="fd6b3-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="fd6b3-111">[Altre informazioni sui trigger](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fd6b3-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="fd6b3-112">Di seguito è riportata una sequenza di esempio di come tooset di una ricorrenza attivare in un'app di logica:</span><span class="sxs-lookup"><span data-stu-id="fd6b3-112">Here’s an example sequence of how tooset up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="fd6b3-113">Aggiungere hello **ricorrenza** trigger come primo passaggio di hello in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="fd6b3-113">Add hello **Recurrence** trigger as hello first step in a logic app.</span></span>
2. <span data-ttu-id="fd6b3-114">Specificare i parametri di hello per l'intervallo di ricorrenza hello.</span><span class="sxs-lookup"><span data-stu-id="fd6b3-114">Fill in hello parameters for hello recurrence interval.</span></span>

<span data-ttu-id="fd6b3-115">Hello logica app verrà avviata un'esecuzione dopo ogni intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="fd6b3-115">hello logic app now starts a run after each interval of time.</span></span>

![Trigger HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="fd6b3-117">Dettagli del trigger</span><span class="sxs-lookup"><span data-stu-id="fd6b3-117">Trigger details</span></span>
<span data-ttu-id="fd6b3-118">i trigger di ricorrenza Hello è hello seguenti proprietà che è possibile configurare.</span><span class="sxs-lookup"><span data-stu-id="fd6b3-118">hello recurrence trigger has hello following properties that you can configure.</span></span>

<span data-ttu-id="fd6b3-119">Attiva un'app per la logica dopo un intervallo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="fd6b3-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="fd6b3-120">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="fd6b3-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="fd6b3-121">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="fd6b3-121">Display name</span></span> | <span data-ttu-id="fd6b3-122">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="fd6b3-122">Property name</span></span> | <span data-ttu-id="fd6b3-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fd6b3-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fd6b3-124">Frequenza*</span><span class="sxs-lookup"><span data-stu-id="fd6b3-124">Frequency*</span></span> |<span data-ttu-id="fd6b3-125">frequency</span><span class="sxs-lookup"><span data-stu-id="fd6b3-125">frequency</span></span> |<span data-ttu-id="fd6b3-126">unità di Hello di tempo: `Second`, `Minute`, `Hour`, `Day`, o `Year`.</span><span class="sxs-lookup"><span data-stu-id="fd6b3-126">hello unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="fd6b3-127">Intervallo*</span><span class="sxs-lookup"><span data-stu-id="fd6b3-127">Interval*</span></span> |<span data-ttu-id="fd6b3-128">interval</span><span class="sxs-lookup"><span data-stu-id="fd6b3-128">interval</span></span> |<span data-ttu-id="fd6b3-129">intervallo di Hello di hello dato frequenza ricorrenza hello.</span><span class="sxs-lookup"><span data-stu-id="fd6b3-129">hello interval of hello given frequency for hello recurrence.</span></span> |
| <span data-ttu-id="fd6b3-130">Fuso orario</span><span class="sxs-lookup"><span data-stu-id="fd6b3-130">Time Zone</span></span> |<span data-ttu-id="fd6b3-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="fd6b3-131">timeZone</span></span> |<span data-ttu-id="fd6b3-132">Se viene fornito un valore startTime senza una differenza dall'ora UTC, verrà usato tale valore timeZone.</span><span class="sxs-lookup"><span data-stu-id="fd6b3-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="fd6b3-133">Ora di inizio</span><span class="sxs-lookup"><span data-stu-id="fd6b3-133">Start time</span></span> |<span data-ttu-id="fd6b3-134">startTime</span><span class="sxs-lookup"><span data-stu-id="fd6b3-134">startTime</span></span> |<span data-ttu-id="fd6b3-135">ora di inizio Hello in [formato ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="fd6b3-135">hello start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="fd6b3-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd6b3-136">Next steps</span></span>
<span data-ttu-id="fd6b3-137">A questo punto, provare a piattaforma hello e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="fd6b3-137">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="fd6b3-138">È possibile esplorare altri connettori disponibile in App per la logica di hello esaminando il nostro [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="fd6b3-138">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

