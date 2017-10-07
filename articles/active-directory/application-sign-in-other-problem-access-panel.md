---
title: la firma nell'applicazione tooan dal Pannello di accesso hello aaaProblems | Documenti Microsoft
description: Come l'accesso a un'applicazione da problemi di tootroubleshoot hello Pannello di accesso di Microsoft Azure AD all'indirizzo myapps.microsoft.com
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
ms.reviewer: japere
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a><span data-ttu-id="90e02-103">Problemi durante l'accesso dell'applicazione tooan dal Pannello di accesso hello</span><span class="sxs-lookup"><span data-stu-id="90e02-103">Problems signing in tooan application from hello access panel</span></span>

<span data-ttu-id="90e02-104">Hello Pannello di accesso è un portale basato sul web che consente a un utente con un lavoro o account Azure Active Directory (Azure AD) tooview avvio basato su cloud le applicazioni e dell'istituto di istruzione che hello amministratore di Azure AD ha concesso l'accesso a.</span><span class="sxs-lookup"><span data-stu-id="90e02-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="90e02-105">Queste applicazioni sono configurate per conto di utente hello nel portale di Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="90e02-106">un'applicazione Hello deve essere configurata correttamente e toohello assegnato utente o un utente di hello gruppo è un membro di un'applicazione hello toosee in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="90e02-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="90e02-107">tipo Hello delle App, potrebbe essere visualizzato un utente rientrano nelle seguenti categorie di hello:</span><span class="sxs-lookup"><span data-stu-id="90e02-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="90e02-108">Applicazioni di Office 365</span><span class="sxs-lookup"><span data-stu-id="90e02-108">Office 365 Applications</span></span>

-   <span data-ttu-id="90e02-109">Applicazioni Microsoft e di terze parti configurate con il servizio Single Sign-On basato su federazione</span><span class="sxs-lookup"><span data-stu-id="90e02-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="90e02-110">Applicazioni SSO basate su password</span><span class="sxs-lookup"><span data-stu-id="90e02-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="90e02-111">Applicazioni con soluzioni SSO esistenti</span><span class="sxs-lookup"><span data-stu-id="90e02-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="90e02-112">Generale problemi toocheck prima</span><span class="sxs-lookup"><span data-stu-id="90e02-112">General issues toocheck first</span></span>

-   <span data-ttu-id="90e02-113">Assicurarsi di usare un **browser** che soddisfi i requisiti minimi di hello per hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="90e02-113">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="90e02-114">Assicurarsi che il browser dell'utente hello sia aggiunto URL hello di hello applicazione tooits **siti attendibili**.</span><span class="sxs-lookup"><span data-stu-id="90e02-114">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="90e02-115">Assicurarsi che sia un'applicazione hello toocheck **configurato** correttamente.</span><span class="sxs-lookup"><span data-stu-id="90e02-115">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="90e02-116">Verificare che l'account dell'utente hello è **abilitato** per accessi.</span><span class="sxs-lookup"><span data-stu-id="90e02-116">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="90e02-117">Verificare che l'account dell'utente hello è **non bloccato.**</span><span class="sxs-lookup"><span data-stu-id="90e02-117">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="90e02-118">Assicurarsi che utente hello **password non è scaduta o è stata dimenticata.**</span><span class="sxs-lookup"><span data-stu-id="90e02-118">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="90e02-119">Verificare che **Multi-Factor Authentication** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="90e02-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="90e02-120">Verificare che un criterio di **accesso condizionale** o di **protezione delle identità** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="90e02-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="90e02-121">Assicurarsi che un utente **informazioni di contatto autenticazione** è toodate tooallow multi-Factor Authentication o l'accesso condizionale criteri toobe applicata.</span><span class="sxs-lookup"><span data-stu-id="90e02-121">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="90e02-122">Verificare che tooalso try cancellare i cookie del browser e riprovare toosign in.</span><span class="sxs-lookup"><span data-stu-id="90e02-122">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="90e02-123">Requisiti del browser per hello Pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="90e02-123">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="90e02-124">Pannello di accesso Hello richiede un browser che supporta JavaScript e CSS sono state abilitate.</span><span class="sxs-lookup"><span data-stu-id="90e02-124">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="90e02-125">toouse basato su password single sign-on (SSO nel Pannello di accesso, hello estensione del Pannello di accesso hello) deve essere installato nel browser dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-125">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="90e02-126">Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.</span><span class="sxs-lookup"><span data-stu-id="90e02-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="90e02-127">Per SSO basato su password, browser dell'utente finale di hello può essere:</span><span class="sxs-lookup"><span data-stu-id="90e02-127">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="90e02-128">Internet Explorer 8, 9, 10, 11 su Windows 7 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="90e02-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="90e02-129">Edge su Windows 10 Anniversary Edition o versioni successive</span><span class="sxs-lookup"><span data-stu-id="90e02-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="90e02-130">Chrome in Windows 7 o versione successiva e MacOS X o versione successiva</span><span class="sxs-lookup"><span data-stu-id="90e02-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="90e02-131">Firefox 26.0 o versione successiva in Windows XP SP2 o versione successiva e in Mac OS X 10.6 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="90e02-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="90e02-132">Come tooinstall hello estensione Browser Pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="90e02-132">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="90e02-133">hello tooinstall estensione Browser Pannello di accesso, le operazioni di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="90e02-133">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="90e02-134">Aprire hello [Pannello di accesso](https://myapps.microsoft.com) in uno dei browser supportato hello e accedere come un **utente** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90e02-134">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="90e02-135">Fare clic su un **applicazione password SSO** in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="90e02-135">Click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="90e02-136">Hello prompt dei comandi in cui viene chiesto tooinstall hello selezionare software **installa**.</span><span class="sxs-lookup"><span data-stu-id="90e02-136">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="90e02-137">Basata sul browser è il collegamento di download toohello diretto.</span><span class="sxs-lookup"><span data-stu-id="90e02-137">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="90e02-138">**Aggiungere** browser tooyour di estensione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-138">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="90e02-139">Se il browser viene richiesto, selezionare tooeither **abilitare** o **Consenti** hello estensione.</span><span class="sxs-lookup"><span data-stu-id="90e02-139">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="90e02-140">Al termine dell'installazione, **riavviare** la sessione del browser.</span><span class="sxs-lookup"><span data-stu-id="90e02-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="90e02-141">Accedere in hello Pannello di accesso e di vedere se è possibile **avviare** applicazioni password SSO</span><span class="sxs-lookup"><span data-stu-id="90e02-141">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="90e02-142">È anche possibile scaricare l'estensione hello per colore e bordo da collegamenti diretti hello riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="90e02-142">You may also download hello extension for Chrome and Edge from hello direct links below:</span></span>

-   [<span data-ttu-id="90e02-143">Estensione Pannello di accesso per Chrome</span><span class="sxs-lookup"><span data-stu-id="90e02-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="90e02-144">Estensione Pannello di accesso per Edge</span><span class="sxs-lookup"><span data-stu-id="90e02-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="90e02-145">Come tooconfigure federata single sign-on per un'applicazione di raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90e02-145">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="90e02-146">Tutte le applicazioni nella raccolta di Azure AD hello abilitata con funzionalità di Enterprise Single Sign-On con un'esercitazione dettagliata disponibile.</span><span class="sxs-lookup"><span data-stu-id="90e02-146">All application in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="90e02-147">È possibile accedere hello [elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) per una Guida di dettaglio.</span><span class="sxs-lookup"><span data-stu-id="90e02-147">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="90e02-148">un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:</span><span class="sxs-lookup"><span data-stu-id="90e02-148">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="90e02-149">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90e02-149">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="90e02-150">Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="90e02-150">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="90e02-151">Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente</span><span class="sxs-lookup"><span data-stu-id="90e02-151">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="90e02-152">Recuperare il certificato e i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90e02-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="90e02-153">Configurare i valori dei metadati di Azure AD in un'applicazione hello (accesso URL, autorità emittente, Logout URL e certificato)</span><span class="sxs-lookup"><span data-stu-id="90e02-153">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="90e02-154">Assegnare gli utenti dell'applicazione toohello</span><span class="sxs-lookup"><span data-stu-id="90e02-154">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="90e02-155">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90e02-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="90e02-156">un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="90e02-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="90e02-157">Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**</span><span class="sxs-lookup"><span data-stu-id="90e02-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="90e02-158">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="90e02-159">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="90e02-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="90e02-160">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90e02-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="90e02-161">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** pannello</span><span class="sxs-lookup"><span data-stu-id="90e02-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="90e02-162">In hello **immettere un nome** casella di testo da hello **Aggiungi dalla raccolta hello** sezione, il nome del tipo hello di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="90e02-163">Selezionare l'applicazione hello da tooconfigure per single sign-on.</span><span class="sxs-lookup"><span data-stu-id="90e02-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="90e02-164">Prima di aggiungere un'applicazione hello, è possibile modificarne il nome da hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="90e02-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="90e02-165">Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="90e02-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="90e02-166">Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="90e02-167">Configurare single sign-on per un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90e02-167">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="90e02-168">tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="90e02-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="90e02-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="90e02-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="90e02-170">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="90e02-171">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="90e02-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="90e02-172">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90e02-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="90e02-173">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="90e02-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="90e02-174">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="90e02-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="90e02-175">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="90e02-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="90e02-176">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="90e02-177">Selezionare **basato su SAML Sign-on** da hello **modalità** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="90e02-177">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="90e02-178">Immettere i valori hello necessarie nelle **dominio e gli URL.**</span><span class="sxs-lookup"><span data-stu-id="90e02-178">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="90e02-179">È necessario ottenere questi valori dal fornitore dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-179">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="90e02-180">un'applicazione hello tooconfigure come SSO avviato da SP, hello Sign in URL è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="90e02-180">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="90e02-181">Per alcune applicazioni, identificatore hello è anche un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="90e02-181">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="90e02-182">applicazione hello tooconfigure come avviata da IdP SSO, hello URL di risposta è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="90e02-182">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="90e02-183">Per alcune applicazioni, identificatore hello è anche un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="90e02-183">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="90e02-184">**Facoltativo:** fare clic su **Mostra URL impostazioni avanzate** se si desidera toosee hello non obbligatori valori.</span><span class="sxs-lookup"><span data-stu-id="90e02-184">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="90e02-185">In hello **gli attributi utente**, selezionare hello identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="90e02-185">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="90e02-186">**Facoltativo:** fare clic su **visualizzare e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.</span><span class="sxs-lookup"><span data-stu-id="90e02-186">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="90e02-187">un attributo tooadd:</span><span class="sxs-lookup"><span data-stu-id="90e02-187">tooadd an attribute:</span></span>

   1. <span data-ttu-id="90e02-188">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="90e02-188">click **Add attribute**.</span></span> <span data-ttu-id="90e02-189">Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-189">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="90e02-190">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="90e02-190">Click **Save.**</span></span> <span data-ttu-id="90e02-191">Vedrai hello nuovo attributo tabella hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-191">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="90e02-192">Fare clic su **configura &lt;nome applicazione&gt;**  tooaccess documentazione sulla tooconfigure single sign-on nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-192">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="90e02-193">È inoltre gli URL dei metadati di hello e certificato richiesto toosetup SSO con un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-193">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="90e02-194">Fare clic su **salvare** configurazione hello toosave.</span><span class="sxs-lookup"><span data-stu-id="90e02-194">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="90e02-195">Assegnare gli utenti dell'applicazione toohello.</span><span class="sxs-lookup"><span data-stu-id="90e02-195">Assign users toohello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="90e02-196">Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente</span><span class="sxs-lookup"><span data-stu-id="90e02-196">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="90e02-197">tooselect hello identificatore utente o aggiungere gli attributi utente, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="90e02-197">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="90e02-198">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="90e02-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="90e02-199">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="90e02-200">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="90e02-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="90e02-201">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90e02-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="90e02-202">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="90e02-202">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="90e02-203">Se non viene visualizzata l'applicazione hello da tooshow qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="90e02-203">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="90e02-204">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="90e02-204">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="90e02-205">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="90e02-206">In hello **gli attributi utente** hello di sezione, selezionare un identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="90e02-206">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="90e02-207">Hello opzione selezionata deve toomatch hello previsto valore utente hello tooauthenticate dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-207">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="90e02-208">Azure AD selezionare hello formato attributo NameID hello (ID utente) in base al valore di hello selezionato o per hello formato richiesto da un'applicazione hello in hello AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="90e02-208">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="90e02-209">Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) in hello sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="90e02-209">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="90e02-210">Fare clic su attributi utente tooadd, **visualizzazione e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.</span><span class="sxs-lookup"><span data-stu-id="90e02-210">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="90e02-211">un attributo tooadd:</span><span class="sxs-lookup"><span data-stu-id="90e02-211">tooadd an attribute:</span></span>

   1. <span data-ttu-id="90e02-212">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="90e02-212">click **Add attribute**.</span></span> <span data-ttu-id="90e02-213">Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-213">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="90e02-214">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="90e02-214">Click **Save.**</span></span> <span data-ttu-id="90e02-215">Vedrai hello nuovo attributo tabella hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-215">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="90e02-216">Scaricare i metadati di Azure AD hello o certificato</span><span class="sxs-lookup"><span data-stu-id="90e02-216">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="90e02-217">i metadati dell'applicazione hello toodownload o un certificato da Azure AD, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="90e02-217">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="90e02-218">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="90e02-218">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="90e02-219">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-219">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="90e02-220">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="90e02-220">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="90e02-221">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90e02-221">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="90e02-222">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="90e02-222">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="90e02-223">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="90e02-223">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="90e02-224">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="90e02-224">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="90e02-225">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-225">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="90e02-226">Andare troppo**certificato di firma SAML** sezione, quindi fare clic su **scaricare** valore della colonna.</span><span class="sxs-lookup"><span data-stu-id="90e02-226">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="90e02-227">A seconda di quale applicazione hello richiede la configurazione di single sign-on, vedere uno toodownload opzione hello hello Metadata XML o hello certificato.</span><span class="sxs-lookup"><span data-stu-id="90e02-227">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="90e02-228">Azure AD non fornisce i metadati hello tooget URL.</span><span class="sxs-lookup"><span data-stu-id="90e02-228">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="90e02-229">Hello metadati possono essere recuperati solo come un file XML.</span><span class="sxs-lookup"><span data-stu-id="90e02-229">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="90e02-230">Come tooconfigure federata single sign-on per un'applicazione non-raccolta</span><span class="sxs-lookup"><span data-stu-id="90e02-230">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="90e02-231">un'applicazione non raccolta tooconfigure, è necessario toohave Azure AD premium e un'applicazione hello supporta SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="90e02-231">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="90e02-232">Per altre informazioni sulle versioni di Azure AD, vedere [Prezzi di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="90e02-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="90e02-233">Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="90e02-233">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="90e02-234">Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente</span><span class="sxs-lookup"><span data-stu-id="90e02-234">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="90e02-235">Recuperare il certificato e i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90e02-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="90e02-236">Configurare i valori dei metadati di Azure AD in un'applicazione hello (accesso URL, autorità emittente, Logout URL e certificato)</span><span class="sxs-lookup"><span data-stu-id="90e02-236">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="90e02-237">Configurare i valori dei metadati dell'applicazione hello in Azure AD (accesso URL, identificatore, l'URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="90e02-237">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="90e02-238">tooconfigure single sign-on per un'applicazione che non si trova nella raccolta di Azure AD hello, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="90e02-238">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="90e02-239">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="90e02-239">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="90e02-240">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-240">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="90e02-241">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="90e02-241">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="90e02-242">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90e02-242">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="90e02-243">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** pannello</span><span class="sxs-lookup"><span data-stu-id="90e02-243">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="90e02-244">Fare clic su **applicazione Non raccolta** in hello **aggiungere la propria app** sezione</span><span class="sxs-lookup"><span data-stu-id="90e02-244">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="90e02-245">Immettere il nome di hello dell'applicazione hello in hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="90e02-245">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="90e02-246">Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="90e02-246">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="90e02-247">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-247">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="90e02-248">Selezionare **basato su SAML Sign-on** in hello **modalità** elenco a discesa</span><span class="sxs-lookup"><span data-stu-id="90e02-248">Select **SAML-based Sign-on** in hello **Mode** dropdown</span></span>

11. <span data-ttu-id="90e02-249">Immettere i valori hello necessarie nelle **dominio e gli URL.**</span><span class="sxs-lookup"><span data-stu-id="90e02-249">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="90e02-250">È necessario ottenere questi valori dal fornitore dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-250">You should get these values from hello application vendor.</span></span>

  1. <span data-ttu-id="90e02-251">un'applicazione hello tooconfigure come avviata da IdP SSO, immettere hello URL di risposta e l'identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-251">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

  2. <span data-ttu-id="90e02-252">**Facoltativo:** tooconfigure un'applicazione hello come SSO avviato da SP, hello Sign in URL è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="90e02-252">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="90e02-253">In hello **gli attributi utente**, selezionare hello identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="90e02-253">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="90e02-254">**Facoltativo:** fare clic su **visualizzare e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.</span><span class="sxs-lookup"><span data-stu-id="90e02-254">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="90e02-255">un attributo tooadd:</span><span class="sxs-lookup"><span data-stu-id="90e02-255">tooadd an attribute:</span></span>

   1. <span data-ttu-id="90e02-256">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="90e02-256">click **Add attribute**.</span></span> <span data-ttu-id="90e02-257">Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-257">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="90e02-258">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="90e02-258">Click **Save.**</span></span> <span data-ttu-id="90e02-259">Vedrai hello nuovo attributo tabella hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-259">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="90e02-260">Fare clic su **configura &lt;nome applicazione&gt;**  tooaccess documentazione sulla tooconfigure single sign-on nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-260">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="90e02-261">È inoltre URL AD Azure e certificato richiesto per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-261">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="90e02-262">Identificatore utente di selezionare e aggiungere l'applicazione toohello toobe inviati gli attributi di utente</span><span class="sxs-lookup"><span data-stu-id="90e02-262">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="90e02-263">tooselect hello identificatore utente o aggiungere gli attributi utente, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="90e02-263">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="90e02-264">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="90e02-264">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="90e02-265">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-265">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="90e02-266">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="90e02-266">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="90e02-267">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90e02-267">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="90e02-268">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="90e02-268">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="90e02-269">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="90e02-269">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="90e02-270">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="90e02-270">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="90e02-271">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-271">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="90e02-272">In hello **gli attributi utente** hello di sezione, selezionare un identificatore univoco per gli utenti in hello **identificatore utente** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="90e02-272">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="90e02-273">Hello opzione selezionata deve toomatch hello previsto valore utente hello tooauthenticate dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-273">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="90e02-274">Azure AD selezionare hello formato attributo NameID hello (ID utente) in base al valore di hello selezionato o per hello formato richiesto da un'applicazione hello in hello AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="90e02-274">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="90e02-275">Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) in hello sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="90e02-275">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="90e02-276">Fare clic su attributi utente tooadd, **visualizzazione e modificare tutti gli altri attributi utente** tooedit hello attributi applicazione toohello toobe inviati nel token SAML hello quando l'utente accede.</span><span class="sxs-lookup"><span data-stu-id="90e02-276">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="90e02-277">un attributo tooadd:</span><span class="sxs-lookup"><span data-stu-id="90e02-277">tooadd an attribute:</span></span>

   <span data-ttu-id="90e02-278">1. Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="90e02-278">1.click **Add attribute**.</span></span> <span data-ttu-id="90e02-279">Immettere hello **nome** hello selezionare hello e **valore** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-279">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   <span data-ttu-id="90e02-280">2. Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="90e02-280">2 Click **Save.**</span></span> <span data-ttu-id="90e02-281">Vedrai hello nuovo attributo tabella hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-281">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="90e02-282">Scaricare i metadati di Azure AD hello o certificato</span><span class="sxs-lookup"><span data-stu-id="90e02-282">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="90e02-283">i metadati dell'applicazione hello toodownload o un certificato da Azure AD, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="90e02-283">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="90e02-284">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="90e02-284">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="90e02-285">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-285">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="90e02-286">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="90e02-286">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="90e02-287">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90e02-287">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="90e02-288">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="90e02-288">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="90e02-289">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="90e02-289">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="90e02-290">Selezionare un'applicazione hello è stato configurato single sign-on.</span><span class="sxs-lookup"><span data-stu-id="90e02-290">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="90e02-291">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-291">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="90e02-292">Andare troppo**certificato di firma SAML** sezione, quindi fare clic su **scaricare** valore della colonna.</span><span class="sxs-lookup"><span data-stu-id="90e02-292">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="90e02-293">A seconda di quale applicazione hello richiede la configurazione di single sign-on, vedere uno toodownload opzione hello hello Metadata XML o hello certificato.</span><span class="sxs-lookup"><span data-stu-id="90e02-293">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="90e02-294">Azure AD non fornisce i metadati hello tooget URL.</span><span class="sxs-lookup"><span data-stu-id="90e02-294">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="90e02-295">Hello metadati possono essere recuperati solo come un file XML.</span><span class="sxs-lookup"><span data-stu-id="90e02-295">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="90e02-296">Come password tooconfigure single sign-on per un'applicazione di raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90e02-296">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="90e02-297">un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:</span><span class="sxs-lookup"><span data-stu-id="90e02-297">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="90e02-298">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90e02-298">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="90e02-299">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="90e02-299">Configure hello application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="90e02-300">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="90e02-300">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="90e02-301">un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="90e02-301">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="90e02-302">Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**</span><span class="sxs-lookup"><span data-stu-id="90e02-302">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="90e02-303">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-303">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="90e02-304">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="90e02-304">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="90e02-305">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90e02-305">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="90e02-306">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** pannello</span><span class="sxs-lookup"><span data-stu-id="90e02-306">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="90e02-307">In hello **immettere un nome** casella di testo da hello **Aggiungi dalla raccolta hello** sezione, il nome del tipo hello di un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="90e02-307">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="90e02-308">Selezionare l'applicazione hello da tooconfigure per single sign-on</span><span class="sxs-lookup"><span data-stu-id="90e02-308">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="90e02-309">Prima di aggiungere un'applicazione hello, è possibile modificarne il nome da hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="90e02-309">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="90e02-310">Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="90e02-310">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="90e02-311">Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-311">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="90e02-312">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="90e02-312">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="90e02-313">tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="90e02-313">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="90e02-314">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="90e02-314">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="90e02-315">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-315">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="90e02-316">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="90e02-316">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="90e02-317">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90e02-317">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="90e02-318">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="90e02-318">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="90e02-319">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="90e02-319">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="90e02-320">Selezionare l'applicazione hello da tooconfigure single sign-on</span><span class="sxs-lookup"><span data-stu-id="90e02-320">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="90e02-321">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-321">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="90e02-322">Modalità di selezione hello **basato su Password Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="90e02-322">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="90e02-323">Assegnare gli utenti dell'applicazione toohello.</span><span class="sxs-lookup"><span data-stu-id="90e02-323">Assign users toohello application.</span></span>

10. <span data-ttu-id="90e02-324">Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-324">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="90e02-325">In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.</span><span class="sxs-lookup"><span data-stu-id="90e02-325">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="90e02-326">Come password tooconfigure single sign-on per un'applicazione non-raccolta</span><span class="sxs-lookup"><span data-stu-id="90e02-326">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="90e02-327">un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:</span><span class="sxs-lookup"><span data-stu-id="90e02-327">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="90e02-328">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="90e02-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="90e02-329">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="90e02-329">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="90e02-330">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="90e02-330">Add a non-gallery application</span></span>

<span data-ttu-id="90e02-331">un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="90e02-331">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="90e02-332">Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**</span><span class="sxs-lookup"><span data-stu-id="90e02-332">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="90e02-333">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-333">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="90e02-334">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="90e02-334">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="90e02-335">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90e02-335">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="90e02-336">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** pannello</span><span class="sxs-lookup"><span data-stu-id="90e02-336">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="90e02-337">Fare clic su**Applicazione non nella raccolta**.</span><span class="sxs-lookup"><span data-stu-id="90e02-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="90e02-338">Immettere il nome di hello dell'applicazione in hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="90e02-338">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="90e02-339">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="90e02-339">Select **Add.**</span></span>

<span data-ttu-id="90e02-340">Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-340">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="90e02-341">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="90e02-341">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="90e02-342">tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="90e02-342">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="90e02-343">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="90e02-343">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="90e02-344">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-344">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="90e02-345">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="90e02-345">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="90e02-346">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90e02-346">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="90e02-347">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="90e02-347">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="90e02-348">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="90e02-348">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="90e02-349">Selezionare l'applicazione hello tooconfigure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="90e02-349">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="90e02-350">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-350">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="90e02-351">Modalità di selezione hello **basato su Password Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="90e02-351">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="90e02-352">Immettere hello **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="90e02-352">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="90e02-353">Si tratta hello URL in cui gli utenti immettono il nome utente e password toosign in a.</span><span class="sxs-lookup"><span data-stu-id="90e02-353">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="90e02-354">Verificare i campi di accesso hello sono visibili nell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-354">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="90e02-355">Assegnare gli utenti dell'applicazione toohello.</span><span class="sxs-lookup"><span data-stu-id="90e02-355">Assign users toohello application.</span></span>

11. <span data-ttu-id="90e02-356">Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-356">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="90e02-357">In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.</span><span class="sxs-lookup"><span data-stu-id="90e02-357">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="90e02-358">Come tooassign direttamente un'applicazione utente tooan</span><span class="sxs-lookup"><span data-stu-id="90e02-358">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="90e02-359">tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="90e02-359">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="90e02-360">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="90e02-360">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="90e02-361">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-361">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="90e02-362">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="90e02-362">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="90e02-363">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="90e02-363">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="90e02-364">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="90e02-364">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="90e02-365">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="90e02-365">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="90e02-366">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="90e02-366">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="90e02-367">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90e02-367">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="90e02-368">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="90e02-368">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="90e02-369">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="90e02-369">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="90e02-370">Tipo di hello **nome completo** o **indirizzo di posta elettronica** dell'utente hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="90e02-370">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="90e02-371">Passare il mouse su hello **utente** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="90e02-371">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="90e02-372">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello dell'utente il toohello utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="90e02-372">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="90e02-373">**Facoltativo:** se si desidera troppo**aggiungere più di un utente**, in un altro tipo di **nome completo** o **indirizzo di posta elettronica** in hello **Cerca per nome o l'indirizzo di posta elettronica** casella di ricerca e fare clic su questo toohello utente hello casella di controllo tooadd **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="90e02-373">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="90e02-374">Al termine della selezione utenti, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="90e02-374">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="90e02-375">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un ruolo tooassign toohello utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="90e02-375">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="90e02-376">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="90e02-376">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="90e02-377">Dopo un breve periodo, gli utenti di hello selezionato toolaunch in grado di queste applicazioni in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="90e02-377">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="90e02-378">Se questi passaggi di risoluzione dei problemi non hello di risolvere il problema di hello</span><span class="sxs-lookup"><span data-stu-id="90e02-378">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="90e02-379">Aprire un ticket di supporto con hello se disponibili le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="90e02-379">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="90e02-380">ID errore di correlazione</span><span class="sxs-lookup"><span data-stu-id="90e02-380">Correlation error ID</span></span>

-   <span data-ttu-id="90e02-381">UPN (indirizzo di posta elettronica dell'utente)</span><span class="sxs-lookup"><span data-stu-id="90e02-381">UPN (user email address)</span></span>

-   <span data-ttu-id="90e02-382">ID tenant</span><span class="sxs-lookup"><span data-stu-id="90e02-382">TenantID</span></span>

-   <span data-ttu-id="90e02-383">Tipo di browser</span><span class="sxs-lookup"><span data-stu-id="90e02-383">Browser type</span></span>

-   <span data-ttu-id="90e02-384">Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore</span><span class="sxs-lookup"><span data-stu-id="90e02-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="90e02-385">Tracce Fiddler</span><span class="sxs-lookup"><span data-stu-id="90e02-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="90e02-386">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90e02-386">Next steps</span></span>
[<span data-ttu-id="90e02-387">Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="90e02-387">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

