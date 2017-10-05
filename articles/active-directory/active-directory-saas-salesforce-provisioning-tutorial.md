---
title: 'Esercitazione: Integrazione di Azure Active Directory con Salesforce | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Salesforce.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a573a7ef79e28c50ae0923849a88f88af40f21be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a><span data-ttu-id="eae22-103">Esercitazione: Configurazione di Salesforce per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="eae22-103">Tutorial: Configuring Salesforce for Automatic User Provisioning</span></span>

<span data-ttu-id="eae22-104">Questa esercitazione descrive le procedure da eseguire in Salesforce e Azure AD per effettuare automaticamente il provisioning e il deprovisioning degli account utente da Azure AD a Salesforce.</span><span class="sxs-lookup"><span data-stu-id="eae22-104">The objective of this tutorial is to show the steps required to perform in Salesforce and Azure AD to automatically provision and de-provision user accounts from Azure AD to Salesforce.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eae22-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eae22-105">Prerequisites</span></span>

<span data-ttu-id="eae22-106">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="eae22-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="eae22-107">Tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eae22-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="eae22-108">È necessario disporre di un tenant valido per Salesforce for Work o Salesforce for Education.</span><span class="sxs-lookup"><span data-stu-id="eae22-108">You must have a valid tenant for Salesforce for Work or Salesforce for Education.</span></span> <span data-ttu-id="eae22-109">È possibile usare un account della versione di valutazione gratuita per entrambi i servizi.</span><span class="sxs-lookup"><span data-stu-id="eae22-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="eae22-110">Account utente in Salesforce con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="eae22-110">A user account in Salesforce with Team Admin permissions.</span></span>

## <a name="assigning-users-to-salesforce"></a><span data-ttu-id="eae22-111">Assegnazione di utenti a Salesforce</span><span class="sxs-lookup"><span data-stu-id="eae22-111">Assigning users to Salesforce</span></span>

<span data-ttu-id="eae22-112">Per determinare gli utenti che dovranno ricevere l'accesso alle app selezionate, Azure Active Directory usa il concetto delle "assegnazioni".</span><span class="sxs-lookup"><span data-stu-id="eae22-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="eae22-113">Nel contesto del provisioning automatico degli account utente, vengono sincronizzati solo gli utenti e i gruppi che sono stati "assegnati" a un'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eae22-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="eae22-114">Prima di configurare e abilitare il servizio di provisioning, è necessario stabilire quali utenti e/o gruppi in Azure AD rappresentano gli utenti che devono accedere all'app Salesforce.</span><span class="sxs-lookup"><span data-stu-id="eae22-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Salesforce app.</span></span> <span data-ttu-id="eae22-115">Dopo aver stabilito questo, è possibile assegnare tali utenti all'app Salesforce seguendo le istruzioni riportate qui:</span><span class="sxs-lookup"><span data-stu-id="eae22-115">Once decided, you can assign these users to your Salesforce app by following the instructions here:</span></span>

[<span data-ttu-id="eae22-116">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="eae22-116">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-salesforce"></a><span data-ttu-id="eae22-117">Suggerimenti importanti per l'assegnazione di utenti a Salesforce</span><span class="sxs-lookup"><span data-stu-id="eae22-117">Important tips for assigning users to Salesforce</span></span>

*   <span data-ttu-id="eae22-118">È consigliabile assegnare un singolo utente di Azure AD a Salesforce per testare la configurazione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="eae22-118">It is recommended that a single Azure AD user is assigned to Salesforce to test the provisioning configuration.</span></span> <span data-ttu-id="eae22-119">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="eae22-119">Additional users and/or groups may be assigned later.</span></span>

*  <span data-ttu-id="eae22-120">Quando si assegna un utente a Salesforce, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="eae22-120">When assigning a user to Salesforce, you must select a valid user role.</span></span> <span data-ttu-id="eae22-121">Il ruolo "Default Access" (Accesso predefinito) non è applicabile per il provisioning</span><span class="sxs-lookup"><span data-stu-id="eae22-121">The "Default Access" role does not work for provisioning</span></span>

    > [!NOTE]
    > <span data-ttu-id="eae22-122">Questa app importa ruoli personalizzati da Salesforce come parte del processo di provisioning che il cliente può decidere di selezionare durante l'assegnazione di utenti</span><span class="sxs-lookup"><span data-stu-id="eae22-122">This app imports custom roles from Salesforce as part of the provisioning process, which the customer may want to select when assigning users</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="eae22-123">Abilitare il provisioning utenti automatizzato</span><span class="sxs-lookup"><span data-stu-id="eae22-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="eae22-124">Questa sezione illustra la connessione di Azure AD all'API per il provisioning degli account utente di Salesforce e la configurazione del servizio di provisioning per la creazione, l'aggiornamento e la disabilitazione degli account utente assegnati in Salesforce in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eae22-124">This section guides you through connecting your Azure AD to Salesforce's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Salesforce based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="eae22-125">Si può anche scegliere di abilitare l'accesso Single Sign-On basato su SAML per Salesforce, seguendo le istruzioni disponibili nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eae22-125">You may also choose to enabled SAML-based Single Sign-On for Salesforce, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="eae22-126">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="eae22-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="eae22-127">Per configurare il provisioning automatico degli account utente:</span><span class="sxs-lookup"><span data-stu-id="eae22-127">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="eae22-128">In questa sezione viene descritto come abilitare il provisioning utenti degli account utente di Active Directory in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="eae22-128">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce.</span></span>

1. <span data-ttu-id="eae22-129">Nel [portale di Azure](https://portal.azure.com) passare alla sezione **Azure Active Directory > App aziendali > Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="eae22-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="eae22-130">Se è già stato configurato Salesforce per l'accesso Single Sign-On, cercare l'istanza di Salesforce usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="eae22-130">If you have already configured Salesforce for single sign-on, search for your instance of Salesforce using the search field.</span></span> <span data-ttu-id="eae22-131">In caso contrario, selezionare **Aggiungi** e cercare **Salesforce** nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="eae22-131">Otherwise, select **Add** and search for **Salesforce** in the application gallery.</span></span> <span data-ttu-id="eae22-132">Selezionare Salesforce nei risultati della ricerca e aggiungerlo all'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="eae22-132">Select Salesforce from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="eae22-133">Selezionare l'istanza di Salesforce e quindi la scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="eae22-133">Select your instance of Salesforce, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="eae22-134">Impostare **Modalità di provisioning** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="eae22-134">Set the **Provisioning Mode** to **Automatic**.</span></span> 
<span data-ttu-id="eae22-135">![provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="eae22-135">![provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="eae22-136">Nella sezione **Credenziali di amministratore** specificare le impostazioni di configurazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="eae22-136">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="eae22-137">a.</span><span class="sxs-lookup"><span data-stu-id="eae22-137">a.</span></span> <span data-ttu-id="eae22-138">Nella casella di testo **Nome utente amministratore** digitare un nome account di Salesforce con il profilo **Amministratore di sistema** assegnato in Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="eae22-138">In the **Admin User Name** textbox, type a Salesforce account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="eae22-139">b.</span><span class="sxs-lookup"><span data-stu-id="eae22-139">b.</span></span> <span data-ttu-id="eae22-140">Nella casella di testo **Password amministratore** digitare la password per questo account.</span><span class="sxs-lookup"><span data-stu-id="eae22-140">In the **Admin Password** textbox, type the password for this account.</span></span>

6. <span data-ttu-id="eae22-141">Per ottenere il token di sicurezza di Salesforce, aprire una nuova scheda e accedere allo stesso account di amministratore di Salesforce.</span><span class="sxs-lookup"><span data-stu-id="eae22-141">To get your Salesforce security token, open a new tab and sign into the same Salesforce admin account.</span></span> <span data-ttu-id="eae22-142">Nell'angolo superiore destro della pagina fare clic sul proprio nome e quindi su **Impostazioni personali**.</span><span class="sxs-lookup"><span data-stu-id="eae22-142">On the top right corner of the page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="eae22-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="eae22-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="eae22-144">Nel pannello di navigazione sinistro fare clic su **Personal** (Personale) per espandere la sezione corrispondente, quindi fare clic su **Reset My Security Token** (Reimposta token di sicurezza personale).</span><span class="sxs-lookup"><span data-stu-id="eae22-144">On the left navigation pane, click **Personal** to expand the related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="eae22-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="eae22-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="eae22-146">Nella pagina **Reset My Security Token** (Reimposta token di sicurezza personale) fare clic sul pulsante **Reset Security Token** (Reimposta token di sicurezza).</span><span class="sxs-lookup"><span data-stu-id="eae22-146">On the **Reset My Security Token** page, click **Reset Security Token** button.</span></span>

    <span data-ttu-id="eae22-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="eae22-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="eae22-148">Controllare la casella di posta elettronica associata a questo account di amministratore.</span><span class="sxs-lookup"><span data-stu-id="eae22-148">Check the email inbox associated with this admin account.</span></span> <span data-ttu-id="eae22-149">Cercare un messaggio di posta elettronica da Salesforce.com contenente il nuovo token di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="eae22-149">Look for an email from Salesforce.com that contains the new security token.</span></span>
10. <span data-ttu-id="eae22-150">Copiare il token, passare alla finestra di Azure AD e incollarlo nel campo **Socket Token**.</span><span class="sxs-lookup"><span data-stu-id="eae22-150">Copy the token, go to your Azure AD window, and paste it into the **Socket Token** field.</span></span>

11. <span data-ttu-id="eae22-151">Nel portale di Azure fare clic su **Test connessione** per verificare che Azure AD possa connettersi all'app Salesforce.</span><span class="sxs-lookup"><span data-stu-id="eae22-151">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Salesforce app.</span></span>

12. <span data-ttu-id="eae22-152">Nel campo **Messaggio di posta elettronica di notifica** immettere l'indirizzo di posta elettronica di una persona o un gruppo che riceverà le notifiche di errore relative al provisioning e selezionare la casella di controllo qui di seguito.</span><span class="sxs-lookup"><span data-stu-id="eae22-152">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox below.</span></span>

13. <span data-ttu-id="eae22-153">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="eae22-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="eae22-154">Nella sezione Mapping selezionare **Synchronize Azure Active Directory Users to Salesforce** (Sincronizza utenti di Azure Active Directory in Salesforce).</span><span class="sxs-lookup"><span data-stu-id="eae22-154">Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce.**</span></span>

15. <span data-ttu-id="eae22-155">Nella sezione **Mapping degli attributi** esaminare gli attributi utente che vengono sincronizzati da Azure AD a Salesforce.</span><span class="sxs-lookup"><span data-stu-id="eae22-155">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Salesforce.</span></span> <span data-ttu-id="eae22-156">Notar e che gli attributi selezionati come proprietà **corrispondenti** vengono usati per trovare le corrispondenze con gli account utente in Salesforce per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="eae22-156">Note that the attributes selected as **Matching** properties are used to match the user accounts in Salesforce for update operations.</span></span> <span data-ttu-id="eae22-157">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="eae22-157">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="eae22-158">Per abilitare il servizio di provisioning di Azure AD per Salesforce, impostare **Stato del provisioning** su **Attivato** nella sezione Impostazioni</span><span class="sxs-lookup"><span data-stu-id="eae22-158">To enable the Azure AD provisioning service for Salesforce, change the **Provisioning Status** to **On** in the Settings section</span></span>

17. <span data-ttu-id="eae22-159">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="eae22-159">Click **Save.**</span></span>

<span data-ttu-id="eae22-160">Viene avviata la sincronizzazione iniziale di tutti gli utenti e/o i gruppi assegnati a Salesforce nella sezione Utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="eae22-160">This starts the initial synchronization of any users and/or groups assigned to Salesforce in the Users and Groups section.</span></span> <span data-ttu-id="eae22-161">Notare che la sincronizzazione iniziale richiede più tempo delle sincronizzazioni successive, che saranno eseguite circa ogni 20 minuti per tutto il tempo che il servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="eae22-161">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="eae22-162">È possibile usare la sezione **Dettagli sincronizzazione** per monitorare lo stato di avanzamento e selezionare i collegamenti ai report delle attività di provisioning, che descrivono tutte le azioni eseguite dal servizio di provisioning sull'app Salesforce.</span><span class="sxs-lookup"><span data-stu-id="eae22-162">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Salesforce app.</span></span>

<span data-ttu-id="eae22-163">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="eae22-163">You can now create a test account.</span></span> <span data-ttu-id="eae22-164">Attendere 20 minuti per verificare che l'account sia stato sincronizzato con Salesforce.</span><span class="sxs-lookup"><span data-stu-id="eae22-164">Wait for up to 20 minutes to verify that the account has been synchronized to Salesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eae22-165">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="eae22-165">Additional resources</span></span>

* [<span data-ttu-id="eae22-166">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="eae22-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eae22-167">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eae22-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="eae22-168">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="eae22-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforce-tutorial.md)