---
title: errori aaaDiagnose - App Azure per la logica | Documenti Microsoft
description: Comuni toounderstand modi in cui la logica App non sono stati superati
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
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="e487c-103">Eseguire una diagnosi degli errori delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="e487c-103">Diagnose logic app failures</span></span>
<span data-ttu-id="e487c-104">Se si verificano errori o problemi con le applicazioni di logica, esistono due approcci consentono di comprendere meglio provengano errori hello.</span><span class="sxs-lookup"><span data-stu-id="e487c-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where hello failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="e487c-105">Strumenti del portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e487c-105">Azure portal tools</span></span>
<span data-ttu-id="e487c-106">Hello portale di Azure fornisce molti strumenti toodiagnose ogni app per la logica in ogni fase.</span><span class="sxs-lookup"><span data-stu-id="e487c-106">hello Azure portal provides many tools toodiagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="e487c-107">Cronologia di attivazione</span><span class="sxs-lookup"><span data-stu-id="e487c-107">Trigger history</span></span>

<span data-ttu-id="e487c-108">Ogni app per la logica ha almeno un trigger.</span><span class="sxs-lookup"><span data-stu-id="e487c-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="e487c-109">Se si nota che non sono la generazione di applicazioni, cercare nella cronologia di trigger hello per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="e487c-109">If you notice that apps aren't firing, look first at hello trigger history for more information.</span></span> <span data-ttu-id="e487c-110">È possibile accedere a cronologia trigger hello nel pannello principale di hello logica app'ss.</span><span class="sxs-lookup"><span data-stu-id="e487c-110">You can access hello trigger history on hello logic app'ss main blade.</span></span>

![Individuazione cronologia trigger hello][1]

<span data-ttu-id="e487c-112">la cronologia di trigger Hello Elenca tutti i tentativi di trigger che ha effettuato l'app logica.</span><span class="sxs-lookup"><span data-stu-id="e487c-112">hello trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="e487c-113">È possibile fare clic su ogni toodrill tentativo trigger i dettagli di hello, in particolare, qualsiasi input o output di hello tentativo trigger generato.</span><span class="sxs-lookup"><span data-stu-id="e487c-113">You can click each trigger attempt toodrill into hello details, specifically, any inputs or outputs that hello trigger attempt generated.</span></span> <span data-ttu-id="e487c-114">Se si trova il trigger non riuscito, selezionare il tentativo di trigger hello e scegliere hello **output** collegamento tooreview qualsiasi errore generato i messaggi, ad esempio, per le credenziali FTP che non sono valide.</span><span class="sxs-lookup"><span data-stu-id="e487c-114">If you find failed triggers, select hello trigger attempt and choose hello **Outputs** link tooreview any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="e487c-115">potrebbe essere visualizzato in base ai diversi stati Hello sono:</span><span class="sxs-lookup"><span data-stu-id="e487c-115">hello different statuses you might see are:</span></span>

* <span data-ttu-id="e487c-116">**Operazione ignorata**.</span><span class="sxs-lookup"><span data-stu-id="e487c-116">**Skipped**.</span></span> <span data-ttu-id="e487c-117">endpoint Hello toocheck polling per i dati di stato e ha ricevuto una risposta che nessun dato è disponibile.</span><span class="sxs-lookup"><span data-stu-id="e487c-117">hello endpoint was polled toocheck for data and received a response that no data was available.</span></span>
* <span data-ttu-id="e487c-118">**Operazione completata**.</span><span class="sxs-lookup"><span data-stu-id="e487c-118">**Succeeded**.</span></span> <span data-ttu-id="e487c-119">trigger Hello ha ricevuto una risposta che dati non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="e487c-119">hello trigger received a response that data was available.</span></span> <span data-ttu-id="e487c-120">Questo può essere il risultato di un trigger manuale, un trigger di ricorrenza o un trigger di poll.</span><span class="sxs-lookup"><span data-stu-id="e487c-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="e487c-121">Questo stato è generalmente seguito da hello **generato** stato, ma potrebbe non essere la presenza di una condizione o un comando di SplitOn nella visualizzazione codice che non è stata soddisfatta.</span><span class="sxs-lookup"><span data-stu-id="e487c-121">This status is usually accompanied by hello **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="e487c-122">**Operazione non riuscita**.</span><span class="sxs-lookup"><span data-stu-id="e487c-122">**Failed**.</span></span> <span data-ttu-id="e487c-123">È stato generato un errore.</span><span class="sxs-lookup"><span data-stu-id="e487c-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="e487c-124">Avviare manualmente un trigger</span><span class="sxs-lookup"><span data-stu-id="e487c-124">Start a trigger manually</span></span>

<span data-ttu-id="e487c-125">Se si desidera hello logica app toocheck per un trigger disponibile immediatamente senza attendere l'occorrenza successiva di hello, fare clic su **selezionare Trigger** nel pannello principale di hello tooforce un segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="e487c-125">If you want hello logic app toocheck for an available trigger immediately without waiting for hello next recurrence, click **Select Trigger** on hello main blade tooforce a check.</span></span> <span data-ttu-id="e487c-126">Ad esempio, facendo clic su questo collegamento con un trigger di sincronizzazione determina hello del flusso di lavoro tooimmediately polling dell'area di sincronizzazione per i nuovi file.</span><span class="sxs-lookup"><span data-stu-id="e487c-126">For example, clicking this link with a Dropbox trigger causes hello workflow tooimmediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="e487c-127">Cronologia di esecuzione</span><span class="sxs-lookup"><span data-stu-id="e487c-127">Run history</span></span>

<span data-ttu-id="e487c-128">Ogni trigger attivato comporta un'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e487c-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="e487c-129">È possibile accedere a informazioni sull'esecuzione dal pannello principale hello, che contiene molti dettagli che aiutano a capire cosa è successo durante il flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="e487c-129">You can access run information from hello main blade, which contains many details that can help you understand what happened during hello workflow.</span></span>

![Individuazione hello cronologia di esecuzione][2]

<span data-ttu-id="e487c-131">Un'esecuzione viene visualizzato uno dei seguenti stati hello:</span><span class="sxs-lookup"><span data-stu-id="e487c-131">A run displays one of hello following statuses:</span></span>

* <span data-ttu-id="e487c-132">**Operazione completata**.</span><span class="sxs-lookup"><span data-stu-id="e487c-132">**Succeeded**.</span></span> <span data-ttu-id="e487c-133">Tutte le azioni hanno avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="e487c-133">All actions succeeded.</span></span> <span data-ttu-id="e487c-134">Se si è verificato un errore, tale errore è stato gestito da un'azione che si è verificato in un secondo momento nel flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="e487c-134">If a failure happened, that failure was handled by an action that occurred later in hello workflow.</span></span> <span data-ttu-id="e487c-135">Errore di hello, ovvero è stato gestito da un'azione che è stata impostata toorun dopo un'azione non riuscita.</span><span class="sxs-lookup"><span data-stu-id="e487c-135">That is, hello failure was handled by an action that was set toorun after a failed action.</span></span>
* <span data-ttu-id="e487c-136">**Operazione non riuscita**.</span><span class="sxs-lookup"><span data-stu-id="e487c-136">**Failed**.</span></span> <span data-ttu-id="e487c-137">Almeno un'azione ha esito negativo che non è stata gestita da un'azione nel flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="e487c-137">At least one action had a failure that was not handled by an action later in hello workflow.</span></span>
* <span data-ttu-id="e487c-138">**Operazione annullata**.</span><span class="sxs-lookup"><span data-stu-id="e487c-138">**Cancelled**.</span></span> <span data-ttu-id="e487c-139">flusso di lavoro Hello era in esecuzione ma ha ricevuto una richiesta di annullamento.</span><span class="sxs-lookup"><span data-stu-id="e487c-139">hello workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="e487c-140">**In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="e487c-140">**Running**.</span></span> <span data-ttu-id="e487c-141">flusso di lavoro Hello è attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e487c-141">hello workflow is currently running.</span></span> <span data-ttu-id="e487c-142">Questo stato può verificarsi per i flussi di lavoro limitate, o a causa di hello prezzi piano corrente.</span><span class="sxs-lookup"><span data-stu-id="e487c-142">This status might occur for throttled workflows, or because of hello current pricing plan.</span></span> <span data-ttu-id="e487c-143">Per informazioni dettagliate, vedere [i limiti di azione nella pagina relativa ai prezzi hello](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="e487c-143">For details, see [action limits on hello pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="e487c-144">Configurazione della diagnostica (grafici hello che vengono visualizzati nella cronologia di esecuzione hello) inoltre possibile fornire informazioni su tutti gli eventi di limitazione che si verificano.</span><span class="sxs-lookup"><span data-stu-id="e487c-144">Configuring diagnostics (hello charts that appear under hello run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="e487c-145">Quando si analizza una cronologia di esecuzione, è possibile visualizzare ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="e487c-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="e487c-146">Output dei trigger</span><span class="sxs-lookup"><span data-stu-id="e487c-146">Trigger outputs</span></span>

<span data-ttu-id="e487c-147">Trigger genera Mostra hello i dati provenienti da trigger hello.</span><span class="sxs-lookup"><span data-stu-id="e487c-147">Trigger outputs show hello data that came from hello trigger.</span></span> <span data-ttu-id="e487c-148">Questi output consentono di determinare se tutte le proprietà sono state restituite come previsto.</span><span class="sxs-lookup"><span data-stu-id="e487c-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="e487c-149">Se si notano contenuti poco chiari, potrebbe essere utile comprendere il modo in cui le App per la logica di Azure [gestiscono i diversi tipi di contenuto](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="e487c-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Esempi di output di trigger][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="e487c-151">Input e output delle azioni</span><span class="sxs-lookup"><span data-stu-id="e487c-151">Action inputs and outputs</span></span>

<span data-ttu-id="e487c-152">È possibile analizzare hello input e output che ha ricevuta un'azione.</span><span class="sxs-lookup"><span data-stu-id="e487c-152">You can drill into hello inputs and outputs that an action received.</span></span> <span data-ttu-id="e487c-153">Questi dati sono utili per comprendere hello dimensioni e la forma di output di hello, nonché per individuare eventuali messaggi di errore che potrebbero essere stati generati.</span><span class="sxs-lookup"><span data-stu-id="e487c-153">This data is useful for understanding hello size and shape of hello outputs, and also for finding any error messages that might have been generated.</span></span>

![Input e output delle azioni][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="e487c-155">Debug del runtime del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="e487c-155">Debug workflow runtime</span></span>

<span data-ttu-id="e487c-156">Insieme a monitoraggio hello input, output e i trigger di un'esecuzione, è possibile aggiungere alcuni passaggi tooa del flusso di lavoro che consentono il debug.</span><span class="sxs-lookup"><span data-stu-id="e487c-156">Along with monitoring hello inputs, outputs, and triggers of a run, you could add some steps tooa workflow that help with debugging.</span></span> 
<span data-ttu-id="e487c-157">[RequestBin](http://requestb.in) è uno strumento utile che è possibile aggiungere come passaggio in un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e487c-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="e487c-158">Se si utilizza RequestBin, è possibile impostare un controllo toodetermine hello esatta dimensione della richiesta HTTP, forma e formato di una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="e487c-158">By using RequestBin, you can set up an HTTP request inspector toodetermine hello exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="e487c-159">È possibile creare un RequestBin e incollare l'URL di hello in un'app di logica di azione HTTP POST con il contenuto del corpo che si desidera tootest, ad esempio, un'espressione o un altro output di passaggio.</span><span class="sxs-lookup"><span data-stu-id="e487c-159">You can create a RequestBin and paste hello URL in a logic app HTTP POST action with body content that you want tootest, for example, an expression or another step output.</span></span> <span data-ttu-id="e487c-160">Dopo aver eseguito hello logica app, è possibile aggiornare il toosee RequestBin come richiesta hello valido quando generati dal motore di App per la logica di hello.</span><span class="sxs-lookup"><span data-stu-id="e487c-160">After you run hello logic app, you can refresh your RequestBin toosee how hello request was formed when generated from hello Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
