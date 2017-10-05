---
title: Aggiungere il trigger di ricorrenza nelle app per la logica | Documentazione Microsoft
description: Panoramica dei trigger di ricorrenza e di come usarli con un'app per la logica di Azure.
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
ms.openlocfilehash: fe558958c316c8dba42163e277ae01451f712e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-recurrence-trigger"></a><span data-ttu-id="9981c-103">Introduzione al trigger di ricorrenza</span><span class="sxs-lookup"><span data-stu-id="9981c-103">Get started with the recurrence trigger</span></span>
<span data-ttu-id="9981c-104">Usando il trigger di ricorrenza è possibile creare potenti flussi di lavoro nel cloud.</span><span class="sxs-lookup"><span data-stu-id="9981c-104">By using the recurrence trigger, you can create powerful workflows in the cloud.</span></span>

<span data-ttu-id="9981c-105">Ad esempio, è possibile:</span><span class="sxs-lookup"><span data-stu-id="9981c-105">For example, you can:</span></span>

* <span data-ttu-id="9981c-106">Pianificare un flusso di lavoro per eseguire una stored procedure SQL ogni giorno.</span><span class="sxs-lookup"><span data-stu-id="9981c-106">Schedule a workflow to run a SQL stored procedure every day.</span></span>
* <span data-ttu-id="9981c-107">Inviare un messaggio di posta elettronica con il riepilogo di tutti i tweet dell'ultima settimana riguardanti un determinato hashtag.</span><span class="sxs-lookup"><span data-stu-id="9981c-107">Email a summary of all tweets within the last week about a certain hashtag.</span></span>

<span data-ttu-id="9981c-108">Per informazioni su come iniziare a usare un trigger di ricorrenza in un'app per la logica, vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9981c-108">To get started using the recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="9981c-109">Usare un trigger di ricorrenza</span><span class="sxs-lookup"><span data-stu-id="9981c-109">Use a recurrence trigger</span></span>
<span data-ttu-id="9981c-110">Un trigger è un evento che può essere usato per avviare il flusso di lavoro definito in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="9981c-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="9981c-111">[Altre informazioni sui trigger](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9981c-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="9981c-112">Ecco una sequenza di esempio di come configurare un trigger di ricorrenza in un'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="9981c-112">Here’s an example sequence of how to set up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="9981c-113">Aggiungere il trigger di **ricorrenza** come primo passaggio di un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="9981c-113">Add the **Recurrence** trigger as the first step in a logic app.</span></span>
2. <span data-ttu-id="9981c-114">Specificare i parametri per l'intervallo di ricorrenza.</span><span class="sxs-lookup"><span data-stu-id="9981c-114">Fill in the parameters for the recurrence interval.</span></span>

<span data-ttu-id="9981c-115">L'app per la logica avvia ora un'esecuzione dopo ogni intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="9981c-115">The logic app now starts a run after each interval of time.</span></span>

![Trigger HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="9981c-117">Dettagli del trigger</span><span class="sxs-lookup"><span data-stu-id="9981c-117">Trigger details</span></span>
<span data-ttu-id="9981c-118">Il trigger di ricorrenza ha le proprietà seguenti che è possibile configurare.</span><span class="sxs-lookup"><span data-stu-id="9981c-118">The recurrence trigger has the following properties that you can configure.</span></span>

<span data-ttu-id="9981c-119">Attiva un'app per la logica dopo un intervallo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="9981c-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="9981c-120">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="9981c-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="9981c-121">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="9981c-121">Display name</span></span> | <span data-ttu-id="9981c-122">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="9981c-122">Property name</span></span> | <span data-ttu-id="9981c-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9981c-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9981c-124">Frequenza*</span><span class="sxs-lookup"><span data-stu-id="9981c-124">Frequency*</span></span> |<span data-ttu-id="9981c-125">frequency</span><span class="sxs-lookup"><span data-stu-id="9981c-125">frequency</span></span> |<span data-ttu-id="9981c-126">L'unità di tempo: `Second`, `Minute`, `Hour`, `Day` o `Year`.</span><span class="sxs-lookup"><span data-stu-id="9981c-126">The unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="9981c-127">Intervallo*</span><span class="sxs-lookup"><span data-stu-id="9981c-127">Interval*</span></span> |<span data-ttu-id="9981c-128">interval</span><span class="sxs-lookup"><span data-stu-id="9981c-128">interval</span></span> |<span data-ttu-id="9981c-129">Intervallo della frequenza specificata per la ricorrenza.</span><span class="sxs-lookup"><span data-stu-id="9981c-129">The interval of the given frequency for the recurrence.</span></span> |
| <span data-ttu-id="9981c-130">Fuso orario</span><span class="sxs-lookup"><span data-stu-id="9981c-130">Time Zone</span></span> |<span data-ttu-id="9981c-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="9981c-131">timeZone</span></span> |<span data-ttu-id="9981c-132">Se viene fornito un valore startTime senza una differenza dall'ora UTC, verrà usato tale valore timeZone.</span><span class="sxs-lookup"><span data-stu-id="9981c-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="9981c-133">Ora di inizio</span><span class="sxs-lookup"><span data-stu-id="9981c-133">Start time</span></span> |<span data-ttu-id="9981c-134">startTime</span><span class="sxs-lookup"><span data-stu-id="9981c-134">startTime</span></span> |<span data-ttu-id="9981c-135">Ora di inizio nel [formato ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="9981c-135">The start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="9981c-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9981c-136">Next steps</span></span>
<span data-ttu-id="9981c-137">Provare ora a usare la piattaforma e [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9981c-137">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="9981c-138">È possibile esplorare gli altri connettori disponibili nelle app per la logica esaminando l' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="9981c-138">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

