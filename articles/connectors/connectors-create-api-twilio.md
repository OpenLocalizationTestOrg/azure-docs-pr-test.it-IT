---
title: aaaAdd hello connettore Twilio in App per la logica di Azure | Documenti Microsoft
description: Panoramica di hello connettore Twilio con i parametri di API REST
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a>Iniziare con il connettore di Twilio hello
Connettersi tooTwilio toosend e ricevere i messaggi SMS e MMS IP globali. Con Twilio è possibile:

* Compilare il flusso di business in base ai dati hello che si ottiene da Twilio. 
* Usare le azioni per recuperare un messaggio, elencare i messaggi e così via. Tali azioni ottengono una risposta e quindi apportare output di hello per le altre azioni. Ad esempio, quando si recupera un nuovo messaggio di Twilio, è possibile usarlo come flusso di lavoro del bus di servizio. 

Creare prima di tutto un'app per la logica. Vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-tootwilio"></a>Creare una connessione tooTwilio
Quando si aggiunge questa App per la logica tooyour connettore, immettere hello Twilio valori seguenti:

| Proprietà | Obbligatorio | Descrizione |
| --- | --- | --- |
| Account ID |Sì |Immettere l'ID dell'account Twilio |
| Access Token |Sì |Immettere Il token di accesso di Twilio |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

Se non è disponibile un token di accesso di Twilio, vedere [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity) (Identità utente e token di accesso).

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/twilio/).

## <a name="more-connectors"></a>Altri connettori
Tornare indietro toohello [elenco API](apis-list.md).
