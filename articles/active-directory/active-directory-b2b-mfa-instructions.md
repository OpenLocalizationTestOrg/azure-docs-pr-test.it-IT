---
title: Accesso condizionale per gli utenti di Collaborazione B2B di Azure Active Directory | Microsoft Docs
description: "La Collaborazione B2B di Azure Active Directory supporta l'autenticazione a più fattori (MFA) per l'accesso selettivo alle applicazioni aziendali"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: d85f711d6551a68d1248ae8ec61e2ecc1ddc8ecd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="77c8f-103">Accesso condizionale per gli utenti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="77c8f-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="77c8f-104">Autenticazione a più fattori per gli utenti B2B</span><span class="sxs-lookup"><span data-stu-id="77c8f-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="77c8f-105">Con Collaborazione B2B di Azure AD, le organizzazioni possono applicare criteri di autenticazione a più fattori (MFA) per gli utenti B2B.</span><span class="sxs-lookup"><span data-stu-id="77c8f-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="77c8f-106">Questi criteri possono essere applicati a livello di tenant, di app o di singolo utente, così come vengono abilitati per dipendenti a tempo pieno e membri dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="77c8f-106">These policies can be enforced at the tenant, app, or individual user level, the same way that they are enabled for full-time employees and members of the organization.</span></span> <span data-ttu-id="77c8f-107">I criteri di autenticazione a più fattori (MFA) vengono applicati all'organizzazione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="77c8f-107">MFA policies are enforced at the resource organization.</span></span>

<span data-ttu-id="77c8f-108">Esempio:</span><span class="sxs-lookup"><span data-stu-id="77c8f-108">Example:</span></span>
1. <span data-ttu-id="77c8f-109">Un amministratore o un information worker della società A invita gli utenti della società B in un'applicazione *Foo* della società A.</span><span class="sxs-lookup"><span data-stu-id="77c8f-109">Admin or information worker in Company A invites user from company B to an application *Foo* in company A.</span></span>
2. <span data-ttu-id="77c8f-110">L'applicazione *Foo* nella società A è configurata per richiedere l'autenticazione a più fattori all'accesso.</span><span class="sxs-lookup"><span data-stu-id="77c8f-110">Application *Foo* in company A is configured to require MFA on access.</span></span>
3. <span data-ttu-id="77c8f-111">Quando l'utente della società B tenta di accedere all'app *Foo* nel tenant della società A, gli viene chiesto di completare una richiesta di autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="77c8f-111">When the user from company B attempts to access app *Foo* in the company A tenant, they are asked to complete an MFA challenge.</span></span>
4. <span data-ttu-id="77c8f-112">L'utente può configurare la propria autenticazione a più fattori con la società A e ne sceglie l'opzione MFA.</span><span class="sxs-lookup"><span data-stu-id="77c8f-112">The user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="77c8f-113">Questo scenario funziona per qualsiasi identità, ad esempio di Azure AD o account del servizio gestito, se gli utenti della società B eseguono l'autenticazione usando un ID per social network.</span><span class="sxs-lookup"><span data-stu-id="77c8f-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="77c8f-114">La società A deve avere un numero sufficiente di licenze di Azure AD Premium che supportano l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="77c8f-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="77c8f-115">L'utente della società B utilizza la licenza della società A.</span><span class="sxs-lookup"><span data-stu-id="77c8f-115">The user from company B consumes this license from company A.</span></span>

<span data-ttu-id="77c8f-116">La tenancy che emette l'invito è sempre responsabile dell'autenticazione a più fattori degli utenti dell'organizzazione partner, anche se l'organizzazione partner ha funzionalità di autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="77c8f-116">The inviting tenancy is always responsible for MFA for users from the partner organization, even if the partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="77c8f-117">Configurazione dell'autenticazione a più fattori per gli utenti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="77c8f-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="77c8f-118">La configurazione di MFA per gli utenti di Collaborazione B2B è estremamente semplice, come illustrato nel video seguente:</span><span class="sxs-lookup"><span data-stu-id="77c8f-118">To discover how easy it is to set up MFA for B2B collaboration users, see how in the following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="77c8f-119">Esperienza di autenticazione a più fattori per gli utenti di B2B per il riscatto dell'offerta</span><span class="sxs-lookup"><span data-stu-id="77c8f-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="77c8f-120">Guardare l'animazione seguente per visualizzare l'esperienza di riscatto:</span><span class="sxs-lookup"><span data-stu-id="77c8f-120">Check out the following animation to see the redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="77c8f-121">Reimpostazione dell'autenticazione a più fattori per gli utenti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="77c8f-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="77c8f-122">L'amministratore attualmente può richiedere agli utenti di Collaborazione B2B di ripetere l'identificazione solo usando i cmdlet di PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="77c8f-122">Currently, the admin can require B2B collaboration users to proof up again only by using the following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="77c8f-123">Connettersi ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="77c8f-123">Connect to Azure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="77c8f-124">Ottenere tutti gli utenti con metodi di identificazione</span><span class="sxs-lookup"><span data-stu-id="77c8f-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="77c8f-125">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="77c8f-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="77c8f-126">Reimpostare il metodo di autenticazione a più fattori per un utente specifico in modo da richiedere all'utente di Collaborazione B2B di impostare di nuovo i metodi di identificazione.</span><span class="sxs-lookup"><span data-stu-id="77c8f-126">Reset the MFA method for a specific user to require the B2B collaboration user to set proof-up methods again.</span></span> <span data-ttu-id="77c8f-127">Esempio:</span><span class="sxs-lookup"><span data-stu-id="77c8f-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-the-resource-tenancy"></a><span data-ttu-id="77c8f-128">Perché si esegue un'autenticazione a più fattori nella tenancy delle risorse?</span><span class="sxs-lookup"><span data-stu-id="77c8f-128">Why do we perform MFA at the resource tenancy?</span></span>

<span data-ttu-id="77c8f-129">Nella versione corrente, l'autenticazione a più fattori è sempre nella tenancy delle risorse, per motivi di prevedibilità.</span><span class="sxs-lookup"><span data-stu-id="77c8f-129">In the current release, MFA is always in the resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="77c8f-130">Ad esempio, si supponga che un utente di Contoso (Sara) riceve un invito da Fabrikam e Fabrikam ha abilitato l'autenticazione a più fattori per gli utenti B2B.</span><span class="sxs-lookup"><span data-stu-id="77c8f-130">For example, let’s say a Contoso user (Sally) is invited to Fabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="77c8f-131">Se Contoso ha abilitato i criteri di autenticazione a più fattori per App1 ma non per App2, esaminando l'attestazione MFA di Contoso nel token si potrebbe riscontrare il problema seguente.</span><span class="sxs-lookup"><span data-stu-id="77c8f-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at the Contoso MFA claim in the token, we might see the following issue:</span></span>

* <span data-ttu-id="77c8f-132">Giorno 1: un utente con autenticazione a più fattori in Contoso accede ad App1 e non viene quindi visualizzata una richiesta MFA aggiuntiva in Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="77c8f-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="77c8f-133">Giorno 2: l'utente ha eseguito l'accesso ad App2 in Contoso e quando accede a Fabrikam deve eseguirvi la registrazione al servizio MFA.</span><span class="sxs-lookup"><span data-stu-id="77c8f-133">Day 2: The user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="77c8f-134">Questo processo può generare confusione e determinare una riduzione del numero di accessi completati.</span><span class="sxs-lookup"><span data-stu-id="77c8f-134">This process can be confusing and could lead to drop in sign-in completions.</span></span>

<span data-ttu-id="77c8f-135">In aggiunta, anche se Contoso ha una funzionalità di autenticazione a più fattori, non è sempre probabile che Fabrikam accetti i criteri di autenticazione a più fattori di Contoso.</span><span class="sxs-lookup"><span data-stu-id="77c8f-135">Moreover, even if Contoso has MFA capability, it is not always the case the Fabrikam would trust the Contoso MFA policy.</span></span>

<span data-ttu-id="77c8f-136">Infine, l'autenticazione a più fattori del tenant delle risorse funziona anche per account del servizio gestito, ID per social network e organizzazioni partner che non hanno configurato l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="77c8f-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="77c8f-137">Di conseguenza, per l'autenticazione a più fattori degli utenti B2B è consigliabile richiedere sempre l'autenticazione a più fattori nel tenant che emette l'invito.</span><span class="sxs-lookup"><span data-stu-id="77c8f-137">Therefore, the recommendation for MFA for B2B users is to always require MFA in the inviting tenant.</span></span> <span data-ttu-id="77c8f-138">Questo requisito potrebbe causare la duplicazione dell'autenticazione a più fattori in alcuni casi, ma l'esperienza degli utenti finali è prevedibile a ogni accesso al tenant che emette l'invito: l'utente deve eseguire la registrazione al servizio MFA con tale tenant.</span><span class="sxs-lookup"><span data-stu-id="77c8f-138">This requirement could lead to double MFA in some cases, but whenever accessing the inviting tenant, the end-users experience is predictable: Sally must register for MFA with the inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="77c8f-139">Accesso condizionale basato sul dispositivo, sulla posizione e sui rischi per gli utenti B2B</span><span class="sxs-lookup"><span data-stu-id="77c8f-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="77c8f-140">Quando Contoso abilita criteri di accesso condizionale basati sul dispositivo per i dati aziendali, viene impedito l'accesso da dispositivi non gestiti da Contoso e non conformi ai criteri dei dispositivi di Contoso.</span><span class="sxs-lookup"><span data-stu-id="77c8f-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with the Contoso device policies.</span></span>

<span data-ttu-id="77c8f-141">Se il dispositivo dell'utente B2B non è gestito da Contoso, l'accesso degli utenti B2B delle organizzazioni partner viene bloccato in qualsiasi contesto vengano applicati i criteri.</span><span class="sxs-lookup"><span data-stu-id="77c8f-141">If the B2B user’s device isn't managed by Contoso, access of B2B users from the partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="77c8f-142">Contoso, tuttavia, può creare elenchi di esclusione contenenti gli utenti di partner specifici per escluderli dai criteri di accesso condizionale basati sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="77c8f-142">However, Contoso can create exclusion lists containing specific partner users to exclude them from the device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="77c8f-143">Accesso condizionale basato sulla posizione per B2B</span><span class="sxs-lookup"><span data-stu-id="77c8f-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="77c8f-144">I criteri di accesso condizionale basati sulla posizione possono essere applicati per gli utenti B2B se l'organizzazione che emette l'invito può creare un intervallo di indirizzi IP attendibili che definisce le organizzazioni partner.</span><span class="sxs-lookup"><span data-stu-id="77c8f-144">Location-based conditional access policies can be enforced for B2B users if the inviting organization is able to create a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="77c8f-145">Accesso condizionale basato sui rischi per B2B</span><span class="sxs-lookup"><span data-stu-id="77c8f-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="77c8f-146">Attualmente non è possibile applicare criteri di accesso basati sui rischi agli utenti B2B, perché la valutazione dei rischi viene eseguita nell'organizzazione principale dell'utente B2B.</span><span class="sxs-lookup"><span data-stu-id="77c8f-146">Currently, risk-based sign-in policies cannot be applied to B2B users because the risk evaluation is performed at the B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77c8f-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77c8f-147">Next steps</span></span>

<span data-ttu-id="77c8f-148">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="77c8f-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="77c8f-149">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="77c8f-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="77c8f-150">Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori</span><span class="sxs-lookup"><span data-stu-id="77c8f-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="77c8f-151">Procedura di aggiunta di utenti di Collaborazione B2B da parte di information worker</span><span class="sxs-lookup"><span data-stu-id="77c8f-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="77c8f-152">Elementi del messaggio di posta elettronica di invito per la Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="77c8f-152">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="77c8f-153">Riscatto dell'invito di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="77c8f-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="77c8f-154">Licenze per la Collaborazione B2B di Azure AD</span><span class="sxs-lookup"><span data-stu-id="77c8f-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="77c8f-155">Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77c8f-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="77c8f-156">Domande frequenti su Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77c8f-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="77c8f-157">API e personalizzazione per Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77c8f-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="77c8f-158">Aggiungere gli utenti per la Collaborazione B2B senza un invito</span><span class="sxs-lookup"><span data-stu-id="77c8f-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="77c8f-159">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77c8f-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
