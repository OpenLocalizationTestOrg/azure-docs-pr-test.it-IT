---
title: aaaSchema Aggiorna 2016 - 1 giugno Azure logica App | Documenti Microsoft
description: Creare definizioni JSON per App per la logica di Azure con la versione dello schema 2016-06-01
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: b0347fbbd692a93b63a2f8b741402a225450b35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="87dc5-103">Aggiornamenti dello schema per App per la logica di Azure: 1° giugno 2016</span><span class="sxs-lookup"><span data-stu-id="87dc5-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="87dc5-104">Questo nuovo schema e l'API di versione per App di logica di Azure include importanti miglioramenti che App per la logica di rendere più affidabile e facile toouse:</span><span class="sxs-lookup"><span data-stu-id="87dc5-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

* <span data-ttu-id="87dc5-105">Gli [ambiti](#scopes) consentono di raggruppare o annidare le azioni come una raccolta di azioni.</span><span class="sxs-lookup"><span data-stu-id="87dc5-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="87dc5-106">[Condizioni e cicli](#conditions-loops) sono ora azioni di prima classe.</span><span class="sxs-lookup"><span data-stu-id="87dc5-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="87dc5-107">Ordinamento più preciso per l'esecuzione di azioni con hello `runAfter` proprietà, la sostituzione`dependsOn`</span><span class="sxs-lookup"><span data-stu-id="87dc5-107">More precise ordering for running actions with hello `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="87dc5-108">schema XML schema toohello 1 giugno 2016, visualizzare in anteprima tooupgrade App per la logica di hello 1 agosto 2015 [estrarre sezione aggiornamento hello](##upgrade-your-schema).</span><span class="sxs-lookup"><span data-stu-id="87dc5-108">tooupgrade your logic apps from hello August 1, 2015 preview schema toohello June 1, 2016 schema, [check out hello upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="87dc5-109">Ambiti</span><span class="sxs-lookup"><span data-stu-id="87dc5-109">Scopes</span></span>

<span data-ttu-id="87dc5-110">Questo schema include gli ambiti, che consentono di raggruppare le azioni o annidarle all'interno di altre.</span><span class="sxs-lookup"><span data-stu-id="87dc5-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="87dc5-111">Una condizione, ad esempio, può contenere un'altra condizione.</span><span class="sxs-lookup"><span data-stu-id="87dc5-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="87dc5-112">Vedere altre informazioni sulla [sintassi degli ambiti](../logic-apps/logic-apps-loops-and-scopes.md) oppure esaminare questo esempio di ambito di base:</span><span class="sxs-lookup"><span data-stu-id="87dc5-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="87dc5-113">Modifiche di condizioni e cicli</span><span class="sxs-lookup"><span data-stu-id="87dc5-113">Conditions and loops changes</span></span>

<span data-ttu-id="87dc5-114">Nelle versioni precedenti dello schema, le condizioni e i cicli sono parametri associati a una singola azione.</span><span class="sxs-lookup"><span data-stu-id="87dc5-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="87dc5-115">In questo schema è stata rimossa questa limitazione e le condizioni e i cicli sono disponibili come tipi di azione.</span><span class="sxs-lookup"><span data-stu-id="87dc5-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="87dc5-116">Vedere altre informazioni su [cicli e ambiti](../logic-apps/logic-apps-loops-and-scopes.md) oppure esaminare questo esempio di base di un'azione condizione:</span><span class="sxs-lookup"><span data-stu-id="87dc5-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a><span data-ttu-id="87dc5-117">Proprietà "runAfter"</span><span class="sxs-lookup"><span data-stu-id="87dc5-117">'runAfter' property</span></span>

<span data-ttu-id="87dc5-118">Hello `runAfter` sostituisce proprietà `dependsOn`, fornisce maggiore precisione quando si specifica l'ordine di esecuzione hello per le azioni in base allo stato di hello delle azioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="87dc5-118">hello `runAfter` property replaces `dependsOn`, providing more precision when you specify hello run order for actions based on hello status of previous actions.</span></span>

<span data-ttu-id="87dc5-119">Hello `dependsOn` proprietà è un sinonimo di azione hello eseguito "e" è stata eseguita correttamente, indipendentemente da quante volte si desiderava tooexecute un'azione, in base alle azioni di hello precedente è stata eseguita, non è riuscita o ignorato.</span><span class="sxs-lookup"><span data-stu-id="87dc5-119">hello `dependsOn` property was synonymous with "hello action ran and was successful", no matter how many times you wanted tooexecute an action, based on whether hello previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="87dc5-120">Hello `runAfter` proprietà flessibilità che un oggetto che specifica tutti hello dopo cui hello oggetto esegue i nomi di azione.</span><span class="sxs-lookup"><span data-stu-id="87dc5-120">hello `runAfter` property provides that flexibility as an object that specifies all hello action names after which hello object runs.</span></span> <span data-ttu-id="87dc5-121">Questa proprietà definisce anche una matrice degli stati accettabili come trigger.</span><span class="sxs-lookup"><span data-stu-id="87dc5-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="87dc5-122">Ad esempio, se si desidera toorun dopo un passaggio ha esito positivo e anche dopo passaggio B ha esito positivo o negativo, costruire questo `runAfter` proprietà:</span><span class="sxs-lookup"><span data-stu-id="87dc5-122">For example, if you wanted toorun after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="87dc5-123">Aggiornare lo schema</span><span class="sxs-lookup"><span data-stu-id="87dc5-123">Upgrade your schema</span></span>

<span data-ttu-id="87dc5-124">Aggiornamento toohello nuovo schema richiede solo pochi passaggi.</span><span class="sxs-lookup"><span data-stu-id="87dc5-124">Upgrading toohello new schema only takes a few steps.</span></span> <span data-ttu-id="87dc5-125">Hello processo di aggiornamento include l'esecuzione dello script di aggiornamento hello, salvataggio come una nuova app per la logica e, se si desidera, eventualmente sovrascrivendo hello precedente logica app.</span><span class="sxs-lookup"><span data-stu-id="87dc5-125">hello upgrade process includes running hello upgrade script, saving as a new logic app, and if you want, possibly overwriting hello previous logic app.</span></span>

1. <span data-ttu-id="87dc5-126">Nel portale di Azure hello, Apri l'app logica.</span><span class="sxs-lookup"><span data-stu-id="87dc5-126">In hello Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="87dc5-127">Andare troppo**Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="87dc5-127">Go too**Overview**.</span></span> <span data-ttu-id="87dc5-128">Sulla barra degli strumenti applicazione hello logica, scegliere **Aggiorna Schema**.</span><span class="sxs-lookup"><span data-stu-id="87dc5-128">On hello logic app toolbar, choose **Update Schema**.</span></span>
   
    ![Scegliere Aggiorna schema][1]
   
    <span data-ttu-id="87dc5-130">Hello definizione aggiornata viene restituito, che è possibile copiare e incollare in una definizione di risorsa, se necessario.</span><span class="sxs-lookup"><span data-stu-id="87dc5-130">hello upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="87dc5-131">Tuttavia, si **consigliabile** si sceglie **Salva con nome** toomake assicurarsi che tutti i riferimenti di connessione siano validi in hello aggiornato logica app.</span><span class="sxs-lookup"><span data-stu-id="87dc5-131">However, we **strongly recommend** you choose **Save As** toomake sure that all connection references are valid in hello upgraded logic app.</span></span>

3. <span data-ttu-id="87dc5-132">Nella barra strumenti del Pannello di aggiornamento hello scegliere **Salva con nome**.</span><span class="sxs-lookup"><span data-stu-id="87dc5-132">In hello upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="87dc5-133">Immettere il nome di logica hello e di stato.</span><span class="sxs-lookup"><span data-stu-id="87dc5-133">Enter hello logic name and status.</span></span> <span data-ttu-id="87dc5-134">toodeploy app logica aggiornato, scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="87dc5-134">toodeploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="87dc5-135">Verificare che l'app per la logica aggiornata funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="87dc5-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="87dc5-136">Se si utilizza un trigger manuale o richiesta, URL callback hello cambia nell'app nuova logica.</span><span class="sxs-lookup"><span data-stu-id="87dc5-136">If you are using a manual or request trigger, hello callback URL changes in your new logic app.</span></span> <span data-ttu-id="87dc5-137">Esperienza di test hello nuovo URL toomake che hello end-to-end.</span><span class="sxs-lookup"><span data-stu-id="87dc5-137">Test hello new URL toomake sure hello end-to-end experience works.</span></span> <span data-ttu-id="87dc5-138">toopreserve URL precedenti, è possibile clonare tramite l'app logica esistente.</span><span class="sxs-lookup"><span data-stu-id="87dc5-138">toopreserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="87dc5-139">*Parametro facoltativo* toooverwrite app logica precedente con hello nuova versione dello schema, sulla barra degli strumenti hello, scegliere **Clone**, accanto troppo**Aggiorna Schema**.</span><span class="sxs-lookup"><span data-stu-id="87dc5-139">*Optional* toooverwrite your previous logic app with hello new schema version, on hello toolbar, choose **Clone**, next too**Update Schema**.</span></span> <span data-ttu-id="87dc5-140">Questo passaggio è necessario solo se si desidera tookeep hello stessa risorsa ID richiesta trigger URL o dell'app logica.</span><span class="sxs-lookup"><span data-stu-id="87dc5-140">This step is necessary only if you want tookeep hello same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="87dc5-141">Note sullo strumento di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="87dc5-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="87dc5-142">Mapping delle condizioni</span><span class="sxs-lookup"><span data-stu-id="87dc5-142">Mapping conditions</span></span>

<span data-ttu-id="87dc5-143">Nella definizione di hello aggiornato, strumento di hello rende tentativi al raggruppamento delle azioni branch true e false come ambito.</span><span class="sxs-lookup"><span data-stu-id="87dc5-143">In hello upgraded definition, hello tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="87dc5-144">In particolare, hello progettazione modello di `@equals(actions('a').status, 'Skipped')` dovrebbe essere visualizzato come un `else` azione.</span><span class="sxs-lookup"><span data-stu-id="87dc5-144">Specifically, hello designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="87dc5-145">Tuttavia, se lo strumento hello rileva modelli non riconoscibile, strumento hello potrebbe creare condizioni distinte per true hello e branch false hello.</span><span class="sxs-lookup"><span data-stu-id="87dc5-145">However, if hello tool detects unrecognizable patterns, hello tool might create separate conditions for both hello true and hello false branch.</span></span> <span data-ttu-id="87dc5-146">Se necessario, è possibile modificare il mapping delle azioni dopo l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="87dc5-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="87dc5-147">Ciclo "foreach" con condizione</span><span class="sxs-lookup"><span data-stu-id="87dc5-147">'foreach' loop with condition</span></span>

<span data-ttu-id="87dc5-148">Nel nuovo schema hello, è possibile utilizzare il modello hello filtro azione tooreplicate hello di un `foreach` ciclo con una condizione per ogni elemento, ma questa modifica dovrebbe verificarsi automaticamente quando esegue l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="87dc5-148">In hello new schema, you can use hello filter action tooreplicate hello pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="87dc5-149">condizione Hello diventa un'operazione di filtro prima di ciclo foreach hello per la restituzione solo di una matrice di elementi che corrispondono alla condizione hello e tale matrice viene passata in azione foreach hello.</span><span class="sxs-lookup"><span data-stu-id="87dc5-149">hello condition becomes a filter action before hello foreach loop for returning only an array of items that match hello condition, and that array is passed into hello foreach action.</span></span> <span data-ttu-id="87dc5-150">Per un esempio, vedere l'articolo relativo a [cicli e ambiti](../logic-apps/logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="87dc5-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="87dc5-151">Tag delle risorse</span><span class="sxs-lookup"><span data-stu-id="87dc5-151">Resource tags</span></span>

<span data-ttu-id="87dc5-152">Dopo l'aggiornamento, vengono rimossi i tag delle risorse, pertanto è necessario reimpostarli per flusso di lavoro hello aggiornato.</span><span class="sxs-lookup"><span data-stu-id="87dc5-152">After you upgrade, resource tags are removed, so you must reset them for hello upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="87dc5-153">Altre modifiche</span><span class="sxs-lookup"><span data-stu-id="87dc5-153">Other changes</span></span>

### <a name="renamed-manual-trigger-toorequest-trigger"></a><span data-ttu-id="87dc5-154">Rinominare il trigger 'manual' too'request' trigger</span><span class="sxs-lookup"><span data-stu-id="87dc5-154">Renamed 'manual' trigger too'request' trigger</span></span>

<span data-ttu-id="87dc5-155">Hello `manual` tipo di trigger è stato deprecato e rinominato troppo`request` con tipo `http`.</span><span class="sxs-lookup"><span data-stu-id="87dc5-155">hello `manual` trigger type was deprecated and renamed too`request` with type `http`.</span></span> <span data-ttu-id="87dc5-156">Questa modifica crea maggiore coerenza per il tipo di hello di pattern che hello trigger è toobuild utilizzato.</span><span class="sxs-lookup"><span data-stu-id="87dc5-156">This change creates more consistency for hello kind of pattern that hello trigger is used toobuild.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="87dc5-157">Nuova azione "filtro"</span><span class="sxs-lookup"><span data-stu-id="87dc5-157">New 'filter' action</span></span>

<span data-ttu-id="87dc5-158">una matrice di grandi dimensioni verso il basso tooa ridurre il numero di elementi, hello nuovi toofilter `filter` tipo accetta una matrice e una condizione, valuta la condizione hello per ogni elemento e restituisce una matrice con gli elementi che soddisfano la condizione hello.</span><span class="sxs-lookup"><span data-stu-id="87dc5-158">toofilter a large array down tooa smaller set of items, hello new `filter` type accepts an array and a condition, evaluates hello condition for each item, and returns an array with items meeting hello condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="87dc5-159">Restrizioni per le azioni "foreach" e "until"</span><span class="sxs-lookup"><span data-stu-id="87dc5-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="87dc5-160">Hello `foreach` e `until` ciclo sono limitate tooa singola azione.</span><span class="sxs-lookup"><span data-stu-id="87dc5-160">hello `foreach` and `until` loop are restricted tooa single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="87dc5-161">Nuova proprietà "trackedProperties" per le azioni</span><span class="sxs-lookup"><span data-stu-id="87dc5-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="87dc5-162">Azioni ora possono avere una proprietà aggiuntiva chiamata `trackedProperties`, che è l'elemento di pari livello toohello `runAfter` e `type` proprietà.</span><span class="sxs-lookup"><span data-stu-id="87dc5-162">Actions can now have an additional property called `trackedProperties`, which is sibling toohello `runAfter` and `type` properties.</span></span> <span data-ttu-id="87dc5-163">Questo oggetto consente di specificare alcuni input azione o l'output che si desidera tooinclude in telemetria di diagnostica di Azure hello, generata come parte di un flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="87dc5-163">This object specifies certain action inputs or outputs that you want tooinclude in hello Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="87dc5-164">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="87dc5-164">For example:</span></span>

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="87dc5-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="87dc5-165">Next Steps</span></span>
* [<span data-ttu-id="87dc5-166">Creare definizioni dei flussi di lavoro per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="87dc5-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="87dc5-167">Creare modelli di distribuzione per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="87dc5-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
