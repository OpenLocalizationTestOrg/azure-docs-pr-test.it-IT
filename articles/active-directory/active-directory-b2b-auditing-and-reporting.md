---
title: Controllo e creazione di report per un utente di Collaborazione B2B di Azure Active Directory | Microsoft Docs
description: "Le proprietà di un utente guest sono configurabili in Collaborazione B2B di Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/12/2017
ms.author: sasubram
ms.openlocfilehash: ba782270f3280e52235bc13148d232284b55762a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="auditing-and-reporting-a-b2b-collaboration-user"></a><span data-ttu-id="40148-103">Controllo e creazione di report per un utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="40148-103">Auditing and reporting a B2B collaboration user</span></span>
<span data-ttu-id="40148-104">Con gli utenti guest, sono disponibili funzionalità di controllo analoghe a quelle degli utenti membri.</span><span class="sxs-lookup"><span data-stu-id="40148-104">With guest users, you have auditing capabilities similar to with member users.</span></span> <span data-ttu-id="40148-105">Di seguito è riportato un esempio di cronologia di inviti e riscatti dell'invitato Sam Oogle:</span><span class="sxs-lookup"><span data-stu-id="40148-105">Here's an example of the invitation and redemption history of invitee Sam Oogle:</span></span>

![log di controllo](./media/active-directory-b2b-auditing-and-reporting/audit-log.png)

<span data-ttu-id="40148-107">È possibile selezionare ogni evento per visualizzare i dettagli.</span><span class="sxs-lookup"><span data-stu-id="40148-107">You can dive into each of these events to get the details.</span></span> <span data-ttu-id="40148-108">È ad esempio possibile esaminare i dettagli relativi all'accettazione.</span><span class="sxs-lookup"><span data-stu-id="40148-108">For example, let's look at the acceptance details.</span></span>

![dettagli dell'attività](./media/active-directory-b2b-auditing-and-reporting/activity-details.png)

<span data-ttu-id="40148-110">È anche possibile esportare i log da Azure AD e usare lo strumento di creazione di report per ottenere report personalizzati.</span><span class="sxs-lookup"><span data-stu-id="40148-110">You can also export these logs from Azure AD and use the reporting tool of your choice to get customized reports.</span></span>

### <a name="next-steps"></a><span data-ttu-id="40148-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="40148-111">Next steps</span></span>

<span data-ttu-id="40148-112">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="40148-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="40148-113">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="40148-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="40148-114">Proprietà dell'utente di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="40148-114">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="40148-115">Aggiunta di un utente di Collaborazione B2B a un ruolo</span><span class="sxs-lookup"><span data-stu-id="40148-115">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="40148-116">Delegare gli inviti a Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="40148-116">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="40148-117">Gruppi dinamici e Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="40148-117">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="40148-118">Codici ed esempi di PowerShell per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="40148-118">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="40148-119">Configurare app SaaS per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="40148-119">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="40148-120">Token utente in Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="40148-120">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="40148-121">Mapping delle attestazioni utente per Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="40148-121">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="40148-122">Condivisione esterna di Office 365</span><span class="sxs-lookup"><span data-stu-id="40148-122">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="40148-123">Limitazioni correnti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="40148-123">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
