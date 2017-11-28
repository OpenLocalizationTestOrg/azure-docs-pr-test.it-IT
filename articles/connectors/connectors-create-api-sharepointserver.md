---
title: Usare il connettore SharePoint Server nelle app per la logica | Microsoft Docs
description: Introduzione all'uso del connettore SharePoint Server nelle app per la logica
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
ms.openlocfilehash: 0f3274816e279a1aa57febaa2f8294914900799a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-connector"></a><span data-ttu-id="a1c9c-103">Introduzione al connettore SharePoint</span><span class="sxs-lookup"><span data-stu-id="a1c9c-103">Get started with the SharePoint connector</span></span>
<span data-ttu-id="a1c9c-104">Il connettore SharePoint consente di utilizzare gli elenchi in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a1c9c-104">The SharePoint Connector provides an way to work with Lists on SharePoint.</span></span>

<span data-ttu-id="a1c9c-105">Creare prima di tutto un'app per la logica. Vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a1c9c-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sharepoint"></a><span data-ttu-id="a1c9c-106">Creare una connessione a SharePoint</span><span class="sxs-lookup"><span data-stu-id="a1c9c-106">Create a connection to SharePoint</span></span>
<span data-ttu-id="a1c9c-107">Per usare il connettore SharePoint, creare prima una **connessione** , quindi indicare i dettagli di queste proprietà:</span><span class="sxs-lookup"><span data-stu-id="a1c9c-107">To use the SharePoint Connector , you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="a1c9c-108">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a1c9c-108">Property</span></span> | <span data-ttu-id="a1c9c-109">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="a1c9c-109">Required</span></span> | <span data-ttu-id="a1c9c-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a1c9c-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1c9c-111">Token</span><span class="sxs-lookup"><span data-stu-id="a1c9c-111">Token</span></span> |<span data-ttu-id="a1c9c-112">Sì</span><span class="sxs-lookup"><span data-stu-id="a1c9c-112">Yes</span></span> |<span data-ttu-id="a1c9c-113">Fornire le credenziali di SharePoint</span><span class="sxs-lookup"><span data-stu-id="a1c9c-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="a1c9c-114">Per connettersi a **SharePoint**, immettere la propria identità (nome utente e password, credenziali di smart card e così via) in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a1c9c-114">To connect to **SharePoint**, enter your identity (username and password, smart card credentials, etc.) to SharePoint.</span></span> <span data-ttu-id="a1c9c-115">Dopo l'autenticazione, è possibile usare il connettore SharePoint nella propria app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a1c9c-115">Once you've been authenticated, you can proceed to use the SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="a1c9c-116">Dall'applicazione di progettazione delle app per la logica, seguire questi passaggi per accedere a SharePoint e creare la connessione **connessione** da usare con l'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="a1c9c-116">While on the designer of your logic app, follow these steps to sign into SharePoint to create the connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="a1c9c-117">Immettere SharePoint nella casella di ricerca e attendere che la ricerca restituisca tutte le voci con SharePoint nel nome: </span><span class="sxs-lookup"><span data-stu-id="a1c9c-117">Enter SharePoint in the search box and wait for the search to return all entries with SharePoint in the name:</span></span>   
   ![Configurare SharePoint][1]  
2. <span data-ttu-id="a1c9c-119">Selezionare **SharePoint - Quando un file viene creato**</span><span class="sxs-lookup"><span data-stu-id="a1c9c-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="a1c9c-120">Selezionare **Sign in to SharePoint** (Accedi a SharePoint):</span><span class="sxs-lookup"><span data-stu-id="a1c9c-120">Select **Sign in to SharePoint**:</span></span>   
   <span data-ttu-id="a1c9c-121">![Configurare SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="a1c9c-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="a1c9c-122">Fornire le credenziali di SharePoint per accedere ed eseguire l'autenticazione con SharePoint </span><span class="sxs-lookup"><span data-stu-id="a1c9c-122">Provide your SharePoint credentials to sign in to authenticate with SharePoint</span></span>   
   ![Configurare SharePoint][3]     
5. <span data-ttu-id="a1c9c-124">Al termine dell'autenticazione si verrà reindirizzati all'app per la logica per completarla tramite la configurazione della finestra di dialogo **Quando un file viene creato** di SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a1c9c-124">After the authentication completes you'll be redirected to your logic app to complete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="a1c9c-125">![Configurare SharePoint][4]</span><span class="sxs-lookup"><span data-stu-id="a1c9c-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="a1c9c-126">È quindi possibile aggiungere altri trigger e azioni necessari per completare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a1c9c-126">You can then add other triggers and actions that you need to complete your logic app.</span></span>   
7. <span data-ttu-id="a1c9c-127">Salvare il lavoro selezionando **Salva** nella barra dei menu visualizzata in alto.</span><span class="sxs-lookup"><span data-stu-id="a1c9c-127">Save your work by selecting **Save** on the menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="a1c9c-128">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="a1c9c-128">Connector-specific details</span></span>

<span data-ttu-id="a1c9c-129">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="a1c9c-129">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="a1c9c-130">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="a1c9c-130">More connectors</span></span>
<span data-ttu-id="a1c9c-131">Tornare all' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="a1c9c-131">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
