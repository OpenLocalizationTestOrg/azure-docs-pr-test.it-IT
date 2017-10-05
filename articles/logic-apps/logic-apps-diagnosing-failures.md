---
title: Diagnosi degli errori - App per la logica di Azure | Documentazione Microsoft
description: Approcci comuni per la comprensione degli errori delle app per la logica
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 814e6f93088cdd96b0a663d2a7494b5a11470d99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="11fa0-103">Eseguire una diagnosi degli errori delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="11fa0-103">Diagnose logic app failures</span></span>
<span data-ttu-id="11fa0-104">Se si verificano problemi o errori con le app per la logica, con alcuni accorgimenti sarà possibile capire meglio l'origine degli errori.</span><span class="sxs-lookup"><span data-stu-id="11fa0-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where the failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="11fa0-105">Strumenti del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="11fa0-105">Azure portal tools</span></span>
<span data-ttu-id="11fa0-106">Il portale di Azure offre molti strumenti per la diagnosi delle app per la logica a ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="11fa0-106">The Azure portal provides many tools to diagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="11fa0-107">Cronologia di attivazione</span><span class="sxs-lookup"><span data-stu-id="11fa0-107">Trigger history</span></span>

<span data-ttu-id="11fa0-108">Ogni app per la logica ha almeno un trigger.</span><span class="sxs-lookup"><span data-stu-id="11fa0-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="11fa0-109">Se si nota che le app non vengono attivate, controllare prima la cronologia di attivazione per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="11fa0-109">If you notice that apps aren't firing, look first at the trigger history for more information.</span></span> <span data-ttu-id="11fa0-110">La cronologia di attivazione è disponibile nel pannello principale delle app per la logica.</span><span class="sxs-lookup"><span data-stu-id="11fa0-110">You can access the trigger history on the logic app'ss main blade.</span></span>

![Accedere alla cronologia dei trigger][1]

<span data-ttu-id="11fa0-112">Elenca tutti i tentativi di attivazione eseguiti dall'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="11fa0-112">The trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="11fa0-113">Facendo clic su ogni tentativo di attivazione si esegue il drill-down dei dettagli, nello specifico sugli eventuali input o output generati dal tentativo di attivazione.</span><span class="sxs-lookup"><span data-stu-id="11fa0-113">You can click each trigger attempt to drill into the details, specifically, any inputs or outputs that the trigger attempt generated.</span></span> <span data-ttu-id="11fa0-114">Se si individuano trigger non riusciti, selezionare il tentativo di trigger e scegliere il collegamento **Output** per rivedere tutti i messaggi di errore generati, ad esempio quelli relativi a credenziali FTP non valide.</span><span class="sxs-lookup"><span data-stu-id="11fa0-114">If you find failed triggers, select the trigger attempt and choose the **Outputs** link to review any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="11fa0-115">Possono essere visualizzati i seguenti stati:</span><span class="sxs-lookup"><span data-stu-id="11fa0-115">The different statuses you might see are:</span></span>

* <span data-ttu-id="11fa0-116">**Operazione ignorata**.</span><span class="sxs-lookup"><span data-stu-id="11fa0-116">**Skipped**.</span></span> <span data-ttu-id="11fa0-117">È stato eseguito il poll dell'endpoint per verificare la presenza di dati e la risposta ricevuta ha indicato che non ci sono dati disponibili.</span><span class="sxs-lookup"><span data-stu-id="11fa0-117">The endpoint was polled to check for data and received a response that no data was available.</span></span>
* <span data-ttu-id="11fa0-118">**Operazione completata**.</span><span class="sxs-lookup"><span data-stu-id="11fa0-118">**Succeeded**.</span></span> <span data-ttu-id="11fa0-119">La risposta ricevuta dal trigger ha indicato che non sono disponibili dati.</span><span class="sxs-lookup"><span data-stu-id="11fa0-119">The trigger received a response that data was available.</span></span> <span data-ttu-id="11fa0-120">Questo può essere il risultato di un trigger manuale, un trigger di ricorrenza o un trigger di poll.</span><span class="sxs-lookup"><span data-stu-id="11fa0-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="11fa0-121">È possibile che sia associato in genere allo stato **Attivato**, ma questo stato non viene visualizzato se in visualizzazione Codice è presente un valore SplitOn o una condizione non soddisfatta.</span><span class="sxs-lookup"><span data-stu-id="11fa0-121">This status is usually accompanied by the **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="11fa0-122">**Operazione non riuscita**.</span><span class="sxs-lookup"><span data-stu-id="11fa0-122">**Failed**.</span></span> <span data-ttu-id="11fa0-123">È stato generato un errore.</span><span class="sxs-lookup"><span data-stu-id="11fa0-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="11fa0-124">Avviare manualmente un trigger</span><span class="sxs-lookup"><span data-stu-id="11fa0-124">Start a trigger manually</span></span>

<span data-ttu-id="11fa0-125">Se si vuole che l'app per la logica verifichi immediatamente la presenza di un trigger disponibile, senza attendere la ricorrenza successiva, è possibile fare clic sul pulsante **Seleziona trigger** nel pannello principale per forzare un controllo.</span><span class="sxs-lookup"><span data-stu-id="11fa0-125">If you want the logic app to check for an available trigger immediately without waiting for the next recurrence, click **Select Trigger** on the main blade to force a check.</span></span> <span data-ttu-id="11fa0-126">Ad esempio, facendo clic su questo collegamento con un trigger di Dropbox, il flusso di lavoro esegue immediatamente il poll di Dropbox alla ricerca di nuovi file.</span><span class="sxs-lookup"><span data-stu-id="11fa0-126">For example, clicking this link with a Dropbox trigger causes the workflow to immediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="11fa0-127">Cronologia di esecuzione</span><span class="sxs-lookup"><span data-stu-id="11fa0-127">Run history</span></span>

<span data-ttu-id="11fa0-128">Ogni trigger attivato comporta un'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="11fa0-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="11fa0-129">Le informazioni sull'esecuzione sono accessibili dal pannello principale, che contiene numerose informazioni potenzialmente utili per capire cosa si è verificato durante il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="11fa0-129">You can access run information from the main blade, which contains many details that can help you understand what happened during the workflow.</span></span>

![Accedere alla cronologia di attivazione][2]

<span data-ttu-id="11fa0-131">Un'esecuzione può visualizzare uno dei seguenti stati:</span><span class="sxs-lookup"><span data-stu-id="11fa0-131">A run displays one of the following statuses:</span></span>

* <span data-ttu-id="11fa0-132">**Operazione completata**.</span><span class="sxs-lookup"><span data-stu-id="11fa0-132">**Succeeded**.</span></span> <span data-ttu-id="11fa0-133">Tutte le azioni hanno avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="11fa0-133">All actions succeeded.</span></span> <span data-ttu-id="11fa0-134">Se è stato generato un errore, questo è stato gestito da un'azione che si è verificata in un secondo momento nel flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="11fa0-134">If a failure happened, that failure was handled by an action that occurred later in the workflow.</span></span> <span data-ttu-id="11fa0-135">Vale a dire, l'errore è stato gestito da un'azione che è stata impostata per l'esecuzione dopo un'azione non riuscita.</span><span class="sxs-lookup"><span data-stu-id="11fa0-135">That is, the failure was handled by an action that was set to run after a failed action.</span></span>
* <span data-ttu-id="11fa0-136">**Operazione non riuscita**.</span><span class="sxs-lookup"><span data-stu-id="11fa0-136">**Failed**.</span></span> <span data-ttu-id="11fa0-137">Almeno un'azione presenta un errore non gestito da un'azione successiva nel flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="11fa0-137">At least one action had a failure that was not handled by an action later in the workflow.</span></span>
* <span data-ttu-id="11fa0-138">**Operazione annullata**.</span><span class="sxs-lookup"><span data-stu-id="11fa0-138">**Cancelled**.</span></span> <span data-ttu-id="11fa0-139">Il flusso di lavoro era in esecuzione ma ha ricevuto una richiesta di annullamento.</span><span class="sxs-lookup"><span data-stu-id="11fa0-139">The workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="11fa0-140">**In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="11fa0-140">**Running**.</span></span> <span data-ttu-id="11fa0-141">Il flusso di lavoro è attualmente in esecuzione,</span><span class="sxs-lookup"><span data-stu-id="11fa0-141">The workflow is currently running.</span></span> <span data-ttu-id="11fa0-142">ad esempio per flussi di lavoro limitati o a causa del piano tariffario corrente.</span><span class="sxs-lookup"><span data-stu-id="11fa0-142">This status might occur for throttled workflows, or because of the current pricing plan.</span></span> <span data-ttu-id="11fa0-143">Per i dettagli, vedere la [pagina relativa ai limiti di azione sui prezzi](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="11fa0-143">For details, see [action limits on the pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="11fa0-144">Inoltre, la configurazione della diagnostica (i grafici sotto la cronologia di esecuzione) possono fornire informazioni sugli eventuali eventi di limitazione in atto.</span><span class="sxs-lookup"><span data-stu-id="11fa0-144">Configuring diagnostics (the charts that appear under the run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="11fa0-145">Quando si analizza una cronologia di esecuzione, è possibile visualizzare ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="11fa0-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="11fa0-146">Output dei trigger</span><span class="sxs-lookup"><span data-stu-id="11fa0-146">Trigger outputs</span></span>

<span data-ttu-id="11fa0-147">Gli output dei trigger mostrano i dati ricevuti dal trigger.</span><span class="sxs-lookup"><span data-stu-id="11fa0-147">Trigger outputs show the data that came from the trigger.</span></span> <span data-ttu-id="11fa0-148">Questi output consentono di determinare se tutte le proprietà sono state restituite come previsto.</span><span class="sxs-lookup"><span data-stu-id="11fa0-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="11fa0-149">Se si notano contenuti poco chiari, potrebbe essere utile comprendere il modo in cui le App per la logica di Azure [gestiscono i diversi tipi di contenuto](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="11fa0-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Esempi di output di trigger][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="11fa0-151">Input e output delle azioni</span><span class="sxs-lookup"><span data-stu-id="11fa0-151">Action inputs and outputs</span></span>

<span data-ttu-id="11fa0-152">È possibile visualizzare informazioni dettagliate sugli input e sugli output ricevuti da un'azione,</span><span class="sxs-lookup"><span data-stu-id="11fa0-152">You can drill into the inputs and outputs that an action received.</span></span> <span data-ttu-id="11fa0-153">in modo da semplificare la comprensione delle dimensioni e delle forme degli output, oltre a cercare eventuali messaggi di errore generati.</span><span class="sxs-lookup"><span data-stu-id="11fa0-153">This data is useful for understanding the size and shape of the outputs, and also for finding any error messages that might have been generated.</span></span>

![Input e output delle azioni][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="11fa0-155">Debug del runtime del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="11fa0-155">Debug workflow runtime</span></span>

<span data-ttu-id="11fa0-156">Oltre al monitoraggio di input, output e trigger di un'esecuzione, potrebbe essere utile aggiungere alcuni passaggi a un flusso di lavoro per semplificare il debug.</span><span class="sxs-lookup"><span data-stu-id="11fa0-156">Along with monitoring the inputs, outputs, and triggers of a run, you could add some steps to a workflow that help with debugging.</span></span> 
<span data-ttu-id="11fa0-157">[RequestBin](http://requestb.in) è uno strumento utile che è possibile aggiungere come passaggio in un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="11fa0-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="11fa0-158">Utilizzando RequestBin, è possibile configurare un controllo per le richieste HTTP, in modo da stabilire esattamente le dimensioni, la forma e il formato di una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="11fa0-158">By using RequestBin, you can set up an HTTP request inspector to determine the exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="11fa0-159">È possibile creare un nuovo RequestBin e incollare l'URL in un'azione HTTP POST dell'app per la logica, con qualsiasi contenuto del corpo da verificare, ad esempio un'espressione o l'output di un altro passaggio.</span><span class="sxs-lookup"><span data-stu-id="11fa0-159">You can create a RequestBin and paste the URL in a logic app HTTP POST action with body content that you want to test, for example, an expression or another step output.</span></span> <span data-ttu-id="11fa0-160">Dopo l'esecuzione dell'app per la logica, è possibile aggiornare RequestBin per verificare in che modo è stata formata la richiesta durante la generazione dal motore di App per la logica.</span><span class="sxs-lookup"><span data-stu-id="11fa0-160">After you run the logic app, you can refresh your RequestBin to see how the request was formed when generated from the Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
