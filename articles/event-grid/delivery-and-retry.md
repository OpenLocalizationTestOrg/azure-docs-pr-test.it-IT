---
title: Recapito di Griglia di eventi di Azure e nuovi tentativi
description: Viene descritto in che modo Griglia di eventi di Azure recapita gli eventi e come gestisce i messaggi non recapitati.
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: e0f8afdfd84ea3c0c061459c27da285f6ae8957e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="933cf-103">Recapito di messaggi di Griglia di eventi e nuovi tentativi</span><span class="sxs-lookup"><span data-stu-id="933cf-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="933cf-104">Questo articolo descrive in che modo Griglia di eventi di Azure gestisce gli eventi quando il recapito non viene confermato.</span><span class="sxs-lookup"><span data-stu-id="933cf-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="933cf-105">Griglia di eventi fornisce il recapito durevole.</span><span class="sxs-lookup"><span data-stu-id="933cf-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="933cf-106">Ogni messaggio viene recapitato almeno una volta per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="933cf-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="933cf-107">Gli eventi vengono inviati immediatamente al webhook registrato di ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="933cf-107">Events are sent to the registered webhook of each subscription immediately.</span></span> <span data-ttu-id="933cf-108">Se un webhook non conferma la ricezione di un evento entro 60 secondi dal primo tentativo di recapito, Griglia di eventi esegue un nuovo tentativo di recapito dell'evento.</span><span class="sxs-lookup"><span data-stu-id="933cf-108">If a webhook does not acknowledge receipt of an event within 60 seconds of the first delivery attempt, Event Grid retries delivery of the event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="933cf-109">Stato di recapito del messaggio</span><span class="sxs-lookup"><span data-stu-id="933cf-109">Message delivery status</span></span>

<span data-ttu-id="933cf-110">Griglia di eventi usa i codici di risposta HTTP per confermare la ricezione degli eventi.</span><span class="sxs-lookup"><span data-stu-id="933cf-110">Event Grid uses HTTP response codes to acknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="933cf-111">Codici di riuscita</span><span class="sxs-lookup"><span data-stu-id="933cf-111">Success codes</span></span>

<span data-ttu-id="933cf-112">I codici di risposta HTTP seguenti indicano che un evento è stato recapitato correttamente al webhook.</span><span class="sxs-lookup"><span data-stu-id="933cf-112">The following HTTP response codes indicate that an event has been delivered successfully to your webhook.</span></span> <span data-ttu-id="933cf-113">Griglia di eventi considera il recapito completato.</span><span class="sxs-lookup"><span data-stu-id="933cf-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="933cf-114">200 - OK</span><span class="sxs-lookup"><span data-stu-id="933cf-114">200 OK</span></span>
- <span data-ttu-id="933cf-115">202 - Accettato</span><span class="sxs-lookup"><span data-stu-id="933cf-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="933cf-116">Codici di errore</span><span class="sxs-lookup"><span data-stu-id="933cf-116">Failure codes</span></span>

<span data-ttu-id="933cf-117">I codici di risposta HTTP seguenti indicano che un tentativo di recapito di un evento non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="933cf-117">The following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="933cf-118">Griglia di eventi tenta nuovamente di inviare l'evento.</span><span class="sxs-lookup"><span data-stu-id="933cf-118">Event Grid tries again to send the event.</span></span> 

- <span data-ttu-id="933cf-119">400 - Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="933cf-119">400 Bad Request</span></span>
- <span data-ttu-id="933cf-120">401 - Non autorizzato</span><span class="sxs-lookup"><span data-stu-id="933cf-120">401 Unauthorized</span></span>
- <span data-ttu-id="933cf-121">404 - Non trovato</span><span class="sxs-lookup"><span data-stu-id="933cf-121">404 Not Found</span></span>
- <span data-ttu-id="933cf-122">408 - Timeout richiesta</span><span class="sxs-lookup"><span data-stu-id="933cf-122">408 Request timeout</span></span>
- <span data-ttu-id="933cf-123">414 - URI richiesta troppo lungo</span><span class="sxs-lookup"><span data-stu-id="933cf-123">414 URI Too Long</span></span>
- <span data-ttu-id="933cf-124">500 - Errore interno del server</span><span class="sxs-lookup"><span data-stu-id="933cf-124">500 Internal Server Error</span></span>
- <span data-ttu-id="933cf-125">503 - Servizio non disponibile</span><span class="sxs-lookup"><span data-stu-id="933cf-125">503 Service Unavailable</span></span>
- <span data-ttu-id="933cf-126">504 - Timeout gateway</span><span class="sxs-lookup"><span data-stu-id="933cf-126">504 Gateway Timeout</span></span>

<span data-ttu-id="933cf-127">Qualsiasi altro codice di risposta o la mancanza di una risposta indica un errore.</span><span class="sxs-lookup"><span data-stu-id="933cf-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="933cf-128">Griglia di eventi esegue un nuovo tentativo di recapito.</span><span class="sxs-lookup"><span data-stu-id="933cf-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="933cf-129">Intervalli tra tentativi</span><span class="sxs-lookup"><span data-stu-id="933cf-129">Retry intervals</span></span>

<span data-ttu-id="933cf-130">Griglia di eventi usa criteri per i tentativi di tipo backoff esponenziale per il recapito degli eventi.</span><span class="sxs-lookup"><span data-stu-id="933cf-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="933cf-131">Se il webhook non risponde o restituisce un codice di errore, Griglia di eventi esegue un nuovo tentativo di recapito in base alla pianificazione seguente:</span><span class="sxs-lookup"><span data-stu-id="933cf-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on the following schedule:</span></span>

1. <span data-ttu-id="933cf-132">10 secondi</span><span class="sxs-lookup"><span data-stu-id="933cf-132">10 seconds</span></span>
2. <span data-ttu-id="933cf-133">30 secondi</span><span class="sxs-lookup"><span data-stu-id="933cf-133">30 seconds</span></span>
3. <span data-ttu-id="933cf-134">1 minuto</span><span class="sxs-lookup"><span data-stu-id="933cf-134">1 minute</span></span>
4. <span data-ttu-id="933cf-135">5 minuti</span><span class="sxs-lookup"><span data-stu-id="933cf-135">5 minutes</span></span>
5. <span data-ttu-id="933cf-136">10 minuti</span><span class="sxs-lookup"><span data-stu-id="933cf-136">10 minutes</span></span>
6. <span data-ttu-id="933cf-137">30 minuti</span><span class="sxs-lookup"><span data-stu-id="933cf-137">30 minutes</span></span>
7. <span data-ttu-id="933cf-138">1 ora</span><span class="sxs-lookup"><span data-stu-id="933cf-138">1 hour</span></span>

<span data-ttu-id="933cf-139">Griglia di eventi aggiunge una piccola parte di casualità a tutti gli intervalli tra tentativi.</span><span class="sxs-lookup"><span data-stu-id="933cf-139">Event Grid adds a small randomization to all retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="933cf-140">Durata dei tentativi</span><span class="sxs-lookup"><span data-stu-id="933cf-140">Retry duration</span></span>

<span data-ttu-id="933cf-141">Con la versione di anteprima, Griglia di eventi di Azure fa scadere tutti gli eventi che non vengono recapitati entro due ore.</span><span class="sxs-lookup"><span data-stu-id="933cf-141">During the preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="933cf-142">Prima del rilascio del servizio con disponibilità generale, questo intervallo di tempo verrà aumentato a 24 ore.</span><span class="sxs-lookup"><span data-stu-id="933cf-142">Before General Availability, this time will be increased to 24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="933cf-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="933cf-143">Next steps</span></span>

* <span data-ttu-id="933cf-144">Per un'introduzione a Griglia di eventi, vedere [Informazioni su Griglia di eventi](overview.md).</span><span class="sxs-lookup"><span data-stu-id="933cf-144">For an introduction to Event Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="933cf-145">Per iniziare rapidamente a usare Griglia di eventi, vedere [Creare e instradare eventi personalizzati con Griglia di eventi di Azure](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="933cf-145">To quickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>