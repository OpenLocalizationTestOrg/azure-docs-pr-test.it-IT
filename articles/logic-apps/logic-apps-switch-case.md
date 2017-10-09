---
title: istruzione aaaSwitch per azioni diverse nelle app di logica di Azure | Documenti Microsoft
description: Scegliere tooperform azioni diverse in base ai valori dell'espressione, utilizzando un'istruzione switch App per la logica
services: logic-apps
keywords: Istruzione switch
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a>Eseguire diverse azioni in app per la logica con un'istruzione switch

Durante la creazione di un flusso di lavoro, spesso è tootake azioni diverse in base al valore di hello di un oggetto o l'espressione. Ad esempio, è il toobehave app logica in modo diverso in base al codice di stato hello di una richiesta HTTP o un'opzione selezionata in un messaggio di posta elettronica.

È possibile utilizzare un tooimplement istruzione switch questi scenari. L'app di logica possibile valutare un token o un'espressione e scegliere caso hello hello hello di tooexecute stesso valore specificato di azioni. Un solo case deve corrispondere l'istruzione switch hello.

> [!TIP]
> Come tutti i linguaggi di programmazione, le istruzioni switch supportano solo gli operatori di uguaglianza. Se sono necessari altri operatori relazionali, ad esempio "maggiore di", usare un'istruzione di condizione.
> comportamento di esecuzione deterministico tooensure, casi devono contenere un valore univoco e statico invece di token dinamico o un'espressione.

## <a name="prerequisites"></a>Prerequisiti

- Una sottoscrizione di Azure attiva. Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) o provare l'[App per la logica gratuita](https://tryappservice.azure.com/).
- [Conoscenze di base di app per la logica](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a>Aggiungere un flusso di lavoro tooyour istruzione switch

tooshow funzionamento di un'istruzione switch, in questo esempio crea un'app di logica che i file di monitoraggi caricati tooDropbox. Quando vengono caricati i nuovi file hello, hello logica app Invia messaggio di posta elettronica tooan responsabile sceglie se tootransfer tooSharePoint tali file. app Hello utilizza un'istruzione switch che consente di eseguire azioni diverse in base al valore di hello hello Seleziona responsabile approvazione.

1. Creare un'app per la logica e selezionare questo trigger: **Dropbox - When a file is created** (Dropbox - Quando viene creato un file).

   ![Usare il trigger Dropbox - When a file is created (Dropbox - Quando viene creato un file)](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. Aggiungere trigger hello, questa azione: **Outlook.com - invio di email approvazione**

   > [!TIP]
   > Le app per la logica supportano anche gli scenari di posta elettronica di approvazione da un account di Outlook Office 365.

   - Se non si dispone di una connessione esistente, viene chiesto toocreate uno.
   - Compilare i campi necessario hello. Ad esempio, in **a**, specificare l'indirizzo di posta elettronica hello per l'invio di posta elettronica responsabile approvazione hello.
   - In **Opzioni utente**, inserire `Approve, Reject`.

   ![Configurare la connessione](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. Aggiungere un'istruzione switc.

   - Selezionare **+ Nuovo passaggio** > **... Altro** > **Aggiungi istruzione switch case**. 
   - Ora desideriamo tooselect hello azione tooperform in base a hello `SelectedOptions` l'output di hello *inviare posta elettronica di approvazione* azione. 
   Questo campo si trova in hello **aggiungere contenuto dinamico** selettore.
   - Utilizzare *caso 1* toohandle quando seleziona responsabile approvazione hello `Approve`.
     - Se approvata, copiare hello originale file tooSharePoint Online con hello [ **SharePoint Online - creare file** azione](../connectors/connectors-create-api-sharepointonline.md).
     - Aggiungere un'altra azione all'interno di hello case toonotify utenti che un nuovo file è disponibile in SharePoint.
   - Aggiungere un altro toohandle maiuscole quando l'utente seleziona `Reject`.
     - Se rifiutata, inviare una notifica tramite posta elettronica per informare gli altri revisori che file hello viene rifiutato e se è necessaria alcuna azione ulteriore.
   - `SelectedOptions`sono disponibili solo due opzioni, pertanto, è possibile mantenere hello **predefinito** case vuota.

   ![Istruzioni switch](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > Un'istruzione switch è necessario almeno un case nel caso di aggiunta toohello predefinito.

4. Dopo l'istruzione switch hello, eliminare hello originale file caricato tooDropbox aggiungendo questa azione: **Dropbox - Elimina file**

5. Salvare l'app per la logica. Testare l'app caricando un file tooDropbox. Si dovrebbe ricevere in breve tempo un messaggio di posta elettronica di approvazione. Selezionare un'opzione e osservare il comportamento di hello.

   > [!TIP]
   > Estrarre come troppo[monitorare App per la logica](logic-apps-monitor-your-logic-apps.md).

## <a name="understand-hello-code-behind-switch-statements"></a>Comprendere il codice hello dietro istruzioni switch

Ora che è stato creato correttamente un'applicazione logica utilizzando un'istruzione switch, esaminare la definizione di codice hello dietro istruzione switch hello.

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* `"Switch"`è il nome di hello dell'istruzione switch hello, che è possibile rinominare per migliorare la leggibilità. 
* `"type": "Switch"`indica che l'azione di hello è un'istruzione switch. 
* `"expression"`è l'opzione del revisore hello in questo esempio e viene valutato rispetto a ogni caso dichiarato in un secondo momento nella definizione di hello. 
* `"cases"` può contenere qualsiasi numero di case. Per ogni case, `"Case *"` è il nome predefinito hello del case hello, che è possibile rinominare per migliorare la leggibilità. 
`"case"`Specifica l'etichetta case hello, che hello commutatore utilizzo delle espressioni per il confronto e deve essere un valore costante e univoco. Se nessuno dei casi hello corrisponde espressione switch hello, azioni `"default"` vengono eseguite.

## <a name="get-help"></a>Ottenere aiuto

in caso di altri utenti le app di logica di Azure, vedere tooask domande e rispondere alle domande visitare hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp migliorare Azure logica App e connettori, votare o inviare idee in hello [sito commenti e suggerimenti dell'utente di Azure logica app](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Passaggi successivi

- Informazioni su come troppo[aggiungere condizioni](logic-apps-use-logic-app-features.md)
- Informazioni sulla [gestione di errori ed eccezioni](logic-apps-exception-handling.md)
- Esplorare altre [funzionalità di linguaggio del flusso di lavoro](logic-apps-author-definitions.md)