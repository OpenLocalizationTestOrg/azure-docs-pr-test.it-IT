---
title: Informazioni su come usare il connettore SharePoint Online nelle app per la logica | Documentazione Microsoft
description: Creare app per la logica con il connettore SharePoint Online per la gestione degli elenchi SharePoint.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: e0ec3149-507a-409d-8e7b-d5fbded006ce
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 96fc1347604c0c6cc2c2463a5dbd83b560183a16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-online-connector"></a><span data-ttu-id="5e392-103">Introduzione al connettore SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="5e392-103">Get started with the SharePoint Online connector</span></span>
<span data-ttu-id="5e392-104">Usare il connettore SharePoint Online per gestire gli elenchi SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5e392-104">Use the SharePoint Online connector to manage SharePoint lists.</span></span>  

<span data-ttu-id="5e392-105">Per usare [qualsiasi connettore](apis-list.md), è necessario innanzitutto creare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="5e392-105">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="5e392-106">Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5e392-106">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sharepoint-online"></a><span data-ttu-id="5e392-107">Connettersi a SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="5e392-107">Connect to SharePoint Online</span></span>
<span data-ttu-id="5e392-108">Perché l'app per la logica possa accedere a qualsiasi servizio, è necessario creare una *connessione* al servizio.</span><span class="sxs-lookup"><span data-stu-id="5e392-108">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="5e392-109">Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="5e392-109">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sharepoint-online"></a><span data-ttu-id="5e392-110">Creare una connessione a SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="5e392-110">Create a connection to SharePoint Online</span></span>
> [!INCLUDE [Steps to create a connection to SharePoint](../../includes/connectors-create-api-sharepointonline.md)]


## <a name="use-a-sharepoint-online-trigger"></a><span data-ttu-id="5e392-111">Usare un trigger di SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="5e392-111">Use a SharePoint Online trigger</span></span>
<span data-ttu-id="5e392-112">Un trigger è un evento che può essere usato per avviare il flusso di lavoro definito in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="5e392-112">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="5e392-113">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="5e392-113">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a SharePoint Online trigger](../../includes/connectors-create-api-sharepointonline-trigger.md)]


## <a name="use-a-sharepoint-online-action"></a><span data-ttu-id="5e392-114">Usare un'azione di SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="5e392-114">Use a SharePoint Online action</span></span>
<span data-ttu-id="5e392-115">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="5e392-115">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="5e392-116">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="5e392-116">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a SharePoint Online action](../../includes/connectors-create-api-sharepointonline-action.md)]


## <a name="connector-specific-details"></a><span data-ttu-id="5e392-117">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="5e392-117">Connector-specific details</span></span>

<span data-ttu-id="5e392-118">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="5e392-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e392-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5e392-119">Next Steps</span></span>
[<span data-ttu-id="5e392-120">Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="5e392-120">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

