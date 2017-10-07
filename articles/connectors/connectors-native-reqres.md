---
title: azioni di richiesta e risposta aaaUse | Documenti Microsoft
description: Panoramica di trigger di richiesta e risposta hello e azione in un'applicazione Azure logica
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a>Iniziare con i componenti di richiesta e risposta hello
Con hello richiesta e risposta componenti in un'app di logica, è possibile rispondere in tempo reale tooevents.

Ad esempio, è possibile:

* Rispondere tooan di richiesta HTTP con i dati da un database locale tramite un'app di logica.
* Attivare un'app per la logica da un evento webhook esterno.
* Chiamare un'app per la logica con un'azione di richiesta e risposta dall'interno di un'altra app per la logica.

tooget avviate tramite operazioni di richiesta e risposta hello in un'app di logica, vedere [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-request-trigger"></a>Utilizzare trigger di richiesta HTTP hello
Un trigger è un evento che può essere utilizzato toostart hello flusso di lavoro che è definito in un'app di logica. [Altre informazioni sui trigger](connectors-overview.md).

Di seguito è riportata una sequenza di esempio di come tooset backup HTTP richiesta in Progettazione applicazione logica hello.

1. Aggiungere trigger hello **richiesta - viene ricevuta la richiesta HTTP quando** nell'app logica. È anche possibile specificare uno schema JSON (utilizzando uno strumento come [JSONSchema.net](http://jsonschema.net)) per il corpo della richiesta hello. In questo modo i token della finestra di progettazione toogenerate hello per le proprietà nella richiesta HTTP hello.
2. Aggiungere un'altra operazione in modo che sia possibile salvare hello logica app.
3. Dopo aver salvato hello logica app, è possibile ottenere l'URL della richiesta HTTP hello dalla scheda richiesta hello.
4. Un POST HTTP (è possibile utilizzare uno strumento come [Postman](https://www.getpostman.com/)) trigger URL toohello hello logica app.

> [!NOTE]
> Se non si definisce un'azione di risposta, un `202 ACCEPTED` risposta viene restituita immediatamente toohello chiamante. È possibile utilizzare hello risposta azione toocustomize una risposta.
> 
> 

![Trigger di risposta](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a>Utilizzare l'azione di risposta HTTP hello
azione di risposta HTTP Hello è valida solo quando si usa un flusso di lavoro attivato da una richiesta HTTP. Se non si definisce un'azione di risposta, un `202 ACCEPTED` risposta viene restituita immediatamente toohello chiamante.  È possibile aggiungere un'azione di risposta in un passaggio all'interno del flusso di lavoro di hello. app per la logica Hello mantiene solo aperta richiesta in ingresso hello per un minuto per una risposta.  Dopo un minuto, se è stata inviata alcuna risposta dal flusso di lavoro hello (e un'azione di risposta è presente nella definizione di hello), un `504 GATEWAY TIMEOUT` viene restituito toohello chiamante.

Ecco come tooadd un'azione di risposta HTTP:

1. Seleziona hello **nuovo passaggio** pulsante.
2. Selezionare **Aggiungi un'azione**.
3. Nella casella di ricerca azione hello, digitare **risposta** hello toolist azione di risposta.
   
    ![Selezionare l'azione di risposta hello](./media/connectors-native-reqres/using-action-1.png)
4. Aggiungere i parametri necessari per il messaggio di risposta HTTP hello.
   
    ![Azione di risposta hello completo](./media/connectors-native-reqres/using-action-2.png)
5. Fare clic su nell'angolo superiore sinistro hello di hello barra degli strumenti toosave e la logica app verrà entrambi salvare e pubblicare (attivare).

## <a name="request-trigger"></a>Trigger di richiesta
Ecco i dettagli di hello per trigger hello che supporta il connettore. È disponibile un solo trigger di richiesta.

| Trigger | Descrizione |
| --- | --- |
| Richiesta |Si verifica quando viene ricevuta una richiesta HTTP |

## <a name="response-action"></a>Azione di risposta
Ecco hello dettagli per l'azione di hello che supporta questo connettore. Esiste una sola azione di risposta che può essere usata solo quando è accompagnata da un trigger di richiesta.

| Azione | Descrizione |
| --- | --- |
| Response |Restituisce che una risposta toohello correlati richiesta HTTP |

### <a name="trigger-and-action-details"></a>Dettagli sui trigger e le azioni
Hello nelle tabelle seguenti vengono descritti i campi di input hello per trigger hello e l'azione e hello dettagli output corrispondenti.

#### <a name="request-trigger"></a>Trigger di richiesta
di seguito Hello è un campo di input per il trigger hello da una richiesta HTTP in ingresso.

| Nome visualizzato | Nome proprietà | Descrizione |
| --- | --- | --- |
| Schema JSON |schema |schema JSON Hello del corpo della richiesta HTTP hello |

<br>

**Dettagli dell'output**

di seguito Hello sono i dettagli di output per la richiesta di hello.

| Nome proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| headers |object |Intestazioni della richiesta |
| Corpo |object |Oggetto della richiesta |

#### <a name="response-action"></a>Azione di risposta
di seguito Hello sono campi di input per hello azione di risposta HTTP. Un asterisco (*) indica che è un campo obbligatorio.

| Nome visualizzato | Nome proprietà | Descrizione |
| --- | --- | --- |
| Codice di stato* |statusCode |codice di stato HTTP Hello |
| Headers |headers |Un oggetto JSON di qualsiasi tooinclude di intestazioni di risposta |
| Corpo |body |corpo della risposta Hello |

## <a name="next-steps"></a>Passaggi successivi
A questo punto, provare a piattaforma hello e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md). È possibile esplorare altri connettori disponibile in App per la logica di hello esaminando il nostro [elenco API](apis-list.md).

