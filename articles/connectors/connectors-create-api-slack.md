---
title: Usare il connettore Slack nelle app per la logica di Azure | Microsoft Docs
description: Connettersi a Slack nelle app per la logica
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: fc5fc128efe01bd0727e3ff30d8938918e89ac3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-slack-connector"></a><span data-ttu-id="40f67-103">Introduzione al connettore Slack</span><span class="sxs-lookup"><span data-stu-id="40f67-103">Get started with the Slack connector</span></span>
<span data-ttu-id="40f67-104">Slack è uno strumento di comunicazione del team, che riunisce tutte le comunicazioni del team in un'unica posizione immediatamente disponibile e individuabile in qualsiasi luogo.</span><span class="sxs-lookup"><span data-stu-id="40f67-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="40f67-105">Creare prima di tutto un'app per la logica. Vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="40f67-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-slack"></a><span data-ttu-id="40f67-106">Creare una connessione a Slack</span><span class="sxs-lookup"><span data-stu-id="40f67-106">Create a connection to Slack</span></span>
<span data-ttu-id="40f67-107">Per usare il connettore Slack, creare prima una **connessione** , quindi specificare i dettagli di queste proprietà:</span><span class="sxs-lookup"><span data-stu-id="40f67-107">To use the Slack connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="40f67-108">Proprietà</span><span class="sxs-lookup"><span data-stu-id="40f67-108">Property</span></span> | <span data-ttu-id="40f67-109">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="40f67-109">Required</span></span> | <span data-ttu-id="40f67-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="40f67-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40f67-111">Token</span><span class="sxs-lookup"><span data-stu-id="40f67-111">Token</span></span> |<span data-ttu-id="40f67-112">Sì</span><span class="sxs-lookup"><span data-stu-id="40f67-112">Yes</span></span> |<span data-ttu-id="40f67-113">Fornire le credenziali di Slack</span><span class="sxs-lookup"><span data-stu-id="40f67-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="40f67-114">Seguire questi passaggi per accedere a Slack e completare la configurazione della **connessione** Slack nell'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="40f67-114">Follow these steps to sign into Slack, and complete the configuration of the Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="40f67-115">Selezionare **Ricorrenza**</span><span class="sxs-lookup"><span data-stu-id="40f67-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="40f67-116">Selezionare una **frequenza** e immettere un **intervallo**</span><span class="sxs-lookup"><span data-stu-id="40f67-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="40f67-117">Selezionare **Aggiungi un'azione**</span><span class="sxs-lookup"><span data-stu-id="40f67-117">Select **Add an action**</span></span>  
   <span data-ttu-id="40f67-118">![Configurare Slack][1]</span><span class="sxs-lookup"><span data-stu-id="40f67-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="40f67-119">Immettere Slack nella casella di ricerca e attendere che la ricerca restituisca tutte le voci con Slack nel nome</span><span class="sxs-lookup"><span data-stu-id="40f67-119">Enter Slack in the search box and wait for the search to return all entries with Slack in the name</span></span>
5. <span data-ttu-id="40f67-120">Selezionare **Slack - Invia messaggio**</span><span class="sxs-lookup"><span data-stu-id="40f67-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="40f67-121">Selezionare **Sign in to Slack** (Accedi a Slack):</span><span class="sxs-lookup"><span data-stu-id="40f67-121">Select **Sign in to Slack**:</span></span>  
   <span data-ttu-id="40f67-122">![Configurare Slack][2]</span><span class="sxs-lookup"><span data-stu-id="40f67-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="40f67-123">Specificare le credenziali di Slack per accedere e autorizzare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="40f67-123">Provide your Slack credentials to sign in to authorize the  application</span></span>    
   ![Configurare Slack][3]  
8. <span data-ttu-id="40f67-125">Si verrà reindirizzati alla pagina di accesso dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="40f67-125">You'll be redirected to your organization's Log in page.</span></span> <span data-ttu-id="40f67-126">**Autorizzare** l'interazione di Slack con l'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="40f67-126">**Authorize** Slack to interact with your logic app:</span></span>      
   <span data-ttu-id="40f67-127">![Configurare Slack][5]</span><span class="sxs-lookup"><span data-stu-id="40f67-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="40f67-128">Al termine dell'autenticazione si verrà reindirizzati all'app per la logica per completarla tramite la configurazione della sezione **Slack - Recupera tutti i messaggi** .</span><span class="sxs-lookup"><span data-stu-id="40f67-128">After the authorization completes you'll be redirected to your logic app to complete it by configuring the **Slack - Get all messages** section.</span></span> <span data-ttu-id="40f67-129">Aggiungere altri trigger e azioni necessari.</span><span class="sxs-lookup"><span data-stu-id="40f67-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="40f67-130">![Configurare Slack][6]</span><span class="sxs-lookup"><span data-stu-id="40f67-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="40f67-131">Salvare il lavoro selezionando **Salva** nella barra dei menu visualizzata in alto.</span><span class="sxs-lookup"><span data-stu-id="40f67-131">Save your work by selecting **Save** on the menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="40f67-132">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="40f67-132">Connector-specific details</span></span>

<span data-ttu-id="40f67-133">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="40f67-133">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="40f67-134">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="40f67-134">More connectors</span></span>
<span data-ttu-id="40f67-135">Tornare all' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="40f67-135">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
