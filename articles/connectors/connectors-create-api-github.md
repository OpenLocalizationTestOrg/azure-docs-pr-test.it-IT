---
title: Connettore GitHub per App per la logica di Azure | Microsoft Docs
description: "Creare app per la logica in Servizio app di Azure. GitHub è un servizio di hosting di repository Git basato sul Web. Offre tutte le funzionalità di Git per il controllo delle revisioni distribuite e la gestione del codice sorgente , oltre a diverse funzionalità aggiuntive."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8f873e6c-f4c0-4c2e-a5bd-2e953efe5e2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: d4614b0ceff0ec0d36dbb1a136551f985f2fc1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-github-connector"></a><span data-ttu-id="49ab8-105">Introduzione al connettore GitHub</span><span class="sxs-lookup"><span data-stu-id="49ab8-105">Get started with the GitHub connector</span></span>
<span data-ttu-id="49ab8-106">GitHub è un servizio di hosting di repository Git basato sul Web.</span><span class="sxs-lookup"><span data-stu-id="49ab8-106">GitHub is a web-based Git repository hosting service.</span></span> <span data-ttu-id="49ab8-107">Offre tutte le funzionalità di Git per il controllo delle revisioni distribuite e la gestione del codice sorgente , oltre a diverse funzionalità aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="49ab8-107">It offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features.</span></span>

<span data-ttu-id="49ab8-108">Per iniziare subito a creare un'app per la logica, vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="49ab8-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-github"></a><span data-ttu-id="49ab8-109">Creare una connessione a GitHub</span><span class="sxs-lookup"><span data-stu-id="49ab8-109">Create a connection to GitHub</span></span>
<span data-ttu-id="49ab8-110">Per creare app per la logica con GitHub, è prima necessario creare una **connessione** e quindi indicare i dettagli per le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="49ab8-110">To create Logic apps with GitHub, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="49ab8-111">Proprietà</span><span class="sxs-lookup"><span data-stu-id="49ab8-111">Property</span></span> | <span data-ttu-id="49ab8-112">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="49ab8-112">Required</span></span> | <span data-ttu-id="49ab8-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="49ab8-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49ab8-114">Token</span><span class="sxs-lookup"><span data-stu-id="49ab8-114">Token</span></span> |<span data-ttu-id="49ab8-115">Sì</span><span class="sxs-lookup"><span data-stu-id="49ab8-115">Yes</span></span> |<span data-ttu-id="49ab8-116">Fornisce le credenziali per GitHub</span><span class="sxs-lookup"><span data-stu-id="49ab8-116">Provide GitHub Credentials</span></span> |

<span data-ttu-id="49ab8-117">Dopo aver creato la connessione, è possibile usarla per eseguire le azioni e restare in ascolto dei trigger descritti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="49ab8-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span> 

> [!INCLUDE [Steps to create a connection to GitHub](../../includes/connectors-create-api-github.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="49ab8-118">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="49ab8-118">Connector-specific details</span></span>

<span data-ttu-id="49ab8-119">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/github/).</span><span class="sxs-lookup"><span data-stu-id="49ab8-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/github/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="49ab8-120">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="49ab8-120">More connectors</span></span>
<span data-ttu-id="49ab8-121">Tornare all' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="49ab8-121">Go back to the [APIs list](apis-list.md).</span></span>