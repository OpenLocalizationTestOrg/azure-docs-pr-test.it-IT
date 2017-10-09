---
title: hello aaaUse connettore Server SharePoint nelle App logica | Documenti Microsoft
description: Introduzione all'uso hello hello connettore Server SharePoint in App per la logica
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a><span data-ttu-id="3f5aa-103">Iniziare con il connettore di SharePoint hello</span><span class="sxs-lookup"><span data-stu-id="3f5aa-103">Get started with hello SharePoint connector</span></span>
<span data-ttu-id="3f5aa-104">Hello connettore di SharePoint fornisce un modo toowork con gli elenchi in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3f5aa-104">hello SharePoint Connector provides an way toowork with Lists on SharePoint.</span></span>

<span data-ttu-id="3f5aa-105">Creare prima di tutto un'app per la logica. Vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3f5aa-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toosharepoint"></a><span data-ttu-id="3f5aa-106">Creare una connessione tooSharePoint</span><span class="sxs-lookup"><span data-stu-id="3f5aa-106">Create a connection tooSharePoint</span></span>
<span data-ttu-id="3f5aa-107">toouse hello connettore di SharePoint, creare innanzitutto un **connessione** quindi fornire i dettagli di hello per queste proprietà:</span><span class="sxs-lookup"><span data-stu-id="3f5aa-107">toouse hello SharePoint Connector , you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="3f5aa-108">Proprietà</span><span class="sxs-lookup"><span data-stu-id="3f5aa-108">Property</span></span> | <span data-ttu-id="3f5aa-109">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3f5aa-109">Required</span></span> | <span data-ttu-id="3f5aa-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3f5aa-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3f5aa-111">Token</span><span class="sxs-lookup"><span data-stu-id="3f5aa-111">Token</span></span> |<span data-ttu-id="3f5aa-112">Sì</span><span class="sxs-lookup"><span data-stu-id="3f5aa-112">Yes</span></span> |<span data-ttu-id="3f5aa-113">Fornire le credenziali di SharePoint</span><span class="sxs-lookup"><span data-stu-id="3f5aa-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="3f5aa-114">tooconnect troppo**SharePoint**, immettere il tooSharePoint identità (nome utente e password, le credenziali della smart card e così via).</span><span class="sxs-lookup"><span data-stu-id="3f5aa-114">tooconnect too**SharePoint**, enter your identity (username and password, smart card credentials, etc.) tooSharePoint.</span></span> <span data-ttu-id="3f5aa-115">Una volta che si è stati autenticati, è possibile procedere connettore di SharePoint hello toouse nell'app logica.</span><span class="sxs-lookup"><span data-stu-id="3f5aa-115">Once you've been authenticated, you can proceed toouse hello SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="3f5aa-116">Mentre nella finestra di progettazione di hello dell'app logica, seguire questi toosign passaggi in connessioni di SharePoint toocreate hello **connessione** per l'utilizzo nell'app logica:</span><span class="sxs-lookup"><span data-stu-id="3f5aa-116">While on hello designer of your logic app, follow these steps toosign into SharePoint toocreate hello connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="3f5aa-117">Immettere SharePoint nella casella di ricerca hello e attendere che tutte le voci con SharePoint nel nome hello tooreturn ricerca hello:</span><span class="sxs-lookup"><span data-stu-id="3f5aa-117">Enter SharePoint in hello search box and wait for hello search tooreturn all entries with SharePoint in hello name:</span></span>   
   ![Configurare SharePoint][1]  
2. <span data-ttu-id="3f5aa-119">Selezionare **SharePoint - Quando un file viene creato**</span><span class="sxs-lookup"><span data-stu-id="3f5aa-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="3f5aa-120">Selezionare **Accedi tooSharePoint**:</span><span class="sxs-lookup"><span data-stu-id="3f5aa-120">Select **Sign in tooSharePoint**:</span></span>   
   <span data-ttu-id="3f5aa-121">![Configurare SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="3f5aa-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="3f5aa-122">Fornire il toosign le credenziali di SharePoint in tooauthenticate con SharePoint</span><span class="sxs-lookup"><span data-stu-id="3f5aa-122">Provide your SharePoint credentials toosign in tooauthenticate with SharePoint</span></span>   
   ![Configurare SharePoint][3]     
5. <span data-ttu-id="3f5aa-124">Al termine dell'autenticazione hello sarà reindirizzato tooyour logica app toocomplete, tramite la configurazione di SharePoint **quando viene creato un file** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="3f5aa-124">After hello authentication completes you'll be redirected tooyour logic app toocomplete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="3f5aa-125">![Configurare SharePoint][4]</span><span class="sxs-lookup"><span data-stu-id="3f5aa-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="3f5aa-126">È quindi possibile aggiungere altre azioni che è necessario toocomplete app logica e i trigger.</span><span class="sxs-lookup"><span data-stu-id="3f5aa-126">You can then add other triggers and actions that you need toocomplete your logic app.</span></span>   
7. <span data-ttu-id="3f5aa-127">Salvare il lavoro selezionando **salvare** sulla barra dei menu hello precedente.</span><span class="sxs-lookup"><span data-stu-id="3f5aa-127">Save your work by selecting **Save** on hello menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="3f5aa-128">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="3f5aa-128">Connector-specific details</span></span>

<span data-ttu-id="3f5aa-129">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="3f5aa-129">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="3f5aa-130">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="3f5aa-130">More connectors</span></span>
<span data-ttu-id="3f5aa-131">Tornare indietro toohello [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="3f5aa-131">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
