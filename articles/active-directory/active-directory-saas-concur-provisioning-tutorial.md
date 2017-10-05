---
title: 'Esercitazione: Integrazione di Azure Active Directory con Concur | Documentazione Microsoft'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Concur.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: cd35b6e2dc3171e9cffdb820bbc5b0d45ff58e07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="fc271-103">Esercitazione: Configurazione di Concur per il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="fc271-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="fc271-104">Questa esercitazione descrive le procedure da eseguire in Concur e Azure AD per effettuare automaticamente il provisioning e il deprovisioning degli account utente da Azure AD a Concur.</span><span class="sxs-lookup"><span data-stu-id="fc271-104">The objective of this tutorial is to show you the steps you need to perform in Concur and Azure AD to automatically provision and de-provision user accounts from Azure AD to Concur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc271-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fc271-105">Prerequisites</span></span>

<span data-ttu-id="fc271-106">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="fc271-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="fc271-107">Tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fc271-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="fc271-108">Sottoscrizione di Concur abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="fc271-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="fc271-109">Account utente in Concur con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="fc271-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-to-concur"></a><span data-ttu-id="fc271-110">Assegnazione di utenti a Concur</span><span class="sxs-lookup"><span data-stu-id="fc271-110">Assigning users to Concur</span></span>

<span data-ttu-id="fc271-111">Per determinare gli utenti che dovranno ricevere l'accesso alle app selezionate, Azure Active Directory usa il concetto delle "assegnazioni".</span><span class="sxs-lookup"><span data-stu-id="fc271-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="fc271-112">Nel contesto del provisioning automatico degli account utente, vengono sincronizzati solo gli utenti e i gruppi che sono stati "assegnati" a un'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc271-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="fc271-113">Prima di configurare e abilitare il servizio di provisioning, è necessario stabilire quali utenti e/o gruppi in Azure AD rappresentano gli utenti che devono accedere all'app Concur.</span><span class="sxs-lookup"><span data-stu-id="fc271-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Concur app.</span></span> <span data-ttu-id="fc271-114">Dopo aver stabilito questo, è possibile assegnare tali utenti all'app Concur seguendo le istruzioni riportate qui:</span><span class="sxs-lookup"><span data-stu-id="fc271-114">Once decided, you can assign these users to your Concur app by following the instructions here:</span></span>

[<span data-ttu-id="fc271-115">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="fc271-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-concur"></a><span data-ttu-id="fc271-116">Suggerimenti importanti per l'assegnazione di utenti a Concur</span><span class="sxs-lookup"><span data-stu-id="fc271-116">Important tips for assigning users to Concur</span></span>

*   <span data-ttu-id="fc271-117">È consigliabile assegnare un singolo utente di Azure AD a Concur per testare la configurazione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="fc271-117">It is recommended that a single Azure AD user be assigned to Concur to test the provisioning configuration.</span></span> <span data-ttu-id="fc271-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="fc271-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="fc271-119">Quando si assegna un utente a Concur, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="fc271-119">When assigning a user to Concur, you must select a valid user role.</span></span> <span data-ttu-id="fc271-120">Il ruolo "Default Access" (Accesso predefinito) non è applicabile per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="fc271-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="fc271-121">Abilitare il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="fc271-121">Enable user provisioning</span></span>

<span data-ttu-id="fc271-122">Questa sezione illustra la connessione di Azure AD all'API per il provisioning degli account utente di Concur e la configurazione del servizio di provisioning per la creazione, l'aggiornamento e la disabilitazione degli account utente assegnati in Concur in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc271-122">This section guides you through connecting your Azure AD to Concur's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="fc271-123">Si può anche scegliere di abilitare l'accesso Single Sign-On basato su SAML per Concur, seguendo le istruzioni disponibili nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fc271-123">You may also choose to enabled SAML-based Single Sign-On for Concur, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fc271-124">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="fc271-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="fc271-125">Per configurare il provisioning degli account utente:</span><span class="sxs-lookup"><span data-stu-id="fc271-125">To configure user account provisioning:</span></span>

<span data-ttu-id="fc271-126">Questa sezione descrive come abilitare il provisioning utente degli account utente di Active Directory in Concur.</span><span class="sxs-lookup"><span data-stu-id="fc271-126">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.</span></span>

<span data-ttu-id="fc271-127">Per abilitare le app nel servizio Expense, è necessario configurare e usare in modo corretto un profilo di amministratore di servizi Web.</span><span class="sxs-lookup"><span data-stu-id="fc271-127">To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="fc271-128">Non aggiungere il ruolo di amministratore dei servizi Web al profilo amministratore esistente usato per le funzioni amministrative di T&E.</span><span class="sxs-lookup"><span data-stu-id="fc271-128">Don't add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="fc271-129">I consulenti Concur o l'amministratore client devono creare un diverso profilo di amministratore dei servizi Web e l'amministratore client deve usare tale profilo per le funzioni di amministratore dei servizi Web, ad esempio per abilitare le app.</span><span class="sxs-lookup"><span data-stu-id="fc271-129">Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="fc271-130">Questi profili devono essere mantenuti separati dal profilo di amministratore T&E giornaliero dell'amministratore del client. Questo significa che al profilo di amministratore T&E non deve essere assegnato il ruolo di amministratore dei servizi Web.</span><span class="sxs-lookup"><span data-stu-id="fc271-130">These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).</span></span>

<span data-ttu-id="fc271-131">Quando si crea il profilo da usare per abilitare l'app, immettere il nome dell'amministratore client nei campi del profilo utente per assegnare la proprietà al profilo.</span><span class="sxs-lookup"><span data-stu-id="fc271-131">When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields.</span></span> <span data-ttu-id="fc271-132">Ciò consente di assegnare la proprietà al profilo.</span><span class="sxs-lookup"><span data-stu-id="fc271-132">This assigns ownership to the profile.</span></span> <span data-ttu-id="fc271-133">Dopo la creazione di uno o più profili, il client dovrà accedere con questo profilo per poter fare clic sul pulsante "*Abilita*" relativo a un'app dei partner nel menu Servizi web.</span><span class="sxs-lookup"><span data-stu-id="fc271-133">Once one or more profiles is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.</span></span>

<span data-ttu-id="fc271-134">Per i seguenti motivi è consigliabile non eseguire questa operazione con il profilo usato per la normale amministrazione T&E.</span><span class="sxs-lookup"><span data-stu-id="fc271-134">For the following reasons, this action should not be done with the profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="fc271-135">Il client deve essere quello che fa clic su "*Sì*" nella finestra di dialogo visualizzata dopo l'abilitazione di un'app.</span><span class="sxs-lookup"><span data-stu-id="fc271-135">The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="fc271-136">Tale operazione conferma che il client consente all'applicazione del partner di accedere ai dati, di conseguenza non può essere l'utente o il partner a fare clic sul pulsante Yes.</span><span class="sxs-lookup"><span data-stu-id="fc271-136">This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="fc271-137">Se un amministratore client che ha abilitato un'app con il profilo di amministratore T&E lascia la società e il relativo profilo viene disattivato, tutte le app abilitate tramite tale profilo non funzioneranno finché l'app non viene abilitata con un altro profilo di amministratore di servizi Web attivo.</span><span class="sxs-lookup"><span data-stu-id="fc271-137">If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile does not function until the app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="fc271-138">È per questo motivo che è richiesta la creazione di profili distinti per l'amministratore di servizi Web.</span><span class="sxs-lookup"><span data-stu-id="fc271-138">This is why you are supposed to create distinct WS Admin profiles.</span></span>

* <span data-ttu-id="fc271-139">Se un amministratore lascia la società, se necessario è possibile modificare il nome associato al profilo dell'amministratore di servizi Web impostandolo su quello di sostituzione senza alcun impatto sull'app abilitata perché non è necessario disattivare tale profilo.</span><span class="sxs-lookup"><span data-stu-id="fc271-139">If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="fc271-140">**Per configurare il provisioning utenti, seguire questa procedura:**</span><span class="sxs-lookup"><span data-stu-id="fc271-140">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="fc271-141">Accedere al tenant di **Concur**.</span><span class="sxs-lookup"><span data-stu-id="fc271-141">Log on to your **Concur** tenant.</span></span>

2. <span data-ttu-id="fc271-142">Nel menu **Administration** (Amministrazione) selezionare **Web Services** (Servizi Web).</span><span class="sxs-lookup"><span data-stu-id="fc271-142">From the **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="fc271-143">![Tenant Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Tenant Concur")</span><span class="sxs-lookup"><span data-stu-id="fc271-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="fc271-144">Sul lato sinistro nel riquadro **Web Services** (Servizi Web) selezionare **Enable Partner Application** (Abilita applicazione partner).</span><span class="sxs-lookup"><span data-stu-id="fc271-144">On the left side, from the **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="fc271-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span><span class="sxs-lookup"><span data-stu-id="fc271-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="fc271-146">Dall'elenco **Enable Application** (Abilita applicazione) selezionare **Azure Active Directory**, quindi fare clic su **Enable** (Abilita).</span><span class="sxs-lookup"><span data-stu-id="fc271-146">From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="fc271-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="fc271-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="fc271-148">Fare clic su **Yes** (Sì) per chiudere la finestra di dialogo **Confirm Action** (Conferma operazione).</span><span class="sxs-lookup"><span data-stu-id="fc271-148">Click **Yes** to close the **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="fc271-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span><span class="sxs-lookup"><span data-stu-id="fc271-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="fc271-150">Nel [portale di Azure](https://portal.azure.com) passare alla sezione **Azure Active Directory > App aziendali > Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fc271-150">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="fc271-151">Se si è già configurato Concur per l'accesso Single Sign-On, cercare l'istanza di Concur usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="fc271-151">If you have already configured Concur for single sign-on, search for your instance of Concur using the search field.</span></span> <span data-ttu-id="fc271-152">In caso contrario, selezionare **Aggiungi** e cercare **Concur** nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="fc271-152">Otherwise, select **Add** and search for **Concur** in the application gallery.</span></span> <span data-ttu-id="fc271-153">Selezionare Concur nei risultati della ricerca e aggiungerlo all'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="fc271-153">Select Concur from the search results, and add it to your list of applications.</span></span>

8. <span data-ttu-id="fc271-154">Selezionare l'istanza di Concur e quindi la scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="fc271-154">Select your instance of Concur, then select the **Provisioning** tab.</span></span>

9. <span data-ttu-id="fc271-155">Impostare **Modalità di provisioning** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="fc271-155">Set the **Provisioning Mode** to **Automatic**.</span></span> 
 
    ![provisioning](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="fc271-157">Nella sezione **Credenziali amministratore** immettere il **nome utente** e la **password** dell'amministratore di Concur.</span><span class="sxs-lookup"><span data-stu-id="fc271-157">Under the **Admin Credentials** section, enter the **user name** and the **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="fc271-158">Nel portale di Azure fare clic su **Connessione di test** per verificare che Azure AD possa connettersi all'app Concur.</span><span class="sxs-lookup"><span data-stu-id="fc271-158">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Concur app.</span></span> <span data-ttu-id="fc271-159">Se la connessione non riesce, verificare che l'account Concur disponga di autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="fc271-159">If the connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="fc271-160">Immettere l'indirizzo di posta elettronica di una persona o un gruppo che riceverà le notifiche di errore relative al provisioning nel campo **Messaggio di posta elettronica di notifica** e selezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="fc271-160">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

13. <span data-ttu-id="fc271-161">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fc271-161">Click **Save.**</span></span>

14. <span data-ttu-id="fc271-162">Nella sezione Mapping selezionare **Synchronize Azure Active Directory Users to Concur** (Sincronizza utenti di Azure Active Directory in Concur).</span><span class="sxs-lookup"><span data-stu-id="fc271-162">Under the Mappings section, select **Synchronize Azure Active Directory Users to Concur.**</span></span>

15. <span data-ttu-id="fc271-163">Nella sezione **Mapping degli attributi** esaminare gli attributi utente che vengono sincronizzati da Azure AD a Concur.</span><span class="sxs-lookup"><span data-stu-id="fc271-163">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Concur.</span></span> <span data-ttu-id="fc271-164">Gli attributi selezionati come proprietà **corrispondenti** vengono usati per trovare le corrispondenze con gli account utente in Concur per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="fc271-164">The attributes selected as **Matching** properties are used to match the user accounts in Concur for update operations.</span></span> <span data-ttu-id="fc271-165">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="fc271-165">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="fc271-166">Per abilitare il servizio di provisioning di Azure AD per Concur, impostare lo **Stato del provisioning** su **Sì** nella sezione **Impostazioni**</span><span class="sxs-lookup"><span data-stu-id="fc271-166">To enable the Azure AD provisioning service for Concur, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

17. <span data-ttu-id="fc271-167">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fc271-167">Click **Save.**</span></span>

<span data-ttu-id="fc271-168">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="fc271-168">You can now create a test account.</span></span> <span data-ttu-id="fc271-169">Attendere 20 minuti per verificare che l'account sia stato sincronizzato con Concur.</span><span class="sxs-lookup"><span data-stu-id="fc271-169">Wait for up to 20 minutes to verify that the account has been synchronized to Concur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fc271-170">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="fc271-170">Additional resources</span></span>

* [<span data-ttu-id="fc271-171">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="fc271-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fc271-172">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc271-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="fc271-173">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fc271-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

