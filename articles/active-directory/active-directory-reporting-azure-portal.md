---
title: Creazione di report in Azure Active Directory | Microsoft Docs
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
ms.openlocfilehash: 738c8f4a56586b87f03973ec258b0a3023affa60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="272d9-103">Creazione di report in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="272d9-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="272d9-104">La creazione di report in Azure Active Directory permette di ottenere informazioni approfondite sullo stato dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="272d9-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="272d9-105">I dati forniti consentono di:</span><span class="sxs-lookup"><span data-stu-id="272d9-105">The provided data enables you to:</span></span>

- <span data-ttu-id="272d9-106">Determinare l'utilizzo di app e servizi da parte degli utenti</span><span class="sxs-lookup"><span data-stu-id="272d9-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="272d9-107">Rilevare rischi potenziali che pregiudicano l'integrità dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="272d9-107">Detect potential risks affecting the health of your environment</span></span>
- <span data-ttu-id="272d9-108">Risolvere problemi che influiscono negativamente sulla produttività degli utenti</span><span class="sxs-lookup"><span data-stu-id="272d9-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="272d9-109">L'architettura dei report si basa su due elementi fondamentali:</span><span class="sxs-lookup"><span data-stu-id="272d9-109">The reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="272d9-110">Report sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="272d9-110">Security reports</span></span>
- <span data-ttu-id="272d9-111">Report sull’attività</span><span class="sxs-lookup"><span data-stu-id="272d9-111">Activity reports</span></span>

![Creazione di report](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="272d9-113">Report sulla sicurezza</span><span class="sxs-lookup"><span data-stu-id="272d9-113">Security reports</span></span>

<span data-ttu-id="272d9-114">I report sulla sicurezza in Azure Active Directory consentono di proteggere le identità dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="272d9-114">The security reports in Azure Active Directory help you to protect your organization's identities.</span></span>  
<span data-ttu-id="272d9-115">Azure Active Directory prevede due tipi di report sulla sicurezza:</span><span class="sxs-lookup"><span data-stu-id="272d9-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="272d9-116">**Utenti contrassegnati per il rischio**: il [report sulla sicurezza relativo agli utenti contrassegni per il rischio](active-directory-reporting-security-user-at-risk.md) offre una panoramica degli account utente che potrebbero essere stati compromessi.</span><span class="sxs-lookup"><span data-stu-id="272d9-116">**Users flagged for risk** - From the [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="272d9-117">**Accessi a rischio**: il [report sulla sicurezza relativo agli accessi a rischio](active-directory-reporting-security-risky-sign-ins.md) offre una indicazione sui tentativi di accesso che potrebbero essere stati eseguiti da qualcuno che non è il legittimo proprietario di un account utente.</span><span class="sxs-lookup"><span data-stu-id="272d9-117">**Risky sign-ins** - With the [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 

<span data-ttu-id="272d9-118">**Quale licenza di Azure AD è necessaria per accedere a un report sulla sicurezza?**</span><span class="sxs-lookup"><span data-stu-id="272d9-118">**What Azure AD license do you need to access a security report?**</span></span>  
<span data-ttu-id="272d9-119">Tutte le edizioni di Azure Active Directory offrono report sugli utenti contrassegnati per il rischio e sugli accessi a rischio.</span><span class="sxs-lookup"><span data-stu-id="272d9-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="272d9-120">Tuttavia, il livello di granularità dei report varia a seconda delle edizioni:</span><span class="sxs-lookup"><span data-stu-id="272d9-120">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="272d9-121">Nelle edizioni **Azure Active Directory Free e Basic**  è già incluso un elenco degli utenti contrassegnati per il rischio e degli accessi a rischio.</span><span class="sxs-lookup"><span data-stu-id="272d9-121">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="272d9-122">Nell'edizione **Azure Active Directory Premium 1** questo modello consente anche di esaminare alcuni degli eventi di rischio sottostanti che sono stati rilevati per ogni report.</span><span class="sxs-lookup"><span data-stu-id="272d9-122">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="272d9-123">L'edizione **Azure Active Directory Premium 2** offre informazioni più dettagliate sugli eventi di rischio sottostanti e permette anche di configurare criteri di sicurezza che rispondono automaticamente a livelli di rischio configurati.</span><span class="sxs-lookup"><span data-stu-id="272d9-123">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about the underlying risk events and it also enables you to configure security policies that automatically respond to configured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="272d9-124">Report sull’attività</span><span class="sxs-lookup"><span data-stu-id="272d9-124">Activity reports</span></span>

<span data-ttu-id="272d9-125">Azure Active Directory prevede due tipi di report sull'attività:</span><span class="sxs-lookup"><span data-stu-id="272d9-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="272d9-126">**Log di controllo**: il [report sull'attività relativo ai log di controllo](active-directory-reporting-activity-audit-logs.md) consente di accedere alla cronologia di ogni attività eseguita nel tenant.</span><span class="sxs-lookup"><span data-stu-id="272d9-126">**Audit logs** - The [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access to the history of every task performed in your tenant.</span></span>

- <span data-ttu-id="272d9-127">**Accessi**: il [report sull'attività relativo agli accessi](active-directory-reporting-activity-sign-ins.md) permette di determinare chi ha eseguito le attività segnalate nel report dei log di controllo.</span><span class="sxs-lookup"><span data-stu-id="272d9-127">**Sign-ins** -  With the [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed the tasks reported by the audit logs report.</span></span>



<span data-ttu-id="272d9-128">Il **report dei log di controllo** include i record delle attività di sistema per la conformità.</span><span class="sxs-lookup"><span data-stu-id="272d9-128">The **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="272d9-129">I dati forniti consentono, tra l'altro, di risolvere scenari comuni. Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="272d9-129">Amongst others, the provided data enables you to address common scenarios such as:</span></span>

- <span data-ttu-id="272d9-130">Un utente del tenant ha avuto accesso a un gruppo amministrativo e</span><span class="sxs-lookup"><span data-stu-id="272d9-130">Someone in my tenant got access to an admin group.</span></span> <span data-ttu-id="272d9-131">si vuole sapere chi ha concesso tale accesso.</span><span class="sxs-lookup"><span data-stu-id="272d9-131">Who gave them access?</span></span> 

- <span data-ttu-id="272d9-132">Si vuole ottenere un elenco degli utenti che accedono a un'app specifica caricata di recente, per sapere se viene usata.</span><span class="sxs-lookup"><span data-stu-id="272d9-132">I want to know the list of users signing into a specific app since I recently onboarded the app and want to know if it’s doing well</span></span>

- <span data-ttu-id="272d9-133">Si vuole conoscere il numero di reimpostazioni della password eseguite nel tenant.</span><span class="sxs-lookup"><span data-stu-id="272d9-133">I want to know how many password resets are happening in my tenant</span></span>


<span data-ttu-id="272d9-134">**Quale licenza di Azure AD è necessaria per accedere al report dei log di controllo?**</span><span class="sxs-lookup"><span data-stu-id="272d9-134">**What Azure AD license do you need to access the audit logs report?**</span></span>  
<span data-ttu-id="272d9-135">Il report dei log di controllo è disponibile per le funzionalità per le quali si possiede una licenza.</span><span class="sxs-lookup"><span data-stu-id="272d9-135">The audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="272d9-136">Se è disponibile una licenza per una funzionalità specifica, si ha anche accesso alle relative informazioni del log di controllo.</span><span class="sxs-lookup"><span data-stu-id="272d9-136">If you have a license for a specific feature, you also have access to the audit log information for it.</span></span>

<span data-ttu-id="272d9-137">Per altre informazioni, vedere il **Confronto tra le funzionalità generalmente disponibili nelle edizioni Free, Basic e Premium**  in [Caratteristiche e funzionalità di Azure Active Directory ](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span><span class="sxs-lookup"><span data-stu-id="272d9-137">For more details, see **Comparing generally available features of the Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="272d9-138">Il **report sull'attività relativo agli accessi** permette di rispondere a domande simili alle seguenti:</span><span class="sxs-lookup"><span data-stu-id="272d9-138">The **sign-ins activity report** enables to to find answers to questions such as:</span></span>

- <span data-ttu-id="272d9-139">Qual è il modello di accesso di un utente?</span><span class="sxs-lookup"><span data-stu-id="272d9-139">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="272d9-140">Quanti utenti hanno effettuato l'accesso nell'arco di una settimana?</span><span class="sxs-lookup"><span data-stu-id="272d9-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="272d9-141">Qual è lo stato di questi accessi?</span><span class="sxs-lookup"><span data-stu-id="272d9-141">What’s the status of these sign-ins?</span></span>


<span data-ttu-id="272d9-142">**Quale licenza di Azure AD è necessaria per accedere al report sull'attività relativo agli accessi?**</span><span class="sxs-lookup"><span data-stu-id="272d9-142">**What Azure AD license do you need to access the sign-ins activity report?**</span></span>  
<span data-ttu-id="272d9-143">Per visualizzare il report sull'attività relativo agli accessi, è necessario che al tenant sia associata una licenza di Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="272d9-143">To access the sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="272d9-144">Accesso a livello di codice</span><span class="sxs-lookup"><span data-stu-id="272d9-144">Programmatic access</span></span>

<span data-ttu-id="272d9-145">Oltre all'interfaccia utente, la creazione di report di Azure Active Directory offre anche l'[accesso a livello di codice](active-directory-reporting-api-getting-started-azure-portal.md) ai dati dei report.</span><span class="sxs-lookup"><span data-stu-id="272d9-145">In addition to the user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) to the reporting data.</span></span> <span data-ttu-id="272d9-146">I dati di questi report possono essere molto utili per le applicazioni, ad esempio i sistemi SIEM e gli strumenti di controllo e business intelligence.</span><span class="sxs-lookup"><span data-stu-id="272d9-146">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="272d9-147">L'API di creazione report di Azure AD fornisce l'accesso ai dati dal codice tramite un set di API basate su REST.</span><span class="sxs-lookup"><span data-stu-id="272d9-147">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="272d9-148">È possibile chiamare le API da numerosi linguaggi di programmazione e strumenti.</span><span class="sxs-lookup"><span data-stu-id="272d9-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="272d9-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="272d9-149">Next steps</span></span>

<span data-ttu-id="272d9-150">Per altre informazioni sui vari tipi di report in Azure Active Directory, vedere:</span><span class="sxs-lookup"><span data-stu-id="272d9-150">If you want to know more about the various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="272d9-151">Report sugli utenti contrassegnati per il rischio</span><span class="sxs-lookup"><span data-stu-id="272d9-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="272d9-152">Report sugli accessi a rischio</span><span class="sxs-lookup"><span data-stu-id="272d9-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="272d9-153">Report dei log di controllo</span><span class="sxs-lookup"><span data-stu-id="272d9-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="272d9-154">Report dei log di accesso</span><span class="sxs-lookup"><span data-stu-id="272d9-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="272d9-155">Per altre informazioni sull'accesso ai dati dei report tramite l'API di creazione report, vedere:</span><span class="sxs-lookup"><span data-stu-id="272d9-155">If you want to know more about accessing the the reporting data using the reporting API, see:</span></span> 

- [<span data-ttu-id="272d9-156">Introduzione all'API di creazione report di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="272d9-156">Getting started with the Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png