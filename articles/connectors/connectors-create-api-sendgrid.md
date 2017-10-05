---
title: SendGrid | Microsoft Docs
description: Creare app per la logica in Servizio app di Azure. Il provider di connessione SendGrid consente di inviare messaggi di posta elettronica e gestire elenchi di destinatari.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: bc4f1fc2-824c-4ed7-8de8-e82baff3b746
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 9ff0591741899d65b8274fb14ab3f3c8db9abe36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sendgrid-connector"></a><span data-ttu-id="4a1f7-104">Introduzione al connettore SendGrid</span><span class="sxs-lookup"><span data-stu-id="4a1f7-104">Get started with the SendGrid connector</span></span>
<span data-ttu-id="4a1f7-105">Il provider di connessione SendGrid consente di inviare messaggi di posta elettronica e gestire elenchi di destinatari.</span><span class="sxs-lookup"><span data-stu-id="4a1f7-105">SendGrid Connection Provider lets you send email and manage recipient lists.</span></span>

<span data-ttu-id="4a1f7-106">Per iniziare subito a creare un'app per la logica, vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4a1f7-106">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sendgrid"></a><span data-ttu-id="4a1f7-107">Creare una connessione a SendGrid</span><span class="sxs-lookup"><span data-stu-id="4a1f7-107">Create a connection to SendGrid</span></span>
<span data-ttu-id="4a1f7-108">Per creare app per la logica con SendGrid, è prima necessario creare una **connessione**, quindi fornire i dettagli per le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="4a1f7-108">To create Logic apps with SendGrid, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="4a1f7-109">Proprietà</span><span class="sxs-lookup"><span data-stu-id="4a1f7-109">Property</span></span> | <span data-ttu-id="4a1f7-110">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a1f7-110">Required</span></span> | <span data-ttu-id="4a1f7-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a1f7-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a1f7-112">ApiKey</span><span class="sxs-lookup"><span data-stu-id="4a1f7-112">ApiKey</span></span> |<span data-ttu-id="4a1f7-113">Sì</span><span class="sxs-lookup"><span data-stu-id="4a1f7-113">Yes</span></span> |<span data-ttu-id="4a1f7-114">Fornisce la chiave API per SendGrid</span><span class="sxs-lookup"><span data-stu-id="4a1f7-114">Provide Your SendGrid Api Key</span></span> |

> [!INCLUDE [Steps to create a connection to SendGrid](../../includes/connectors-create-api-sendgrid.md)]
> 


<span data-ttu-id="4a1f7-115">Dopo aver creato la connessione, è possibile usarla per eseguire le azioni e restare in ascolto dei trigger.</span><span class="sxs-lookup"><span data-stu-id="4a1f7-115">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="4a1f7-116">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="4a1f7-116">Connector-specific details</span></span>

<span data-ttu-id="4a1f7-117">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/sendgrid/).</span><span class="sxs-lookup"><span data-stu-id="4a1f7-117">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sendgrid/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="4a1f7-118">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="4a1f7-118">More connectors</span></span>
<span data-ttu-id="4a1f7-119">Tornare all' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="4a1f7-119">Go back to the [APIs list](apis-list.md).</span></span>