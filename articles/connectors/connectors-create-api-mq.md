---
title: aaaLearn come toouse hello connettore MQ nelle app di logica di Azure | Documenti Microsoft
description: Collegare tooan locale o server MQ Azure dalla toobrowse di flusso di lavoro app logica, ricevere e inviare messaggi tooWebSphere MQ
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a>Connessione server IBM MQ tooan da logica App usando il connettore MQ hello 

Microsoft Connector per MQ consente di inviare e recuperare i messaggi archiviati in un server MQ locale o in Azure. Il connettore include un client MQ Microsoft che comunica con un server IBM MQ remoto tramite una rete TCP/IP. Questo documento è un connettore MQ starter Guida toouse hello. È consigliabile iniziare cercando un singolo messaggio in una coda e quindi si tenta di hello altre azioni.    

connettore MQ Hello include hello seguenti azioni. Non sono disponibili trigger.

-   Selezionare un singolo messaggio senza eliminare il messaggio hello dal Server IBM MQ hello
-   Selezionare un batch di messaggi senza eliminare i messaggi hello dal Server IBM MQ hello
-   Un singolo messaggio di ricezione ed eliminare messaggio hello dal Server IBM MQ hello
-   Ricevere un batch di messaggi ed eliminare messaggi hello dalla hello Server IBM MQ
-   Inviare toohello un singolo messaggio IBM MQ Server 

## <a name="prerequisites"></a>Prerequisiti

* Se si utilizza un server di MSMQ locale, [installare il gateway dati locale di hello](../logic-apps/logic-apps-gateway-install.md) in un server all'interno della rete. Se hello Server MQ pubblicamente disponibili, o all'interno di Azure, quindi gateway dati hello non è utilizzate o necessarie.

    > [!NOTE]
    > server Hello in hello è installato il Gateway dati locale deve inoltre disporre di .net Framework 4.6 per hello connettore MQ toofunction installato.

* Creare risorse di Azure per il gateway dati locale di hello - hello [impostare la connessione del gateway dati hello](../logic-apps/logic-apps-gateway-connection.md).

* Versioni supportate ufficialmente di IBM WebSphere MQ:
   * MQ 7.5
   * MQ 8.0

## <a name="create-a-logic-app"></a>Creare un'app per la logica

1. In hello **Azure avviare discussioni**selezionare  **+**  (segno), **Web e dispositivi mobili**e quindi **logica App**. 
2. Immettere hello **nome**, ad esempio, MQTestApp **sottoscrizione**, **gruppo di risorse**, e **percorso** (utilizzare il percorso di hello dove hello connessione Gateway dati locale è configurato). Selezionare **Pin toodashboard**e selezionare **crea**.  
![Creare un'app per la logica](media/connectors-create-api-mq/Create_Logic_App.png)

## <a name="add-a-trigger"></a>Aggiungere un trigger

> [!NOTE]
> Hello MQ connettore non dispone di tutti i trigger. In tal caso, utilizzare un altro trigger toostart app logica, ad esempio hello **ricorrenza** trigger. 

1. Hello **logica App progettazione** viene visualizzata, selezionare **ricorrenza** nell'elenco di hello dei trigger comune.
2. Selezionare **modifica** all'interno di hello ricorrenza Trigger. 
3. Set hello **frequenza** troppo**giorno**e set hello **intervallo** troppo**7**. 

## <a name="browse-a-single-message"></a>Visualizzare un singolo messaggio
1. Selezionare **+ Nuovo passaggio** e quindi **Aggiungi un'azione**.
2. Nella casella di ricerca hello, digitare `mq`, quindi selezionare **MQ - Sfoglia messaggio**.  
![Browse message](media/connectors-create-api-mq/Browse_message.png) (Visualizza messaggio)

3. Se non è disponibile una connessione MSMQ esistente, quindi creare la connessione hello:  

    1. Selezionare **Connetti tramite il gateway dati locale**e immettere le proprietà di hello del server MQ.  
    Per **Server**, è possibile immettere il nome di server MQ hello o immettere l'indirizzo IP hello seguita da una virgola e hello il numero di porta. 
    2. Hello **gateway** tutte le connessioni gateway esistenti che sono state configurate gli elenchi a discesa. Selezionare il gateway.
    3. Selezionare **Create** (Crea) al termine. La connessione è simile toohello seguenti:   
    ![Proprietà connessione](media/connectors-create-api-mq/Connection_Properties.png)

4. Nelle proprietà di azione hello, è possibile:  

    * Hello utilizzare **coda** tooaccess proprietà un nome diverso rispetto a quello definito nella connessione hello
    * Hello utilizzare **MessageId**, **CorrelationId**, **GroupId**, toobrowse altre proprietà per un messaggio in base alle proprietà dei messaggi MSMQ diversi hello e
    * Impostare **IncludeInfo** troppo**True** tooinclude informazioni di altri messaggi nell'output di hello. O, impostare il valore troppo**False** toonot includere informazioni di altri messaggi nell'output di hello.
    * Immettere un **Timeout** valore toodetermine toowait il tempo per tooarrive un messaggio in una coda vuota. Se si specifica alcun valore, viene recuperato il primo messaggio hello nella coda di hello e non vi è alcun tempo di attesa per tooappear un messaggio.  
    ![Visualizzare le proprietà del messaggio](media/connectors-create-api-mq/Browse_message_Props.png)

5. **Salvare** le modifiche e quindi **eseguire** l'app per la logica:  
![Salvare ed eseguire](media/connectors-create-api-mq/Save_Run.png)

6. Dopo alcuni secondi, vengono illustrati i passaggi di hello di hello eseguire e output di hello è possibile esaminare. Selezionare hello segno di spunta verde toosee dettagli di ogni passaggio. Selezionare **vedere output raw** toosee ulteriori dettagli su hello i dati di output.  
![Visualizzare l'output del messaggio](media/connectors-create-api-mq/Browse_message_output.png)  

    Output non elaborato:  
    ![Visualizzare l'output non elaborato del messaggio](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. Quando hello **IncludeInfo** impostazione tootrue, viene visualizzato hello seguente output:  
![Visualizzare le informazioni incluse del messaggio](media/connectors-create-api-mq/Browse_message_Include_Info.png)

## <a name="browse-multiple-messages"></a>Visualizzare più messaggi
Hello **visualizzare messaggi di** azione include un **BatchSize** tooindicate opzione deve essere restituito il numero di messaggi dalla coda hello.  In assenza di un valore per **BatchSize**, vengono restituiti tutti i messaggi. Hello ha restituito l'output è una matrice di messaggi.

1. Quando si aggiungono hello **visualizzare messaggi** azione, hello prima connessione che è configurato sia selezionata per impostazione predefinita. Selezionare **Cambia connessione** toocreate una nuova connessione, oppure selezionare una connessione diversa.

2. output di Hello di Sfoglia messaggi Mostra:  
![Output dell'azione Browse messages (Visualizza messaggi)](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a>Ricevere un singolo messaggio
Hello **Ricevi messaggio** azione ha hello stesso input e output di hello **messaggio Sfoglia** azione. Quando si utilizza **Ricevi messaggio**, il messaggio hello viene eliminato dalla coda hello.

## <a name="receive-multiple-messages"></a>Ricevere più messaggi
Hello **ricevere messaggi** azione ha hello stesso input e output di hello **visualizzare messaggi** azione. Quando si utilizza **ricevere messaggi**, messaggi hello vengono eliminati dalla coda hello.

Se non sono presenti messaggi nella coda di hello quando si esegue una ricerca o un'operazione di ricezione, passaggio hello ha esito negativo con hello seguente output:  
![Errore di nessun messaggio in MQ](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a>Inviare un messaggio
1. Quando si aggiungono hello **Send message** azione, hello prima connessione che è configurato sia selezionata per impostazione predefinita. Selezionare **Cambia connessione** toocreate una nuova connessione, oppure selezionare una connessione diversa. Hello valido **tipi di messaggio** sono **datagramma**, **risposta**, o **richiesta**.  
![Proprietà dell'azione Send message (Invia messaggio)](media/connectors-create-api-mq/Send_Msg_Props.png)

2. Hello output del messaggio di trasmissione simile hello seguente:  
![Output dell'azione Send message (Invia messaggio)](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/mq/).

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md). Esplorare hello altri connettori disponibile in App per la logica nel nostro [elenco API](apis-list.md).
