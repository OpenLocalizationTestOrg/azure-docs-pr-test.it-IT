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
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a>Aggiornamenti dello schema per App per la logica di Azure: 1° giugno 2016

Questo nuovo schema e l'API di versione per App di logica di Azure include importanti miglioramenti che App per la logica di rendere più affidabile e facile toouse:

* Gli [ambiti](#scopes) consentono di raggruppare o annidare le azioni come una raccolta di azioni.
* [Condizioni e cicli](#conditions-loops) sono ora azioni di prima classe.
* Ordinamento più preciso per l'esecuzione di azioni con hello `runAfter` proprietà, la sostituzione`dependsOn`

schema XML schema toohello 1 giugno 2016, visualizzare in anteprima tooupgrade App per la logica di hello 1 agosto 2015 [estrarre sezione aggiornamento hello](##upgrade-your-schema).

<a name="scopes"></a>
## <a name="scopes"></a>Ambiti

Questo schema include gli ambiti, che consentono di raggruppare le azioni o annidarle all'interno di altre. Una condizione, ad esempio, può contenere un'altra condizione. Vedere altre informazioni sulla [sintassi degli ambiti](../logic-apps/logic-apps-loops-and-scopes.md) oppure esaminare questo esempio di ambito di base:

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
## <a name="conditions-and-loops-changes"></a>Modifiche di condizioni e cicli

Nelle versioni precedenti dello schema, le condizioni e i cicli sono parametri associati a una singola azione. In questo schema è stata rimossa questa limitazione e le condizioni e i cicli sono disponibili come tipi di azione. Vedere altre informazioni su [cicli e ambiti](../logic-apps/logic-apps-loops-and-scopes.md) oppure esaminare questo esempio di base di un'azione condizione:

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
## <a name="runafter-property"></a>Proprietà "runAfter"

Hello `runAfter` sostituisce proprietà `dependsOn`, fornisce maggiore precisione quando si specifica l'ordine di esecuzione hello per le azioni in base allo stato di hello delle azioni precedenti.

Hello `dependsOn` proprietà è un sinonimo di azione hello eseguito "e" è stata eseguita correttamente, indipendentemente da quante volte si desiderava tooexecute un'azione, in base alle azioni di hello precedente è stata eseguita, non è riuscita o ignorato. Hello `runAfter` proprietà flessibilità che un oggetto che specifica tutti hello dopo cui hello oggetto esegue i nomi di azione. Questa proprietà definisce anche una matrice degli stati accettabili come trigger. Ad esempio, se si desidera toorun dopo un passaggio ha esito positivo e anche dopo passaggio B ha esito positivo o negativo, costruire questo `runAfter` proprietà:

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a>Aggiornare lo schema

Aggiornamento toohello nuovo schema richiede solo pochi passaggi. Hello processo di aggiornamento include l'esecuzione dello script di aggiornamento hello, salvataggio come una nuova app per la logica e, se si desidera, eventualmente sovrascrivendo hello precedente logica app.

1. Nel portale di Azure hello, Apri l'app logica.

2. Andare troppo**Panoramica**. Sulla barra degli strumenti applicazione hello logica, scegliere **Aggiorna Schema**.
   
    ![Scegliere Aggiorna schema][1]
   
    Hello definizione aggiornata viene restituito, che è possibile copiare e incollare in una definizione di risorsa, se necessario. 
    Tuttavia, si **consigliabile** si sceglie **Salva con nome** toomake assicurarsi che tutti i riferimenti di connessione siano validi in hello aggiornato logica app.

3. Nella barra strumenti del Pannello di aggiornamento hello scegliere **Salva con nome**.

4. Immettere il nome di logica hello e di stato. toodeploy app logica aggiornato, scegliere **crea**.

5. Verificare che l'app per la logica aggiornata funzioni come previsto.
   
   > [!NOTE]
   > Se si utilizza un trigger manuale o richiesta, URL callback hello cambia nell'app nuova logica. Esperienza di test hello nuovo URL toomake che hello end-to-end. toopreserve URL precedenti, è possibile clonare tramite l'app logica esistente.

6. *Parametro facoltativo* toooverwrite app logica precedente con hello nuova versione dello schema, sulla barra degli strumenti hello, scegliere **Clone**, accanto troppo**Aggiorna Schema**. Questo passaggio è necessario solo se si desidera tookeep hello stessa risorsa ID richiesta trigger URL o dell'app logica.

### <a name="upgrade-tool-notes"></a>Note sullo strumento di aggiornamento

#### <a name="mapping-conditions"></a>Mapping delle condizioni

Nella definizione di hello aggiornato, strumento di hello rende tentativi al raggruppamento delle azioni branch true e false come ambito. In particolare, hello progettazione modello di `@equals(actions('a').status, 'Skipped')` dovrebbe essere visualizzato come un `else` azione. Tuttavia, se lo strumento hello rileva modelli non riconoscibile, strumento hello potrebbe creare condizioni distinte per true hello e branch false hello. Se necessario, è possibile modificare il mapping delle azioni dopo l'aggiornamento.

#### <a name="foreach-loop-with-condition"></a>Ciclo "foreach" con condizione

Nel nuovo schema hello, è possibile utilizzare il modello hello filtro azione tooreplicate hello di un `foreach` ciclo con una condizione per ogni elemento, ma questa modifica dovrebbe verificarsi automaticamente quando esegue l'aggiornamento. condizione Hello diventa un'operazione di filtro prima di ciclo foreach hello per la restituzione solo di una matrice di elementi che corrispondono alla condizione hello e tale matrice viene passata in azione foreach hello. Per un esempio, vedere l'articolo relativo a [cicli e ambiti](../logic-apps/logic-apps-loops-and-scopes.md).

#### <a name="resource-tags"></a>Tag delle risorse

Dopo l'aggiornamento, vengono rimossi i tag delle risorse, pertanto è necessario reimpostarli per flusso di lavoro hello aggiornato.

## <a name="other-changes"></a>Altre modifiche

### <a name="renamed-manual-trigger-toorequest-trigger"></a>Rinominare il trigger 'manual' too'request' trigger

Hello `manual` tipo di trigger è stato deprecato e rinominato troppo`request` con tipo `http`. Questa modifica crea maggiore coerenza per il tipo di hello di pattern che hello trigger è toobuild utilizzato.

### <a name="new-filter-action"></a>Nuova azione "filtro"

una matrice di grandi dimensioni verso il basso tooa ridurre il numero di elementi, hello nuovi toofilter `filter` tipo accetta una matrice e una condizione, valuta la condizione hello per ogni elemento e restituisce una matrice con gli elementi che soddisfano la condizione hello.

### <a name="restrictions-for-foreach-and-until-actions"></a>Restrizioni per le azioni "foreach" e "until"

Hello `foreach` e `until` ciclo sono limitate tooa singola azione.

### <a name="new-trackedproperties-for-actions"></a>Nuova proprietà "trackedProperties" per le azioni

Azioni ora possono avere una proprietà aggiuntiva chiamata `trackedProperties`, che è l'elemento di pari livello toohello `runAfter` e `type` proprietà. Questo oggetto consente di specificare alcuni input azione o l'output che si desidera tooinclude in telemetria di diagnostica di Azure hello, generata come parte di un flusso di lavoro. ad esempio:

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

## <a name="next-steps"></a>Passaggi successivi
* [Creare definizioni dei flussi di lavoro per le app per la logica](../logic-apps/logic-apps-author-definitions.md)
* [Creare modelli di distribuzione per le app per la logica](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
