---
title: "Aggiornamenti dello schema del 1° giugno 2016 - App per la logica di Azure | Microsoft Docs"
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
ms.openlocfilehash: 43df04d6478e44c82c88b17d916cfc9fe4afc03e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="7601a-103">Aggiornamenti dello schema per App per la logica di Azure: 1° giugno 2016</span><span class="sxs-lookup"><span data-stu-id="7601a-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="7601a-104">La nuova versione dello schema e dell'API per App per la logica di Azure include importanti miglioramenti che rendono le app per la logica più affidabili e facili da usare:</span><span class="sxs-lookup"><span data-stu-id="7601a-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

* <span data-ttu-id="7601a-105">Gli [ambiti](#scopes) consentono di raggruppare o annidare le azioni come una raccolta di azioni.</span><span class="sxs-lookup"><span data-stu-id="7601a-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="7601a-106">[Condizioni e cicli](#conditions-loops) sono ora azioni di prima classe.</span><span class="sxs-lookup"><span data-stu-id="7601a-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="7601a-107">La proprietà `runAfter`, che sostituisce `dependsOn`, consente di ordinare con maggiore precisione l'esecuzione delle azioni.</span><span class="sxs-lookup"><span data-stu-id="7601a-107">More precise ordering for running actions with the `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="7601a-108">Per aggiornare le app per la logica dallo schema di anteprima del 1° agosto 2015 allo schema del 1° giugno 2016, [vedere la sezione relativa all'aggiornamento](##upgrade-your-schema).</span><span class="sxs-lookup"><span data-stu-id="7601a-108">To upgrade your logic apps from the August 1, 2015 preview schema to the June 1, 2016 schema, [check out the upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="7601a-109">Ambiti</span><span class="sxs-lookup"><span data-stu-id="7601a-109">Scopes</span></span>

<span data-ttu-id="7601a-110">Questo schema include gli ambiti, che consentono di raggruppare le azioni o annidarle all'interno di altre.</span><span class="sxs-lookup"><span data-stu-id="7601a-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="7601a-111">Una condizione, ad esempio, può contenere un'altra condizione.</span><span class="sxs-lookup"><span data-stu-id="7601a-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="7601a-112">Vedere altre informazioni sulla [sintassi degli ambiti](../logic-apps/logic-apps-loops-and-scopes.md) oppure esaminare questo esempio di ambito di base:</span><span class="sxs-lookup"><span data-stu-id="7601a-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

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
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="7601a-113">Modifiche di condizioni e cicli</span><span class="sxs-lookup"><span data-stu-id="7601a-113">Conditions and loops changes</span></span>

<span data-ttu-id="7601a-114">Nelle versioni precedenti dello schema, le condizioni e i cicli sono parametri associati a una singola azione.</span><span class="sxs-lookup"><span data-stu-id="7601a-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="7601a-115">In questo schema è stata rimossa questa limitazione e le condizioni e i cicli sono disponibili come tipi di azione.</span><span class="sxs-lookup"><span data-stu-id="7601a-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="7601a-116">Vedere altre informazioni su [cicli e ambiti](../logic-apps/logic-apps-loops-and-scopes.md) oppure esaminare questo esempio di base di un'azione condizione:</span><span class="sxs-lookup"><span data-stu-id="7601a-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

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
## <a name="runafter-property"></a><span data-ttu-id="7601a-117">Proprietà "runAfter"</span><span class="sxs-lookup"><span data-stu-id="7601a-117">'runAfter' property</span></span>

<span data-ttu-id="7601a-118">La proprietà `runAfter` sostituisce `dependsOn`, offrendo maggiore precisione quando si specifica l'ordine di esecuzione delle azioni in base allo stato di azioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="7601a-118">The `runAfter` property replaces `dependsOn`, providing more precision when you specify the run order for actions based on the status of previous actions.</span></span>

<span data-ttu-id="7601a-119">La proprietà `dependsOn` indica l'esecuzione riuscita dell'azione, indipendentemente dal numero di volte che si vuole eseguire un'azione a seconda che la precedente sia riuscita, abbia avuto esito negativo o sia stata ignorata.</span><span class="sxs-lookup"><span data-stu-id="7601a-119">The `dependsOn` property was synonymous with "the action ran and was successful", no matter how many times you wanted to execute an action, based on whether the previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="7601a-120">La proprietà `runAfter` offre tale flessibilità in quanto oggetto che specifica tutti nomi delle azioni dopo cui viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="7601a-120">The `runAfter` property provides that flexibility as an object that specifies all the action names after which the object runs.</span></span> <span data-ttu-id="7601a-121">Questa proprietà definisce anche una matrice degli stati accettabili come trigger.</span><span class="sxs-lookup"><span data-stu-id="7601a-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="7601a-122">Per impostare l'esecuzione dopo l'esito positivo del passaggio A e dopo l'esito positivo o negativo del passaggio B, ad esempio, si costruisce questa proprietà `runAfter`:</span><span class="sxs-lookup"><span data-stu-id="7601a-122">For example, if you wanted to run after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="7601a-123">Aggiornare lo schema</span><span class="sxs-lookup"><span data-stu-id="7601a-123">Upgrade your schema</span></span>

<span data-ttu-id="7601a-124">L'aggiornamento al nuovo schema richiede pochi passaggi.</span><span class="sxs-lookup"><span data-stu-id="7601a-124">Upgrading to the new schema only takes a few steps.</span></span> <span data-ttu-id="7601a-125">Il processo di aggiornamento include l'esecuzione dello script di aggiornamento, il salvataggio come nuova app per la logica ed eventualmente, se necessario, la sovrascrittura dell'app per la logica precedente.</span><span class="sxs-lookup"><span data-stu-id="7601a-125">The upgrade process includes running the upgrade script, saving as a new logic app, and if you want, possibly overwriting the previous logic app.</span></span>

1. <span data-ttu-id="7601a-126">Nel portale di Azure aprire l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="7601a-126">In the Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="7601a-127">Passare a **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="7601a-127">Go to **Overview**.</span></span> <span data-ttu-id="7601a-128">Sulla barra degli strumenti dell'app per la logica scegliere **Aggiorna schema**.</span><span class="sxs-lookup"><span data-stu-id="7601a-128">On the logic app toolbar, choose **Update Schema**.</span></span>
   
    ![Scegliere Aggiorna schema][1]
   
    <span data-ttu-id="7601a-130">Verrà restituita la definizione aggiornata, che è possibile copiare e incollare in una definizione di risorsa, se necessario.</span><span class="sxs-lookup"><span data-stu-id="7601a-130">The upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="7601a-131">È tuttavia **altamente consigliabile** scegliere **Salva con nome** per assicurarsi che tutti i riferimenti alla connessione siano validi nell'app per la logica aggiornata.</span><span class="sxs-lookup"><span data-stu-id="7601a-131">However, we **strongly recommend** you choose **Save As** to make sure that all connection references are valid in the upgraded logic app.</span></span>

3. <span data-ttu-id="7601a-132">Sulla barra degli strumenti del pannello per l'aggiornamento scegliere **Salva con nome**.</span><span class="sxs-lookup"><span data-stu-id="7601a-132">In the upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="7601a-133">Immettere il nome logico e lo stato.</span><span class="sxs-lookup"><span data-stu-id="7601a-133">Enter the logic name and status.</span></span> <span data-ttu-id="7601a-134">Per distribuire l'app per la logica aggiornata, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7601a-134">To deploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="7601a-135">Verificare che l'app per la logica aggiornata funzioni come previsto.</span><span class="sxs-lookup"><span data-stu-id="7601a-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7601a-136">Se si usa un trigger manuale o di richiesta, l'URL di callback viene modificato nella nuova app per la logica.</span><span class="sxs-lookup"><span data-stu-id="7601a-136">If you are using a manual or request trigger, the callback URL changes in your new logic app.</span></span> <span data-ttu-id="7601a-137">Testare il nuovo URL per verificare il funzionamento dell'esperienza end-to-end.</span><span class="sxs-lookup"><span data-stu-id="7601a-137">Test the new URL to make sure the end-to-end experience works.</span></span> <span data-ttu-id="7601a-138">Per mantenere gli URL precedenti, è possibile clonare l'app per la logica esistente.</span><span class="sxs-lookup"><span data-stu-id="7601a-138">To preserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="7601a-139">*Facoltativo* Per sovrascrivere l'app per la logica precedente con la nuova versione dello schema, sulla barra degli strumenti scegliere **Clona** accanto ad **Aggiorna schema**.</span><span class="sxs-lookup"><span data-stu-id="7601a-139">*Optional* To overwrite your previous logic app with the new schema version, on the toolbar, choose **Clone**, next to **Update Schema**.</span></span> <span data-ttu-id="7601a-140">Questo passaggio è necessario solo se si vuole mantenere lo stesso ID risorsa o lo stesso URL del trigger di richiesta dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="7601a-140">This step is necessary only if you want to keep the same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="7601a-141">Note sullo strumento di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="7601a-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="7601a-142">Mapping delle condizioni</span><span class="sxs-lookup"><span data-stu-id="7601a-142">Mapping conditions</span></span>

<span data-ttu-id="7601a-143">Nella definizione aggiornata, lo strumento tenta di raggruppare le azioni dei rami true e false in un ambito.</span><span class="sxs-lookup"><span data-stu-id="7601a-143">In the upgraded definition, the tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="7601a-144">In particolare, il modello di progettazione `@equals(actions('a').status, 'Skipped')` verrà visualizzato come un'azione `else`.</span><span class="sxs-lookup"><span data-stu-id="7601a-144">Specifically, the designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="7601a-145">Se lo strumento rileva modelli non riconoscibili, tuttavia, potrebbe creare condizioni separate per i rami true e false.</span><span class="sxs-lookup"><span data-stu-id="7601a-145">However, if the tool detects unrecognizable patterns, the tool might create separate conditions for both the true and the false branch.</span></span> <span data-ttu-id="7601a-146">Se necessario, è possibile modificare il mapping delle azioni dopo l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="7601a-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="7601a-147">Ciclo "foreach" con condizione</span><span class="sxs-lookup"><span data-stu-id="7601a-147">'foreach' loop with condition</span></span>

<span data-ttu-id="7601a-148">Nel nuovo schema, è possibile usare l'azione di filtro per replicare il modello di un ciclo `foreach` con una condizione per elemento, ma questa modifica dovrebbe essere eseguita automaticamente durante l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="7601a-148">In the new schema, you can use the filter action to replicate the pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="7601a-149">La condizione diventa un'azione di filtro prima del ciclo foreach per restituire solo una matrice di elementi che soddisfano la condizione e tale matrice viene passata nell'azione foreach.</span><span class="sxs-lookup"><span data-stu-id="7601a-149">The condition becomes a filter action before the foreach loop for returning only an array of items that match the condition, and that array is passed into the foreach action.</span></span> <span data-ttu-id="7601a-150">Per un esempio, vedere l'articolo relativo a [cicli e ambiti](../logic-apps/logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="7601a-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="7601a-151">Tag delle risorse</span><span class="sxs-lookup"><span data-stu-id="7601a-151">Resource tags</span></span>

<span data-ttu-id="7601a-152">Dopo l'aggiornamento, i tag delle risorse vengono rimossi. È quindi necessario reimpostarli per il flusso di lavoro aggiornato.</span><span class="sxs-lookup"><span data-stu-id="7601a-152">After you upgrade, resource tags are removed, so you must reset them for the upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="7601a-153">Altre modifiche</span><span class="sxs-lookup"><span data-stu-id="7601a-153">Other changes</span></span>

### <a name="renamed-manual-trigger-to-request-trigger"></a><span data-ttu-id="7601a-154">Ridenominazione del trigger "manual" in "request"</span><span class="sxs-lookup"><span data-stu-id="7601a-154">Renamed 'manual' trigger to 'request' trigger</span></span>

<span data-ttu-id="7601a-155">Il tipo di trigger `manual` è deprecato ed è stato rinominato `request` con tipo `http`.</span><span class="sxs-lookup"><span data-stu-id="7601a-155">The `manual` trigger type was deprecated and renamed to `request` with type `http`.</span></span> <span data-ttu-id="7601a-156">Questa modifica offre maggiore coerenza per la tipologia di modello creata con il trigger.</span><span class="sxs-lookup"><span data-stu-id="7601a-156">This change creates more consistency for the kind of pattern that the trigger is used to build.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="7601a-157">Nuova azione "filtro"</span><span class="sxs-lookup"><span data-stu-id="7601a-157">New 'filter' action</span></span>

<span data-ttu-id="7601a-158">Per filtrare una matrice di grandi dimensioni in modo da ottenere un set ridotto di elementi, il nuovo tipo `filter` accetta una matrice e una condizione, valuta la condizione per ogni elemento e restituisce una matrice con gli elementi che soddisfano la condizione.</span><span class="sxs-lookup"><span data-stu-id="7601a-158">To filter a large array down to a smaller set of items, the new `filter` type accepts an array and a condition, evaluates the condition for each item, and returns an array with items meeting the condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="7601a-159">Restrizioni per le azioni "foreach" e "until"</span><span class="sxs-lookup"><span data-stu-id="7601a-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="7601a-160">I cicli `foreach` e `until` sono limitati a una singola azione.</span><span class="sxs-lookup"><span data-stu-id="7601a-160">The `foreach` and `until` loop are restricted to a single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="7601a-161">Nuova proprietà "trackedProperties" per le azioni</span><span class="sxs-lookup"><span data-stu-id="7601a-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="7601a-162">Le azioni possono ora includere una proprietà aggiuntiva denominata `trackedProperties`, di pari livello rispetto alle proprietà `runAfter` e `type`.</span><span class="sxs-lookup"><span data-stu-id="7601a-162">Actions can now have an additional property called `trackedProperties`, which is sibling to the `runAfter` and `type` properties.</span></span> <span data-ttu-id="7601a-163">Questo oggetto specifica determinati input o output delle azioni da includere nei dati di telemetria di Diagnostica di Azure generati come parte di un flusso di lavoro,</span><span class="sxs-lookup"><span data-stu-id="7601a-163">This object specifies certain action inputs or outputs that you want to include in the Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="7601a-164">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7601a-164">For example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7601a-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7601a-165">Next Steps</span></span>
* [<span data-ttu-id="7601a-166">Creare definizioni dei flussi di lavoro per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="7601a-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="7601a-167">Creare modelli di distribuzione per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="7601a-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
