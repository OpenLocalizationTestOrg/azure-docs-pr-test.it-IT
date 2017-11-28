---
title: azione di query aaaAdd hello in App per la logica | Documenti Microsoft
description: Panoramica dell'azione query hello per eseguire azioni come matrice di filtro.
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a><span data-ttu-id="94f9e-103">Iniziare a utilizzare l'azione di query hello</span><span class="sxs-lookup"><span data-stu-id="94f9e-103">Get started with hello query action</span></span>
<span data-ttu-id="94f9e-104">Tramite l'azione di query hello, è possibile utilizzare batch e le matrici tooaccomplish dei flussi di lavoro:</span><span class="sxs-lookup"><span data-stu-id="94f9e-104">By using hello query action, you can work with batches and arrays tooaccomplish workflows to:</span></span>

* <span data-ttu-id="94f9e-105">Creare un'attività per tutti i record ad alta priorità di un database.</span><span class="sxs-lookup"><span data-stu-id="94f9e-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="94f9e-106">Salvare tutti gli allegati PDF per i messaggi di posta elettronica in un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="94f9e-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="94f9e-107">tooget avviato utilizzando l'azione di query hello in un'app di logica, vedere [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="94f9e-107">tooget started using hello query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-query-action"></a><span data-ttu-id="94f9e-108">Utilizzare l'azione di query hello</span><span class="sxs-lookup"><span data-stu-id="94f9e-108">Use hello query action</span></span>
<span data-ttu-id="94f9e-109">Un'azione è un'operazione che viene eseguita dal flusso di lavoro hello è definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="94f9e-109">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="94f9e-110">[Altre informazioni sulle azioni](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="94f9e-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="94f9e-111">azione di query Hello è attualmente un'unica operazione, detta matrice di filtro hello, che viene visualizzata nella finestra di progettazione hello.</span><span class="sxs-lookup"><span data-stu-id="94f9e-111">hello query action currently has one operation, called hello filter array, that is exposed in hello designer.</span></span> <span data-ttu-id="94f9e-112">Ciò consente tooquery una matrice e restituire un set di risultati filtrati.</span><span class="sxs-lookup"><span data-stu-id="94f9e-112">This allows you tooquery an array and return a set of filtered results.</span></span>

<span data-ttu-id="94f9e-113">Ecco come è possibile aggiungerla in un'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="94f9e-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="94f9e-114">Seleziona hello **nuovo passaggio** pulsante.</span><span class="sxs-lookup"><span data-stu-id="94f9e-114">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="94f9e-115">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="94f9e-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="94f9e-116">Nella casella di ricerca azione hello, digitare **filtro** hello toolist **matrice filtro** azione.</span><span class="sxs-lookup"><span data-stu-id="94f9e-116">In hello action search box, type **filter** toolist hello **Filter array** action.</span></span>
   
    ![Selezionare l'azione di query hello](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="94f9e-118">Selezionare un toofilter di matrice.</span><span class="sxs-lookup"><span data-stu-id="94f9e-118">Select an array toofilter.</span></span> <span data-ttu-id="94f9e-119">(hello seguente schermata Mostra matrice hello di risultati da una ricerca di Twitter.)</span><span class="sxs-lookup"><span data-stu-id="94f9e-119">(hello following screenshot shows hello array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="94f9e-120">Creare una condizione tooevaluate su ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="94f9e-120">Create a condition tooevaluate on each item.</span></span> <span data-ttu-id="94f9e-121">(hello seguente schermata Filtra TWEET gli utenti che hanno bisogno di più di 100 seguenti).</span><span class="sxs-lookup"><span data-stu-id="94f9e-121">(hello following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Azione di query completa hello](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="94f9e-123">azione di Hello output conterrà una nuova matrice che contiene solo i risultati che soddisfano i requisiti di filtro hello.</span><span class="sxs-lookup"><span data-stu-id="94f9e-123">hello action will output a new array that contains only results that met hello filter requirements.</span></span>
6. <span data-ttu-id="94f9e-124">Fare clic su nell'angolo superiore sinistro hello di hello barra degli strumenti toosave e la logica app verrà entrambi salvare e pubblicare (attivare).</span><span class="sxs-lookup"><span data-stu-id="94f9e-124">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="94f9e-125">Azione di query</span><span class="sxs-lookup"><span data-stu-id="94f9e-125">Query action</span></span>
<span data-ttu-id="94f9e-126">Ecco hello dettagli per l'azione di hello che supporta questo connettore.</span><span class="sxs-lookup"><span data-stu-id="94f9e-126">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="94f9e-127">connettore Hello è un'opzione possibile.</span><span class="sxs-lookup"><span data-stu-id="94f9e-127">hello connector has one possible action.</span></span>

| <span data-ttu-id="94f9e-128">Azione</span><span class="sxs-lookup"><span data-stu-id="94f9e-128">Action</span></span> | <span data-ttu-id="94f9e-129">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94f9e-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="94f9e-130">Filtra matrice</span><span class="sxs-lookup"><span data-stu-id="94f9e-130">Filter array</span></span> |<span data-ttu-id="94f9e-131">Valuta una condizione per ogni elemento in una matrice e restituisce i risultati di hello</span><span class="sxs-lookup"><span data-stu-id="94f9e-131">Evaluates a condition for each item in an array and returns hello results</span></span> |

## <a name="action-details"></a><span data-ttu-id="94f9e-132">Informazioni dettagliate sulle azioni</span><span class="sxs-lookup"><span data-stu-id="94f9e-132">Action details</span></span>
<span data-ttu-id="94f9e-133">l'azione di query Hello viene fornito con un'azione possibile.</span><span class="sxs-lookup"><span data-stu-id="94f9e-133">hello query action comes with one possible action.</span></span> <span data-ttu-id="94f9e-134">Hello nelle tabelle seguenti vengono descritti hello necessarie e i campi di input facoltativi per azione di hello e i dettagli di output corrispondenti hello associati mediante l'azione di hello.</span><span class="sxs-lookup"><span data-stu-id="94f9e-134">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="94f9e-135">Filtra matrice</span><span class="sxs-lookup"><span data-stu-id="94f9e-135">Filter array</span></span>
<span data-ttu-id="94f9e-136">di seguito Hello sono campi di input per l'azione di hello, che esegue una richiesta HTTP in uscita.</span><span class="sxs-lookup"><span data-stu-id="94f9e-136">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="94f9e-137">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="94f9e-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="94f9e-138">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="94f9e-138">Display name</span></span> | <span data-ttu-id="94f9e-139">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="94f9e-139">Property name</span></span> | <span data-ttu-id="94f9e-140">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94f9e-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="94f9e-141">Da*</span><span class="sxs-lookup"><span data-stu-id="94f9e-141">From*</span></span> |<span data-ttu-id="94f9e-142">from</span><span class="sxs-lookup"><span data-stu-id="94f9e-142">from</span></span> |<span data-ttu-id="94f9e-143">Hello matrice toofilter</span><span class="sxs-lookup"><span data-stu-id="94f9e-143">hello array toofilter</span></span> |
| <span data-ttu-id="94f9e-144">Condizione*</span><span class="sxs-lookup"><span data-stu-id="94f9e-144">Condition*</span></span> |<span data-ttu-id="94f9e-145">dove</span><span class="sxs-lookup"><span data-stu-id="94f9e-145">where</span></span> |<span data-ttu-id="94f9e-146">Hello tooevaluate condizione per ogni elemento</span><span class="sxs-lookup"><span data-stu-id="94f9e-146">hello condition tooevaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="94f9e-147">Dettagli dell'output</span><span class="sxs-lookup"><span data-stu-id="94f9e-147">Output details</span></span>
<span data-ttu-id="94f9e-148">di seguito Hello sono i dettagli di output per hello risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="94f9e-148">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="94f9e-149">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="94f9e-149">Property name</span></span> | <span data-ttu-id="94f9e-150">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="94f9e-150">Data type</span></span> | <span data-ttu-id="94f9e-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="94f9e-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="94f9e-152">Matrice filtrata</span><span class="sxs-lookup"><span data-stu-id="94f9e-152">Filtered array</span></span> |<span data-ttu-id="94f9e-153">array</span><span class="sxs-lookup"><span data-stu-id="94f9e-153">array</span></span> |<span data-ttu-id="94f9e-154">Matrice che contiene un oggetto per ogni risultato filtrato</span><span class="sxs-lookup"><span data-stu-id="94f9e-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="94f9e-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94f9e-155">Next steps</span></span>
<span data-ttu-id="94f9e-156">A questo punto, provare a piattaforma hello e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="94f9e-156">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="94f9e-157">È possibile esplorare altri connettori disponibile in App per la logica di hello esaminando il nostro [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="94f9e-157">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

