---
title: aaaHow tooconfigure password single sign-on per un applicationn non raccolta | Documenti Microsoft
description: "Come tooconfigure un'applicazione non raccolta personalizzata per proteggere basato su password single sign-on quando non è elencato nella raccolta di applicazioni Azure AD hello"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="a04a0-103">Come password tooconfigure single sign-on per un'applicazione non-raccolta</span><span class="sxs-lookup"><span data-stu-id="a04a0-103">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="a04a0-104">Inoltre scelte toohello trovato all'interno della raccolta applicazione hello Azure AD, è inoltre hello opzione tooadd un **applicazione non raccolta** quando un'applicazione hello desiderato non è elencata.</span><span class="sxs-lookup"><span data-stu-id="a04a0-104">In addition toohello choices found within hello Azure AD Application Gallery, you also have hello option tooadd a **non-gallery application** when hello application you want is not listed there.</span></span> <span data-ttu-id="a04a0-105">Mediante questa funzionalità, è possibile aggiungere qualsiasi applicazione che esiste già all'interno dell'organizzazione o in qualsiasi applicazione di terze parti che è possibile utilizzare da un fornitore che non fa già parte di hello [raccolta di applicazioni Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="a04a0-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="a04a0-106">Dopo aver aggiunto un'applicazione non raccolta, è quindi possibile configurare hello metodo Single sign-on questa applicazione usa selezionando hello **Single Sign-on** elemento di navigazione in un'applicazione aziendale in hello [portale di Azure ](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a04a0-106">Once you add a non-gallery application, you can then configure hello Single sign-on method this application uses by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="a04a0-107">Uno dei hello Single Sign-on metodi disponibili tooyou è hello [basato su Password Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opzione.</span><span class="sxs-lookup"><span data-stu-id="a04a0-107">One of hello Single Sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="a04a0-108">Con hello **aggiungere un'applicazione non raccolta** esperienza, è possibile integrare qualsiasi applicazione che esegue il rendering di un nome utente basato su HTML e la password anche se non è il set di applicazioni preintegrate campo, di input.</span><span class="sxs-lookup"><span data-stu-id="a04a0-108">With hello **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="a04a0-109">Hello questo procedimento funziona consiste in una pagina scraping tecnologia che fa parte di hello estensione del Pannello di accesso che consente di elaborare tooauto-rileva i campi di input nome utente e password, archiviarli in modo sicuro per l'istanza dell'applicazione specifici.</span><span class="sxs-lookup"><span data-stu-id="a04a0-109">hello way this works is by a page scraping technology that is part of hello Access Panel extension that allows us tooauto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="a04a0-110">Quindi riprodurre in modo sicuro i nomi utente e i campi di toothose password quando un utente si sposta toothat applicazioni nel Pannello di accesso dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a04a0-110">Then securely replay usernames and passwords toothose fields when a user navigates toothat application on hello application access panel.</span></span>

<span data-ttu-id="a04a0-111">Questo è un ottimo modo tooget avviato l'integrazione di qualsiasi tipo di applicazione in Azure AD rapidamente e consente di:</span><span class="sxs-lookup"><span data-stu-id="a04a0-111">This is a great way tooget started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="a04a0-112">Integrare **qualsiasi applicazione HelloWorld** con il tenant di Azure AD, purché il rendering di un nome utente e password campo di input HTML</span><span class="sxs-lookup"><span data-stu-id="a04a0-112">Integrate **any application in hello world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="a04a0-113">Abilitare **Single Sign-on per gli utenti** archiviandoli in modo sicuro e riproduzione di nomi utente e password per l'applicazione hello è stata integrata con Azure AD</span><span class="sxs-lookup"><span data-stu-id="a04a0-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="a04a0-114">**Rilevamento automatico di input** campi per qualsiasi applicazione e consentono di toomanually rilevare tali campi utilizzando hello estensione Browser del Pannello di accesso, nel caso in cui non viene trovato il rilevamento automatico</span><span class="sxs-lookup"><span data-stu-id="a04a0-114">**Auto-detect input** fields for any application and allow you toomanually detect those fields using hello Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="a04a0-115">**Supporto di applicazioni che richiedono più campi Accedi** per applicazioni che richiedono più di un semplice nome utente e password campi toosign in</span><span class="sxs-lookup"><span data-stu-id="a04a0-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="a04a0-116">**Personalizzare le etichette di hello** hello nome utente e password dei campi di input utente di vedere in hello [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) quando si immettono le proprie credenziali</span><span class="sxs-lookup"><span data-stu-id="a04a0-116">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="a04a0-117">Consenti il **utenti** tooprovide i propri nomi utente e password per tutti gli account esistenti dell'applicazione che sta digitando manualmente su hello [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="a04a0-117">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="a04a0-118">Consentire un **membro del gruppo aziendale hello** toospecify hello utente e password utente tooa da assegnato utilizzando hello [accesso all'applicazione Self-Service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) funzionalità</span><span class="sxs-lookup"><span data-stu-id="a04a0-118">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="a04a0-119">Consentire un **amministratore** funzionalità quando i nomi utente hello toospecify e le password assegnate tooa utente con credenziali di aggiornamento hello [l'assegnazione di un'applicazione tooan utente](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="a04a0-119">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="a04a0-120">Consentire un **amministratore** toospecify hello condiviso username o password utilizzata da un gruppo di persone con le credenziali di aggiornamento hello funzionalità quando [l'assegnazione di un'applicazione di gruppo tooan](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="a04a0-120">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="a04a0-121">Di seguito viene descritto come abilitare [basato su Password Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany applicazione aggiungere utilizzando hello **aggiungere un'applicazione non raccolta** esperienza.</span><span class="sxs-lookup"><span data-stu-id="a04a0-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany application that you add using hello **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="a04a0-122">Panoramica dei passaggi necessari</span><span class="sxs-lookup"><span data-stu-id="a04a0-122">Overview of steps required</span></span>

<span data-ttu-id="a04a0-123">un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:</span><span class="sxs-lookup"><span data-stu-id="a04a0-123">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="a04a0-124">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="a04a0-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="a04a0-125">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="a04a0-125">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="a04a0-126">Assegnare l'utente tooa dell'applicazione hello o un gruppo</span><span class="sxs-lookup"><span data-stu-id="a04a0-126">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="a04a0-127">Assegnare un'applicazione tooan utente direttamente</span><span class="sxs-lookup"><span data-stu-id="a04a0-127">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="a04a0-128">Assegnare un gruppo di applicazioni tooa direttamente</span><span class="sxs-lookup"><span data-stu-id="a04a0-128">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="a04a0-129">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="a04a0-129">Add a non-gallery application</span></span>

<span data-ttu-id="a04a0-130">un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="a04a0-130">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="a04a0-131">Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**</span><span class="sxs-lookup"><span data-stu-id="a04a0-131">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="a04a0-132">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="a04a0-132">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a04a0-133">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="a04a0-133">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a04a0-134">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a04a0-134">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a04a0-135">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** pannello</span><span class="sxs-lookup"><span data-stu-id="a04a0-135">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="a04a0-136">Fare clic su**Applicazione non nella raccolta**.</span><span class="sxs-lookup"><span data-stu-id="a04a0-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="a04a0-137">Immettere il nome di hello dell'applicazione in hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="a04a0-137">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="a04a0-138">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a04a0-138">Select **Add.**</span></span>

<span data-ttu-id="a04a0-139">Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.</span><span class="sxs-lookup"><span data-stu-id="a04a0-139">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="a04a0-140">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="a04a0-140">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="a04a0-141">tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="a04a0-141">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="a04a0-142">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="a04a0-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a04a0-143">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="a04a0-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a04a0-144">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="a04a0-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a04a0-145">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a04a0-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a04a0-146">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a04a0-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="a04a0-147">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="a04a0-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="a04a0-148">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a04a0-148">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="a04a0-149">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a04a0-149">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a04a0-150">Modalità di selezione hello **basato su Password Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="a04a0-150">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="a04a0-151">Immettere hello **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="a04a0-151">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="a04a0-152">Si tratta hello URL in cui gli utenti immettono il nome utente e password toosign in a.</span><span class="sxs-lookup"><span data-stu-id="a04a0-152">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="a04a0-153">Verificare i campi di accesso hello sono visibili nell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="a04a0-153">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="a04a0-154">Assegnare gli utenti dell'applicazione toohello.</span><span class="sxs-lookup"><span data-stu-id="a04a0-154">Assign users toohello application.</span></span>

11. <span data-ttu-id="a04a0-155">Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello.</span><span class="sxs-lookup"><span data-stu-id="a04a0-155">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="a04a0-156">In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.</span><span class="sxs-lookup"><span data-stu-id="a04a0-156">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="a04a0-157">Assegnare un'applicazione tooan utente direttamente</span><span class="sxs-lookup"><span data-stu-id="a04a0-157">Assign a user tooan application directly</span></span>

<span data-ttu-id="a04a0-158">tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="a04a0-158">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="a04a0-159">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="a04a0-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a04a0-160">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="a04a0-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a04a0-161">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="a04a0-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a04a0-162">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a04a0-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a04a0-163">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a04a0-163">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="a04a0-164">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="a04a0-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="a04a0-165">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="a04a0-165">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="a04a0-166">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a04a0-166">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a04a0-167">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="a04a0-167">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="a04a0-168">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="a04a0-168">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="a04a0-169">Tipo di hello **nome completo** o **indirizzo di posta elettronica** dell'utente hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="a04a0-169">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="a04a0-170">Passare il mouse su hello **utente** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="a04a0-170">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="a04a0-171">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello dell'utente il toohello utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="a04a0-171">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="a04a0-172">**Facoltativo:** se si desidera troppo**aggiungere più di un utente**, in un altro tipo di **nome completo** o **indirizzo di posta elettronica** in hello **Cerca per nome o l'indirizzo di posta elettronica** casella di ricerca e fare clic su questo toohello utente hello casella di controllo tooadd **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="a04a0-172">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="a04a0-173">Al termine della selezione utenti, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="a04a0-173">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="a04a0-174">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un ruolo tooassign toohello utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="a04a0-174">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="a04a0-175">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="a04a0-175">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="a04a0-176">Assegnare un gruppo di applicazioni tooa direttamente</span><span class="sxs-lookup"><span data-stu-id="a04a0-176">Assign an application tooa group directly</span></span>

<span data-ttu-id="a04a0-177">tooassign uno o più gruppi di applicazioni tooan direttamente, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="a04a0-177">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="a04a0-178">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="a04a0-178">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a04a0-179">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="a04a0-179">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a04a0-180">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="a04a0-180">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a04a0-181">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a04a0-181">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a04a0-182">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a04a0-182">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="a04a0-183">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="a04a0-183">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="a04a0-184">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="a04a0-184">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="a04a0-185">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a04a0-185">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a04a0-186">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="a04a0-186">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="a04a0-187">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="a04a0-187">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="a04a0-188">Tipo di hello **nome del gruppo completo** del gruppo di hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="a04a0-188">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="a04a0-189">Passare il mouse su hello **gruppo** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="a04a0-189">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="a04a0-190">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello del gruppo toohello l'utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="a04a0-190">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="a04a0-191">**Facoltativo:** se si desidera troppo**aggiungere più di un gruppo**, in un altro tipo di **nome del gruppo completo** in hello **ricerca per nome o indirizzo di posta** casella di ricerca Fare clic su hello casella di controllo tooadd toohello questo gruppo **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="a04a0-191">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="a04a0-192">Al termine della selezione gruppi, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="a04a0-192">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="a04a0-193">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un toohello tooassign ruolo gruppi di sicurezza selezionato.</span><span class="sxs-lookup"><span data-stu-id="a04a0-193">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="a04a0-194">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="a04a0-194">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="a04a0-195">Dopo un breve periodo, gli utenti di hello selezionato toolaunch in grado di queste applicazioni in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a04a0-195">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a04a0-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a04a0-196">Next steps</span></span>
[<span data-ttu-id="a04a0-197">Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a04a0-197">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
