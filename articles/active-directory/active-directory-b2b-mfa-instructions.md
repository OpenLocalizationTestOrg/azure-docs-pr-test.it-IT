---
title: l'accesso per gli utenti di collaborazione B2B di Azure Active Directory aaaConditional | Documenti Microsoft
description: Collaborazione B2B di Active Directory di Azure supporta multi-factor authentication (MFA) per applicazioni aziendali di accesso selettivo tooyour
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
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="15fe8-103">Accesso condizionale per gli utenti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="15fe8-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="15fe8-104">Autenticazione a più fattori per gli utenti B2B</span><span class="sxs-lookup"><span data-stu-id="15fe8-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="15fe8-105">Con Collaborazione B2B di Azure AD, le organizzazioni possono applicare criteri di autenticazione a più fattori (MFA) per gli utenti B2B.</span><span class="sxs-lookup"><span data-stu-id="15fe8-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="15fe8-106">Questi criteri possono essere applicati al tenant di hello, app o il livello di singolo utente, hello allo stesso modo che sono abilitate per i dipendenti a tempo pieno e i membri dell'organizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="15fe8-106">These policies can be enforced at hello tenant, app, or individual user level, hello same way that they are enabled for full-time employees and members of hello organization.</span></span> <span data-ttu-id="15fe8-107">Criteri di autenticazione a più fattori vengono applicati all'organizzazione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="15fe8-107">MFA policies are enforced at hello resource organization.</span></span>

<span data-ttu-id="15fe8-108">Esempio:</span><span class="sxs-lookup"><span data-stu-id="15fe8-108">Example:</span></span>
1. <span data-ttu-id="15fe8-109">Lavoro informazioni o di amministrazione nella società invita l'utente dall'applicazione della società B tooan *Foo* nella società A.</span><span class="sxs-lookup"><span data-stu-id="15fe8-109">Admin or information worker in Company A invites user from company B tooan application *Foo* in company A.</span></span>
2. <span data-ttu-id="15fe8-110">Applicazione *Foo* società A è configurato toorequire MFA accesso.</span><span class="sxs-lookup"><span data-stu-id="15fe8-110">Application *Foo* in company A is configured toorequire MFA on access.</span></span>
3. <span data-ttu-id="15fe8-111">Quando di tenta app tooaccess utente hello dalla società B *Foo* società hello un tenant, sono frequenti toocomplete una richiesta di autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="15fe8-111">When hello user from company B attempts tooaccess app *Foo* in hello company A tenant, they are asked toocomplete an MFA challenge.</span></span>
4. <span data-ttu-id="15fe8-112">Hello utente può impostare i relativi MFA con la società e sceglie l'opzione di autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="15fe8-112">hello user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="15fe8-113">Questo scenario funziona per qualsiasi identità, ad esempio di Azure AD o account del servizio gestito, se gli utenti della società B eseguono l'autenticazione usando un ID per social network.</span><span class="sxs-lookup"><span data-stu-id="15fe8-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="15fe8-114">La società A deve avere un numero sufficiente di licenze di Azure AD Premium che supportano l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="15fe8-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="15fe8-115">utente Hello dalla società B utilizza questa licenza dalla società A.</span><span class="sxs-lookup"><span data-stu-id="15fe8-115">hello user from company B consumes this license from company A.</span></span>

<span data-ttu-id="15fe8-116">tenancy invitando Hello è sempre responsabile per l'autenticazione a più fattori per gli utenti dell'organizzazione partner hello, anche se l'organizzazione partner hello dispone di funzionalità di autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="15fe8-116">hello inviting tenancy is always responsible for MFA for users from hello partner organization, even if hello partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="15fe8-117">Configurazione dell'autenticazione a più fattori per gli utenti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="15fe8-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="15fe8-118">toodiscover facilmente tooset di autenticazione a più fattori per gli utenti di collaborazione B2B, vedere vedere hello seguenti video:</span><span class="sxs-lookup"><span data-stu-id="15fe8-118">toodiscover how easy it is tooset up MFA for B2B collaboration users, see how in hello following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="15fe8-119">Esperienza di autenticazione a più fattori per gli utenti di B2B per il riscatto dell'offerta</span><span class="sxs-lookup"><span data-stu-id="15fe8-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="15fe8-120">Estrarre hello esperienza riscatto di animazione toosee hello seguente:</span><span class="sxs-lookup"><span data-stu-id="15fe8-120">Check out hello following animation toosee hello redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="15fe8-121">Reimpostazione dell'autenticazione a più fattori per gli utenti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="15fe8-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="15fe8-122">Attualmente, salve può richiedere tooproof agli utenti di collaborazione B2B di nuovo solo usando hello i cmdlet di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="15fe8-122">Currently, hello admin can require B2B collaboration users tooproof up again only by using hello following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="15fe8-123">Connettersi AD tooAzure</span><span class="sxs-lookup"><span data-stu-id="15fe8-123">Connect tooAzure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="15fe8-124">Ottenere tutti gli utenti con metodi di identificazione</span><span class="sxs-lookup"><span data-stu-id="15fe8-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="15fe8-125">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="15fe8-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="15fe8-126">Ripristinare nuovamente il metodo di autenticazione a più fattori hello per un utente specifico toorequire hello B2B collaborazione utente tooset prova i metodi.</span><span class="sxs-lookup"><span data-stu-id="15fe8-126">Reset hello MFA method for a specific user toorequire hello B2B collaboration user tooset proof-up methods again.</span></span> <span data-ttu-id="15fe8-127">Esempio:</span><span class="sxs-lookup"><span data-stu-id="15fe8-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a><span data-ttu-id="15fe8-128">Perché eseguire autenticazione a più fattori in tenancy risorse hello?</span><span class="sxs-lookup"><span data-stu-id="15fe8-128">Why do we perform MFA at hello resource tenancy?</span></span>

<span data-ttu-id="15fe8-129">Nella versione corrente di hello, autenticazione a più fattori è sempre tenancy risorse hello, per motivi di prevedibilità.</span><span class="sxs-lookup"><span data-stu-id="15fe8-129">In hello current release, MFA is always in hello resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="15fe8-130">Si supponga, ad esempio, un utente di Contoso (Sally) è invitato tooFabrikam e Fabrikam è abilitata l'autenticazione a più fattori per gli utenti B2B.</span><span class="sxs-lookup"><span data-stu-id="15fe8-130">For example, let’s say a Contoso user (Sally) is invited tooFabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="15fe8-131">Se Contoso dispone di criteri di autenticazione a più fattori abilitato per App1, ma non App2, quindi se si esamina hello attestazione Contoso MFA nel token hello, è possibile visualizzare hello problema seguente:</span><span class="sxs-lookup"><span data-stu-id="15fe8-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at hello Contoso MFA claim in hello token, we might see hello following issue:</span></span>

* <span data-ttu-id="15fe8-132">Giorno 1: un utente con autenticazione a più fattori in Contoso accede ad App1 e non viene quindi visualizzata una richiesta MFA aggiuntiva in Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="15fe8-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="15fe8-133">Il giorno 2: utente hello ha avuto accesso alle App 2 in Contoso, a questo punto quando si accede a Fabrikam, deve registrare per l'autenticazione a più fattori non esiste.</span><span class="sxs-lookup"><span data-stu-id="15fe8-133">Day 2: hello user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="15fe8-134">Questo processo può generare confusione e provocare toodrop in completamenti di accesso.</span><span class="sxs-lookup"><span data-stu-id="15fe8-134">This process can be confusing and could lead toodrop in sign-in completions.</span></span>

<span data-ttu-id="15fe8-135">Inoltre, anche se Contoso dispone di funzionalità di autenticazione a più fattori, non è sempre hello case hello Fabrikam sarebbe attendibili hello criteri Contoso MFA.</span><span class="sxs-lookup"><span data-stu-id="15fe8-135">Moreover, even if Contoso has MFA capability, it is not always hello case hello Fabrikam would trust hello Contoso MFA policy.</span></span>

<span data-ttu-id="15fe8-136">Infine, l'autenticazione a più fattori del tenant delle risorse funziona anche per account del servizio gestito, ID per social network e organizzazioni partner che non hanno configurato l'autenticazione a più fattori.</span><span class="sxs-lookup"><span data-stu-id="15fe8-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="15fe8-137">Pertanto, hello per l'autenticazione a più fattori per gli utenti B2B si consiglia di tooalways richiedono l'autenticazione a più fattori in hello si invitano tenant.</span><span class="sxs-lookup"><span data-stu-id="15fe8-137">Therefore, hello recommendation for MFA for B2B users is tooalways require MFA in hello inviting tenant.</span></span> <span data-ttu-id="15fe8-138">Questo requisito può causare toodouble autenticazione a più fattori in alcuni casi, ma ogni volta che accedono tenant invitando hello, l'esperienza degli utenti finali di hello è stimabile: Sally deve registrare per l'autenticazione a più fattori con tenant invitando hello.</span><span class="sxs-lookup"><span data-stu-id="15fe8-138">This requirement could lead toodouble MFA in some cases, but whenever accessing hello inviting tenant, hello end-users experience is predictable: Sally must register for MFA with hello inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="15fe8-139">Accesso condizionale basato sul dispositivo, sulla posizione e sui rischi per gli utenti B2B</span><span class="sxs-lookup"><span data-stu-id="15fe8-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="15fe8-140">Quando Contoso Abilita criteri di accesso condizionale basato su dispositivo per i dati aziendali, i dispositivi non gestiti da Contoso e non conformi ai criteri di dispositivi Contoso hello viene impedito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="15fe8-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with hello Contoso device policies.</span></span>

<span data-ttu-id="15fe8-141">Se il dispositivo dell'utente hello B2B non è gestito da Contoso, accesso di utenti B2B da organizzazioni partner hello è bloccato in qualsiasi contesto di questi criteri vengono applicati.</span><span class="sxs-lookup"><span data-stu-id="15fe8-141">If hello B2B user’s device isn't managed by Contoso, access of B2B users from hello partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="15fe8-142">Tuttavia, Contoso è possibile creare elenchi contenenti tooexclude gli utenti partner specifico da hello criteri di accesso condizionale basato su dispositivi di esclusione.</span><span class="sxs-lookup"><span data-stu-id="15fe8-142">However, Contoso can create exclusion lists containing specific partner users tooexclude them from hello device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="15fe8-143">Accesso condizionale basato sulla posizione per B2B</span><span class="sxs-lookup"><span data-stu-id="15fe8-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="15fe8-144">Se l'organizzazione di invitare hello è in grado di toocreate un intervallo di indirizzi IP attendibile che definisce le organizzazioni partner, i criteri di accesso condizionale in base alla posizione possono essere applicati per gli utenti B2B.</span><span class="sxs-lookup"><span data-stu-id="15fe8-144">Location-based conditional access policies can be enforced for B2B users if hello inviting organization is able toocreate a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="15fe8-145">Accesso condizionale basato sui rischi per B2B</span><span class="sxs-lookup"><span data-stu-id="15fe8-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="15fe8-146">Attualmente, criteri basati sul rischio di accesso non possono essere applicato tooB2B utenti perché viene eseguita la valutazione dei rischi hello organizzazione principale dell'utente hello B2B.</span><span class="sxs-lookup"><span data-stu-id="15fe8-146">Currently, risk-based sign-in policies cannot be applied tooB2B users because hello risk evaluation is performed at hello B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15fe8-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="15fe8-147">Next steps</span></span>

<span data-ttu-id="15fe8-148">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="15fe8-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="15fe8-149">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="15fe8-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="15fe8-150">Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori</span><span class="sxs-lookup"><span data-stu-id="15fe8-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="15fe8-151">Procedura per aggiungere utenti di Collaborazione B2B da parte di Information Worker</span><span class="sxs-lookup"><span data-stu-id="15fe8-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="15fe8-152">elementi Hello di posta elettronica di invito collaborazione B2B di hello</span><span class="sxs-lookup"><span data-stu-id="15fe8-152">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="15fe8-153">Riscatto dell'invito di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="15fe8-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="15fe8-154">Licenze per la Collaborazione B2B di Azure AD</span><span class="sxs-lookup"><span data-stu-id="15fe8-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="15fe8-155">Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15fe8-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="15fe8-156">Domande frequenti su Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15fe8-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="15fe8-157">API e personalizzazione per Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15fe8-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="15fe8-158">Aggiungere gli utenti per la Collaborazione B2B senza un invito</span><span class="sxs-lookup"><span data-stu-id="15fe8-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="15fe8-159">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15fe8-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
