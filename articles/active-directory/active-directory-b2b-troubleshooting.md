---
title: collaborazione B2B di Azure Active Directory aaaTroubleshooting | Documenti Microsoft
description: Informazioni su come risolvere i problemi comuni di Collaborazione B2B di Azure Active Directory
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="f737e-103">Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f737e-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="f737e-104">Questo articolo illustra come risolvere i problemi comuni di Collaborazione B2B di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f737e-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a><span data-ttu-id="f737e-105">È stato aggiunto un utente esterno, ma non vengano visualizzati nella Rubrica globale o in selezione utenti hello</span><span class="sxs-lookup"><span data-stu-id="f737e-105">I’ve added an external user but do not see them in my Global Address Book or in hello people picker</span></span>

<span data-ttu-id="f737e-106">In casi in cui gli utenti esterni non vengono popolati nell'elenco di hello, oggetto hello potrebbe richiedere alcuni minuti tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="f737e-106">In cases where external users are not populated in hello list, hello object might take a few minutes tooreplicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="f737e-107">Un utente guest B2B non compare nella selezione utenti di SharePoint Online/OneDrive</span><span class="sxs-lookup"><span data-stu-id="f737e-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="f737e-108">Hello toosearch di possibilità per gli utenti guest esistenti nella selezione di utenti di SharePoint Online (Simulato) hello è disattivato per il comportamento legacy toomatch predefinito.</span><span class="sxs-lookup"><span data-stu-id="f737e-108">hello ability toosearch for existing guest users in hello SharePoint Online (SPO) people picker is OFF by default toomatch legacy behavior.</span></span>

<span data-ttu-id="f737e-109">È possibile abilitare questa funzionalità tramite l'impostazione di 'ShowPeoplePickerSuggestionsForGuestUsers' in hello tenant e una raccolta siti livello hello.</span><span class="sxs-lookup"><span data-stu-id="f737e-109">You can enable this feature by using hello setting 'ShowPeoplePickerSuggestionsForGuestUsers' at hello tenant and site collection level.</span></span> <span data-ttu-id="f737e-110">È possibile impostare funzionalità hello usano hello SPOTenant di Set e Set-SPOSite cmdlet, che consente ai membri toosearch tutti gli utenti guest esistenti nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="f737e-110">You can set hello feature using hello Set-SPOTenant and Set-SPOSite cmdlets, which allow members toosearch all existing guest users in hello directory.</span></span> <span data-ttu-id="f737e-111">Le modifiche apportate nell'ambito del tenant hello non influiscono sui siti Simulato già sottoposto a provisioning.</span><span class="sxs-lookup"><span data-stu-id="f737e-111">Changes in hello tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="f737e-112">Gli inviti sono stati disabilitati per la directory</span><span class="sxs-lookup"><span data-stu-id="f737e-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="f737e-113">Se si riceve una notifica che non dispongono di autorizzazioni tooinvite utenti, verificare che l'account utente sia autorizzato tooinvite utenti esterni in impostazioni utente:</span><span class="sxs-lookup"><span data-stu-id="f737e-113">If you are notified that you do not have permissions tooinvite users, verify that your user account is authorized tooinvite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="f737e-114">Se recentemente sono state modificate le impostazioni o assegnato hello mittente dell'invito Guest ruolo tooa utente, potrebbe essere presente un ritardo di 15-60 minuti affinché hello modifiche abbiano effetto.</span><span class="sxs-lookup"><span data-stu-id="f737e-114">If you have recently modified these settings or assigned hello Guest Inviter role tooa user, there might be a 15-60 minute delay before hello changes take effect.</span></span>

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="f737e-115">utente Hello invitati, riceve un errore durante il riscatto</span><span class="sxs-lookup"><span data-stu-id="f737e-115">hello user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="f737e-116">Di seguito sono riportati gli errori più comuni.</span><span class="sxs-lookup"><span data-stu-id="f737e-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="f737e-117">L'amministratore dell'invitato non consente la creazione di utenti EmailVerified nel tenant</span><span class="sxs-lookup"><span data-stu-id="f737e-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="f737e-118">Quando si invitano gli utenti il cui organizzazione utilizza Azure Active Directory, ma in cui hello specifico account utente non esiste (ad esempio, hello utente non esiste in Azure Active Directory contoso.com).</span><span class="sxs-lookup"><span data-stu-id="f737e-118">When inviting users whose organization is using Azure Active Directory, but where hello specific user’s account does not exist (for example, hello user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="f737e-119">messaggio per l'amministratore di contoso.com può disporre di criteri sul posto impediscono agli utenti di creazione.</span><span class="sxs-lookup"><span data-stu-id="f737e-119">hello administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="f737e-120">utente di Hello deve controllare con loro toodetermine amministratore se gli utenti esterni sono consentiti.</span><span class="sxs-lookup"><span data-stu-id="f737e-120">hello user must check with their admin toodetermine if external users are allowed.</span></span> <span data-ttu-id="f737e-121">Hello amministratore dell'utente esterno potrebbe essere necessario tooallow verificato tramite posta elettronica agli utenti del proprio dominio (vedere questo [articolo](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) in modo che gli utenti verificati tramite posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="f737e-121">hello external user’s admin may need tooallow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="f737e-122">L'utente esterno non esiste già in un dominio federato</span><span class="sxs-lookup"><span data-stu-id="f737e-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="f737e-123">Se si utilizza l'autenticazione di federazione e hello utente non esiste già in Azure Active Directory, non può essere invitati utente hello.</span><span class="sxs-lookup"><span data-stu-id="f737e-123">If you are using federation authentication and hello user does not already exist in Azure Active Directory, hello user cannot be invited.</span></span>

<span data-ttu-id="f737e-124">Questo problema, hello tooresolve amministratore dell'utente esterno deve sincronizzare tooAzure account dell'utente hello Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f737e-124">tooresolve this issue, hello external user’s admin must synchronize hello user’s account tooAzure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="f737e-125">In che modo "\#", che in genere è un carattere non valido, viene sincronizzato con Azure AD?</span><span class="sxs-lookup"><span data-stu-id="f737e-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="f737e-126">"\#" è un carattere riservato in UPN per collaborazione B2B di Azure Active Directory o utenti esterni, perché hello invitato account user@contoso.com diventa user_contoso.com#EXT@fabrikam.onmicrosoft.com. Pertanto, \# in UPN provenienti da locali non sono consentiti toosign in toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f737e-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because hello invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com. Therefore, \# in UPNs coming from on-premises aren't allowed toosign in toohello Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a><span data-ttu-id="f737e-127">Viene visualizzato un errore durante l'aggiunta di utenti esterni tooa sincronizzazione gruppo</span><span class="sxs-lookup"><span data-stu-id="f737e-127">I receive an error when adding external users tooa synchronized group</span></span>

<span data-ttu-id="f737e-128">Gli utenti esterni possono essere aggiunte solo troppo "assegnato" o i gruppi "Sicurezza" e non toogroups che vengono controllati in locale.</span><span class="sxs-lookup"><span data-stu-id="f737e-128">External users can be added only too“assigned” or “Security” groups and not toogroups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a><span data-ttu-id="f737e-129">L'utente esterno non ha ricevuto un messaggio di posta elettronica tooredeem</span><span class="sxs-lookup"><span data-stu-id="f737e-129">My external user did not receive an email tooredeem</span></span>

<span data-ttu-id="f737e-130">l'invitato Hello deve verificare con i provider di servizi Internet o se è consentita tooensure filtro posta indesiderata che hello seguente indirizzo:Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="f737e-130">hello invitee should check with their ISP or spam filter tooensure that hello following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="f737e-131">Si nota che messaggio hello personalizzati non vengono incluso con i messaggi di invito in alcuni casi</span><span class="sxs-lookup"><span data-stu-id="f737e-131">I notice that hello custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="f737e-132">toocomply leggi in materia di privacy, le API non includono messaggi personalizzati nell'invito tramite posta elettronica hello quando:</span><span class="sxs-lookup"><span data-stu-id="f737e-132">toocomply with privacy laws, our APIs do not include custom messages in hello email invitation when:</span></span>

- <span data-ttu-id="f737e-133">mittente dell'invito Hello non dispone di un indirizzo di posta elettronica in hello si invitano tenant</span><span class="sxs-lookup"><span data-stu-id="f737e-133">hello inviter doesn’t have an email address in hello inviting tenant</span></span>
- <span data-ttu-id="f737e-134">Quando un'entità di servizio App Invia invito hello</span><span class="sxs-lookup"><span data-stu-id="f737e-134">When an appservice principal sends hello invitation</span></span>

<span data-ttu-id="f737e-135">Se questo scenario è tooyou importanti, è possibile eliminare l'account di posta elettronica di invito API e inviarlo tramite il meccanismo di posta elettronica hello di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="f737e-135">If this scenario is important tooyou, you can suppress our API invitation email, and send it through hello email mechanism of your choice.</span></span> <span data-ttu-id="f737e-136">Consultare toomake legale dell'organizzazione che qualsiasi messaggio di posta elettronica inviati in questo modo inoltre conforme allo standard leggi sulla privacy.</span><span class="sxs-lookup"><span data-stu-id="f737e-136">Consult your organization’s legal counsel toomake sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f737e-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f737e-137">Next steps</span></span>

<span data-ttu-id="f737e-138">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="f737e-138">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="f737e-139">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="f737e-139">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="f737e-140">Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori</span><span class="sxs-lookup"><span data-stu-id="f737e-140">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="f737e-141">Procedura per aggiungere utenti di Collaborazione B2B da parte di Information Worker</span><span class="sxs-lookup"><span data-stu-id="f737e-141">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="f737e-142">elementi Hello di posta elettronica di invito collaborazione B2B di hello</span><span class="sxs-lookup"><span data-stu-id="f737e-142">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="f737e-143">Riscatto dell'invito di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="f737e-143">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="f737e-144">Licenze per la Collaborazione B2B di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f737e-144">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="f737e-145">Domande frequenti su Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f737e-145">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="f737e-146">API e personalizzazione per Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f737e-146">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="f737e-147">Autenticazione a più fattori per utenti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="f737e-147">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="f737e-148">Aggiungere gli utenti per la Collaborazione B2B senza un invito</span><span class="sxs-lookup"><span data-stu-id="f737e-148">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="f737e-149">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f737e-149">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
