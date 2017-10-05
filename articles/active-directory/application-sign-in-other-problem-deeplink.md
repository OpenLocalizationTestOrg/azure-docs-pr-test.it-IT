---
title: Problemi di accesso a un'applicazione usando un collegamento diretto | Microsoft Docs
description: Come risolvere i problemi di accesso a un'applicazione da un URL con collegamento diretto usando Azure AD
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
ms.openlocfilehash: 798015ab68afc65378cffc75afec9c7f91fc1926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-using-a-deeplink"></a><span data-ttu-id="1e300-103">Problemi di accesso a un'applicazione usando un collegamento diretto</span><span class="sxs-lookup"><span data-stu-id="1e300-103">Problems signing in to an application using a deeplink</span></span>

<span data-ttu-id="1e300-104">Il pannello di accesso è un portale basato sul Web e consente a un utente che ha un account aziendale o dell'istituto di istruzione in Azure Active Directory (Azure AD) di visualizzare e avviare applicazioni basate su cloud a cui l'amministratore di Azure AD ha concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="1e300-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="1e300-105">Queste applicazioni sono configurate per conto dell'utente nel portale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e300-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="1e300-106">Perché l'applicazione sia visibile nel pannello di accesso, è necessario che sia configurata correttamente e assegnata all'utente o a un gruppo di cui l'utente è membro.</span><span class="sxs-lookup"><span data-stu-id="1e300-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="1e300-107">I collegamenti diretti o gli URL di accesso utente sono collegamenti che gli utenti potrebbero utilizzare per accedere alle applicazioni con SSO basato su password direttamente dalla barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="1e300-107">Deep links or User access URLs are links your users may use to access their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="1e300-108">Usando questo collegamento gli utenti accedono automaticamente all'applicazione senza dover passare prima per il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1e300-108">By navigating to this link, users be automatically signed into the application without having to go to the Access Panel first.</span></span> <span data-ttu-id="1e300-109">Questo è lo stesso collegamento usato dagli utenti per accedere a queste applicazioni dall'applicazione di avvio di Office 365.</span><span class="sxs-lookup"><span data-stu-id="1e300-109">This is the same link that users use to access these applications from the Office 365 application launcher.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="1e300-110">Problemi generali da verificare per primi</span><span class="sxs-lookup"><span data-stu-id="1e300-110">General issues to check first</span></span>

-   <span data-ttu-id="1e300-111">Assicurarsi di usare un **browser** che soddisfi i requisiti minimi per il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1e300-111">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="1e300-112">Verificare che il browser dell'utente abbia aggiunto l'URL ai **siti attendibili** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e300-112">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="1e300-113">Assicurarsi di controllare che l'applicazione sia **configurata** correttamente.</span><span class="sxs-lookup"><span data-stu-id="1e300-113">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="1e300-114">Verificare che l'account dell'utente sia **abilitato** per l'accesso.</span><span class="sxs-lookup"><span data-stu-id="1e300-114">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="1e300-115">Verificare che l'account dell'utente non sia **bloccato**.</span><span class="sxs-lookup"><span data-stu-id="1e300-115">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="1e300-116">Verificare che la **password dell'utente non sia scaduta o non sia stata dimenticata**.</span><span class="sxs-lookup"><span data-stu-id="1e300-116">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="1e300-117">Verificare che **Multi-Factor Authentication** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="1e300-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="1e300-118">Verificare che un criterio di **accesso condizionale** o di **protezione delle identità** non blocchi l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="1e300-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="1e300-119">Verificare che le **informazioni di contatto per l'autenticazione** di un utente siano aggiornate per permettere l'applicazione di Multi-Factor Authentication o di criteri di accesso condizionale.</span><span class="sxs-lookup"><span data-stu-id="1e300-119">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="1e300-120">Assicurarsi anche di cancellare i cookie del browser e riprovare ad accedere.</span><span class="sxs-lookup"><span data-stu-id="1e300-120">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="checking-the-deeplink"></a><span data-ttu-id="1e300-121">Verifica del collegamento diretto</span><span class="sxs-lookup"><span data-stu-id="1e300-121">Checking the deeplink</span></span>

<span data-ttu-id="1e300-122">Per verificare se si dispone del collegamento diretto corretto, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1e300-122">To check if you have the correct deeplink, follow the steps below:</span></span>

1.  <span data-ttu-id="1e300-123">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="1e300-123">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1e300-124">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1e300-124">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1e300-125">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e300-125">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1e300-126">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1e300-126">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1e300-127">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1e300-127">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="1e300-128">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'**elenco di tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1e300-128">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1e300-129">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="1e300-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="1e300-130">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1e300-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

8.  <span data-ttu-id="1e300-131">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e300-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="1e300-132">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1e300-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="1e300-133">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1e300-133">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="1e300-134">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'**elenco di tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1e300-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

11. <span data-ttu-id="1e300-135">Selezionare l'applicazione di cui si desidera verificare il .collegamento diretto.</span><span class="sxs-lookup"><span data-stu-id="1e300-135">Select the application you want the check the deeplink for.</span></span>

12. <span data-ttu-id="1e300-136">Trovare l'etichetta **URL accesso utente**.</span><span class="sxs-lookup"><span data-stu-id="1e300-136">Find the label **User Access URL**.</span></span> <span data-ttu-id="1e300-137">Il collegamento diretto deve corrispondere a questo URL.</span><span class="sxs-lookup"><span data-stu-id="1e300-137">You deeplink should match this URL.</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="1e300-138">Come installare l'estensione del browser per il pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="1e300-138">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="1e300-139">Per installare l'estensione del browser per il pannello di accesso, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1e300-139">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="1e300-140">Aprire il [pannello di accesso](https://myapps.microsoft.com) in uno dei browser supportati e accedere come **utente** ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e300-140">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="1e300-141">Fare clic su un'**applicazione con accesso SSO basato su password** nel pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1e300-141">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="1e300-142">Quando viene richiesto di installare il software, selezionare **Installa ora**.</span><span class="sxs-lookup"><span data-stu-id="1e300-142">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="1e300-143">A seconda del browser in uso, si verrà indirizzati al collegamento per il download.</span><span class="sxs-lookup"><span data-stu-id="1e300-143">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="1e300-144">**Aggiungere** l'estensione al browser.</span><span class="sxs-lookup"><span data-stu-id="1e300-144">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="1e300-145">Se richiesto dal browser, scegliere se **abilitare** o **consentire** l'uso dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="1e300-145">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="1e300-146">Al termine dell'installazione, **riavviare** la sessione del browser.</span><span class="sxs-lookup"><span data-stu-id="1e300-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="1e300-147">Accedere al pannello di accesso e verificare se è possibile **avviare** le applicazioni con accesso SSO basato su password.</span><span class="sxs-lookup"><span data-stu-id="1e300-147">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="1e300-148">È anche possibile scaricare l'estensione per Chrome e Firefox dai collegamenti diretti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1e300-148">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="1e300-149">Estensione Pannello di accesso per Chrome</span><span class="sxs-lookup"><span data-stu-id="1e300-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="1e300-150">Estensione Pannello di accesso per Firefox</span><span class="sxs-lookup"><span data-stu-id="1e300-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="1e300-151">Come configurare un accesso Single Sign-On basato su password per un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e300-151">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="1e300-152">Per configurare un'applicazione della raccolta di Azure AD è necessario:</span><span class="sxs-lookup"><span data-stu-id="1e300-152">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="1e300-153">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e300-153">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="1e300-154">Configurare l'applicazione con l'accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="1e300-154">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="1e300-155">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e300-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="1e300-156">Per aggiungere un'applicazione dalla raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1e300-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="1e300-157">Aprire il [portale di Azure](https://portal.azure.com) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="1e300-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="1e300-158">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1e300-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1e300-159">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e300-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1e300-160">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1e300-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1e300-161">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1e300-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="1e300-162">Nella casella di testo **Immettere un nome** della sezione **Aggiungi dalla raccolta** digitare il nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e300-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="1e300-163">Selezionare l'applicazione che si vuole configurare con l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1e300-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="1e300-164">Prima di aggiungere l'applicazione, è possibile modificarne il nome usando la casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="1e300-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="1e300-165">Fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e300-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="1e300-166">Dopo un breve periodo di tempo sarà possibile visualizzare il pannello di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e300-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="1e300-167">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="1e300-167">Configure the application for password single sign-on</span></span>

<span data-ttu-id="1e300-168">Per configurare un accesso Single Sign-On per un'applicazione, seguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1e300-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="1e300-169">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="1e300-169">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1e300-170">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1e300-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1e300-171">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e300-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1e300-172">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1e300-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1e300-173">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1e300-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="1e300-174">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1e300-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1e300-175">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1e300-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="1e300-176">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e300-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1e300-177">Selezionare la modalità **Accesso basato su password**.</span><span class="sxs-lookup"><span data-stu-id="1e300-177">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="1e300-178">[Assegnare gli utenti all'applicazione](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="1e300-178">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="1e300-179">È anche possibile specificare le credenziali per conto dell'utente selezionando le righe degli utenti e facendo clic su **Aggiorna credenziali**, quindi immettendo il nome utente e la password per conto degli utenti.</span><span class="sxs-lookup"><span data-stu-id="1e300-179">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="1e300-180">In caso contrario, verrà richiesto agli utenti di immettere le credenziali all'avvio.</span><span class="sxs-lookup"><span data-stu-id="1e300-180">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="1e300-181">Come configurare l'accesso Single Sign-On basato su password per un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="1e300-181">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="1e300-182">Per configurare un'applicazione della raccolta di Azure AD è necessario:</span><span class="sxs-lookup"><span data-stu-id="1e300-182">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="1e300-183">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="1e300-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="1e300-184">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="1e300-184">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="1e300-185">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="1e300-185">Add a non-gallery application</span></span>

<span data-ttu-id="1e300-186">Per aggiungere un'applicazione dalla raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1e300-186">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="1e300-187">Aprire il [portale di Azure](https://portal.azure.com) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="1e300-187">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="1e300-188">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1e300-188">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1e300-189">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e300-189">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1e300-190">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1e300-190">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1e300-191">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1e300-191">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="1e300-192">Fare clic su**Applicazione non nella raccolta**.</span><span class="sxs-lookup"><span data-stu-id="1e300-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="1e300-193">Immettere il nome dell'applicazione nella casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="1e300-193">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="1e300-194">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1e300-194">Select **Add.**</span></span>

<span data-ttu-id="1e300-195">Dopo un breve periodo di tempo, sarà possibile visualizzare il pannello di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e300-195">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="1e300-196">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="1e300-196">Configure the application for password single sign-on</span></span>

<span data-ttu-id="1e300-197">Per configurare un accesso Single Sign-On per un'applicazione, seguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1e300-197">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="1e300-198">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="1e300-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1e300-199">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1e300-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1e300-200">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e300-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1e300-201">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1e300-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1e300-202">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1e300-202">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="1e300-203">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1e300-203">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1e300-204">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1e300-204">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="1e300-205">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e300-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1e300-206">Selezionare la modalità **Accesso basato su password**.</span><span class="sxs-lookup"><span data-stu-id="1e300-206">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="1e300-207">Immettere l'**URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="1e300-207">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="1e300-208">Questo è l'URL in cui gli utenti immettono il nome utente e la password per accedere.</span><span class="sxs-lookup"><span data-stu-id="1e300-208">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="1e300-209">Verificare che i campi di accesso siano visibili nell'URL.</span><span class="sxs-lookup"><span data-stu-id="1e300-209">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="1e300-210">Assegnare gli utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e300-210">Assign users to the application.</span></span>

11. <span data-ttu-id="1e300-211">È anche possibile specificare le credenziali per conto dell'utente selezionando le righe degli utenti e facendo clic su **Aggiorna credenziali**, quindi immettendo il nome utente e la password per conto degli utenti.</span><span class="sxs-lookup"><span data-stu-id="1e300-211">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="1e300-212">In caso contrario, verrà richiesto agli utenti di immettere le credenziali all'avvio.</span><span class="sxs-lookup"><span data-stu-id="1e300-212">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="1e300-213">Come assegnare un utente direttamente a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="1e300-213">How to assign a user to an application directly</span></span>

<span data-ttu-id="1e300-214">Per assegnare uno o più utenti direttamente a un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1e300-214">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="1e300-215">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1e300-215">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1e300-216">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1e300-216">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1e300-217">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e300-217">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1e300-218">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1e300-218">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1e300-219">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1e300-219">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="1e300-220">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1e300-220">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1e300-221">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="1e300-221">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="1e300-222">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e300-222">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1e300-223">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1e300-223">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="1e300-224">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1e300-224">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="1e300-225">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo**  o l'**indirizzo di posta elettronica** dell'utente oggetto dell'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="1e300-225">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="1e300-226">Passare il puntatore sull'**utente** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="1e300-226">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="1e300-227">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo dell'utente per aggiungere l'utente all'elenco **Selezionato**.</span><span class="sxs-lookup"><span data-stu-id="1e300-227">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="1e300-228">**Facoltativo:** se si vuole **aggiungere più di un utente**, digitare un altro **nome completo** o **indirizzo di posta elettronica** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere l'utente all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="1e300-228">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="1e300-229">Dopo avere selezionato gli utenti, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e300-229">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="1e300-230">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="1e300-230">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="1e300-231">Fare clic sul pulsante **Assegna** per assegnare l'applicazione agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="1e300-231">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="1e300-232">Dopo un breve periodo di tempo, gli utenti selezionati saranno in grado di avviare queste applicazioni nel pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1e300-232">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="1e300-233">Se questi passaggi di risoluzione dei problemi non risolvono il problema</span><span class="sxs-lookup"><span data-stu-id="1e300-233">If these troubleshooting steps do not the resolve the issue.</span></span> 

<span data-ttu-id="1e300-234">Aprire un ticket di supporto con le informazioni seguenti, se disponibili:</span><span class="sxs-lookup"><span data-stu-id="1e300-234">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="1e300-235">ID errore di correlazione</span><span class="sxs-lookup"><span data-stu-id="1e300-235">Correlation error ID</span></span>

-   <span data-ttu-id="1e300-236">UPN (indirizzo di posta elettronica dell'utente)</span><span class="sxs-lookup"><span data-stu-id="1e300-236">UPN (user email address)</span></span>

-   <span data-ttu-id="1e300-237">ID tenant</span><span class="sxs-lookup"><span data-stu-id="1e300-237">TenantID</span></span>

-   <span data-ttu-id="1e300-238">Tipo di browser</span><span class="sxs-lookup"><span data-stu-id="1e300-238">Browser type</span></span>

-   <span data-ttu-id="1e300-239">Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore</span><span class="sxs-lookup"><span data-stu-id="1e300-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="1e300-240">Tracce Fiddler</span><span class="sxs-lookup"><span data-stu-id="1e300-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e300-241">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e300-241">Next steps</span></span>
[<span data-ttu-id="1e300-242">Fornire l'accesso Single Sign-On alle app con il proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="1e300-242">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
