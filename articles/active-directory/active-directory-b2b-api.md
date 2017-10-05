---
title: API e personalizzazione per Collaborazione B2B di Azure Active Directory | Microsoft Docs
description: "La collaborazione B2B di Azure Active Directory supporta le relazioni tra società abilitando i partner commerciali ad accedere in modo selettivo alle applicazioni aziendali"
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
ms.openlocfilehash: c85e05b38b4a9525e13ec510a17b7ef4841198d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="b58d9-103">API e personalizzazione per Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b58d9-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="b58d9-104">Molti clienti hanno manifestato il desiderio di poter personalizzare il processo di invito in modo più adatto alla propria organizzazione.</span><span class="sxs-lookup"><span data-stu-id="b58d9-104">We've had many customers tell us that they want to customize the invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="b58d9-105">Con l'API, è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="b58d9-105">With our API, you can do just that.</span></span> [<span data-ttu-id="b58d9-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span><span class="sxs-lookup"><span data-stu-id="b58d9-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-the-invitation-api"></a><span data-ttu-id="b58d9-107">Funzionalità dell'API di invito</span><span class="sxs-lookup"><span data-stu-id="b58d9-107">Capabilities of the invitation API</span></span>
<span data-ttu-id="b58d9-108">L'API offre le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="b58d9-108">The API offers the following capabilities:</span></span>

1. <span data-ttu-id="b58d9-109">Invitare un utente esterno con *qualsiasi* indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="b58d9-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="b58d9-110">Personalizzare la pagina di destinazione visualizzata dagli utenti dopo avere accettato l'invito.</span><span class="sxs-lookup"><span data-stu-id="b58d9-110">Customize where you want your users to land after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="b58d9-111">Scegliere di inviare il messaggio di invito standard tramite Microsoft</span><span class="sxs-lookup"><span data-stu-id="b58d9-111">Choose to send the standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="b58d9-112">con un messaggio personalizzabile per il destinatario</span><span class="sxs-lookup"><span data-stu-id="b58d9-112">with a message to the recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="b58d9-113">Scegliere di mettere in copia conoscenza le persone che si vuole mantenere nel ciclo relativo all'invito di questo collaboratore.</span><span class="sxs-lookup"><span data-stu-id="b58d9-113">And choose to cc: people you want to keep in the loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="b58d9-114">Personalizzare completamente l'invito e il flusso di lavoro di onboarding scegliendo di non inviare notifiche tramite Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b58d9-114">Or completely customize your invitation and onboarding workflow by choosing not to send notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="b58d9-115">In questo caso, si ottiene un URL di riscatto dall'API, che è possibile incorporare in un modello di messaggio di posta elettronica, in un messaggio istantaneo o in un altro metodo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b58d9-115">In this case, you get back a redemption URL from the API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="b58d9-116">Gli amministratori infine possono scegliere di invitare l'utente come membro.</span><span class="sxs-lookup"><span data-stu-id="b58d9-116">Finally, if you are an admin, you can choose to invite the user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="b58d9-117">Modello di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="b58d9-117">Authorization model</span></span>
<span data-ttu-id="b58d9-118">L'API può essere eseguita nelle modalità di autorizzazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="b58d9-118">The API can be run in the following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="b58d9-119">Modalità app + utente</span><span class="sxs-lookup"><span data-stu-id="b58d9-119">App + User mode</span></span>
<span data-ttu-id="b58d9-120">In questa modalità, chiunque usi l'API deve disporre delle autorizzazioni per creare gli inviti B2B.</span><span class="sxs-lookup"><span data-stu-id="b58d9-120">In this mode, whoever is using the API needs to have the permissions to be create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="b58d9-121">Modalità solo app</span><span class="sxs-lookup"><span data-stu-id="b58d9-121">App only mode</span></span>
<span data-ttu-id="b58d9-122">In un contesto solo app, per garantire l'esito positivo dell'invio è necessario che l'app disponga dell'ambito User.ReadWrite.All o Directory.ReadWrite.All.</span><span class="sxs-lookup"><span data-stu-id="b58d9-122">In app only context, the app needs the User.ReadWrite.All or Directory.ReadWrite.All scopes for the invitation to succeed.</span></span>

<span data-ttu-id="b58d9-123">Per altre informazioni, vedere https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="b58d9-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="b58d9-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b58d9-124">PowerShell</span></span>
<span data-ttu-id="b58d9-125">Ora è possibile usare PowerShell per aggiungere e invitare facilmente utenti esterni a un'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="b58d9-125">It is now possible to use PowerShell to add and invite external users to an organization easily.</span></span> <span data-ttu-id="b58d9-126">Creare un invito tramite il cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b58d9-126">Create an invitation using the cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="b58d9-127">È possibile usare le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b58d9-127">You can use the following options:</span></span>

* <span data-ttu-id="b58d9-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="b58d9-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="b58d9-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="b58d9-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="b58d9-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="b58d9-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="b58d9-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="b58d9-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="b58d9-132">È anche possibile controllare il riferimento all'API di invito in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="b58d9-132">You can also check out the invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b58d9-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b58d9-133">Next steps</span></span>

<span data-ttu-id="b58d9-134">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="b58d9-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="b58d9-135">Che cos'è Azure AD B2B Collaboration?</span><span class="sxs-lookup"><span data-stu-id="b58d9-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="b58d9-136">Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori</span><span class="sxs-lookup"><span data-stu-id="b58d9-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="b58d9-137">Procedura di aggiunta di utenti di Collaborazione B2B da parte di information worker</span><span class="sxs-lookup"><span data-stu-id="b58d9-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="b58d9-138">Elementi del messaggio di posta elettronica di invito per la Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="b58d9-138">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="b58d9-139">Riscatto dell'invito di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="b58d9-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="b58d9-140">Licenze per la Collaborazione B2B di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b58d9-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="b58d9-141">Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b58d9-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="b58d9-142">Domande frequenti su Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b58d9-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="b58d9-143">Autenticazione a più fattori per utenti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="b58d9-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="b58d9-144">Aggiungere gli utenti per la Collaborazione B2B senza un invito</span><span class="sxs-lookup"><span data-stu-id="b58d9-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="b58d9-145">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b58d9-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
