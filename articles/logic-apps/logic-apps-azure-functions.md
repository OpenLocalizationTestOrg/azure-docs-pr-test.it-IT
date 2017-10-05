---
title: Scrivere un codice personalizzato per le app per la logica di Azure con Funzioni di Azure | Microsoft Docs
description: Creare ed eseguire un codice personalizzato per le app per la logica di Azure con Funzioni di Azure
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18442c87b049200fac5ed41cc7034ba7a848b8d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="68830-103">Aggiungere ed eseguire un codice personalizzato per le app per la logica di Azure tramite Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="68830-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="68830-104">Per eseguire frammenti di codice personalizzati di C# o Node.js nelle app per la logica, è possibile creare funzioni personalizzate mediante Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="68830-104">To run custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="68830-105">Le [Funzioni di Azure](../azure-functions/functions-overview.md) offrono funzionalità di calcolo indipendenti dal server in Microsoft Azure e sono utili per eseguire queste attività:</span><span class="sxs-lookup"><span data-stu-id="68830-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="68830-106">Formattazione avanzata o calcolo di campi nelle app per la logica</span><span class="sxs-lookup"><span data-stu-id="68830-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="68830-107">Esecuzione di calcoli in un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="68830-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="68830-108">Estensione della funzionalità delle app per la logica con funzioni supportate in C# o node.js</span><span class="sxs-lookup"><span data-stu-id="68830-108">Extend the logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="68830-109">Creare funzioni personalizzate per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="68830-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="68830-110">È consigliabile creare una funzione nel portale Funzioni di Azure dai modelli **Generic Webhook - Node** (Webhook generico - Node) o **Generic Webhook - C#** (Webhook generico - C#).</span><span class="sxs-lookup"><span data-stu-id="68830-110">We recommend that you create a function in the Azure Functions portal, from the **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="68830-111">Il risultato crea un modello popolato automaticamente che accetta `application/json` da un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="68830-111">The result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="68830-112">Le funzioni che vengono create da questi modelli sono individuate automaticamente ed elencate nella finestra di progettazione delle app per la logica in **Funzioni di Azure nell'area**.</span><span class="sxs-lookup"><span data-stu-id="68830-112">Functions that you create from these templates are automatically detected and appear in the Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="68830-113">Nel portale di Azure, nel riquadro **Integrazione** per la funzione il modello deve visualizzare **Modalità** impostata su **Webhook** e **Tipo di webhook** impostato su **Generic JSON** (JSON generico).</span><span class="sxs-lookup"><span data-stu-id="68830-113">In the Azure portal, on the **Integrate** pane for your function, your template should show that **Mode** set to **Webhook** and **Webhook type** is set to **Generic JSON**.</span></span> 

<span data-ttu-id="68830-114">Le funzioni webhook accettano una richiesta e la passano al metodo tramite una variabile `data` .</span><span class="sxs-lookup"><span data-stu-id="68830-114">Webhook functions accept a request and pass it into the method via a `data` variable.</span></span> <span data-ttu-id="68830-115">È possibile accedere alle proprietà del payload usando una notazione punto come `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="68830-115">You can access the properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="68830-116">Ad esempio, una semplice funzione JavaScript che converte un valore DateTime in una stringa di dati ha un aspetto simile a quello dell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="68830-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like the following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="68830-117">Chiamare Funzioni di Azure da app per la logica</span><span class="sxs-lookup"><span data-stu-id="68830-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="68830-118">Per elencare i contenitori nella sottoscrizione e selezionare la funzione che si desidera chiamare, in Progettazione app per la logica fare clic sul menu **Azioni**e scegliere da **Azure Functions in my Region** (Funzioni di Azure nella mia area).</span><span class="sxs-lookup"><span data-stu-id="68830-118">To list the containers in your subscription and select the function that you want to call, in Logic App Designer, click the **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="68830-119">Dopo la selezione della funzione, viene richiesto di specificare un oggetto payload di input.</span><span class="sxs-lookup"><span data-stu-id="68830-119">After you select the function, you are asked to specify an input payload object.</span></span> <span data-ttu-id="68830-120">Questo oggetto è il messaggio inviato dall'app per la logica alla funzione e deve essere un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="68830-120">This object is the message that the logic app sends to the function and must be a JSON object.</span></span> <span data-ttu-id="68830-121">Se ad esempio si vuole passare la **Data ultima modifica** da un trigger Salesforce, il payload della funzione potrebbe avere un aspetto analogo all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="68830-121">For example, if you want to pass in the **Last Modified** date from a Salesforce trigger, the function payload might look like this example:</span></span>

![Data ultima modifica][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="68830-123">Attivare app per la logica da una funzione</span><span class="sxs-lookup"><span data-stu-id="68830-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="68830-124">È possibile attivare un'app per la logica all'interno di una funzione.</span><span class="sxs-lookup"><span data-stu-id="68830-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="68830-125">Vedere [App per la logica come endpoint che è possibile chiamare](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="68830-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="68830-126">Creare un'app per la logica dotata di trigger manuale, quindi dall'interno della funzione generare un HTTP POST all'URL del trigger manuale con il payload che da inviare all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="68830-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST to the manual trigger URL with the payload that you want sent to the logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="68830-127">Creare una funzione dalla finestra di progettazione delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="68830-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="68830-128">È anche possibile creare una funzione webhook node.js dalla finestra di progettazione.</span><span class="sxs-lookup"><span data-stu-id="68830-128">You can also create a node.js webhook function from the designer.</span></span> <span data-ttu-id="68830-129">Selezionare prima di tutto **Funzioni di Azure nell'area** , quindi scegliere un contenitore per la funzione.</span><span class="sxs-lookup"><span data-stu-id="68830-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="68830-130">Se non è ancora disponibile un contenitore, è necessario crearne uno dal [portale delle funzioni di Azure](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="68830-130">If you don't yet have a container, you need to create one from the [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="68830-131">Selezionare quindi **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="68830-131">Then select **Create New**.</span></span>  

<span data-ttu-id="68830-132">Per generare un modello in base ai dati da elaborare, specificare l'oggetto di contesto che si prevede di passare a una funzione.</span><span class="sxs-lookup"><span data-stu-id="68830-132">To generate a template based on the data that you want to compute, specify the context object that you plan to pass into a function.</span></span> <span data-ttu-id="68830-133">Deve trattarsi di un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="68830-133">This object must be a JSON object.</span></span> <span data-ttu-id="68830-134">Se, ad esempio, si passa il contenuto del file da un'azione FTP, il payload di contesto è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="68830-134">For example, if you pass in the file content from an FTP action, the context payload looks like this example:</span></span>

![Payload di contesto][2]

> [!NOTE]
> <span data-ttu-id="68830-136">Poiché non è stato eseguito il cast per convertire questo oggetto in stringa, il contenuto viene aggiunto direttamente al payload JSON.</span><span class="sxs-lookup"><span data-stu-id="68830-136">Because this object wasn't cast as a string, the content is added directly to the JSON payload.</span></span> <span data-ttu-id="68830-137">Viene tuttavia generato un errore se l'oggetto non è un token JSON, ad esempio una stringa o un oggetto/matrice JSON.</span><span class="sxs-lookup"><span data-stu-id="68830-137">However, an error occurs if the object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="68830-138">Per eseguire il cast come stringa, aggiungere le virgolette, come mostrato nella prima figura di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="68830-138">To cast the object as a string, add quotes as shown in the first illustration in this article.</span></span>
> 

<span data-ttu-id="68830-139">La finestra di progettazione genera quindi un modello di funzione che è possibile creare inline.</span><span class="sxs-lookup"><span data-stu-id="68830-139">The designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="68830-140">Le variabili vengono create prima in base al contesto che si intende passare alla funzione.</span><span class="sxs-lookup"><span data-stu-id="68830-140">Variables are pre-created based on the context that you plan to pass into the function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
