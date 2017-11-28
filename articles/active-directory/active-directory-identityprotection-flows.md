---
title: esperienze di aaaSign con Azure AD Identity Protection | Documenti Microsoft
description: "Fornisce una panoramica di esperienza utente hello quando la protezione dell'identità è risolti o aggiornato un utente o quando è necessario effettuare l'autenticazione di multi-factor un criterio."
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
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="bb9f4-104">Esperienze di accesso con Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="bb9f4-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="bb9f4-105">Con Azure Active Directory Identity Protection è possibile:</span><span class="sxs-lookup"><span data-stu-id="bb9f4-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="bb9f4-106">Richiedi tooregister utenti multi-factor Authentication</span><span class="sxs-lookup"><span data-stu-id="bb9f4-106">require users tooregister for multi-factor authentication</span></span>
* <span data-ttu-id="bb9f4-107">gestire gli accessi rischiosi e gli utenti compromessi</span><span class="sxs-lookup"><span data-stu-id="bb9f4-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="bb9f4-108">risposta Hello dei problemi di hello sistema toothese ha impatto sull'esperienza di accesso dell'utente, poiché solo direttamente firma-in, fornendo un nome utente e una password non essere possibile più.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-108">hello response of hello system toothese issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="bb9f4-109">Ulteriori passaggi sono necessari tooget un utente in modo sicuro allo stato di business.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-109">Additional steps are required tooget a user safely back into business.</span></span>

<span data-ttu-id="bb9f4-110">Questo argomento presenta una panoramica dell'esperienza di accesso dell'utente per tutti i casi possibili.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="bb9f4-111">**Autenticazione a più fattori**</span><span class="sxs-lookup"><span data-stu-id="bb9f4-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="bb9f4-112">Registrazione per l'autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="bb9f4-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="bb9f4-113">**Accesso a rischio**</span><span class="sxs-lookup"><span data-stu-id="bb9f4-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="bb9f4-114">Ripristino di un accesso rischioso</span><span class="sxs-lookup"><span data-stu-id="bb9f4-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="bb9f4-115">Accesso rischioso bloccato</span><span class="sxs-lookup"><span data-stu-id="bb9f4-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="bb9f4-116">Registrazione per l'autenticazione a più fattori durante un accesso rischioso</span><span class="sxs-lookup"><span data-stu-id="bb9f4-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="bb9f4-117">**Utente a rischio**</span><span class="sxs-lookup"><span data-stu-id="bb9f4-117">**User at risk**</span></span>

* <span data-ttu-id="bb9f4-118">Ripristino di account compromessi</span><span class="sxs-lookup"><span data-stu-id="bb9f4-118">Compromised account recovery</span></span>
* <span data-ttu-id="bb9f4-119">Account compromesso bloccato</span><span class="sxs-lookup"><span data-stu-id="bb9f4-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="bb9f4-120">Registrazione per l'autenticazione a più fattori</span><span class="sxs-lookup"><span data-stu-id="bb9f4-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="bb9f4-121">Hello un'esperienza utente ottimale sia per, hello flusso di ripristino di un account compromesso hello rischioso flusso di accesso, quando l'utente hello autonomo è possibile ripristinare.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-121">hello best user experience for both, hello compromised account recovery flow and hello risky sign-in flow, is when hello user can self-recover.</span></span> <span data-ttu-id="bb9f4-122">Se gli utenti sono registrati per l'autenticazione a più fattori, si dispone già di un numero di telefono associato all'account che possono essere utilizzati toopass problematiche di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used toopass security challenges.</span></span> <span data-ttu-id="bb9f4-123">Alcun modo coinvolta tecnico o l'amministratore della Guida non è necessario toorecover da eventuali compromissioni account.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-123">No help desk or administrator involvement is needed toorecover from account compromise.</span></span> <span data-ttu-id="bb9f4-124">Pertanto, è consigliabile tooget agli utenti registrati per l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-124">Thus, it’s highly recommended tooget your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="bb9f4-125">Gli amministratori possono:</span><span class="sxs-lookup"><span data-stu-id="bb9f4-125">Administrators can:</span></span>

* <span data-ttu-id="bb9f4-126">impostare un criterio che richiede tooset agli utenti di account per la verifica aggiuntiva di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-126">set a policy that requires users tooset up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="bb9f4-127">Consenti registrazione multi-factor authentication per i giorni di too30 ignorata nel caso in cui si desidera che gli utenti toogive prima di registrare un periodo di tolleranza.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-127">allow skipping multi-factor authentication registration for up too30 days, in case they want toogive users a grace period before registering.</span></span>

<span data-ttu-id="bb9f4-128">**registrazione con l'autenticazione a più fattori Hello prevede tre passaggi:**</span><span class="sxs-lookup"><span data-stu-id="bb9f4-128">**hello multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="bb9f4-129">Nel primo passaggio hello, utente hello Ottiene una notifica sull'account di hello requisito tooset hello per multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-129">In hello first step, hello user gets a notification about hello requirement tooset hello account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="bb9f4-130">![Correzione](./media/active-directory-identityprotection-flows/140.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="bb9f4-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="bb9f4-131">autenticazione a più fattori tooset backup, è necessario system hello toolet sapere come si desidera toobe contattato.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-131">tooset multi-factor authentication up, you need toolet hello system know how you want toobe contacted.</span></span>
   
    <span data-ttu-id="bb9f4-132">![Correzione](./media/active-directory-identityprotection-flows/141.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="bb9f4-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="bb9f4-133">sistema Hello invia una richiesta tooyou ed è necessario toorespond.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-133">hello system submits a challenge tooyou and you need toorespond.</span></span>
   
    <span data-ttu-id="bb9f4-134">![Correzione](./media/active-directory-identityprotection-flows/142.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="bb9f4-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="bb9f4-135">Ripristino di un accesso rischioso</span><span class="sxs-lookup"><span data-stu-id="bb9f4-135">Risky sign-in recovery</span></span>
<span data-ttu-id="bb9f4-136">Quando un amministratore ha configurato un criterio per i rischi di accesso, gli utenti di hello interessato vengono informati quando tentano di toosign-in.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-136">When an administrator has configured a policy for sign-in risks, hello affected users are notified when they try toosign-in.</span></span> 

<span data-ttu-id="bb9f4-137">**flusso Hello rischiosa Accedi prevede due passaggi:**</span><span class="sxs-lookup"><span data-stu-id="bb9f4-137">**hello risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="bb9f4-138">utente di Hello viene informato che qualcosa di sospetto è stato rilevato sulla loro l'accesso in, ad esempio la firma un nuovo percorso, un dispositivo o app.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-138">hello user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="bb9f4-139">![Correzione](./media/active-directory-identityprotection-flows/120.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="bb9f4-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="bb9f4-140">utente Hello è obbligatorio tooprove la propria identità risolvendo un problema di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-140">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="bb9f4-141">Se l'utente hello è registrato per l'autenticazione a più fattori devono tooround-trip un numero di telefono tootheir codice di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-141">If hello user is registered for multi-factor authentication they need tooround-trip a security code tootheir phone number.</span></span> <span data-ttu-id="bb9f4-142">Poiché si tratta di un solo di un accesso rischioso e non un account compromesso, utente hello avrà password hello toochange in questo flusso.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-142">Since this is a just a risky sign in and not a compromised account, hello user won’t have toochange hello password in this flow.</span></span> 
   
    <span data-ttu-id="bb9f4-143">![Correzione](./media/active-directory-identityprotection-flows/121.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="bb9f4-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="bb9f4-144">Accesso rischioso bloccato</span><span class="sxs-lookup"><span data-stu-id="bb9f4-144">Risky sign-in blocked</span></span>
<span data-ttu-id="bb9f4-145">Gli amministratori possono anche scegliere tooset un rischio di accesso criteri tooblock di utenti al momento dell'accesso in base al livello di rischio hello.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-145">Administrators can also choose tooset a Sign-In Risk policy tooblock users upon sign-in depending on hello risk level.</span></span> <span data-ttu-id="bb9f4-146">tooget sbloccato, gli utenti finali deve contattare un amministratore o al supporto tecnico o tentano l'accesso da una posizione familiare o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-146">tooget unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="bb9f4-147">Il ripristino automatico tramite l'autenticazione a più fattori non è possibile in questo caso.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="bb9f4-148">![Correzione](./media/active-directory-identityprotection-flows/200.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="bb9f4-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="bb9f4-149">Ripristino di account compromessi</span><span class="sxs-lookup"><span data-stu-id="bb9f4-149">Compromised account recovery</span></span>
<span data-ttu-id="bb9f4-150">Quando è stato configurato un criterio di sicurezza utente dei rischi, gli utenti che soddisfano utente hello corre il rischio livello specificato nei criteri di hello (e pertanto vengono considerati compromessi) devono transitare attraverso hello utente compromissione ripristino flusso prima che essi possono Accedi.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-150">When a user risk security policy has been configured, users who meet hello user risk level specified in hello policy (and are therefore assumed compromised) must go through hello user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="bb9f4-151">**flusso di ripristino di Hello utente compromissione include tre passaggi:**</span><span class="sxs-lookup"><span data-stu-id="bb9f4-151">**hello user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="bb9f4-152">Hello utente viene informato che la sicurezza dell'account è a rischio a causa di attività sospette o perdita di credenziali.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-152">hello user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="bb9f4-153">![Correzione](./media/active-directory-identityprotection-flows/101.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="bb9f4-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="bb9f4-154">utente Hello è obbligatorio tooprove la propria identità risolvendo un problema di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-154">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="bb9f4-155">Se l'utente hello è registrato per l'autenticazione a più fattori è possibile self-ripristinare vengano compromessi.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-155">If hello user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="bb9f4-156">Sarà necessario tooround-trip un numero di telefono tootheir codice di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-156">They will need tooround-trip a security code tootheir phone number.</span></span> 
   
   <span data-ttu-id="bb9f4-157">![Correzione](./media/active-directory-identityprotection-flows/110.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="bb9f4-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="bb9f4-158">Infine, hello utente è forzato toochange la password poiché qualcun altro abbia avuto accesso tootheir account.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-158">Finally, hello user is forced toochange their password since someone else may have had access tootheir account.</span></span> 
   <span data-ttu-id="bb9f4-159">Sono incluse per riferimento le screenshot di questa esperienza.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="bb9f4-160">![Correzione](./media/active-directory-identityprotection-flows/111.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="bb9f4-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="bb9f4-161">Account compromesso bloccato</span><span class="sxs-lookup"><span data-stu-id="bb9f4-161">Compromised account blocked</span></span>
<span data-ttu-id="bb9f4-162">un utente che è stato bloccato da un criterio di sicurezza utente dei rischi sbloccato tooget, hello, l'utente deve contattare un amministratore o il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-162">tooget a user that was blocked by a user risk security policy unblocked, hello user must contact an administrator or help desk.</span></span> <span data-ttu-id="bb9f4-163">Il ripristino automatico tramite l'autenticazione a più fattori non è possibile in questo caso.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="bb9f4-164">![Correzione](./media/active-directory-identityprotection-flows/104.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="bb9f4-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="bb9f4-165">Reimpostazione delle password</span><span class="sxs-lookup"><span data-stu-id="bb9f4-165">Reset password</span></span>
<span data-ttu-id="bb9f4-166">Se l’accesso degli utenti compromessi è bloccato, un amministratore può generare una password temporanea per consentire l’accesso.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="bb9f4-167">Hello gli utenti avranno toochange la propria password durante un successivo accesso in.</span><span class="sxs-lookup"><span data-stu-id="bb9f4-167">hello users will have toochange their password during a next sign-in.</span></span>

<span data-ttu-id="bb9f4-168">![Correzione](./media/active-directory-identityprotection-flows/160.png "Correzione")</span><span class="sxs-lookup"><span data-stu-id="bb9f4-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="bb9f4-169">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="bb9f4-169">See also</span></span>
* [<span data-ttu-id="bb9f4-170">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="bb9f4-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

