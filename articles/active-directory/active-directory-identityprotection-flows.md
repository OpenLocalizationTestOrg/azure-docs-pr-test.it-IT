---
title: Esperienze di accesso con Azure AD Identity Protection | Microsoft Docs
description: "Presenta una panoramica dell'esperienza utente quando Identity Protection ha mitigato o risolto la situazione di rischio di un utente o quando l'autenticazione a più fattori è richiesta da una policy."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestione applicazioni, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: e45936280b51fb2e54012a688fceddcc8dabe984
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="96344-104">Esperienze di accesso con Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="96344-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="96344-105">Con Azure Active Directory Identity Protection è possibile:</span><span class="sxs-lookup"><span data-stu-id="96344-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="96344-106">richiedere la registrazione degli utenti per l'autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="96344-106">require users to register for multi-factor authentication</span></span>
* <span data-ttu-id="96344-107">gestire gli accessi rischiosi e gli utenti compromessi</span><span class="sxs-lookup"><span data-stu-id="96344-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="96344-108">La risposta del sistema a questi problemi ha un impatto sull’esperienza di accesso dell’utente, in quanto non sarà più possibile effettuare l’accesso in modo diretto fornendo semplicemente il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="96344-108">The response of the system to these issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="96344-109">Saranno necessari passaggi aggiuntivi per consentire all’utente un accesso sicuro al sistema.</span><span class="sxs-lookup"><span data-stu-id="96344-109">Additional steps are required to get a user safely back into business.</span></span>

<span data-ttu-id="96344-110">Questo argomento presenta una panoramica dell'esperienza di accesso dell'utente per tutti i casi possibili.</span><span class="sxs-lookup"><span data-stu-id="96344-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="96344-111">**Autenticazione a più fattori**</span><span class="sxs-lookup"><span data-stu-id="96344-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="96344-112">Registrazione per l'autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="96344-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="96344-113">**Accesso a rischio**</span><span class="sxs-lookup"><span data-stu-id="96344-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="96344-114">Ripristino di un accesso rischioso</span><span class="sxs-lookup"><span data-stu-id="96344-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="96344-115">Accesso rischioso bloccato</span><span class="sxs-lookup"><span data-stu-id="96344-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="96344-116">Registrazione per l'autenticazione a più fattori durante un accesso rischioso</span><span class="sxs-lookup"><span data-stu-id="96344-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="96344-117">**Utente a rischio**</span><span class="sxs-lookup"><span data-stu-id="96344-117">**User at risk**</span></span>

* <span data-ttu-id="96344-118">Ripristino di account compromessi</span><span class="sxs-lookup"><span data-stu-id="96344-118">Compromised account recovery</span></span>
* <span data-ttu-id="96344-119">Account compromesso bloccato</span><span class="sxs-lookup"><span data-stu-id="96344-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="96344-120">Registrazione per l'autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="96344-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="96344-121">Sia per il ripristino di un account compromesso che per l'accesso rischioso, la migliore esperienza utente si ottiene quando l'utente può eseguire il ripristino automatico.</span><span class="sxs-lookup"><span data-stu-id="96344-121">The best user experience for both, the compromised account recovery flow and the risky sign-in flow, is when the user can self-recover.</span></span> <span data-ttu-id="96344-122">Se gli utenti sono registrati per l’autenticazione a più fattori, hanno già un numero di telefono associato con l’account che può essere usato per trasmettere le richieste di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="96344-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used to pass security challenges.</span></span> <span data-ttu-id="96344-123">Non è necessario coinvolgere il supporto tecnico o l'amministratore per ripristinare un account compromesso.</span><span class="sxs-lookup"><span data-stu-id="96344-123">No help desk or administrator involvement is needed to recover from account compromise.</span></span> <span data-ttu-id="96344-124">È quindi consigliabile fare in modo che gli utenti siano registrati per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="96344-124">Thus, it’s highly recommended to get your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="96344-125">Gli amministratori possono:</span><span class="sxs-lookup"><span data-stu-id="96344-125">Administrators can:</span></span>

* <span data-ttu-id="96344-126">Impostare criteri che richiedono agli utenti di configurare l'account per la verifica di sicurezza aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="96344-126">set a policy that requires users to set up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="96344-127">Consentire di ignorare la registrazione per l'autenticazione a più fattori per un massimo di 30 giorni, per dare agli utenti un periodo di tolleranza prima della registrazione.</span><span class="sxs-lookup"><span data-stu-id="96344-127">allow skipping multi-factor authentication registration for up to 30 days, in case they want to give users a grace period before registering.</span></span>

<span data-ttu-id="96344-128">**La registrazione per l’autenticazione a più fattori prevede tre passaggi:**</span><span class="sxs-lookup"><span data-stu-id="96344-128">**The multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="96344-129">Nel primo passaggio l'utente riceve una notifica della necessità di impostare l'account per l’autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="96344-129">In the first step, the user gets a notification about the requirement to set the account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="96344-130">![Correzione](./media/active-directory-identityprotection-flows/140.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="96344-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="96344-131">Per impostare l'autenticazione a più fattori, occorre indicare al sistema in che modo si desidera essere contattati.</span><span class="sxs-lookup"><span data-stu-id="96344-131">To set multi-factor authentication up, you need to let the system know how you want to be contacted.</span></span>
   
    <span data-ttu-id="96344-132">![Correzione](./media/active-directory-identityprotection-flows/141.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="96344-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="96344-133">Il sistema invia una richiesta ed è necessario rispondere.</span><span class="sxs-lookup"><span data-stu-id="96344-133">The system submits a challenge to you and you need to respond.</span></span>
   
    <span data-ttu-id="96344-134">![Correzione](./media/active-directory-identityprotection-flows/142.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="96344-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="96344-135">Ripristino di un accesso rischioso</span><span class="sxs-lookup"><span data-stu-id="96344-135">Risky sign-in recovery</span></span>
<span data-ttu-id="96344-136">Se un amministratore ha configurato dei criteri per i rischi di accesso, gli utenti interessati ricevono una notifica quando provano ad accedere.</span><span class="sxs-lookup"><span data-stu-id="96344-136">When an administrator has configured a policy for sign-in risks, the affected users are notified when they try to sign-in.</span></span> 

<span data-ttu-id="96344-137">**Il flusso per l'accesso rischioso prevede due passaggi:**</span><span class="sxs-lookup"><span data-stu-id="96344-137">**The risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="96344-138">L’utente è informato del fatto che qualcosa di insolito è stato rilevato in merito al suo accesso, ad esempio l’accesso da una nuova posizione, dispositivo o app.</span><span class="sxs-lookup"><span data-stu-id="96344-138">The user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="96344-139">![Correzione](./media/active-directory-identityprotection-flows/120.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="96344-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="96344-140">L'utente deve dimostrare la propria identità rispondendo a una richiesta di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="96344-140">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="96344-141">Se l'utente è registrato per l'autenticazione a più fattori, deve eseguire il round trip di un codice di sicurezza al proprio numero di telefono.</span><span class="sxs-lookup"><span data-stu-id="96344-141">If the user is registered for multi-factor authentication they need to round-trip a security code to their phone number.</span></span> <span data-ttu-id="96344-142">Poiché questo è solo un accesso rischioso e non un account compromesso, l’utente non dovrà cambiare la password in questo flusso.</span><span class="sxs-lookup"><span data-stu-id="96344-142">Since this is a just a risky sign in and not a compromised account, the user won’t have to change the password in this flow.</span></span> 
   
    <span data-ttu-id="96344-143">![Correzione](./media/active-directory-identityprotection-flows/121.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="96344-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="96344-144">Accesso rischioso bloccato</span><span class="sxs-lookup"><span data-stu-id="96344-144">Risky sign-in blocked</span></span>
<span data-ttu-id="96344-145">Gli amministratori possono anche impostare criteri di rischio di accesso per bloccare gli utenti al momento dell'accesso in base al livello di rischio.</span><span class="sxs-lookup"><span data-stu-id="96344-145">Administrators can also choose to set a Sign-In Risk policy to block users upon sign-in depending on the risk level.</span></span> <span data-ttu-id="96344-146">Per essere sbloccati, gli utenti finali devono contattare un amministratore o il supporto tecnico oppure possono provare a eseguire l'accesso da una posizione o un dispositivo noto.</span><span class="sxs-lookup"><span data-stu-id="96344-146">To get unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="96344-147">Il ripristino automatico tramite l'autenticazione a più fattori non è possibile in questo caso.</span><span class="sxs-lookup"><span data-stu-id="96344-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="96344-148">![Correzione](./media/active-directory-identityprotection-flows/200.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="96344-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="96344-149">Ripristino di account compromessi</span><span class="sxs-lookup"><span data-stu-id="96344-149">Compromised account recovery</span></span>
<span data-ttu-id="96344-150">Dopo che sono stati configurati criteri di sicurezza per il rischio utente, gli utenti che rientrano nel livello di rischio utente specificato nei criteri, e quindi considerati compromessi, devono seguire il flusso di ripristino di utenti compromessi per poter eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="96344-150">When a user risk security policy has been configured, users who meet the user risk level specified in the policy (and are therefore assumed compromised) must go through the user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="96344-151">**Il flusso di ripristino di utenti compromessi è composto da tre passaggi:**</span><span class="sxs-lookup"><span data-stu-id="96344-151">**The user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="96344-152">L'utente viene informato che la sicurezza dell'account è a rischio a causa di attività sospette o di credenziali perse.</span><span class="sxs-lookup"><span data-stu-id="96344-152">The user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="96344-153">![Correzione](./media/active-directory-identityprotection-flows/101.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="96344-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="96344-154">L'utente deve dimostrare la propria identità rispondendo a una richiesta di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="96344-154">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="96344-155">Se l'utente è registrato per l'autenticazione a più fattori può eseguire il ripristino automatico da eventuali compromissioni.</span><span class="sxs-lookup"><span data-stu-id="96344-155">If the user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="96344-156">Deve eseguire il round trip di un codice di sicurezza al proprio numero di telefono.</span><span class="sxs-lookup"><span data-stu-id="96344-156">They will need to round-trip a security code to their phone number.</span></span> 
   
   <span data-ttu-id="96344-157">![Correzione](./media/active-directory-identityprotection-flows/110.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="96344-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="96344-158">Infine, all'utente viene richiesto di modificare la password perché qualcun altro potrebbe aver avuto accesso all'account.</span><span class="sxs-lookup"><span data-stu-id="96344-158">Finally, the user is forced to change their password since someone else may have had access to their account.</span></span> 
   <span data-ttu-id="96344-159">Sono incluse per riferimento le screenshot di questa esperienza.</span><span class="sxs-lookup"><span data-stu-id="96344-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="96344-160">![Correzione](./media/active-directory-identityprotection-flows/111.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="96344-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="96344-161">Account compromesso bloccato</span><span class="sxs-lookup"><span data-stu-id="96344-161">Compromised account blocked</span></span>
<span data-ttu-id="96344-162">Per sbloccare un utente bloccato da criteri di sicurezza per il rischio utente, è necessario contattare un amministratore o il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="96344-162">To get a user that was blocked by a user risk security policy unblocked, the user must contact an administrator or help desk.</span></span> <span data-ttu-id="96344-163">Il ripristino automatico tramite l'autenticazione a più fattori non è possibile in questo caso.</span><span class="sxs-lookup"><span data-stu-id="96344-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="96344-164">![Correzione](./media/active-directory-identityprotection-flows/104.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="96344-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="96344-165">Reimpostazione delle password</span><span class="sxs-lookup"><span data-stu-id="96344-165">Reset password</span></span>
<span data-ttu-id="96344-166">Se l’accesso degli utenti compromessi è bloccato, un amministratore può generare una password temporanea per consentire l’accesso.</span><span class="sxs-lookup"><span data-stu-id="96344-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="96344-167">Gli utenti dovranno modificare la password all'accesso successivo.</span><span class="sxs-lookup"><span data-stu-id="96344-167">The users will have to change their password during a next sign-in.</span></span>

<span data-ttu-id="96344-168">![Correzione](./media/active-directory-identityprotection-flows/160.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="96344-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="96344-169">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="96344-169">See also</span></span>
* [<span data-ttu-id="96344-170">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="96344-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

