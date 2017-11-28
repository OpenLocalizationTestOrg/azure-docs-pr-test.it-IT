---
title: un ritardo nell'App per la logica aaaAdd | Documenti Microsoft
description: Panoramica di hello ritardo e il ritardo-fino a quando le azioni e come toouse con un'app per la logica di Azure.
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a><span data-ttu-id="162ee-103">Introduzione a hello ritardo e il ritardo-fino a quando le azioni</span><span class="sxs-lookup"><span data-stu-id="162ee-103">Get started with hello delay and delay-until actions</span></span>
<span data-ttu-id="162ee-104">Tramite il ritardo di hello e "ritardo-fino a quando non" azioni, è possibile completare gli scenari di flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="162ee-104">By using hello delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="162ee-105">Ad esempio, è possibile:</span><span class="sxs-lookup"><span data-stu-id="162ee-105">For example, you can:</span></span>

* <span data-ttu-id="162ee-106">Attendere l'aggiornamento toosend un giorno della settimana lo stato tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="162ee-106">Wait until a weekday toosend a status update over email.</span></span>
* <span data-ttu-id="162ee-107">Ritardo del flusso di lavoro hello fino a quando una chiamata HTTP è ora toofinish prima di ripresa e recuperare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="162ee-107">Delay hello workflow until an HTTP call has time toofinish before resuming and retrieving hello result.</span></span>

<span data-ttu-id="162ee-108">tooget avviato utilizzando l'azione di ritardo hello in un'app di logica, vedere [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="162ee-108">tooget started using hello delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-delay-actions"></a><span data-ttu-id="162ee-109">Utilizzare le azioni di ritardo hello</span><span class="sxs-lookup"><span data-stu-id="162ee-109">Use hello delay actions</span></span>
<span data-ttu-id="162ee-110">Un'azione è un'operazione che viene eseguita dal flusso di lavoro hello è definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="162ee-110">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="162ee-111">[Altre informazioni sulle azioni](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="162ee-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="162ee-112">Di seguito è riportata una sequenza di esempio della modalità di passaggio toouse un ritardo in un'app di logica:</span><span class="sxs-lookup"><span data-stu-id="162ee-112">Here’s an example sequence of how toouse a delay step in a logic app:</span></span>

1. <span data-ttu-id="162ee-113">Dopo l'aggiunta di un trigger, fare clic su **nuovo passaggio** tooadd un'azione.</span><span class="sxs-lookup"><span data-stu-id="162ee-113">After adding a trigger, click **New Step** tooadd an action.</span></span>
2. <span data-ttu-id="162ee-114">Cercare **ritardo** toobring le azioni di ritardo hello.</span><span class="sxs-lookup"><span data-stu-id="162ee-114">Search for **delay** toobring up hello delay actions.</span></span> <span data-ttu-id="162ee-115">In questo esempio si selezionerà **Ritarda**.</span><span class="sxs-lookup"><span data-stu-id="162ee-115">In this example, we will select **Delay**.</span></span>
   
    ![Azioni di ritardo](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="162ee-117">Completa eventuali di ritardo di hello azione proprietà tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="162ee-117">Complete any of hello action properties tooconfigure hello delay.</span></span>
   
    ![Configurazione del ritardo](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="162ee-119">Fare clic su **salvare** toopublish e attivare hello logica app.</span><span class="sxs-lookup"><span data-stu-id="162ee-119">Click **Save** toopublish and activate hello logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="162ee-120">Informazioni dettagliate sulle azioni</span><span class="sxs-lookup"><span data-stu-id="162ee-120">Action details</span></span>
<span data-ttu-id="162ee-121">i trigger di ricorrenza Hello è hello seguenti proprietà che possono essere configurate.</span><span class="sxs-lookup"><span data-stu-id="162ee-121">hello recurrence trigger has hello following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="162ee-122">Azione Ritarda</span><span class="sxs-lookup"><span data-stu-id="162ee-122">Delay action</span></span>
<span data-ttu-id="162ee-123">Questo hello ritardi azione eseguita per un determinato intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="162ee-123">This action delays hello run for a certain time interval.</span></span>
<span data-ttu-id="162ee-124">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="162ee-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="162ee-125">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="162ee-125">Display name</span></span> | <span data-ttu-id="162ee-126">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="162ee-126">Property name</span></span> | <span data-ttu-id="162ee-127">Descrizione</span><span class="sxs-lookup"><span data-stu-id="162ee-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="162ee-128">Conteggio*</span><span class="sxs-lookup"><span data-stu-id="162ee-128">Count*</span></span> |<span data-ttu-id="162ee-129">count</span><span class="sxs-lookup"><span data-stu-id="162ee-129">count</span></span> |<span data-ttu-id="162ee-130">numero di Hello di toodelay unità di tempo</span><span class="sxs-lookup"><span data-stu-id="162ee-130">hello number of time units toodelay</span></span> |
| <span data-ttu-id="162ee-131">Unità*</span><span class="sxs-lookup"><span data-stu-id="162ee-131">Unit*</span></span> |<span data-ttu-id="162ee-132">unit</span><span class="sxs-lookup"><span data-stu-id="162ee-132">unit</span></span> |<span data-ttu-id="162ee-133">unità di Hello di tempo: `Second`, `Minute`, `Hour`, o`Day`</span><span class="sxs-lookup"><span data-stu-id="162ee-133">hello unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="162ee-134">Azione Ritarda fino a</span><span class="sxs-lookup"><span data-stu-id="162ee-134">Delay-until action</span></span>
<span data-ttu-id="162ee-135">Questa azione consente di ritardare hello eseguito fino a quando una data/ora specificata.</span><span class="sxs-lookup"><span data-stu-id="162ee-135">This action delays hello run until a specified date/time.</span></span>
<span data-ttu-id="162ee-136">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="162ee-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="162ee-137">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="162ee-137">Display name</span></span> | <span data-ttu-id="162ee-138">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="162ee-138">Property name</span></span> | <span data-ttu-id="162ee-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="162ee-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="162ee-140">Anno*</span><span class="sxs-lookup"><span data-stu-id="162ee-140">Year*</span></span> |<span data-ttu-id="162ee-141">timestamp</span><span class="sxs-lookup"><span data-stu-id="162ee-141">timestamp</span></span> |<span data-ttu-id="162ee-142">Hello anno toodelay finché (GMT)</span><span class="sxs-lookup"><span data-stu-id="162ee-142">hello year toodelay until (GMT)</span></span> |
| <span data-ttu-id="162ee-143">Mese*</span><span class="sxs-lookup"><span data-stu-id="162ee-143">Month*</span></span> |<span data-ttu-id="162ee-144">timestamp</span><span class="sxs-lookup"><span data-stu-id="162ee-144">timestamp</span></span> |<span data-ttu-id="162ee-145">Hello mese toodelay finché (GMT)</span><span class="sxs-lookup"><span data-stu-id="162ee-145">hello month toodelay until (GMT)</span></span> |
| <span data-ttu-id="162ee-146">Giorno*</span><span class="sxs-lookup"><span data-stu-id="162ee-146">Day*</span></span> |<span data-ttu-id="162ee-147">timestamp</span><span class="sxs-lookup"><span data-stu-id="162ee-147">timestamp</span></span> |<span data-ttu-id="162ee-148">Hello toodelay giorno finché (GMT)</span><span class="sxs-lookup"><span data-stu-id="162ee-148">hello day toodelay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="162ee-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="162ee-149">Next steps</span></span>
<span data-ttu-id="162ee-150">A questo punto, provare a piattaforma hello e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="162ee-150">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="162ee-151">È possibile esplorare altri connettori disponibile in App per la logica di hello esaminando il nostro [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="162ee-151">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

