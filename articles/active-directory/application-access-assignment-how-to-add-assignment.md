---
title: Come assegnare utenti e gruppi a un'applicazione | Microsoft Docs
description: Assegnare utenti per concedere l'accesso all'applicazione
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
ms.openlocfilehash: 61536612e0dd5102b8f5e911c350826846f5ed77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-and-groups-to-an-application"></a><span data-ttu-id="7ad50-103">Come assegnare utenti e gruppi a un'applicazione</span><span class="sxs-lookup"><span data-stu-id="7ad50-103">How to assign users and groups to an application</span></span>

<span data-ttu-id="7ad50-104">Prima che gli utenti effettuino una delle operazioni seguenti per un'applicazione specifica, è necessario innanzitutto **assegnarli all'applicazione** per concedere loro l'accesso:</span><span class="sxs-lookup"><span data-stu-id="7ad50-104">Before your users can do any of the below for a specific application, you need to first **assign them to the application** to grant them access:</span></span>

-   <span data-ttu-id="7ad50-105">Accedere a un'applicazione **passando direttamente all'URL dell'applicazione** (noto anche come accesso avviato da provider di servizi).</span><span class="sxs-lookup"><span data-stu-id="7ad50-105">Access an application by **navigating to the application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="7ad50-106">Accedere a un'applicazione usando l'**URL di accesso utente** nella pagina **Proprietà** di un'applicazione (noto anche come accesso avviato da provider di identità).</span><span class="sxs-lookup"><span data-stu-id="7ad50-106">Access an application by using the **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="7ad50-107">Visualizzare un'applicazione nel [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) o l'applicazione per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="7ad50-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="7ad50-108">Visualizzare un'applicazione nell'[icona di avvio delle app di Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="7ad50-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-to-assign-applications-with-azure-active-directory"></a><span data-ttu-id="7ad50-109">Metodi per assegnare applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ad50-109">Methods to assign applications with Azure Active Directory</span></span> 

<span data-ttu-id="7ad50-110">Esistono 3 modi per poter assegnare applicazioni con Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="7ad50-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="7ad50-111">Assegnare un utente direttamente a un'applicazione come amministratore</span><span class="sxs-lookup"><span data-stu-id="7ad50-111">Assign a user directly to an application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="7ad50-112">Assegnare un gruppo direttamente a un'applicazione come amministratore</span><span class="sxs-lookup"><span data-stu-id="7ad50-112">Assign a group directly to an application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="7ad50-113">Abilitare l'accesso alle applicazioni self-service per consentire agli utenti di trovare le proprie applicazioni</span><span class="sxs-lookup"><span data-stu-id="7ad50-113">Enable self-service application access to allow users to find their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="7ad50-114">Assegnare un utente direttamente come amministratore</span><span class="sxs-lookup"><span data-stu-id="7ad50-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="7ad50-115">Per assegnare uno o più utenti direttamente a un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7ad50-115">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="7ad50-116">Aprire il [**portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7ad50-117">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7ad50-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7ad50-118">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7ad50-119">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7ad50-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7ad50-120">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7ad50-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="7ad50-121">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7ad50-122">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="7ad50-122">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="7ad50-123">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7ad50-123">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7ad50-124">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-124">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="7ad50-125">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-125">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="7ad50-126">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo**  o l'**indirizzo di posta elettronica** dell'utente oggetto dell'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="7ad50-126">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="7ad50-127">Passare il puntatore sull'**utente** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-127">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="7ad50-128">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo dell'utente per aggiungere l'utente all'elenco **Selezionato**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-128">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="7ad50-129">**Facoltativo:** se si vuole **aggiungere più di un utente**, digitare un altro **nome completo** o **indirizzo di posta elettronica** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere l'utente all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-129">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="7ad50-130">Dopo avere selezionato gli utenti, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7ad50-130">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="7ad50-131">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="7ad50-131">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="7ad50-132">Fare clic sul pulsante **Assegna** per assegnare l'applicazione agli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="7ad50-132">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="7ad50-133">Dopo un breve periodo di tempo, gli utenti selezionati potranno avviare queste applicazioni usando i metodi illustrati nella sezione Descrizione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="7ad50-133">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="7ad50-134">Assegnare un gruppo direttamente a un'applicazione come amministratore</span><span class="sxs-lookup"><span data-stu-id="7ad50-134">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="7ad50-135">Per assegnare uno o più gruppi direttamente a un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7ad50-135">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="7ad50-136">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7ad50-137">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7ad50-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7ad50-138">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7ad50-139">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7ad50-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7ad50-140">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7ad50-140">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="7ad50-141">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'elenco **Tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7ad50-142">Selezionare nell'elenco l'applicazione che si vuole assegnare a un utente.</span><span class="sxs-lookup"><span data-stu-id="7ad50-142">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="7ad50-143">Dopo il caricamento dell'applicazione, fare clic su **Utenti e gruppi** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7ad50-143">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7ad50-144">Fare clic sul pulsante **Aggiungi** nella parte superiore dell'elenco **Utenti e gruppi** per aprire il pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-144">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="7ad50-145">Fare clic sul selettore **Utenti e gruppi** nel pannello **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-145">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="7ad50-146">Nella casella di ricerca **Cerca per nome o indirizzo di posta** digitare il **nome completo del gruppo** a cui si vuole eseguire l'assegnazione.</span><span class="sxs-lookup"><span data-stu-id="7ad50-146">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="7ad50-147">Posizionare il puntatore sul **gruppo** nell'elenco per visualizzare una **casella di controllo**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-147">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="7ad50-148">Fare clic sulla casella di controllo accanto alla foto o al logo del profilo del gruppo per aggiungere il gruppo all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-148">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="7ad50-149">**Facoltativo:** se si vuole **aggiungere più di un gruppo**, digitare un altro **nome completo di gruppo** nella casella di ricerca **Cerca per nome o indirizzo di posta** e fare clic sulla casella di controllo per aggiungere il gruppo all'elenco **selezionato**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-149">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="7ad50-150">Dopo avere selezionato i gruppi, fare clic sul pulsante **Seleziona** per aggiungerli all'elenco di utenti e gruppi da assegnare all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7ad50-150">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="7ad50-151">**Facoltativo:** fare clic sul selettore **Seleziona ruolo** nel pannello **Aggiungi assegnazione** per scegliere un ruolo da assegnare ai gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="7ad50-151">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="7ad50-152">Fare clic sul pulsante **Assegna** per assegnare l'applicazione ai gruppi selezionati.</span><span class="sxs-lookup"><span data-stu-id="7ad50-152">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="7ad50-153">Dopo un breve periodo di tempo, gli utenti nei gruppi selezionati potranno avviare queste applicazioni usando i metodi illustrati nella sezione Descrizione della soluzione.</span><span class="sxs-lookup"><span data-stu-id="7ad50-153">After a short period of time, the users within the groups you have selected be able to launch these applications using the methods described in the solution description section.</span></span> <span data-ttu-id="7ad50-154">Se i gruppi sono dinamici, potrebbe verificarsi un ritardo di elaborazione aggiuntivo nella visualizzazione di queste assegnazioni per gli utenti dei gruppi assegnati.</span><span class="sxs-lookup"><span data-stu-id="7ad50-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="7ad50-155">Abilitare l'accesso alle applicazioni self-service per consentire agli utenti di trovare le proprie applicazioni</span><span class="sxs-lookup"><span data-stu-id="7ad50-155">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="7ad50-156">L'accesso alle applicazioni self-service è un modo efficace per consentire agli utenti di individuare da soli le applicazioni e, facoltativamente, al gruppo aziendale di approvare l'accesso a tali applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7ad50-156">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="7ad50-157">È possibile consentire al gruppo aziendale di gestire le credenziali assegnate agli utenti per il diritto di accesso alle applicazioni Single Sign-On tramite password dal pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7ad50-157">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="7ad50-158">Per abilitare l'accesso self-service per un'applicazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7ad50-158">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="7ad50-159">Aprire il [**Portale di Azure**](https://portal.azure.com/) e accedere come **Amministratore globale**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7ad50-160">Aprire l'**estensione Azure Active Directory** facendo clic su **Altri servizi** nella parte inferiore del menu di navigazione principale a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7ad50-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7ad50-161">Digitare "**Azure Active Directory**" nella casella di ricerca filtro e selezionare l'elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7ad50-162">Fare clic su **Applicazioni aziendali** nel menu di navigazione a sinistra di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7ad50-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7ad50-163">Fare clic su **Tutte le applicazioni** per visualizzare un elenco di tutte le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7ad50-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="7ad50-164">Se l'applicazione non è inclusa nell'elenco, usare il controllo **Filtro** all'inizio dell'**elenco di tutte le applicazioni** e impostare l'opzione **Mostra** su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7ad50-165">Selezionare l'applicazione per cui si desidera abilitare l'accesso self-service dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="7ad50-165">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="7ad50-166">Dopo il caricamento dell'applicazione, fare clic su **Self-service** nel menu di navigazione a sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7ad50-166">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7ad50-167">Per abilitare l'accesso self-service per questa applicazione, impostare l'opzione **Consentire agli utenti di richiedere l'accesso a questa applicazione?** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-167">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="7ad50-168">Successivamente, per selezionare il gruppo al quale devono essere aggiunti gli utenti che richiedono l'accesso a questa applicazione, fare clic sul selettore accanto all'etichetta **Gruppo a cui devono essere aggiunti gli utenti assegnati** e selezionare un gruppo.</span><span class="sxs-lookup"><span data-stu-id="7ad50-168">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="7ad50-169">**Facoltativo:** se si desidera richiedere un'approvazione aziendale prima che venga consentito l'accesso agli utenti, impostare l'opzione **Richiedere l'approvazione prima di concedere l'accesso a questa applicazione?** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-169">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="7ad50-170">**Facoltativo: per applicazioni che usano solo l'accesso Single Sign-On tramite password,** se si desidera consentire ai responsabili approvazione aziendali di specificare le password inviate a questa applicazione per gli utenti approvati, impostare l'opzione **Consentire ai responsabili approvazione di impostare le password utente per questa applicazione?** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="7ad50-170">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="7ad50-171">**Facoltativo:** per specificare i responsabili approvazione aziendali che possono approvare l'accesso a questa applicazione, fare clic sul selettore accanto all'etichetta **Utenti autorizzati ad approvare l'accesso a questa applicazione** per selezionare un massimo di 10 singoli responsabili approvazione aziendali.</span><span class="sxs-lookup"><span data-stu-id="7ad50-171">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="7ad50-172">I gruppi non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="7ad50-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="7ad50-173">**Facoltativo:** **per le applicazioni che espongono i ruoli**, se si desidera assegnare un ruolo agli utenti approvati self-service, fare clic sul selettore accanto all'opzione **A quale ruolo è necessario assegnare gli utenti in questa applicazione?** per selezionare il ruolo a cui devono essere assegnati questi utenti.</span><span class="sxs-lookup"><span data-stu-id="7ad50-173">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="7ad50-174">Per terminare, fare clic sul pulsante **Salva** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="7ad50-174">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="7ad50-175">Dopo aver completato la configurazione dell'applicazione self-service, gli utenti possono accedere al [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/) e fare clic sul pulsante **+Aggiungi** per trovare le app per cui è stato abilitato l'accesso self-service.</span><span class="sxs-lookup"><span data-stu-id="7ad50-175">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="7ad50-176">Anche i responsabili approvazione aziendali visualizzano una notifica nel loro [Pannello di accesso dell'applicazione](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="7ad50-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="7ad50-177">È possibile abilitare un messaggio di posta elettronica per informare i responsabili dell'approvazione quando un utente richiede l'accesso a un'applicazione per cui è necessaria l'approvazione.</span><span class="sxs-lookup"><span data-stu-id="7ad50-177">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="7ad50-178">Tali approvazioni supportano solo flussi di lavoro di approvazione individuali. Se si specificano pertanto più responsabili approvazione, uno qualsiasi di esso potrà approvare l'accesso all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7ad50-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ad50-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7ad50-179">Next steps</span></span>
[<span data-ttu-id="7ad50-180">Fornire l'accesso Single Sign-On alle app con il proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="7ad50-180">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
