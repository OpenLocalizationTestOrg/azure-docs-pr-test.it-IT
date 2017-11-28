---
title: "domande sulla protezione di Active Directory identità aaaAzure | Documenti Microsoft"
description: Domande frequenti su Azure AD Identity Protection
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6a053ce02bf7a248a284f482f20f96a312f1c204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-faq"></a><span data-ttu-id="db3b1-103">Domande frequenti su Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="db3b1-103">Azure Active Directory Identity Protection FAQ</span></span>


## <a name="why-do-some-risk-events-have-closed-system-status"></a><span data-ttu-id="db3b1-104">Perché alcuni eventi di rischio hanno lo stato "Closed (system)" (Chiuso (sistema))?</span><span class="sxs-lookup"><span data-stu-id="db3b1-104">Why do some risk events have “Closed (system)” status?</span></span>

<span data-ttu-id="db3b1-105">**R:** eventi a cui la protezione dell'identità Azure Active Directory rilevato e successivamente chiusa perché gli eventi di hello non sono stati considerati rischiosi.</span><span class="sxs-lookup"><span data-stu-id="db3b1-105">**A:** These are events that Azure Active Directory Identity Protection detected and later closed because hello events were no longer considered risky.</span></span> <span data-ttu-id="db3b1-106">Questi eventi non vengono contano un livello di rischio dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="db3b1-106">These events do not count towards hello user’s risk level.</span></span> 

---

## <a name="do-i-need-toobe-a-global-admin-toouse-identity-protection-in-hello-azure-portal"></a><span data-ttu-id="db3b1-107">È necessario toobe toouse un amministratore globale la protezione dell'identità nel portale di Azure hello?</span><span class="sxs-lookup"><span data-stu-id="db3b1-107">Do I need toobe a global admin toouse Identity Protection in hello Azure portal?</span></span>
<span data-ttu-id="db3b1-108">**R:** **No**.</span><span class="sxs-lookup"><span data-stu-id="db3b1-108">**A:** **No**.</span></span> <span data-ttu-id="db3b1-109">Può essere un lettore di sicurezza, un amministratore responsabile della sicurezza o toouse un amministratore globale Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="db3b1-109">You can either be a Security Reader, a Security Admin or a Global Admin toouse Identity Protection.</span></span>

---

## <a name="how-do-i-get-identity-protection"></a><span data-ttu-id="db3b1-110">Come si ottiene Identity Protection?</span><span class="sxs-lookup"><span data-stu-id="db3b1-110">How do I get Identity Protection?</span></span>
<span data-ttu-id="db3b1-111">**R:** vedere [Introduzione a Azure Active Directory Premium](active-directory-get-started-premium.md) per una domanda toothis di risposta.</span><span class="sxs-lookup"><span data-stu-id="db3b1-111">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

## <a name="what-happens-when-your-azure-active-directory-premium-2-trial-expires"></a><span data-ttu-id="db3b1-112">Cosa accade quando scade la versione di valutazione gratuita di Azure Active Directory Premium 2?</span><span class="sxs-lookup"><span data-stu-id="db3b1-112">What happens when your Azure Active Directory Premium 2 trial expires?</span></span>

<span data-ttu-id="db3b1-113">**R:** se la versione di valutazione di Azure Active Directory Premium 2 scaduto l'edizione Azure Active Directory Free, Basic o Premium 1 ed è stato abilitata la protezione identità, sarà necessario tooit accesso anche se non sono in conformità con concessione di licenze.</span><span class="sxs-lookup"><span data-stu-id="db3b1-113">**A:** If your Azure Active Directory Premium 2 trial edition has expired on your Azure Active Directory Free, Basic or Premium 1 edition, and you had Identity Protection enabled, you still have access tooit even though you are not in compliance with licensing.</span></span>

---
