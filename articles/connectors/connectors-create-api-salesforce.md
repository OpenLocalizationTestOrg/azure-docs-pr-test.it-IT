---
title: Informazioni su come usare il connettore Salesforce nelle app per la logica | Microsoft Docs
description: Creare app per la logica con Servizio app di Azure. Il connettore Salesforce offre un'API per lavorare con gli oggetti Salesforce.
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
ms.openlocfilehash: c2e2efd356382df9404f5c4ed54f24758b2cd22b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-salesforce-connector"></a><span data-ttu-id="38d08-104">Introduzione al connettore Salesforce</span><span class="sxs-lookup"><span data-stu-id="38d08-104">Get started with the Salesforce connector</span></span>
<span data-ttu-id="38d08-105">Il connettore Salesforce offre un'API per lavorare con gli oggetti Salesforce.</span><span class="sxs-lookup"><span data-stu-id="38d08-105">The Salesforce Connector provides an API to work with Salesforce objects.</span></span>

<span data-ttu-id="38d08-106">Per usare [qualsiasi connettore](apis-list.md), è necessario innanzitutto creare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="38d08-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="38d08-107">Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="38d08-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-salesforce-connector"></a><span data-ttu-id="38d08-108">Connettersi al connettore Salesforce</span><span class="sxs-lookup"><span data-stu-id="38d08-108">Connect to Salesforce connector</span></span>
<span data-ttu-id="38d08-109">Perché l'app per la logica possa accedere a qualsiasi servizio, è necessario creare una *connessione* al servizio.</span><span class="sxs-lookup"><span data-stu-id="38d08-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="38d08-110">Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="38d08-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-salesforce-connector"></a><span data-ttu-id="38d08-111">Creare una connessione al connettore Salesforce</span><span class="sxs-lookup"><span data-stu-id="38d08-111">Create a connection to Salesforce connector</span></span>
> [!INCLUDE [Steps to create a connection to Salesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="38d08-112">Usare un trigger del connettore Salesforce</span><span class="sxs-lookup"><span data-stu-id="38d08-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="38d08-113">Un trigger è un evento che può essere usato per avviare il flusso di lavoro definito in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="38d08-113">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="38d08-114">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="38d08-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="38d08-115">Add a condition</span><span class="sxs-lookup"><span data-stu-id="38d08-115">Add a condition</span></span>
> [!INCLUDE [Steps to create a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="38d08-116">Usare un'azione del connettore Salesforce</span><span class="sxs-lookup"><span data-stu-id="38d08-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="38d08-117">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="38d08-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="38d08-118">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="38d08-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="38d08-119">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="38d08-119">Connector-specific details</span></span>

<span data-ttu-id="38d08-120">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="38d08-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="38d08-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38d08-121">Next steps</span></span>
[<span data-ttu-id="38d08-122">Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="38d08-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

