---
title: reporting di Active Directory aaaAzure | Documenti Microsoft
description: Offre una panoramica generale della creazione di report in Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="09531-103">Creazione di report in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09531-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="09531-104">La creazione di report in Azure Active Directory permette di ottenere informazioni approfondite sullo stato dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="09531-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="09531-105">dati Hello fornito consentono di:</span><span class="sxs-lookup"><span data-stu-id="09531-105">hello provided data enables you to:</span></span>

- <span data-ttu-id="09531-106">Determinare l'utilizzo di app e servizi da parte degli utenti</span><span class="sxs-lookup"><span data-stu-id="09531-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="09531-107">Rilevare potenziali rischi che pregiudicano hello integrità dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="09531-107">Detect potential risks affecting hello health of your environment</span></span>
- <span data-ttu-id="09531-108">Risolvere problemi che influiscono negativamente sulla produttività degli utenti</span><span class="sxs-lookup"><span data-stu-id="09531-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="09531-109">architettura di reporting Hello si basa su due concetti di base:</span><span class="sxs-lookup"><span data-stu-id="09531-109">hello reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="09531-110">Report sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="09531-110">Security reports</span></span>
- <span data-ttu-id="09531-111">Report sull’attività</span><span class="sxs-lookup"><span data-stu-id="09531-111">Activity reports</span></span>

![Creazione di report](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="09531-113">Report sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="09531-113">Security reports</span></span>

<span data-ttu-id="09531-114">report sulla sicurezza Hello in Azure Active Directory della Guida è tooprotect identità dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="09531-114">hello security reports in Azure Active Directory help you tooprotect your organization's identities.</span></span>  
<span data-ttu-id="09531-115">Azure Active Directory prevede due tipi di report sulla sicurezza:</span><span class="sxs-lookup"><span data-stu-id="09531-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="09531-116">**Utenti contrassegno i rischi** - hello [utenti contrassegno per report di sicurezza di rischio](active-directory-reporting-security-user-at-risk.md), una panoramica degli account utente che sia stato compromesso.</span><span class="sxs-lookup"><span data-stu-id="09531-116">**Users flagged for risk** - From hello [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="09531-117">**Accessi rischiosi** : con hello [rapporto sulla sicurezza rischiosa Accedi](active-directory-reporting-security-risky-sign-ins.md), si ottiene un indicatore per tentativi di accesso che siano stati eseguiti da un utente che non hello legittimo proprietario di un account utente.</span><span class="sxs-lookup"><span data-stu-id="09531-117">**Risky sign-ins** - With hello [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 

<span data-ttu-id="09531-118">**Licenza Azure AD è necessario tooaccess un report di sicurezza?**</span><span class="sxs-lookup"><span data-stu-id="09531-118">**What Azure AD license do you need tooaccess a security report?**</span></span>  
<span data-ttu-id="09531-119">Tutte le edizioni di Azure Active Directory offrono report sugli utenti contrassegnati per il rischio e sugli accessi a rischio.</span><span class="sxs-lookup"><span data-stu-id="09531-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="09531-120">Tuttavia, il livello di hello di granularità dei report varia tra le edizioni di hello:</span><span class="sxs-lookup"><span data-stu-id="09531-120">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="09531-121">In hello **le edizioni di Azure Active Directory Free e Basic**, già un elenco degli utenti contrassegnati per rischio e accessi rischiosi.</span><span class="sxs-lookup"><span data-stu-id="09531-121">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="09531-122">Hello **Azure Active Directory Premium 1** edition estende questo modello, consentendo anche tooexamine alcune hello sottostante gli eventi di rischio che sono stati rilevati per ogni report.</span><span class="sxs-lookup"><span data-stu-id="09531-122">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="09531-123">Hello **Azure Active Directory Premium 2** edition fornisce all'hello più informazioni dettagliate su hello sottostante gli eventi di rischio e consente inoltre di criteri di sicurezza tooconfigure rispondono automaticamente tooconfigured livelli di rischio.</span><span class="sxs-lookup"><span data-stu-id="09531-123">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about hello underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="09531-124">Report sull’attività</span><span class="sxs-lookup"><span data-stu-id="09531-124">Activity reports</span></span>

<span data-ttu-id="09531-125">Azure Active Directory prevede due tipi di report sull'attività:</span><span class="sxs-lookup"><span data-stu-id="09531-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="09531-126">**Log di controllo** : hello [report attività i log di controllo](active-directory-reporting-activity-audit-logs.md) fornisce cronologia toohello di accesso di ogni attività eseguita nel tenant.</span><span class="sxs-lookup"><span data-stu-id="09531-126">**Audit logs** - hello [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access toohello history of every task performed in your tenant.</span></span>

- <span data-ttu-id="09531-127">**Accessi** : con hello [report attività accessi](active-directory-reporting-activity-sign-ins.md), è possibile determinare chi ha eseguito l'attività hello segnalate dal report di log di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="09531-127">**Sign-ins** -  With hello [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed hello tasks reported by hello audit logs report.</span></span>



<span data-ttu-id="09531-128">Hello **i report di log di controllo** fornisce per conformità con i record di attività di sistema.</span><span class="sxs-lookup"><span data-stu-id="09531-128">hello **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="09531-129">Tra le altre operazioni, hello forniti dati consentono gli scenari comuni di tooaddress, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="09531-129">Amongst others, hello provided data enables you tooaddress common scenarios such as:</span></span>

- <span data-ttu-id="09531-130">Un utente al tenant ottenuto gruppo admin tooan di accesso.</span><span class="sxs-lookup"><span data-stu-id="09531-130">Someone in my tenant got access tooan admin group.</span></span> <span data-ttu-id="09531-131">si vuole sapere chi ha concesso tale accesso.</span><span class="sxs-lookup"><span data-stu-id="09531-131">Who gave them access?</span></span> 

- <span data-ttu-id="09531-132">Si desidera tooknow hello lista di utenti di accedere a un'app specifica dopo I caricate hello app e di recente da tooknow se viene eseguito correttamente</span><span class="sxs-lookup"><span data-stu-id="09531-132">I want tooknow hello list of users signing into a specific app since I recently onboarded hello app and want tooknow if it’s doing well</span></span>

- <span data-ttu-id="09531-133">Voglio tooknow il numero di password Reimposta viene eseguite nel mio tenant</span><span class="sxs-lookup"><span data-stu-id="09531-133">I want tooknow how many password resets are happening in my tenant</span></span>


<span data-ttu-id="09531-134">**Licenza Azure AD è necessario tooaccess hello audit log report?**</span><span class="sxs-lookup"><span data-stu-id="09531-134">**What Azure AD license do you need tooaccess hello audit logs report?**</span></span>  
<span data-ttu-id="09531-135">report di log di controllo Hello è disponibile per le funzionalità per i quali si dispone di licenze.</span><span class="sxs-lookup"><span data-stu-id="09531-135">hello audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="09531-136">Se si dispone di una licenza per una funzionalità specifica, è inoltre accesso toohello informazioni del log per il controllo.</span><span class="sxs-lookup"><span data-stu-id="09531-136">If you have a license for a specific feature, you also have access toohello audit log information for it.</span></span>

<span data-ttu-id="09531-137">Per ulteriori informazioni, vedere **il confronto delle funzionalità disponibili in genere delle edizioni Free, Basic e Premium di hello** in [Azure Active Directory e le funzionalità](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span><span class="sxs-lookup"><span data-stu-id="09531-137">For more details, see **Comparing generally available features of hello Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="09531-138">Hello **report attività accessi** tootoofind Abilita risponde tooquestions, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="09531-138">hello **sign-ins activity report** enables tootoofind answers tooquestions such as:</span></span>

- <span data-ttu-id="09531-139">Che cos'è hello sign-in schema di un utente?</span><span class="sxs-lookup"><span data-stu-id="09531-139">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="09531-140">Quanti utenti hanno effettuato l'accesso nell'arco di una settimana?</span><span class="sxs-lookup"><span data-stu-id="09531-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="09531-141">Qual è stato hello di tali accessi?</span><span class="sxs-lookup"><span data-stu-id="09531-141">What’s hello status of these sign-ins?</span></span>


<span data-ttu-id="09531-142">**Licenza Azure AD eseguire tale operazione è necessario tooaccess hello report attività accessi?**</span><span class="sxs-lookup"><span data-stu-id="09531-142">**What Azure AD license do you need tooaccess hello sign-ins activity report?**</span></span>  
<span data-ttu-id="09531-143">tooaccess hello report attività accessi, il tenant deve avere una licenza di Azure AD Premium è associata.</span><span class="sxs-lookup"><span data-stu-id="09531-143">tooaccess hello sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="09531-144">Accesso a livello di codice</span><span class="sxs-lookup"><span data-stu-id="09531-144">Programmatic access</span></span>

<span data-ttu-id="09531-145">Nell'interfaccia utente toohello aggiunta reporting di Azure Active Directory offre inoltre funzioni di [l'accesso programmatico](active-directory-reporting-api-getting-started-azure-portal.md) toohello dati di report.</span><span class="sxs-lookup"><span data-stu-id="09531-145">In addition toohello user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) toohello reporting data.</span></span> <span data-ttu-id="09531-146">dati di Hello di questi report possono essere molto utile tooyour applicazioni, ad esempio i sistemi SIEM, controllo e strumenti di business intelligence.</span><span class="sxs-lookup"><span data-stu-id="09531-146">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="09531-147">Hello Azure AD reporting che API forniscono dati toohello accesso a livello di codice tramite un set di API basata su REST.</span><span class="sxs-lookup"><span data-stu-id="09531-147">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="09531-148">È possibile chiamare le API da numerosi linguaggi di programmazione e strumenti.</span><span class="sxs-lookup"><span data-stu-id="09531-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="09531-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="09531-149">Next steps</span></span>

<span data-ttu-id="09531-150">Se si desidera approfondire hello tooknow vari tipi di report in Azure Active Directory, vedere:</span><span class="sxs-lookup"><span data-stu-id="09531-150">If you want tooknow more about hello various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="09531-151">Report sugli utenti contrassegnati per il rischio</span><span class="sxs-lookup"><span data-stu-id="09531-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="09531-152">Report sugli accessi a rischio</span><span class="sxs-lookup"><span data-stu-id="09531-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="09531-153">Report dei log di controllo</span><span class="sxs-lookup"><span data-stu-id="09531-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="09531-154">Report dei log di accesso</span><span class="sxs-lookup"><span data-stu-id="09531-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="09531-155">Se si desidera tooknow ulteriori informazioni sull'accesso hello hello utilizzando hello API di segnalazione dei dati di report, vedere:</span><span class="sxs-lookup"><span data-stu-id="09531-155">If you want tooknow more about accessing hello hello reporting data using hello reporting API, see:</span></span> 

- [<span data-ttu-id="09531-156">Introduzione a hello reporting API Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09531-156">Getting started with hello Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png