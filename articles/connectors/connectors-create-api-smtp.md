---
title: connettore aaaSMTP nelle app di logica di Azure | Documenti Microsoft
description: Creare app per la logica con Servizio app di Azure. Connettersi tramite posta elettronica toosend tooSMTP.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a>Iniziare con il connettore SMTP hello
Connettersi tramite posta elettronica toosend tooSMTP.

toouse [i connettori](apis-list.md), è necessario innanzitutto toocreate un'app di logica. Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosmtp"></a>Connettersi tooSMTP
Prima che la logica app possa accedere a qualsiasi servizio, è necessario innanzitutto toocreate un *connessione* toohello servizio. Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio. Ad esempio, tooSMTP tooconnect, è necessario innanzitutto un SMTP *connessione*. toocreate una connessione, immettere le credenziali di hello utilizzato normalmente il servizio di hello tooaccess ci si connette a. In tal caso, nell'esempio hello SMTP immettere hello credenziali tooyour connessione nome, indirizzo del server SMTP e utente accesso informazioni toocreate hello connessione tooSMTP.  

### <a name="create-a-connection-toosmtp"></a>Creare una connessione tooSMTP
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a>Usare un trigger SMTP
Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica. [Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

In questo esempio, perché non dispone di un trigger di un proprio, SMTP utilizzeremo hello **Salesforce - quando viene creato un oggetto** trigger. Questo trigger viene attivato quando viene creato un nuovo oggetto in Salesforce. Per questo esempio, verrà configurato tale che ogni volta un nuovo cliente potenziale creato in Salesforce, un *inviare posta elettronica* azione si verifica tramite il connettore SMTP hello con una notifica di hello nuovo cliente potenziale da creare.

1. Immettere *salesforce* nella casella di ricerca hello nella finestra di progettazione di hello logica App, quindi selezionare hello **Salesforce - quando viene creato un oggetto** trigger.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. Hello **quando viene creato un oggetto** controllo viene visualizzato.
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. Seleziona hello **tipo di oggetto** selezionare *causare* elenco hello degli oggetti. In questo passaggio si indica che si sta creando un trigger che invierà una notifica all'app per la logica ogni volta che viene creato un nuovo lead in Salesforce.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. Hello trigger è stato creato.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a>Usare un'azione SMTP
Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica. [Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Ora che hello trigger è stato aggiunto, seguire queste azioni tooadd un SMTP passaggi che si verificano quando viene creato un nuovo cliente potenziale in Salesforce.

1. Selezionare **+ nuovo passaggio** azione hello tooadd desideri tootake quando viene creato un nuovo cliente potenziale.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. Selezionare **Aggiungi un'azione**. Questa casella di ricerca hello viene visualizzata in cui è possibile cercare qualsiasi azione si desidera tootake.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. Immettere *smtp* toosearch per azioni correlate tooSMTP.  
4. Selezionare **SMTP - invio di posta elettronica** come hello tootake azione quando viene creato nuovo lead hello. verrà visualizzata la finestra di blocco di controllo azione Hello. Sarà necessario tooestablish la connessione smtp nel blocco progettazione hello se si è già stato in precedenza.  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. Immettere le informazioni del messaggio di posta elettronica desiderato in hello **SMTP - invio di posta elettronica** blocco.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. Salvare il lavoro in ordine tooactivate il flusso di lavoro.  

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/smtpconnector/).

## <a name="more-connectors"></a>Altri connettori
Tornare indietro toohello [elenco API](apis-list.md).
