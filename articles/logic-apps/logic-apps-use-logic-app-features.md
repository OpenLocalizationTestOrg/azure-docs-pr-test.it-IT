---
title: le condizioni e avviare i flussi di lavoro - App Azure per la logica di aaaAdd | Documenti Microsoft
description: Controllare l'esecuzione dei flussi di lavoro nelle app per la logica di Azure mediante l'aggiunta di logica condizionale, trigger, azioni e parametri.
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a>Usare le funzionalità delle app per la logica

In un [argomento precedente](../logic-apps/logic-apps-create-a-logic-app.md) è stata creata la prima app per la logica. toocontrol flusso di lavoro logica dell'applicazione, è possibile specificare percorsi diversi per il toorun app logica e come troppo elaborare i dati in batch, le raccolte e matrici. È possibile includere questi elementi nel flusso di lavoro dell'app per la logica:

* Le condizioni e le [istruzioni switch](../logic-apps/logic-apps-switch-case.md) consentono all'app per la logica di eseguire azioni diverse in base al fatto che vengano soddisfatte o meno condizioni specifiche.

* I [cicli](../logic-apps/logic-apps-loops-and-scopes.md) consentono di eseguire ripetutamente passaggi dell'app per la logica. Ad esempio, è possibile ripetere azioni su una matrice quando si usa un ciclo **For_each**. Oppure è possibile ripetere azioni fino a quando non viene soddisfatta una condizione se si usa un ciclo **Until**.

* [Gli ambiti](../logic-apps/logic-apps-loops-and-scopes.md) consentono raggruppare serie di azioni, ad esempio, la gestione delle eccezioni tooimplement.

* [Scomposizione dei batch](../logic-apps/logic-apps-loops-and-scopes.md) consente di avviare i flussi di lavoro separati per gli elementi in una matrice quando si utilizza hello app logica **SplitOn** comando.

Questo argomento introduce altri concetti per la compilazione dell'app per la logica:

* Visualizzazione tooedit un'app esistente per la logica del codice
* Opzioni per avviare un flusso di lavoro

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a>Condizioni: eseguire i passaggi solo quando è soddisfatta una condizione

toohave logica app eseguire passaggi solo quando i dati soddisfano criteri specifici, è possibile aggiungere una condizione che confronta i dati nel flusso di lavoro hello in campi specifici o valori.

Si supponga, ad esempio, di avere un'app per la logica che invia troppi messaggi di posta elettronica per i post sul feed RSS di un sito Web. È possibile aggiungere una condizione in modo che l'app logica invia posta elettronica solo quando Registra nuovo hello categoria specifica tooa appartiene.

1. In hello [portale di Azure](https://portal.azure.com), trovare e aprire l'app logica nella finestra di progettazione logica App.

2. Aggiungere un percorso del flusso di lavoro toohello a condizione che si desidera. 

   condizione di hello tooadd tra i passaggi esistenti nel flusso di lavoro di hello logica app, spostare il puntatore di hello sulla freccia di hello in cui si desidera condizione hello tooadd. 
   Scegliere hello **segno** (**+**), quindi scegliere **aggiungere una condizione**. ad esempio:

   ![Aggiungi condizione toologic app](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > Se si desidera tooadd una condizione alla fine di hello del flusso di lavoro corrente, toohello inferiore dell'app logica, quindi **+ nuovo passaggio**.

3. Ora definire la condizione hello. Specificare il campo di origine hello che si desidera tooevaluate, hello operazione tooperform e il valore di destinazione hello o un campo. tooadd esistente campi tooyour condizione, scegliere hello **elenco contenuto dinamico Aggiungi**.

   ad esempio:

   ![Modificare la condizione nella modalità di base](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   Di seguito è la condizione completa hello:

   ![Condizione completa](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > condizione di hello toodefine nel codice, scegliere **modifica nella modalità avanzata**. ad esempio:
   > 
   > ![Modificare la condizione nel codice](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. In **Sì se** e **NO se**, aggiungere tooperform passaggi hello in base che hello condizione è soddisfatta.

   ad esempio:

   ![Condizione con percorsi SÌ e NO](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > È possibile trascinare le azioni esistenti nel hello **Sì se** e **NO se** percorsi.

5. Al termine, salvare l'app per la logica.

Ora si ottiene i messaggi di posta elettronica solo quando il postback hello soddisfa la condizione.

## <a name="repeat-actions-over-a-list-with-foreach"></a>Ripetere l'azione in un elenco con forEach

ciclo forEach Hello specifica un toorepeat matrice un'azione su. Se non è una matrice, il flusso di hello ha esito negativo. Ad esempio, se è azione1 che restituisce una matrice di messaggi che si desidera toosend ogni messaggio, è possibile includere l'istruzione forEach nelle proprietà hello dell'azione:`forEach : "@action('action1').outputs.messages"`

## <a name="edit-hello-code-definition-for-a-logic-app"></a>Modifica definizione di codice hello per un'app di logica

Anche se non si hello progettazione applicazione logica, è possibile modificare direttamente il codice hello che definisce un'app di logica.

1. Nella barra dei comandi di hello, scegliere **Code vista**.

    Un editor completo viene visualizzata la definizione di hello che è stato modificato.

    ![Visualizzazione Codice](media/logic-apps-use-logic-app-features/codeview.png)

    Nell'editor di testo hello, è possibile copiare e incollare qualsiasi numero di azioni all'interno di hello stessa logica app o tra App per la logica. 
    È possibile anche aggiungere o rimuovere intere sezioni dalla definizione di hello ed è anche possibile condividere definizioni con altri utenti.

2. Scegliere le modifiche, toosave **salvare**.

## <a name="parameters"></a>parameters

Alcune funzionalità delle app per la logica sono disponibili solo nella visualizzazione codice, ad esempio, i parametri. Parametri rendono facile tooreuse valori in tutta la logica app. Ad esempio, se si ha un indirizzo e-mail che si vuole usare in diverse azioni, è consigliabile definirlo come parametro.

I parametri sono ideali per l'estrazione di valori che si è molto probabile toochange. Sono particolarmente utili quando è necessario toooverride parametri in ambienti diversi. toolearn toooverride parametri basati sull'ambiente, vedere [creare definizioni di logica app](../logic-apps/logic-apps-author-definitions.md) e [documentazione dell'API REST](https://docs.microsoft.com/rest/api/logic).

Questo esempio viene illustrato come tooupdate app logica esistente in modo che è possibile utilizzare i parametri per il termine di query hello.

1. Nella visualizzazione codice, trovare hello `parameters : {}` e aggiungere un `currentFeedUrl` oggetto:

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. Passare toohello `When_a_feed-item_is_published` azione, hello trova `queries` sezione e sostituire il valore di query hello con:`"feedUrl": "#@{parameters('currentFeedUrl')}"` 

    toojoin due o più stringhe, è inoltre possibile utilizzare hello `concat` (funzione). 
    Ad esempio, `"@concat('#',parameters('currentFeedUrl'))"` works hello stesso come hello precedente.

3.  Al termine dell'operazione, scegliere **Salva**. 

    Ora è possibile modificare RSS del sito Web di hello feed passando un URL diverso tramite hello `currentFeedURL` oggetto.

Altre informazioni, vedere [come definizioni di tooauthor logica app](../logic-apps/logic-apps-author-definitions.md).

## <a name="start-logic-app-workflows"></a>Avviare i flussi di lavoro delle app per la logica

Sono disponibili opzioni diverse per l'avvio del flusso di lavoro hello definito nell'applicazione la logica. È sempre possibile avviare un flusso di lavoro su richiesta in hello [portale di Azure].

### <a name="recurrence-triggers"></a>Trigger di ricorrenza

Un trigger di ricorrenza viene eseguito a un intervallo specificato dall'utente. Quando il trigger di hello logica condizionale, trigger hello determina necessità di un flusso di lavoro hello toorun. Un trigger indica flusso di lavoro hello devono essere eseguite tramite la restituzione di un `200` codice di stato. Quando non è necessaria toorun, flusso di lavoro hello trigger hello restituisce un `202` codice di stato.

### <a name="callback-using-rest-apis"></a>Callback tramite le API REST

toostart un flusso di lavoro, è possono chiamare un endpoint di app logica servizi. Scegliere questo tipo di logica dell'applicazione su richiesta, toostart **Esegui ora** hello barra dei comandi. Vedere [Avviare i flussi di lavoro chiamando endpoint dell'app per la logica come trigger](../logic-apps/logic-apps-http-endpoint.md). 

<!-- Shared links -->
[portale di Azure]: https://portal.azure.com

## <a name="next-steps"></a>Passaggi successivi

* [Istruzioni switch](../logic-apps/logic-apps-switch-case.md) 
* [Cicli, ambiti e debatching](../logic-apps/logic-apps-loops-and-scopes.md)
* [Creare definizioni di app per la logica](../logic-apps/logic-apps-author-definitions.md)