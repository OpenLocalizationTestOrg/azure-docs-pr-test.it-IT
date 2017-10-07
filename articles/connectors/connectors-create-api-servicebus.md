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
# <a name="get-started-with-hello-azure-service-bus-connector"></a><span data-ttu-id="4a5f0-105">Iniziare con il connettore di Azure Service Bus hello</span><span class="sxs-lookup"><span data-stu-id="4a5f0-105">Get started with hello Azure Service Bus connector</span></span>
<span data-ttu-id="4a5f0-106">Connettersi tooAzure toosend di Bus di servizio e ricevere messaggi.</span><span class="sxs-lookup"><span data-stu-id="4a5f0-106">Connect tooAzure Service Bus toosend and receive messages.</span></span> <span data-ttu-id="4a5f0-107">È possibile eseguire azioni come trasmissione tooqueue inviare tootopic, dalla coda la ricezione dalla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4a5f0-107">You can perform actions such as send tooqueue, send tootopic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="4a5f0-108">toouse [i connettori](apis-list.md), è necessario innanzitutto toocreate un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="4a5f0-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="4a5f0-109">Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4a5f0-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooservice-bus"></a><span data-ttu-id="4a5f0-110">Connettersi tooService Bus</span><span class="sxs-lookup"><span data-stu-id="4a5f0-110">Connect tooService Bus</span></span>
<span data-ttu-id="4a5f0-111">Prima che la logica app possa accedere a qualsiasi servizio, è necessario innanzitutto toocreate un servizio toohello di connessione.</span><span class="sxs-lookup"><span data-stu-id="4a5f0-111">Before your logic app can access any service, you first need toocreate a connection toohello service.</span></span> <span data-ttu-id="4a5f0-112">Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="4a5f0-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="4a5f0-113">Usare un trigger di bus di servizio</span><span class="sxs-lookup"><span data-stu-id="4a5f0-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="4a5f0-114">Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="4a5f0-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="4a5f0-115">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="4a5f0-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="4a5f0-116">Usare un'azione del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="4a5f0-116">Use a Service Bus action</span></span>
<span data-ttu-id="4a5f0-117">Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="4a5f0-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="4a5f0-118">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="4a5f0-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="4a5f0-119">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="4a5f0-119">Connector-specific details</span></span>

<span data-ttu-id="4a5f0-120">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="4a5f0-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4a5f0-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4a5f0-121">Next steps</span></span>
<span data-ttu-id="4a5f0-122">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4a5f0-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

