---
title: 'Esercitazione: Integrazione di Azure Active Directory con Dropbox for Business | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Dropbox for Business.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6f7616e47322242f01a13d763f71c93d4ac06a92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="c520f-103">Esercitazione: Configurazione di Dropbox for Business per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="c520f-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="c520f-104">Questa esercitazione descrive le procedure da eseguire in Dropbox for Business e Azure AD per effettuare automaticamente il provisioning e il deprovisioning degli account utente da Azure AD a Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="c520f-104">The objective of this tutorial is to show you the steps you need to perform in Dropbox for Business and Azure AD to automatically provision and de-provision user accounts from Azure AD to Dropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c520f-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c520f-105">Prerequisites</span></span>

<span data-ttu-id="c520f-106">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c520f-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="c520f-107">Tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c520f-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="c520f-108">Sottoscrizione di Dropbox for Business abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="c520f-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="c520f-109">Account utente in Dropbox for Business con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="c520f-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-to-dropbox-for-business"></a><span data-ttu-id="c520f-110">Assegnazione di utenti in Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="c520f-110">Assigning users to Dropbox for Business</span></span>

<span data-ttu-id="c520f-111">Per determinare gli utenti che dovranno ricevere l'accesso alle app selezionate, Azure Active Directory usa il concetto delle "assegnazioni".</span><span class="sxs-lookup"><span data-stu-id="c520f-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="c520f-112">Nel contesto del provisioning automatico degli account utente, vengono sincronizzati solo gli utenti e i gruppi che sono stati "assegnati" a un'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c520f-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="c520f-113">Prima di configurare e abilitare il servizio di provisioning, è necessario stabilire quali utenti e/o gruppi in Azure AD rappresentano gli utenti che devono accedere all'app Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="c520f-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Dropbox for Business app.</span></span> <span data-ttu-id="c520f-114">Dopo aver stabilito questo, è possibile assegnare tali utenti all'app Dropbox for Business seguendo le istruzioni riportate qui:</span><span class="sxs-lookup"><span data-stu-id="c520f-114">Once decided, you can assign these users to your Dropbox for Business app by following the instructions here:</span></span>

[<span data-ttu-id="c520f-115">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="c520f-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-dropbox-for-business"></a><span data-ttu-id="c520f-116">Suggerimenti importanti per l'assegnazione di utenti a Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="c520f-116">Important tips for assigning users to Dropbox for Business</span></span>

*   <span data-ttu-id="c520f-117">È consigliabile assegnare un singolo utente di Azure AD a Dropbox for Business per testare la configurazione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="c520f-117">It is recommended that a single Azure AD user is assigned to Dropbox for Business to test the provisioning configuration.</span></span> <span data-ttu-id="c520f-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="c520f-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="c520f-119">Quando si assegna un utente a Dropbox for Business, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="c520f-119">When assigning a user to Dropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="c520f-120">Il ruolo "Accesso predefinito" non è applicabile per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="c520f-120">The "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="c520f-121">Abilitare il provisioning utenti automatizzato</span><span class="sxs-lookup"><span data-stu-id="c520f-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="c520f-122">Questa sezione illustra la connessione di Azure AD all'API per il provisioning degli account utente di Dropbox for Business e la configurazione del servizio di provisioning per la creazione, l'aggiornamento e la disabilitazione degli account utente assegnati in Dropbox for Business in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c520f-122">This section guides you through connecting your Azure AD to Dropbox for Business's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="c520f-123">Si può anche scegliere di abilitare l'accesso Single Sign-On basato su SAML per Dropbox for Business, seguendo le istruzioni disponibili nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c520f-123">You may also choose to enabled SAML-based Single Sign-On for Dropbox for Business, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c520f-124">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="c520f-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="c520f-125">Per configurare il provisioning automatico degli account utente:</span><span class="sxs-lookup"><span data-stu-id="c520f-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="c520f-126">Nel [portale di Azure](https://portal.azure.com) passare alla sezione **Azure Active Directory > App aziendali > Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c520f-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="c520f-127">Se è già stato configurato Dropbox for Business per l'accesso Single Sign-On, cercare l'istanza di Dropbox for Business usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="c520f-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using the search field.</span></span> <span data-ttu-id="c520f-128">In caso contrario, selezionare **Aggiungi** e cercare **Dropbox for Business** nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c520f-128">Otherwise, select **Add** and search for **Dropbox for Business** in the application gallery.</span></span> <span data-ttu-id="c520f-129">Selezionare Dropbox for Business nei risultati della ricerca e aggiungerlo all'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c520f-129">Select Dropbox for Business from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="c520f-130">Selezionare l'istanza di Dropbox for Business e quindi la scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="c520f-130">Select your instance of Dropbox for Business, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="c520f-131">Impostare **Modalità di provisioning** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="c520f-131">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="c520f-133">Nella sezione **Credenziali amministratore** fare clic su **Autorizza**.</span><span class="sxs-lookup"><span data-stu-id="c520f-133">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="c520f-134">Viene aperta una finestra di dialogo di accesso di Dropbox for Business in una nuova finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="c520f-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="c520f-135">Nella finestra di dialogo di **Sign in to Dropbox to link with Azure AD** (Accedi a Dropbox per il collegamento ad Azure AD) accedere al tenant di Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="c520f-135">On the **Sign-in to Dropbox to link with Azure AD** dialog, sign in to your Dropbox for Business tenant.</span></span>

     <span data-ttu-id="c520f-136">![Provisioning degli utenti](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Provisioning degli utenti")</span><span class="sxs-lookup"><span data-stu-id="c520f-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="c520f-137">Confermare che si desidera concedere l'autorizzazione Azure Active Directory per apportare modifiche al tenant di Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="c520f-137">Confirm that you would like to give Azure Active Directory permission to make changes to your Dropbox for Business tenant.</span></span> <span data-ttu-id="c520f-138">Fare clic su **Consenti**.</span><span class="sxs-lookup"><span data-stu-id="c520f-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="c520f-139">![Provisioning degli utenti](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Provisioning degli utenti")</span><span class="sxs-lookup"><span data-stu-id="c520f-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="c520f-140">Nel portale di Azure fare clic su **Test connessione** per verificare che Azure AD possa connettersi all'app Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="c520f-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Dropbox for Business app.</span></span> <span data-ttu-id="c520f-141">Se la connessione non riesce, verificare che l'account di Dropbox for Business abbia autorizzazioni di amministratore di team e ripetere il passaggio **Autorizza**.</span><span class="sxs-lookup"><span data-stu-id="c520f-141">If the connection fails, ensure your Dropbox for Business account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

9. <span data-ttu-id="c520f-142">Immettere l'indirizzo e-mail di una persona o un gruppo che riceverà le notifiche di errore relative al provisioning nel campo **Messaggio di posta elettronica di notifica** e selezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="c520f-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

10. <span data-ttu-id="c520f-143">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c520f-143">Click **Save.**</span></span>

11. <span data-ttu-id="c520f-144">Nella sezione Mapping selezionare **Synchronize Azure Active Directory Users to Dropbox for Business** (Sincronizza utenti di Azure Active Directory in Dropbox for Business).</span><span class="sxs-lookup"><span data-stu-id="c520f-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Dropbox for Business.**</span></span>

12. <span data-ttu-id="c520f-145">Nella sezione **Mapping degli attributi** esaminare gli attributi utente che vengono sincronizzati da Azure AD a Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="c520f-145">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Dropbox for Business.</span></span> <span data-ttu-id="c520f-146">Gli attributi selezionati come proprietà **corrispondenti** vengono usati per trovare le corrispondenze con gli account utente in Dropbox for Business per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c520f-146">The attributes selected as **Matching** properties are used to match the user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="c520f-147">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="c520f-147">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="c520f-148">Per abilitare il servizio di provisioning di Azure AD per Dropbox for Business, impostare **Stato del provisioning** su **Attivato** nella sezione Impostazioni</span><span class="sxs-lookup"><span data-stu-id="c520f-148">To enable the Azure AD provisioning service for Dropbox for Business, change the **Provisioning Status** to **On** in the Settings section</span></span>

14. <span data-ttu-id="c520f-149">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c520f-149">Click **Save.**</span></span>

<span data-ttu-id="c520f-150">Viene avviata la sincronizzazione iniziale di tutti gli utenti e/o i gruppi assegnati a Dropbox for Business nella sezione Utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="c520f-150">It starts the initial synchronization of any users and/or groups assigned to Dropbox for Business in the Users and Groups section.</span></span> <span data-ttu-id="c520f-151">La sincronizzazione iniziale richiede più tempo delle sincronizzazioni successive, che saranno eseguite circa ogni 20 minuti per tutto il tempo che il servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c520f-151">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="c520f-152">È possibile usare la sezione **Dettagli sincronizzazione** per monitorare lo stato di avanzamento e selezionare i collegamenti ai report delle attività di provisioning, che descrivono tutte le azioni eseguite dal servizio di provisioning per l'app Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="c520f-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="c520f-153">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="c520f-153">You can now create a test account.</span></span> <span data-ttu-id="c520f-154">Attendere 20 minuti per verificare che l'account sia stato sincronizzato con Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="c520f-154">Wait for up to 20 minutes to verify that the account has been synchronized to Dropbox for Business.</span></span>

<span data-ttu-id="c520f-155">Un ciclo di provisioning utenti completato correttamente è indicato da uno stato correlato.</span><span class="sxs-lookup"><span data-stu-id="c520f-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="c520f-156">![Assegnare utenti](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="c520f-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c520f-157">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c520f-157">Additional resources</span></span>

* [<span data-ttu-id="c520f-158">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="c520f-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c520f-159">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c520f-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c520f-160">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c520f-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)