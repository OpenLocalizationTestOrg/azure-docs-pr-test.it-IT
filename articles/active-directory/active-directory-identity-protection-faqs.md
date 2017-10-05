---
title: Domande frequenti su Azure Active Directory Identity Protection | Microsoft Docs
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
ms.openlocfilehash: 781f868c87cea3cd790d89c61e26eecf352babea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-faq"></a><span data-ttu-id="8d532-103">Domande frequenti su Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="8d532-103">Azure Active Directory Identity Protection FAQ</span></span>


## <a name="why-do-some-risk-events-have-closed-system-status"></a><span data-ttu-id="8d532-104">Perché alcuni eventi di rischio hanno lo stato "Closed (system)" (Chiuso (sistema))?</span><span class="sxs-lookup"><span data-stu-id="8d532-104">Why do some risk events have “Closed (system)” status?</span></span>

<span data-ttu-id="8d532-105">**R:** si tratta di eventi che Azure Active Directory Identity Protection ha rilevato e successivamente chiusi perché gli eventi non venivano più considerati rischiosi.</span><span class="sxs-lookup"><span data-stu-id="8d532-105">**A:** These are events that Azure Active Directory Identity Protection detected and later closed because the events were no longer considered risky.</span></span> <span data-ttu-id="8d532-106">Questi eventi non vengono conteggiati ai fini del livello di rischio dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8d532-106">These events do not count towards the user’s risk level.</span></span> 

---

## <a name="do-i-need-to-be-a-global-admin-to-use-identity-protection-in-the-azure-portal"></a><span data-ttu-id="8d532-107">È necessario essere un amministratore globale per usare Identity Protection nel portale di Azure?</span><span class="sxs-lookup"><span data-stu-id="8d532-107">Do I need to be a global admin to use Identity Protection in the Azure portal?</span></span>
<span data-ttu-id="8d532-108">**R:** **No**.</span><span class="sxs-lookup"><span data-stu-id="8d532-108">**A:** **No**.</span></span> <span data-ttu-id="8d532-109">È possibile avere il ruolo con autorizzazioni di lettura per la sicurezza, di amministratore protezione o amministratore globale per usare Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="8d532-109">You can either be a Security Reader, a Security Admin or a Global Admin to use Identity Protection.</span></span>

---

## <a name="how-do-i-get-identity-protection"></a><span data-ttu-id="8d532-110">Come si ottiene Identity Protection?</span><span class="sxs-lookup"><span data-stu-id="8d532-110">How do I get Identity Protection?</span></span>
<span data-ttu-id="8d532-111">**R:** Per la risposta a questa domanda, vedere [Introduzione ad Azure Active Directory Premium](active-directory-get-started-premium.md).</span><span class="sxs-lookup"><span data-stu-id="8d532-111">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

## <a name="what-happens-when-your-azure-active-directory-premium-2-trial-expires"></a><span data-ttu-id="8d532-112">Cosa accade quando scade la versione di valutazione gratuita di Azure Active Directory Premium 2?</span><span class="sxs-lookup"><span data-stu-id="8d532-112">What happens when your Azure Active Directory Premium 2 trial expires?</span></span>

<span data-ttu-id="8d532-113">**R:** Se la versione di valutazione gratuita di Azure Active Directory Premium 2 è scaduta nella versione Azure Active Directory Free, Basic o Premium 1, ed era abilitata la Protezione Identità, sarà comunque possibile accedere ad essa, anche se non in mancanza di conformità con la licenza.</span><span class="sxs-lookup"><span data-stu-id="8d532-113">**A:** If your Azure Active Directory Premium 2 trial edition has expired on your Azure Active Directory Free, Basic or Premium 1 edition, and you had Identity Protection enabled, you still have access to it even though you are not in compliance with licensing.</span></span>

---
