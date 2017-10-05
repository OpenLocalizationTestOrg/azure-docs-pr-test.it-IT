---
title: Aggiungere l'azione di query alle app per la logica | Documentazione Microsoft
description: Panoramica dell'azione di query per l'esecuzione di azioni come Filtra matrice.
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
ms.openlocfilehash: a992fa17a07d6167297c4cf5fe9fb3b58181d7df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-query-action"></a><span data-ttu-id="21fd1-103">Introduzione all'azione di query</span><span class="sxs-lookup"><span data-stu-id="21fd1-103">Get started with the query action</span></span>
<span data-ttu-id="21fd1-104">Con l'azione di query è possibile usare batch e matrici per poter eseguire flussi di lavoro per:</span><span class="sxs-lookup"><span data-stu-id="21fd1-104">By using the query action, you can work with batches and arrays to accomplish workflows to:</span></span>

* <span data-ttu-id="21fd1-105">Creare un'attività per tutti i record ad alta priorità di un database.</span><span class="sxs-lookup"><span data-stu-id="21fd1-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="21fd1-106">Salvare tutti gli allegati PDF per i messaggi di posta elettronica in un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="21fd1-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="21fd1-107">Per iniziare a usare l'azione di query in un'app per la logica, vedere [Creare una nuova app per la logica che connette servizi SaaS](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="21fd1-107">To get started using the query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-query-action"></a><span data-ttu-id="21fd1-108">Usare l'azione di query</span><span class="sxs-lookup"><span data-stu-id="21fd1-108">Use the query action</span></span>
<span data-ttu-id="21fd1-109">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="21fd1-109">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="21fd1-110">[Altre informazioni sulle azioni](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="21fd1-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="21fd1-111">L'azione di query ha attualmente un'operazione, denominata Filtra matrice, esposta nella finestra di progettazione.</span><span class="sxs-lookup"><span data-stu-id="21fd1-111">The query action currently has one operation, called the filter array, that is exposed in the designer.</span></span> <span data-ttu-id="21fd1-112">Questa consente di interrogare una matrice e restituire un set di risultati filtrati.</span><span class="sxs-lookup"><span data-stu-id="21fd1-112">This allows you to query an array and return a set of filtered results.</span></span>

<span data-ttu-id="21fd1-113">Ecco come è possibile aggiungerla in un'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="21fd1-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="21fd1-114">Fare clic sul pulsante **Nuovo passaggio** .</span><span class="sxs-lookup"><span data-stu-id="21fd1-114">Select the **New Step** button.</span></span>
2. <span data-ttu-id="21fd1-115">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="21fd1-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="21fd1-116">Nella casella di ricerca azione digitare **filtro** per elencare l'azione **Filtra matrice**.</span><span class="sxs-lookup"><span data-stu-id="21fd1-116">In the action search box, type **filter** to list the **Filter array** action.</span></span>
   
    ![Selezionare l'azione di query](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="21fd1-118">Selezionare una matrice da filtrare.</span><span class="sxs-lookup"><span data-stu-id="21fd1-118">Select an array to filter.</span></span> <span data-ttu-id="21fd1-119">Lo screenshot seguente illustra la matrice di risultati ottenuta da una ricerca in Twitter.</span><span class="sxs-lookup"><span data-stu-id="21fd1-119">(The following screenshot shows the array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="21fd1-120">Creare una condizione da valutare per ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="21fd1-120">Create a condition to evaluate on each item.</span></span> <span data-ttu-id="21fd1-121">Lo screenshot seguente filtra i tweet degli utenti con più di 100 follower.</span><span class="sxs-lookup"><span data-stu-id="21fd1-121">(The following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Completare l'azione di query](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="21fd1-123">L'azione genera una nuova matrice che contiene solo i risultati che soddisfano i requisiti del filtro.</span><span class="sxs-lookup"><span data-stu-id="21fd1-123">The action will output a new array that contains only results that met the filter requirements.</span></span>
6. <span data-ttu-id="21fd1-124">Fare clic sull'angolo in alto a sinistra della barra degli strumenti per salvare e pubblicare (attivare) l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="21fd1-124">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="21fd1-125">Azione di query</span><span class="sxs-lookup"><span data-stu-id="21fd1-125">Query action</span></span>
<span data-ttu-id="21fd1-126">Ecco i dettagli per l'azione supportata da questo connettore.</span><span class="sxs-lookup"><span data-stu-id="21fd1-126">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="21fd1-127">Il connettore supporta una sola azione possibile.</span><span class="sxs-lookup"><span data-stu-id="21fd1-127">The connector has one possible action.</span></span>

| <span data-ttu-id="21fd1-128">Azione</span><span class="sxs-lookup"><span data-stu-id="21fd1-128">Action</span></span> | <span data-ttu-id="21fd1-129">Descrizione</span><span class="sxs-lookup"><span data-stu-id="21fd1-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21fd1-130">Filtra matrice</span><span class="sxs-lookup"><span data-stu-id="21fd1-130">Filter array</span></span> |<span data-ttu-id="21fd1-131">Valuta una condizione per ogni elemento in una matrice e restituisce i risultati</span><span class="sxs-lookup"><span data-stu-id="21fd1-131">Evaluates a condition for each item in an array and returns the results</span></span> |

## <a name="action-details"></a><span data-ttu-id="21fd1-132">Informazioni dettagliate sulle azioni</span><span class="sxs-lookup"><span data-stu-id="21fd1-132">Action details</span></span>
<span data-ttu-id="21fd1-133">L'azione di query supporta un'azione possibile.</span><span class="sxs-lookup"><span data-stu-id="21fd1-133">The query action comes with one possible action.</span></span> <span data-ttu-id="21fd1-134">La tabella seguente descrive i campi di input obbligatori e facoltativi per l'azione e i dettagli di output corrispondenti associati all'uso dell'azione.</span><span class="sxs-lookup"><span data-stu-id="21fd1-134">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="21fd1-135">Filtra matrice</span><span class="sxs-lookup"><span data-stu-id="21fd1-135">Filter array</span></span>
<span data-ttu-id="21fd1-136">Di seguito sono riportati campi di input per l'azione, che esegue una richiesta HTTP in uscita.</span><span class="sxs-lookup"><span data-stu-id="21fd1-136">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="21fd1-137">Un asterisco (*) indica che è un campo obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="21fd1-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="21fd1-138">Nome visualizzato</span><span class="sxs-lookup"><span data-stu-id="21fd1-138">Display name</span></span> | <span data-ttu-id="21fd1-139">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="21fd1-139">Property name</span></span> | <span data-ttu-id="21fd1-140">Descrizione</span><span class="sxs-lookup"><span data-stu-id="21fd1-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21fd1-141">Da*</span><span class="sxs-lookup"><span data-stu-id="21fd1-141">From*</span></span> |<span data-ttu-id="21fd1-142">from</span><span class="sxs-lookup"><span data-stu-id="21fd1-142">from</span></span> |<span data-ttu-id="21fd1-143">La matrice da filtrare</span><span class="sxs-lookup"><span data-stu-id="21fd1-143">The array to filter</span></span> |
| <span data-ttu-id="21fd1-144">Condizione*</span><span class="sxs-lookup"><span data-stu-id="21fd1-144">Condition*</span></span> |<span data-ttu-id="21fd1-145">dove</span><span class="sxs-lookup"><span data-stu-id="21fd1-145">where</span></span> |<span data-ttu-id="21fd1-146">La condizione da valutare per ogni elemento</span><span class="sxs-lookup"><span data-stu-id="21fd1-146">The condition to evaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="21fd1-147">Dettagli dell'output</span><span class="sxs-lookup"><span data-stu-id="21fd1-147">Output details</span></span>
<span data-ttu-id="21fd1-148">Di seguito sono riportati i dettagli di output per la risposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="21fd1-148">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="21fd1-149">Nome proprietà</span><span class="sxs-lookup"><span data-stu-id="21fd1-149">Property name</span></span> | <span data-ttu-id="21fd1-150">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="21fd1-150">Data type</span></span> | <span data-ttu-id="21fd1-151">Descrizione</span><span class="sxs-lookup"><span data-stu-id="21fd1-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21fd1-152">Matrice filtrata</span><span class="sxs-lookup"><span data-stu-id="21fd1-152">Filtered array</span></span> |<span data-ttu-id="21fd1-153">array</span><span class="sxs-lookup"><span data-stu-id="21fd1-153">array</span></span> |<span data-ttu-id="21fd1-154">Matrice che contiene un oggetto per ogni risultato filtrato</span><span class="sxs-lookup"><span data-stu-id="21fd1-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="21fd1-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21fd1-155">Next steps</span></span>
<span data-ttu-id="21fd1-156">Provare ora a usare la piattaforma e [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="21fd1-156">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="21fd1-157">È possibile esplorare gli altri connettori disponibili nelle app per la logica esaminando l' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="21fd1-157">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

