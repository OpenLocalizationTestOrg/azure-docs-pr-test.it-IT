---
title: aaaBatch elaborare i messaggi a un gruppo o raccolta - App Azure per la logica | Documenti Microsoft
description: Inviare e ricevere messaggi per l'elaborazione in batch nelle app per la logica
keywords: batch, processo batch
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a>Inviare, ricevere ed elaborare in batch i messaggi nelle app per la logica

messaggi tooprocess riuniti in gruppi, è possibile inviare dati elementi o i messaggi, tooa *batch*e quindi elaborare tali elementi come un batch. Questo approccio è utile quando si desidera toomake gli elementi di dati che vengono raggruppati in modo specifico e vengono elaborati insieme. 

È possibile creare App per la logica che ricevono gli elementi come un batch utilizzando hello **Batch** trigger. È quindi possibile creare App per la logica che inviano elementi tooa batch utilizzando hello **Batch** azione.

Questo argomento illustra come compilare una soluzione di invio in batch mediante l'esecuzione di queste attività: 

* [Creare un'app per la logica che riceve e raccoglie gli elementi in batch](#batch-receiver). Questa app "ricevitore batch" per la logica specifica hello batch nome e la versione criteri toomeet prima hello ricevitore logica app rilascia ed elabora gli elementi. 

* [Creare un'app di logica che invia gli elementi tooa batch](#batch-sender). Questa app "mittente batch" per la logica specifica dove toosend elementi, che devono essere un'app di logica di ricevitore batch esistente. Si può inoltre specificare una chiave univoca, ad esempio un numero cliente, troppo "partizione" o divide, batch di destinazione hello in subset in base a tale chiave. Tutti gli elementi con questa chiave verranno così raccolti ed elaborati insieme. 

## <a name="requirements"></a>Requisiti

toofollow in questo esempio, è necessario di questi elementi:

* Una sottoscrizione di Azure. Se non si ha una sottoscrizione, è possibile [creare un account Azure gratuito](https://azure.microsoft.com/free/). In alternativa, è possibile [iscriversi per ottenere una sottoscrizione con pagamento in base al consumo](https://azure.microsoft.com/pricing/purchase-options/).

* Conoscenza di base [come toocreate logica App](../logic-apps/logic-apps-create-a-logic-app.md) 

* Un account di posta elettronica con un [provider di posta elettronica supportato da App per la logica di Azure](../connectors/apis-list.md)

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a>Creare app per la logica che ricevono messaggi in batch

Prima di poter inviare batch di messaggi tooa, è innanzitutto necessario creare un'app di logica "ricevitore batch" con hello **Batch** trigger. In questo modo, quando si crea un'app di hello mittente logica, è possibile selezionare questa app logica ricevitore. Per i ricevitori di hello, specificare nome batch hello, criteri di rilascio e altre impostazioni. 

Mittente logica App necessario sapere dove gli elementi toosend, mentre ricevitore logica App non è necessario tooknow qualsiasi valore sulla mittenti hello.

1. In hello [portale di Azure](https://portal.azure.com), creare un'app logica con questo nome: "BatchReceiver" 

2. Nella finestra di progettazione di logica di App, aggiungere hello **Batch** trigger, che avvia il flusso di lavoro logica app. Nella casella di ricerca hello, immettere "batch" come filtro. Selezionare il trigger: **Batch - Messaggi batch**

   ![Aggiungere il trigger Batch](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. Specificare un nome per il batch di hello e specificare i criteri per il rilascio di batch di hello, ad esempio:

   * **Nome batch**: hello nome utilizzato tooidentify hello batch, ovvero "TestBatch" in questo esempio.
   * **Numero di messaggi**: hello numero di messaggi toohold come un batch prima del rilascio per l'elaborazione, ovvero "5" in questo esempio.

   ![Specificare i dettagli del trigger Batch](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. Aggiungere un'altra azione che invia un messaggio di posta elettronica quando viene attivato il trigger di batch hello. Ogni batch di hello ora ha cinque elementi, hello logica app invia un messaggio di posta elettronica.

   1. In trigger batch hello, scegliere **+ nuovo passaggio** > **aggiungere un'azione**.

   2. Nella casella di ricerca hello, immettere "email" come filtro.
   In base al provider di posta elettronica in uso, selezionare un connettore di posta elettronica.
   
      Ad esempio, se si dispone di un account aziendale o dell'istituto di istruzione, selezionare il connettore di Office 365 Outlook hello. 
      Se si dispone di un account Gmail, selezionare il connettore di Gmail hello.

   3. Selezionare questa azione per il connettore: **{*provider di posta elettronica*} - Invia messaggio di posta elettronica**,

      ad esempio:

      ![Selezionare l'azione "Invia un messaggio di posta elettronica" per il provider di posta elettronica](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. Se non è stata creata prima una connessione per il provider di posta elettronica, immettere al prompt le credenziali per l'autenticazione. Leggere altre informazioni sull'[autenticazione delle credenziali di posta elettronica](../logic-apps/logic-apps-create-a-logic-app.md).

6. Impostare le proprietà hello azione hello che appena aggiunto.

   * In hello **a** , immettere l'indirizzo di posta elettronica del destinatario hello. 
   AI fini del test delle app è possibile indicare il proprio indirizzo di posta elettronica.

   * In hello **soggetto** casella quando hello **contenuto dinamico** viene visualizzato l'elenco, selezionare hello **nome partizione** campo.

     ![Selezionare "Nome di partizione" hello "Contenuto dinamico" elenco](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     In una sezione successiva, è possibile specificare una chiave di partizione univoca che divide hello batch di destinazione in logico imposta toowhere è possibile inviare messaggi. 
     Ogni set ha un numero univoco generato da hello mittente logica app. 
     Questa funzionalità consente di utilizzare un singolo batch con più sottoinsiemi e definire ogni subset con nome hello specificata dall'utente.

   * In hello **corpo** casella quando hello **contenuto dinamico** viene visualizzato l'elenco, selezionare hello **Id messaggio** campo.

     ![Per la casella "Body" selezionare "ID messaggio"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     Poiché l'input hello per azione di hello invio messaggio di posta elettronica è una matrice, hello viene automaticamente aggiunta una **per ogni** cerchio attorno hello **invia un messaggio di posta elettronica** azione. 
     Questo ciclo esegue l'azione interna hello su ogni elemento nel batch hello. 
     In tal caso, con elementi di toofive set trigger batch hello, sono disponibili cinque messaggi di posta elettronica che viene attivato ogni trigger hello ora.

7.  Ora che è stata creata un'app per la logica ricevente, occorre salvarla.

    ![Salvare l'app per la logica](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a>Creare App per la logica che inviano batch di messaggi tooa

Creare uno o più App per la logica che inviano batch toohello elementi definiti da hello ricevitore logica app. Per il mittente di hello, si specifica hello ricevitore logica app e nome del batch, il contenuto del messaggio e tutte le altre impostazioni. È anche possibile specificare un batch di hello toodivide chiave di partizione univoca negli elementi toocollect subset con tale chiave.

Mittente logica App necessario sapere dove gli elementi toosend, mentre ricevitore logica App non è necessario tooknow qualsiasi valore sulla mittenti hello.

1. Creare un'altra app per la logica con questo nome: "BatchSender"

   1. Nella casella di ricerca hello, immettere "recurrence" come filtro. 
   Selezionare il trigger **Pianificazione - Ricorrenza**

      ![Aggiungere trigger hello "Ricorrenza pianificazione"](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. Impostare la frequenza di hello e intervallo toorun hello mittente logica app ogni minuto.

      ![Impostare la frequenza e l'intervallo del trigger di ricorrenza](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. Aggiungere un nuovo passaggio per l'invio di batch di messaggi tooa.

   1. Trigger di ricorrenza hello, scegliere **+ nuovo passaggio** > **aggiungere un'azione**.

   2. Nella casella di ricerca hello, immettere "batch" come filtro. 

   3. Selezionare l'azione: **inviare messaggi toobatch: scegliere un flusso di lavoro App per la logica con trigger batch**

      ![Selezionare "Invia messaggi toobatch"](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. Selezionare a questo punto l'app per la logica "BatchReceiver" creata in precedenza, che ora viene visualizzata sotto forma di azione.

      ![Selezionare l'app per la logica "ricevente il batch"](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > elenco di Hello Mostra anche le altre app di logica a cui sono presenti trigger batch.

3. Impostare le proprietà batch hello.

   * **Nome batch**: nome batch hello definito dall'applicazione logica ricevitore hello, "TestBatch" in questo esempio e viene convalidato in fase di esecuzione.

     > [!IMPORTANT]
     > Assicurarsi di non modificare il nome batch hello, che deve corrispondere al nome specificato da hello ricevitore logica app batch hello.
     > Modifica nome batch di hello fa sì che il mittente hello logica app toofail.

   * **Contenuto del messaggio**: hello che si desidera toosend il contenuto del messaggio. 
   Per questo esempio, aggiungere l'espressione che inserimenti hello data e ora correnti nel messaggio hello del contenuto che si invia toohello batch:

     1. Quando hello **contenuto dinamico** viene visualizzato l'elenco, scegliere **espressione**. 
     2. Immettere l'espressione hello **utcnow()**e scegliere **OK**. 

        ![In "Contenuto messaggio" scegliere "Espressione". Immettere "utcnow()".](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. Ora consente di impostare una partizione per il batch di hello. Nell'azione "BatchReceiver" hello, scegliere **Visualizza le opzioni avanzate**.

   * **Nome di partizione**: un toouse chiave di partizione univoco facoltativo per la suddivisione del batch di destinazione hello. Per questo esempio aggiungere un'espressione che genera un numero casuale compreso tra uno e cinque.
   
     1. Quando hello **contenuto dinamico** viene visualizzato l'elenco, scegliere **espressione**.
     2. Immettere l'espressione **rand(1,6)**

        ![Configurare una partizione per il batch di destinazione](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        Questa funzione **rand** genera un numero compreso tra uno e cinque. 
        Si divide pertanto il batch in cinque partizioni numerate, che questa espressione imposta in modo dinamico.

   * **ID messaggio**: un identificatore di messaggio facoltativo e GUID generato quando vuoto. 
   Per questo esempio lasciare vuota questa casella.

5. Salvare l'app per la logica. Logica app mittente sarà esempio toothis simile:

   ![Salvare l'app per la logica mittente](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a>Testare le app per la logica

tootest l'invio in batch di soluzione, lasciare l'App in esecuzione per alcuni minuti per la logica. Presto iniziare il recupero di messaggi di posta elettronica nei gruppi di cinque, tutti con hello stessa chiave di partizione.

Logica app BatchSender viene eseguito ogni minuto, genera un numero casuale compreso tra uno e cinque e viene utilizzato questo numero generato come chiave di partizione hello per il batch di destinazione hello in cui i messaggi vengono inviati. Ogni volta che il batch hello ha cinque elementi con hello stessa chiave di partizione, BatchReceiver logica app genera e invia posta elettronica per ogni messaggio.

> [!IMPORTANT]
> Al termine di test, assicurarsi di disattivare hello BatchSender logica app toostop l'invio di messaggi e di evitare il sovraccarico di posta in arrivo.

## <a name="next-steps"></a>Passaggi successivi

* [Build on logic app definitions by using JSON](../logic-apps/logic-apps-author-definitions.md) (Compilare definizioni di app per la logica on JSON)
* [Compilare un'app senza server in Visual Studio con App per la logica e Funzioni](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [Gestione delle eccezioni e registrazione degli errori per le app per la logica](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
