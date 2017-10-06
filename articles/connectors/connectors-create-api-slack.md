---
title: Ciao aaaUse Slack connettore App per la logica di Azure | Documenti Microsoft
description: Connettersi tooSlack nelle app di logica
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
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a><span data-ttu-id="916e8-103">Iniziare con connettore Slack hello</span><span class="sxs-lookup"><span data-stu-id="916e8-103">Get started with hello Slack connector</span></span>
<span data-ttu-id="916e8-104">Slack è uno strumento di comunicazione del team, che riunisce tutte le comunicazioni del team in un'unica posizione immediatamente disponibile e individuabile in qualsiasi luogo.</span><span class="sxs-lookup"><span data-stu-id="916e8-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="916e8-105">Creare prima di tutto un'app per la logica. Vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="916e8-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooslack"></a><span data-ttu-id="916e8-106">Creare una connessione tooSlack</span><span class="sxs-lookup"><span data-stu-id="916e8-106">Create a connection tooSlack</span></span>
<span data-ttu-id="916e8-107">connettore di Slack hello toouse, creare innanzitutto un **connessione** quindi fornire i dettagli di hello per queste proprietà:</span><span class="sxs-lookup"><span data-stu-id="916e8-107">toouse hello Slack connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="916e8-108">Proprietà</span><span class="sxs-lookup"><span data-stu-id="916e8-108">Property</span></span> | <span data-ttu-id="916e8-109">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="916e8-109">Required</span></span> | <span data-ttu-id="916e8-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="916e8-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="916e8-111">Token</span><span class="sxs-lookup"><span data-stu-id="916e8-111">Token</span></span> |<span data-ttu-id="916e8-112">Sì</span><span class="sxs-lookup"><span data-stu-id="916e8-112">Yes</span></span> |<span data-ttu-id="916e8-113">Fornire le credenziali di Slack</span><span class="sxs-lookup"><span data-stu-id="916e8-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="916e8-114">Seguire questi passaggi toosign in Slack e la configurazione completa hello di hello Slack **connessione** nell'app logica:</span><span class="sxs-lookup"><span data-stu-id="916e8-114">Follow these steps toosign into Slack, and complete hello configuration of hello Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="916e8-115">Selezionare **Ricorrenza**</span><span class="sxs-lookup"><span data-stu-id="916e8-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="916e8-116">Selezionare una **frequenza** e immettere un **intervallo**</span><span class="sxs-lookup"><span data-stu-id="916e8-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="916e8-117">Selezionare **Aggiungi un'azione**</span><span class="sxs-lookup"><span data-stu-id="916e8-117">Select **Add an action**</span></span>  
   <span data-ttu-id="916e8-118">![Configurare Slack][1]</span><span class="sxs-lookup"><span data-stu-id="916e8-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="916e8-119">Immettere il margine di flessibilità nella casella di ricerca hello e attendere hello ricerca tooreturn tutte le voci con Slack nel nome hello</span><span class="sxs-lookup"><span data-stu-id="916e8-119">Enter Slack in hello search box and wait for hello search tooreturn all entries with Slack in hello name</span></span>
5. <span data-ttu-id="916e8-120">Selezionare **Slack - Invia messaggio**</span><span class="sxs-lookup"><span data-stu-id="916e8-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="916e8-121">Selezionare **Accedi tooSlack**:</span><span class="sxs-lookup"><span data-stu-id="916e8-121">Select **Sign in tooSlack**:</span></span>  
   <span data-ttu-id="916e8-122">![Configurare Slack][2]</span><span class="sxs-lookup"><span data-stu-id="916e8-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="916e8-123">Fornire il toosign Slack credenziali in un'applicazione hello tooauthorize</span><span class="sxs-lookup"><span data-stu-id="916e8-123">Provide your Slack credentials toosign in tooauthorize hello  application</span></span>    
   ![Configurare Slack][3]  
8. <span data-ttu-id="916e8-125">Sarà nella pagina di accesso reindirizzato tooyour dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="916e8-125">You'll be redirected tooyour organization's Log in page.</span></span> <span data-ttu-id="916e8-126">**Autorizzare** toointeract Slack con l'app logica:</span><span class="sxs-lookup"><span data-stu-id="916e8-126">**Authorize** Slack toointeract with your logic app:</span></span>      
   <span data-ttu-id="916e8-127">![Configurare Slack][5]</span><span class="sxs-lookup"><span data-stu-id="916e8-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="916e8-128">Al termine dell'autorizzazione hello sarà reindirizzato tooyour logica app toocomplete, configurando hello **margine di flessibilità: ottenere tutti i messaggi** sezione.</span><span class="sxs-lookup"><span data-stu-id="916e8-128">After hello authorization completes you'll be redirected tooyour logic app toocomplete it by configuring hello **Slack - Get all messages** section.</span></span> <span data-ttu-id="916e8-129">Aggiungere altri trigger e azioni necessari.</span><span class="sxs-lookup"><span data-stu-id="916e8-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="916e8-130">![Configurare Slack][6]</span><span class="sxs-lookup"><span data-stu-id="916e8-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="916e8-131">Salvare il lavoro selezionando **salvare** sulla barra dei menu hello precedente.</span><span class="sxs-lookup"><span data-stu-id="916e8-131">Save your work by selecting **Save** on hello menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="916e8-132">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="916e8-132">Connector-specific details</span></span>

<span data-ttu-id="916e8-133">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="916e8-133">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="916e8-134">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="916e8-134">More connectors</span></span>
<span data-ttu-id="916e8-135">Tornare indietro toohello [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="916e8-135">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
