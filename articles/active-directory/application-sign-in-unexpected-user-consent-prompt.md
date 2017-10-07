---
title: richiesta di consenso aaaUnexpected durante l'accesso dell'applicazione tooan | Documenti Microsoft
description: "Come tootroubleshoot quando un utente visualizza una richiesta di consenso per un'applicazione è stata integrata con Azure Active Directory che non prevista"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a><span data-ttu-id="4a04d-103">Consenso imprevisto durante l'accesso dell'applicazione tooan</span><span class="sxs-lookup"><span data-stu-id="4a04d-103">Unexpected consent prompt when signing in tooan application</span></span>

<span data-ttu-id="4a04d-104">Molte applicazioni che si integrano con Azure Active Directory richiedono risorse di toovarious autorizzazioni in ordine toorun.</span><span class="sxs-lookup"><span data-stu-id="4a04d-104">Many applications that integrate with Azure Active Directory require permissions toovarious resources in order toorun.</span></span> <span data-ttu-id="4a04d-105">Quando queste risorse sono inoltre integrate con Azure Active Directory, framework di consenso tooaccess autorizzazioni li viene richiesto tramite hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a04d-105">When these resources are also integrated with Azure Active Directory, permissions tooaccess them is requested using hello Azure AD consent framework.</span></span> 

<span data-ttu-id="4a04d-106">Ciò comporta una richiesta di consenso visualizzandola hello prima volta che un'applicazione, è spesso un'unica operazione.</span><span class="sxs-lookup"><span data-stu-id="4a04d-106">This results in a consent prompt being shown hello first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="4a04d-107">Scenari in cui gli utenti visualizzano richieste di consenso</span><span class="sxs-lookup"><span data-stu-id="4a04d-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="4a04d-108">Ulteriori richieste aggiuntive sono possibili in vari scenari:</span><span class="sxs-lookup"><span data-stu-id="4a04d-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="4a04d-109">Hello insieme di autorizzazioni richiesto dall'applicazione hello è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="4a04d-109">hello set of permissions required by hello application have changed.</span></span>

* <span data-ttu-id="4a04d-110">gli utenti Hello originariamente acconsentito toohello applicazione non è un amministratore, e ora un utente diverso (non-admin) si usa un'applicazione hello per hello prima volta.</span><span class="sxs-lookup"><span data-stu-id="4a04d-110">hello user who originally consented toohello application was not an administrator, and now a different (non-admin) User is using hello application for hello first time.</span></span>

* <span data-ttu-id="4a04d-111">gli utenti Hello originariamente acconsentito toohello applicazione sono un amministratore, ma essi non fornire il consenso per conto di tutta l'organizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="4a04d-111">hello user who originally consented toohello application was an administrator, but they did not consent on-behalf of hello entire organization.</span></span>

* <span data-ttu-id="4a04d-112">utilizza un'applicazione Hello [consenso incrementale e dinamico](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest autorizzazioni aggiuntive dopo che è stato inizialmente consenso.</span><span class="sxs-lookup"><span data-stu-id="4a04d-112">hello application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest additional permissions after consent was initially granted.</span></span> <span data-ttu-id="4a04d-113">Questo tipo di consenso viene frequentemente usato quando funzionalità facoltative di un'applicazione richiedono autorizzazioni ulteriori a quelle richieste per la funzionalità di base.</span><span class="sxs-lookup"><span data-stu-id="4a04d-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="4a04d-114">Il consenso è stato revocato dopo essere stato inizialmente consentito.</span><span class="sxs-lookup"><span data-stu-id="4a04d-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="4a04d-115">sviluppatore Hello è configurato toorequire applicazione hello una richiesta di consenso ogni volta che viene utilizzata (Nota: questo non è consigliata).</span><span class="sxs-lookup"><span data-stu-id="4a04d-115">hello developer has configured hello application toorequire a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a04d-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4a04d-116">Next steps</span></span>

-   [<span data-ttu-id="4a04d-117">App, autorizzazioni e consenso in Azure Active Directory (endpoint v1.0)</span><span class="sxs-lookup"><span data-stu-id="4a04d-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="4a04d-118">Gli ambiti, autorizzazioni e consenso hello Azure Active Directory (endpoint v 2.0)</span><span class="sxs-lookup"><span data-stu-id="4a04d-118">Scopes, permissions, and consent in hello Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


