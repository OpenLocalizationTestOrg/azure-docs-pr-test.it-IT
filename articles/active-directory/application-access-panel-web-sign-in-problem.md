---
title: la firma nel sito Web del Pannello di accesso toohello aaaProblem | Documenti Microsoft
description: Problemi di tootroubleshoot informazioni aggiuntive che possono verificarsi durante il tentativo di toosign in toouse hello Pannello di accesso
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
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a><span data-ttu-id="09007-103">Problema di accesso sito Web del Pannello di accesso toohello</span><span class="sxs-lookup"><span data-stu-id="09007-103">Problem signing in toohello access panel website</span></span>

<span data-ttu-id="09007-104">Hello Pannello di accesso è un portale basato sul web che consente un utente che ha un lavoro o scuola account in Azure Active Directory (Azure AD) tooview e avviare basato su cloud applicazioni che amministratore hello Azure AD ha concesso l'accesso a.</span><span class="sxs-lookup"><span data-stu-id="09007-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="09007-105">Un utente con le edizioni di Azure AD consente inoltre di gruppi self-service e funzionalità di gestione di app tramite hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="09007-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="09007-106">Hello Pannello di accesso è separato dal portale di Azure hello e non richiede agli utenti toohave una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="09007-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="09007-107">Gli utenti possono accedere toohello Pannello di accesso se hanno un account aziendale o dell'istituto di istruzione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="09007-107">Users can sign in toohello Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="09007-108">Gli utenti possono essere autenticati direttamente tramite Azure AD.</span><span class="sxs-lookup"><span data-stu-id="09007-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="09007-109">Gli utenti possono essere autenticati tramite Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="09007-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="09007-110">Gli utenti possono essere autenticati tramite Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="09007-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="09007-111">Se un utente dispone di una sottoscrizione per Azure o Office 365 e ha utilizzato hello portale di Azure o un'applicazione di Office 365, saranno in grado di toouse hello facilmente Pannello di accesso senza la necessità di toosign in nuovamente.</span><span class="sxs-lookup"><span data-stu-id="09007-111">If a user has a subscription for Azure or Office 365 and has been using hello Azure portal or an Office 365 application, they'll be able toouse hello Access Panel seamlessly without needing toosign in again.</span></span> <span data-ttu-id="09007-112">Gli utenti non autenticati in toosign richiesta in utilizzando hello username e password per il proprio account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="09007-112">Users who are not authenticated be prompted toosign in by using hello username and password for their account in Azure AD.</span></span> <span data-ttu-id="09007-113">Se l'organizzazione hello è configurata la federazione, digitare il nome utente hello è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="09007-113">If hello organization has configured federation, typing hello username is sufficient.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="09007-114">Generale problemi toocheck prima</span><span class="sxs-lookup"><span data-stu-id="09007-114">General issues toocheck first</span></span> 

-   <span data-ttu-id="09007-115">Verificare che l'utente hello accede toohello **correggere URL**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="09007-115">Make sure hello user is signing in toohello **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="09007-116">Assicurarsi che il browser dell'utente hello sia aggiunto hello URL tooits **siti attendibili**</span><span class="sxs-lookup"><span data-stu-id="09007-116">Make sure hello user’s browser has added hello URL tooits **trusted sites**</span></span>

-   <span data-ttu-id="09007-117">Verificare che l'account dell'utente hello è **abilitato** per accessi.</span><span class="sxs-lookup"><span data-stu-id="09007-117">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="09007-118">Verificare che l'account dell'utente hello è **non bloccato.**</span><span class="sxs-lookup"><span data-stu-id="09007-118">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="09007-119">Assicurarsi che utente hello **password non è scaduta o è stata dimenticata.**</span><span class="sxs-lookup"><span data-stu-id="09007-119">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="09007-120">Verificare che **Multi-Factor Authentication** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="09007-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="09007-121">Verificare che un criterio di **accesso condizionale** o di **protezione delle identità** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="09007-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="09007-122">Assicurarsi che un utente **informazioni di contatto autenticazione** è toodate tooallow multi-Factor Authentication o l'accesso condizionale criteri toobe applicata.</span><span class="sxs-lookup"><span data-stu-id="09007-122">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="09007-123">Verificare che tooalso try cancellare i cookie del browser e riprovare toosign in.</span><span class="sxs-lookup"><span data-stu-id="09007-123">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="09007-124">Requisiti del browser per hello Pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="09007-124">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="09007-125">Pannello di accesso Hello richiede un browser che supporta JavaScript e CSS sono state abilitate.</span><span class="sxs-lookup"><span data-stu-id="09007-125">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="09007-126">toouse basato su password single sign-on (SSO nel Pannello di accesso, hello estensione del Pannello di accesso hello) deve essere installato nel browser dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="09007-126">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="09007-127">Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.</span><span class="sxs-lookup"><span data-stu-id="09007-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="09007-128">Per SSO basato su password, browser dell'utente finale di hello può essere:</span><span class="sxs-lookup"><span data-stu-id="09007-128">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="09007-129">Internet Explorer 8, 9, 10, 11 su Windows 7 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="09007-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="09007-130">Edge su Windows 10 Anniversary Edition o versioni successive</span><span class="sxs-lookup"><span data-stu-id="09007-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="09007-131">Chrome in Windows 7 o versione successiva e MacOS X o versione successiva</span><span class="sxs-lookup"><span data-stu-id="09007-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="09007-132">Firefox 26.0 o versione successiva in Windows XP SP2 o versione successiva e in Mac OS X 10.6 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="09007-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-hello-users-account"></a><span data-ttu-id="09007-133">Problemi con l'account dell'utente hello</span><span class="sxs-lookup"><span data-stu-id="09007-133">Problems with hello user’s account</span></span>

<span data-ttu-id="09007-134">Accesso toohello Pannello di accesso può essere bloccata a causa di problemi di tooa hello account utente.</span><span class="sxs-lookup"><span data-stu-id="09007-134">Access toohello Access Panel can be blocked due tooa problem with hello user’s account.</span></span> <span data-ttu-id="09007-135">Di seguito sono riportate alcune soluzioni per i problemi relativi agli utenti e alle impostazioni degli account:</span><span class="sxs-lookup"><span data-stu-id="09007-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="09007-136">Controllare se esiste un account utente in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09007-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="09007-137">Controllare lo stato dell'account di un utente</span><span class="sxs-lookup"><span data-stu-id="09007-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="09007-138">Reimpostare la password di un utente</span><span class="sxs-lookup"><span data-stu-id="09007-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="09007-139">Abilitare la reimpostazione self-service delle password</span><span class="sxs-lookup"><span data-stu-id="09007-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="09007-140">Controllare lo stato di autenticazione a più fattori di un utente</span><span class="sxs-lookup"><span data-stu-id="09007-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="09007-141">Controllare le informazioni di contatto per l'autenticazione di un utente</span><span class="sxs-lookup"><span data-stu-id="09007-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="09007-142">Controllare le appartenenze ai gruppi di un utente </span><span class="sxs-lookup"><span data-stu-id="09007-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="09007-143">Controllare le licenze assegnate di un utente</span><span class="sxs-lookup"><span data-stu-id="09007-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="09007-144">Assegnare una licenza a un utente</span><span class="sxs-lookup"><span data-stu-id="09007-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="09007-145">Controllare se esiste un account utente in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09007-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="09007-146">Se è presente, un account utente di toocheck procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="09007-146">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="09007-147">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="09007-147">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="09007-148">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="09007-148">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="09007-149">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="09007-149">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="09007-150">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="09007-150">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="09007-151">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="09007-151">click **All users**.</span></span>

6.  <span data-ttu-id="09007-152">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="09007-152">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="09007-153">Controllare la proprietà hello di hello utente oggetto toobe assicurarsi che vengano visualizzate come previsto e che nessun dato è manca.</span><span class="sxs-lookup"><span data-stu-id="09007-153">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="09007-154">Controllare lo stato dell'account di un utente</span><span class="sxs-lookup"><span data-stu-id="09007-154">Check a user’s account status</span></span>

<span data-ttu-id="09007-155">di toocheck un utente stato dell'account, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="09007-155">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="09007-156">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="09007-156">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="09007-157">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="09007-157">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="09007-158">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="09007-158">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="09007-159">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="09007-159">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="09007-160">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="09007-160">click **All users**.</span></span>

6.  <span data-ttu-id="09007-161">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="09007-161">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="09007-162">Fare clic su **Profilo**.</span><span class="sxs-lookup"><span data-stu-id="09007-162">click **Profile**.</span></span>

8.  <span data-ttu-id="09007-163">In **impostazioni** assicurarsi che **blocco Accedi** è troppo**n**.</span><span class="sxs-lookup"><span data-stu-id="09007-163">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="09007-164">Reimpostare la password di un utente</span><span class="sxs-lookup"><span data-stu-id="09007-164">Reset a user’s password</span></span>

<span data-ttu-id="09007-165">tooreset una password, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="09007-165">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="09007-166">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="09007-166">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="09007-167">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="09007-167">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="09007-168">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="09007-168">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="09007-169">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="09007-169">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="09007-170">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="09007-170">click **All users**.</span></span>

6.  <span data-ttu-id="09007-171">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="09007-171">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="09007-172">Fare clic su hello **reimpostazione password** pulsante nella parte superiore di hello del Pannello di utente hello.</span><span class="sxs-lookup"><span data-stu-id="09007-172">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="09007-173">Fare clic su hello **reimpostazione password** pulsante hello **reimpostazione password** pannello visualizzato.</span><span class="sxs-lookup"><span data-stu-id="09007-173">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="09007-174">Hello copia **password temporanea** o **immettere una nuova password** per utente hello.</span><span class="sxs-lookup"><span data-stu-id="09007-174">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="09007-175">Comunicare il nuovo utente toohello password, essere necessario toochange questa password durante il successivo accesso tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="09007-175">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="09007-176">Abilitare la reimpostazione self-service delle password</span><span class="sxs-lookup"><span data-stu-id="09007-176">Enable self-service password reset</span></span>

<span data-ttu-id="09007-177">password self-service tooenable reimpostare, attenersi alla procedura di distribuzione hello seguente:</span><span class="sxs-lookup"><span data-stu-id="09007-177">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="09007-178">Abilitare gli utenti tooreset le password di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09007-178">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="09007-179">Abilitare gli utenti tooreset o modificare le password di Active Directory locale</span><span class="sxs-lookup"><span data-stu-id="09007-179">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="09007-180">Controllare lo stato di autenticazione a più fattori di un utente</span><span class="sxs-lookup"><span data-stu-id="09007-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="09007-181">toocheck un utente di multi-factor lo stato di autenticazione, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="09007-181">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="09007-182">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="09007-182">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="09007-183">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="09007-183">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="09007-184">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="09007-184">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="09007-185">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="09007-185">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="09007-186">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="09007-186">click **All users**.</span></span>

6.  <span data-ttu-id="09007-187">Fare clic su hello **multi-Factor Authentication** pulsante nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="09007-187">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="09007-188">Una volta hello **portale di amministrazione di multi-Factor Authentication** carichi, verificare che trovano in hello **utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="09007-188">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="09007-189">Trovare utente hello elenco hello degli utenti, la ricerca, filtro o l'ordinamento.</span><span class="sxs-lookup"><span data-stu-id="09007-189">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="09007-190">Utente selezionare hello hello elenco di utenti e **abilitare**, **disabilitare**, o **Imponi** autenticazione a più fattori in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="09007-190">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="09007-191">Se un utente si trova in un **applicato** stato, è possibile impostarle troppo**disabilitato** temporaneamente toolet li nuovamente nel proprio account.</span><span class="sxs-lookup"><span data-stu-id="09007-191">If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="09007-192">Una volta in, è possibile modificare il proprio stato troppo**abilitato** nuovamente toorequire li toore la registrazione di informazioni sul contatto durante il successivo accesso.</span><span class="sxs-lookup"><span data-stu-id="09007-192">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="09007-193">In alternativa, è possibile seguire i passaggi hello hello [informazioni di contatto di autenticazione dell'utente di controllare](#check-a-users-authentication-contact-info) tooverify o set di dati per loro.</span><span class="sxs-lookup"><span data-stu-id="09007-193">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="09007-194">Controllare le informazioni di contatto per l'autenticazione di un utente</span><span class="sxs-lookup"><span data-stu-id="09007-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="09007-195">informazioni utilizzate per multi-factor authentication, l'accesso condizionale, la protezione dell'identità e la reimpostazione della Password, contattare l'autenticazione dell'utente toocheck procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="09007-195">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="09007-196">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="09007-196">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="09007-197">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="09007-197">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="09007-198">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="09007-198">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="09007-199">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="09007-199">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="09007-200">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="09007-200">click **All users**.</span></span>

6.  <span data-ttu-id="09007-201">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="09007-201">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="09007-202">Fare clic su **Profilo**.</span><span class="sxs-lookup"><span data-stu-id="09007-202">click **Profile**.</span></span>

8.  <span data-ttu-id="09007-203">Scorrere verso il basso troppo**informazioni di contatto autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="09007-203">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="09007-204">**Revisione** dati hello registrati per utente hello e aggiornare in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="09007-204">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="09007-205">Controllare le appartenenze a gruppi dell'utente</span><span class="sxs-lookup"><span data-stu-id="09007-205">Check a user’s group memberships</span></span>

<span data-ttu-id="09007-206">di toocheck un utente appartenenza ai gruppi, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="09007-206">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="09007-207">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="09007-207">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="09007-208">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="09007-208">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="09007-209">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="09007-209">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="09007-210">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="09007-210">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="09007-211">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="09007-211">click **All users**.</span></span>

6.  <span data-ttu-id="09007-212">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="09007-212">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="09007-213">Fare clic su **gruppi** toosee gruppi utente hello è membro.</span><span class="sxs-lookup"><span data-stu-id="09007-213">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="09007-214">Controllare le licenze assegnate di un utente</span><span class="sxs-lookup"><span data-stu-id="09007-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="09007-215">toocheck un utente assegnate le licenze, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="09007-215">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="09007-216">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="09007-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="09007-217">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="09007-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="09007-218">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="09007-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="09007-219">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="09007-219">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="09007-220">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="09007-220">click **All users**.</span></span>

6.  <span data-ttu-id="09007-221">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="09007-221">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="09007-222">Fare clic su **licenze** toosee utente hello licenze è attualmente assegnato.</span><span class="sxs-lookup"><span data-stu-id="09007-222">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="09007-223">Assegnare una licenza a un utente</span><span class="sxs-lookup"><span data-stu-id="09007-223">Assign a user a license</span></span> 

<span data-ttu-id="09007-224">un utente, tooa licenza tooassign procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="09007-224">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="09007-225">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="09007-225">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="09007-226">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="09007-226">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="09007-227">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="09007-227">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="09007-228">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="09007-228">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="09007-229">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="09007-229">click **All users**.</span></span>

6.  <span data-ttu-id="09007-230">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="09007-230">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="09007-231">Fare clic su **licenze** toosee utente hello licenze è attualmente assegnato.</span><span class="sxs-lookup"><span data-stu-id="09007-231">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="09007-232">Fare clic su hello **assegnare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="09007-232">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="09007-233">Selezionare **uno o più prodotti** dall'elenco di hello dei prodotti disponibili.</span><span class="sxs-lookup"><span data-stu-id="09007-233">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="09007-234">**Parametro facoltativo** fare clic su hello **opzioni assegnazione** toogranularly elemento assegnare i prodotti.</span><span class="sxs-lookup"><span data-stu-id="09007-234">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="09007-235">Fare clic su **OK** al termine.</span><span class="sxs-lookup"><span data-stu-id="09007-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="09007-236">Fare clic su hello **assegnare** pulsante tooassign questi utente toothis licenze.</span><span class="sxs-lookup"><span data-stu-id="09007-236">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="09007-237">Se i passaggi di risoluzione dei problemi non risolvono il problema di hello</span><span class="sxs-lookup"><span data-stu-id="09007-237">If these troubleshooting steps do not resolve hello issue</span></span>

<span data-ttu-id="09007-238">Aprire un ticket di supporto con hello se disponibili le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="09007-238">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="09007-239">ID errore di correlazione</span><span class="sxs-lookup"><span data-stu-id="09007-239">Correlation error ID</span></span>

-   <span data-ttu-id="09007-240">UPN (indirizzo di posta elettronica dell'utente)</span><span class="sxs-lookup"><span data-stu-id="09007-240">UPN (user email address)</span></span>

-   <span data-ttu-id="09007-241">ID tenant</span><span class="sxs-lookup"><span data-stu-id="09007-241">Tenant ID</span></span>

-   <span data-ttu-id="09007-242">Tipo di browser</span><span class="sxs-lookup"><span data-stu-id="09007-242">Browser type</span></span>

-   <span data-ttu-id="09007-243">Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore</span><span class="sxs-lookup"><span data-stu-id="09007-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="09007-244">Tracce Fiddler</span><span class="sxs-lookup"><span data-stu-id="09007-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="09007-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="09007-245">Next steps</span></span>
[<span data-ttu-id="09007-246">Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="09007-246">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
