---
title: Elementi del messaggio di posta elettronica di invito per la collaborazione B2B di Azure Active Directory | Documentazione Microsoft
description: Modello di messaggio di posta elettronica di invito per la collaborazione B2B di Azure Active Directory
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 458a2cab13b7e83f120e0926a95d454070181dfb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="the-elements-of-the-b2b-collaboration-invitation-email"></a><span data-ttu-id="09668-103">Elementi del messaggio di posta elettronica di invito per la collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="09668-103">The elements of the B2B collaboration invitation email</span></span>

<span data-ttu-id="09668-104">I messaggi di posta elettronica di invito sono strumenti fondamentali per entrare in contatto con i partner e introdurli alla funzionalità di collaborazione B2B di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="09668-104">Invitation emails are a critical component to bring partners on board as B2B collaboration users in Azure AD.</span></span> <span data-ttu-id="09668-105">È possibile usarli per aumentare l'attendibilità del destinatario.</span><span class="sxs-lookup"><span data-stu-id="09668-105">You can use them to increase the recipient's trust.</span></span> <span data-ttu-id="09668-106">È possibile aggiungere elementi di legittimità e riprova sociale al messaggio di posta elettronica, per assicurarsi che il destinatario scelga di selezionare con tranquillità il pulsante **Get Started** (Inizia) per accettare l'invito.</span><span class="sxs-lookup"><span data-stu-id="09668-106">you can add legitimacy and social proof to the email, to make sure the recipient feels comfortable with selecting the **Get Started** button to accept the invitation.</span></span> <span data-ttu-id="09668-107">L'attendibilità è uno strumento fondamentale per ridurre i problemi di condivisione.</span><span class="sxs-lookup"><span data-stu-id="09668-107">This trust is a key means to reduce sharing friction.</span></span> <span data-ttu-id="09668-108">Il messaggio di posta elettronica deva anche avere un aspetto accattivante.</span><span class="sxs-lookup"><span data-stu-id="09668-108">And you also want to make the email look great!</span></span>

![Messaggio di posta elettronica di invito per la collaborazione B2B](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-the-email"></a><span data-ttu-id="09668-110">Descrizione del messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="09668-110">Explaining the email</span></span>
<span data-ttu-id="09668-111">Per sfruttare al meglio le potenzialità del messaggio di posta elettronica, di seguito ne vengono descritti alcuni elementi.</span><span class="sxs-lookup"><span data-stu-id="09668-111">Let's look at a few elements of the email so you know how best to use their capabilities.</span></span>

### <a name="subject"></a><span data-ttu-id="09668-112">Subject</span><span class="sxs-lookup"><span data-stu-id="09668-112">Subject</span></span>
<span data-ttu-id="09668-113">Il contenuto dell'oggetto del messaggio di posta elettronica è basato su questo modello: Ti invitiamo all'organizzazione &lt;nometenant&gt;</span><span class="sxs-lookup"><span data-stu-id="09668-113">The subject of the email follows the following pattern: You're invited to the &lt;tenantname&gt; organization</span></span>

### <a name="from-address"></a><span data-ttu-id="09668-114">Indirizzo del mittente.</span><span class="sxs-lookup"><span data-stu-id="09668-114">From address</span></span>
<span data-ttu-id="09668-115">Per l'indirizzo del mittente si userà un modello simile a quello LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="09668-115">We use a LinkedIn-like pattern for the From address.</span></span>  <span data-ttu-id="09668-116">È consigliabile chiarire chi è il mittente dell'invito e a quale azienda appartiene, oltre a mettere in evidenza che il messaggio proviene da un indirizzo di posta elettronica Microsoft.</span><span class="sxs-lookup"><span data-stu-id="09668-116">You should be clear who the inviter is and from which company, and also clarify that the email is coming from a Microsoft email address.</span></span> <span data-ttu-id="09668-117">Il formato è: &lt;nome visualizzato del mittente dell'invito&gt; da &lt;nometenant&gt; (tramite Microsoft)invites@microsoft.com&gt;</span><span class="sxs-lookup"><span data-stu-id="09668-117">The format is: &lt;Display name of inviter&gt; from &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;</span></span>

### <a name="reply-to"></a><span data-ttu-id="09668-118">Rispondi a</span><span class="sxs-lookup"><span data-stu-id="09668-118">Reply To</span></span>
<span data-ttu-id="09668-119">Se disponibile, viene impostato l'indirizzo di posta elettronica del mittente dell'invito. Un'eventuale risposta all'invito viene quindi inviata al mittente.</span><span class="sxs-lookup"><span data-stu-id="09668-119">The reply-to email is set to the inviter's email when available, so that replying to the email sends an email back to the inviter.</span></span>

### <a name="branding"></a><span data-ttu-id="09668-120">Personalizzazione</span><span class="sxs-lookup"><span data-stu-id="09668-120">Branding</span></span>
<span data-ttu-id="09668-121">Nei messaggi di posta elettronica di invito vengono usate le informazioni personalizzate distintive dell'azienda eventualmente impostate per il tenant.</span><span class="sxs-lookup"><span data-stu-id="09668-121">The invitation emails from your tenant use the company branding that you may have set up for your tenant.</span></span> <span data-ttu-id="09668-122">Se si vogliono sfruttare i vantaggi offerti da questa funzionalità, [qui](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) sono disponibili i dettagli su come configurarla.</span><span class="sxs-lookup"><span data-stu-id="09668-122">If you want to take advantage of this capability, [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) are the details on how to configure it.</span></span> <span data-ttu-id="09668-123">Il logo banner viene visualizzato nel messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="09668-123">The banner logo appears in the email.</span></span> <span data-ttu-id="09668-124">Per ottenere risultati ottimali, seguire le istruzioni relative a qualità e dimensioni dell'immagine, disponibili [qui](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="09668-124">Follow the image size and quality instructions [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) for best results.</span></span> <span data-ttu-id="09668-125">Il nome dell'azienda viene anche visualizzato nella chiamata all'azione.</span><span class="sxs-lookup"><span data-stu-id="09668-125">In addition, the company name also shows up in the call to action.</span></span>

### <a name="call-to-action"></a><span data-ttu-id="09668-126">Chiamata all'azione</span><span class="sxs-lookup"><span data-stu-id="09668-126">Call to action</span></span>
<span data-ttu-id="09668-127">La chiamata all'azione è costituita da due parti: la spiegazione del motivo per cui il destinatario ha ricevuto il messaggio e l'indicazione delle successive azioni richieste al destinatario.</span><span class="sxs-lookup"><span data-stu-id="09668-127">The call to action consists of two parts: explaining why the recipient has received the mail and what the recipient is being asked to do about it.</span></span>
- <span data-ttu-id="09668-128">La sezione relativa al "motivo" può essere basata sul seguente modello: Hai ricevuto l'invito per accedere alle applicazioni nell'organizzazione &lt;nometenant&gt;</span><span class="sxs-lookup"><span data-stu-id="09668-128">The "why" section can be addressed using the following pattern: You've been invited to access applications in the &lt;tenantname&gt; organization</span></span>

- <span data-ttu-id="09668-129">La sezione relativa alle "successive azioni richieste al destinatario" è indicata dalla presenza del pulsante **Get Started** (Inizia).</span><span class="sxs-lookup"><span data-stu-id="09668-129">And the "what you're being asked to do" section is indicated by the presence of the **Get Started** button.</span></span> <span data-ttu-id="09668-130">Se per aggiungere il destinatario non è stato necessario inviare inviti, questo pulsante non viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="09668-130">When the recipient has been added without the need for invitations, this button doesn't show up.</span></span>

### <a name="inviters-information"></a><span data-ttu-id="09668-131">Informazioni sul mittente dell'invito</span><span class="sxs-lookup"><span data-stu-id="09668-131">Inviter's information</span></span>
<span data-ttu-id="09668-132">Il nome visualizzato del mittente dell'invito è incluso nel messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="09668-132">The inviter's display name is included in the email.</span></span> <span data-ttu-id="09668-133">Nel messaggio di invito verrà inclusa anche l'immagine del profilo per l'account di Azure AD, qualora sia stata impostata.</span><span class="sxs-lookup"><span data-stu-id="09668-133">And in addition, if you've set up a profile picture for your Azure AD account, the inviting email will include that picture as well.</span></span> <span data-ttu-id="09668-134">Entrambi consentono di rendere il messaggio di posta elettronica più attendibile per il destinatario.</span><span class="sxs-lookup"><span data-stu-id="09668-134">Both are intended to increase your recipient's confidence in the email.</span></span>

<span data-ttu-id="09668-135">Se non è ancora stata impostata un'immagine del profilo, al posto dell'immagine viene visualizzata un'icona con le iniziali del mittente dell'invito:</span><span class="sxs-lookup"><span data-stu-id="09668-135">If you haven't yet set up your profile picture, an icon with the inviter's initials in place of the picture is shown:</span></span>

  ![visualizzazione iniziali del mittente dell'invito](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a><span data-ttu-id="09668-137">Corpo</span><span class="sxs-lookup"><span data-stu-id="09668-137">Body</span></span>
<span data-ttu-id="09668-138">Il corpo contiene il messaggio digitato dal mittente dell'invito oppure passato tramite l'API di invito.</span><span class="sxs-lookup"><span data-stu-id="09668-138">The body contains the message that the inviter composes or is passed through the invitation API.</span></span> <span data-ttu-id="09668-139">Si tratta di un'area di testo, che quindi non supporta l'elaborazione dei tag HTML per motivi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="09668-139">It is a text area, so it does not process HTML tags for security reasons.</span></span>

### <a name="footer-section"></a><span data-ttu-id="09668-140">Sezione piè di pagina</span><span class="sxs-lookup"><span data-stu-id="09668-140">Footer section</span></span>
<span data-ttu-id="09668-141">Il piè di pagina contiene il marchio aziendale di Microsoft e indica al destinatario se il messaggio di posta elettronica è stato inviato da un alias non monitorato.</span><span class="sxs-lookup"><span data-stu-id="09668-141">The footer contains the Microsoft company brand and lets the recipient know if the email was sent from an unmonitored alias.</span></span> <span data-ttu-id="09668-142">Casi speciali:</span><span class="sxs-lookup"><span data-stu-id="09668-142">Special cases:</span></span>

- <span data-ttu-id="09668-143">Il mittente dell'invito non dispone di un indirizzo di posta elettronica nella tenancy di invito</span><span class="sxs-lookup"><span data-stu-id="09668-143">The inviter doesn't have an email address in the inviting tenancy</span></span>

  ![l'immagine del profilo del mittente dell'invito non è associata a un indirizzo di posta elettronica nella tenancy di invito](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- <span data-ttu-id="09668-145">Il destinatario non deve riscattare l'invito</span><span class="sxs-lookup"><span data-stu-id="09668-145">The recipient doesn't need to redeem the invitation</span></span>

  ![caso in cui il destinatario non deve riscattare l'invito](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a><span data-ttu-id="09668-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="09668-147">Next steps</span></span>

<span data-ttu-id="09668-148">Vedere gli altri articoli su Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="09668-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="09668-149">Che cos'è la collaborazione B2B di Azure AD?</span><span class="sxs-lookup"><span data-stu-id="09668-149">What is Azure AD B2B collaboration</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="09668-150">Procedura per aggiungere utenti di Collaborazione B2B ad Azure Active Directory da parte degli amministratori</span><span class="sxs-lookup"><span data-stu-id="09668-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="09668-151">Procedura per aggiungere utenti di Collaborazione B2B da parte di Information Worker</span><span class="sxs-lookup"><span data-stu-id="09668-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="09668-152">Riscatto dell'invito di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="09668-152">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="09668-153">Licenze per la Collaborazione B2B di Azure AD</span><span class="sxs-lookup"><span data-stu-id="09668-153">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="09668-154">Risoluzione dei problemi di Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09668-154">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="09668-155">Domande frequenti su Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09668-155">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="09668-156">API e personalizzazione per Collaborazione B2B di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09668-156">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="09668-157">Autenticazione a più fattori per utenti di Collaborazione B2B</span><span class="sxs-lookup"><span data-stu-id="09668-157">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="09668-158">Aggiungere gli utenti per la Collaborazione B2B senza un invito</span><span class="sxs-lookup"><span data-stu-id="09668-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="09668-159">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09668-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
