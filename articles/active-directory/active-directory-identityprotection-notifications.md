---
title: Notifiche di Azure Active Directory Identity Protection| Documentazione Microsoft
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
ms.openlocfilehash: 079d16bbf75cd2b3b94269d684e1ae1a0e6aa967
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="47b5b-104">Notifiche di Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="47b5b-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="47b5b-105">Azure AD Identity Protection invia due tipi di messaggi di posta elettronica di notifica automatica per la gestione del rischio utente e degli eventi di rischio:</span><span class="sxs-lookup"><span data-stu-id="47b5b-105">Azure AD Identity Protection sends two types of automated notification emails to help you manage user risk and risk events:</span></span>

* <span data-ttu-id="47b5b-106">Messaggio di posta elettronica di avviso utente compromesso</span><span class="sxs-lookup"><span data-stu-id="47b5b-106">User compromised alert email</span></span>
* <span data-ttu-id="47b5b-107">Messaggio di posta elettronica di riepilogo settimanale</span><span class="sxs-lookup"><span data-stu-id="47b5b-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="47b5b-108">Messaggio di posta elettronica di avviso utente compromesso</span><span class="sxs-lookup"><span data-stu-id="47b5b-108">User compromised alert email</span></span>
<span data-ttu-id="47b5b-109">Quando Azure AD Identity Protection identifica un account come compromesso, viene generato un avviso di posta elettronica utente compromesso.</span><span class="sxs-lookup"><span data-stu-id="47b5b-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="47b5b-110">Il messaggio include un collegamento al report relativo agli utenti contrassegnati per il rischio nel dashboard di Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="47b5b-110">The email includes a link to the Users flagged for risk report in the Identity Protection dashboard.</span></span> <span data-ttu-id="47b5b-111">È consigliabile analizzare immediatamente le notifiche relative agli account compromessi.</span><span class="sxs-lookup"><span data-stu-id="47b5b-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="47b5b-112">Messaggio di posta elettronica di riepilogo settimanale</span><span class="sxs-lookup"><span data-stu-id="47b5b-112">Weekly digest email</span></span>
<span data-ttu-id="47b5b-113">Il messaggio di riepilogo settimanale contiene un riepilogo dei nuovi eventi di rischio.</span><span class="sxs-lookup"><span data-stu-id="47b5b-113">The weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="47b5b-114">Sono inclusi:</span><span class="sxs-lookup"><span data-stu-id="47b5b-114">It includes:</span></span>

* <span data-ttu-id="47b5b-115">Utenti a rischio.</span><span class="sxs-lookup"><span data-stu-id="47b5b-115">Users at risk</span></span>
* <span data-ttu-id="47b5b-116">Attività sospette</span><span class="sxs-lookup"><span data-stu-id="47b5b-116">Suspicious activities</span></span>
* <span data-ttu-id="47b5b-117">Vulnerabilità rilevate.</span><span class="sxs-lookup"><span data-stu-id="47b5b-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="47b5b-118">Collegamenti ai report correlati in Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="47b5b-118">Links to the related reports in Identity Protection</span></span>

<br><span data-ttu-id="47b5b-119">
![Monitoraggio e aggiornamento](./media/active-directory-identityprotection-notifications/400.png "monitoraggio e aggiornamento")
</span><span class="sxs-lookup"><span data-stu-id="47b5b-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="47b5b-120">È possibile disattivare l’invio del messaggio di posta elettronica settimanale contenente il riepilogo.</span><span class="sxs-lookup"><span data-stu-id="47b5b-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="47b5b-121">
![Rischi per gli utenti](./media/active-directory-identityprotection-notifications/62.png "rischi per gli utenti")
</span><span class="sxs-lookup"><span data-stu-id="47b5b-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="47b5b-122">**Per aprire la relativa finestra di dialogo di configurazione**:</span><span class="sxs-lookup"><span data-stu-id="47b5b-122">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="47b5b-123">Nel pannello **Azure AD Identity Protection** fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="47b5b-123">On the **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="47b5b-124">
   ![I criteri di rischio utente](./media/active-directory-identityprotection-notifications/401.png "rischio utente")
   </span><span class="sxs-lookup"><span data-stu-id="47b5b-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="47b5b-125">Nella sezione **Generale** fare clic su **Notifiche**.</span><span class="sxs-lookup"><span data-stu-id="47b5b-125">In the **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="47b5b-126">
   ![I criteri di rischio utente](./media/active-directory-identityprotection-notifications/405.png "rischio utente")
   </span><span class="sxs-lookup"><span data-stu-id="47b5b-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="47b5b-127">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="47b5b-127">See also</span></span>
* [<span data-ttu-id="47b5b-128">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="47b5b-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
