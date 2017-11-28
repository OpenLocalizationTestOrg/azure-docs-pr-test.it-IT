---
title: aaaAdd hello connettore Twilio in App per la logica di Azure | Documenti Microsoft
description: Panoramica di hello connettore Twilio con i parametri di API REST
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
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a><span data-ttu-id="d5b4a-103">Iniziare con il connettore di Twilio hello</span><span class="sxs-lookup"><span data-stu-id="d5b4a-103">Get started with hello Twilio connector</span></span>
<span data-ttu-id="d5b4a-104">Connettersi tooTwilio toosend e ricevere i messaggi SMS e MMS IP globali.</span><span class="sxs-lookup"><span data-stu-id="d5b4a-104">Connect tooTwilio toosend and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="d5b4a-105">Con Twilio è possibile:</span><span class="sxs-lookup"><span data-stu-id="d5b4a-105">With Twilio, you can:</span></span>

* <span data-ttu-id="d5b4a-106">Compilare il flusso di business in base ai dati hello che si ottiene da Twilio.</span><span class="sxs-lookup"><span data-stu-id="d5b4a-106">Build your business flow based on hello data you get from Twilio.</span></span> 
* <span data-ttu-id="d5b4a-107">Usare le azioni per recuperare un messaggio, elencare i messaggi e così via.</span><span class="sxs-lookup"><span data-stu-id="d5b4a-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="d5b4a-108">Tali azioni ottengono una risposta e quindi apportare output di hello per le altre azioni.</span><span class="sxs-lookup"><span data-stu-id="d5b4a-108">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="d5b4a-109">Ad esempio, quando si recupera un nuovo messaggio di Twilio, è possibile usarlo come flusso di lavoro del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="d5b4a-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="d5b4a-110">Creare prima di tutto un'app per la logica. Vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d5b4a-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tootwilio"></a><span data-ttu-id="d5b4a-111">Creare una connessione tooTwilio</span><span class="sxs-lookup"><span data-stu-id="d5b4a-111">Create a connection tooTwilio</span></span>
<span data-ttu-id="d5b4a-112">Quando si aggiunge questa App per la logica tooyour connettore, immettere hello Twilio valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="d5b4a-112">When you add this Connector tooyour logic apps, enter hello following Twilio values:</span></span>

| <span data-ttu-id="d5b4a-113">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d5b4a-113">Property</span></span> | <span data-ttu-id="d5b4a-114">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d5b4a-114">Required</span></span> | <span data-ttu-id="d5b4a-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d5b4a-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5b4a-116">Account ID</span><span class="sxs-lookup"><span data-stu-id="d5b4a-116">Account ID</span></span> |<span data-ttu-id="d5b4a-117">Sì</span><span class="sxs-lookup"><span data-stu-id="d5b4a-117">Yes</span></span> |<span data-ttu-id="d5b4a-118">Immettere l'ID dell'account Twilio</span><span class="sxs-lookup"><span data-stu-id="d5b4a-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="d5b4a-119">Access Token</span><span class="sxs-lookup"><span data-stu-id="d5b4a-119">Access Token</span></span> |<span data-ttu-id="d5b4a-120">Sì</span><span class="sxs-lookup"><span data-stu-id="d5b4a-120">Yes</span></span> |<span data-ttu-id="d5b4a-121">Immettere Il token di accesso di Twilio</span><span class="sxs-lookup"><span data-stu-id="d5b4a-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="d5b4a-122">Se non è disponibile un token di accesso di Twilio, vedere [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity) (Identità utente e token di accesso).</span><span class="sxs-lookup"><span data-stu-id="d5b4a-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="d5b4a-123">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="d5b4a-123">Connector-specific details</span></span>

<span data-ttu-id="d5b4a-124">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="d5b4a-124">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="d5b4a-125">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="d5b4a-125">More connectors</span></span>
<span data-ttu-id="d5b4a-126">Tornare indietro toohello [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d5b4a-126">Go back toohello [APIs list](apis-list.md).</span></span>
