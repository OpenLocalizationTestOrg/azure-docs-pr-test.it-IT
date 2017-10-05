---
title: Connettore Wunderlist nelle app per la logica di Azure | Microsoft Docs
description: Creare una connessione a Wunderlist e usarla per creare il flusso di lavoro nelle app per la logica.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: e4773ecf-3ad3-44b4-a1b5-ee5f58baeadd
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 899110992cc52ca5edf1706320fd5570473de784
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-wunderlist-connector"></a><span data-ttu-id="a47e9-103">Introduzione al connettore Wunderlist</span><span class="sxs-lookup"><span data-stu-id="a47e9-103">Get started with the Wunderlist connector</span></span>
<span data-ttu-id="a47e9-104">Wunderlist fornisce un elenco di attività e uno strumento di gestione attività per aiutare le persone a portare a termine ciò che devono fare.</span><span class="sxs-lookup"><span data-stu-id="a47e9-104">Wunderlist provide a todo list and task manager to help people get their stuff done.</span></span>  <span data-ttu-id="a47e9-105">Che si tratti di condividere una lista della spesa con un familiare, lavorare a un progetto o pianificare una vacanza, Wunderlist consente di acquisire, condividere e completare le attività da svolgere in modo semplice.</span><span class="sxs-lookup"><span data-stu-id="a47e9-105">Whether you’re sharing a grocery list with a loved one, working on a project, or planning a vacation, Wunderlist makes it easy to capture, share, and complete your to¬dos.</span></span> <span data-ttu-id="a47e9-106">Wunderlist esegue immediatamente la sincronizzazione tra il telefono, il tablet e il computer, per consentire l'accesso a tutte le attività da qualsiasi posizione.</span><span class="sxs-lookup"><span data-stu-id="a47e9-106">Wunderlist instantly syncs between your phone, tablet and computer, so you can access all your tasks from anywhere.</span></span>

<span data-ttu-id="a47e9-107">Creare prima di tutto un'app per la logica. Vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a47e9-107">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-wunderlist"></a><span data-ttu-id="a47e9-108">Creare una connessione a Wunderlist</span><span class="sxs-lookup"><span data-stu-id="a47e9-108">Create a connection to Wunderlist</span></span>
<span data-ttu-id="a47e9-109">Per creare app per la logica con Wunderlist, è prima necessario creare una **connessione** e quindi fornire i dettagli per le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="a47e9-109">To create Logic apps with Wunderlist, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="a47e9-110">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a47e9-110">Property</span></span> | <span data-ttu-id="a47e9-111">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a47e9-111">Required</span></span> | <span data-ttu-id="a47e9-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a47e9-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a47e9-113">Token</span><span class="sxs-lookup"><span data-stu-id="a47e9-113">Token</span></span> |<span data-ttu-id="a47e9-114">Sì</span><span class="sxs-lookup"><span data-stu-id="a47e9-114">Yes</span></span> |<span data-ttu-id="a47e9-115">Fornisce le credenziali di Wunderlist</span><span class="sxs-lookup"><span data-stu-id="a47e9-115">Provide Wunderlist Credentials</span></span> |

<span data-ttu-id="a47e9-116">Dopo aver creato la connessione, è possibile usarla per eseguire le azioni e restare in ascolto dei trigger.</span><span class="sxs-lookup"><span data-stu-id="a47e9-116">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

> [!INCLUDE [Steps to create a connection to Wunderlist](../../includes/connectors-create-api-wunderlist.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="a47e9-117">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="a47e9-117">Connector-specific details</span></span>

<span data-ttu-id="a47e9-118">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/wunderlist/).</span><span class="sxs-lookup"><span data-stu-id="a47e9-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/wunderlist/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="a47e9-119">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="a47e9-119">More connectors</span></span>
<span data-ttu-id="a47e9-120">Tornare all' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="a47e9-120">Go back to the [APIs list](apis-list.md).</span></span>