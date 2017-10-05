---
title: Informazioni su come usare il connettore del bus di servizio di Azure nelle app per la logica | Documentazione Microsoft
description: "Creare app per la logica con Servizio app di Azure. Connettersi al bus di servizio di Azure per inviare e ricevere messaggi. È possibile eseguire varie azioni, ad esempio inviare alla coda, inviare all'argomento, ricevere dalla coda e ricevere dalla sottoscrizione."
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
ms.openlocfilehash: 1e2ce06f5993280dbdb67121849591e67f7979e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-service-bus-connector"></a><span data-ttu-id="0b921-105">Introduzione al connettore del bus di servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="0b921-105">Get started with the Azure Service Bus connector</span></span>
<span data-ttu-id="0b921-106">Connettersi al bus di servizio di Azure per inviare e ricevere messaggi.</span><span class="sxs-lookup"><span data-stu-id="0b921-106">Connect to Azure Service Bus to send and receive messages.</span></span> <span data-ttu-id="0b921-107">È possibile eseguire varie azioni, ad esempio inviare alla coda, inviare all'argomento, ricevere dalla coda e ricevere dalla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0b921-107">You can perform actions such as send to queue, send to topic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="0b921-108">Per usare [qualsiasi connettore](apis-list.md), è necessario innanzitutto creare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="0b921-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="0b921-109">Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0b921-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-service-bus"></a><span data-ttu-id="0b921-110">Connettersi al bus di servizio</span><span class="sxs-lookup"><span data-stu-id="0b921-110">Connect to Service Bus</span></span>
<span data-ttu-id="0b921-111">Perché l'app per la logica possa accedere a qualsiasi servizio, è necessario creare una connessione al servizio.</span><span class="sxs-lookup"><span data-stu-id="0b921-111">Before your logic app can access any service, you first need to create a connection to the service.</span></span> <span data-ttu-id="0b921-112">Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="0b921-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps to create a connection to Azure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="0b921-113">Usare un trigger di bus di servizio</span><span class="sxs-lookup"><span data-stu-id="0b921-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="0b921-114">Un trigger è un evento che può essere usato per avviare il flusso di lavoro definito in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="0b921-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="0b921-115">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="0b921-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="0b921-116">Usare un'azione del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="0b921-116">Use a Service Bus action</span></span>
<span data-ttu-id="0b921-117">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="0b921-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="0b921-118">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="0b921-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps to create a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="0b921-119">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="0b921-119">Connector-specific details</span></span>

<span data-ttu-id="0b921-120">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="0b921-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0b921-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0b921-121">Next steps</span></span>
<span data-ttu-id="0b921-122">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0b921-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

