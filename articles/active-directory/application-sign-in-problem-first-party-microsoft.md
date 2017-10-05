---
title: Problemi di accesso a un'applicazione Microsoft | Microsoft Docs
description: Risoluzione di problemi comuni relativi all'accesso ad applicazioni prodotte direttamente da Microsoft usando Azure AD (ad esempio Office 365)
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
ms.openlocfilehash: 5638434270ee82d2b9737ea8eed8b5a8c62f7121
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
## <a name="problems-signing-in-to-a-microsoft-application"></a><span data-ttu-id="1d86e-103">Problemi di accesso a un'applicazione Microsoft</span><span class="sxs-lookup"><span data-stu-id="1d86e-103">Problems signing in to a Microsoft application</span></span>

<span data-ttu-id="1d86e-104">Le applicazioni Microsoft (ad esempio Office 365 Exchange, SharePoint, Yammer e così via) vengono assegnate e gestite in modo leggermente diverso dalle applicazioni SaaS di terza parte o da altre applicazioni che si integrano con Azure AD per Single Sign On.</span><span class="sxs-lookup"><span data-stu-id="1d86e-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="1d86e-105">Vi sono tre principali modi con cui un utente può accedere a un'applicazione pubblicata da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1d86e-105">There are three main ways that a user can get access to a Microsoft-published application.</span></span>

-   <span data-ttu-id="1d86e-106">Per le applicazioni in Office 365 o in altre famiglie di prodotti a pagamento, agli utenti è consentito l'accesso tramite l'**assegnazione di una licenza** direttamente all'account utente o tramite un gruppo utilizzando la funzionalità di assegnazione di licenze di gruppo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-106">For applications in the Office 365 or other paid suites, users are granted access through **license assignment** either directly to their user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="1d86e-107">Per le applicazioni che Microsoft o una terza parte pubblica per l'utilizzo gratuito da parte di chiunque, gli utenti possono ottenere l'accesso tramite **consenso dell'utente**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-107">For applications that Microsoft or a Third Party publishes freely for anyone to use, users may be granted access through **user consent**.</span></span> <span data-ttu-id="1d86e-108">Ciò significa che gli utenti accedono all'applicazione con il loro account Azure AD Work o School e consentono a tale applicazione di accedere a un set limitato di dati del loro account.</span><span class="sxs-lookup"><span data-stu-id="1d86e-108">This0 means that they sign in to the application with their Azure AD Work or School account and allow it to have access to some limited set of data on their account.</span></span>

-   <span data-ttu-id="1d86e-109">Per le applicazioni che Microsoft o una terza parte pubblica per l'utilizzo gratuito da parte di chiunque, gli utenti possono ottenere l'accesso tramite **consenso dell'amministratore**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-109">For applications that Microsoft or a 3rd Party publishes freely for anyone to use, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="1d86e-110">Ciò significa che un amministratore ha determinato che l'applicazione può essere usata da qualsiasi utente dell'organizzazione e, tale scopo, ha effettuato l'accesso all'applicazione con un account di amministratore globale e ha consentito l'accesso a tutti gli utenti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-110">This means that an administrator has determined the application may be used by everyone in the organization, so they sign in to the application with a Global Administrator account and grant access to everyone in the organization.</span></span>

<span data-ttu-id="1d86e-111">Per risolvere il problema, iniziare dalla sezione [Aree generali da considerare per i problemi di accesso alle applicazioni](#general-problem-areas-with-application-access-to-consider) e quindi leggere la [Procedura dettagliata: passaggi per risolvere i problemi di accesso alle applicazioni Microsoft](#walkthrough-steps-to-troubleshoot-microsoft-application-access) per maggiori dettagli.</span><span class="sxs-lookup"><span data-stu-id="1d86e-111">To troubleshoot your issue, start with the [General Problem Areas with Application Access to consider](#general-problem-areas-with-application-access-to-consider) and then read the [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) to get into the details.</span></span>

## <a name="general-problem-areas-with-application-access-to-consider"></a><span data-ttu-id="1d86e-112">Aree generali da considerare per i problemi di accesso alle applicazioni</span><span class="sxs-lookup"><span data-stu-id="1d86e-112">General Problem Areas with Application Access to consider</span></span>

<span data-ttu-id="1d86e-113">Di seguito è riportato un elenco delle aree generali del problema da consultare se si sa da dove iniziare ma, per procedere rapidamente, è consigliabile leggere la [Procedura dettagliata: passaggi per risolvere i problemi di accesso alle applicazioni Microsoft](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="1d86e-113">Below is a list of the general problem areas that you can drill into if you have an idea of where to start, but we recommend you read the walkthrough to get going quickly: [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="1d86e-114">Problemi relativi all'account dell'utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-114">Problems with the user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="1d86e-115">Problemi relativi ai gruppi</span><span class="sxs-lookup"><span data-stu-id="1d86e-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="1d86e-116">Problemi relativi ai criteri di accesso condizionale</span><span class="sxs-lookup"><span data-stu-id="1d86e-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="1d86e-117">Problemi relativi al consenso dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="1d86e-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-to-troubleshoot-microsoft-application-access"></a><span data-ttu-id="1d86e-118">Passaggi per risolvere i problemi di accesso alle applicazioni Microsoft</span><span class="sxs-lookup"><span data-stu-id="1d86e-118">Steps to troubleshoot Microsoft Application access</span></span>

<span data-ttu-id="1d86e-119">Di seguito sono riportati alcuni problemi comuni che vengono riscontrati quando gli utenti non riescono ad accedere a un'applicazione Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1d86e-119">Below are some common issues folks run into when their users cannot sign in to a Microsoft application.</span></span>

-   <span data-ttu-id="1d86e-120">Problemi generali da verificare per primi</span><span class="sxs-lookup"><span data-stu-id="1d86e-120">General issues to check first</span></span>

  * <span data-ttu-id="1d86e-121">Verificare che l'utente acceda all'**URL corretto** e non a un URL dell'applicazione locale.</span><span class="sxs-lookup"><span data-stu-id="1d86e-121">Make sure the user is signing in to the **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="1d86e-122">Verificare che l'account dell'utente non sia **bloccato**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-122">Make sure the user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="1d86e-123">Verificare che l'**account dell'utente sia presente** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1d86e-123">Make sure the **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="1d86e-124">Controllare se esiste un account utente in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d86e-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="1d86e-125">Verificare che l'account dell'utente sia **abilitato** per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="1d86e-125">Make sure the user’s account is **enabled** for sign ins.</span></span> [<span data-ttu-id="1d86e-126">Controllare lo stato dell'account di un utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-126">Check a user’s account status</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="1d86e-127">Verificare che la **password dell'utente non sia scaduta o non sia stata dimenticata**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-127">Make sure the user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="1d86e-128">[Reimpostare la password di un utente](#reset-a-users-password) o [Abilitare la reimpostazione self-service delle password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="1d86e-128">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="1d86e-129">Verificare che **Multi-Factor Authentication** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="1d86e-129">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="1d86e-130">[Controllare lo stato di autenticazione a più fattori di un utente](#check-a-users-multi-factor-authentication-status) o [Controllare le informazioni di contatto per l'autenticazione di un utente](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="1d86e-130">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="1d86e-131">Verificare che un criterio di **accesso condizionale** o di **protezione delle identità** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="1d86e-131">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="1d86e-132">[Controllare un criterio specifico di accesso condizionale](#problems-with-conditional-access-policies), [Controllare i criteri di accesso condizionale di un'applicazione specifica](#check-a-specific-applications-conditional-access-policy) o [Disabilitare un criterio specifico di accesso condizionale](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="1d86e-132">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="1d86e-133">Verificare che le **informazioni di contatto per l'autenticazione** di un utente siano aggiornate per permettere l'applicazione di Multi-Factor Authentication o di criteri di accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="1d86e-133">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span> <span data-ttu-id="1d86e-134">[Controllare lo stato di autenticazione a più fattori di un utente](#check-a-users-multi-factor-authentication-status) o [Controllare le informazioni di contatto per l'autenticazione di un utente](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="1d86e-134">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="1d86e-135">Per le applicazioni **Microsoft** **che richiedono una licenza** (ad esempio Office365), di seguito sono riportati alcuni problemi specifici da verificare dopo aver escluso i problemi generali sopra elencati:</span><span class="sxs-lookup"><span data-stu-id="1d86e-135">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues to check once you have ruled out the general issues above:</span></span>

   * <span data-ttu-id="1d86e-136">Assicurarsi che all'utente sia **assegnata una licenza**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-136">Ensure the user or has a **license assigned.**</span></span> <span data-ttu-id="1d86e-137">[Controllare le licenze assegnate a un utente](#check-a-users-assigned-licenses) o [Controllare le licenze assegnate a un gruppo](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="1d86e-137">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="1d86e-138">Se la licenza è **assegnata a un** **gruppo statico**, assicurarsi che l'**utente sia membro** di tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-138">If the license is **assigned to a** **static group**, ensure that the **user is a member** of that group.</span></span> [<span data-ttu-id="1d86e-139">Controllare le appartenenze ai gruppi di un utente </span><span class="sxs-lookup"><span data-stu-id="1d86e-139">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="1d86e-140">Se la licenza è **assegnata a un** **gruppo dinamico**, assicurarsi che **la regola di gruppo dinamico sia impostata correttamente**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-140">If the license is **assigned to a** **dynamic group**, ensure that the **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="1d86e-141">Controllare i criteri di appartenenza di un gruppo dinamico</span><span class="sxs-lookup"><span data-stu-id="1d86e-141">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="1d86e-142">Se la licenza è **assegnata a un** **gruppo dinamico**, assicurarsi che il gruppo dinamico abbia **completato l'elaborazione** della propria appartenenza e che l'**utente sia un membro** (questa operazione può richiedere un certo tempo).</span><span class="sxs-lookup"><span data-stu-id="1d86e-142">If the license is **assigned to a** **dynamic group**, ensure that the dynamic group has **finished processing** its membership and that the **user is a member** (this can take some time).</span></span> [<span data-ttu-id="1d86e-143">Controllare le appartenenze ai gruppi di un utente </span><span class="sxs-lookup"><span data-stu-id="1d86e-143">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="1d86e-144">Dopo aver verificato che la licenza è assegnata, assicurarsi che **non sia scaduta**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-144">Once you make sure the license is assigned, make sure the license is **not expired**.</span></span>

   *  <span data-ttu-id="1d86e-145">Accertarsi che la licenza sia **relativa all'applicazione** a cui gli utenti stanno accedendo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-145">Make sure the license is **for the application** they are accessing.</span></span>

-   <span data-ttu-id="1d86e-146">Per le applicazioni **Microsoft** **che non richiedono una licenza**, di seguito sono riportati altri aspetti da controllare:</span><span class="sxs-lookup"><span data-stu-id="1d86e-146">For **Microsoft** **applications that don’t require a license**, here are some other things to check:</span></span>

   * <span data-ttu-id="1d86e-147">Se l'applicazione richiede **autorizzazioni a livello di utente** (ad esempio "Accesso alla cassetta postale di questo utente"), assicurarsi che l'utente abbia eseguito l'accesso all'applicazione e abbia eseguito un'**operazione di consenso a livello di utente** per permettere all'applicazione di accedere ai suoi dati.</span><span class="sxs-lookup"><span data-stu-id="1d86e-147">If the application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that the user has signed in to the application and has performed a **user-level consent operation** to let the application access her data.</span></span>

   * <span data-ttu-id="1d86e-148">Se l'applicazione richiede **autorizzazioni a livello di amministratore** (ad esempio "Accesso alle cassette postali di tutti gli utenti"), assicurarsi che un amministratore globale abbia eseguito un'**operazione di consenso a livello di amministratore per conto di tutti gli utenti** dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-148">If the application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in the organization.</span></span>

## <a name="problems-with-the-users-account"></a><span data-ttu-id="1d86e-149">Problemi relativi all'account dell'utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-149">Problems with the user’s account</span></span>

<span data-ttu-id="1d86e-150">L'accesso all'applicazione può essere bloccato a causa di un problema relativo a un utente assegnato all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-150">Application access can be blocked due to a problem with a user that is assigned to the application.</span></span> <span data-ttu-id="1d86e-151">Di seguito sono riportate alcune soluzioni per i problemi relativi agli utenti e alle impostazioni degli account:</span><span class="sxs-lookup"><span data-stu-id="1d86e-151">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="1d86e-152">Controllare se esiste un account utente in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d86e-152">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="1d86e-153">Controllare lo stato dell'account di un utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-153">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="1d86e-154">Reimpostare la password di un utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-154">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="1d86e-155">Abilitare la reimpostazione self-service delle password</span><span class="sxs-lookup"><span data-stu-id="1d86e-155">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="1d86e-156">Controllare lo stato di autenticazione a più fattori di un utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-156">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="1d86e-157">Controllare le informazioni di contatto per l'autenticazione di un utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-157">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="1d86e-158">Controllare le appartenenze ai gruppi di un utente </span><span class="sxs-lookup"><span data-stu-id="1d86e-158">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="1d86e-159">Controllare le licenze assegnate di un utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-159">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="1d86e-160">Assegnare una licenza a un utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-160">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="1d86e-161">Controllare se esiste un account utente in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d86e-161">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="1d86e-162">Per controllare se l'account di un utente è presente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1d86e-162">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="1d86e-163">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-163">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-164">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-164">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-165">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-165">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-166">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-166">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-167">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-167">click **All users**.</span></span>

6.  <span data-ttu-id="1d86e-168">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-168">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="1d86e-169">Controllare le proprietà dell'oggetto utente per assicurarsi che vengano specificate come previsto e che non manchi alcun dato.</span><span class="sxs-lookup"><span data-stu-id="1d86e-169">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="1d86e-170">Controllare lo stato dell'account di un utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-170">Check a user’s account status</span></span>

<span data-ttu-id="1d86e-171">Per controllare lo stato dell'account di un utente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1d86e-171">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="1d86e-172">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-172">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-173">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-173">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-174">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-174">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-175">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-175">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-176">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-176">click **All users**.</span></span>

6.  <span data-ttu-id="1d86e-177">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-177">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="1d86e-178">Fare clic su **Profilo**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-178">click **Profile**.</span></span>

8.  <span data-ttu-id="1d86e-179">In **Impostazioni** assicurarsi che l'opzione **Blocca l'accesso** sia impostata su **No**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-179">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="1d86e-180">Reimpostare la password di un utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-180">Reset a user’s password</span></span>

<span data-ttu-id="1d86e-181">Per reimpostare la password di un utente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1d86e-181">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="1d86e-182">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-183">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-184">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-185">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-186">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-186">click **All users**.</span></span>

6.  <span data-ttu-id="1d86e-187">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-187">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="1d86e-188">Fare clic sul pulsante **Reimposta password** nella parte superiore del pannello dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1d86e-188">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="1d86e-189">Fare clic sul pulsante **Reimposta password** nel pannello **Reimposta password** visualizzato.</span><span class="sxs-lookup"><span data-stu-id="1d86e-189">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="1d86e-190">Copiare la **password temporanea** o **immettere una nuova password** per l'utente.</span><span class="sxs-lookup"><span data-stu-id="1d86e-190">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="1d86e-191">Comunicare questa nuova password all'utente, che potrebbe doverla modificare durante il successivo accesso ad Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1d86e-191">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="1d86e-192">Abilitare la reimpostazione self-service delle password</span><span class="sxs-lookup"><span data-stu-id="1d86e-192">Enable self-service password reset</span></span>

<span data-ttu-id="1d86e-193">Per abilitare la reimpostazione self-service delle password, eseguire questa procedura di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="1d86e-193">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="1d86e-194">Consentire agli utenti di reimpostare le password di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d86e-194">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="1d86e-195">Consentire agli utenti di reimpostare o modificare le password locali di Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d86e-195">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="1d86e-196">Controllare lo stato di autenticazione a più fattori di un utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-196">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="1d86e-197">Per controllare lo stato di autenticazione a più fattori di un utente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1d86e-197">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="1d86e-198">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-199">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-200">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-201">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-201">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-202">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-202">click **All users**.</span></span>

6.  <span data-ttu-id="1d86e-203">Fare clic sul pulsante **Multi-Factor Authentication** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="1d86e-203">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="1d86e-204">Quando viene caricato il **portale di amministrazione di Multi-Factor Authentication**, assicurarsi di passare alla scheda **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-204">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="1d86e-205">Trovare l'utente nell'elenco degli utenti tramite una ricerca, l'applicazione di un filtro o l'ordinamento.</span><span class="sxs-lookup"><span data-stu-id="1d86e-205">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="1d86e-206">Selezionare l'utente nell'elenco di utenti e scegliere **Abilita**, **Disabilita** o **Applica** per l'autenticazione a più fattori nel modo desiderato.</span><span class="sxs-lookup"><span data-stu-id="1d86e-206">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="1d86e-207">**Nota**: Se lo stato di un utente è impostato su **Applicato**, è possibile impostarlo temporaneamente su **Disattivato** per permettere all'utente di accedere di nuovo al proprio account.</span><span class="sxs-lookup"><span data-stu-id="1d86e-207">**Note**: If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="1d86e-208">Quando l'utente è connesso, è possibile modificarne di nuovo lo stato in **Attivato** per chiedergli di registrare di nuovo le informazioni di contatto durante il successivo accesso.</span><span class="sxs-lookup"><span data-stu-id="1d86e-208">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="1d86e-209">In alternativa, è possibile eseguire la procedura descritta in [Controllare le informazioni di contatto per l'autenticazione di un utente](#check-a-users-authentication-contact-info) per verificare o impostare questi dati per l'utente.</span><span class="sxs-lookup"><span data-stu-id="1d86e-209">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="1d86e-210">Controllare le informazioni di contatto per l'autenticazione di un utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-210">Check a user’s authentication contact info</span></span>

<span data-ttu-id="1d86e-211">Per controllare le informazioni di contatto per l'autenticazione di un utente usate per l'autenticazione a più fattori, l'accesso condizionale, la protezione delle identità e la reimpostazione delle password, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1d86e-211">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="1d86e-212">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-212">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-213">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-213">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-214">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-214">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-215">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-215">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-216">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-216">click **All users**.</span></span>

6.  <span data-ttu-id="1d86e-217">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-217">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="1d86e-218">Fare clic su **Profilo**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-218">click **Profile**.</span></span>

8.  <span data-ttu-id="1d86e-219">Scorrere fino a **Informazioni di contatto per l'autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-219">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="1d86e-220">Fare clic su **Verifica** per controllare i dati registrati per l'utente e aggiornarli nel modo necessario.</span><span class="sxs-lookup"><span data-stu-id="1d86e-220">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="1d86e-221">Controllare le appartenenze ai gruppi di un utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-221">Check a user’s group memberships</span></span>

<span data-ttu-id="1d86e-222">Per controllare le appartenenze ai gruppi di un utente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1d86e-222">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="1d86e-223">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-223">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-224">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-224">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-225">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-225">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-226">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-226">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-227">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-227">click **All users**.</span></span>

6.  <span data-ttu-id="1d86e-228">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-228">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="1d86e-229">Fare clic su **Gruppi** per visualizzare i gruppi di cui l'utente è membro.</span><span class="sxs-lookup"><span data-stu-id="1d86e-229">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="1d86e-230">Controllare le licenze assegnate di un utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-230">Check a user’s assigned licenses</span></span>

<span data-ttu-id="1d86e-231">Per controllare le licenze assegnate di un utente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1d86e-231">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="1d86e-232">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-232">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-233">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-233">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-234">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-234">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-235">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-235">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-236">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-236">click **All users**.</span></span>

6.  <span data-ttu-id="1d86e-237">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-237">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="1d86e-238">Fare clic su **Licenze** per visualizzare le licenze attualmente assegnate all'utente.</span><span class="sxs-lookup"><span data-stu-id="1d86e-238">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="1d86e-239">Assegnare una licenza a un utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-239">Assign a user a license</span></span> 

<span data-ttu-id="1d86e-240">Per assegnare una licenza a un utente, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1d86e-240">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="1d86e-241">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-242">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-243">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-244">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-244">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-245">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-245">click **All users**.</span></span>

6.  <span data-ttu-id="1d86e-246">**Cercare** l'utente desiderato e **fare clic sulla riga corrispondente** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-246">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="1d86e-247">Fare clic su **Licenze** per visualizzare le licenze attualmente assegnate all'utente.</span><span class="sxs-lookup"><span data-stu-id="1d86e-247">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="1d86e-248">Fare clic sul pulsante **Assegna** .</span><span class="sxs-lookup"><span data-stu-id="1d86e-248">click the **Assign** button.</span></span>

9.  <span data-ttu-id="1d86e-249">Selezionare **uno o più prodotti** nell'elenco dei prodotti disponibili.</span><span class="sxs-lookup"><span data-stu-id="1d86e-249">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="1d86e-250">**Facoltativo**: fare clic sulla voce **Opzioni di assegnazione** per assegnare in modo granulare i prodotti.</span><span class="sxs-lookup"><span data-stu-id="1d86e-250">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="1d86e-251">Fare clic su **OK** al termine.</span><span class="sxs-lookup"><span data-stu-id="1d86e-251">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="1d86e-252">Fare clic sul pulsante **Assegna** per assegnare queste licenze all'utente.</span><span class="sxs-lookup"><span data-stu-id="1d86e-252">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="1d86e-253">Problemi relativi ai gruppi</span><span class="sxs-lookup"><span data-stu-id="1d86e-253">Problems with groups</span></span>

<span data-ttu-id="1d86e-254">L'accesso all'applicazione può essere bloccato a causa di un problema relativo a un gruppo assegnato all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-254">Application access can be blocked due to a problem with a group that is assigned to the application.</span></span> <span data-ttu-id="1d86e-255">Di seguito sono riportate alcune soluzioni per i problemi relativi a gruppi e ad appartenenze a gruppi:</span><span class="sxs-lookup"><span data-stu-id="1d86e-255">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="1d86e-256">Controllare l'appartenenza di un gruppo</span><span class="sxs-lookup"><span data-stu-id="1d86e-256">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="1d86e-257">Controllare i criteri di appartenenza di un gruppo dinamico</span><span class="sxs-lookup"><span data-stu-id="1d86e-257">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="1d86e-258">Controllare le licenze assegnate di un gruppo</span><span class="sxs-lookup"><span data-stu-id="1d86e-258">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="1d86e-259">Rielaborare le licenze di un gruppo</span><span class="sxs-lookup"><span data-stu-id="1d86e-259">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="1d86e-260">Assegnare una licenza a un gruppo</span><span class="sxs-lookup"><span data-stu-id="1d86e-260">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="1d86e-261">Controllare l'appartenenza di un gruppo</span><span class="sxs-lookup"><span data-stu-id="1d86e-261">Check a group’s membership</span></span>

<span data-ttu-id="1d86e-262">Per controllare un'appartenenza a un gruppo, seguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d86e-262">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="1d86e-263">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-263">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-264">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-264">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-265">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-265">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-266">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-266">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-267">Fare clic su **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-267">click **All groups**.</span></span>

6.  <span data-ttu-id="1d86e-268">**Cercare** il gruppo desiderato e **fare clic sulla relativa riga** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-268">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="1d86e-269">Fare clic su **Membri** per esaminare l'elenco di utenti assegnati a questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-269">click **Members** to review the list of users assigned to this group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="1d86e-270">Controllare i criteri di appartenenza di un gruppo dinamico</span><span class="sxs-lookup"><span data-stu-id="1d86e-270">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="1d86e-271">Per controllare i criteri di appartenenza di un gruppo dinamico, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1d86e-271">To check a dynamic group’s membership criteria, follow the steps below:</span></span>

1.  <span data-ttu-id="1d86e-272">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-272">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-273">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-273">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-274">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-274">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-275">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-275">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-276">Fare clic su **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-276">click **All groups**.</span></span>

6.  <span data-ttu-id="1d86e-277">**Cercare** il gruppo desiderato e **fare clic sulla relativa riga** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-277">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="1d86e-278">Fare clic su **Regole di appartenenza dinamica**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-278">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="1d86e-279">Verificare la regola **semplice** o **avanzata** definita per questo gruppo e assicurarsi che l'utente che deve appartenere al gruppo soddisfi i criteri relativi.</span><span class="sxs-lookup"><span data-stu-id="1d86e-279">Review the **simple** or **advanced** rule defined for this group and ensure that the user you want to be a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="1d86e-280">Controllare le licenze assegnate di un gruppo</span><span class="sxs-lookup"><span data-stu-id="1d86e-280">Check a group’s assigned licenses</span></span>

<span data-ttu-id="1d86e-281">Per controllare le licenze assegnate di un gruppo, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1d86e-281">To check a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="1d86e-282">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-282">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-283">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-283">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-284">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-284">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-285">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-285">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-286">Fare clic su **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-286">click **All groups**.</span></span>

6.  <span data-ttu-id="1d86e-287">**Cercare** il gruppo desiderato e **fare clic sulla relativa riga** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-287">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="1d86e-288">Fare clic su **Licenze** per visualizzare le licenze attualmente assegnate al gruppo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-288">click **Licenses** to see which licenses the group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="1d86e-289">Rielaborare le licenze di un gruppo</span><span class="sxs-lookup"><span data-stu-id="1d86e-289">Reprocess a group’s licenses</span></span>

<span data-ttu-id="1d86e-290">Per rielaborare le licenze assegnate di un gruppo, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1d86e-290">To reprocess a group’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="1d86e-291">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-292">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-293">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-294">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-294">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-295">Fare clic su **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-295">click **All groups**.</span></span>

6.  <span data-ttu-id="1d86e-296">**Cercare** il gruppo desiderato e **fare clic sulla relativa riga** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-296">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="1d86e-297">Fare clic su **Licenze** per visualizzare le licenze attualmente assegnate al gruppo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-297">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="1d86e-298">Fare clic sul pulsante **Rielabora** per assicurarsi che le licenze assegnate ai membri di questo gruppo siano aggiornate.</span><span class="sxs-lookup"><span data-stu-id="1d86e-298">click the **Reprocess** button to ensure that the licenses assigned to this group’s members are up-to-date.</span></span> <span data-ttu-id="1d86e-299">L'operazione potrebbe richiedere molto tempo a seconda della dimensione e della complessità del gruppo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-299">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="1d86e-300">Per eseguire l'operazione più velocemente, è consigliabile assegnare temporaneamente una licenza direttamente all'utente.</span><span class="sxs-lookup"><span data-stu-id="1d86e-300">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="1d86e-301">[Assegnare una licenza a un utente](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="1d86e-301">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="1d86e-302">Assegnare una licenza a un gruppo</span><span class="sxs-lookup"><span data-stu-id="1d86e-302">Assign a group a license</span></span>

<span data-ttu-id="1d86e-303">Per assegnare una licenza a un gruppo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1d86e-303">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="1d86e-304">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-304">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-305">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-305">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-306">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-306">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-307">Fare clic su **Utenti e gruppi** nel menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-307">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-308">Fare clic su **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-308">click **All groups**.</span></span>

6.  <span data-ttu-id="1d86e-309">**Cercare** il gruppo desiderato e **fare clic sulla relativa riga** per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-309">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="1d86e-310">Fare clic su **Licenze** per visualizzare le licenze attualmente assegnate al gruppo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-310">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="1d86e-311">Fare clic sul pulsante **Assegna** .</span><span class="sxs-lookup"><span data-stu-id="1d86e-311">click the **Assign** button.</span></span>

9.  <span data-ttu-id="1d86e-312">Selezionare **uno o più prodotti** nell'elenco dei prodotti disponibili.</span><span class="sxs-lookup"><span data-stu-id="1d86e-312">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="1d86e-313">**Facoltativo**: fare clic sulla voce **Opzioni di assegnazione** per assegnare in modo granulare i prodotti.</span><span class="sxs-lookup"><span data-stu-id="1d86e-313">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="1d86e-314">Fare clic su **OK** al termine.</span><span class="sxs-lookup"><span data-stu-id="1d86e-314">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="1d86e-315">Fare clic sul pulsante **Assegna** per assegnare queste licenze al gruppo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-315">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="1d86e-316">L'operazione potrebbe richiedere molto tempo a seconda della dimensione e della complessità del gruppo.</span><span class="sxs-lookup"><span data-stu-id="1d86e-316">This may take a long time, depending on the size and complexity of the group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="1d86e-317">Per eseguire l'operazione più velocemente, è consigliabile assegnare temporaneamente una licenza direttamente all'utente.</span><span class="sxs-lookup"><span data-stu-id="1d86e-317">To do this faster, consider temporarily assigning a license to the user directly.</span></span> <span data-ttu-id="1d86e-318">[Assegnare una licenza a un utente](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="1d86e-318">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="1d86e-319">Problemi relativi ai criteri di accesso condizionale</span><span class="sxs-lookup"><span data-stu-id="1d86e-319">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="1d86e-320">Selezionare un criterio di accesso condizionale specifico</span><span class="sxs-lookup"><span data-stu-id="1d86e-320">Check a specific conditional access policy</span></span>

<span data-ttu-id="1d86e-321">Per verificare o convalidare un singolo criterio di accesso condizionale:</span><span class="sxs-lookup"><span data-stu-id="1d86e-321">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="1d86e-322">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-322">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-323">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-323">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-324">Digitare **"Azure Active Directory"** nella casella di ricerca del filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-324">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-325">Scegliere **Applicazioni aziendali** dal menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-325">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-326">Fare clic sulla voce di navigazione **Accesso condizionale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-326">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="1d86e-327">Fare clic sul criterio che si desidera controllare.</span><span class="sxs-lookup"><span data-stu-id="1d86e-327">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="1d86e-328">Verificare che non vi siano condizioni specifiche, assegnazioni o altre impostazioni che possano bloccare l'accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1d86e-328">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="1d86e-329">Può essere opportuno disabilitare temporaneamente questo criterio per assicurarsi che non impedisca gli accessi.</span><span class="sxs-lookup"><span data-stu-id="1d86e-329">You may wish to temporarily disable this policy to ensure it is not affecting sign ins.</span></span> <span data-ttu-id="1d86e-330">A tale scopo, impostare **Abilita criterio** su **No** e fare clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-330">To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="1d86e-331">Controllare i criteri di accesso condizionale di un'applicazione specifica</span><span class="sxs-lookup"><span data-stu-id="1d86e-331">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="1d86e-332">Per verificare o convalidare i criteri di accesso condizionale attualmente configurati di una singola applicazione:</span><span class="sxs-lookup"><span data-stu-id="1d86e-332">To check or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="1d86e-333">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-333">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-334">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-334">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-335">Digitare **"Azure Active Directory"** nella casella di ricerca del filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-335">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-336">Scegliere **Applicazioni aziendali** dal menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-336">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-337">Fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-337">click **All applications**.</span></span>

6.  <span data-ttu-id="1d86e-338">Cercare l'applicazione desiderata, o a cui l'utente sta cercando di accedere, mediante il nome visualizzato o l'ID dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-338">Search for the application you are interested in, or the user is attempting to sign in to by application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="1d86e-339">Se l'applicazione che si sta cercando non è visualizzata, fare clic sul pulsante **Filtro** ed espandere l'ambito dell'elenco a **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-339">If you don’t see the application you are looking for, click the **Filter** button and expand the scope of the list to **All applications**.</span></span> <span data-ttu-id="1d86e-340">Se si desidera visualizzare più colonne, fare clic sul pulsante **Colonne** per aggiungere ulteriori dettagli per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1d86e-340">If you want to see more columns, click the **Columns** button to add additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="1d86e-341">Fare clic sulla voce di navigazione **Accesso condizionale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-341">click the **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="1d86e-342">Fare clic sul criterio che si desidera controllare.</span><span class="sxs-lookup"><span data-stu-id="1d86e-342">click the policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="1d86e-343">Verificare che non vi siano condizioni specifiche, assegnazioni o altre impostazioni che possano bloccare l'accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1d86e-343">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="1d86e-344">Può essere opportuno disabilitare temporaneamente questo criterio per assicurarsi che non impedisca gli accessi.</span><span class="sxs-lookup"><span data-stu-id="1d86e-344">You may wish to temporarily disable this policy to ensure it is not affecting sign ins.</span></span> <span data-ttu-id="1d86e-345">A tale scopo, impostare **Abilita criterio** su **No** e fare clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-345">To do this, set the **Enable policy** toggle to **No** and click the **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="1d86e-346">Disabilitare un criterio di accesso condizionale specifico</span><span class="sxs-lookup"><span data-stu-id="1d86e-346">Disable a specific conditional access policy</span></span>

<span data-ttu-id="1d86e-347">Per verificare o convalidare un singolo criterio di accesso condizionale:</span><span class="sxs-lookup"><span data-stu-id="1d86e-347">To check or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="1d86e-348">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-348">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1d86e-349">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d86e-349">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d86e-350">Digitare **"Azure Active Directory"** nella casella di ricerca del filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-350">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d86e-351">Scegliere **Applicazioni aziendali** dal menu di navigazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-351">click **Enterprise applications** in the navigation menu.</span></span>

5.  <span data-ttu-id="1d86e-352">Fare clic sulla voce di navigazione **Accesso condizionale**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-352">click the **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="1d86e-353">Fare clic sul criterio che si desidera controllare.</span><span class="sxs-lookup"><span data-stu-id="1d86e-353">click the policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="1d86e-354">Disabilitare il criterio impostando **Abilita criterio** su **No** e facendo clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-354">Disable the policy by setting the **Enable policy** toggle to **No** and click the **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="1d86e-355">Problemi relativi al consenso dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="1d86e-355">Problems with application consent</span></span>

<span data-ttu-id="1d86e-356">L'accesso all'applicazione può essere bloccato poiché non è stata eseguita l'operazione appropriata per consenso delle autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="1d86e-356">Application access can be blocked because the proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="1d86e-357">Di seguito sono riportate alcune soluzioni per i problemi relativi al consenso dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="1d86e-357">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="1d86e-358">Eseguire un'operazione di consenso a livello di utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-358">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="1d86e-359">Eseguire un'operazione di consenso a livello di amministratore per qualsiasi applicazione</span><span class="sxs-lookup"><span data-stu-id="1d86e-359">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="1d86e-360">Eseguire un'operazione di consenso a livello di amministratore per un'applicazione a tenant singolo</span><span class="sxs-lookup"><span data-stu-id="1d86e-360">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="1d86e-361">Eseguire un'operazione di consenso a livello di amministratore per un'applicazione multi-tenant</span><span class="sxs-lookup"><span data-stu-id="1d86e-361">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="1d86e-362">Eseguire un'operazione di consenso a livello di utente</span><span class="sxs-lookup"><span data-stu-id="1d86e-362">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="1d86e-363">Per qualsiasi applicazione abilitata a OpenID Connect che richiede le autorizzazioni, lo spostamento sulla schermata di accesso rappresenta un consenso a livello di utente all'applicazione per l'utente connesso.</span><span class="sxs-lookup"><span data-stu-id="1d86e-363">For any Open ID Connect-enabled application that requests permissions, navigating to the application’s sign in screen performs a user level consent to the application for the signed-in user.</span></span>

-   <span data-ttu-id="1d86e-364">Se si desidera eseguire questa operazione a livello di codice, vedere [Richiesta di consenso per un singolo utente](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span><span class="sxs-lookup"><span data-stu-id="1d86e-364">If you wish to do this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="1d86e-365">Eseguire un'operazione di consenso a livello di amministratore per qualsiasi applicazione</span><span class="sxs-lookup"><span data-stu-id="1d86e-365">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="1d86e-366">**Solo per le applicazioni sviluppate usando il modello di applicazione V1**, è possibile imporre questo consenso a livello di amministratore aggiungendo "**?prompt=admin\_consent**" alla fine dell'URL di accesso di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1d86e-366">For **only applications developed using the V1 application model**, you can force this administrator level consent to occur by adding “**?prompt=admin\_consent**” to the end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="1d86e-367">Per **qualsiasi applicazione sviluppata usando il modello di applicazione V2**, è possibile applicare questo consenso a livello di amministratore attenendosi alle istruzioni riportate nella sezione **Richiedere le autorizzazioni da un amministratore di directory** di [Uso dell'endpoint di consenso dell'amministratore](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="1d86e-367">For **any application developed using the V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="1d86e-368">Eseguire un'operazione di consenso a livello di amministratore per un'applicazione a tenant singolo</span><span class="sxs-lookup"><span data-stu-id="1d86e-368">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="1d86e-369">Per le **applicazioni a tenant singolo** che richiedono autorizzazioni (ad esempio quelle sviluppate internamente o di proprietà della propria organizzazione), è possibile eseguire un'operazione di **consenso a livello di amministratore** per conto di tutti gli utenti accedendo come amministratore globale e facendo clic sul pulsante **Concedi autorizzazioni** nella parte superiore del pannello **Registro applicazioni -&gt; Tutte le applicazioni -&gt; Seleziona un'app -&gt; Autorizzazioni necessarie**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-369">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on the **Grant permissions** button at the top of the **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="1d86e-370">Per **qualsiasi applicazione sviluppata usando il modello di applicazione V1 o V2**, è possibile applicare questo consenso a livello di amministratore attenendosi alle istruzioni riportate nella sezione **Richiedere le autorizzazioni da un amministratore di directory** di [Uso dell'endpoint di consenso dell'amministratore](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="1d86e-370">For **any application developed using the V1 or V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="1d86e-371">Eseguire un'operazione di consenso a livello di amministratore per un'applicazione multi-tenant</span><span class="sxs-lookup"><span data-stu-id="1d86e-371">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="1d86e-372">Per le **applicazioni multi-tenant** che richiedono autorizzazioni (ad esempio un'applicazione sviluppata da terza parte o da Microsoft), è possibile eseguire un'operazione di **consenso a livello di amministratore**.</span><span class="sxs-lookup"><span data-stu-id="1d86e-372">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="1d86e-373">Accedere come amministratore globale e fare clic sul pulsante **Concedi autorizzazioni** nel pannello **Applicazioni aziendali -&gt; Tutte le applicazioni -&gt; Seleziona un'app -&gt; Autorizzazioni** (presto disponibile).</span><span class="sxs-lookup"><span data-stu-id="1d86e-373">Sign in as a Global Administrator and clicking on the **Grant permissions** button under the **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="1d86e-374">È anche possibile applicare questo consenso a livello di amministratore attenendosi alle istruzioni riportate nella sezione **Richiedere le autorizzazioni da un amministratore di directory** di [Uso dell'endpoint di consenso dell'amministratore](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="1d86e-374">You can also enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d86e-375">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1d86e-375">Next steps</span></span>
[<span data-ttu-id="1d86e-376">Uso dell'endpoint di consenso dell'amministratore</span><span class="sxs-lookup"><span data-stu-id="1d86e-376">Using the admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

