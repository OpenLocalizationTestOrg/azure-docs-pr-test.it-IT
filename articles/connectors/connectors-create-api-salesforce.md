---
title: aaaLearn toouse hello connettore Salesforce nelle App logica | Documenti Microsoft
description: Creare app per la logica con Servizio app di Azure. Hello connettore Salesforce fornisce un'API toowork con gli oggetti di Salesforce.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 54fe5af8-7d2a-4da8-94e7-15d029e029bf
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/05/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b14b41fa8a4648b4f0090472dc0f9575bf13a2ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-salesforce-connector"></a><span data-ttu-id="ca683-104">Iniziare con il connettore Salesforce hello</span><span class="sxs-lookup"><span data-stu-id="ca683-104">Get started with hello Salesforce connector</span></span>
<span data-ttu-id="ca683-105">Hello connettore Salesforce fornisce un'API toowork con gli oggetti di Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ca683-105">hello Salesforce Connector provides an API toowork with Salesforce objects.</span></span>

<span data-ttu-id="ca683-106">toouse [i connettori](apis-list.md), è necessario innanzitutto toocreate un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="ca683-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="ca683-107">Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ca683-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosalesforce-connector"></a><span data-ttu-id="ca683-108">Collegare tooSalesforce connettore</span><span class="sxs-lookup"><span data-stu-id="ca683-108">Connect tooSalesforce connector</span></span>
<span data-ttu-id="ca683-109">Prima che la logica app possa accedere a qualsiasi servizio, è necessario innanzitutto toocreate un *connessione* toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="ca683-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="ca683-110">Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="ca683-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosalesforce-connector"></a><span data-ttu-id="ca683-111">Creare un connettore tooSalesforce connessione</span><span class="sxs-lookup"><span data-stu-id="ca683-111">Create a connection tooSalesforce connector</span></span>
> [!INCLUDE [Steps toocreate a connection tooSalesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="ca683-112">Usare un trigger del connettore Salesforce</span><span class="sxs-lookup"><span data-stu-id="ca683-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="ca683-113">Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="ca683-113">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="ca683-114">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="ca683-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="ca683-115">Add a condition</span><span class="sxs-lookup"><span data-stu-id="ca683-115">Add a condition</span></span>
> [!INCLUDE [Steps toocreate a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="ca683-116">Usare un'azione del connettore Salesforce</span><span class="sxs-lookup"><span data-stu-id="ca683-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="ca683-117">Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="ca683-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="ca683-118">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="ca683-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="ca683-119">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="ca683-119">Connector-specific details</span></span>

<span data-ttu-id="ca683-120">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="ca683-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ca683-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ca683-121">Next steps</span></span>
[<span data-ttu-id="ca683-122">Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="ca683-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

