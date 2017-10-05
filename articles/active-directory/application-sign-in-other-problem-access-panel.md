---
title: Problemi di accesso a un'applicazione dal pannello di accesso | Microsoft Docs
description: Come risolvere i problemi di accesso a un'applicazione dal pannello di accesso di Microsoft Azure AD su myapps.microsoft.com
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
ms.openlocfilehash: 188a00db59b0aa8d26facc678fb52d96272183b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-from-the-access-panel"></a><span data-ttu-id="626d6-103">Problemi di accesso a un'applicazione dal pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="626d6-103">Problems signing in to an application from the access panel</span></span>

<span data-ttu-id="626d6-104">Il pannello di accesso è un portale basato sul Web e consente a un utente che ha un account aziendale o dell'istituto di istruzione in Azure Active Directory (Azure AD) di visualizzare e avviare applicazioni basate su cloud a cui l'amministratore di Azure AD ha concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="626d6-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="626d6-105">Queste applicazioni sono configurate per conto dell'utente nel portale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="626d6-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="626d6-106">Perché l'applicazione sia visibile nel pannello di accesso, è necessario che sia configurata correttamente e assegnata all'utente o a un gruppo di cui l'utente è membro.</span><span class="sxs-lookup"><span data-stu-id="626d6-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="626d6-107">Il tipo di app che l'utente può visualizzare rientra nelle categorie seguenti:</span><span class="sxs-lookup"><span data-stu-id="626d6-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="626d6-108">Applicazioni di Office 365</span><span class="sxs-lookup"><span data-stu-id="626d6-108">Office 365 Applications</span></span>

-   <span data-ttu-id="626d6-109">Applicazioni Microsoft e di terze parti configurate con il servizio Single Sign-On basato su federazione</span><span class="sxs-lookup"><span data-stu-id="626d6-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="626d6-110">Applicazioni SSO basate su password</span><span class="sxs-lookup"><span data-stu-id="626d6-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="626d6-111">Applicazioni con soluzioni SSO esistenti</span><span class="sxs-lookup"><span data-stu-id="626d6-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="626d6-112">Problemi generali da verificare per primi</span><span class="sxs-lookup"><span data-stu-id="626d6-112">General issues to check first</span></span>

-   <span data-ttu-id="626d6-113">Assicurarsi di usare un **browser** che soddisfi i requisiti minimi per il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="626d6-113">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="626d6-114">Verificare che il browser dell'utente abbia aggiunto l'URL ai **siti attendibili** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-114">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="626d6-115">Assicurarsi di controllare che l'applicazione sia **configurata** correttamente.</span><span class="sxs-lookup"><span data-stu-id="626d6-115">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="626d6-116">Verificare che l'account dell'utente sia **abilitato** per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="626d6-116">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="626d6-117">Verificare che l'account dell'utente non sia **bloccato**.</span><span class="sxs-lookup"><span data-stu-id="626d6-117">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="626d6-118">Verificare che la **password dell'utente non sia scaduta o non sia stata dimenticata**.</span><span class="sxs-lookup"><span data-stu-id="626d6-118">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="626d6-119">Verificare che **Multi-Factor Authentication** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="626d6-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="626d6-120">Verificare che un criterio di **accesso condizionale** o di **protezione delle identità** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="626d6-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="626d6-121">Verificare che le **informazioni di contatto per l'autenticazione** di un utente siano aggiornate per permettere l'applicazione di Multi-Factor Authentication o di criteri di accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="626d6-121">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="626d6-122">Assicurarsi anche di cancellare i cookie del browser e riprovare ad accedere.</span><span class="sxs-lookup"><span data-stu-id="626d6-122">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="626d6-123">Applicazione dei requisiti del browser per il pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="626d6-123">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="626d6-124">Per il pannello di accesso è necessario un browser che supporti JavaScript e in cui sia abilitato CSS.</span><span class="sxs-lookup"><span data-stu-id="626d6-124">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="626d6-125">Per usare il servizio Single Sign-On (SSO) basato su password nel pannello di accesso, è necessario installare l'estensione del pannello di accesso nel browser dell'utente.</span><span class="sxs-lookup"><span data-stu-id="626d6-125">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="626d6-126">Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.</span><span class="sxs-lookup"><span data-stu-id="626d6-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="626d6-127">Per l'accesso Single Sign-On basato su password il browser dell'utente finale può essere uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="626d6-127">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="626d6-128">Internet Explorer 8, 9, 10, 11 su Windows 7 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="626d6-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="626d6-129">Edge su Windows 10 Anniversary Edition o versioni successive</span><span class="sxs-lookup"><span data-stu-id="626d6-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="626d6-130">Chrome in Windows 7 o versione successiva e MacOS X o versione successiva</span><span class="sxs-lookup"><span data-stu-id="626d6-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="626d6-131">Firefox 26.0 o versione successiva in Windows XP SP2 o versione successiva e in Mac OS X 10.6 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="626d6-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="626d6-132">Come installare l'estensione del browser per il pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="626d6-132">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="626d6-133">Per installare l'estensione del browser per il pannello di accesso, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="626d6-133">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="626d6-134">Aprire il [pannello di accesso](https://myapps.microsoft.com) in uno dei browser supportati e accedere come **utente** ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="626d6-134">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="626d6-135">Fare clic su un'**applicazione con accesso SSO basato su password** nel pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="626d6-135">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="626d6-136">Quando viene richiesto di installare il software, selezionare **Installa ora**.</span><span class="sxs-lookup"><span data-stu-id="626d6-136">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="626d6-137">A seconda del browser in uso, si verrà indirizzati al collegamento per il download.</span><span class="sxs-lookup"><span data-stu-id="626d6-137">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="626d6-138">**Aggiungere** l'estensione al browser.</span><span class="sxs-lookup"><span data-stu-id="626d6-138">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="626d6-139">Se richiesto dal browser, scegliere se **abilitare** o **consentire** l'uso dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="626d6-139">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="626d6-140">Al termine dell'installazione, **riavviare** la sessione del browser.</span><span class="sxs-lookup"><span data-stu-id="626d6-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="626d6-141">Accedere al pannello di accesso e verificare se è possibile **avviare** le applicazioni con accesso SSO basato su password.</span><span class="sxs-lookup"><span data-stu-id="626d6-141">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="626d6-142">È anche possibile scaricare l'estensione per Chrome ed Edge dai collegamenti diretti seguenti:</span><span class="sxs-lookup"><span data-stu-id="626d6-142">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="626d6-143">Estensione Pannello di accesso per Chrome</span><span class="sxs-lookup"><span data-stu-id="626d6-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="626d6-144">Estensione Pannello di accesso per Edge</span><span class="sxs-lookup"><span data-stu-id="626d6-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="626d6-145">Come configurare l'accesso Single Sign-On federato per un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="626d6-145">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="626d6-146">Per tutte le applicazioni nella raccolta di Azure AD con funzionalità Enterprise Single Sign-On abilitata è disponibile un'esercitazione dettagliata.</span><span class="sxs-lookup"><span data-stu-id="626d6-146">All application in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="626d6-147">Per le istruzioni dettagliate, è possibile accedere all'[Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/).</span><span class="sxs-lookup"><span data-stu-id="626d6-147">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="626d6-148">Per configurare un'applicazione della raccolta di Azure AD è necessario:</span><span class="sxs-lookup"><span data-stu-id="626d6-148">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="626d6-149">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="626d6-149">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="626d6-150">Configurare i valori dei metadati dell'applicazione in Azure AD (URL di accesso, identificatore, URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="626d6-150">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="626d6-151">Selezionare l'identificatore utente e aggiungere gli attributi utente da inviare all'applicazione</span><span class="sxs-lookup"><span data-stu-id="626d6-151">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="626d6-152">Recuperare il certificato e i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="626d6-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="626d6-153">Configurare i valori dei metadati di Azure AD nell'applicazione (URL di accesso, autorità emittente, URL di disconnessione e certificato)</span><span class="sxs-lookup"><span data-stu-id="626d6-153">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="626d6-154">Assegnare utenti all'applicazione</span><span class="sxs-lookup"><span data-stu-id="626d6-154">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="626d6-155">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="626d6-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="626d6-156">Per aggiungere un'applicazione dalla raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="626d6-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="626d6-157">Aprire il [portale di Azure](https://portal.azure.com) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="626d6-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="626d6-158">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="626d6-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="626d6-159">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="626d6-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="626d6-160">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="626d6-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="626d6-161">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="626d6-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="626d6-162">Nella casella di testo **Immettere un nome** della sezione **Aggiungi dalla raccolta** digitare il nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="626d6-163">Selezionare l'applicazione che si vuole configurare con l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="626d6-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="626d6-164">Prima di aggiungere l'applicazione, è possibile modificarne il nome usando la casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="626d6-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="626d6-165">Fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="626d6-166">Dopo un breve periodo di tempo sarà possibile visualizzare il pannello di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="626d6-167">Configurare l'accesso Single Sign-On per un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="626d6-167">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="626d6-168">Per configurare un accesso Single Sign-On per un'applicazione, seguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="626d6-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="626d6-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="626d6-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="626d6-170">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="626d6-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="626d6-171">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="626d6-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="626d6-172">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="626d6-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="626d6-173">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="626d6-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="626d6-174">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="626d6-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="626d6-175">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="626d6-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="626d6-176">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="626d6-177">Selezionare **Accesso basato su SAML** dal menu a discesa **Modalità**.</span><span class="sxs-lookup"><span data-stu-id="626d6-177">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="626d6-178">Immettere i valori necessari in **URL e dominio**.</span><span class="sxs-lookup"><span data-stu-id="626d6-178">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="626d6-179">È necessario ottenere questi valori dal fornitore dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-179">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="626d6-180">Per configurare l'applicazione come SSO avviato da provider di servizi, l'URL di accesso è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="626d6-180">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="626d6-181">Per alcune applicazioni, anche l'identificatore è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="626d6-181">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="626d6-182">Per configurare l'applicazione come SSO avviato da IdP, l'URL di risposta è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="626d6-182">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="626d6-183">Per alcune applicazioni, anche l'identificatore è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="626d6-183">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="626d6-184">**Facoltativo:** fare clic su **Mostra impostazioni URL avanzate** se si vuole vedere i valori non obbligatori.</span><span class="sxs-lookup"><span data-stu-id="626d6-184">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="626d6-185">In **Attributi utente** selezionare l'identificatore univoco per gli utenti nel menu a discesa **Identificatore utente**.</span><span class="sxs-lookup"><span data-stu-id="626d6-185">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="626d6-186">**Facoltativo:** fare clic su **Visualizza e modifica tutti gli altri attributi utente** per modificare gli attributi da inviare all'applicazione nel token SAML quando l'utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="626d6-186">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="626d6-187">Per aggiungere un attributo:</span><span class="sxs-lookup"><span data-stu-id="626d6-187">To add an attribute:</span></span>

   1. <span data-ttu-id="626d6-188">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="626d6-188">click **Add attribute**.</span></span> <span data-ttu-id="626d6-189">Immettere il **Nome** e selezionare il **Valore** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="626d6-189">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="626d6-190">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="626d6-190">Click **Save.**</span></span> <span data-ttu-id="626d6-191">Il nuovo attributo verrà visualizzato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="626d6-191">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="626d6-192">Fare clic su **Configura &lt;nome applicazione&gt;** per accedere alla documentazione che illustra come configurare l'accesso Single Sign-On nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-192">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="626d6-193">Sono inoltre disponibili il certificato e gli URL dei metadati richiesti per configurare l'accesso SSO con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-193">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="626d6-194">Fare clic su **Salva** per salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-194">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="626d6-195">Assegnare utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-195">Assign users to the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="626d6-196">Selezionare l'identificatore utente e aggiungere gli attributi utente da inviare all'applicazione</span><span class="sxs-lookup"><span data-stu-id="626d6-196">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="626d6-197">Per selezionare l'identificatore utente o aggiungere gli attributi dell'utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="626d6-197">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="626d6-198">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="626d6-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="626d6-199">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="626d6-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="626d6-200">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="626d6-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="626d6-201">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="626d6-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="626d6-202">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="626d6-202">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="626d6-203">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="626d6-203">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="626d6-204">Selezionare l'applicazione per cui è stato configurato l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="626d6-204">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="626d6-205">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="626d6-206">Nella sezione **Attributi utente** selezionare l'identificatore univoco per gli utenti nel menu a discesa **Identificatore utente**.</span><span class="sxs-lookup"><span data-stu-id="626d6-206">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="626d6-207">L'opzione selezionata deve corrispondere al valore previsto nell'applicazione per autenticare l'utente.</span><span class="sxs-lookup"><span data-stu-id="626d6-207">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="626d6-208">Azure AD seleziona il formato per l'attributo NameID (identificatore utente) in base al valore selezionato o al formato richiesto dall'applicazione nell'oggetto AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="626d6-208">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="626d6-209">Per altre informazioni, vedere l'articolo relativo al [protocollo SAML per Single Sign-On](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sotto la sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="626d6-209">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="626d6-210">Per aggiungere gli attributi utente, fare clic su **Visualizza e modifica tutti gli altri attributi utente** per modificare gli attributi da inviare all'applicazione nel token SAML quando l'utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="626d6-210">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="626d6-211">Per aggiungere un attributo:</span><span class="sxs-lookup"><span data-stu-id="626d6-211">To add an attribute:</span></span>

   1. <span data-ttu-id="626d6-212">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="626d6-212">click **Add attribute**.</span></span> <span data-ttu-id="626d6-213">Immettere il **Nome** e selezionare il **Valore** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="626d6-213">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="626d6-214">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="626d6-214">Click **Save.**</span></span> <span data-ttu-id="626d6-215">Il nuovo attributo verrà visualizzato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="626d6-215">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="626d6-216">Scaricare il certificato o i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="626d6-216">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="626d6-217">Per scaricare il certificato o i metadati dell'applicazione da Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="626d6-217">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="626d6-218">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="626d6-218">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="626d6-219">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="626d6-219">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="626d6-220">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="626d6-220">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="626d6-221">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="626d6-221">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="626d6-222">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="626d6-222">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="626d6-223">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="626d6-223">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="626d6-224">Selezionare l'applicazione per cui è stato configurato l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="626d6-224">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="626d6-225">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-225">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="626d6-226">Passare alla sezione **Certificato di firma SAML** e quindi fare clic sul valore della colonna **Download**.</span><span class="sxs-lookup"><span data-stu-id="626d6-226">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="626d6-227">A seconda di quale applicazione richiede la configurazione dell'accesso Single Sign-On, è visibile l'opzione per scaricare il codice XML dei metadati o l'opzione per scaricare il certificato.</span><span class="sxs-lookup"><span data-stu-id="626d6-227">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="626d6-228">Azure AD non fornisce URL per ottenere i metadati.</span><span class="sxs-lookup"><span data-stu-id="626d6-228">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="626d6-229">I metadati possono essere recuperati solo come file XML.</span><span class="sxs-lookup"><span data-stu-id="626d6-229">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="626d6-230">Come configurare l'accesso Single Sign-On federato per un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="626d6-230">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="626d6-231">Per configurare un'applicazione non inclusa nella raccolta, è necessario disporre di Azure AD Premium e l'applicazione deve supportare SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="626d6-231">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="626d6-232">Per altre informazioni sulle versioni di Azure AD, vedere [Prezzi di Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="626d6-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="626d6-233">Configurare i valori dei metadati dell'applicazione in Azure AD (URL di accesso, identificatore, URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="626d6-233">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="626d6-234">Selezionare l'identificatore utente e aggiungere gli attributi utente da inviare all'applicazione</span><span class="sxs-lookup"><span data-stu-id="626d6-234">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="626d6-235">Recuperare il certificato e i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="626d6-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="626d6-236">Configurare i valori dei metadati di Azure AD nell'applicazione (URL di accesso, autorità emittente, URL di disconnessione e certificato)</span><span class="sxs-lookup"><span data-stu-id="626d6-236">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="626d6-237">Configurare i valori dei metadati dell'applicazione in Azure AD (URL di accesso, identificatore, URL di risposta)</span><span class="sxs-lookup"><span data-stu-id="626d6-237">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="626d6-238">Per configurare l'accesso Single Sign-On per un'applicazione non inclusa nella raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="626d6-238">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="626d6-239">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="626d6-239">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="626d6-240">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="626d6-240">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="626d6-241">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="626d6-241">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="626d6-242">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="626d6-242">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="626d6-243">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="626d6-243">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="626d6-244">Fare clic su **Applicazione non nella raccolta** nella sezione **Aggiungi app personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="626d6-244">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="626d6-245">Immettere il nome dell'applicazione nella casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="626d6-245">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="626d6-246">Fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-246">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="626d6-247">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-247">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="626d6-248">Selezionare **Accesso basato su SAML** dal menu a discesa **Modalità**.</span><span class="sxs-lookup"><span data-stu-id="626d6-248">Select **SAML-based Sign-on** in the **Mode** dropdown</span></span>

11. <span data-ttu-id="626d6-249">Immettere i valori necessari in **URL e dominio**.</span><span class="sxs-lookup"><span data-stu-id="626d6-249">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="626d6-250">È necessario ottenere questi valori dal fornitore dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-250">You should get these values from the application vendor.</span></span>

  1. <span data-ttu-id="626d6-251">Per configurare l'applicazione come SSO avviato da IdP, immettere l'URL di risposta e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="626d6-251">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

  2. <span data-ttu-id="626d6-252">**Facoltativo:** per configurare l'applicazione come SSO avviato da provider di servizi, l'URL di accesso è un valore obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="626d6-252">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="626d6-253">In **Attributi utente** selezionare l'identificatore univoco per gli utenti nel menu a discesa **Identificatore utente**.</span><span class="sxs-lookup"><span data-stu-id="626d6-253">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="626d6-254">**Facoltativo:** fare clic su **Visualizza e modifica tutti gli altri attributi utente** per modificare gli attributi da inviare all'applicazione nel token SAML quando l'utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="626d6-254">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="626d6-255">Per aggiungere un attributo:</span><span class="sxs-lookup"><span data-stu-id="626d6-255">To add an attribute:</span></span>

   1. <span data-ttu-id="626d6-256">Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="626d6-256">click **Add attribute**.</span></span> <span data-ttu-id="626d6-257">Immettere il **Nome** e selezionare il **Valore** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="626d6-257">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="626d6-258">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="626d6-258">Click **Save.**</span></span> <span data-ttu-id="626d6-259">Il nuovo attributo verrà visualizzato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="626d6-259">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="626d6-260">Fare clic su **Configura &lt;nome applicazione&gt;** per accedere alla documentazione che illustra come configurare l'accesso Single Sign-On nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-260">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="626d6-261">Sono inoltre disponibili il certificato e gli URL di Azure AD richiesti per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-261">Also, you has Azure AD URLs and certificate required for the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="626d6-262">Selezionare l'identificatore utente e aggiungere gli attributi utente da inviare all'applicazione</span><span class="sxs-lookup"><span data-stu-id="626d6-262">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="626d6-263">Per selezionare l'identificatore utente o aggiungere gli attributi dell'utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="626d6-263">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="626d6-264">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="626d6-264">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="626d6-265">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="626d6-265">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="626d6-266">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="626d6-266">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="626d6-267">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="626d6-267">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="626d6-268">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="626d6-268">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="626d6-269">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="626d6-269">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="626d6-270">Selezionare l'applicazione per cui è stato configurato l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="626d6-270">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="626d6-271">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-271">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="626d6-272">Nella sezione **Attributi utente** selezionare l'identificatore univoco per gli utenti nel menu a discesa **Identificatore utente**.</span><span class="sxs-lookup"><span data-stu-id="626d6-272">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="626d6-273">L'opzione selezionata deve corrispondere al valore previsto nell'applicazione per autenticare l'utente.</span><span class="sxs-lookup"><span data-stu-id="626d6-273">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="626d6-274">Azure AD seleziona il formato per l'attributo NameID (identificatore utente) in base al valore selezionato o al formato richiesto dall'applicazione nell'oggetto AuthRequest SAML.</span><span class="sxs-lookup"><span data-stu-id="626d6-274">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="626d6-275">Per altre informazioni, vedere l'articolo relativo al [protocollo SAML per Single Sign-On](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sotto la sezione NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="626d6-275">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="626d6-276">Per aggiungere gli attributi utente, fare clic su **Visualizza e modifica tutti gli altri attributi utente** per modificare gli attributi da inviare all'applicazione nel token SAML quando l'utente effettua l'accesso.</span><span class="sxs-lookup"><span data-stu-id="626d6-276">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="626d6-277">Per aggiungere un attributo:</span><span class="sxs-lookup"><span data-stu-id="626d6-277">To add an attribute:</span></span>

   <span data-ttu-id="626d6-278">1. Fare clic su **Aggiungi attributo**.</span><span class="sxs-lookup"><span data-stu-id="626d6-278">1.click **Add attribute**.</span></span> <span data-ttu-id="626d6-279">Immettere il **Nome** e selezionare il **Valore** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="626d6-279">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   <span data-ttu-id="626d6-280">2. Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="626d6-280">2 Click **Save.**</span></span> <span data-ttu-id="626d6-281">Il nuovo attributo verrà visualizzato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="626d6-281">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="626d6-282">Scaricare il certificato o i metadati di Azure AD</span><span class="sxs-lookup"><span data-stu-id="626d6-282">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="626d6-283">Per scaricare il certificato o i metadati dell'applicazione da Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="626d6-283">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="626d6-284">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="626d6-284">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="626d6-285">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="626d6-285">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="626d6-286">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="626d6-286">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="626d6-287">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="626d6-287">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="626d6-288">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="626d6-288">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="626d6-289">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="626d6-289">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="626d6-290">Selezionare l'applicazione per cui è stato configurato l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="626d6-290">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="626d6-291">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-291">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="626d6-292">Passare alla sezione **Certificato di firma SAML** e quindi fare clic sul valore della colonna **Download**.</span><span class="sxs-lookup"><span data-stu-id="626d6-292">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="626d6-293">A seconda di quale applicazione richiede la configurazione dell'accesso Single Sign-On, è visibile l'opzione per scaricare il codice XML dei metadati o l'opzione per scaricare il certificato.</span><span class="sxs-lookup"><span data-stu-id="626d6-293">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="626d6-294">Azure AD non fornisce URL per ottenere i metadati.</span><span class="sxs-lookup"><span data-stu-id="626d6-294">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="626d6-295">I metadati possono essere recuperati solo come file XML.</span><span class="sxs-lookup"><span data-stu-id="626d6-295">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="626d6-296">Come configurare l'accesso Single Sign-On basato su password per un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="626d6-296">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="626d6-297">Per configurare un'applicazione della raccolta di Azure AD è necessario:</span><span class="sxs-lookup"><span data-stu-id="626d6-297">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="626d6-298">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="626d6-298">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="626d6-299">Configurare l'applicazione con l'accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="626d6-299">Configure the application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="626d6-300">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="626d6-300">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="626d6-301">Per aggiungere un'applicazione dalla raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="626d6-301">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="626d6-302">Aprire il [portale di Azure](https://portal.azure.com) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="626d6-302">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="626d6-303">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="626d6-303">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="626d6-304">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="626d6-304">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="626d6-305">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="626d6-305">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="626d6-306">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="626d6-306">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="626d6-307">Nella casella di testo **Immettere un nome** della sezione **Aggiungi dalla raccolta** digitare il nome dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="626d6-307">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="626d6-308">Selezionare l'applicazione che si vuole configurare per un accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="626d6-308">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="626d6-309">Prima di aggiungere l'applicazione, è possibile modificarne il nome dalla casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="626d6-309">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="626d6-310">Fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-310">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="626d6-311">Dopo un breve periodo di tempo sarà possibile visualizzare il pannello di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-311">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="626d6-312">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="626d6-312">Configure the application for password single sign-on</span></span>

<span data-ttu-id="626d6-313">Per configurare un accesso Single Sign-On per un'applicazione, seguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="626d6-313">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="626d6-314">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="626d6-314">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="626d6-315">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="626d6-315">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="626d6-316">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="626d6-316">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="626d6-317">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="626d6-317">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="626d6-318">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="626d6-318">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="626d6-319">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'**elenco di tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="626d6-319">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="626d6-320">Selezionare l'applicazione per cui si vuole configurare un accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="626d6-320">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="626d6-321">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-321">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="626d6-322">Selezionare la modalità **Accesso basato su password**.</span><span class="sxs-lookup"><span data-stu-id="626d6-322">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="626d6-323">Assegnare gli utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-323">Assign users to the application.</span></span>

10. <span data-ttu-id="626d6-324">È anche possibile specificare le credenziali per conto dell'utente selezionando le righe degli utenti e facendo clic su **Aggiorna credenziali**, quindi immettendo il nome utente e la password per conto degli utenti.</span><span class="sxs-lookup"><span data-stu-id="626d6-324">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="626d6-325">In caso contrario, verrà richiesto agli utenti di immettere le credenziali all'avvio.</span><span class="sxs-lookup"><span data-stu-id="626d6-325">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="626d6-326">Come configurare l'accesso Single Sign-On basato su password per un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="626d6-326">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="626d6-327">Per configurare un'applicazione della raccolta di Azure AD è necessario:</span><span class="sxs-lookup"><span data-stu-id="626d6-327">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="626d6-328">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="626d6-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="626d6-329">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="626d6-329">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="626d6-330">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="626d6-330">Add a non-gallery application</span></span>

<span data-ttu-id="626d6-331">Per aggiungere un'applicazione dalla raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="626d6-331">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="626d6-332">Aprire il [portale di Azure](https://portal.azure.com) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="626d6-332">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="626d6-333">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="626d6-333">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="626d6-334">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="626d6-334">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="626d6-335">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="626d6-335">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="626d6-336">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="626d6-336">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="626d6-337">Fare clic su**Applicazione non nella raccolta**.</span><span class="sxs-lookup"><span data-stu-id="626d6-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="626d6-338">Immettere il nome dell'applicazione nella casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="626d6-338">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="626d6-339">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="626d6-339">Select **Add.**</span></span>

<span data-ttu-id="626d6-340">Dopo un breve periodo di tempo, sarà possibile visualizzare il pannello di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-340">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="626d6-341">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="626d6-341">Configure the application for password single sign-on</span></span>

<span data-ttu-id="626d6-342">Per configurare un accesso Single Sign-On per un'applicazione, seguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="626d6-342">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="626d6-343">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="626d6-343">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="626d6-344">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="626d6-344">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="626d6-345">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="626d6-345">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="626d6-346">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="626d6-346">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="626d6-347">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="626d6-347">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="626d6-348">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="626d6-348">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="626d6-349">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="626d6-349">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="626d6-350">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-350">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="626d6-351">Selezionare la modalità **Accesso basato su password**.</span><span class="sxs-lookup"><span data-stu-id="626d6-351">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="626d6-352">Immettere l'**URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="626d6-352">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="626d6-353">Questo è l'URL in cui gli utenti immettono il nome utente e la password per accedere.</span><span class="sxs-lookup"><span data-stu-id="626d6-353">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="626d6-354">Verificare che i campi di accesso siano visibili nell'URL.</span><span class="sxs-lookup"><span data-stu-id="626d6-354">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="626d6-355">Assegnare gli utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-355">Assign users to the application.</span></span>

11. <span data-ttu-id="626d6-356">È anche possibile specificare le credenziali per conto dell'utente selezionando le righe degli utenti e facendo clic su **Aggiorna credenziali**, quindi immettendo il nome utente e la password per conto degli utenti.</span><span class="sxs-lookup"><span data-stu-id="626d6-356">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="626d6-357">In caso contrario, verrà richiesto agli utenti di immettere le credenziali all'avvio.</span><span class="sxs-lookup"><span data-stu-id="626d6-357">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="626d6-358">Come assegnare un utente direttamente a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="626d6-358">How to assign a user to an application directly</span></span>

<span data-ttu-id="626d6-359">Per assegnare uno o più utenti direttamente a un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="626d6-359">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="626d6-360">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="626d6-360">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="626d6-361">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="626d6-361">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="626d6-362">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="626d6-362">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="626d6-363">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="626d6-363">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="626d6-364">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="626d6-364">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="626d6-365">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="626d6-365">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="626d6-366">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="626d6-366">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="626d6-367">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-367">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="626d6-368">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="626d6-368">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="626d6-369">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="626d6-369">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="626d6-370">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo**  o l'**indirizzo di posta elettronica** dell'utente oggetto dell'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-370">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="626d6-371">Passare il puntatore sull'**utente** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="626d6-371">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="626d6-372">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo dell'utente per aggiungere l'utente all'elenco **Selezionato**.</span><span class="sxs-lookup"><span data-stu-id="626d6-372">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="626d6-373">**Facoltativo:** se si vuole **aggiungere più di un utente**, digitare un altro **nome completo** o **indirizzo di posta elettronica** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere l'utente all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="626d6-373">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="626d6-374">Dopo avere selezionato gli utenti, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="626d6-374">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="626d6-375">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="626d6-375">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="626d6-376">Fare clic sul pulsante **Assegna** per assegnare l'applicazione agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="626d6-376">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="626d6-377">Dopo un breve periodo di tempo, gli utenti selezionati saranno in grado di avviare queste applicazioni nel pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="626d6-377">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="626d6-378">Se questi passaggi di risoluzione dei problemi non risolvono il problema</span><span class="sxs-lookup"><span data-stu-id="626d6-378">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="626d6-379">aprire un ticket di supporto con le informazioni seguenti, se disponibili:</span><span class="sxs-lookup"><span data-stu-id="626d6-379">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="626d6-380">ID errore di correlazione</span><span class="sxs-lookup"><span data-stu-id="626d6-380">Correlation error ID</span></span>

-   <span data-ttu-id="626d6-381">UPN (indirizzo di posta elettronica dell'utente)</span><span class="sxs-lookup"><span data-stu-id="626d6-381">UPN (user email address)</span></span>

-   <span data-ttu-id="626d6-382">ID tenant</span><span class="sxs-lookup"><span data-stu-id="626d6-382">TenantID</span></span>

-   <span data-ttu-id="626d6-383">Tipo di browser</span><span class="sxs-lookup"><span data-stu-id="626d6-383">Browser type</span></span>

-   <span data-ttu-id="626d6-384">Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore</span><span class="sxs-lookup"><span data-stu-id="626d6-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="626d6-385">Tracce Fiddler</span><span class="sxs-lookup"><span data-stu-id="626d6-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="626d6-386">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="626d6-386">Next steps</span></span>
[<span data-ttu-id="626d6-387">Fornire l'accesso Single Sign-On alle app con il proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="626d6-387">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

