---
title: aaaLearn come toouse hello in App per la logica del connettore Twitter | Documenti Microsoft
description: Panoramica del connettore Twitter con i parametri dell'API REST
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a>Iniziare con il connettore di Twitter hello
Con il connettore di Twitter hello è possibile:

* Pubblicare e recuperare tweet
* Accedere a timeline, amici e follower
* Eseguire una delle hello altre azioni e trigger descritto di seguito  

toouse [i connettori](apis-list.md), è necessario innanzitutto toocreate un'app di logica. Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).  

## <a name="connect-tootwitter"></a>Connettersi tooTwitter
Prima che la logica app possa accedere a qualsiasi servizio, è necessario innanzitutto toocreate un *connessione* toohello servizio. Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.  

### <a name="create-a-connection-tootwitter"></a>Creare una connessione tooTwitter
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a>Usare un trigger di Twitter
Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica. [Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

In questo esempio, verrà spiegato come hello toouse **durante il postback un tweet nuovo** attivare toosearch per #Seattle e, se viene trovato #Seattle, è possibile aggiornare un file nell'area di sincronizzazione con il testo hello tweet hello. In un esempio di enterprise, è possibile cercare il nome della società hello e aggiornare un database SQL con il testo hello tweet hello.

1. Immettere *twitter* nella casella di ricerca hello nella finestra di progettazione di hello logica App, quindi selezionare hello **Twitter - quando viene inserito un nuovo tweet** trigger   
   ![Immagine di trigger Twitter 1](./media/connectors-create-api-twitter/trigger-1.png)  
2. Immettere *#Seattle* in hello **testo di ricerca** controllo  
   ![Immagine di trigger Twitter 2](./media/connectors-create-api-twitter/trigger-2.png) 

A questo punto, l'app di logica è stato configurato con un trigger che verrà avviata un'esecuzione di hello altre azioni nel flusso di lavoro hello e il trigger. 

> [!NOTE]
> Per un toobe di app logica funzionale, deve contenere almeno un trigger e un'azione. Seguire passaggi hello hello successiva sezione tooadd un'azione.  
> 
> 

## <a name="add-a-condition"></a>Add a condition
Poiché si intende solo TWEET da utenti con più di 50 utenti, una condizione che il numero di hello di anelli di conferma deve essere aggiunto toohello logica app.  

1. Selezionare **+ nuovo passaggio** azione hello tooadd desideri tootake quando #Seattle si trova in un tweet nuovo  
   ![Immagine di azione Twitter 1](../../includes/media/connectors-create-api-twitter/action-1.png)  
2. Seleziona hello **aggiungere una condizione** collegamento.  
   ![Immagine di condizione Twitter 1](../../includes/media/connectors-create-api-twitter/condition-1.png)   
   Verrà visualizzata hello **condizione** controllo in cui è possibile controllare le condizioni, ad esempio *è uguale a*, *è minore di*, *è maggiore di*, *contiene*e così via.  
   ![Immagine di condizione Twitter 2](../../includes/media/connectors-create-api-twitter/condition-2.png)   
3. Seleziona hello **scegliere un valore** controllo.  
   In questo controllo, è possibile selezionare uno o più proprietà hello dalle azioni precedenti o i trigger come valore di hello la cui condizione verrà valutata tootrue o false.
   ![Immagine di condizione Twitter 3](../../includes/media/connectors-create-api-twitter/condition-3.png)   
4. Seleziona hello **...**  tooexpand hello elenco di proprietà in modo da visualizzare tutte le proprietà di hello disponibili.        
   ![Immagine di condizione Twitter 4](../../includes/media/connectors-create-api-twitter/condition-4.png)   
5. Seleziona hello **il numero di anelli** proprietà.    
   ![Immagine di condizione Twitter 5](../../includes/media/connectors-create-api-twitter/condition-5.png)   
6. Si noti bisogno di hello seguenti proprietà di conteggio è ora nel controllo value hello.    
   ![Immagine di condizione Twitter 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. Selezionare **è maggiore di** dall'elenco di operatori hello.    
   ![Immagine di condizione Twitter 7](../../includes/media/connectors-create-api-twitter/condition-7.png)   
8. Immettere 50 come operando per hello hello *è maggiore di* operatore.  
   condizione Hello viene aggiunto. Salvare il lavoro usando hello **salvare** collegamento nel menu hello precedente.    
   ![Immagine di condizione Twitter 8](../../includes/media/connectors-create-api-twitter/condition-8.png)   

## <a name="use-a-twitter-action"></a>Usare un'azione di Twitter
Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica. [Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Dopo avere aggiunto un trigger, seguire questi tooadd passaggi un'azione che verrà registrato un nuovo tweet con contenuto hello di hello TWEET trovato dal trigger hello. Ai fini di hello di questa procedura dettagliata verrà registrato solo TWEET da utenti con più di 50 anelli.  

Nel passaggio successivo hello, si aggiungerà un'azione di Twitter che eseguirà un tweet utilizzando alcune delle proprietà hello di ogni tweet che è stata registrata da un utente che ha bisogno di più di 50 seguenti.  

1. Selezionare **Aggiungi un'azione**. Verrà aperto il controllo di ricerca hello in cui è possibile cercare altre azioni e trigger.  
   ![Immagine di condizione Twitter 9](../../includes/media/connectors-create-api-twitter/condition-9.png)   
2. Immettere *twitter* nella casella di ricerca hello, quindi selezionare hello **Twitter: registrare un tweet** azione. Verrà visualizzata hello **registra un tweet** controllare dove verrà immesso tutti i dettagli per tweet hello inviata.      
   ![Immagine di azione Twitter 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)   
3. Seleziona hello **Tweet testo** controllo. Tutti gli output di azioni precedenti e i trigger in hello logica app sono ora visibili. È possibile selezionare una delle seguenti e utilizzarle come parte del testo tweet hello di tweet nuovo hello.     
   ![Immagine di azione Twitter 2](../../includes/media/connectors-create-api-twitter/action-2.png)   
4. Selezionare **Nome utente**   
5. Immettere *afferma:* nel controllo di testo tweet hello. Eseguire questa operazione subito dopo il nome utente.  
6. Selezionare *Testo del tweet*.       
   ![Immagine di azione Twitter 3](../../includes/media/connectors-create-api-twitter/action-3.png)   
7. Salvare il lavoro e invii un tweet con hello #Seattle hashtag tooactivate il flusso di lavoro.  


## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/twitterconnector/). 

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md)

