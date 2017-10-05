---
title: Aggiungere il connettore Facebook alle app per la logica | Documentazione Microsoft
description: Panoramica del connettore Facebook con i parametri dell'API REST.
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f4d6f0ed-c09b-488c-be1c-8cf2b5b1d4b8
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia; ladocs
ms.openlocfilehash: e10a30ccef3e81cb3d7749696453d82b8958d076
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-facebook-connector"></a><span data-ttu-id="7cc5d-103">Introduzione al connettore Facebook</span><span class="sxs-lookup"><span data-stu-id="7cc5d-103">Get started with the Facebook connector</span></span>
<span data-ttu-id="7cc5d-104">Connettersi a Facebook e pubblicare un post in una sequenza temporale, recuperare il feed di una pagina e così via.</span><span class="sxs-lookup"><span data-stu-id="7cc5d-104">Connect to Facebook and post to a timeline, get a page feed, and more.</span></span> <span data-ttu-id="7cc5d-105">Con Facebook è possibile:</span><span class="sxs-lookup"><span data-stu-id="7cc5d-105">With Facebook, you can:</span></span>

* <span data-ttu-id="7cc5d-106">Creare il flusso aziendale in base ai dati ottenuti da Facebook.</span><span class="sxs-lookup"><span data-stu-id="7cc5d-106">Build your business flow based on the data you get from Facebook.</span></span> 
* <span data-ttu-id="7cc5d-107">Usare un trigger quando si riceve un nuovo post.</span><span class="sxs-lookup"><span data-stu-id="7cc5d-107">Use a trigger when a new post is received.</span></span>
* <span data-ttu-id="7cc5d-108">Usare azioni per pubblicare un post nella sequenza temporale, recuperare il feed di una pagina e così via.</span><span class="sxs-lookup"><span data-stu-id="7cc5d-108">Use actions that post to your timeline, get a page feed, and more.</span></span> <span data-ttu-id="7cc5d-109">Queste azioni ottengono una risposta e quindi rendono l'output disponibile per altre azioni.</span><span class="sxs-lookup"><span data-stu-id="7cc5d-109">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="7cc5d-110">Ad esempio, quando nella sequenza temporale è presente un nuovo post, è possibile selezionare tale post ed eseguirne il push al feed di Twitter.</span><span class="sxs-lookup"><span data-stu-id="7cc5d-110">For example, when there is a new post on your timeline, you can take that post and push it to your Twitter feed.</span></span> 

<span data-ttu-id="7cc5d-111">Per iniziare subito a creare un'app per la logica, vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="7cc5d-111">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-facebook"></a><span data-ttu-id="7cc5d-112">Creare una connessione a Facebook</span><span class="sxs-lookup"><span data-stu-id="7cc5d-112">Create a connection to Facebook</span></span>
<span data-ttu-id="7cc5d-113">Quando si aggiunge questo connettore alle app per la logica, è necessario autorizzare le app per la logica per la connessione a Facebook.</span><span class="sxs-lookup"><span data-stu-id="7cc5d-113">When you add this connector to your logic apps, you must authorize logic apps to connect to your Facebook.</span></span>

1. <span data-ttu-id="7cc5d-114">Accedere al proprio account Facebook</span><span class="sxs-lookup"><span data-stu-id="7cc5d-114">Sign in to your Facebook account</span></span>
2. <span data-ttu-id="7cc5d-115">Selezionare **Autorizza**e consentire alle app per la logica di connettersi e usare Facebook.</span><span class="sxs-lookup"><span data-stu-id="7cc5d-115">Select **Authorize**, and allow your logic apps to connect and use your Facebook.</span></span> 

> [!INCLUDE [Steps to create a connection to Facebook](../../includes/connectors-create-api-facebook.md)]
> 


## <a name="connector-specific-details"></a><span data-ttu-id="7cc5d-116">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="7cc5d-116">Connector-specific details</span></span>

<span data-ttu-id="7cc5d-117">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/facebook/).</span><span class="sxs-lookup"><span data-stu-id="7cc5d-117">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/facebook/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="7cc5d-118">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="7cc5d-118">More connectors</span></span>
<span data-ttu-id="7cc5d-119">Tornare all' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="7cc5d-119">Go back to the [APIs list](apis-list.md).</span></span>