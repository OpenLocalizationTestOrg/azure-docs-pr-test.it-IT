---
title: aaaHow tooconfigure password single sign-on per un'applicazione Azure AD raccolta | Documenti Microsoft
description: "Come tooconfigure un'applicazione per proteggere basato su password single sign-on quando è già elencato nella raccolta di applicazioni Azure AD hello"
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
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="1b96b-103">Come password tooconfigure single sign-on per un'applicazione di raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b96b-103">How tooconfigure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="1b96b-104">Quando si aggiunge un'applicazione da hello [raccolta di applicazioni Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), è possibile scegliere di hello di come si desidera il toosign gli utenti nell'applicazione toothat.</span><span class="sxs-lookup"><span data-stu-id="1b96b-104">When you add an application from hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have hello choice of how you want your users toosign in toothat application.</span></span> <span data-ttu-id="1b96b-105">È possibile configurare questa opzione in qualsiasi momento selezionando hello **Single Sign-on** elemento di navigazione in un'applicazione aziendale in hello [portale Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1b96b-105">You can configure this choice at any time by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="1b96b-106">Uno dei tooyou disponibili metodi del servizio single sign-on di hello è hello [basato su Password Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opzione.</span><span class="sxs-lookup"><span data-stu-id="1b96b-106">One of hello single sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="1b96b-107">Questo è un ottimo modo tooget avviato l'integrazione di applicazioni in Azure AD rapidamente e consente di:</span><span class="sxs-lookup"><span data-stu-id="1b96b-107">This is a great way tooget started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="1b96b-108">Abilitare **Single Sign-on per gli utenti** archiviandoli in modo sicuro e riproduzione di nomi utente e password per l'applicazione hello è stata integrata con Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b96b-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="1b96b-109">**Supporto di applicazioni che richiedono più campi Accedi** per applicazioni che richiedono più di un semplice nome utente e password campi toosign in</span><span class="sxs-lookup"><span data-stu-id="1b96b-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="1b96b-110">**Personalizzare le etichette di hello** hello nome utente e password dei campi di input utente di vedere in hello [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) quando si immettono le proprie credenziali</span><span class="sxs-lookup"><span data-stu-id="1b96b-110">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="1b96b-111">Consenti il **utenti** tooprovide i propri nomi utente e password per tutti gli account esistenti dell'applicazione che sta digitando manualmente su hello [Pannello di accesso dell'applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="1b96b-111">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="1b96b-112">Consentire un **membro del gruppo aziendale hello** toospecify hello utente e password utente tooa da assegnato utilizzando hello [accesso all'applicazione Self-Service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) funzionalità</span><span class="sxs-lookup"><span data-stu-id="1b96b-112">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="1b96b-113">Consentire un **amministratore** funzionalità quando i nomi utente hello toospecify e le password assegnate tooa utente con credenziali di aggiornamento hello [l'assegnazione di un'applicazione tooan utente](#assign-a-user-to-an-application-directly)</span><span class="sxs-lookup"><span data-stu-id="1b96b-113">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="1b96b-114">Consentire un **amministratore** toospecify hello condiviso username o password utilizzata da un gruppo di persone con le credenziali di aggiornamento hello funzionalità quando [l'assegnazione di un'applicazione di gruppo tooan](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="1b96b-114">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="1b96b-115">Di seguito viene descritto come abilitare [basato su Password Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan applicazione che è già in hello [raccolta di applicazioni Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="1b96b-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan application that is already in hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="1b96b-116">Panoramica dei passaggi necessari</span><span class="sxs-lookup"><span data-stu-id="1b96b-116">Overview of steps required</span></span>
<span data-ttu-id="1b96b-117">un'applicazione dalla raccolta di Azure AD hello tooconfigure è necessario:</span><span class="sxs-lookup"><span data-stu-id="1b96b-117">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="1b96b-118">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b96b-118">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="1b96b-119">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b96b-119">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="1b96b-120">Assegnare l'utente tooa dell'applicazione hello o un gruppo</span><span class="sxs-lookup"><span data-stu-id="1b96b-120">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="1b96b-121">Assegnare un'applicazione tooan utente direttamente</span><span class="sxs-lookup"><span data-stu-id="1b96b-121">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="1b96b-122">Assegnare un gruppo di applicazioni tooa direttamente</span><span class="sxs-lookup"><span data-stu-id="1b96b-122">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="1b96b-123">Aggiungere un'applicazione hello raccolta di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b96b-123">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="1b96b-124">un'applicazione dalla raccolta di Azure AD, hello tooadd procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="1b96b-124">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="1b96b-125">Aprire hello [portale Azure](https://portal.azure.com) e accedere come un **amministratore globale** o **Co-amministratore**</span><span class="sxs-lookup"><span data-stu-id="1b96b-125">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="1b96b-126">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="1b96b-126">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1b96b-127">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1b96b-127">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1b96b-128">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b96b-128">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1b96b-129">Fare clic su hello **Aggiungi** pulsante nell'angolo superiore destro di hello in hello **applicazioni aziendali** pannello</span><span class="sxs-lookup"><span data-stu-id="1b96b-129">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="1b96b-130">In hello **immettere un nome** casella di testo da hello **Aggiungi dalla raccolta hello** sezione, il nome del tipo hello di un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="1b96b-130">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="1b96b-131">Selezionare l'applicazione hello da tooconfigure per single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b96b-131">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="1b96b-132">Prima di aggiungere un'applicazione hello, è possibile modificarne il nome da hello **nome** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="1b96b-132">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="1b96b-133">Fare clic su **Aggiungi** pulsante, un'applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1b96b-133">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="1b96b-134">Dopo un breve periodo, è il pannello di configurazione dell'applicazione in grado di toosee hello.</span><span class="sxs-lookup"><span data-stu-id="1b96b-134">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="1b96b-135">Configurare un'applicazione hello password single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b96b-135">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="1b96b-136">tooconfigure single sign-on per un'applicazione, attenersi alla procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="1b96b-136">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="1b96b-137">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**</span><span class="sxs-lookup"><span data-stu-id="1b96b-137">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1b96b-138">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="1b96b-138">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1b96b-139">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1b96b-139">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1b96b-140">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b96b-140">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1b96b-141">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1b96b-141">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1b96b-142">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="1b96b-142">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1b96b-143">Selezionare l'applicazione hello da tooconfigure single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b96b-143">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="1b96b-144">Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1b96b-144">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1b96b-145">Modalità di selezione hello **basato su Password Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="1b96b-145">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="1b96b-146">[Assegnare gli utenti dell'applicazione toohello](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="1b96b-146">[Assign users toohello application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="1b96b-147">Inoltre, è anche possibile fornire credenziali per conto dell'utente hello selezionando le righe di hello di utenti hello e facendo clic su **credenziali di aggiornamento** e l'immissione di nome utente hello e una password per conto degli utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1b96b-147">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="1b96b-148">In caso contrario, gli utenti in tooenter richiesta hello credenziali stessi all'avvio.</span><span class="sxs-lookup"><span data-stu-id="1b96b-148">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="1b96b-149">Assegnare un'applicazione tooan utente direttamente</span><span class="sxs-lookup"><span data-stu-id="1b96b-149">Assign a user tooan application directly</span></span>

<span data-ttu-id="1b96b-150">tooassign uno o più applicazioni tooan utenti direttamente, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="1b96b-150">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="1b96b-151">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="1b96b-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1b96b-152">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="1b96b-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1b96b-153">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1b96b-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1b96b-154">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b96b-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1b96b-155">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1b96b-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1b96b-156">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="1b96b-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1b96b-157">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="1b96b-157">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="1b96b-158">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1b96b-158">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1b96b-159">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="1b96b-159">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="1b96b-160">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="1b96b-160">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="1b96b-161">Tipo di hello **nome completo** o **indirizzo di posta elettronica** dell'utente hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="1b96b-161">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="1b96b-162">Passare il mouse su hello **utente** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="1b96b-162">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="1b96b-163">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello dell'utente il toohello utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="1b96b-163">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="1b96b-164">**Facoltativo:** se si desidera troppo**aggiungere più di un utente**, in un altro tipo di **nome completo** o **indirizzo di posta elettronica** in hello **Cerca per nome o l'indirizzo di posta elettronica** casella di ricerca e fare clic su questo toohello utente hello casella di controllo tooadd **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="1b96b-164">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="1b96b-165">Al termine della selezione utenti, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b96b-165">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="1b96b-166">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un ruolo tooassign toohello utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="1b96b-166">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="1b96b-167">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="1b96b-167">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="1b96b-168">Assegnare un gruppo di applicazioni tooa direttamente</span><span class="sxs-lookup"><span data-stu-id="1b96b-168">Assign an application tooa group directly</span></span>

<span data-ttu-id="1b96b-169">tooassign uno o più gruppi di applicazioni tooan direttamente, seguire hello passaggi riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="1b96b-169">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="1b96b-170">Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale.**</span><span class="sxs-lookup"><span data-stu-id="1b96b-170">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1b96b-171">Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.</span><span class="sxs-lookup"><span data-stu-id="1b96b-171">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1b96b-172">Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="1b96b-172">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1b96b-173">Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b96b-173">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1b96b-174">Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1b96b-174">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1b96b-175">Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**</span><span class="sxs-lookup"><span data-stu-id="1b96b-175">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1b96b-176">Selezionare l'applicazione hello da un elenco di utenti toofrom hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="1b96b-176">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="1b96b-177">Una volta che un'applicazione hello caricato, fare clic su **utenti e gruppi** dal menu di navigazione a sinistra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1b96b-177">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1b96b-178">Fare clic su hello **Aggiungi** pulsante sopra hello **utenti e gruppi** hello tooopen elenco **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="1b96b-178">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="1b96b-179">Fare clic su hello **utenti e gruppi** selettore di hello **Aggiungi** blade.</span><span class="sxs-lookup"><span data-stu-id="1b96b-179">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="1b96b-180">Tipo di hello **nome del gruppo completo** del gruppo di hello si è interessati nell'assegnazione di hello **ricerca per nome o indirizzo di posta** casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="1b96b-180">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="1b96b-181">Passare il mouse su hello **gruppo** in hello elenco tooreveal un **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="1b96b-181">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="1b96b-182">Fare clic su tooadd di foto o logo profilo hello casella di controllo successivo toohello del gruppo toohello l'utente **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="1b96b-182">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="1b96b-183">**Facoltativo:** se si desidera troppo**aggiungere più di un gruppo**, in un altro tipo di **nome del gruppo completo** in hello **ricerca per nome o indirizzo di posta** casella di ricerca Fare clic su hello casella di controllo tooadd toohello questo gruppo **selezionati** elenco.</span><span class="sxs-lookup"><span data-stu-id="1b96b-183">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="1b96b-184">Al termine della selezione gruppi, fare clic su hello **selezionare** tooadd pulsante li toohello elenco di utenti e gruppi toobe assegnato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b96b-184">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="1b96b-185">**Facoltativo:** fare clic su hello **selezionare il ruolo** selettore di hello **Aggiungi** pannello tooselect un toohello tooassign ruolo gruppi di sicurezza selezionato.</span><span class="sxs-lookup"><span data-stu-id="1b96b-185">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="1b96b-186">Fare clic su hello **assegnare** pulsante tooassign hello applicazione toohello gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="1b96b-186">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="1b96b-187">Dopo un breve periodo, gli utenti di hello selezionato toolaunch in grado di queste applicazioni in hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1b96b-187">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b96b-188">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1b96b-188">Next steps</span></span>
[<span data-ttu-id="1b96b-189">Fornire le applicazioni single sign-on tooyour con Proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="1b96b-189">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
