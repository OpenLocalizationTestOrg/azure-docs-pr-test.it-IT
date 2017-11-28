---
title: firma nell'applicazione tooan utilizzando con un collegamento diretto aaaProblems | Documenti Microsoft
description: Come i problemi di tootroubleshoot l'accesso a un'applicazione da un URL con collegamento diretto con Azure AD
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a><span data-ttu-id="3f3df-103">Problemi durante l'accesso dell'applicazione tooan utilizzando con un collegamento diretto</span><span class="sxs-lookup"><span data-stu-id="3f3df-103">Problems signing in tooan application using a deeplink</span></span>

<span data-ttu-id="3f3df-104">Hello Pannello di accesso è un portale basato sul web che consente a un utente con un lavoro o account Azure Active Directory (Azure AD) tooview avvio basato su cloud le applicazioni e dell'istituto di istruzione che hello amministratore di Azure AD ha concesso l'accesso a.</span><span class="sxs-lookup"><span data-stu-id="3f3df-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="3f3df-105">Queste applicazioni sono configurate per conto di utente hello nel portale di Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="3f3df-106">un'applicazione Hello deve essere configurata correttamente e toohello assegnato utente o un utente di hello gruppo è un membro di un'applicazione hello toosee in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3f3df-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="3f3df-107">Collegamenti diretti o l'accesso gli URL sono collegamenti che gli utenti possono usare tooaccess barre applicazioni password SSO direttamente dall'URL del browser.</span><span class="sxs-lookup"><span data-stu-id="3f3df-107">Deep links or User access URLs are links your users may use tooaccess their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="3f3df-108">Passando toothis collegamento, gli utenti essere automaticamente effettuato l'accesso a un'applicazione hello senza dover prima toogo toohello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3f3df-108">By navigating toothis link, users be automatically signed into hello application without having toogo toohello Access Panel first.</span></span> <span data-ttu-id="3f3df-109">Si tratta di hello stesso collegamento che gli utenti usano tooaccess tali applicazioni dall'avvio dell'applicazione hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="3f3df-109">This is hello same link that users use tooaccess these applications from hello Office 365 application launcher.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="3f3df-110">Generale problemi toocheck prima</span><span class="sxs-lookup"><span data-stu-id="3f3df-110">General issues toocheck first</span></span>

-   <span data-ttu-id="3f3df-111">Assicurarsi di usare un **browser** che soddisfi i requisiti minimi di hello per hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3f3df-111">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="3f3df-112">Assicurarsi che il browser dell'utente hello sia aggiunto URL hello di hello applicazione tooits **siti attendibili**.</span><span class="sxs-lookup"><span data-stu-id="3f3df-112">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="3f3df-113">Assicurarsi che sia un'applicazione hello toocheck **configurato** correttamente.</span><span class="sxs-lookup"><span data-stu-id="3f3df-113">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="3f3df-114">Verificare che l'account dell'utente hello è **abilitato** per accessi.</span><span class="sxs-lookup"><span data-stu-id="3f3df-114">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="3f3df-115">Verificare che l'account dell'utente hello è **non bloccato.**</span><span class="sxs-lookup"><span data-stu-id="3f3df-115">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="3f3df-116">Assicurarsi che utente hello **password non è scaduta o è stata dimenticata.**</span><span class="sxs-lookup"><span data-stu-id="3f3df-116">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="3f3df-117">Verificare che **Multi-Factor Authentication** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="3f3df-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="3f3df-118">Verificare che un criterio di **accesso condizionale** o di **protezione delle identità** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="3f3df-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="3f3df-119">Assicurarsi che un utente **informazioni di contatto autenticazione** è toodate tooallow multi-Factor Authentication o l'accesso condizionale criteri toobe applicata.</span><span class="sxs-lookup"><span data-stu-id="3f3df-119">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="3f3df-120">Verificare che tooalso try cancellare i cookie del browser e riprovare toosign in.</span><span class="sxs-lookup"><span data-stu-id="3f3df-120">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="checking-hello-deeplink"></a><span data-ttu-id="3f3df-121">Il controllo con collegamento diretto hello</span><span class="sxs-lookup"><span data-stu-id="3f3df-121">Checking hello deeplink</span></span>

<span data-ttu-id="3f3df-122">toocheck se si dispone con collegamento diretto corretto hello procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="3f3df-122">toocheck if you have hello correct deeplink, follow hello steps below:</span></span>

1.  <span data-ttu-id="3f3df-123">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="3f3df-123">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3f3df-124">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-124">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3f3df-125">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3f3df-125">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3f3df-126">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f3df-126">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3f3df-127">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="3f3df-127">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3f3df-128">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="3f3df-128">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3f3df-129">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="3f3df-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="3f3df-130">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

8.  <span data-ttu-id="3f3df-131">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3f3df-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="3f3df-132">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f3df-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="3f3df-133">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="3f3df-133">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="3f3df-134">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="3f3df-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

11. <span data-ttu-id="3f3df-135">Selezionare l'applicazione hello da hello controllo hello deeplink per.</span><span class="sxs-lookup"><span data-stu-id="3f3df-135">Select hello application you want hello check hello deeplink for.</span></span>

12. <span data-ttu-id="3f3df-136">Trovare l'etichetta hello **URL di accesso utente**.</span><span class="sxs-lookup"><span data-stu-id="3f3df-136">Find hello label **User Access URL**.</span></span> <span data-ttu-id="3f3df-137">Il collegamento diretto deve corrispondere a questo URL.</span><span class="sxs-lookup"><span data-stu-id="3f3df-137">You deeplink should match this URL.</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="3f3df-138">Come tooinstall hello estensione Browser Pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="3f3df-138">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="3f3df-139">hello tooinstall estensione Browser Pannello di accesso, le operazioni di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="3f3df-139">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="3f3df-140">Aprire hello [Pannello di accesso](https://myapps.microsoft.com) in uno dei browser supportato hello e accedere come un **utente** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f3df-140">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="3f3df-141">Fare clic su un **applicazione password SSO** in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3f3df-141">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="3f3df-142">Hello prompt dei comandi in cui viene chiesto tooinstall hello selezionare software **installa**.</span><span class="sxs-lookup"><span data-stu-id="3f3df-142">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="3f3df-143">Basata sul browser è il collegamento di download toohello diretto.</span><span class="sxs-lookup"><span data-stu-id="3f3df-143">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="3f3df-144">**Aggiungere** browser tooyour di estensione hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-144">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="3f3df-145">Se il browser viene richiesto, selezionare tooeither **abilitare** o **Consenti** hello estensione.</span><span class="sxs-lookup"><span data-stu-id="3f3df-145">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="3f3df-146">Al termine dell'installazione, **riavviare** la sessione del browser.</span><span class="sxs-lookup"><span data-stu-id="3f3df-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="3f3df-147">Accedere in hello Pannello di accesso e di vedere se è possibile **avviare** applicazioni password SSO</span><span class="sxs-lookup"><span data-stu-id="3f3df-147">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="3f3df-148">È anche possibile scaricare l'estensione hello per Chrome e Firefox dai collegamenti diretti hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3f3df-148">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="3f3df-149">Estensione Pannello di accesso per Chrome</span><span class="sxs-lookup"><span data-stu-id="3f3df-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="3f3df-150">Estensione Pannello di accesso per Firefox</span><span class="sxs-lookup"><span data-stu-id="3f3df-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="3f3df-151">Come password tooconfigure single sign-on per un'applicazione di raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f3df-151">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="3f3df-152">un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:</span><span class="sxs-lookup"><span data-stu-id="3f3df-152">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="3f3df-153">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f3df-153">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="3f3df-154">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="3f3df-154">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="3f3df-155">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f3df-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="3f3df-156">un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="3f3df-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="3f3df-157">Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**.</span><span class="sxs-lookup"><span data-stu-id="3f3df-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="3f3df-158">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3f3df-159">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3f3df-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3f3df-160">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f3df-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3f3df-161">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** blade.</span><span class="sxs-lookup"><span data-stu-id="3f3df-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="3f3df-162">In hello **immettere un nome** casella di testo da hello **Aggiungi dalla raccolta hello** sezione, il nome del tipo hello di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="3f3df-163">Selezionare l'applicazione hello da tooconfigure per single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3f3df-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="3f3df-164">Prima di aggiungere un'applicazione hello, è possibile modificarne il nome da hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="3f3df-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="3f3df-165">Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="3f3df-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="3f3df-166">Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="3f3df-167">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="3f3df-167">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="3f3df-168">tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="3f3df-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="3f3df-169">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="3f3df-169">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3f3df-170">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3f3df-171">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3f3df-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3f3df-172">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f3df-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3f3df-173">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="3f3df-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3f3df-174">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="3f3df-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3f3df-175">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3f3df-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="3f3df-176">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3f3df-177">Modalità di selezione hello **basato su Password Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="3f3df-177">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="3f3df-178">[Assegnare gli utenti dell'applicazione toohello](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="3f3df-178">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="3f3df-179">Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-179">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="3f3df-180">In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.</span><span class="sxs-lookup"><span data-stu-id="3f3df-180">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="3f3df-181">Come password tooconfigure single sign-on per un'applicazione non-raccolta</span><span class="sxs-lookup"><span data-stu-id="3f3df-181">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="3f3df-182">un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:</span><span class="sxs-lookup"><span data-stu-id="3f3df-182">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="3f3df-183">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="3f3df-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="3f3df-184">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="3f3df-184">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="3f3df-185">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="3f3df-185">Add a non-gallery application</span></span>

<span data-ttu-id="3f3df-186">un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="3f3df-186">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="3f3df-187">Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**.</span><span class="sxs-lookup"><span data-stu-id="3f3df-187">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="3f3df-188">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-188">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3f3df-189">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3f3df-189">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3f3df-190">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f3df-190">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3f3df-191">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** blade.</span><span class="sxs-lookup"><span data-stu-id="3f3df-191">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="3f3df-192">Fare clic su**Applicazione non nella raccolta**.</span><span class="sxs-lookup"><span data-stu-id="3f3df-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="3f3df-193">Immettere il nome di hello dell'applicazione in hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="3f3df-193">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="3f3df-194">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3f3df-194">Select **Add.**</span></span>

<span data-ttu-id="3f3df-195">Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-195">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="3f3df-196">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="3f3df-196">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="3f3df-197">tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="3f3df-197">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="3f3df-198">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="3f3df-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3f3df-199">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3f3df-200">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3f3df-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3f3df-201">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f3df-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3f3df-202">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="3f3df-202">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="3f3df-203">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="3f3df-203">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3f3df-204">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3f3df-204">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="3f3df-205">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3f3df-206">Modalità di selezione hello **basato su Password Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="3f3df-206">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="3f3df-207">Immettere hello **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="3f3df-207">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="3f3df-208">Si tratta hello URL in cui gli utenti immettono il nome utente e password toosign in a.</span><span class="sxs-lookup"><span data-stu-id="3f3df-208">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="3f3df-209">Verificare i campi di accesso hello sono visibili nell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-209">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="3f3df-210">Assegnare gli utenti dell'applicazione toohello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-210">Assign users toohello application.</span></span>

11. <span data-ttu-id="3f3df-211">Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-211">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="3f3df-212">In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.</span><span class="sxs-lookup"><span data-stu-id="3f3df-212">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="3f3df-213">Come tooassign direttamente un'applicazione utente tooan</span><span class="sxs-lookup"><span data-stu-id="3f3df-213">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="3f3df-214">tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="3f3df-214">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="3f3df-215">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="3f3df-215">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3f3df-216">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-216">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3f3df-217">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3f3df-217">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3f3df-218">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f3df-218">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3f3df-219">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="3f3df-219">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3f3df-220">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="3f3df-220">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3f3df-221">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="3f3df-221">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="3f3df-222">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-222">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3f3df-223">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="3f3df-223">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="3f3df-224">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="3f3df-224">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="3f3df-225">Tipo di hello **nome completo** o **indirizzo di posta elettronica** dell'utente hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="3f3df-225">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="3f3df-226">Passare il mouse su hello **utente** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="3f3df-226">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="3f3df-227">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello dell'utente il toohello utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="3f3df-227">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="3f3df-228">**Facoltativo:** se si desidera troppo**aggiungere più di un utente**, in un altro tipo di **nome completo** o **indirizzo di posta elettronica** in hello **Cerca per nome o l'indirizzo di posta elettronica** casella di ricerca e fare clic su questo toohello utente hello casella di controllo tooadd **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="3f3df-228">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="3f3df-229">Al termine della selezione utenti, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="3f3df-229">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="3f3df-230">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un ruolo tooassign toohello utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="3f3df-230">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="3f3df-231">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="3f3df-231">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="3f3df-232">Dopo un breve periodo, gli utenti di hello selezionato toolaunch in grado di queste applicazioni in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3f3df-232">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="3f3df-233">Se questi passaggi di risoluzione dei problemi non hello per risolvere il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="3f3df-233">If these troubleshooting steps do not hello resolve hello issue.</span></span> 

<span data-ttu-id="3f3df-234">Aprire un ticket di supporto con hello se disponibili le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="3f3df-234">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="3f3df-235">ID errore di correlazione</span><span class="sxs-lookup"><span data-stu-id="3f3df-235">Correlation error ID</span></span>

-   <span data-ttu-id="3f3df-236">UPN (indirizzo di posta elettronica dell'utente)</span><span class="sxs-lookup"><span data-stu-id="3f3df-236">UPN (user email address)</span></span>

-   <span data-ttu-id="3f3df-237">ID tenant</span><span class="sxs-lookup"><span data-stu-id="3f3df-237">TenantID</span></span>

-   <span data-ttu-id="3f3df-238">Tipo di browser</span><span class="sxs-lookup"><span data-stu-id="3f3df-238">Browser type</span></span>

-   <span data-ttu-id="3f3df-239">Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore</span><span class="sxs-lookup"><span data-stu-id="3f3df-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="3f3df-240">Tracce Fiddler</span><span class="sxs-lookup"><span data-stu-id="3f3df-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f3df-241">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3f3df-241">Next steps</span></span>
[<span data-ttu-id="3f3df-242">Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="3f3df-242">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
