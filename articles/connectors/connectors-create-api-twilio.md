---
title: Aggiungere il connettore Twilio alle app per la logica di Azure | Microsoft Docs
description: Panoramica del connettore Twilio con i parametri dell'API REST
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
ms.openlocfilehash: a790ac51b0fea7e3fa379d20e0e094e7ce0d7696
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twilio-connector"></a><span data-ttu-id="1accf-103">Introduzione al connettore Twilio</span><span class="sxs-lookup"><span data-stu-id="1accf-103">Get started with the Twilio connector</span></span>
<span data-ttu-id="1accf-104">Connettersi a Twilio per inviare e ricevere messaggi SMS, MMS e IP globali.</span><span class="sxs-lookup"><span data-stu-id="1accf-104">Connect to Twilio to send and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="1accf-105">Con Twilio è possibile:</span><span class="sxs-lookup"><span data-stu-id="1accf-105">With Twilio, you can:</span></span>

* <span data-ttu-id="1accf-106">Creare il flusso aziendale in base ai dati ottenuti da Twilio.</span><span class="sxs-lookup"><span data-stu-id="1accf-106">Build your business flow based on the data you get from Twilio.</span></span> 
* <span data-ttu-id="1accf-107">Usare le azioni per recuperare un messaggio, elencare i messaggi e così via.</span><span class="sxs-lookup"><span data-stu-id="1accf-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="1accf-108">Queste azioni ottengono una risposta e quindi rendono l'output disponibile per altre azioni.</span><span class="sxs-lookup"><span data-stu-id="1accf-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="1accf-109">Ad esempio, quando si recupera un nuovo messaggio di Twilio, è possibile usarlo come flusso di lavoro del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="1accf-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="1accf-110">Creare prima di tutto un'app per la logica. Vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1accf-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-twilio"></a><span data-ttu-id="1accf-111">Creare una connessione a Twilio</span><span class="sxs-lookup"><span data-stu-id="1accf-111">Create a connection to Twilio</span></span>
<span data-ttu-id="1accf-112">Quando si aggiunge questo connettore alle app per la logica, immettere i valori di Twilio seguenti:</span><span class="sxs-lookup"><span data-stu-id="1accf-112">When you add this Connector to your logic apps, enter the following Twilio values:</span></span>

| <span data-ttu-id="1accf-113">Proprietà</span><span class="sxs-lookup"><span data-stu-id="1accf-113">Property</span></span> | <span data-ttu-id="1accf-114">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="1accf-114">Required</span></span> | <span data-ttu-id="1accf-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1accf-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1accf-116">Account ID</span><span class="sxs-lookup"><span data-stu-id="1accf-116">Account ID</span></span> |<span data-ttu-id="1accf-117">Sì</span><span class="sxs-lookup"><span data-stu-id="1accf-117">Yes</span></span> |<span data-ttu-id="1accf-118">Immettere l'ID dell'account Twilio</span><span class="sxs-lookup"><span data-stu-id="1accf-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="1accf-119">Access Token</span><span class="sxs-lookup"><span data-stu-id="1accf-119">Access Token</span></span> |<span data-ttu-id="1accf-120">Sì</span><span class="sxs-lookup"><span data-stu-id="1accf-120">Yes</span></span> |<span data-ttu-id="1accf-121">Immettere Il token di accesso di Twilio</span><span class="sxs-lookup"><span data-stu-id="1accf-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps to create a connection to Twilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="1accf-122">Se non è disponibile un token di accesso di Twilio, vedere [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity) (Identità utente e token di accesso).</span><span class="sxs-lookup"><span data-stu-id="1accf-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="1accf-123">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="1accf-123">Connector-specific details</span></span>

<span data-ttu-id="1accf-124">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="1accf-124">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="1accf-125">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="1accf-125">More connectors</span></span>
<span data-ttu-id="1accf-126">Tornare all' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="1accf-126">Go back to the [APIs list](apis-list.md).</span></span>