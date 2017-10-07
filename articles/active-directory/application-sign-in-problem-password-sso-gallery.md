---
title: accesso tooan applicazione raccolta di Azure AD configurata per la federazione aaaProblems accesso single sign-on | Documenti Microsoft
description: Come tootroubleshoot problemi con l'applicazione di raccolta di Azure AD configurata per la password single sign-on
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
ms.openlocfilehash: 7ba28765e1d1f13025d740790a2f87654ae0daed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="a8cc0-103">Problemi durante l'accesso tooan applicazione raccolta di Azure AD configurata per single sign-on federato</span><span class="sxs-lookup"><span data-stu-id="a8cc0-103">Problems signing in tooan Azure AD Gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="a8cc0-104">Hello Pannello di accesso è un portale basato sul web che consente un utente che ha un lavoro o scuola account in Azure Active Directory (Azure AD) tooview e avviare basato su cloud applicazioni che amministratore hello Azure AD ha concesso l'accesso a.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="a8cc0-105">Un utente con le edizioni di Azure AD consente inoltre di gruppi self-service e funzionalità di gestione di app tramite hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="a8cc0-106">Hello Pannello di accesso è separato dal portale di Azure hello e non richiede agli utenti toohave una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="a8cc0-107">toouse basato su password single sign-on (SSO nel Pannello di accesso, hello estensione del Pannello di accesso hello) deve essere installato nel browser dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="a8cc0-108">Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="a8cc0-109">Requisiti del browser per hello Pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="a8cc0-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="a8cc0-110">Pannello di accesso Hello richiede un browser che supporta JavaScript e CSS sono state abilitate.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="a8cc0-111">toouse basato su password single sign-on (SSO nel Pannello di accesso, hello estensione del Pannello di accesso hello) deve essere installato nel browser dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="a8cc0-112">Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="a8cc0-113">Per SSO basato su password, browser dell'utente finale di hello può essere:</span><span class="sxs-lookup"><span data-stu-id="a8cc0-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="a8cc0-114">Internet Explorer 8, 9, 10, 11 su Windows 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="a8cc0-114">Internet Explorer 8, 9, 10, 11 - on Windows 7 or later</span></span>

-   <span data-ttu-id="a8cc0-115">Chrome in Windows 7 o versione successiva e MacOS X o versione successiva</span><span class="sxs-lookup"><span data-stu-id="a8cc0-115">Chrome - on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="a8cc0-116">Firefox 26.0 o versione successiva in Windows XP SP2 o versione successiva e in Mac OS X 10.6 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="a8cc0-116">Firefox 26.0 or later - on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="a8cc0-117">estensione SSO basato su password Hello diventano disponibili per Edge in Windows 10 quando diventano supportate le estensioni del browser per Edge.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-117">hello password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="a8cc0-118">Come tooinstall hello estensione Browser Pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="a8cc0-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="a8cc0-119">hello tooinstall estensione Browser Pannello di accesso, le operazioni di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8cc0-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="a8cc0-120">Aprire hello [Pannello di accesso](https://myapps.microsoft.com) in uno dei browser supportato hello e accedere come un **utente** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="a8cc0-121">Fare clic su un **applicazione password SSO** in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-121">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="a8cc0-122">Hello prompt dei comandi in cui viene chiesto tooinstall hello selezionare software **installa**.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="a8cc0-123">Basata sul browser è il collegamento di download toohello diretto.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="a8cc0-124">**Aggiungere** browser tooyour di estensione hello.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="a8cc0-125">Se il browser viene richiesto, selezionare tooeither **abilitare** o **Consenti** hello estensione.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="a8cc0-126">Al termine dell'installazione, **riavviare** la sessione del browser.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="a8cc0-127">Accedere in hello Pannello di accesso e di vedere se è possibile **avviare** applicazioni password SSO</span><span class="sxs-lookup"><span data-stu-id="a8cc0-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="a8cc0-128">È anche possibile scaricare l'estensione hello per Chrome e Firefox dai collegamenti diretti hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="a8cc0-128">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="a8cc0-129">Estensione Pannello di accesso per Chrome</span><span class="sxs-lookup"><span data-stu-id="a8cc0-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="a8cc0-130">Estensione Pannello di accesso per Firefox</span><span class="sxs-lookup"><span data-stu-id="a8cc0-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="a8cc0-131">Impostazione dei Criteri di gruppo per Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="a8cc0-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="a8cc0-132">È possibile configurare criteri di gruppo che consentono di estensione del Pannello di accesso tooremotely installazione hello per Internet Explorer nei computer degli utenti.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="a8cc0-133">prerequisiti di Hello includono:</span><span class="sxs-lookup"><span data-stu-id="a8cc0-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="a8cc0-134">È stato impostato [servizi di dominio Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), e sono stati aggiunti dominio tooyour di computer degli utenti.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="a8cc0-135">È necessario disporre di hello tooedit autorizzazione "Modifica impostazioni" hello oggetto Criteri di gruppo (GPO).</span><span class="sxs-lookup"><span data-stu-id="a8cc0-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="a8cc0-136">Per impostazione predefinita, i membri di gruppi di sicurezza seguente hello dispongono di questa autorizzazione: Domain Administrators, Enterprise Administrators e Group Policy Creator Owners.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="a8cc0-137">[Altre informazioni](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8cc0-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="a8cc0-138">Seguire l'esercitazione hello [come tooDeploy hello estensione del Pannello di accesso per Internet Explorer utilizzando criteri di gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) per istruzioni dettagliate su come tooconfigure hello criteri di gruppo e distribuirlo toousers.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="a8cc0-139">Risoluzione dei problemi hello Pannello di accesso in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="a8cc0-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="a8cc0-140">Seguire hello [Troubleshoot hello estensione del Pannello di accesso per Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) della Guida per l'accesso in uno strumento di diagnostica e istruzioni dettagliate sulla configurazione di estensione hello per Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="a8cc0-141">Come password tooconfigure single sign-on per un'applicazione di raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8cc0-141">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="a8cc0-142">un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:</span><span class="sxs-lookup"><span data-stu-id="a8cc0-142">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="a8cc0-143">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8cc0-143">Add an application from hello Azure AD gallery</span></span>](#_Add_an_application)

-   [<span data-ttu-id="a8cc0-144">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="a8cc0-144">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="a8cc0-145">Assegnare gli utenti dell'applicazione toohello</span><span class="sxs-lookup"><span data-stu-id="a8cc0-145">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="a8cc0-146">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8cc0-146">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="a8cc0-147">un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="a8cc0-147">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="a8cc0-148">Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**</span><span class="sxs-lookup"><span data-stu-id="a8cc0-148">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="a8cc0-149">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-149">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8cc0-150">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-150">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8cc0-151">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-151">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8cc0-152">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** blade.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-152">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="a8cc0-153">In hello **immettere un nome** casella di testo da hello **Aggiungi dalla raccolta hello** sezione, il nome del tipo hello di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-153">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="a8cc0-154">Selezionare l'applicazione hello da tooconfigure per single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-154">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="a8cc0-155">Prima di aggiungere un'applicazione hello, è possibile modificarne il nome da hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-155">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="a8cc0-156">Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-156">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="a8cc0-157">Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-157">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="a8cc0-158">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="a8cc0-158">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="a8cc0-159">tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="a8cc0-159">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="a8cc0-160">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="a8cc0-160">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a8cc0-161">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-161">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8cc0-162">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-162">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8cc0-163">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-163">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8cc0-164">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-164">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="a8cc0-165">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="a8cc0-165">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="a8cc0-166">Selezionare l'applicazione hello da tooconfigure single sign-on</span><span class="sxs-lookup"><span data-stu-id="a8cc0-166">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="a8cc0-167">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-167">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a8cc0-168">Modalità di selezione hello **basato su Password Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="a8cc0-168">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="a8cc0-169">[Assegnare gli utenti dell'applicazione toohello](#_How_to_assign).</span><span class="sxs-lookup"><span data-stu-id="a8cc0-169">[Assign users toohello application](#_How_to_assign).</span></span>

10. <span data-ttu-id="a8cc0-170">Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-170">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="a8cc0-171">In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-171">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="assign-users-toohello-application"></a><span data-ttu-id="a8cc0-172">Assegnare gli utenti dell'applicazione toohello</span><span class="sxs-lookup"><span data-stu-id="a8cc0-172">Assign users toohello application</span></span>

<span data-ttu-id="a8cc0-173">tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="a8cc0-173">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="a8cc0-174">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="a8cc0-174">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a8cc0-175">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-175">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a8cc0-176">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-176">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a8cc0-177">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-177">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a8cc0-178">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-178">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="a8cc0-179">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="a8cc0-179">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="a8cc0-180">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-180">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="a8cc0-181">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-181">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a8cc0-182">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-182">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="a8cc0-183">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-183">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="a8cc0-184">Tipo di hello **nome completo** o **indirizzo di posta elettronica** dell'utente hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-184">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="a8cc0-185">Passare il mouse su hello **utente** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-185">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="a8cc0-186">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello dell'utente il toohello utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-186">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="a8cc0-187">**Facoltativo:** se si desidera troppo**aggiungere più di un utente**, in un altro tipo di **nome completo** o **indirizzo di posta elettronica** in hello **Cerca per nome o l'indirizzo di posta elettronica** casella di ricerca e fare clic su questo toohello utente hello casella di controllo tooadd **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-187">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="a8cc0-188">Al termine della selezione utenti, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-188">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="a8cc0-189">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un ruolo tooassign toohello utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-189">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="a8cc0-190">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-190">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="a8cc0-191">Dopo un breve periodo, gli utenti di hello selezionato toolaunch in grado di queste applicazioni in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a8cc0-191">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshoot-steps-dont-resolve-hello-issue"></a><span data-ttu-id="a8cc0-192">Se risolvere questi passaggi non consentono di risolvere problema hello</span><span class="sxs-lookup"><span data-stu-id="a8cc0-192">If these troubleshoot steps don't resolve hello issue</span></span> 
<span data-ttu-id="a8cc0-193">Aprire un ticket di supporto con hello se disponibili le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="a8cc0-193">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="a8cc0-194">ID errore di correlazione</span><span class="sxs-lookup"><span data-stu-id="a8cc0-194">Correlation error ID</span></span>

-   <span data-ttu-id="a8cc0-195">UPN (indirizzo di posta elettronica dell'utente)</span><span class="sxs-lookup"><span data-stu-id="a8cc0-195">UPN (user email address)</span></span>

-   <span data-ttu-id="a8cc0-196">ID tenant</span><span class="sxs-lookup"><span data-stu-id="a8cc0-196">TenantID</span></span>

-   <span data-ttu-id="a8cc0-197">Tipo di browser</span><span class="sxs-lookup"><span data-stu-id="a8cc0-197">Browser type</span></span>

-   <span data-ttu-id="a8cc0-198">Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore</span><span class="sxs-lookup"><span data-stu-id="a8cc0-198">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="a8cc0-199">Tracce Fiddler</span><span class="sxs-lookup"><span data-stu-id="a8cc0-199">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8cc0-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8cc0-200">Next steps</span></span>
[<span data-ttu-id="a8cc0-201">Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a8cc0-201">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
