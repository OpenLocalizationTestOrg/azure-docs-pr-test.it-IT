---
title: connettore di Office 365 Outlook hello aaaAdd nelle App logica | Documenti Microsoft
description: Creare App per la logica con l'interazione di tooenable connettore di Office 365 con Office 365. Ad esempio, per creare, modificare e aggiornare contatti ed elementi del calendario.
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a>Iniziare con il connettore di Office 365 Outlook hello
connettore di Office 365 Outlook Hello consente l'interazione con Outlook per Office 365. Utilizzare questo connettore toocreate, modificare e Aggiorna contatti e gli elementi del calendario e anche ottenere, inviare e rispondere tooemail.

Con Office 365 Outlook è possibile:

* Compilare il flusso di lavoro utilizzando le funzionalità di posta elettronica e al calendario hello in Office 365. 
* Utilizzare trigger toostart il flusso di lavoro quando si verifica un nuovo indirizzo e-mail, quando viene aggiornato un elemento del calendario e altro ancora.
* Utilizzare azioni toosend un messaggio di posta elettronica, creare un nuovo evento del calendario e altro ancora. Ad esempio, quando è presente un nuovo oggetto in Salesforce (trigger), inviare un messaggio di posta elettronica tooyour Outlook di Office 365 (azione). 

Questo argomento viene illustrato come toouse hello connettore Outlook di Office 365 in un'app per la logica e anche gli elenchi di hello azioni e trigger.

> [!NOTE]
> Questa versione di hello articolo applica tooLogic disponibilità generale di App (GA).
> 
> 

toolearn informazioni sulle App per la logica, vedere [quali sono le app logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toooffice-365"></a>Connettersi tooOffice 365
Prima che la logica app possa accedere a qualsiasi servizio, creare innanzitutto un *connessione* toohello servizio. Una connessione fornisce la connettività tra un'app per la logica e un altro servizio. Ad esempio, tooconnect tooOffice 365 Outlook, è necessario innanzitutto Office 365 *connessione*. toocreate una connessione, immettere le credenziali di hello utilizzato normalmente il servizio di hello tooaccess desiderato tooconnect per. Così con Outlook di Office 365, immettere le credenziali di hello tooyour connessione hello toocreate dell'account Office 365.

## <a name="create-hello-connection"></a>Creare una connessione hello
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a>Usare un trigger
Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica. I trigger "polling" servizio hello in corrispondenza di un intervallo e la frequenza desiderata. [Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Nell'app logica hello, digitare "office 365" tooget un elenco dei trigger hello:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. Selezionare **Office 365 Outlook - All'avvio imminente di un prossimo evento**. Se esiste già una connessione, quindi selezionare un calendario dall'elenco a discesa hello.
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    Nel caso di richiesta toosign in, quindi immettere hello sign in connessione hello toocreate di dettagli. [Creare una connessione hello](connectors-create-api-office365-outlook.md#create-the-connection) in questo argomento vengono elencati i passaggi di hello. 
   
   > [!NOTE]
   > In questo esempio hello logica app viene eseguita quando viene aggiornato un evento del calendario. risultati di hello toosee del trigger, aggiungere un'altra azione che invia un messaggio di testo. Ad esempio, aggiungere hello Twilio *Send message* azione testi quando hello calendario eventi in fase di avvio in 15 minuti. 
   > 
   > 
3. Seleziona hello **modifica** pulsante e impostare hello **frequenza** e **intervallo** valori. Ad esempio, se si desidera hello trigger toopoll ogni 15 minuti, quindi impostare hello **frequenza** troppo**minuto**e set hello **intervallo** troppo**15**. 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. **Salvare** le modifiche (angolo superiore sinistro della barra degli strumenti hello). L'app per la logica viene salvata e può essere attivata automaticamente.

## <a name="use-an-action"></a>Usare un'azione
Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica. [Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Selezionare hello sul segno più. Vedrai diverse opzioni: **aggiungere un'azione**, **aggiungere una condizione**, o uno dei hello **più** opzioni.
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. Selezionare **Aggiungi un'azione**.
3. Nella casella di testo hello, digitare "office 365" tooget un elenco di tutte le azioni disponibili hello.
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. Nell'esempio scegliere **Office 365 Outlook - Crea contatto**. Se esiste già una connessione, quindi scegliere hello **ID cartella**, **nome**e altre proprietà:  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    Se viene chiesto di hello informazioni di connessione, quindi immettere connessione hello toocreate dettagli di hello. [Creare una connessione hello](connectors-create-api-office365-outlook.md#create-the-connection) in questo argomento vengono descritte queste proprietà. 
   
   > [!NOTE]
   > In questo esempio si crea un nuovo contatto in Office 365 Outlook. È possibile utilizzare l'output dal contatto di un altro trigger toocreate hello. Ad esempio, aggiungere hello SalesForce *quando viene creato un oggetto* trigger. Aggiungere quindi hello Outlook di Office 365 *creare contatto* azione che utilizza hello SalesForce campi toocreate hello nuovo nuovo contatto in Office 365. 
   > 
   > 
5. **Salvare** le modifiche (angolo superiore sinistro della barra degli strumenti hello). L'app per la logica viene salvata e può essere attivata automaticamente.

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/office365connector/). 

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md). Esplorare hello altri connettori disponibile in App per la logica nel nostro [elenco API](apis-list.md).

