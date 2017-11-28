---
title: accesso tooa applicazione Microsoft aaaProblems | Documenti Microsoft
description: Risolvere i problemi comuni legati all'accesso toofirst parti Microsoft Applications mediante Azure AD (ad esempio Office 365)
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
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a><span data-ttu-id="26b56-103">Problemi durante l'accesso tooa applicazione Microsoft</span><span class="sxs-lookup"><span data-stu-id="26b56-103">Problems signing in tooa Microsoft application</span></span>

<span data-ttu-id="26b56-104">Le applicazioni Microsoft (ad esempio Office 365 Exchange, SharePoint, Yammer e così via) vengono assegnate e gestite in modo leggermente diverso dalle applicazioni SaaS di terza parte o da altre applicazioni che si integrano con Azure AD per Single Sign On.</span><span class="sxs-lookup"><span data-stu-id="26b56-104">Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.</span></span>

<span data-ttu-id="26b56-105">Esistono tre modi principali che un utente può ottenere accesso tooa applicazione Microsoft pubblicato.</span><span class="sxs-lookup"><span data-stu-id="26b56-105">There are three main ways that a user can get access tooa Microsoft-published application.</span></span>

-   <span data-ttu-id="26b56-106">Per le applicazioni di Office 365 hello o altri gruppi a pagamento, gli utenti hanno accesso tramite **assegnazione delle licenze** entrambi direttamente tootheir account utente o tramite un gruppo utilizzando la funzionalità di assegnazione in base al gruppo di licenze.</span><span class="sxs-lookup"><span data-stu-id="26b56-106">For applications in hello Office 365 or other paid suites, users are granted access through **license assignment** either directly tootheir user account, or through a group using our group-based license assignment capability.</span></span>

-   <span data-ttu-id="26b56-107">Per le applicazioni di Microsoft o una terza parte pubblica liberamente per chiunque toouse, gli utenti possono essere concesso l'accesso tramite **il consenso dell'utente**.</span><span class="sxs-lookup"><span data-stu-id="26b56-107">For applications that Microsoft or a Third Party publishes freely for anyone toouse, users may be granted access through **user consent**.</span></span> <span data-ttu-id="26b56-108">This0 significa che toohello applicazione con il proprio account Azure Active Directory aziendale o dell'istituto di istruzione di accesso e che consentono di set di toohave accesso toosome limitata di dati al proprio account.</span><span class="sxs-lookup"><span data-stu-id="26b56-108">This0 means that they sign in toohello application with their Azure AD Work or School account and allow it toohave access toosome limited set of data on their account.</span></span>

-   <span data-ttu-id="26b56-109">Per le applicazioni di Microsoft o un 3rd Party pubblica liberamente per chiunque toouse, gli utenti possono inoltre essere concesso l'accesso tramite **il consenso dell'amministratore**.</span><span class="sxs-lookup"><span data-stu-id="26b56-109">For applications that Microsoft or a 3rd Party publishes freely for anyone toouse, users may also be granted access through **administrator consent**.</span></span> <span data-ttu-id="26b56-110">Ciò significa che un amministratore ha determinato l'applicazione hello può essere utilizzata da tutti gli utenti nell'organizzazione di hello, in modo toohello applicazione con un account amministratore globale di accesso e concedere l'accesso tooeveryone organizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-110">This means that an administrator has determined hello application may be used by everyone in hello organization, so they sign in toohello application with a Global Administrator account and grant access tooeveryone in hello organization.</span></span>

<span data-ttu-id="26b56-111">tootroubleshoot il problema, iniziare con hello [aree problematiche generali con accesso all'applicazione tooconsider](#general-problem-areas-with-application-access-to-consider) e quindi leggere hello [procedura dettagliata: passaggi tootroubleshoot accesso di Microsoft Application](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget i dettagli di hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-111">tootroubleshoot your issue, start with hello [General Problem Areas with Application Access tooconsider](#general-problem-areas-with-application-access-to-consider) and then read hello [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget into hello details.</span></span>

## <a name="general-problem-areas-with-application-access-tooconsider"></a><span data-ttu-id="26b56-112">Aree problematiche generali con accesso all'applicazione tooconsider</span><span class="sxs-lookup"><span data-stu-id="26b56-112">General Problem Areas with Application Access tooconsider</span></span>

<span data-ttu-id="26b56-113">Di seguito è riportato un elenco di hello aree di problemi generali che è possibile analizzare se si dispone di un'idea di dove toostart, ma è consigliabile leggere hello procedura dettagliata tooget passare rapidamente: [procedura dettagliata: passaggi tootroubleshoot accesso di Microsoft Application](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span><span class="sxs-lookup"><span data-stu-id="26b56-113">Below is a list of hello general problem areas that you can drill into if you have an idea of where toostart, but we recommend you read hello walkthrough tooget going quickly: [Walkthrough: Steps tootroubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).</span></span>

-   [<span data-ttu-id="26b56-114">Problemi con l'account dell'utente hello</span><span class="sxs-lookup"><span data-stu-id="26b56-114">Problems with hello user’s account</span></span>](#problems-with-the-users-account)

-   [<span data-ttu-id="26b56-115">Problemi relativi ai gruppi</span><span class="sxs-lookup"><span data-stu-id="26b56-115">Problems with groups</span></span>](#problems-with-groups)

-   [<span data-ttu-id="26b56-116">Problemi relativi ai criteri di accesso condizionale</span><span class="sxs-lookup"><span data-stu-id="26b56-116">Problems with conditional access policies</span></span>](#problems-with-conditional-access-policies)

-   [<span data-ttu-id="26b56-117">Problemi relativi al consenso dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="26b56-117">Problems with application consent</span></span>](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a><span data-ttu-id="26b56-118">Passaggi tootroubleshoot accesso di Microsoft Application</span><span class="sxs-lookup"><span data-stu-id="26b56-118">Steps tootroubleshoot Microsoft Application access</span></span>

<span data-ttu-id="26b56-119">Di seguito sono alcuni problemi comuni eseguire in quando gli utenti possono accedere tooa applicazione Microsoft.</span><span class="sxs-lookup"><span data-stu-id="26b56-119">Below are some common issues folks run into when their users cannot sign in tooa Microsoft application.</span></span>

-   <span data-ttu-id="26b56-120">Generale problemi toocheck prima</span><span class="sxs-lookup"><span data-stu-id="26b56-120">General issues toocheck first</span></span>

  * <span data-ttu-id="26b56-121">Verificare che l'utente hello accede toohello **correggere URL** e non è un URL dell'applicazione locale.</span><span class="sxs-lookup"><span data-stu-id="26b56-121">Make sure hello user is signing in toohello **correct URL** and not a local application URL.</span></span>

  * <span data-ttu-id="26b56-122">Verificare che l'account dell'utente hello è **non bloccato.**</span><span class="sxs-lookup"><span data-stu-id="26b56-122">Make sure hello user’s account is **not locked out.**</span></span>

  * <span data-ttu-id="26b56-123">Verificare che hello **account utente esista** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="26b56-123">Make sure hello **user’s account exists** in Azure Active Directory.</span></span> [<span data-ttu-id="26b56-124">Controllare se esiste un account utente in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26b56-124">Check if a user account exists in Azure Active Directory</span></span>](#problems-with-the-users-account)

  * <span data-ttu-id="26b56-125">Verificare che l'account dell'utente hello è **abilitato** per accessi. [Controllare lo stato dell'account di un utente](#problems-with-the-users-account)</span><span class="sxs-lookup"><span data-stu-id="26b56-125">Make sure hello user’s account is **enabled** for sign ins. [Check a user’s account status](#problems-with-the-users-account)</span></span>

  * <span data-ttu-id="26b56-126">Assicurarsi che utente hello **password non è scaduta o è stata dimenticata.**</span><span class="sxs-lookup"><span data-stu-id="26b56-126">Make sure hello user’s **password is not expired or forgotten.**</span></span> <span data-ttu-id="26b56-127">[Reimpostare la password di un utente](#reset-a-users-password) o [Abilitare la reimpostazione self-service delle password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span><span class="sxs-lookup"><span data-stu-id="26b56-127">[Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)</span></span>

   * <span data-ttu-id="26b56-128">Verificare che **Multi-Factor Authentication** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="26b56-128">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span> <span data-ttu-id="26b56-129">[Controllare lo stato di autenticazione a più fattori di un utente](#check-a-users-multi-factor-authentication-status) o [Controllare le informazioni di contatto per l'autenticazione di un utente](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="26b56-129">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

   * <span data-ttu-id="26b56-130">Verificare che un criterio di **accesso condizionale** o di **protezione delle identità** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="26b56-130">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span> <span data-ttu-id="26b56-131">[Controllare un criterio specifico di accesso condizionale](#problems-with-conditional-access-policies), [Controllare i criteri di accesso condizionale di un'applicazione specifica](#check-a-specific-applications-conditional-access-policy) o [Disabilitare un criterio specifico di accesso condizionale](#disable-a-specific-conditional-access-policy)</span><span class="sxs-lookup"><span data-stu-id="26b56-131">[Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)</span></span>

   * <span data-ttu-id="26b56-132">Assicurarsi che un utente **informazioni di contatto autenticazione** è toodate tooallow multi-Factor Authentication o l'accesso condizionale criteri toobe applicata.</span><span class="sxs-lookup"><span data-stu-id="26b56-132">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span> <span data-ttu-id="26b56-133">[Controllare lo stato di autenticazione a più fattori di un utente](#check-a-users-multi-factor-authentication-status) o [Controllare le informazioni di contatto per l'autenticazione di un utente](#check-a-users-authentication-contact-info)</span><span class="sxs-lookup"><span data-stu-id="26b56-133">[Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)</span></span>

-   <span data-ttu-id="26b56-134">Per **Microsoft** **le applicazioni che richiedono una licenza** (ad esempio Office 365), ecco alcuni problemi specifici di toocheck dopo aver escluso problemi generali hello precedenti:</span><span class="sxs-lookup"><span data-stu-id="26b56-134">For **Microsoft** **applications that require a license** (like Office365), here are some specific issues toocheck once you have ruled out hello general issues above:</span></span>

   * <span data-ttu-id="26b56-135">Garantire hello utente o ha un **assegnata una licenza.**</span><span class="sxs-lookup"><span data-stu-id="26b56-135">Ensure hello user or has a **license assigned.**</span></span> <span data-ttu-id="26b56-136">[Controllare le licenze assegnate a un utente](#check-a-users-assigned-licenses) o [Controllare le licenze assegnate a un gruppo](#check-a-groups-assigned-licenses)</span><span class="sxs-lookup"><span data-stu-id="26b56-136">[Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)</span></span>

   * <span data-ttu-id="26b56-137">Se la licenza hello **assegnato tooa** **gruppo statico**, verificare che hello **utente è membro** di tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="26b56-137">If hello license is **assigned tooa** **static group**, ensure that hello **user is a member** of that group.</span></span> [<span data-ttu-id="26b56-138">Controllare le appartenenze ai gruppi di un utente </span><span class="sxs-lookup"><span data-stu-id="26b56-138">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   * <span data-ttu-id="26b56-139">Se la licenza hello **assegnato tooa** **gruppo dinamico**, verificare che hello **regola gruppo dinamico è impostato correttamente**.</span><span class="sxs-lookup"><span data-stu-id="26b56-139">If hello license is **assigned tooa** **dynamic group**, ensure that hello **dynamic group rule is set correctly**.</span></span> [<span data-ttu-id="26b56-140">Controllare i criteri di appartenenza di un gruppo dinamico</span><span class="sxs-lookup"><span data-stu-id="26b56-140">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

   * <span data-ttu-id="26b56-141">Se la licenza hello **assegnato tooa** **gruppo dinamico**, assicurarsi che il gruppo dinamico hello include **al termine dell'elaborazione** l'appartenenza e tale hello **utente è un membro** (può richiedere del tempo).</span><span class="sxs-lookup"><span data-stu-id="26b56-141">If hello license is **assigned tooa** **dynamic group**, ensure that hello dynamic group has **finished processing** its membership and that hello **user is a member** (this can take some time).</span></span> [<span data-ttu-id="26b56-142">Controllare le appartenenze ai gruppi di un utente </span><span class="sxs-lookup"><span data-stu-id="26b56-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

   *  <span data-ttu-id="26b56-143">Una volta che viene assegnata la licenza hello, assicurarsi che la licenza hello è **non scaduto**.</span><span class="sxs-lookup"><span data-stu-id="26b56-143">Once you make sure hello license is assigned, make sure hello license is **not expired**.</span></span>

   *  <span data-ttu-id="26b56-144">Verificare che la licenza hello è **per un'applicazione hello** a cui accedono.</span><span class="sxs-lookup"><span data-stu-id="26b56-144">Make sure hello license is **for hello application** they are accessing.</span></span>

-   <span data-ttu-id="26b56-145">Per **Microsoft** **applicazioni che non richiedono una licenza**, ecco alcuni altri aspetti toocheck:</span><span class="sxs-lookup"><span data-stu-id="26b56-145">For **Microsoft** **applications that don’t require a license**, here are some other things toocheck:</span></span>

   * <span data-ttu-id="26b56-146">Se è richiesta l'applicazione hello **autorizzazioni a livello utente** (ad esempio "accedere a questa cassetta postale"), assicurarsi che l'utente hello ha effettuato l'accesso dell'applicazione toohello e ha eseguito un **operazione utente a livello di consenso**  toolet un'applicazione hello di accedere ai propri dati.</span><span class="sxs-lookup"><span data-stu-id="26b56-146">If hello application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that hello user has signed in toohello application and has performed a **user-level consent operation** toolet hello application access her data.</span></span>

   * <span data-ttu-id="26b56-147">Se è richiesta l'applicazione hello **le autorizzazioni a livello di amministratore** (ad esempio "accedere a postali di utenti tutte le cassette"), assicurarsi che un amministratore globale ha eseguito un **operazione consenso a livello di amministratore in per conto di tutti gli utenti** organizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-147">If hello application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in hello organization.</span></span>

## <a name="problems-with-hello-users-account"></a><span data-ttu-id="26b56-148">Problemi con l'account dell'utente hello</span><span class="sxs-lookup"><span data-stu-id="26b56-148">Problems with hello user’s account</span></span>

<span data-ttu-id="26b56-149">È possibile bloccare l'accesso all'applicazione a causa di problemi tooa a un utente assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="26b56-149">Application access can be blocked due tooa problem with a user that is assigned toohello application.</span></span> <span data-ttu-id="26b56-150">Di seguito sono riportate alcune soluzioni per i problemi relativi agli utenti e alle impostazioni degli account:</span><span class="sxs-lookup"><span data-stu-id="26b56-150">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="26b56-151">Controllare se esiste un account utente in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26b56-151">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="26b56-152">Controllare lo stato dell'account di un utente</span><span class="sxs-lookup"><span data-stu-id="26b56-152">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="26b56-153">Reimpostare la password di un utente</span><span class="sxs-lookup"><span data-stu-id="26b56-153">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="26b56-154">Abilitare la reimpostazione self-service delle password</span><span class="sxs-lookup"><span data-stu-id="26b56-154">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="26b56-155">Controllare lo stato di autenticazione a più fattori di un utente</span><span class="sxs-lookup"><span data-stu-id="26b56-155">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="26b56-156">Controllare le informazioni di contatto per l'autenticazione di un utente</span><span class="sxs-lookup"><span data-stu-id="26b56-156">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="26b56-157">Controllare le appartenenze ai gruppi di un utente </span><span class="sxs-lookup"><span data-stu-id="26b56-157">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="26b56-158">Controllare le licenze assegnate di un utente</span><span class="sxs-lookup"><span data-stu-id="26b56-158">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="26b56-159">Assegnare una licenza a un utente</span><span class="sxs-lookup"><span data-stu-id="26b56-159">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="26b56-160">Controllare se esiste un account utente in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26b56-160">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="26b56-161">Se è presente, un account utente di toocheck procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="26b56-161">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="26b56-162">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-162">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-163">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-163">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-164">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-164">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-165">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-165">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-166">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="26b56-166">click **All users**.</span></span>

6.  <span data-ttu-id="26b56-167">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="26b56-167">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="26b56-168">Controllare la proprietà hello di hello utente oggetto toobe assicurarsi che vengano visualizzate come previsto e che nessun dato è manca.</span><span class="sxs-lookup"><span data-stu-id="26b56-168">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="26b56-169">Controllare lo stato dell'account di un utente</span><span class="sxs-lookup"><span data-stu-id="26b56-169">Check a user’s account status</span></span>

<span data-ttu-id="26b56-170">di toocheck un utente stato dell'account, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="26b56-170">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="26b56-171">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-171">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-172">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-172">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-173">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-173">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-174">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-174">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-175">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="26b56-175">click **All users**.</span></span>

6.  <span data-ttu-id="26b56-176">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="26b56-176">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="26b56-177">Fare clic su **Profilo**.</span><span class="sxs-lookup"><span data-stu-id="26b56-177">click **Profile**.</span></span>

8.  <span data-ttu-id="26b56-178">In **impostazioni** assicurarsi che **blocco Accedi** è troppo**n**.</span><span class="sxs-lookup"><span data-stu-id="26b56-178">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="26b56-179">Reimpostare la password di un utente</span><span class="sxs-lookup"><span data-stu-id="26b56-179">Reset a user’s password</span></span>

<span data-ttu-id="26b56-180">tooreset una password, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="26b56-180">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="26b56-181">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-181">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-182">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-182">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-183">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-183">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-184">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-184">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-185">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="26b56-185">click **All users**.</span></span>

6.  <span data-ttu-id="26b56-186">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="26b56-186">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="26b56-187">Fare clic su hello **reimpostazione password** pulsante nella parte superiore di hello del Pannello di utente hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-187">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="26b56-188">Fare clic su hello **reimpostazione password** pulsante hello **reimpostazione password** pannello visualizzato.</span><span class="sxs-lookup"><span data-stu-id="26b56-188">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="26b56-189">Hello copia **password temporanea** o **immettere una nuova password** per utente hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-189">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="26b56-190">Comunicare il nuovo utente toohello password, essere necessario toochange questa password durante il successivo accesso tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="26b56-190">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="26b56-191">Abilitare la reimpostazione self-service delle password</span><span class="sxs-lookup"><span data-stu-id="26b56-191">Enable self-service password reset</span></span>

<span data-ttu-id="26b56-192">password self-service tooenable reimpostare, attenersi alla procedura di distribuzione hello seguente:</span><span class="sxs-lookup"><span data-stu-id="26b56-192">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="26b56-193">Abilitare gli utenti tooreset le password di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26b56-193">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="26b56-194">Abilitare gli utenti tooreset o modificare le password di Active Directory locale</span><span class="sxs-lookup"><span data-stu-id="26b56-194">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="26b56-195">Controllare lo stato di autenticazione a più fattori di un utente</span><span class="sxs-lookup"><span data-stu-id="26b56-195">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="26b56-196">toocheck un utente di multi-factor lo stato di autenticazione, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="26b56-196">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="26b56-197">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-197">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-198">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-198">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-199">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-199">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-200">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-200">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-201">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="26b56-201">click **All users**.</span></span>

6.  <span data-ttu-id="26b56-202">Fare clic su hello **multi-Factor Authentication** pulsante nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-202">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="26b56-203">Una volta hello **portale di amministrazione di multi-Factor Authentication** carichi, verificare che trovano in hello **utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="26b56-203">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="26b56-204">Trovare utente hello elenco hello degli utenti, la ricerca, filtro o l'ordinamento.</span><span class="sxs-lookup"><span data-stu-id="26b56-204">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="26b56-205">Utente selezionare hello hello elenco di utenti e **abilitare**, **disabilitare**, o **Imponi** autenticazione a più fattori in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="26b56-205">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

  * <span data-ttu-id="26b56-206">**Nota**: se un utente si trova in un **applicato** stato, è possibile impostarle troppo**disabilitato** temporaneamente toolet li nuovamente nel proprio account.</span><span class="sxs-lookup"><span data-stu-id="26b56-206">**Note**: If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="26b56-207">Una volta in, è possibile modificare il proprio stato troppo**abilitato** nuovamente toorequire li toore la registrazione di informazioni sul contatto durante il successivo accesso.</span><span class="sxs-lookup"><span data-stu-id="26b56-207">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="26b56-208">In alternativa, è possibile seguire i passaggi hello hello [informazioni di contatto di autenticazione dell'utente di controllare](#check-a-users-authentication-contact-info) tooverify o set di dati per loro.</span><span class="sxs-lookup"><span data-stu-id="26b56-208">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="26b56-209">Controllare le informazioni di contatto per l'autenticazione di un utente</span><span class="sxs-lookup"><span data-stu-id="26b56-209">Check a user’s authentication contact info</span></span>

<span data-ttu-id="26b56-210">informazioni utilizzate per multi-factor authentication, l'accesso condizionale, la protezione dell'identità e la reimpostazione della Password, contattare l'autenticazione dell'utente toocheck procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="26b56-210">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="26b56-211">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-211">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-212">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-212">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-213">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-213">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-214">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-214">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-215">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="26b56-215">click **All users**.</span></span>

6.  <span data-ttu-id="26b56-216">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="26b56-216">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="26b56-217">Fare clic su **Profilo**.</span><span class="sxs-lookup"><span data-stu-id="26b56-217">click **Profile**.</span></span>

8.  <span data-ttu-id="26b56-218">Scorrere verso il basso troppo**informazioni di contatto autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="26b56-218">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="26b56-219">**Revisione** dati hello registrati per utente hello e aggiornare in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="26b56-219">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="26b56-220">Controllare le appartenenze a gruppi dell'utente</span><span class="sxs-lookup"><span data-stu-id="26b56-220">Check a user’s group memberships</span></span>

<span data-ttu-id="26b56-221">di toocheck un utente appartenenza ai gruppi, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="26b56-221">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="26b56-222">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-222">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-223">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-223">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-224">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-224">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-225">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-225">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-226">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="26b56-226">click **All users**.</span></span>

6.  <span data-ttu-id="26b56-227">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="26b56-227">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="26b56-228">Fare clic su **gruppi** toosee gruppi utente hello è membro.</span><span class="sxs-lookup"><span data-stu-id="26b56-228">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="26b56-229">Controllare le licenze assegnate di un utente</span><span class="sxs-lookup"><span data-stu-id="26b56-229">Check a user’s assigned licenses</span></span>

<span data-ttu-id="26b56-230">toocheck un utente assegnate le licenze, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="26b56-230">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="26b56-231">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-231">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-232">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-232">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-233">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-233">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-234">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-234">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-235">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="26b56-235">click **All users**.</span></span>

6.  <span data-ttu-id="26b56-236">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="26b56-236">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="26b56-237">Fare clic su **licenze** toosee utente hello licenze è attualmente assegnato.</span><span class="sxs-lookup"><span data-stu-id="26b56-237">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="26b56-238">Assegnare una licenza a un utente</span><span class="sxs-lookup"><span data-stu-id="26b56-238">Assign a user a license</span></span> 

<span data-ttu-id="26b56-239">un utente, tooa licenza tooassign procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="26b56-239">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="26b56-240">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-240">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-241">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-241">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-242">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-242">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-243">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-243">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-244">Fare clic su **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="26b56-244">click **All users**.</span></span>

6.  <span data-ttu-id="26b56-245">**Ricerca** per utente hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="26b56-245">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="26b56-246">Fare clic su **licenze** toosee utente hello licenze è attualmente assegnato.</span><span class="sxs-lookup"><span data-stu-id="26b56-246">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="26b56-247">Fare clic su hello **assegnare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="26b56-247">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="26b56-248">Selezionare **uno o più prodotti** dall'elenco di hello dei prodotti disponibili.</span><span class="sxs-lookup"><span data-stu-id="26b56-248">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="26b56-249">**Parametro facoltativo** fare clic su hello **opzioni assegnazione** toogranularly elemento assegnare i prodotti.</span><span class="sxs-lookup"><span data-stu-id="26b56-249">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="26b56-250">Fare clic su **OK** al termine.</span><span class="sxs-lookup"><span data-stu-id="26b56-250">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="26b56-251">Fare clic su hello **assegnare** pulsante tooassign questi utente toothis licenze.</span><span class="sxs-lookup"><span data-stu-id="26b56-251">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-with-groups"></a><span data-ttu-id="26b56-252">Problemi relativi ai gruppi</span><span class="sxs-lookup"><span data-stu-id="26b56-252">Problems with groups</span></span>

<span data-ttu-id="26b56-253">Accesso all'applicazione può essere bloccata a causa di problemi tooa con un gruppo a cui è assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="26b56-253">Application access can be blocked due tooa problem with a group that is assigned toohello application.</span></span> <span data-ttu-id="26b56-254">Di seguito sono riportate alcune soluzioni per i problemi relativi a gruppi e ad appartenenze a gruppi:</span><span class="sxs-lookup"><span data-stu-id="26b56-254">Below are some ways you can troubleshoot and solve problems with groups and group memberships:</span></span>

-   [<span data-ttu-id="26b56-255">Controllare l'appartenenza di un gruppo</span><span class="sxs-lookup"><span data-stu-id="26b56-255">Check a group’s membership</span></span>](#check-a-groups-membership)

-   [<span data-ttu-id="26b56-256">Controllare i criteri di appartenenza di un gruppo dinamico</span><span class="sxs-lookup"><span data-stu-id="26b56-256">Check a dynamic group’s membership criteria</span></span>](#check-a-dynamic-groups-membership-criteria)

-   [<span data-ttu-id="26b56-257">Controllare le licenze assegnate di un gruppo</span><span class="sxs-lookup"><span data-stu-id="26b56-257">Check a group’s assigned licenses</span></span>](#check-a-groups-assigned-licenses)

-   [<span data-ttu-id="26b56-258">Rielaborare le licenze di un gruppo</span><span class="sxs-lookup"><span data-stu-id="26b56-258">Reprocess a group’s licenses</span></span>](#reprocess-a-groups-licenses)

-   [<span data-ttu-id="26b56-259">Assegnare una licenza a un gruppo</span><span class="sxs-lookup"><span data-stu-id="26b56-259">Assign a group a license</span></span>](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a><span data-ttu-id="26b56-260">Controllare l'appartenenza di un gruppo</span><span class="sxs-lookup"><span data-stu-id="26b56-260">Check a group’s membership</span></span>

<span data-ttu-id="26b56-261">toocheck appartenenza a un gruppo, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="26b56-261">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="26b56-262">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-262">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-263">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-263">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-264">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-264">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-265">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-265">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-266">Fare clic su **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="26b56-266">click **All groups**.</span></span>

6.  <span data-ttu-id="26b56-267">**Ricerca** per gruppo hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="26b56-267">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="26b56-268">Fare clic su **membri** elenco hello tooreview di utenti assegnati toothis gruppo.</span><span class="sxs-lookup"><span data-stu-id="26b56-268">click **Members** tooreview hello list of users assigned toothis group.</span></span>

### <a name="check-a-dynamic-groups-membership-criteria"></a><span data-ttu-id="26b56-269">Controllare i criteri di appartenenza di un gruppo dinamico</span><span class="sxs-lookup"><span data-stu-id="26b56-269">Check a dynamic group’s membership criteria</span></span> 

<span data-ttu-id="26b56-270">toocheck criteri di appartenenza del gruppo dinamico, seguire i passaggi di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="26b56-270">toocheck a dynamic group’s membership criteria, follow hello steps below:</span></span>

1.  <span data-ttu-id="26b56-271">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-271">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-272">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-272">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-273">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-273">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-274">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-274">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-275">Fare clic su **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="26b56-275">click **All groups**.</span></span>

6.  <span data-ttu-id="26b56-276">**Ricerca** per gruppo hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="26b56-276">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="26b56-277">Fare clic su **Regole di appartenenza dinamica**.</span><span class="sxs-lookup"><span data-stu-id="26b56-277">click **Dynamic membership rules.**</span></span>

8.  <span data-ttu-id="26b56-278">Hello revisione **semplice** o **avanzate** regola definita per questo gruppo e verificare che tale utente hello da toobe un membro di questo gruppo soddisfa questi criteri.</span><span class="sxs-lookup"><span data-stu-id="26b56-278">Review hello **simple** or **advanced** rule defined for this group and ensure that hello user you want toobe a member of this group meets these criteria.</span></span>

### <a name="check-a-groups-assigned-licenses"></a><span data-ttu-id="26b56-279">Controllare le licenze assegnate di un gruppo</span><span class="sxs-lookup"><span data-stu-id="26b56-279">Check a group’s assigned licenses</span></span>

<span data-ttu-id="26b56-280">toocheck un gruppo assegnate le licenze, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="26b56-280">toocheck a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="26b56-281">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-281">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-282">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-282">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-283">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-283">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-284">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-284">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-285">Fare clic su **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="26b56-285">click **All groups**.</span></span>

6.  <span data-ttu-id="26b56-286">**Ricerca** per gruppo hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="26b56-286">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="26b56-287">Fare clic su **licenze** toosee quale gruppo di licenze hello è attualmente assegnato.</span><span class="sxs-lookup"><span data-stu-id="26b56-287">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

### <a name="reprocess-a-groups-licenses"></a><span data-ttu-id="26b56-288">Rielaborare le licenze di un gruppo</span><span class="sxs-lookup"><span data-stu-id="26b56-288">Reprocess a group’s licenses</span></span>

<span data-ttu-id="26b56-289">tooreprocess un gruppo assegnate le licenze, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="26b56-289">tooreprocess a group’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="26b56-290">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-290">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-291">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-291">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-292">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-292">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-293">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-293">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-294">Fare clic su **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="26b56-294">click **All groups**.</span></span>

6.  <span data-ttu-id="26b56-295">**Ricerca** per gruppo hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="26b56-295">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="26b56-296">Fare clic su **licenze** toosee quale gruppo di licenze hello è attualmente assegnato.</span><span class="sxs-lookup"><span data-stu-id="26b56-296">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="26b56-297">Fare clic su hello **rielaborare** tooensure pulsante che i membri del gruppo di licenze assegnate toothis hello siano aggiornati.</span><span class="sxs-lookup"><span data-stu-id="26b56-297">click hello **Reprocess** button tooensure that hello licenses assigned toothis group’s members are up-to-date.</span></span> <span data-ttu-id="26b56-298">L'operazione potrebbe richiedere molto tempo, a seconda delle dimensioni di hello e la complessità del gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-298">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="26b56-299">toodo questo più velocemente, è consigliabile temporaneamente assegna una licenza toohello utente direttamente.</span><span class="sxs-lookup"><span data-stu-id="26b56-299">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="26b56-300">[Assegnare una licenza a un utente](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="26b56-300">[Assign a user a license](#problems-with-application-consent).</span></span>
   >
   >

### <a name="assign-a-group-a-license"></a><span data-ttu-id="26b56-301">Assegnare una licenza a un gruppo</span><span class="sxs-lookup"><span data-stu-id="26b56-301">Assign a group a license</span></span>

<span data-ttu-id="26b56-302">un gruppo di licenze tooa tooassign procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="26b56-302">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="26b56-303">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-303">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-304">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-304">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-305">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-305">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-306">Fare clic su **utenti e gruppi** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-306">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-307">Fare clic su **Tutti i gruppi**.</span><span class="sxs-lookup"><span data-stu-id="26b56-307">click **All groups**.</span></span>

6.  <span data-ttu-id="26b56-308">**Ricerca** per gruppo hello si è interessati e **fare clic sulla riga hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="26b56-308">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="26b56-309">Fare clic su **licenze** toosee quale gruppo di licenze hello è attualmente assegnato.</span><span class="sxs-lookup"><span data-stu-id="26b56-309">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="26b56-310">Fare clic su hello **assegnare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="26b56-310">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="26b56-311">Selezionare **uno o più prodotti** dall'elenco di hello dei prodotti disponibili.</span><span class="sxs-lookup"><span data-stu-id="26b56-311">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="26b56-312">**Parametro facoltativo** fare clic su hello **opzioni assegnazione** toogranularly elemento assegnare i prodotti.</span><span class="sxs-lookup"><span data-stu-id="26b56-312">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="26b56-313">Fare clic su **OK** al termine.</span><span class="sxs-lookup"><span data-stu-id="26b56-313">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="26b56-314">Fare clic su hello **assegnare** pulsante tooassign questi toothis di gruppo di licenze.</span><span class="sxs-lookup"><span data-stu-id="26b56-314">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="26b56-315">L'operazione potrebbe richiedere molto tempo, a seconda delle dimensioni di hello e la complessità del gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-315">This may take a long time, depending on hello size and complexity of hello group.</span></span>

   >[!NOTE]
   ><span data-ttu-id="26b56-316">toodo questo più velocemente, è consigliabile temporaneamente assegna una licenza toohello utente direttamente.</span><span class="sxs-lookup"><span data-stu-id="26b56-316">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> <span data-ttu-id="26b56-317">[Assegnare una licenza a un utente](#problems-with-application-consent).</span><span class="sxs-lookup"><span data-stu-id="26b56-317">[Assign a user a license](#problems-with-application-consent).</span></span>
   > 
   >

## <a name="problems-with-conditional-access-policies"></a><span data-ttu-id="26b56-318">Problemi relativi ai criteri di accesso condizionale</span><span class="sxs-lookup"><span data-stu-id="26b56-318">Problems with conditional access policies</span></span>

### <a name="check-a-specific-conditional-access-policy"></a><span data-ttu-id="26b56-319">Selezionare un criterio di accesso condizionale specifico</span><span class="sxs-lookup"><span data-stu-id="26b56-319">Check a specific conditional access policy</span></span>

<span data-ttu-id="26b56-320">toocheck o convalidare i criteri di accesso condizionale singolo:</span><span class="sxs-lookup"><span data-stu-id="26b56-320">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="26b56-321">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-321">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-322">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-322">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-323">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-323">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-324">Fare clic su **applicazioni aziendali** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-324">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-325">Fare clic su hello **accesso condizionale** elemento di navigazione.</span><span class="sxs-lookup"><span data-stu-id="26b56-325">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="26b56-326">Fare clic su criteri hello si è interessati nel controllo.</span><span class="sxs-lookup"><span data-stu-id="26b56-326">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="26b56-327">Verificare che non vi siano condizioni specifiche, assegnazioni o altre impostazioni che possano bloccare l'accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="26b56-327">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

   >[!NOTE]
   ><span data-ttu-id="26b56-328">È preferibile disabilitare tootemporarily tooensure questo criterio non influisce toodo aggiuntivi sign, hello set **abilitare i criteri di** attivare o disattivare troppo**n** e fare clic su hello **salvare** pulsante .</span><span class="sxs-lookup"><span data-stu-id="26b56-328">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a><span data-ttu-id="26b56-329">Controllare i criteri di accesso condizionale di un'applicazione specifica</span><span class="sxs-lookup"><span data-stu-id="26b56-329">Check a specific application’s conditional access policy</span></span>

<span data-ttu-id="26b56-330">toocheck o convalidare i criteri di accesso condizionale configurati un'unica applicazione:</span><span class="sxs-lookup"><span data-stu-id="26b56-330">toocheck or validate a single application’s currently configured conditional access policy:</span></span>

1.  <span data-ttu-id="26b56-331">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-331">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-332">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-332">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-333">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-333">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-334">Fare clic su **applicazioni aziendali** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-334">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-335">Fare clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="26b56-335">click **All applications**.</span></span>

6.  <span data-ttu-id="26b56-336">Ricerca per un'applicazione hello si è interessati o hello utente sta tentando di toosign nell'applicazione tooby visualizzare id nome o dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="26b56-336">Search for hello application you are interested in, or hello user is attempting toosign in tooby application display name or application id.</span></span>

     >[!NOTE]
     ><span data-ttu-id="26b56-337">Se un'applicazione hello si sta cercando non viene visualizzato, fare clic su hello **filtro** pulsante ed espandere ambito hello dell'elenco di hello troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="26b56-337">If you don’t see hello application you are looking for, click hello **Filter** button and expand hello scope of hello list too**All applications**.</span></span> <span data-ttu-id="26b56-338">Se si desidera toosee più colonne, fare clic su hello **colonne** pulsante tooadd dettagli aggiuntivi per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="26b56-338">If you want toosee more columns, click hello **Columns** button tooadd additional details for your applications.</span></span>
     >
     >

7.  <span data-ttu-id="26b56-339">Fare clic su hello **accesso condizionale** elemento di navigazione.</span><span class="sxs-lookup"><span data-stu-id="26b56-339">click hello **Conditional access** navigation item.</span></span>

8.  <span data-ttu-id="26b56-340">Fare clic su criteri hello si è interessati nel controllo.</span><span class="sxs-lookup"><span data-stu-id="26b56-340">click hello policy you are interested in inspecting.</span></span>

9.  <span data-ttu-id="26b56-341">Verificare che non vi siano condizioni specifiche, assegnazioni o altre impostazioni che possano bloccare l'accesso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="26b56-341">Review that there are no specific conditions, assignments, or other settings which may be blocking user access.</span></span>

     >[!NOTE]
     ><span data-ttu-id="26b56-342">È preferibile disabilitare tootemporarily tooensure questo criterio non influisce toodo aggiuntivi sign, hello set **abilitare i criteri di** attivare o disattivare troppo**n** e fare clic su hello **salvare** pulsante .</span><span class="sxs-lookup"><span data-stu-id="26b56-342">You may wish tootemporarily disable this policy tooensure it is not affecting sign ins. toodo this, set hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a><span data-ttu-id="26b56-343">Disabilitare un criterio di accesso condizionale specifico</span><span class="sxs-lookup"><span data-stu-id="26b56-343">Disable a specific conditional access policy</span></span>

<span data-ttu-id="26b56-344">toocheck o convalidare i criteri di accesso condizionale singolo:</span><span class="sxs-lookup"><span data-stu-id="26b56-344">toocheck or validate a single conditional access policy:</span></span>

1.  <span data-ttu-id="26b56-345">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="26b56-345">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="26b56-346">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-346">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="26b56-347">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="26b56-347">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="26b56-348">Fare clic su **applicazioni aziendali** nel menu di navigazione hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-348">click **Enterprise applications** in hello navigation menu.</span></span>

5.  <span data-ttu-id="26b56-349">Fare clic su hello **accesso condizionale** elemento di navigazione.</span><span class="sxs-lookup"><span data-stu-id="26b56-349">click hello **Conditional access** navigation item.</span></span>

6.  <span data-ttu-id="26b56-350">Fare clic su criteri hello si è interessati nel controllo.</span><span class="sxs-lookup"><span data-stu-id="26b56-350">click hello policy you are interested in inspecting.</span></span>

7.  <span data-ttu-id="26b56-351">Disattivare il criterio di hello impostazione hello **abilitare i criteri di** attivare o disattivare troppo**n** e fare clic su hello **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="26b56-351">Disable hello policy by setting hello **Enable policy** toggle too**No** and click hello **Save** button.</span></span>

## <a name="problems-with-application-consent"></a><span data-ttu-id="26b56-352">Problemi relativi al consenso dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="26b56-352">Problems with application consent</span></span>

<span data-ttu-id="26b56-353">È possibile bloccare l'accesso all'applicazione perché non si è verificata l'operazione di consenso hello delle autorizzazioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="26b56-353">Application access can be blocked because hello proper permissions consent operation has not occurred.</span></span> <span data-ttu-id="26b56-354">Di seguito sono riportate alcune soluzioni per i problemi relativi al consenso dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="26b56-354">Below are some ways you can troubleshoot and solve application consent issues:</span></span>

-   [<span data-ttu-id="26b56-355">Eseguire un'operazione di consenso a livello di utente</span><span class="sxs-lookup"><span data-stu-id="26b56-355">Perform a user-level consent operation</span></span>](#perform-a-user-level-consent-operation)

-   [<span data-ttu-id="26b56-356">Eseguire un'operazione di consenso a livello di amministratore per qualsiasi applicazione</span><span class="sxs-lookup"><span data-stu-id="26b56-356">Perform administrator-level consent operation for any application</span></span>](#perform-administrator-level-consent-operation-for-any-application)

-   [<span data-ttu-id="26b56-357">Eseguire un'operazione di consenso a livello di amministratore per un'applicazione a tenant singolo</span><span class="sxs-lookup"><span data-stu-id="26b56-357">Perform administrator-level consent for a single-tenant application</span></span>](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [<span data-ttu-id="26b56-358">Eseguire un'operazione di consenso a livello di amministratore per un'applicazione multi-tenant</span><span class="sxs-lookup"><span data-stu-id="26b56-358">Perform administrator-level consent for a multi-tenant application</span></span>](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a><span data-ttu-id="26b56-359">Eseguire un'operazione di consenso a livello di utente</span><span class="sxs-lookup"><span data-stu-id="26b56-359">Perform a user-level consent operation</span></span>

-   <span data-ttu-id="26b56-360">Per qualsiasi applicazione abilitata Open ID connessione che richiede autorizzazioni di accesso dell'applicazione toohello nella schermata di esplorazione esegue un'applicazione di toohello livello di consenso dell'utente per l'utente connesso di hello.</span><span class="sxs-lookup"><span data-stu-id="26b56-360">For any Open ID Connect-enabled application that requests permissions, navigating toohello application’s sign in screen performs a user level consent toohello application for hello signed-in user.</span></span>

-   <span data-ttu-id="26b56-361">Se si desidera toodo questo livello di codice, vedere [che richiede il consenso dell'utente singoli](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span><span class="sxs-lookup"><span data-stu-id="26b56-361">If you wish toodo this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).</span></span>

### <a name="perform-administrator-level-consent-operation-for-any-application"></a><span data-ttu-id="26b56-362">Eseguire un'operazione di consenso a livello di amministratore per qualsiasi applicazione</span><span class="sxs-lookup"><span data-stu-id="26b56-362">Perform administrator-level consent operation for any application</span></span>

-   <span data-ttu-id="26b56-363">Per **solo le applicazioni sviluppate utilizzando il modello di applicazione hello V1**, è possibile forzare questa toooccur di livello di consenso dell'utente amministratore aggiungendo "**? prompt = admin\_consenso**" toohello fine di un Nell'URL di accesso dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="26b56-363">For **only applications developed using hello V1 application model**, you can force this administrator level consent toooccur by adding “**?prompt=admin\_consent**” toohello end of an application’s sign in URL.</span></span>

-   <span data-ttu-id="26b56-364">Per **qualsiasi applicazione sviluppata utilizzando il modello di applicazione hello V2**, è possibile applicare questo toooccur amministratore a livello di consenso seguendo le istruzioni di hello in hello **richiedere le autorizzazioni di hello da una directory amministrazione** sezione [endpoint consenso dell'amministratore hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="26b56-364">For **any application developed using hello V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a><span data-ttu-id="26b56-365">Eseguire un'operazione di consenso a livello di amministratore per un'applicazione a tenant singolo</span><span class="sxs-lookup"><span data-stu-id="26b56-365">Perform administrator-level consent for a single-tenant application</span></span>

-   <span data-ttu-id="26b56-366">Per **applicazioni single-tenant** che non richiedono le autorizzazioni (ad esempio quelli di sviluppo o il proprietario dell'organizzazione), è possibile eseguire un **amministrative a livello di consenso** operazione per conto di tutti gli utenti di accedere come amministratore globale e facendo clic su hello **concedere le autorizzazioni** pulsante nella parte superiore di hello di hello **Registro di sistema -&gt; tutte le applicazioni -&gt; selezionare un'App: &gt; Autorizzazioni obbligatorie** blade.</span><span class="sxs-lookup"><span data-stu-id="26b56-366">For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on hello **Grant permissions** button at hello top of hello **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.</span></span>

-   <span data-ttu-id="26b56-367">Per **qualsiasi applicazione sviluppata utilizzando hello V1 o V2 applicazione**, è possibile applicare questo toooccur amministratore a livello di consenso seguendo le istruzioni di hello in hello **richiedere le autorizzazioni di hello da un l'amministratore di directory** sezione [endpoint consenso dell'amministratore hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="26b56-367">For **any application developed using hello V1 or V2 application model**, you can enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a><span data-ttu-id="26b56-368">Eseguire un'operazione di consenso a livello di amministratore per un'applicazione multi-tenant</span><span class="sxs-lookup"><span data-stu-id="26b56-368">Perform administrator-level consent for a multi-tenant application</span></span>

-   <span data-ttu-id="26b56-369">Per le **applicazioni multi-tenant** che richiedono autorizzazioni (ad esempio un'applicazione sviluppata da terza parte o da Microsoft), è possibile eseguire un'operazione di **consenso a livello di amministratore**.</span><span class="sxs-lookup"><span data-stu-id="26b56-369">For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation.</span></span> <span data-ttu-id="26b56-370">Accedere come amministratore globale e facendo clic su hello **concedere le autorizzazioni** pulsante sotto hello **applicazioni aziendali -&gt; tutte le applicazioni -&gt; selezionare un'App -&gt; Autorizzazioni** blade (disponibile non appena).</span><span class="sxs-lookup"><span data-stu-id="26b56-370">Sign in as a Global Administrator and clicking on hello **Grant permissions** button under hello **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).</span></span>

-   <span data-ttu-id="26b56-371">È inoltre possibile applicare questo toooccur amministratore a livello di consenso seguendo le istruzioni di hello in hello **richiedere le autorizzazioni di hello da un amministratore di directory** sezione [endpoint consenso dell'amministratore hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span><span class="sxs-lookup"><span data-stu-id="26b56-371">You can also enforce this administrator-level consent toooccur by following hello instructions under hello **Request hello permissions from a directory admin** section of [Using hello admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).</span></span>

## <a name="next-steps"></a><span data-ttu-id="26b56-372">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="26b56-372">Next steps</span></span>
[<span data-ttu-id="26b56-373">Hello endpoint consenso dell'amministratore</span><span class="sxs-lookup"><span data-stu-id="26b56-373">Using hello admin consent endpoint</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

