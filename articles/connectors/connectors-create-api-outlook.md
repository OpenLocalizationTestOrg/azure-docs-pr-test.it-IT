---
title: Connettore Outlook.com in App per la logica di Azure | Microsoft Docs
description: "Creare app per la logica in Servizio app di Azure. Il connettore Outlook.com consente di gestire la posta elettronica, i calendari e i contatti. Consente anche di eseguire diverse azioni, ad esempio inviare messaggi, pianificare riunioni, aggiungere contatti e così via."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 87113c85-d158-4dd5-9ed5-5748130003d6
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: bde1629504c97cf6706b42219570ffa6243073dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-outlookcom-connector"></a><span data-ttu-id="38422-105">Introduzione al connettore Outlook.com</span><span class="sxs-lookup"><span data-stu-id="38422-105">Get started with the Outlook.com connector</span></span>
<span data-ttu-id="38422-106">Il connettore Outlook.com consente di gestire la posta elettronica, i calendari e i contatti.</span><span class="sxs-lookup"><span data-stu-id="38422-106">Outlook.com connector allows you to manage your mail, calendars, and contacts.</span></span> <span data-ttu-id="38422-107">Consente anche di eseguire diverse azioni, ad esempio inviare messaggi, pianificare riunioni, aggiungere contatti e così via.</span><span class="sxs-lookup"><span data-stu-id="38422-107">You can perform various actions such as send mail, schedule meetings, add contacts, etc.</span></span>

<span data-ttu-id="38422-108">Per iniziare subito a creare un'app per la logica, vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="38422-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-outlookcom"></a><span data-ttu-id="38422-109">Creare una connessione a Outlook.com</span><span class="sxs-lookup"><span data-stu-id="38422-109">Create a connection to Outlook.com</span></span>
<span data-ttu-id="38422-110">Per creare app per la logica con Outlook.com, è prima necessario creare una **connessione** e quindi specificare i dettagli per le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="38422-110">To create Logic apps with Outlook.com, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="38422-111">Proprietà</span><span class="sxs-lookup"><span data-stu-id="38422-111">Property</span></span> | <span data-ttu-id="38422-112">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="38422-112">Required</span></span> | <span data-ttu-id="38422-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="38422-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38422-114">Token</span><span class="sxs-lookup"><span data-stu-id="38422-114">Token</span></span> |<span data-ttu-id="38422-115">Sì</span><span class="sxs-lookup"><span data-stu-id="38422-115">Yes</span></span> |<span data-ttu-id="38422-116">Fornisce le credenziali di Outlook.com</span><span class="sxs-lookup"><span data-stu-id="38422-116">Provide Outlook.com Credentials</span></span> |

<span data-ttu-id="38422-117">Dopo aver creato la connessione, è possibile usarla per eseguire le azioni e restare in ascolto dei trigger descritti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="38422-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span>

> [!INCLUDE [Steps to create a connection to Outlook.com](../../includes/connectors-create-api-outlook.md)]
>

## <a name="connector-specific-details"></a><span data-ttu-id="38422-118">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="38422-118">Connector-specific details</span></span>

<span data-ttu-id="38422-119">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/outlook/).</span><span class="sxs-lookup"><span data-stu-id="38422-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/outlook/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="38422-120">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="38422-120">More connectors</span></span>
<span data-ttu-id="38422-121">Tornare all' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="38422-121">Go back to the [APIs list](apis-list.md).</span></span>