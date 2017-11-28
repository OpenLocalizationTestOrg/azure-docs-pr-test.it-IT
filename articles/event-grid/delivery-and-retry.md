---
title: nuovo tentativo e il recapito di griglia eventi aaaAzure
description: Viene descritto in che modo Griglia di eventi di Azure recapita gli eventi e come gestisce i messaggi non recapitati.
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="d4362-103">Recapito di messaggi di Griglia di eventi e nuovi tentativi</span><span class="sxs-lookup"><span data-stu-id="d4362-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="d4362-104">Questo articolo descrive in che modo Griglia di eventi di Azure gestisce gli eventi quando il recapito non viene confermato.</span><span class="sxs-lookup"><span data-stu-id="d4362-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="d4362-105">Griglia di eventi fornisce il recapito durevole.</span><span class="sxs-lookup"><span data-stu-id="d4362-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="d4362-106">Ogni messaggio viene recapitato almeno una volta per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d4362-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="d4362-107">Gli eventi vengono inviati immediatamente webhook toohello registrato di ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d4362-107">Events are sent toohello registered webhook of each subscription immediately.</span></span> <span data-ttu-id="d4362-108">Se un webhook non riconosce la ricezione di un evento all'interno di 60 secondi, di recapito prima hello tentano, griglia eventi tentativi di recapito dei messaggi di evento hello.</span><span class="sxs-lookup"><span data-stu-id="d4362-108">If a webhook does not acknowledge receipt of an event within 60 seconds of hello first delivery attempt, Event Grid retries delivery of hello event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="d4362-109">Stato di recapito del messaggio</span><span class="sxs-lookup"><span data-stu-id="d4362-109">Message delivery status</span></span>

<span data-ttu-id="d4362-110">Griglia di eventi Usa HTTP risposta codici tooacknowledge conferma recapito eventi.</span><span class="sxs-lookup"><span data-stu-id="d4362-110">Event Grid uses HTTP response codes tooacknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="d4362-111">Codici di riuscita</span><span class="sxs-lookup"><span data-stu-id="d4362-111">Success codes</span></span>

<span data-ttu-id="d4362-112">Hello codici di risposta HTTP seguenti indicano che un evento è stato recapitato correttamente tooyour webhook.</span><span class="sxs-lookup"><span data-stu-id="d4362-112">hello following HTTP response codes indicate that an event has been delivered successfully tooyour webhook.</span></span> <span data-ttu-id="d4362-113">Griglia di eventi considera il recapito completato.</span><span class="sxs-lookup"><span data-stu-id="d4362-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="d4362-114">200 - OK</span><span class="sxs-lookup"><span data-stu-id="d4362-114">200 OK</span></span>
- <span data-ttu-id="d4362-115">202 - Accettato</span><span class="sxs-lookup"><span data-stu-id="d4362-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="d4362-116">Codici di errore</span><span class="sxs-lookup"><span data-stu-id="d4362-116">Failure codes</span></span>

<span data-ttu-id="d4362-117">Hello seguenti codici di risposta HTTP indica che un tentativo di recapito eventi non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="d4362-117">hello following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="d4362-118">Griglia di eventi tenta nuovamente di evento hello toosend.</span><span class="sxs-lookup"><span data-stu-id="d4362-118">Event Grid tries again toosend hello event.</span></span> 

- <span data-ttu-id="d4362-119">400 - Richiesta non valida</span><span class="sxs-lookup"><span data-stu-id="d4362-119">400 Bad Request</span></span>
- <span data-ttu-id="d4362-120">401 - Non autorizzato</span><span class="sxs-lookup"><span data-stu-id="d4362-120">401 Unauthorized</span></span>
- <span data-ttu-id="d4362-121">404 - Non trovato</span><span class="sxs-lookup"><span data-stu-id="d4362-121">404 Not Found</span></span>
- <span data-ttu-id="d4362-122">408 - Timeout richiesta</span><span class="sxs-lookup"><span data-stu-id="d4362-122">408 Request timeout</span></span>
- <span data-ttu-id="d4362-123">414 - URI richiesta troppo lungo</span><span class="sxs-lookup"><span data-stu-id="d4362-123">414 URI Too Long</span></span>
- <span data-ttu-id="d4362-124">500 - Errore interno del server</span><span class="sxs-lookup"><span data-stu-id="d4362-124">500 Internal Server Error</span></span>
- <span data-ttu-id="d4362-125">503 - Servizio non disponibile</span><span class="sxs-lookup"><span data-stu-id="d4362-125">503 Service Unavailable</span></span>
- <span data-ttu-id="d4362-126">504 - Timeout gateway</span><span class="sxs-lookup"><span data-stu-id="d4362-126">504 Gateway Timeout</span></span>

<span data-ttu-id="d4362-127">Qualsiasi altro codice di risposta o la mancanza di una risposta indica un errore.</span><span class="sxs-lookup"><span data-stu-id="d4362-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="d4362-128">Griglia di eventi esegue un nuovo tentativo di recapito.</span><span class="sxs-lookup"><span data-stu-id="d4362-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="d4362-129">Intervalli tra tentativi</span><span class="sxs-lookup"><span data-stu-id="d4362-129">Retry intervals</span></span>

<span data-ttu-id="d4362-130">Griglia di eventi usa criteri per i tentativi di tipo backoff esponenziale per il recapito degli eventi.</span><span class="sxs-lookup"><span data-stu-id="d4362-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="d4362-131">Se il webhook non risponde o restituisce un codice di errore, griglia evento tentativi di recapito in base alla pianificazione hello:</span><span class="sxs-lookup"><span data-stu-id="d4362-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on hello following schedule:</span></span>

1. <span data-ttu-id="d4362-132">10 secondi</span><span class="sxs-lookup"><span data-stu-id="d4362-132">10 seconds</span></span>
2. <span data-ttu-id="d4362-133">30 secondi</span><span class="sxs-lookup"><span data-stu-id="d4362-133">30 seconds</span></span>
3. <span data-ttu-id="d4362-134">1 minuto</span><span class="sxs-lookup"><span data-stu-id="d4362-134">1 minute</span></span>
4. <span data-ttu-id="d4362-135">5 minuti</span><span class="sxs-lookup"><span data-stu-id="d4362-135">5 minutes</span></span>
5. <span data-ttu-id="d4362-136">10 minuti</span><span class="sxs-lookup"><span data-stu-id="d4362-136">10 minutes</span></span>
6. <span data-ttu-id="d4362-137">30 minuti</span><span class="sxs-lookup"><span data-stu-id="d4362-137">30 minutes</span></span>
7. <span data-ttu-id="d4362-138">1 ora</span><span class="sxs-lookup"><span data-stu-id="d4362-138">1 hour</span></span>

<span data-ttu-id="d4362-139">Griglia di eventi aggiunge gli intervalli tra tentativi di tooall una sequenza casuale di piccole dimensioni.</span><span class="sxs-lookup"><span data-stu-id="d4362-139">Event Grid adds a small randomization tooall retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="d4362-140">Durata dei tentativi</span><span class="sxs-lookup"><span data-stu-id="d4362-140">Retry duration</span></span>

<span data-ttu-id="d4362-141">Durante l'anteprima di hello, tutti gli eventi che non vengono recapitati entro due ore di scadenza della griglia di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4362-141">During hello preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="d4362-142">Prima della disponibilità generale, questo tempo sarà maggiore too24 ore.</span><span class="sxs-lookup"><span data-stu-id="d4362-142">Before General Availability, this time will be increased too24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d4362-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4362-143">Next steps</span></span>

* <span data-ttu-id="d4362-144">Per un'introduzione tooEvent griglia, vedere [sulla griglia di eventi](overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4362-144">For an introduction tooEvent Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="d4362-145">tooquickly informazioni introduttive sull'utilizzo della griglia di eventi, vedere [route e creare eventi personalizzati con griglia di eventi di Azure](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="d4362-145">tooquickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
