---
title: Come configurare un accesso Single Sign-On basato su password per un'applicazione della raccolta di Azure AD | Microsoft Docs
description: "Come configurare un'applicazione con un accesso Single Sign-On sicuro basato su password quando è già elencata nella raccolta delle applicazioni di Azure AD"
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
ms.openlocfilehash: d4dc110eb25c3e550ac4663d28e626a696b58f62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="afa5e-103">Come configurare un accesso Single Sign-On basato su password per un'applicazione della raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa5e-103">How to configure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="afa5e-104">Quando si aggiunge un'applicazione della [raccolta di applicazioni di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), è possibile scegliere come gli utenti accedono a tale applicazione.</span><span class="sxs-lookup"><span data-stu-id="afa5e-104">When you add an application from the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have the choice of how you want your users to sign in to that application.</span></span> <span data-ttu-id="afa5e-105">È possibile configurare questa opzione in qualsiasi momento selezionando l'elemento di navigazione **Single Sign-On** in un'applicazione aziendale nel [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="afa5e-105">You can configure this choice at any time by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="afa5e-106">Uno dei metodi di accesso disponibili è l'opzione [Accesso Single Sign-On basato su password](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="afa5e-106">One of the single sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="afa5e-107">Questo metodo è efficace per iniziare rapidamente l'integrazione di applicazioni in Azure AD e consente di:</span><span class="sxs-lookup"><span data-stu-id="afa5e-107">This is a great way to get started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="afa5e-108">Abilitare l'**accesso Single Sign-On per gli utenti** archiviando e riproducendo in modo sicuro i nomi utente e password per l'applicazione integrata con Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa5e-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="afa5e-109">**Supportare applicazioni che richiedono più campi di accesso** per applicazioni che richiedono non solo i campi di nome utente e password per accedere</span><span class="sxs-lookup"><span data-stu-id="afa5e-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="afa5e-110">**Personalizzare le etichette** dei campi di input di nome utente e password visualizzati nel [pannello di accesso all'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) quando si immettono le credenziali</span><span class="sxs-lookup"><span data-stu-id="afa5e-110">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="afa5e-111">Consentire agli **utenti** di immettere i nomi utente e le password per tutti gli account di applicazioni esistenti digitati manualmente nel [pannello di accesso all'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="afa5e-111">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="afa5e-112">Consentire a un **membro del gruppo aziendale** di specificare i nome utente e le password assegnati a un utente tramite la funzionalità di [accesso all'applicazione self-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)</span><span class="sxs-lookup"><span data-stu-id="afa5e-112">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="afa5e-113">Consentire a un **amministratore** di specificare i nomi utente e le password assegnati a un utente tramite la funzionalità di credenziali di aggiornamento quando [viene assegnato un utente a un'applicazione](#assign-a-user-to-an-application-directly)</span><span class="sxs-lookup"><span data-stu-id="afa5e-113">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="afa5e-114">Consentire un **amministratore** di specificare i nomi utente e le password condivisi usati da un gruppo di utenti tramite la funzionalità di credenziali di aggiornamento quando [viene assegnato un gruppo a un'applicazione](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="afa5e-114">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="afa5e-115">Di seguito viene illustrato come abilitare l'[accesso Single Sign-On basato su password](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) per un'applicazione che si trova già nella [raccolta di applicazioni di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="afa5e-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to an application that is already in the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="afa5e-116">Panoramica dei passaggi necessari</span><span class="sxs-lookup"><span data-stu-id="afa5e-116">Overview of steps required</span></span>
<span data-ttu-id="afa5e-117">Per configurare un'applicazione della raccolta di Azure AD è necessario:</span><span class="sxs-lookup"><span data-stu-id="afa5e-117">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="afa5e-118">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa5e-118">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="afa5e-119">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="afa5e-119">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="afa5e-120">Assegnare l'applicazione a un utente o un gruppo</span><span class="sxs-lookup"><span data-stu-id="afa5e-120">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="afa5e-121">Assegnare un utente direttamente a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="afa5e-121">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="afa5e-122">Assegnare un'applicazione direttamente a un gruppo </span><span class="sxs-lookup"><span data-stu-id="afa5e-122">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="afa5e-123">Aggiungere un'applicazione dalla raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa5e-123">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="afa5e-124">Per aggiungere un'applicazione dalla raccolta di Azure AD, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="afa5e-124">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="afa5e-125">Aprire il [portale di Azure](https://portal.azure.com) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-125">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="afa5e-126">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="afa5e-126">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="afa5e-127">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-127">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="afa5e-128">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="afa5e-128">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="afa5e-129">Fare clic sul pulsante **Aggiungi** nell'angolo superiore destro del pannello **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-129">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="afa5e-130">Nella casella di testo **Immettere un nome** della sezione **Aggiungi dalla raccolta** digitare il nome dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="afa5e-130">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="afa5e-131">Selezionare l'applicazione che si vuole configurare per un accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="afa5e-131">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="afa5e-132">Prima di aggiungere l'applicazione, è possibile modificarne il nome dalla casella di testo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-132">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="afa5e-133">Fare clic sul pulsante **Aggiungi** per aggiungere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="afa5e-133">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="afa5e-134">Dopo un breve periodo di tempo sarà possibile visualizzare il pannello di configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="afa5e-134">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="afa5e-135">Configurare l'applicazione per un accesso Single Sign-On basato su password</span><span class="sxs-lookup"><span data-stu-id="afa5e-135">Configure the application for password single sign-on</span></span>

<span data-ttu-id="afa5e-136">Per configurare un accesso Single Sign-On per un'applicazione, seguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="afa5e-136">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="afa5e-137">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale** o **Coamministratore**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-137">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="afa5e-138">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="afa5e-138">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="afa5e-139">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-139">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="afa5e-140">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="afa5e-140">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="afa5e-141">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="afa5e-141">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="afa5e-142">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'**elenco di tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-142">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="afa5e-143">Selezionare l'applicazione per cui si vuole configurare un accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="afa5e-143">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="afa5e-144">Dopo il caricamento dell'applicazione, fare clic su **Single Sign-On** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="afa5e-144">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="afa5e-145">Selezionare la modalità **Accesso basato su password**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-145">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="afa5e-146">[Assegnare gli utenti all'applicazione](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="afa5e-146">[Assign users to the application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="afa5e-147">È anche possibile specificare le credenziali per conto dell'utente selezionando le righe degli utenti e facendo clic su **Aggiorna credenziali**, quindi immettendo il nome utente e la password per conto degli utenti.</span><span class="sxs-lookup"><span data-stu-id="afa5e-147">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="afa5e-148">In caso contrario, verrà richiesto agli utenti di immettere le credenziali all'avvio.</span><span class="sxs-lookup"><span data-stu-id="afa5e-148">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="afa5e-149">Assegnare un utente direttamente a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="afa5e-149">Assign a user to an application directly</span></span>

<span data-ttu-id="afa5e-150">Per assegnare uno o più utenti direttamente a un'applicazione, seguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="afa5e-150">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="afa5e-151">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="afa5e-152">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="afa5e-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="afa5e-153">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="afa5e-154">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="afa5e-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="afa5e-155">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="afa5e-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="afa5e-156">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="afa5e-157">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="afa5e-157">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="afa5e-158">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="afa5e-158">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="afa5e-159">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-159">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="afa5e-160">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-160">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="afa5e-161">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo**  o l'**indirizzo di posta elettronica** dell'utente oggetto dell'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="afa5e-161">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="afa5e-162">Passare il puntatore sull'**utente** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-162">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="afa5e-163">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo dell'utente per aggiungere l'utente all'elenco **Selezionato**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-163">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="afa5e-164">**Facoltativo:** se si vuole **aggiungere più di un utente**, digitare un altro **nome completo** o **indirizzo di posta elettronica** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere l'utente all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-164">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="afa5e-165">Dopo avere selezionato gli utenti, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="afa5e-165">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="afa5e-166">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="afa5e-166">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="afa5e-167">Fare clic sul pulsante **Assegna** per assegnare l'applicazione agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="afa5e-167">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="afa5e-168">Assegnare un'applicazione direttamente a un gruppo</span><span class="sxs-lookup"><span data-stu-id="afa5e-168">Assign an application to a group directly</span></span>

<span data-ttu-id="afa5e-169">Per assegnare uno o più gruppi direttamente a un'applicazione, seguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="afa5e-169">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="afa5e-170">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-170">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="afa5e-171">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="afa5e-171">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="afa5e-172">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-172">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="afa5e-173">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="afa5e-173">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="afa5e-174">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="afa5e-174">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="afa5e-175">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-175">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="afa5e-176">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="afa5e-176">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="afa5e-177">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="afa5e-177">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="afa5e-178">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-178">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="afa5e-179">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-179">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="afa5e-180">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo del gruppo** a cui si vuole eseguire l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="afa5e-180">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="afa5e-181">Posizionare il puntatore sul **gruppo** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-181">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="afa5e-182">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo del gruppo per aggiungere il gruppo all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-182">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="afa5e-183">**Facoltativo:** se si vuole **aggiungere più di un gruppo**, digitare un altro **nome completo di gruppo** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere il gruppo all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="afa5e-183">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="afa5e-184">Dopo avere selezionato i gruppi, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="afa5e-184">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="afa5e-185">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare ai gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="afa5e-185">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="afa5e-186">Fare clic sul pulsante **Assegna** per assegnare l'applicazione ai gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="afa5e-186">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="afa5e-187">Dopo un breve periodo di tempo, gli utenti selezionati saranno in grado di avviare queste applicazioni nel riquadro di accesso.</span><span class="sxs-lookup"><span data-stu-id="afa5e-187">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afa5e-188">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="afa5e-188">Next steps</span></span>
[<span data-ttu-id="afa5e-189">Fornire l'accesso Single Sign-On alle app con il proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="afa5e-189">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
