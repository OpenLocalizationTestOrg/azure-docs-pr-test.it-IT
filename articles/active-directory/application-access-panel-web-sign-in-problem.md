---
title: Problemi di accesso al sito Web del pannello di accesso | Microsoft Docs
description: Linee guida per risolvere i possibili problemi durante il tentativo di accedere per usare il pannello di accesso
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviwer: japere
ms.openlocfilehash: 28d91237adf745e591b02322de7881c8122827ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problem-signing-in-to-the-access-panel-website"></a><span data-ttu-id="983d6-103">Problemi di accesso al sito Web del pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="983d6-103">Problem signing in to the access panel website</span></span>

<span data-ttu-id="983d6-104">Il pannello di accesso è un portale basato sul Web che permette a un utente che ha un account aziendale o dell'istituto di istruzione in Azure Active Directory (Azure AD) di visualizzare e avviare applicazioni basate sul cloud a cui l'amministratore di Azure AD ha concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="983d6-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="983d6-105">Un utente dotato di edizioni di Azure AD può anche usare le funzionalità di gestione self-service di gruppi e app tramite il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="983d6-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="983d6-106">Il pannello di accesso è separato dal portale di Azure e non richiede una sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="983d6-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="983d6-107">Gli utenti possono accedere al pannello di accesso se hanno un account aziendale o dell'istituto di istruzione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="983d6-107">Users can sign in to the Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="983d6-108">Gli utenti possono essere autenticati direttamente tramite Azure AD.</span><span class="sxs-lookup"><span data-stu-id="983d6-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="983d6-109">Gli utenti possono essere autenticati tramite Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="983d6-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="983d6-110">Gli utenti possono essere autenticati tramite Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="983d6-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="983d6-111">Se un utente ha una sottoscrizione per Azure o un abbonamento a Office 365 e ha usato il portale di Azure o un'applicazione di Office 365, potrà usare il pannello di accesso in tutta semplicità senza dover eseguire di nuovo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="983d6-111">If a user has a subscription for Azure or Office 365 and has been using the Azure portal or an Office 365 application, they'll be able to use the Access Panel seamlessly without needing to sign in again.</span></span> <span data-ttu-id="983d6-112">Gli utenti non autenticati dovranno accedere usando il nome utente e la password del proprio account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="983d6-112">Users who are not authenticated be prompted to sign in by using the username and password for their account in Azure AD.</span></span> <span data-ttu-id="983d6-113">Se l'organizzazione ha configurato la federazione, sarà sufficiente digitare il nome utente.</span><span class="sxs-lookup"><span data-stu-id="983d6-113">If the organization has configured federation, typing the username is sufficient.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="983d6-114">Problemi generali da verificare per primi</span><span class="sxs-lookup"><span data-stu-id="983d6-114">General issues to check first</span></span> 

-   <span data-ttu-id="983d6-115">Verificare che l'utente acceda all'**URL corretto**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="983d6-115">Make sure the user is signing in to the **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="983d6-116">Verificare che il browser dell'utente abbia aggiunto l'URL ai **siti attendibili**</span><span class="sxs-lookup"><span data-stu-id="983d6-116">Make sure the user’s browser has added the URL to its **trusted sites**</span></span>

-   <span data-ttu-id="983d6-117">Verificare che l'account dell'utente sia **abilitato** per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="983d6-117">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="983d6-118">Verificare che l'account dell'utente non sia **bloccato**.</span><span class="sxs-lookup"><span data-stu-id="983d6-118">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="983d6-119">Verificare che la **password dell'utente non sia scaduta o non sia stata dimenticata**.</span><span class="sxs-lookup"><span data-stu-id="983d6-119">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="983d6-120">Verificare che **Multi-Factor Authentication** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="983d6-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="983d6-121">Verificare che un criterio di **accesso condizionale** o di **protezione delle identità** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="983d6-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="983d6-122">Verificare che le **informazioni di contatto per l'autenticazione** di un utente siano aggiornate per permettere l'applicazione di Multi-Factor Authentication o di criteri di accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="983d6-122">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="983d6-123">Assicurarsi anche di cancellare i cookie del browser e riprovare ad accedere.</span><span class="sxs-lookup"><span data-stu-id="983d6-123">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="983d6-124">Applicazione dei requisiti del browser per il pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="983d6-124">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="983d6-125">Per il pannello di accesso è necessario un browser che supporti JavaScript e in cui sia abilitato CSS.</span><span class="sxs-lookup"><span data-stu-id="983d6-125">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="983d6-126">Per usare il servizio Single Sign-On (SSO) basato su password nel pannello di accesso, è necessario installare l'estensione del pannello di accesso nel browser dell'utente.</span><span class="sxs-lookup"><span data-stu-id="983d6-126">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="983d6-127">Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.</span><span class="sxs-lookup"><span data-stu-id="983d6-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="983d6-128">Per l'accesso Single Sign-On basato su password il browser dell'utente finale può essere uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="983d6-128">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="983d6-129">Internet Explorer 8, 9, 10, 11 su Windows 7 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="983d6-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="983d6-130">Edge su Windows 10 Anniversary Edition o versioni successive</span><span class="sxs-lookup"><span data-stu-id="983d6-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="983d6-131">Chrome in Windows 7 o versione successiva e MacOS X o versione successiva</span><span class="sxs-lookup"><span data-stu-id="983d6-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="983d6-132">Firefox 26.0 o versione successiva in Windows XP SP2 o versione successiva e in Mac OS X 10.6 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="983d6-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-the-users-account"></a><span data-ttu-id="983d6-133">Problemi relativi all'account dell'utente</span><span class="sxs-lookup"><span data-stu-id="983d6-133">Problems with the user’s account</span></span>

<span data-ttu-id="983d6-134">L'accesso al pannello di accesso può essere bloccato a causa di un problema relativo all'account dell'utente.</span><span class="sxs-lookup"><span data-stu-id="983d6-134">Access to the Access Panel can be blocked due to a problem with the user’s account.</span></span> <span data-ttu-id="983d6-135">Di seguito sono riportate alcune soluzioni per i problemi relativi agli utenti e alle impostazioni degli account:</span><span class="sxs-lookup"><span data-stu-id="983d6-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="983d6-136">Controllare se esiste un account utente in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="983d6-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="983d6-137">Controllare lo stato dell'account di un utente</span><span class="sxs-lookup"><span data-stu-id="983d6-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="983d6-138">Reimpostare la password di un utente</span><span class="sxs-lookup"><span data-stu-id="983d6-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="983d6-139">Abilitare la reimpostazione self-service delle password</span><span class="sxs-lookup"><span data-stu-id="983d6-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="983d6-140">Controllare lo stato di autenticazione a più fattori di un utente</span><span class="sxs-lookup"><span data-stu-id="983d6-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="983d6-141">Controllare le informazioni di contatto per l'autenticazione di un utente</span><span class="sxs-lookup"><span data-stu-id="983d6-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="983d6-142">Controllare le appartenenze ai gruppi di un utente </span><span class="sxs-lookup"><span data-stu-id="983d6-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="983d6-143">Controllare le licenze assegnate di un utente</span><span class="sxs-lookup"><span data-stu-id="983d6-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="983d6-144">Assegnare una licenza a un utente</span><span class="sxs-lookup"><span data-stu-id="983d6-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="983d6-145">Controllare se esiste un account utente in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="983d6-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="983d6-146">Per controllare se l'account di un utente è presente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="983d6-146">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="983d6-147">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="983d6-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="983d6-148">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="983d6-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="983d6-149">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="983d6-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="983d6-150">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="983d6-150">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="983d6-151">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="983d6-151">click **All users**.</span></span>

6.  <span data-ttu-id="983d6-152">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="983d6-152">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="983d6-153">Controllare le proprietà dell'oggetto utente per assicurarsi che vengano specificate come previsto e che non manchi alcun dato.</span><span class="sxs-lookup"><span data-stu-id="983d6-153">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="983d6-154">Controllare lo stato dell'account di un utente</span><span class="sxs-lookup"><span data-stu-id="983d6-154">Check a user’s account status</span></span>

<span data-ttu-id="983d6-155">Per controllare lo stato dell'account di un utente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="983d6-155">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="983d6-156">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="983d6-156">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="983d6-157">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="983d6-157">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="983d6-158">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="983d6-158">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="983d6-159">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="983d6-159">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="983d6-160">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="983d6-160">click **All users**.</span></span>

6.  <span data-ttu-id="983d6-161">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="983d6-161">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="983d6-162">Fare clic su **Profilo**.</span><span class="sxs-lookup"><span data-stu-id="983d6-162">click **Profile**.</span></span>

8.  <span data-ttu-id="983d6-163">In **Impostazioni** assicurarsi che l'opzione **Blocca l'accesso** sia impostata su **No**.</span><span class="sxs-lookup"><span data-stu-id="983d6-163">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="983d6-164">Reimpostare la password di un utente</span><span class="sxs-lookup"><span data-stu-id="983d6-164">Reset a user’s password</span></span>

<span data-ttu-id="983d6-165">Per reimpostare la password di un utente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="983d6-165">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="983d6-166">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="983d6-166">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="983d6-167">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="983d6-167">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="983d6-168">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="983d6-168">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="983d6-169">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="983d6-169">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="983d6-170">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="983d6-170">click **All users**.</span></span>

6.  <span data-ttu-id="983d6-171">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="983d6-171">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="983d6-172">Fare clic sul pulsante **Reimposta password** nella parte superiore del pannello dell'utente.</span><span class="sxs-lookup"><span data-stu-id="983d6-172">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="983d6-173">Fare clic sul pulsante **Reimposta password** nel pannello **Reimposta password** visualizzato.</span><span class="sxs-lookup"><span data-stu-id="983d6-173">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="983d6-174">Copiare la **password temporanea** o **immettere una nuova password** per l'utente.</span><span class="sxs-lookup"><span data-stu-id="983d6-174">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="983d6-175">Comunicare questa nuova password all'utente, che potrebbe doverla modificare durante il successivo accesso ad Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="983d6-175">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="983d6-176">Abilitare la reimpostazione self-service delle password</span><span class="sxs-lookup"><span data-stu-id="983d6-176">Enable self-service password reset</span></span>

<span data-ttu-id="983d6-177">Per abilitare la reimpostazione self-service delle password, eseguire questa procedura di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="983d6-177">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="983d6-178">Consentire agli utenti di reimpostare le password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="983d6-178">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="983d6-179">Consentire agli utenti di reimpostare o modificare le password locali di Active Directory</span><span class="sxs-lookup"><span data-stu-id="983d6-179">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="983d6-180">Controllare lo stato di autenticazione a più fattori di un utente</span><span class="sxs-lookup"><span data-stu-id="983d6-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="983d6-181">Per controllare lo stato di autenticazione a più fattori di un utente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="983d6-181">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="983d6-182">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="983d6-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="983d6-183">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="983d6-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="983d6-184">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="983d6-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="983d6-185">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="983d6-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="983d6-186">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="983d6-186">click **All users**.</span></span>

6.  <span data-ttu-id="983d6-187">Fare clic sul pulsante **Multi-Factor Authentication** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="983d6-187">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="983d6-188">Quando viene caricato il **portale di amministrazione di Multi-Factor Authentication**, assicurarsi di passare alla scheda **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="983d6-188">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="983d6-189">Trovare l'utente nell'elenco degli utenti tramite una ricerca, l'applicazione di un filtro o l'ordinamento.</span><span class="sxs-lookup"><span data-stu-id="983d6-189">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="983d6-190">Selezionare l'utente nell'elenco di utenti e scegliere **Abilita**, **Disabilita** o **Applica** per l'autenticazione a più fattori nel modo desiderato.</span><span class="sxs-lookup"><span data-stu-id="983d6-190">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="983d6-191">Se lo stato di un utente è impostato su **Applicato**, è possibile impostarlo temporaneamente su **Disattivato** per permettere all'utente di accedere di nuovo al proprio account.</span><span class="sxs-lookup"><span data-stu-id="983d6-191">If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="983d6-192">Quando l'utente è connesso, è possibile modificarne di nuovo lo stato in **Attivato** per chiedergli di registrare di nuovo le informazioni di contatto durante il successivo accesso.</span><span class="sxs-lookup"><span data-stu-id="983d6-192">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="983d6-193">In alternativa, è possibile eseguire la procedura descritta in [Controllare le informazioni di contatto per l'autenticazione di un utente](#check-a-users-authentication-contact-info) per verificare o impostare questi dati per l'utente.</span><span class="sxs-lookup"><span data-stu-id="983d6-193">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="983d6-194">Controllare le informazioni di contatto per l'autenticazione di un utente</span><span class="sxs-lookup"><span data-stu-id="983d6-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="983d6-195">Per controllare le informazioni di contatto per l'autenticazione di un utente usate per l'autenticazione a più fattori, l'accesso condizionale, la protezione delle identità e la reimpostazione delle password, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="983d6-195">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="983d6-196">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="983d6-196">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="983d6-197">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="983d6-197">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="983d6-198">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="983d6-198">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="983d6-199">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="983d6-199">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="983d6-200">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="983d6-200">click **All users**.</span></span>

6.  <span data-ttu-id="983d6-201">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="983d6-201">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="983d6-202">Fare clic su **Profilo**.</span><span class="sxs-lookup"><span data-stu-id="983d6-202">click **Profile**.</span></span>

8.  <span data-ttu-id="983d6-203">Scorrere fino a **Informazioni di contatto per l'autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="983d6-203">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="983d6-204">Fare clic su **Verifica** per controllare i dati registrati per l'utente e aggiornarli nel modo necessario.</span><span class="sxs-lookup"><span data-stu-id="983d6-204">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="983d6-205">Controllare le appartenenze ai gruppi di un utente</span><span class="sxs-lookup"><span data-stu-id="983d6-205">Check a user’s group memberships</span></span>

<span data-ttu-id="983d6-206">Per controllare le appartenenze ai gruppi di un utente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="983d6-206">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="983d6-207">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="983d6-207">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="983d6-208">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="983d6-208">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="983d6-209">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="983d6-209">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="983d6-210">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="983d6-210">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="983d6-211">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="983d6-211">click **All users**.</span></span>

6.  <span data-ttu-id="983d6-212">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="983d6-212">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="983d6-213">Fare clic su **Gruppi** per visualizzare i gruppi di cui l'utente è membro.</span><span class="sxs-lookup"><span data-stu-id="983d6-213">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="983d6-214">Controllare le licenze assegnate di un utente</span><span class="sxs-lookup"><span data-stu-id="983d6-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="983d6-215">Per controllare le licenze assegnate di un utente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="983d6-215">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="983d6-216">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="983d6-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="983d6-217">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="983d6-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="983d6-218">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="983d6-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="983d6-219">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="983d6-219">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="983d6-220">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="983d6-220">click **All users**.</span></span>

6.  <span data-ttu-id="983d6-221">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="983d6-221">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="983d6-222">Fare clic su **Licenze** per visualizzare le licenze attualmente assegnate all'utente.</span><span class="sxs-lookup"><span data-stu-id="983d6-222">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="983d6-223">Assegnare una licenza a un utente</span><span class="sxs-lookup"><span data-stu-id="983d6-223">Assign a user a license</span></span> 

<span data-ttu-id="983d6-224">Per assegnare una licenza a un utente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="983d6-224">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="983d6-225">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="983d6-225">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="983d6-226">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="983d6-226">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="983d6-227">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="983d6-227">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="983d6-228">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="983d6-228">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="983d6-229">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="983d6-229">click **All users**.</span></span>

6.  <span data-ttu-id="983d6-230">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="983d6-230">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="983d6-231">Fare clic su **Licenze** per visualizzare le licenze attualmente assegnate all'utente.</span><span class="sxs-lookup"><span data-stu-id="983d6-231">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="983d6-232">Fare clic sul pulsante **Assegna** .</span><span class="sxs-lookup"><span data-stu-id="983d6-232">click the **Assign** button.</span></span>

9.  <span data-ttu-id="983d6-233">Selezionare **uno o più prodotti** nell'elenco dei prodotti disponibili.</span><span class="sxs-lookup"><span data-stu-id="983d6-233">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="983d6-234">**Facoltativo**: fare clic sulla voce **Opzioni di assegnazione** per assegnare in modo granulare i prodotti.</span><span class="sxs-lookup"><span data-stu-id="983d6-234">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="983d6-235">Fare clic su **OK** al termine.</span><span class="sxs-lookup"><span data-stu-id="983d6-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="983d6-236">Fare clic sul pulsante **Assegna** per assegnare queste licenze all'utente.</span><span class="sxs-lookup"><span data-stu-id="983d6-236">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="983d6-237">Se questi passaggi per la risoluzione dei problemi non risolvono il problema</span><span class="sxs-lookup"><span data-stu-id="983d6-237">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="983d6-238">Aprire un ticket di supporto con le informazioni seguenti, se disponibili:</span><span class="sxs-lookup"><span data-stu-id="983d6-238">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="983d6-239">ID errore di correlazione</span><span class="sxs-lookup"><span data-stu-id="983d6-239">Correlation error ID</span></span>

-   <span data-ttu-id="983d6-240">UPN (indirizzo di posta elettronica dell'utente)</span><span class="sxs-lookup"><span data-stu-id="983d6-240">UPN (user email address)</span></span>

-   <span data-ttu-id="983d6-241">ID tenant</span><span class="sxs-lookup"><span data-stu-id="983d6-241">Tenant ID</span></span>

-   <span data-ttu-id="983d6-242">Tipo di browser</span><span class="sxs-lookup"><span data-stu-id="983d6-242">Browser type</span></span>

-   <span data-ttu-id="983d6-243">Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore</span><span class="sxs-lookup"><span data-stu-id="983d6-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="983d6-244">Tracce Fiddler</span><span class="sxs-lookup"><span data-stu-id="983d6-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="983d6-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="983d6-245">Next steps</span></span>
[<span data-ttu-id="983d6-246">Fornire l'accesso Single Sign-On alle app con il proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="983d6-246">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
