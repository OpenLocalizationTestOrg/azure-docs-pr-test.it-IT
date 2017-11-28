---
title: le notifiche di Active Directory Identity Protection aaaAzure | Documenti Microsoft
description: "Informazioni su come le notifiche agevolano le attività di analisi."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestione applicazioni, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="903da-104">Notifiche di Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="903da-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="903da-105">Azure AD Identity Protection invia due tipi di notifica automatica tramite posta elettronica toohelp per gestire il rischio di utente e gli eventi di rischio:</span><span class="sxs-lookup"><span data-stu-id="903da-105">Azure AD Identity Protection sends two types of automated notification emails toohelp you manage user risk and risk events:</span></span>

* <span data-ttu-id="903da-106">Messaggio di posta elettronica di avviso utente compromesso</span><span class="sxs-lookup"><span data-stu-id="903da-106">User compromised alert email</span></span>
* <span data-ttu-id="903da-107">Messaggio di posta elettronica di riepilogo settimanale</span><span class="sxs-lookup"><span data-stu-id="903da-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="903da-108">Messaggio di posta elettronica di avviso utente compromesso</span><span class="sxs-lookup"><span data-stu-id="903da-108">User compromised alert email</span></span>
<span data-ttu-id="903da-109">Quando Azure AD Identity Protection identifica un account come compromesso, viene generato un avviso di posta elettronica utente compromesso.</span><span class="sxs-lookup"><span data-stu-id="903da-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="903da-110">posta elettronica Hello include un collegamento di toohello che utenti contrassegnati per report rischi nel dashboard di hello Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="903da-110">hello email includes a link toohello Users flagged for risk report in hello Identity Protection dashboard.</span></span> <span data-ttu-id="903da-111">È consigliabile analizzare immediatamente le notifiche relative agli account compromessi.</span><span class="sxs-lookup"><span data-stu-id="903da-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="903da-112">Messaggio di posta elettronica di riepilogo settimanale</span><span class="sxs-lookup"><span data-stu-id="903da-112">Weekly digest email</span></span>
<span data-ttu-id="903da-113">Hello settimanale digest messaggio di posta elettronica contenente un riepilogo di nuovi eventi di rischio.</span><span class="sxs-lookup"><span data-stu-id="903da-113">hello weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="903da-114">Sono inclusi:</span><span class="sxs-lookup"><span data-stu-id="903da-114">It includes:</span></span>

* <span data-ttu-id="903da-115">Utenti a rischio.</span><span class="sxs-lookup"><span data-stu-id="903da-115">Users at risk</span></span>
* <span data-ttu-id="903da-116">Attività sospette</span><span class="sxs-lookup"><span data-stu-id="903da-116">Suspicious activities</span></span>
* <span data-ttu-id="903da-117">Vulnerabilità rilevate.</span><span class="sxs-lookup"><span data-stu-id="903da-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="903da-118">Toohello collegamenti correlati di report nella protezione di identità</span><span class="sxs-lookup"><span data-stu-id="903da-118">Links toohello related reports in Identity Protection</span></span>

<br><span data-ttu-id="903da-119">
![Monitoraggio e aggiornamento](./media/active-directory-identityprotection-notifications/400.png "monitoraggio e aggiornamento")
</span><span class="sxs-lookup"><span data-stu-id="903da-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="903da-120">È possibile disattivare l’invio del messaggio di posta elettronica settimanale contenente il riepilogo.</span><span class="sxs-lookup"><span data-stu-id="903da-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="903da-121">
![Rischi per gli utenti](./media/active-directory-identityprotection-notifications/62.png "rischi per gli utenti")
</span><span class="sxs-lookup"><span data-stu-id="903da-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="903da-122">**finestra di dialogo di configurazione correlato hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="903da-122">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="903da-123">In hello **Azure AD Identity Protection** pannello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="903da-123">On hello **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="903da-124">
   ![I criteri di rischio utente](./media/active-directory-identityprotection-notifications/401.png "rischio utente")
   </span><span class="sxs-lookup"><span data-stu-id="903da-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="903da-125">In hello **generale** fare clic su **notifiche**.</span><span class="sxs-lookup"><span data-stu-id="903da-125">In hello **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="903da-126">
   ![I criteri di rischio utente](./media/active-directory-identityprotection-notifications/405.png "rischio utente")
   </span><span class="sxs-lookup"><span data-stu-id="903da-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="903da-127">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="903da-127">See also</span></span>
* [<span data-ttu-id="903da-128">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="903da-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
