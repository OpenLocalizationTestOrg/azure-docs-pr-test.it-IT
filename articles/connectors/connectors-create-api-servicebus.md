---
title: connettore di Azure Service Bus hello toouse aaaLearn nelle App logica | Documenti Microsoft
description: "Creare app per la logica con Servizio app di Azure. Connettersi tooAzure toosend di Bus di servizio e ricevere messaggi. È possibile eseguire azioni come trasmissione tooqueue inviare tootopic, dalla coda la ricezione dalla sottoscrizione."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d6d14f5f-2126-4e33-808e-41de08e6721f
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/02/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c815ac167c3106ade470ce139d119085558a9497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-service-bus-connector"></a>Iniziare con il connettore di Azure Service Bus hello
Connettersi tooAzure toosend di Bus di servizio e ricevere messaggi. È possibile eseguire azioni come trasmissione tooqueue inviare tootopic, dalla coda la ricezione dalla sottoscrizione.

toouse [i connettori](apis-list.md), è necessario innanzitutto toocreate un'app di logica. Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooservice-bus"></a>Connettersi tooService Bus
Prima che la logica app possa accedere a qualsiasi servizio, è necessario innanzitutto toocreate un servizio toohello di connessione. Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a>Usare un trigger di bus di servizio
Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica. [Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a>Usare un'azione del bus di servizio
Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica. [Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/servicebus/). 

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).

