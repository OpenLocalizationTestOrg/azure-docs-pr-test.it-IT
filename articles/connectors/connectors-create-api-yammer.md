---
title: Aggiungere il connettore Yammer alle app per la logica di Azure | Microsoft Docs
description: Panoramica del connettore Yammer con i parametri dell'API REST
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5ae0827-fbb3-45ec-8f45-ad1cc2e7eccc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c7a213343b4fb2b5a89a5052a459061b404a431c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-yammer-connector"></a><span data-ttu-id="f8f90-103">Introduzione al connettore Yammer</span><span class="sxs-lookup"><span data-stu-id="f8f90-103">Get started with the Yammer connector</span></span>
<span data-ttu-id="f8f90-104">Connettersi a Yammer per accedere alle conversazioni della rete dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="f8f90-104">Connect to Yammer to access conversations in your enterprise network.</span></span> <span data-ttu-id="f8f90-105">Con Yammer è possibile:</span><span class="sxs-lookup"><span data-stu-id="f8f90-105">With Yammer, you can:</span></span>

* <span data-ttu-id="f8f90-106">Creare il flusso aziendale in base ai dati ottenuti da Yammer.</span><span class="sxs-lookup"><span data-stu-id="f8f90-106">Build your business flow based on the data you get from Yammer.</span></span> 
* <span data-ttu-id="f8f90-107">Usare i trigger quando c'è un nuovo messaggio in un gruppo o un feed che si sta seguendo.</span><span class="sxs-lookup"><span data-stu-id="f8f90-107">Use triggers for when there is a new message in a group, or a feed your following.</span></span>
* <span data-ttu-id="f8f90-108">Usare le azioni per pubblicare un messaggio, recuperare tutti i messaggi e così via.</span><span class="sxs-lookup"><span data-stu-id="f8f90-108">Use actions to post a message, get all messages, and more.</span></span> <span data-ttu-id="f8f90-109">Queste azioni ottengono una risposta e quindi rendono l'output disponibile per altre azioni.</span><span class="sxs-lookup"><span data-stu-id="f8f90-109">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="f8f90-110">Ad esempio, quando viene visualizzato un nuovo messaggio, è possibile inviare un messaggio di posta elettronica tramite Office 365.</span><span class="sxs-lookup"><span data-stu-id="f8f90-110">For example, when a new message appears, you can send an email using Office 365.</span></span>

<span data-ttu-id="f8f90-111">Creare prima di tutto un'app per la logica. Vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f8f90-111">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-yammer"></a><span data-ttu-id="f8f90-112">Creare una connessione a Yammer</span><span class="sxs-lookup"><span data-stu-id="f8f90-112">Create a connection to Yammer</span></span>
<span data-ttu-id="f8f90-113">Per usare il connettore Yammer, creare prima una **connessione**, quindi specificare i dettagli di queste proprietà:</span><span class="sxs-lookup"><span data-stu-id="f8f90-113">To use the Yammer connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="f8f90-114">Proprietà</span><span class="sxs-lookup"><span data-stu-id="f8f90-114">Property</span></span> | <span data-ttu-id="f8f90-115">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="f8f90-115">Required</span></span> | <span data-ttu-id="f8f90-116">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f8f90-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f8f90-117">Token</span><span class="sxs-lookup"><span data-stu-id="f8f90-117">Token</span></span> |<span data-ttu-id="f8f90-118">Sì</span><span class="sxs-lookup"><span data-stu-id="f8f90-118">Yes</span></span> |<span data-ttu-id="f8f90-119">Specificare le credenziali di Yammer</span><span class="sxs-lookup"><span data-stu-id="f8f90-119">Provide Yammer Credentials</span></span> |

> [!INCLUDE [Steps to create a connection to Yammer](../../includes/connectors-create-api-yammer.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="f8f90-120">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="f8f90-120">Connector-specific details</span></span>

<span data-ttu-id="f8f90-121">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/yammer/).</span><span class="sxs-lookup"><span data-stu-id="f8f90-121">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/yammer/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="f8f90-122">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="f8f90-122">More connectors</span></span>
<span data-ttu-id="f8f90-123">Tornare all' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f8f90-123">Go back to the [APIs list](apis-list.md).</span></span>