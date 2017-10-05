---
title: Aggiungere ritardo nelle app per la logica | Microsoft Docs
description: Panoramica delle azioni di ritardo e ritardo fino a e di come usarle con un'app per la logica di Azure.
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
ms.openlocfilehash: 5f4f7052d48b4ca4ed91212d970551141e78e852
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-delay-and-delay-until-actions"></a><span data-ttu-id="1df98-103">Introduzione alle azioni si ritardo e ritardo fino a</span><span class="sxs-lookup"><span data-stu-id="1df98-103">Get started with the delay and delay-until actions</span></span>
<span data-ttu-id="1df98-104">Le azioni di ritardo e "ritardo fino a" consentono di completare scenari di flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="1df98-104">By using the delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="1df98-105">Ad esempio, è possibile:</span><span class="sxs-lookup"><span data-stu-id="1df98-105">For example, you can:</span></span>

* <span data-ttu-id="1df98-106">Attendere fino a un determinato giorno della settimana per inviare un aggiornamento di stato tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="1df98-106">Wait until a weekday to send a status update over email.</span></span>
* <span data-ttu-id="1df98-107">Ritardare il flusso di lavoro fino a quando una chiamata HTTP viene completata prima di riprendere e recuperare i risultati.</span><span class="sxs-lookup"><span data-stu-id="1df98-107">Delay the workflow until an HTTP call has time to finish before resuming and retrieving the result.</span></span>

<span data-ttu-id="1df98-108">Per iniziare a usare un'azione di ritardo in un'app per la logica, vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1df98-108">To get started using the delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-delay-actions"></a><span data-ttu-id="1df98-109">Usare le azioni di ritardo</span><span class="sxs-lookup"><span data-stu-id="1df98-109">Use the delay actions</span></span>
<span data-ttu-id="1df98-110">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="1df98-110">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="1df98-111">[Altre informazioni sulle azioni](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1df98-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="1df98-112">Di seguito è riportata una sequenza di esempio di come usare un passaggio di ritardo in un'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="1df98-112">Here’s an example sequence of how to use a delay step in a logic app:</span></span>

1. <span data-ttu-id="1df98-113">Dopo aver aggiunto un trigger, fare clic su **Nuovo passaggio** per aggiungere un'azione.</span><span class="sxs-lookup"><span data-stu-id="1df98-113">After adding a trigger, click **New Step** to add an action.</span></span>
2. <span data-ttu-id="1df98-114">Cercare **ritardo** per visualizzare le azioni di ritardo.</span><span class="sxs-lookup"><span data-stu-id="1df98-114">Search for **delay** to bring up the delay actions.</span></span> <span data-ttu-id="1df98-115">In questo esempio si selezionerà **Ritarda**.</span><span class="sxs-lookup"><span data-stu-id="1df98-115">In this example, we will select **Delay**.</span></span>
   
    ![Azioni di ritardo](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="1df98-117">Completare tutte le proprietà dell'azione per configurare il ritardo.</span><span class="sxs-lookup"><span data-stu-id="1df98-117">Complete any of the action properties to configure the delay.</span></span>
   
    ![Configurazione del ritardo](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="1df98-119">Fare clic su **Salva** per pubblicare e attivare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="1df98-119">Click **Save** to publish and activate the logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="1df98-120">Informazioni dettagliate sulle azioni</span><span class="sxs-lookup"><span data-stu-id="1df98-120">Action details</span></span>
<span data-ttu-id="1df98-121">Il trigger di ricorrenza ha le proprietà seguenti che possono essere configurate.</span><span class="sxs-lookup"><span data-stu-id="1df98-121">The recurrence trigger has the following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="1df98-122">Azione Ritarda</span><span class="sxs-lookup"><span data-stu-id="1df98-122">Delay action</span></span>
<span data-ttu-id="1df98-123">Questa azione ritarda l'esecuzione per un determinato intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="1df98-123">This action delays the run for a certain time interval.</span></span>
<span data-ttu-id="1df98-124">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1df98-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="1df98-125">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="1df98-125">Display name</span></span> | <span data-ttu-id="1df98-126">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="1df98-126">Property name</span></span> | <span data-ttu-id="1df98-127">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1df98-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1df98-128">Conteggio*</span><span class="sxs-lookup"><span data-stu-id="1df98-128">Count*</span></span> |<span data-ttu-id="1df98-129">count</span><span class="sxs-lookup"><span data-stu-id="1df98-129">count</span></span> |<span data-ttu-id="1df98-130">Il numero di unità di tempo di ritardo</span><span class="sxs-lookup"><span data-stu-id="1df98-130">The number of time units to delay</span></span> |
| <span data-ttu-id="1df98-131">Unità*</span><span class="sxs-lookup"><span data-stu-id="1df98-131">Unit*</span></span> |<span data-ttu-id="1df98-132">unit</span><span class="sxs-lookup"><span data-stu-id="1df98-132">unit</span></span> |<span data-ttu-id="1df98-133">Unità di tempo: `Second`, `Minute`, `Hour` o `Day`</span><span class="sxs-lookup"><span data-stu-id="1df98-133">The unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="1df98-134">Azione Ritarda fino a</span><span class="sxs-lookup"><span data-stu-id="1df98-134">Delay-until action</span></span>
<span data-ttu-id="1df98-135">Questa azione ritarda l'esecuzione fino a una data e ora specificate.</span><span class="sxs-lookup"><span data-stu-id="1df98-135">This action delays the run until a specified date/time.</span></span>
<span data-ttu-id="1df98-136">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="1df98-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="1df98-137">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="1df98-137">Display name</span></span> | <span data-ttu-id="1df98-138">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="1df98-138">Property name</span></span> | <span data-ttu-id="1df98-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1df98-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1df98-140">Anno*</span><span class="sxs-lookup"><span data-stu-id="1df98-140">Year*</span></span> |<span data-ttu-id="1df98-141">timestamp</span><span class="sxs-lookup"><span data-stu-id="1df98-141">timestamp</span></span> |<span data-ttu-id="1df98-142">L'anno di termine del ritardo (GMT)</span><span class="sxs-lookup"><span data-stu-id="1df98-142">The year to delay until (GMT)</span></span> |
| <span data-ttu-id="1df98-143">Mese*</span><span class="sxs-lookup"><span data-stu-id="1df98-143">Month*</span></span> |<span data-ttu-id="1df98-144">timestamp</span><span class="sxs-lookup"><span data-stu-id="1df98-144">timestamp</span></span> |<span data-ttu-id="1df98-145">Il mese di termine del ritardo (GMT)</span><span class="sxs-lookup"><span data-stu-id="1df98-145">The month to delay until (GMT)</span></span> |
| <span data-ttu-id="1df98-146">Giorno*</span><span class="sxs-lookup"><span data-stu-id="1df98-146">Day*</span></span> |<span data-ttu-id="1df98-147">timestamp</span><span class="sxs-lookup"><span data-stu-id="1df98-147">timestamp</span></span> |<span data-ttu-id="1df98-148">Il giorno di termine del ritardo (GMT)</span><span class="sxs-lookup"><span data-stu-id="1df98-148">The day to delay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="1df98-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1df98-149">Next steps</span></span>
<span data-ttu-id="1df98-150">Provare ora a usare la piattaforma e [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1df98-150">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="1df98-151">È possibile esplorare gli altri connettori disponibili nelle app per la logica esaminando l' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="1df98-151">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

