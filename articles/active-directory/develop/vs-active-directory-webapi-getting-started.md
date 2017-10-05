---
title: Introduzione AD Azure nei progetti di Visual Studio WebApi | Microsoft Docs
description: Come iniziare a utilizzare Azure Active Directory nei progetti WebApi dopo la connessione o la creazione ad Azure AD utilizzando i servizi relativi a Visual Studio
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: a756316054dd3bb63f3b0a9f59621bb1345bc693
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="fbe86-103">Introduzione ad Azure Active Directory e ai servizi relativi a Visual Studio (progetti WebApi)</span><span class="sxs-lookup"><span data-stu-id="fbe86-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fbe86-104">Per iniziare</span><span class="sxs-lookup"><span data-stu-id="fbe86-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="fbe86-105">Risultati</span><span class="sxs-lookup"><span data-stu-id="fbe86-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="fbe86-106">Richiesta di autenticazione ai controller di accesso</span><span class="sxs-lookup"><span data-stu-id="fbe86-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="fbe86-107">Tutti i controller del progetto sono dotati dell'attributo **Authorize** .</span><span class="sxs-lookup"><span data-stu-id="fbe86-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="fbe86-108">Questo attributo richiede l'autenticazione dell'utente prima dell'accesso alle API definite dai controller.</span><span class="sxs-lookup"><span data-stu-id="fbe86-108">This attribute requires the user to be authenticated before accessing the APIs defined by these controllers.</span></span> <span data-ttu-id="fbe86-109">Per permettere l'accesso anonimo al controller, rimuovere l'attributo dal controller.</span><span class="sxs-lookup"><span data-stu-id="fbe86-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="fbe86-110">Per configurare le autorizzazioni con un livello di granularità superiore, applicare l'attributo a ogni metodo che necessita di autorizzazione invece di applicarlo alla classe controller.</span><span class="sxs-lookup"><span data-stu-id="fbe86-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbe86-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fbe86-111">Next steps</span></span>
[<span data-ttu-id="fbe86-112">Altre informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbe86-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

