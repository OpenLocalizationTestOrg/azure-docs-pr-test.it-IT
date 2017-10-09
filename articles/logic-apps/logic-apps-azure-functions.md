---
title: codice aaaCustom per le app di logica di Azure con le funzioni di Azure | Documenti Microsoft
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
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="4e4ba-103">Aggiungere ed eseguire un codice personalizzato per le app per la logica di Azure tramite Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="4e4ba-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="4e4ba-104">toorun frammenti personalizzati di c# o Node. js in App per la logica, è possibile creare funzioni personalizzate mediante le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-104">toorun custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="4e4ba-105">Le [Funzioni di Azure](../azure-functions/functions-overview.md) offrono funzionalità di calcolo indipendenti dal server in Microsoft Azure e sono utili per eseguire queste attività:</span><span class="sxs-lookup"><span data-stu-id="4e4ba-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="4e4ba-106">Formattazione avanzata o calcolo di campi nelle app per la logica</span><span class="sxs-lookup"><span data-stu-id="4e4ba-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="4e4ba-107">Esecuzione di calcoli in un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="4e4ba-108">Estendere le funzionalità di hello logica app con le funzioni che sono supportate in c# o node.js</span><span class="sxs-lookup"><span data-stu-id="4e4ba-108">Extend hello logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="4e4ba-109">Creare funzioni personalizzate per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="4e4ba-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="4e4ba-110">È consigliabile creare una funzione nel portale di Azure funzioni hello da hello **Webhook generico - nodo** o **Webhook - generico c#** modelli.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-110">We recommend that you create a function in hello Azure Functions portal, from hello **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="4e4ba-111">risultato Hello viene creato un popolati automaticamente un modello che accetta `application/json` da un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-111">hello result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="4e4ba-112">Le funzioni che vengono creati tramite questi modelli vengono rilevate automaticamente e visualizzate in hello progettazione applicazione logica in **funzioni di Azure nella mia area.**</span><span class="sxs-lookup"><span data-stu-id="4e4ba-112">Functions that you create from these templates are automatically detected and appear in hello Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="4e4ba-113">Nel portale di Azure su hello hello **integrazione** riquadro per la funzione, il modello viene mostrato che **modalità** impostare troppo**Webhook** e **Webhook tipo** è troppo**JSON generico**.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-113">In hello Azure portal, on hello **Integrate** pane for your function, your template should show that **Mode** set too**Webhook** and **Webhook type** is set too**Generic JSON**.</span></span> 

<span data-ttu-id="4e4ba-114">Funzioni Webhook accettare una richiesta e passarlo nel metodo hello tramite un `data` variabile.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-114">Webhook functions accept a request and pass it into hello method via a `data` variable.</span></span> <span data-ttu-id="4e4ba-115">È possibile accedere a proprietà hello del payload usando la notazione come `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-115">You can access hello properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="4e4ba-116">Ad esempio, una semplice funzione JavaScript che converte un valore DateTime in una stringa di data aspetto hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="4e4ba-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like hello following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="4e4ba-117">Chiamare Funzioni di Azure da app per la logica</span><span class="sxs-lookup"><span data-stu-id="4e4ba-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="4e4ba-118">contenitori di hello toolist nella sottoscrizione e funzione select hello che si desidera toocall, in Progettazione applicazione logica, fare clic su hello **azioni** menu, quindi scegliere **funzioni di Azure nella mia area**.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-118">toolist hello containers in your subscription and select hello function that you want toocall, in Logic App Designer, click hello **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="4e4ba-119">Dopo aver selezionato la funzione hello, sono frequenti toospecify un oggetto payload di input.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-119">After you select hello function, you are asked toospecify an input payload object.</span></span> <span data-ttu-id="4e4ba-120">Questo oggetto è il messaggio hello logica app invia toohello funzione hello e deve essere un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-120">This object is hello message that hello logic app sends toohello function and must be a JSON object.</span></span> <span data-ttu-id="4e4ba-121">Ad esempio, se si desidera toopass in hello **Data ultima modifica** data da un trigger di Salesforce, payload di funzione hello potrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4e4ba-121">For example, if you want toopass in hello **Last Modified** date from a Salesforce trigger, hello function payload might look like this example:</span></span>

![Data ultima modifica][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="4e4ba-123">Attivare app per la logica da una funzione</span><span class="sxs-lookup"><span data-stu-id="4e4ba-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="4e4ba-124">È possibile attivare un'app per la logica all'interno di una funzione.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="4e4ba-125">Vedere [App per la logica come endpoint che è possibile chiamare](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="4e4ba-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="4e4ba-126">Creare un'app di logica che include un trigger manuale, quindi da all'interno della funzione, generare un URL di attivazione manuale toohello HTTP POST con payload hello che si desidera inviare toohello logica app.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST toohello manual trigger URL with hello payload that you want sent toohello logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="4e4ba-127">Creare una funzione dalla finestra di progettazione delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="4e4ba-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="4e4ba-128">È anche possibile creare una funzione di webhook node.js da Progettazione hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-128">You can also create a node.js webhook function from hello designer.</span></span> <span data-ttu-id="4e4ba-129">Selezionare prima di tutto **Funzioni di Azure nell'area** , quindi scegliere un contenitore per la funzione.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="4e4ba-130">Se si dispone ancora di un contenitore, è necessario toocreate da hello [portale di Azure funzioni](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="4e4ba-130">If you don't yet have a container, you need toocreate one from hello [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="4e4ba-131">Selezionare quindi **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-131">Then select **Create New**.</span></span>  

<span data-ttu-id="4e4ba-132">toogenerate un modello basato su dati hello che si desidera toocompute, specificare l'oggetto di contesto hello pianificare toopass in una funzione.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-132">toogenerate a template based on hello data that you want toocompute, specify hello context object that you plan toopass into a function.</span></span> <span data-ttu-id="4e4ba-133">Deve trattarsi di un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-133">This object must be a JSON object.</span></span> <span data-ttu-id="4e4ba-134">Ad esempio, se si passa nel contenuto del file hello da un'azione di FTP, il payload di contesto hello è simile in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="4e4ba-134">For example, if you pass in hello file content from an FTP action, hello context payload looks like this example:</span></span>

![Payload di contesto][2]

> [!NOTE]
> <span data-ttu-id="4e4ba-136">Poiché non è stato eseguito il cast di questo oggetto sotto forma di stringa, payload JSON toohello venga aggiunto direttamente il contenuto di hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-136">Because this object wasn't cast as a string, hello content is added directly toohello JSON payload.</span></span> <span data-ttu-id="4e4ba-137">Tuttavia, si verifica un errore se l'oggetto hello non è un token JSON (ovvero, una stringa o un formato JSON/matrice di oggetti).</span><span class="sxs-lookup"><span data-stu-id="4e4ba-137">However, an error occurs if hello object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="4e4ba-138">oggetto hello toocast sotto forma di stringa, aggiunge le virgolette come illustrato nella figura prima di hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-138">toocast hello object as a string, add quotes as shown in hello first illustration in this article.</span></span>
> 

<span data-ttu-id="4e4ba-139">finestra di progettazione Hello genera quindi un modello di funzione che è possibile creare inline.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-139">hello designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="4e4ba-140">Le variabili sono create in precedenza in base al contesto hello pianificare toopass nella funzione hello.</span><span class="sxs-lookup"><span data-stu-id="4e4ba-140">Variables are pre-created based on hello context that you plan toopass into hello function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
