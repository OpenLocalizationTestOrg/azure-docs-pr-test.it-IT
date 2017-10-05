---
title: Come configurare un accesso Single Sign-On basato su password per un'applicazione non inclusa nella raccolta | Microsoft Docs
description: "Come configurare un'applicazione personalizzata per un accesso Single Sign-On sicuro basato su password quando non è elencata nella raccolta delle applicazioni di Azure AD"
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
ms.openlocfilehash: f629ec99824199306ebf825901beaa99d83d434d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="36c79-103">Come configurare un accesso Single Sign-On basato su password per un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="36c79-103">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="36c79-104">Oltre alle applicazioni della raccolta di Azure AD, è anche possibile aggiungere un'**applicazione non inclusa nella raccolta**.</span><span class="sxs-lookup"><span data-stu-id="36c79-104">In addition to the choices found within the Azure AD Application Gallery, you also have the option to add a **non-gallery application** when the application you want is not listed there.</span></span> <span data-ttu-id="36c79-105">Tramite questa funzionalità, è possibile aggiungere qualsiasi applicazione che esiste già nell'organizzazione o qualsiasi applicazione di terze parti che potrebbe essere usata da un fornitore che non fa parte della [raccolta di applicazioni di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="36c79-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="36c79-106">Dopo aver aggiunto un'applicazione non inclusa nella raccolta, è possibile configurare il metodo Single Sign-On usato da questa applicazione selezionando l'elemento di navigazione **Single Sign-On** in un'applicazione aziendale nel [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="36c79-106">Once you add a non-gallery application, you can then configure the Single sign-on method this application uses by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="36c79-107">Uno dei metodi di accesso disponibili è l'opzione [Accesso Single Sign-On basato su password](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="36c79-107">One of the Single Sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="36c79-108">Con il metodo di **aggiungere un'applicazione non inclusa nella raccolta**, è possibile integrare qualsiasi applicazione che usa un campo di input per il nome utente e la password basati su HTML, anche se non è inclusa nel set di applicazioni preintegrate.</span><span class="sxs-lookup"><span data-stu-id="36c79-108">With the **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="36c79-109">A tale scopo viene usata una tecnologia di scraping delle pagine che fa parte dell'estensione del pannello di accesso. Ciò consente di rilevare automaticamente i campi di input di nome utente e password e archiviarli in modo sicuro per l'istanza dell'applicazione specifica.</span><span class="sxs-lookup"><span data-stu-id="36c79-109">The way this works is by a page scraping technology that is part of the Access Panel extension that allows us to auto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="36c79-110">Eseguire quindi in modo sicuro la riproduzione di nomi utente e password per tali campi quando un utente passa all'applicazione nel pannello di accesso dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="36c79-110">Then securely replay usernames and passwords to those fields when a user navigates to that application on the application access panel.</span></span>

<span data-ttu-id="36c79-111">Questo è un modo efficace per iniziare rapidamente l'integrazione di qualsiasi tipo di applicazione in Azure AD e consente di:</span><span class="sxs-lookup"><span data-stu-id="36c79-111">This is a great way to get started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="36c79-112">Integrare **qualsiasi applicazione disponibile** con il tenant di Azure AD, se usa un campo di input di nome utente e password in formato HTML</span><span class="sxs-lookup"><span data-stu-id="36c79-112">Integrate **any application in the world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="36c79-113">Abilitare l'**accesso Single Sign-On per gli utenti** archiviando e riproducendo in modo sicuro i nomi utente e password per l'applicazione integrata con Azure AD</span><span class="sxs-lookup"><span data-stu-id="36c79-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="36c79-114">**Rilevare automaticamente i campi di input** per qualsiasi applicazione e rilevare manualmente tali campi usando l'estensione del browser per il pannello di accesso, non vengono trovati dal rilevamento automatico</span><span class="sxs-lookup"><span data-stu-id="36c79-114">**Auto-detect input** fields for any application and allow you to manually detect those fields using the Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="36c79-115">**Supportare applicazioni che richiedono più campi di accesso** per applicazioni che richiedono non solo i campi di nome utente e password per accedere</span><span class="sxs-lookup"><span data-stu-id="36c79-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="36c79-116">**Personalizzare le etichette** dei campi di input di nome utente e password visualizzati nel [pannello di accesso all'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) quando si immettono le credenziali</span><span class="sxs-lookup"><span data-stu-id="36c79-116">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="36c79-117">Consentire agli **utenti** di immettere i nomi utente e le password per tutti gli account di applicazioni esistenti digitati manualmente nel [pannello di accesso all'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="36c79-117">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="36c79-118">Consentire a un **membro del gruppo aziendale** di specificare i nome utente e le password assegnati a un utente tramite la funzionalità di [accesso all'applicazione self-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)</span><span class="sxs-lookup"><span data-stu-id="36c79-118">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="36c79-119">Consentire a un **amministratore** di specificare i nomi utente e le password assegnati a un utente tramite la funzionalità di credenziali di aggiornamento quando [viene assegnato un utente a un'applicazione](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="36c79-119">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="36c79-120">Consentire un **amministratore** di specificare i nomi utente e le password condivisi usati da un gruppo di utenti tramite la funzionalità di credenziali di aggiornamento quando [viene assegnato un gruppo a un'applicazione](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="36c79-120">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="36c79-121">Di seguito viene illustrato come abilitare l'[accesso Single Sign-On basato su password](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) per un'applicazione aggiunta usando il metodo di **aggiungere un'applicazione non inclusa nella raccolta**.</span><span class="sxs-lookup"><span data-stu-id="36c79-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to any application that you add using the **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="36c79-122">Panoramica dei passaggi necessari</span><span class="sxs-lookup"><span data-stu-id="36c79-122">Overview of steps required</span></span>

<span data-ttu-id="36c79-123">Per configurare un'applicazione della raccolta di Azure AD è necessario:</span><span class="sxs-lookup"><span data-stu-id="36c79-123">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="36c79-124">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="36c79-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="36c79-125">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="36c79-125">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="36c79-126">Assegnare l'applicazione a un utente o un gruppo</span><span class="sxs-lookup"><span data-stu-id="36c79-126">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="36c79-127">Assegnare un utente direttamente a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="36c79-127">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="36c79-128">Assegnare un'applicazione direttamente a un gruppo </span><span class="sxs-lookup"><span data-stu-id="36c79-128">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="36c79-129">Aggiungere un'applicazione non inclusa nella raccolta</span><span class="sxs-lookup"><span data-stu-id="36c79-129">Add a non-gallery application</span></span>

<span data-ttu-id="36c79-130">Per aggiungere un'applicazione dalla raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="36c79-130">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="36c79-131">Aprire il [portale di Azure](https://portal.azure.com) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="36c79-131">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="36c79-132">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="36c79-132">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="36c79-133">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36c79-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="36c79-134">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36c79-134">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="36c79-135">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="36c79-135">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="36c79-136">Fare clic su**Applicazione non nella raccolta**.</span><span class="sxs-lookup"><span data-stu-id="36c79-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="36c79-137">Immettere il nome dell'applicazione nella casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="36c79-137">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="36c79-138">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="36c79-138">Select **Add.**</span></span>

<span data-ttu-id="36c79-139">Dopo un breve periodo di tempo, sarà possibile visualizzare il pannello di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="36c79-139">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="36c79-140">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="36c79-140">Configure the application for password single sign-on</span></span>

<span data-ttu-id="36c79-141">Per configurare un accesso Single Sign-On per un'applicazione, seguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="36c79-141">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="36c79-142">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="36c79-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="36c79-143">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="36c79-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="36c79-144">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36c79-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="36c79-145">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36c79-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="36c79-146">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="36c79-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="36c79-147">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="36c79-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="36c79-148">Selezionare l'applicazione per cui si vuole configurare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="36c79-148">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="36c79-149">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="36c79-149">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="36c79-150">Selezionare la modalità **Accesso basato su password**.</span><span class="sxs-lookup"><span data-stu-id="36c79-150">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="36c79-151">Immettere l'**URL di accesso**.</span><span class="sxs-lookup"><span data-stu-id="36c79-151">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="36c79-152">Questo è l'URL in cui gli utenti immettono il nome utente e la password per accedere.</span><span class="sxs-lookup"><span data-stu-id="36c79-152">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="36c79-153">Verificare che i campi di accesso siano visibili nell'URL.</span><span class="sxs-lookup"><span data-stu-id="36c79-153">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="36c79-154">Assegnare gli utenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="36c79-154">Assign users to the application.</span></span>

11. <span data-ttu-id="36c79-155">È anche possibile specificare le credenziali per conto dell'utente selezionando le righe degli utenti e facendo clic su **Aggiorna credenziali**, quindi immettendo il nome utente e la password per conto degli utenti.</span><span class="sxs-lookup"><span data-stu-id="36c79-155">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="36c79-156">In caso contrario, verrà richiesto agli utenti di immettere le credenziali all'avvio.</span><span class="sxs-lookup"><span data-stu-id="36c79-156">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="36c79-157">Assegnare un utente direttamente a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="36c79-157">Assign a user to an application directly</span></span>

<span data-ttu-id="36c79-158">Per assegnare uno o più utenti direttamente a un'applicazione, seguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="36c79-158">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="36c79-159">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="36c79-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="36c79-160">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="36c79-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="36c79-161">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36c79-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="36c79-162">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36c79-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="36c79-163">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="36c79-163">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="36c79-164">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="36c79-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="36c79-165">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="36c79-165">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="36c79-166">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="36c79-166">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="36c79-167">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="36c79-167">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="36c79-168">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="36c79-168">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="36c79-169">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo**  o l'**indirizzo di posta elettronica** dell'utente oggetto dell'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="36c79-169">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="36c79-170">Passare il puntatore sull'**utente** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="36c79-170">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="36c79-171">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo dell'utente per aggiungere l'utente all'elenco **Selezionato**.</span><span class="sxs-lookup"><span data-stu-id="36c79-171">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="36c79-172">**Facoltativo:** se si vuole **aggiungere più di un utente**, digitare un altro **nome completo** o **indirizzo di posta elettronica** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere l'utente all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="36c79-172">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="36c79-173">Dopo avere selezionato gli utenti, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="36c79-173">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="36c79-174">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="36c79-174">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="36c79-175">Fare clic sul pulsante **Assegna** per assegnare l'applicazione agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="36c79-175">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="36c79-176">Assegnare un'applicazione direttamente a un gruppo</span><span class="sxs-lookup"><span data-stu-id="36c79-176">Assign an application to a group directly</span></span>

<span data-ttu-id="36c79-177">Per assegnare uno o più gruppi direttamente a un'applicazione, seguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="36c79-177">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="36c79-178">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="36c79-178">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="36c79-179">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="36c79-179">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="36c79-180">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36c79-180">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="36c79-181">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36c79-181">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="36c79-182">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="36c79-182">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="36c79-183">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="36c79-183">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="36c79-184">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="36c79-184">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="36c79-185">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="36c79-185">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="36c79-186">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="36c79-186">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="36c79-187">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="36c79-187">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="36c79-188">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo del gruppo** a cui si vuole eseguire l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="36c79-188">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="36c79-189">Posizionare il puntatore sul **gruppo** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="36c79-189">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="36c79-190">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo del gruppo per aggiungere il gruppo all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="36c79-190">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="36c79-191">**Facoltativo:** se si vuole **aggiungere più di un gruppo**, digitare un altro **nome completo di gruppo** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere il gruppo all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="36c79-191">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="36c79-192">Dopo avere selezionato i gruppi, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="36c79-192">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="36c79-193">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare ai gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="36c79-193">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="36c79-194">Fare clic sul pulsante **Assegna** per assegnare l'applicazione ai gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="36c79-194">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="36c79-195">Dopo un breve periodo di tempo, gli utenti selezionati saranno in grado di avviare queste applicazioni nel riquadro di accesso.</span><span class="sxs-lookup"><span data-stu-id="36c79-195">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36c79-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="36c79-196">Next steps</span></span>
[<span data-ttu-id="36c79-197">Fornire l'accesso Single Sign-On alle app con il proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="36c79-197">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
