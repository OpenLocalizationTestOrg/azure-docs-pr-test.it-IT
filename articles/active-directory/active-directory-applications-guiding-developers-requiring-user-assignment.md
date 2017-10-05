---
title: Richiedere l'assegnazione di utenti - Azure AD | Documentazione Microsoft
description: Come richiedere l'assegnazione di un utente per le applicazioni Azure.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 30b78cba-1e0f-472f-8314-f2250a9b91c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
robots: noindex
ms.openlocfilehash: 079b806c041a4a21e9350342867aee581c57bf45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-and-applications-require-user-assignment"></a><span data-ttu-id="0d79d-103">Azure AD e applicazioni: richiedere l'assegnazione di utenti</span><span class="sxs-lookup"><span data-stu-id="0d79d-103">Azure AD and applications: Require user assignment</span></span>
## <a name="requiring-user-assignment"></a><span data-ttu-id="0d79d-104">Richiedere l'assegnazione utente</span><span class="sxs-lookup"><span data-stu-id="0d79d-104">Requiring User Assignment</span></span>
1. <span data-ttu-id="0d79d-105">Accedere al portale di Azure con un account amministratore.</span><span class="sxs-lookup"><span data-stu-id="0d79d-105">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="0d79d-106">Fare clic sulla voce **Tutti gli elementi** del menu principale.</span><span class="sxs-lookup"><span data-stu-id="0d79d-106">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="0d79d-107">Scegliere la directory utilizzata per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d79d-107">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="0d79d-108">Fare clic sulla scheda **APPLICAZIONI** .</span><span class="sxs-lookup"><span data-stu-id="0d79d-108">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="0d79d-109">Selezionare l'applicazione dall'elenco di applicazioni associate a questa directory.</span><span class="sxs-lookup"><span data-stu-id="0d79d-109">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="0d79d-110">Fare clic sulla scheda **CONFIGURE** .</span><span class="sxs-lookup"><span data-stu-id="0d79d-110">Click the **CONFIGURE** tab.</span></span>
7. <span data-ttu-id="0d79d-111">Modificare **Assegnazione utente necessaria per l'accesso all’App** su Sì.</span><span class="sxs-lookup"><span data-stu-id="0d79d-111">Change the **User Assignment Required to Access App** toggle to Yes.</span></span>
8. <span data-ttu-id="0d79d-112">Fare clic sul pulsante **Salva** nella parte inferiore della schermata.</span><span class="sxs-lookup"><span data-stu-id="0d79d-112">Click the **Save** button at the bottom of the screen.</span></span>

<span data-ttu-id="0d79d-113">A questo punto è necessario assegnare utenti e gruppi all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0d79d-113">You will now have to assign users and/or groups to the application.</span></span> <span data-ttu-id="0d79d-114">Vedere [Assegnazione di utenti a un'applicazione](active-directory-applications-guiding-developers-assigning-users.md) e [Assegnazione di gruppi a un'applicazione](active-directory-applications-guiding-developers-assigning-groups.md).</span><span class="sxs-lookup"><span data-stu-id="0d79d-114">See [Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md) and [Assigning groups to an application](active-directory-applications-guiding-developers-assigning-groups.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d79d-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0d79d-115">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
