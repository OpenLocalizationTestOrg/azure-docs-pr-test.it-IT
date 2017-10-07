---
title: connettore aaaWebhook per le app di logica di Azure | Documenti Microsoft
description: Le azioni webhook toouse e le azioni di trigger tooperform come matrice di filtro da logica App
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 71775384-6c3a-482c-a484-6624cbe4fcc7
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: b2dee12750f3f20f10e7b257da05a79f28f90f43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-webhook-connector"></a>Iniziare con connettore webhook hello

Con l'azione webhook hello e trigger, è possibile avviare, sospendere e riprendere i flussi tooperform queste attività:

* Eseguire l'attivazione da un [Hub eventi di Azure](https://github.com/logicappsio/EventHubAPI) alla ricezione di un elemento
* Attendere l'approvazione prima di continuare un flusso di lavoro

Altre informazioni, vedere [come toocreate API personalizzate che supportano un webhook](../logic-apps/logic-apps-create-api-app.md).

## <a name="use-hello-webhook-trigger"></a>Utilizzare trigger webhook hello

Un [*trigger*](connectors-overview.md) è un evento che avvia un flusso di lavoro nell'app per la logica. Un trigger webhook è basato su eventi e non si basa sul polling per nuovi elementi. Ad esempio hello [trigger richiesta](connectors-native-reqres.md), hello logica app genera hello immediato che si verifica un evento. trigger webhook Hello registra un *URL callback* tooa servizio e viene utilizzato tale URL toofire hello app per la logica come necessario.

Di seguito è riportato un esempio che illustra come trigger tooset backup HTTP hello progettazione applicazione logica. Hello passaggi presuppongono che si hanno già distribuito o se si accede a un'API che segue hello [webhook sottoscrivere e annullare la sottoscrizione di modello di App per la logica](../logic-apps/logic-apps-create-api-app.md#webhook-triggers). Hello sottoscrizione chiamata viene eseguita ogni volta che un'app logica viene salvata con un nuovo webhook o passa da tooenabled disabilitato. annullare la sottoscrizione Hello chiamata viene eseguita quando un trigger di logica app webhook viene rimosso e salvato o passa da toodisabled abilitato.

**trigger di tooadd hello webhook**

1. Aggiungere hello **HTTP Webhook** trigger come primo passaggio di hello in un'app di logica.
2. Specificare i parametri di hello per hello webhook sottoscrivere e annullare la sottoscrizione di chiamate.

   Questo passaggio segue hello stesso schema come hello [azione HTTP](connectors-native-http.md) formato.

     ![Trigger HTTP](./media/connectors-native-webhook/using-trigger.png)

3. Aggiungere almeno un'azione.
4. Fare clic su **salvare** toopublish hello logica app. Questo hello chiamate passaggio sottoscrizione endpoint con hello callback URL necessario tootrigger questa app per la logica.
5. Ogni volta che hello servizio rende un `HTTP POST` toohello URL callback, hello logica app generato e include tutti i dati passati richiesta hello.

## <a name="use-hello-webhook-action"></a>Utilizzare l'azione di hello webhook

Un [ *azione* ](connectors-overview.md) viene eseguita un'operazione dal flusso di lavoro hello definito in un'app di logica. Un'azione webhook registra un *URL callback* con un servizio e attende fino a quando viene chiamato hello URL prima di riprendere. Hello ["Invio di posta elettronica di approvazione"](connectors-create-api-office365-outlook.md) è riportato un esempio di un connettore che segue questo modello. È possibile estendere questo modello in qualsiasi servizio tramite un'azione di hello webhook. 

Di seguito è riportato un esempio che illustra come tooset un webhook di azione in hello progettazione applicazione logica. Questa procedura si presuppone che si hanno già distribuito o se si accede a un'API che segue hello [webhook sottoscrivere e annullare la sottoscrizione criterio usato nell'App per la logica](../logic-apps/logic-apps-create-api-app.md#webhook-actions). Hello sottoscrizione chiamata viene eseguita quando un'app per la logica esegue azioni webhook hello. annullare la sottoscrizione Hello chiamata viene eseguita quando un'esecuzione è stata annullata durante l'attesa di una risposta, o prima della logica di hello app timeout.

**tooadd un'azione webhook**

1. Scegliere **Nuovo passaggio** > **Aggiungi un'azione**.

2. Nella casella di ricerca hello, digitare "webhook" toofind hello **HTTP Webhook** azione.

    ![Selezionare l'azione di query](./media/connectors-native-webhook/using-action-1.png)

3. Specificare i parametri di hello per hello webhook sottoscrivere e annullare la sottoscrizione di chiamate

   Questo passaggio segue hello stesso schema come hello [azione HTTP](connectors-native-http.md) formato.

     ![Completare l'azione di query](./media/connectors-native-webhook/using-action-2.png)
   
   In fase di esecuzione, hello logica app chiamate hello sottoscrizione endpoint dopo il raggiungimento di tale passaggio.

4. Fare clic su **salvare** toopublish hello logica app.

## <a name="technical-details"></a>Dettagli tecnici

Ecco altri dettagli sulle azioni e trigger hello supporta tale webhook.

## <a name="webhook-triggers"></a>Trigger webhook

| Azione | Descrizione |
| --- | --- |
| HTTP Webhook |Effettuare la sottoscrizione di un servizio di tooa URL callback che può chiamare URL toofire logica app hello in base alle esigenze. |

### <a name="trigger-details"></a>Dettagli del trigger

#### <a name="http-webhook"></a>HTTP Webhook

Effettuare la sottoscrizione di un servizio di tooa URL callback che può chiamare URL toofire logica app hello in base alle esigenze.
L'asterisco (*) indica che il campo è obbligatorio.

| Nome visualizzato | Nome proprietà | Descrizione |
| --- | --- | --- |
| Subscribe Method* |statico |Metodo HTTP toouse per la richiesta di sottoscrizione |
| Subscribe URI* |Uri |Toouse URI HTTP per la richiesta di sottoscrizione |
| Unsubscribe Method* |statico |Toouse metodo HTTP per la richiesta di annullamento della sottoscrizione |
| Unsubscribe URI* |Uri |Toouse URI HTTP per la richiesta di annullamento della sottoscrizione |
| Subscribe Body |body |Request body HTTP per la sottoscrizione |
| Subscribe Headers |headers |Intestazioni della richiesta HTTP per la sottoscrizione |
| Subscribe Authentication |authentication |Toouse di autenticazione HTTP per la sottoscrizione. Vedere [Connettore HTTP](connectors-native-http.md#authentication) per informazioni dettagliate |
| Unsubscribe Body |body |Request body HTTP per annullare la sottoscrizione |
| Unsubscribe Headers |headers |Intestazioni della richiesta HTTP per annullare la sottoscrizione |
| Unsubscribe Authentication |authentication |Toouse di autenticazione HTTP per l'annullamento della sottoscrizione. Vedere [Connettore HTTP](connectors-native-http.md#authentication) per informazioni dettagliate |

**Dettagli dell'output**

Richiesta Webhook

| Nome proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| headers |object |Intestazioni della richiesta webhook |
| body |object |Oggetto della richiesta webhook |
| Codice di stato |int |Codice di stato della richiesta webhook |

## <a name="webhook-actions"></a>Azioni webhook

| Azione | Descrizione |
| --- | --- |
| HTTP Webhook |Effettuare la sottoscrizione di un servizio di tooa URL callback che può chiamare hello URL tooresume un passaggio del flusso di lavoro in base alle esigenze. |

### <a name="action-details"></a>Informazioni dettagliate sulle azioni

#### <a name="http-webhook"></a>HTTP Webhook

Effettuare la sottoscrizione di un servizio di tooa URL callback che può chiamare hello URL tooresume un passaggio del flusso di lavoro in base alle esigenze.
L'asterisco (*) indica che il campo è obbligatorio.

| Nome visualizzato | Nome proprietà | Descrizione |
| --- | --- | --- |
| Subscribe Method* |statico |Metodo HTTP toouse per la richiesta di sottoscrizione |
| Subscribe URI* |Uri |Toouse URI HTTP per la richiesta di sottoscrizione |
| Unsubscribe Method* |statico |Toouse metodo HTTP per la richiesta di annullamento della sottoscrizione |
| Unsubscribe URI* |Uri |Toouse URI HTTP per la richiesta di annullamento della sottoscrizione |
| Subscribe Body |body |Request body HTTP per la sottoscrizione |
| Subscribe Headers |headers |Intestazioni della richiesta HTTP per la sottoscrizione |
| Subscribe Authentication |authentication |Toouse di autenticazione HTTP per la sottoscrizione. Vedere [Connettore HTTP](connectors-native-http.md#authentication) per informazioni dettagliate |
| Unsubscribe Body |body |Request body HTTP per annullare la sottoscrizione |
| Unsubscribe Headers |headers |Intestazioni della richiesta HTTP per annullare la sottoscrizione |
| Unsubscribe Authentication |authentication |Toouse di autenticazione HTTP per l'annullamento della sottoscrizione. Vedere [Connettore HTTP](connectors-native-http.md#authentication) per informazioni dettagliate |

**Dettagli dell'output**

Richiesta Webhook

| Nome proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| headers |object |Intestazioni della richiesta webhook |
| body |object |Oggetto della richiesta webhook |
| Codice di stato |int |Codice di stato della richiesta webhook |

## <a name="next-steps"></a>Passaggi successivi

* [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md)
* [Trovare altri connettori](apis-list.md)