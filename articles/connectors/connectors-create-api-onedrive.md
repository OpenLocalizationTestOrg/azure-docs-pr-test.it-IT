---
title: connettore di OneDrive aaaAdd hello nelle App logica | Documenti Microsoft
description: Panoramica del connettore di hello OneDrive con i parametri di API REST
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a>Iniziare con il connettore di OneDrive hello
Connettersi tooOneDrive toomanage dei file, inclusi il caricamento, get, eliminare i file e molto altro. 

Con OneDrive è possibile: 

* Creare un flusso di lavoro mediante l'archiviazione di file in OneDrive o aggiornare i file esistenti in OneDrive. 
* Utilizzare trigger toostart il flusso di lavoro quando un file viene creato o aggiornato all'interno di OneDrive.
* Usare azioni toocreate un file, eliminare un file e altro ancora. Ad esempio, creare un nuovo file in OneDrive (azione) quando viene ricevuto un nuovo messaggio di posta elettronica di Office 365 con un allegato (trigger).

Questo argomento viene illustrato come toouse hello OneDrive connettore in un'app di logica e anche gli elenchi di hello azioni e trigger.

toolearn informazioni sulle App per la logica, vedere [quali sono le app logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooonedrive"></a>Connettersi tooOneDrive
Prima che la logica app possa accedere a qualsiasi servizio, creare innanzitutto un *connessione* toohello servizio. Una connessione fornisce la connettività tra un'app per la logica e un altro servizio. Ad esempio, tooOneDrive tooconnect, è necessario innanzitutto un OneDrive *connessione*. toocreate una connessione, immettere le credenziali di hello utilizzato normalmente il servizio di hello tooaccess desiderato tooconnect per. In tal caso, OneDrive, immettere hello credenziali tooyour OneDrive toocreate hello connessione ad account di.

### <a name="create-hello-connection"></a>Creare una connessione hello
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a>Usare un trigger
Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica. I trigger "polling" servizio hello in corrispondenza di un intervallo e la frequenza desiderata. [Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Nell'app logica hello, digitare "onedrive" tooget un elenco dei trigger hello:  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. Selezionare **Quando viene modificato un file**. Se esiste già una connessione, quindi selezionare hello selezione Mostra pulsante tooselect una cartella.
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    Nel caso di richiesta toosign in, quindi immettere hello sign in connessione hello toocreate di dettagli. [Creare una connessione hello](connectors-create-api-onedrive.md#create-the-connection) in questo argomento vengono elencati i passaggi di hello. 
   
   > [!NOTE]
   > In questo esempio hello logica app viene eseguita quando un file nella cartella hello che scelto viene aggiornato. risultati di hello toosee del trigger, aggiungere un'altra azione che invia un messaggio di posta elettronica. Ad esempio, aggiungere hello Outlook di Office 365 *invia un messaggio di posta elettronica* azione che tramite posta elettronica quando viene aggiornato un file. 

3. Seleziona hello **modifica** pulsante e impostare hello **frequenza** e **intervallo** valori. Ad esempio, se si desidera hello trigger toopoll ogni 15 minuti, quindi impostare hello **frequenza** troppo**minuto**e set hello **intervallo** troppo**15**. 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. **Salvare** le modifiche (angolo superiore sinistro della barra degli strumenti hello). L'app per la logica viene salvata e può essere attivata automaticamente.

## <a name="use-an-action"></a>Usare un'azione
Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica. [Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Selezionare hello sul segno più. Vedrai diverse opzioni: **aggiungere un'azione**, **aggiungere una condizione**, o uno dei hello **più** opzioni.
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. Selezionare **Aggiungi un'azione**.
3. Nella casella di testo hello, digitare "onedrive" tooget un elenco di tutte le azioni disponibili hello.
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. Nell'esempio scegliere **OneDrive - Crea file**. Se esiste già una connessione, quindi selezionare hello **percorso della cartella** tooput hello file, immettere hello **nome File**e scegliere hello **contenuto File** desiderato:  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    Se viene chiesto di hello informazioni di connessione, quindi immettere connessione hello toocreate dettagli di hello. [Creare una connessione hello](connectors-create-api-onedrive.md#create-the-connection) in questo argomento vengono descritte queste proprietà. 
   
   > [!NOTE]
   > In questo esempio creiamo un nuovo file in una cartella di OneDrive. È possibile utilizzare l'output da un altro file di OneDrive hello di toocreate trigger. Ad esempio, aggiungere hello Outlook di Office 365 *all'arrivo di un nuovo indirizzo e-mail* trigger. Aggiungere quindi hello OneDrive *crea file* azione che utilizza hello allegati e i campi di tipo di contenuto all'interno di ForEach toocreate hello nuovo file in OneDrive. 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. **Salvare** le modifiche (angolo superiore sinistro della barra degli strumenti hello). L'app per la logica viene salvata e può essere attivata automaticamente.


## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/onedriveconnector/).

## <a name="more-connectors"></a>Altri connettori
Tornare indietro toohello [elenco API](apis-list.md).
