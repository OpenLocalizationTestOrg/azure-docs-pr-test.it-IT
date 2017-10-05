---
title: Problemi riscontrati con il portale App personali in Azure Active Directory | Microsoft Docs
description: "Vengono fornite le istruzioni per eseguire le attività comuni quando si lavora nell'Access Panel (Riquadro di accesso)."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: c67cd675-b567-41e1-8bc2-e06fe0b38d3b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: japere
ms.openlocfilehash: 613c68d5c13793a3b696b6afbfc0e1a31595e201
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="do-you-need-help-with-the-my-apps-portal"></a><span data-ttu-id="ba520-103">Problemi riscontrati con il portale App personali</span><span class="sxs-lookup"><span data-stu-id="ba520-103">Do you need help with the My Apps portal?</span></span>

<span data-ttu-id="ba520-104">Questa pagina viene in genere visualizzata quando si verifica un problema durante l'uso del portale App personali.</span><span class="sxs-lookup"><span data-stu-id="ba520-104">You have probably reached this page because you were unfortunately running into an issue when using the My Apps portal.</span></span> <span data-ttu-id="ba520-105">In alcuni casi il problema richiede l'intervento del supporto tecnico o dell'amministratore, ma in altri casi può essere utile vedere prima uno dei seguenti argomenti di risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="ba520-105">While there are cases that require you to contact helpdesk or your administrator to get a problem solved, here are some troubleshooting topics that might be able to help, first.</span></span>

## <a name="i-am-having-trouble-signing-into-the-my-apps-portal"></a><span data-ttu-id="ba520-106">Si è verificato un problema durante l'accesso al portale App personali</span><span class="sxs-lookup"><span data-stu-id="ba520-106">I am having trouble signing into the My Apps portal</span></span>

<span data-ttu-id="ba520-107">Problemi generali da verificare:</span><span class="sxs-lookup"><span data-stu-id="ba520-107">General issues to check:</span></span>

- <span data-ttu-id="ba520-108">Verificare di accedere all'URL corretto: [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="ba520-108">Check to see if you are signing into the correct URL: [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>

- <span data-ttu-id="ba520-109">Provare ad aggiungere l'URL ai siti attendibili del browser.</span><span class="sxs-lookup"><span data-stu-id="ba520-109">Try adding the URL to your browser’s trusted sites.</span></span>

- <span data-ttu-id="ba520-110">Verificare che la password non sia scaduta o non sia stata dimenticata.</span><span class="sxs-lookup"><span data-stu-id="ba520-110">Make sure your password is not expired or forgotten.</span></span> <span data-ttu-id="ba520-111">Vedere [qui](active-directory-passwords-update-your-own-password.md) informazioni dettagliate per l'aggiornamento della password.</span><span class="sxs-lookup"><span data-stu-id="ba520-111">Check [here](active-directory-passwords-update-your-own-password.md) for more details on how to update your password.</span></span>

- <span data-ttu-id="ba520-112">Verificare che le informazioni di contatto per l'autenticazione siano aggiornate e non impediscano l'accesso.</span><span class="sxs-lookup"><span data-stu-id="ba520-112">Check to see if your authentication contact info is up to date and not blocking your access.</span></span> <span data-ttu-id="ba520-113">Vedere [qui](https://docs.microsoft.com/en-us/azure/multi-factor-authentication/end-user/multi-factor-authentication-end-user) altri dettagli per l'impostazione delle informazioni di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ba520-113">Check [here](https://docs.microsoft.com/en-us/azure/multi-factor-authentication/end-user/multi-factor-authentication-end-user) for more details on setting up your authentication info.</span></span>

- <span data-ttu-id="ba520-114">Cancellare i cookie del browser e riprovare ad accedere.</span><span class="sxs-lookup"><span data-stu-id="ba520-114">Try clearing your browser’s cookies, and then try to sign in again.</span></span>

<span data-ttu-id="ba520-115">Se i problemi persistono e non consentono l'accesso, rivolgersi all'amministratore per ulteriore assistenza.</span><span class="sxs-lookup"><span data-stu-id="ba520-115">If you are still encountering issues while trying to sign in, please contact your administrator for further help.</span></span>


## <a name="how-do-i-update-my-password"></a><span data-ttu-id="ba520-116">Come aggiornare la password</span><span class="sxs-lookup"><span data-stu-id="ba520-116">How do I update my password?</span></span>

<span data-ttu-id="ba520-117">Se si dimentica la password, la si vuole modificare, il personale IT non l'ha mai inviata oppure se l'account è stato bloccato, vedere [Help, I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md) (Password di Azure AD dimenticata).</span><span class="sxs-lookup"><span data-stu-id="ba520-117">If you forgot your password, never received one from your IT staff, been locked out of your account, or want to change it, see [Help, I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md) for more details.</span></span>

## <a name="how-do-i-register-for-password-reset"></a><span data-ttu-id="ba520-118">Come registrarsi per la reimpostazione della password</span><span class="sxs-lookup"><span data-stu-id="ba520-118">How do I register for password reset?</span></span>

<span data-ttu-id="ba520-119">Come utente finale, è possibile reimpostare la password o sbloccare l'account senza la necessità di rivolgersi a un'altra persona usando la funzionalità di reimpostazione della password self-service (SSPR).</span><span class="sxs-lookup"><span data-stu-id="ba520-119">As an end user, you can reset your password or unlock your account without having to speak to a person using self-service password reset (SSPR).</span></span> <span data-ttu-id="ba520-120">Per poter usare questa funzionalità, è prima necessario registrare i metodi di autenticazione o confermare i metodi di autenticazione predefiniti inseriti dall'amministratore.</span><span class="sxs-lookup"><span data-stu-id="ba520-120">Before you can use this functionality, you have to register authentication methods or confirm the predefined authentication methods your administrator has populated.</span></span> <span data-ttu-id="ba520-121">Per altre informazioni, vedere [Eseguire la registrazione per la reimpostazione password self-service](active-directory-passwords-reset-register.md).</span><span class="sxs-lookup"><span data-stu-id="ba520-121">For more details, see [Register for self-service password reset](active-directory-passwords-reset-register.md).</span></span>


## <a name="i-am-having-trouble-installing-the-my-apps-portal-browser-extension"></a><span data-ttu-id="ba520-122">Si riscontrano problemi con l'installazione dell'estensione browser per il portale App personali</span><span class="sxs-lookup"><span data-stu-id="ba520-122">I am having trouble installing the My Apps portal browser extension</span></span>

<span data-ttu-id="ba520-123">Verificare se i requisiti del browser sono soddisfatti:</span><span class="sxs-lookup"><span data-stu-id="ba520-123">Check to see if you are meeting browser requirements:</span></span>

- <span data-ttu-id="ba520-124">Per il portale è necessario un browser che supporti JavaScript e in cui sia abilitato CSS.</span><span class="sxs-lookup"><span data-stu-id="ba520-124">The portal requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="ba520-125">Se si usano app con accesso Single Sign-On basato su password è necessario installare anche l'estensione corrispondente.</span><span class="sxs-lookup"><span data-stu-id="ba520-125">If you are using password-based single sign-on apps, the accompanying extension must be installed as well.</span></span> <span data-ttu-id="ba520-126">L'estensione viene scaricata automaticamente quando si avvia un'applicazione configurata per le app con accesso Single Sign-On basato su password.</span><span class="sxs-lookup"><span data-stu-id="ba520-126">This extension is downloaded automatically when you launch an application that is configured for password-based single sign-on apps.</span></span>

- <span data-ttu-id="ba520-127">I requisiti del browser per l'estensione sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="ba520-127">The browser requirements for the extension are:</span></span>
    - <span data-ttu-id="ba520-128">Internet Explorer 8, 9, 10, 11 su Windows 7 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="ba520-128">Internet Explorer 8, 9, 10, 11 on Windows 7 or later</span></span>
    - <span data-ttu-id="ba520-129">Edge su Windows 10 Anniversary Edition o versioni successive</span><span class="sxs-lookup"><span data-stu-id="ba520-129">Edge on Windows 10 Anniversary Edition or later</span></span>
    - <span data-ttu-id="ba520-130">Chrome in Windows 7 o versione successiva e in MacOS X o versione successiva</span><span class="sxs-lookup"><span data-stu-id="ba520-130">Chrome on Windows 7 or later, and on MacOS X or later</span></span>
    - <span data-ttu-id="ba520-131">Firefox 26.0 o versione successiva in Windows XP SP2 o versione successiva e in Mac OS X 10.6 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="ba520-131">Firefox 26.0 or later on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

<span data-ttu-id="ba520-132">È anche possibile scaricare l'estensione per Chrome ed Edge dai collegamenti diretti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ba520-132">You can also download the extension for Chrome and Edge from the direct links below:</span></span>

- [<span data-ttu-id="ba520-133">Estensione per Chrome</span><span class="sxs-lookup"><span data-stu-id="ba520-133">Chrome Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

- [<span data-ttu-id="ba520-134">Estensione per Edge</span><span class="sxs-lookup"><span data-stu-id="ba520-134">Edge Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

<span data-ttu-id="ba520-135">Se dopo l'installazione si riscontrano problemi, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ba520-135">After installation try the following steps if you are encountering issues:</span></span>

- <span data-ttu-id="ba520-136">Verificare che l'estensione sia abilitata nelle impostazioni delle estensioni del browser.</span><span class="sxs-lookup"><span data-stu-id="ba520-136">Check to in your browser extension settings that the extension is enabled.</span></span>

- <span data-ttu-id="ba520-137">Riavviare il browser e accedere al portale App personali.</span><span class="sxs-lookup"><span data-stu-id="ba520-137">Restart your browser and sign in to the My Apps portal.</span></span>

- <span data-ttu-id="ba520-138">Cancellare i cookie del browser e accedere al portale App personali.</span><span class="sxs-lookup"><span data-stu-id="ba520-138">Clear your browser’s cookies and sign in to the My Apps portal.</span></span>

## <a name="how-do-i-add-a-new-app"></a><span data-ttu-id="ba520-139">Come aggiungere una nuova app</span><span class="sxs-lookup"><span data-stu-id="ba520-139">How do I add a new app?</span></span>

1.  <span data-ttu-id="ba520-140">Nella pagina **App** fare clic su **Aggiungi app**.</span><span class="sxs-lookup"><span data-stu-id="ba520-140">On the **Apps** page, click **Add App**.</span></span>

2.  <span data-ttu-id="ba520-141">Cercare l'applicazione da aggiungere e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ba520-141">Search the app you want to add, and then click **Add**.</span></span>

<span data-ttu-id="ba520-142">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="ba520-142">**Remarks:**</span></span>

- <span data-ttu-id="ba520-143">Si ha accesso a questa opzione solo se è stata abilitata dall'amministratore per l'account.</span><span class="sxs-lookup"><span data-stu-id="ba520-143">You only have access to this option if your admin has enabled this for your account.</span></span>

- <span data-ttu-id="ba520-144">Se l'applicazione richiede l'autorizzazione può essere necessario attendere l'approvazione dell'amministratore.</span><span class="sxs-lookup"><span data-stu-id="ba520-144">If the app requires permission, you may need to wait for admin approval.</span></span>


## <a name="how-do-i-manage-my-group-memberships"></a><span data-ttu-id="ba520-145">Come gestire l'appartenenza ai gruppi</span><span class="sxs-lookup"><span data-stu-id="ba520-145">How do I manage my group memberships?</span></span>

1. <span data-ttu-id="ba520-146">Fare clic nel riquadro delle app Gruppi.</span><span class="sxs-lookup"><span data-stu-id="ba520-146">Click the Groups app tile.</span></span> 
2. <span data-ttu-id="ba520-147">Per creare un gruppo, in Gruppi di cui si è proprietari fare clic su Crea gruppo, quindi seguire le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="ba520-147">To create a group, under Groups I own, click Create group, and then follow the instructions.</span></span>
3. <span data-ttu-id="ba520-148">Per partecipare a un gruppo, in Gruppi a cui si appartiene fare clic su Partecipa a gruppo, quindi seguire le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="ba520-148">To join a group, under Groups I'm in, click Join group, and then follow the instructions.</span></span>

<span data-ttu-id="ba520-149">**Osservazioni:**</span><span class="sxs-lookup"><span data-stu-id="ba520-149">**Remarks:**</span></span>

- <span data-ttu-id="ba520-150">Si ha accesso a questa opzione solo se è stata abilitata dall'amministratore per l'account.</span><span class="sxs-lookup"><span data-stu-id="ba520-150">You only have access to this option if your admin has enabled this for your account.</span></span>

- <span data-ttu-id="ba520-151">Nei gruppi di appartenenza è possibile visualizzare i dettagli o abbandonare il gruppo.</span><span class="sxs-lookup"><span data-stu-id="ba520-151">Groups you are a member of allow you to view details and leave the group.</span></span>

- <span data-ttu-id="ba520-152">Nei gruppi di cui si proprietari è possibile visualizzare i dettagli, aggiungere o rimuovere membri e abbandonare il gruppo.</span><span class="sxs-lookup"><span data-stu-id="ba520-152">Groups you are an owner of allows you to view details, add or remove members, and leave the group.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ba520-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ba520-153">Next steps</span></span>

<span data-ttu-id="ba520-154">Per informazioni correlate alla risoluzione dei problemi, vedere [Problemi relativi all'uso del sito Web o dell'applicazione per dispositivi mobili del pannello di accesso dell'applicazione](active-directory-application-access-panel-content-map.md)</span><span class="sxs-lookup"><span data-stu-id="ba520-154">For troubleshooting related information, see [Problems using the application access panel website or mobile application](active-directory-application-access-panel-content-map.md)</span></span>

