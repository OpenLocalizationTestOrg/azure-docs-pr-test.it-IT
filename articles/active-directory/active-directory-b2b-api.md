---
title: aaaAzure attivo B2B Directory API di collaborazione e la personalizzazione | Documenti Microsoft
description: "Collaborazione B2B di Active Directory di Azure supporta le relazioni tra società consentendo a partner commerciali tooselectively l'accesso alle applicazioni aziendali"
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="69678-103">API e personalizzazione per Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69678-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="69678-104">Molti clienti abbiamo prodotto segnalare che desiderano toocustomize processo di invito hello in modo ottimale per le organizzazioni.</span><span class="sxs-lookup"><span data-stu-id="69678-104">We've had many customers tell us that they want toocustomize hello invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="69678-105">Con l'API, è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="69678-105">With our API, you can do just that.</span></span> [<span data-ttu-id="69678-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span><span class="sxs-lookup"><span data-stu-id="69678-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a><span data-ttu-id="69678-107">Funzionalità di invito hello API</span><span class="sxs-lookup"><span data-stu-id="69678-107">Capabilities of hello invitation API</span></span>
<span data-ttu-id="69678-108">Hello API offre hello seguenti funzionalità:</span><span class="sxs-lookup"><span data-stu-id="69678-108">hello API offers hello following capabilities:</span></span>

1. <span data-ttu-id="69678-109">Invitare un utente esterno con *qualsiasi* indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="69678-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="69678-110">Personalizzare in cui si desidera il tooland utenti dopo che accettino le invito.</span><span class="sxs-lookup"><span data-stu-id="69678-110">Customize where you want your users tooland after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="69678-111">Scegliere posta elettronica di invito standard hello toosend tramite us</span><span class="sxs-lookup"><span data-stu-id="69678-111">Choose toosend hello standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="69678-112">con un destinatario che è possibile personalizzare toohello</span><span class="sxs-lookup"><span data-stu-id="69678-112">with a message toohello recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="69678-113">Scegliere toocc: i partecipanti tookeep in hello ciclo su questo collaboratore l'invito.</span><span class="sxs-lookup"><span data-stu-id="69678-113">And choose toocc: people you want tookeep in hello loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="69678-114">O personalizzare completamente l'invito e flusso di lavoro caricamento scegliendo non toosend notifiche tramite Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69678-114">Or completely customize your invitation and onboarding workflow by choosing not toosend notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="69678-115">In questo caso, verrà restituito un URL di rimborso da hello API che è possibile incorporare in un modello di posta elettronica, messaggi immediati o altro metodo di distribuzione di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="69678-115">In this case, you get back a redemption URL from hello API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="69678-116">Infine, se si è un amministratore, è possibile scegliere utente hello tooinvite come membro.</span><span class="sxs-lookup"><span data-stu-id="69678-116">Finally, if you are an admin, you can choose tooinvite hello user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="69678-117">Modello di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="69678-117">Authorization model</span></span>
<span data-ttu-id="69678-118">Hello API può essere eseguito in hello seguenti modalità di autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="69678-118">hello API can be run in hello following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="69678-119">Modalità app + utente</span><span class="sxs-lookup"><span data-stu-id="69678-119">App + User mode</span></span>
<span data-ttu-id="69678-120">In questo modo, quando ci si accinge utilizza hello API esigenze toohave hello autorizzazioni toobe creare inviti B2B.</span><span class="sxs-lookup"><span data-stu-id="69678-120">In this mode, whoever is using hello API needs toohave hello permissions toobe create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="69678-121">Modalità solo app</span><span class="sxs-lookup"><span data-stu-id="69678-121">App only mode</span></span>
<span data-ttu-id="69678-122">Nel contesto solo app, app hello deve hello User.ReadWrite.All o Directory.ReadWrite.All ambiti per toosucceed invito hello.</span><span class="sxs-lookup"><span data-stu-id="69678-122">In app only context, hello app needs hello User.ReadWrite.All or Directory.ReadWrite.All scopes for hello invitation toosucceed.</span></span>

<span data-ttu-id="69678-123">Per altre informazioni, vedere https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="69678-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="69678-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69678-124">PowerShell</span></span>
<span data-ttu-id="69678-125">È ora possibile toouse PowerShell tooadd e invita gli utenti esterni tooan organizzazione facilmente.</span><span class="sxs-lookup"><span data-stu-id="69678-125">It is now possible toouse PowerShell tooadd and invite external users tooan organization easily.</span></span> <span data-ttu-id="69678-126">Creare un invito tramite i cmdlet di hello:</span><span class="sxs-lookup"><span data-stu-id="69678-126">Create an invitation using hello cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="69678-127">È possibile utilizzare hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="69678-127">You can use hello following options:</span></span>

* <span data-ttu-id="69678-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="69678-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="69678-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="69678-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="69678-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="69678-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="69678-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="69678-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="69678-132">È inoltre possibile estrarre riferimento invito API hello in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="69678-132">You can also check out hello invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="69678-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="69678-133">Next steps</span></span>

<span data-ttu-id="69678-134">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="69678-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="69678-135">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="69678-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="69678-136">Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori</span><span class="sxs-lookup"><span data-stu-id="69678-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="69678-137">Procedura per aggiungere utenti di Collaborazione B2B da parte di Information Worker</span><span class="sxs-lookup"><span data-stu-id="69678-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="69678-138">elementi Hello di posta elettronica di invito collaborazione B2B di hello</span><span class="sxs-lookup"><span data-stu-id="69678-138">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="69678-139">Riscatto dell'invito di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="69678-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="69678-140">Licenze per la Collaborazione B2B di Azure AD</span><span class="sxs-lookup"><span data-stu-id="69678-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="69678-141">Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69678-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="69678-142">Domande frequenti su Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69678-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="69678-143">Autenticazione a più fattori per utenti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="69678-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="69678-144">Aggiungere gli utenti per la Collaborazione B2B senza un invito</span><span class="sxs-lookup"><span data-stu-id="69678-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="69678-145">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69678-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
