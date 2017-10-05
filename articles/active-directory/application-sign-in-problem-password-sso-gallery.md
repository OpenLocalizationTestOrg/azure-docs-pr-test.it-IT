---
title: Problemi di accesso a un'applicazione della raccolta di Azure AD configurata per il Single Sign-On federato | Microsoft Docs
description: Come risolvere i problemi relativi a un'applicazione della raccolta di Azure AD configurata per il Single Sign-On basato su password
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
ms.openlocfilehash: f8521d1386bba8004e84fe8862a5f59a65ea19ad
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="1bde7-103">Problemi di accesso a un'applicazione della raccolta di Azure AD configurata per il Single Sign-On federato</span><span class="sxs-lookup"><span data-stu-id="1bde7-103">Problems signing in to an Azure AD Gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="1bde7-104">Il pannello di accesso è un portale basato sul Web che permette a un utente che ha un account aziendale o dell'istituto di istruzione in Azure Active Directory (Azure AD) di visualizzare e avviare applicazioni basate sul cloud a cui l'amministratore di Azure AD ha concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="1bde7-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="1bde7-105">Un utente dotato di edizioni di Azure AD può anche usare le funzionalità di gestione self-service di gruppi e app tramite il pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1bde7-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="1bde7-106">Il pannello di accesso è separato dal portale di Azure e non richiede una sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="1bde7-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="1bde7-107">Per usare il servizio Single Sign-On (SSO) basato su password nel pannello di accesso, è necessario installare l'estensione del pannello di accesso nel browser dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1bde7-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="1bde7-108">Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.</span><span class="sxs-lookup"><span data-stu-id="1bde7-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="1bde7-109">Applicazione dei requisiti del browser per il pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="1bde7-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="1bde7-110">Per il pannello di accesso è necessario un browser che supporti JavaScript e in cui sia abilitato CSS.</span><span class="sxs-lookup"><span data-stu-id="1bde7-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="1bde7-111">Per usare il servizio Single Sign-On (SSO) basato su password nel pannello di accesso, è necessario installare l'estensione del pannello di accesso nel browser dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1bde7-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="1bde7-112">Questa estensione viene scaricata automaticamente quando un utente seleziona un'applicazione configurata per il servizio Single Sign-On basato su password.</span><span class="sxs-lookup"><span data-stu-id="1bde7-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="1bde7-113">Per l'accesso Single Sign-On basato su password il browser dell'utente finale può essere uno dei seguenti:</span><span class="sxs-lookup"><span data-stu-id="1bde7-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="1bde7-114">Internet Explorer 8, 9, 10, 11 su Windows 7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="1bde7-114">Internet Explorer 8, 9, 10, 11 - on Windows 7 or later</span></span>

-   <span data-ttu-id="1bde7-115">Chrome in Windows 7 o versione successiva e MacOS X o versione successiva</span><span class="sxs-lookup"><span data-stu-id="1bde7-115">Chrome - on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="1bde7-116">Firefox 26.0 o versione successiva in Windows XP SP2 o versione successiva e in Mac OS X 10.6 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="1bde7-116">Firefox 26.0 or later - on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="1bde7-117">L'estensione SSO basata su password sarà disponibile per Edge in Windows 10 quando le estensioni del browser saranno supportate per Edge.</span><span class="sxs-lookup"><span data-stu-id="1bde7-117">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="1bde7-118">Come installare l'estensione del browser per il pannello di accesso</span><span class="sxs-lookup"><span data-stu-id="1bde7-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="1bde7-119">Per installare l'estensione del browser per il pannello di accesso, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1bde7-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="1bde7-120">Aprire il [pannello di accesso](https://myapps.microsoft.com) in uno dei browser supportati e accedere come **utente** ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1bde7-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="1bde7-121">Fare clic su un'**applicazione con accesso SSO basato su password** nel pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1bde7-121">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="1bde7-122">Quando viene richiesto di installare il software, selezionare **Installa ora**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="1bde7-123">A seconda del browser in uso, si verrà indirizzati al collegamento per il download.</span><span class="sxs-lookup"><span data-stu-id="1bde7-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="1bde7-124">**Aggiungere** l'estensione al browser.</span><span class="sxs-lookup"><span data-stu-id="1bde7-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="1bde7-125">Se richiesto dal browser, scegliere se **abilitare** o **consentire** l'uso dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="1bde7-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="1bde7-126">Al termine dell'installazione, **riavviare** la sessione del browser.</span><span class="sxs-lookup"><span data-stu-id="1bde7-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="1bde7-127">Accedere al pannello di accesso e verificare se è possibile **avviare** le applicazioni con accesso SSO basato su password.</span><span class="sxs-lookup"><span data-stu-id="1bde7-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="1bde7-128">È anche possibile scaricare l'estensione per Chrome e Firefox dai collegamenti diretti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1bde7-128">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="1bde7-129">Estensione Pannello di accesso per Chrome</span><span class="sxs-lookup"><span data-stu-id="1bde7-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="1bde7-130">Estensione Pannello di accesso per Firefox</span><span class="sxs-lookup"><span data-stu-id="1bde7-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="1bde7-131">Impostazione dei Criteri di gruppo per Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="1bde7-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="1bde7-132">È possibile impostare Criteri di gruppo che consentono di installare l'estensione del pannello di accesso per Internet Explorer nei computer degli utenti in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="1bde7-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="1bde7-133">I prerequisiti includono:</span><span class="sxs-lookup"><span data-stu-id="1bde7-133">The prerequisites include:</span></span>

-   <span data-ttu-id="1bde7-134">[Servizi di dominio Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)è già stato configurato e i computer degli utenti sono stati aggiunti al dominio.</span><span class="sxs-lookup"><span data-stu-id="1bde7-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="1bde7-135">Per modificare l'oggetto Criteri di gruppo è necessaria l'autorizzazione "Modifica impostazione".</span><span class="sxs-lookup"><span data-stu-id="1bde7-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="1bde7-136">Questa autorizzazione è assegnata per impostazione predefinita ai membri dei gruppi di sicurezza seguenti: Domain Administrators, Enterprise Administrators e Group Policy Creator Owners.</span><span class="sxs-lookup"><span data-stu-id="1bde7-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="1bde7-137">[Altre informazioni](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="1bde7-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="1bde7-138">Per istruzioni passo passo su come configurare i Criteri di gruppo e distribuirli agli utenti, seguire l'esercitazione [Come distribuire l'estensione Pannello di accesso per Internet Explorer con Criteri di gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy).</span><span class="sxs-lookup"><span data-stu-id="1bde7-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="1bde7-139">Risoluzione dei problemi del pannello di accesso in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="1bde7-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="1bde7-140">Per accedere a uno strumento diagnostico e per istruzioni passo passo sulla configurazione dell'estensione per IE, seguire la procedura nella sezione sulla [risoluzione dei problemi relativi all'estensione del pannello di accesso per Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="1bde7-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="1bde7-141">Come configurare un accesso Single Sign-On basato su password per un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bde7-141">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="1bde7-142">Per configurare un'applicazione della raccolta di Azure AD è necessario:</span><span class="sxs-lookup"><span data-stu-id="1bde7-142">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="1bde7-143">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bde7-143">Add an application from the Azure AD gallery</span></span>](#_Add_an_application)

-   [<span data-ttu-id="1bde7-144">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="1bde7-144">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="1bde7-145">Assegnare gli utenti all'applicazione</span><span class="sxs-lookup"><span data-stu-id="1bde7-145">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="1bde7-146">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bde7-146">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="1bde7-147">Per aggiungere un'applicazione dalla raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1bde7-147">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="1bde7-148">Aprire il [portale di Azure](https://portal.azure.com) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-148">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="1bde7-149">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1bde7-149">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1bde7-150">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-150">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1bde7-151">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1bde7-151">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1bde7-152">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-152">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="1bde7-153">Nella casella di testo **Immettere un nome** della sezione **Aggiungi dalla raccolta** digitare il nome dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bde7-153">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="1bde7-154">Selezionare l'applicazione che si vuole configurare con l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1bde7-154">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="1bde7-155">Prima di aggiungere l'applicazione, è possibile modificarne il nome usando la casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-155">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="1bde7-156">Fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bde7-156">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="1bde7-157">Dopo un breve periodo di tempo sarà possibile visualizzare il pannello di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bde7-157">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="1bde7-158">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="1bde7-158">Configure the application for password single sign-on</span></span>

<span data-ttu-id="1bde7-159">Per configurare un accesso Single Sign-On per un'applicazione, seguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1bde7-159">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="1bde7-160">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-160">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1bde7-161">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1bde7-161">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1bde7-162">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-162">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1bde7-163">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1bde7-163">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1bde7-164">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1bde7-164">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="1bde7-165">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'**elenco di tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-165">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1bde7-166">Selezionare l'applicazione per cui si vuole configurare un accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1bde7-166">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="1bde7-167">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bde7-167">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1bde7-168">Selezionare la modalità **Accesso basato su password**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-168">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="1bde7-169">[Assegnare gli utenti all'applicazione](#_How_to_assign).</span><span class="sxs-lookup"><span data-stu-id="1bde7-169">[Assign users to the application](#_How_to_assign).</span></span>

10. <span data-ttu-id="1bde7-170">È anche possibile specificare le credenziali per conto dell'utente selezionando le righe degli utenti e facendo clic su **Aggiorna credenziali**, quindi immettendo il nome utente e la password per conto degli utenti.</span><span class="sxs-lookup"><span data-stu-id="1bde7-170">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="1bde7-171">In caso contrario, verrà richiesto agli utenti di immettere le credenziali all'avvio.</span><span class="sxs-lookup"><span data-stu-id="1bde7-171">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="assign-users-to-the-application"></a><span data-ttu-id="1bde7-172">Assegnare gli utenti all'applicazione</span><span class="sxs-lookup"><span data-stu-id="1bde7-172">Assign users to the application</span></span>

<span data-ttu-id="1bde7-173">Per assegnare uno o più utenti direttamente a un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1bde7-173">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="1bde7-174">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-174">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1bde7-175">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1bde7-175">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1bde7-176">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-176">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1bde7-177">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1bde7-177">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1bde7-178">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1bde7-178">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="1bde7-179">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-179">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1bde7-180">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="1bde7-180">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="1bde7-181">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bde7-181">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1bde7-182">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-182">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="1bde7-183">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-183">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="1bde7-184">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo**  o l'**indirizzo di posta elettronica** dell'utente oggetto dell'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="1bde7-184">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="1bde7-185">Passare il puntatore sull'**utente** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-185">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="1bde7-186">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo dell'utente per aggiungere l'utente all'elenco **Selezionato**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-186">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="1bde7-187">**Facoltativo:** se si vuole **aggiungere più di un utente**, digitare un altro **nome completo** o **indirizzo di posta elettronica** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere l'utente all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="1bde7-187">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="1bde7-188">Dopo avere selezionato gli utenti, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bde7-188">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="1bde7-189">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="1bde7-189">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="1bde7-190">Fare clic sul pulsante **Assegna** per assegnare l'applicazione agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="1bde7-190">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="1bde7-191">Dopo un breve periodo di tempo, gli utenti selezionati saranno in grado di avviare queste applicazioni nel pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1bde7-191">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshoot-steps-dont-resolve-the-issue"></a><span data-ttu-id="1bde7-192">Se questi passaggi per la risoluzione dei problemi non risolvono il problema</span><span class="sxs-lookup"><span data-stu-id="1bde7-192">If these troubleshoot steps don't resolve the issue</span></span> 
<span data-ttu-id="1bde7-193">Aprire un ticket di supporto con le informazioni seguenti, se disponibili:</span><span class="sxs-lookup"><span data-stu-id="1bde7-193">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="1bde7-194">ID errore di correlazione</span><span class="sxs-lookup"><span data-stu-id="1bde7-194">Correlation error ID</span></span>

-   <span data-ttu-id="1bde7-195">UPN (indirizzo di posta elettronica dell'utente)</span><span class="sxs-lookup"><span data-stu-id="1bde7-195">UPN (user email address)</span></span>

-   <span data-ttu-id="1bde7-196">ID tenant</span><span class="sxs-lookup"><span data-stu-id="1bde7-196">TenantID</span></span>

-   <span data-ttu-id="1bde7-197">Tipo di browser</span><span class="sxs-lookup"><span data-stu-id="1bde7-197">Browser type</span></span>

-   <span data-ttu-id="1bde7-198">Fuso orario e ora o intervallo di tempo durante il quale si verifica l'errore</span><span class="sxs-lookup"><span data-stu-id="1bde7-198">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="1bde7-199">Tracce Fiddler</span><span class="sxs-lookup"><span data-stu-id="1bde7-199">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bde7-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1bde7-200">Next steps</span></span>
[<span data-ttu-id="1bde7-201">Fornire l'accesso Single Sign-On alle app con il proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="1bde7-201">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
