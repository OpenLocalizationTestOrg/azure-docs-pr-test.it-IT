---
title: Aggiungere il connettore Utenti di Office 365 alle app per la logica | Documentazione Microsoft
description: Panoramica del connettore Office 365 Users con i parametri dell'API REST
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2146481-9105-4f56-b4c2-7ae340cb922f
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 330f733440932a769eb0fe6031cd0d947a820080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-users-connector"></a><span data-ttu-id="bdf54-103">Introduzione al connettore Office 365 Users</span><span class="sxs-lookup"><span data-stu-id="bdf54-103">Get started with the Office 365 Users connector</span></span>
<span data-ttu-id="bdf54-104">Connettersi a Office 365 Users per ottenere profili, cercare utenti e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="bdf54-104">Connect to Office 365 Users to get profiles, search users, and more.</span></span> <span data-ttu-id="bdf54-105">Con Office 365 Users è possibile:</span><span class="sxs-lookup"><span data-stu-id="bdf54-105">With Office 365 Users, you can:</span></span>

* <span data-ttu-id="bdf54-106">Creare il flusso aziendale in base ai dati ottenuti da Office 365 Users.</span><span class="sxs-lookup"><span data-stu-id="bdf54-106">Build your business flow based on the data you get from Office 365 Users.</span></span> 
* <span data-ttu-id="bdf54-107">Usare azioni per ottenere i dipendenti diretti, il profilo utente di un manager e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="bdf54-107">Use actions that get direct reports, get a manager's user profile, and more.</span></span> <span data-ttu-id="bdf54-108">Queste azioni ottengono una risposta e quindi rendono l'output disponibile per altre azioni.</span><span class="sxs-lookup"><span data-stu-id="bdf54-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="bdf54-109">Ad esempio, ottenere i dipendenti diretti di una persona e quindi sfruttare queste informazioni per aggiornare un database SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bdf54-109">For example, get a person's direct reports, and then take this information and update a SQL Azure database.</span></span> 

<span data-ttu-id="bdf54-110">Per iniziare subito a creare un'app per la logica, vedere [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="bdf54-110">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-office-365-users"></a><span data-ttu-id="bdf54-111">Creare una connessione a Office 365 Users</span><span class="sxs-lookup"><span data-stu-id="bdf54-111">Create a connection to Office 365 Users</span></span>
<span data-ttu-id="bdf54-112">Quando si aggiunge questo connettore alle app per la logica, è necessario accedere all'account Office 365 Users e consentire alle app per la logica di connettersi all'account.</span><span class="sxs-lookup"><span data-stu-id="bdf54-112">When you add this connector to your logic apps, you must sign-in to your Office 365 Users account and allow logic apps to connect to your account.</span></span>

> [!INCLUDE [Steps to create a connection to Office 365 Users](../../includes/connectors-create-api-office365users.md)]
> 
> 

<span data-ttu-id="bdf54-113">Dopo aver creato la connessione, immettere le proprietà di Office 365 Users, ad esempio l'ID utente.</span><span class="sxs-lookup"><span data-stu-id="bdf54-113">After you create the connection, you enter the Office 365 Users properties, like the user ID.</span></span> <span data-ttu-id="bdf54-114">Il **riferimento all'API REST** in questo argomento descrive tali proprietà.</span><span class="sxs-lookup"><span data-stu-id="bdf54-114">The **REST API reference** in this topic describes these properties.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="bdf54-115">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="bdf54-115">Connector-specific details</span></span>

<span data-ttu-id="bdf54-116">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/officeusers/).</span><span class="sxs-lookup"><span data-stu-id="bdf54-116">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/officeusers/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="bdf54-117">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="bdf54-117">More connectors</span></span>
<span data-ttu-id="bdf54-118">Tornare all' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="bdf54-118">Go back to the [APIs list](apis-list.md).</span></span>