---
title: 'Esercitazione: Configurazione di Slack per il provisioning utenti automatico con Azure Active Directory | Documentazione Microsoft'
description: Informazioni su come configurare Azure Active Directory per effettuare automaticamente il provisioning e il deprovisioning degli account utente in Slack.
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: 3cb49a4abb26c34a938c963c4cf326b5ccd490de
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="4be39-103">Esercitazione: Configurazione di Slack per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="4be39-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="4be39-104">Questa esercitazione descrive le procedure da eseguire in Slack e Azure AD per effettuare automaticamente il provisioning e il deprovisioning degli account utente da Azure AD a Slack.</span><span class="sxs-lookup"><span data-stu-id="4be39-104">The objective of this tutorial is to show you the steps you need to perform in Slack and Azure AD to automatically provision and de-provision user accounts from Azure AD to Slack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4be39-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4be39-105">Prerequisites</span></span>

<span data-ttu-id="4be39-106">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="4be39-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="4be39-107">Tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4be39-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="4be39-108">Tenant di Slack con [piano Plus](https://aadsyncfabric.slack.com/pricing) o superiore abilitato</span><span class="sxs-lookup"><span data-stu-id="4be39-108">A Slack tenant with the [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="4be39-109">Account utente in Slack con autorizzazioni di amministratore di team</span><span class="sxs-lookup"><span data-stu-id="4be39-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="4be39-110">Nota: l'integrazione del provisioning di Azure AD è basata sull'[API SCIM di Slack](https://api.slack.com/scim), disponibile per team Slack con piano Plus o superiore.</span><span class="sxs-lookup"><span data-stu-id="4be39-110">Note: The Azure AD provisioning integration relies on the [Slack SCIM API](https://api.slack.com/scim) which is available to Slack teams on the Plus plan or better.</span></span>

## <a name="assigning-users-to-slack"></a><span data-ttu-id="4be39-111">Assegnazione di utenti a Slack</span><span class="sxs-lookup"><span data-stu-id="4be39-111">Assigning users to Slack</span></span>

<span data-ttu-id="4be39-112">Per determinare gli utenti che dovranno ricevere l'accesso alle app selezionate, Azure Active Directory usa il concetto delle "assegnazioni".</span><span class="sxs-lookup"><span data-stu-id="4be39-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="4be39-113">Nel contesto del provisioning automatico degli account utente, verranno sincronizzati solo gli utenti e i gruppi che sono stati "assegnati" a un'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4be39-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="4be39-114">Prima di configurare e abilitare il servizio di provisioning, è necessario stabilire quali utenti e/o gruppi in Azure AD rappresentano gli utenti che devono accedere all'app Slack.</span><span class="sxs-lookup"><span data-stu-id="4be39-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to your Slack app.</span></span> <span data-ttu-id="4be39-115">Dopo aver stabilito questo, è possibile assegnare tali utenti all'app Slack seguendo le istruzioni riportate nell'articolo seguente:</span><span class="sxs-lookup"><span data-stu-id="4be39-115">Once decided, you can assign these users to your Slack app by following the instructions here:</span></span>

[<span data-ttu-id="4be39-116">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="4be39-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-slack"></a><span data-ttu-id="4be39-117">Suggerimenti importanti per l'assegnazione di utenti a Slack</span><span class="sxs-lookup"><span data-stu-id="4be39-117">Important tips for assigning users to Slack</span></span>

*   <span data-ttu-id="4be39-118">È consigliabile assegnare un singolo utente di Azure AD a Slack per testare la configurazione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="4be39-118">It is recommended that a single Azure AD user be assigned to Slack to test the provisioning configuration.</span></span> <span data-ttu-id="4be39-119">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="4be39-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="4be39-120">Quando si assegna un utente a Slack, è necessario selezionare il ruolo **Utente** o "Gruppo" nella finestra di dialogo di assegnazione.</span><span class="sxs-lookup"><span data-stu-id="4be39-120">When assigning a user to Slack, you must select the **User** or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="4be39-121">Il ruolo "Default Access" (Accesso predefinito) non è applicabile per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="4be39-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-slack"></a><span data-ttu-id="4be39-122">Configurazione del provisioning utenti in Slack</span><span class="sxs-lookup"><span data-stu-id="4be39-122">Configuring user provisioning to Slack</span></span> 

<span data-ttu-id="4be39-123">Questa sezione illustra la connessione di Azure AD all'API per il provisioning degli account utente di Slack e la configurazione del servizio di provisioning per la creazione, l'aggiornamento e la disabilitazione degli account utente assegnati in Slack in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4be39-123">This section guides you through connecting your Azure AD to Slack's user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="4be39-124">**Suggerimento:** si può anche scegliere di abilitare l'accesso Single Sign-On basato su SAML per Slack, seguendo le istruzioni disponibili nel portale di Azure [https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="4be39-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for Slack, following the instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="4be39-125">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="4be39-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-slack-in-azure-ad"></a><span data-ttu-id="4be39-126">Per configurare il provisioning automatico degli account utente in Slack con Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4be39-126">To configure automatic user account provisioning to Slack in Azure AD:</span></span>


1)  <span data-ttu-id="4be39-127">Nel [portale di Azure](https://portal.azure.com) passare alla sezione **Azure Active Directory > App aziendali > Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4be39-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="4be39-128">Se si è già configurato Slack per l'accesso Single Sign-On, cercare l'istanza di Slack usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="4be39-128">If you have already configured Slack for single sign-on, search for your instance of Slack using the search field.</span></span> <span data-ttu-id="4be39-129">In caso contrario, selezionare **Aggiungi** e cercare **Slack** nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4be39-129">Otherwise, select **Add** and search for **Slack** in the application gallery.</span></span> <span data-ttu-id="4be39-130">Selezionare Slack nei risultati della ricerca e aggiungerlo all'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4be39-130">Select Slack from the search results, and add it to your list of applications.</span></span>

3)  <span data-ttu-id="4be39-131">Selezionare l'istanza di Slack e quindi la scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="4be39-131">Select your instance of Slack, then select the **Provisioning** tab.</span></span>

4)  <span data-ttu-id="4be39-132">Impostare **Modalità di provisioning** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="4be39-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Provisioning in Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="4be39-134">Nella sezione **Credenziali amministratore** fare clic su **Autorizza**.</span><span class="sxs-lookup"><span data-stu-id="4be39-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="4be39-135">Verrà aperta una finestra di dialogo di autorizzazione di Slack in una nuova finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="4be39-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="4be39-136">Nella nuova finestra accedere a Slack con l'account di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="4be39-136">In the new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="4be39-137">Nella finestra di dialogo di autorizzazione risultante selezionare il team Slack per cui si vuole abilitare il provisioning e quindi **Authorize** (Autorizza).</span><span class="sxs-lookup"><span data-stu-id="4be39-137">in the resulting authorization dialog, select the Slack team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="4be39-138">Al termine, tornare al portale di Azure per completare la configurazione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="4be39-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

![Finestra di dialogo di autorizzazione](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="4be39-140">Nel portale di Azure fare clic su **Test connessione** per verificare che Azure AD possa connettersi all'app Slack.</span><span class="sxs-lookup"><span data-stu-id="4be39-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Slack app.</span></span> <span data-ttu-id="4be39-141">Se la connessione non riesce, verificare che l'account Slack abbia autorizzazioni di amministratore di team e ripetere il passaggio "Authorize" (Autorizza).</span><span class="sxs-lookup"><span data-stu-id="4be39-141">If the connection fails, ensure your Slack account has Team Admin permissions and try the "Authorize" step again.</span></span>

8) <span data-ttu-id="4be39-142">Immettere l'indirizzo di posta elettronica di una persona o un gruppo che riceverà le notifiche di errore relative al provisioning nel campo **Messaggio di posta elettronica di notifica** e selezionare la casella di controllo seguente.</span><span class="sxs-lookup"><span data-stu-id="4be39-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

9) <span data-ttu-id="4be39-143">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="4be39-143">Click **Save**.</span></span> 

10) <span data-ttu-id="4be39-144">Nella sezione Mapping selezionare **Synchronize Azure Active Directory Users to Slack** (Sincronizza utenti di Azure Active Directory in Slack).</span><span class="sxs-lookup"><span data-stu-id="4be39-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Slack**.</span></span>

11) <span data-ttu-id="4be39-145">Nella sezione **Mapping degli attributi** esaminare gli attributi utente che verranno sincronizzati da Azure AD a Slack.</span><span class="sxs-lookup"><span data-stu-id="4be39-145">In the **Attribute Mappings** section, review the user attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="4be39-146">Si noti che gli attributi selezionati come proprietà **corrispondenti** verranno usati per trovare le corrispondenze con gli account utente in Slack per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="4be39-146">Note that the attributes selected as **Matching** properties will be used to match the user accounts in Slack for update operations.</span></span> <span data-ttu-id="4be39-147">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="4be39-147">Select the Save button to commit any changes.</span></span>

12) <span data-ttu-id="4be39-148">Per abilitare il servizio di provisioning di Azure AD per Slack, impostare **Stato del provisioning** su **Sì** nella sezione **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="4be39-148">To enable the Azure AD provisioning service for Slack, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13) <span data-ttu-id="4be39-149">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="4be39-149">Click **Save**.</span></span> 

<span data-ttu-id="4be39-150">Verrà avviata la sincronizzazione iniziale di tutti gli utenti e/o i gruppi assegnati a Slack nella sezione Utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="4be39-150">This will start the initial synchronization of any users and/or groups assigned to Slack in the Users and Groups section.</span></span> <span data-ttu-id="4be39-151">Si noti che la sincronizzazione iniziale richiederà più tempo delle sincronizzazioni successive, eseguite circa ogni 10 minuti fintanto che è in esecuzione il servizio.</span><span class="sxs-lookup"><span data-stu-id="4be39-151">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 10 minutes as long as the service is running.</span></span> <span data-ttu-id="4be39-152">È possibile usare la sezione **Dettagli sincronizzazione** per monitorare lo stato di avanzamento e selezionare i collegamenti ai report delle attività di provisioning, che descrivono tutte le azioni eseguite dal servizio di provisioning sull'app Slack.</span><span class="sxs-lookup"><span data-stu-id="4be39-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-to-slack"></a><span data-ttu-id="4be39-153">[Facoltativo] Configurazione del provisioning di oggetti gruppo in Slack</span><span class="sxs-lookup"><span data-stu-id="4be39-153">[Optional] Configuring group object provisioning to Slack</span></span> 

<span data-ttu-id="4be39-154">Facoltativamente, è possibile abilitare il provisioning di oggetti gruppo da Azure AD a Slack.</span><span class="sxs-lookup"><span data-stu-id="4be39-154">Optionally, you can enable the provisioning of group objects from Azure AD to Slack.</span></span> <span data-ttu-id="4be39-155">La differenza rispetto all'assegnazione di gruppi di utenti risiede nel fatto che verrà eseguita la replica da Azure AD a Slack dell'oggetto gruppo effettivo, oltre che dei relativi membri.</span><span class="sxs-lookup"><span data-stu-id="4be39-155">This is different from "assigning groups of users", in that the actual group object in addition to its members will be replicated from Azure AD to Slack.</span></span> <span data-ttu-id="4be39-156">Se si ha un gruppo denominato "Gruppo personale" in Azure AD, ad esempio, in Slack verrà creato un identico gruppo denominato "Gruppo personale".</span><span class="sxs-lookup"><span data-stu-id="4be39-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="to-enable-provisioning-of-group-objects"></a><span data-ttu-id="4be39-157">Per abilitare il provisioning di oggetti gruppo:</span><span class="sxs-lookup"><span data-stu-id="4be39-157">To enable provisioning of group objects:</span></span>

1) <span data-ttu-id="4be39-158">Nella sezione Mapping selezionare **Synchronize Azure Active Directory Groups to Slack** (Sincronizza gruppi di Azure Active Directory in Slack).</span><span class="sxs-lookup"><span data-stu-id="4be39-158">Under the Mappings section, select **Synchronize Azure Active Directory Groups to Slack**.</span></span>

2) <span data-ttu-id="4be39-159">Nel pannello Mapping attributi impostare Abilitato su Sì.</span><span class="sxs-lookup"><span data-stu-id="4be39-159">In the Attribute Mapping blade, set Enabled to Yes.</span></span>

3) <span data-ttu-id="4be39-160">Nella sezione **Mapping degli attributi** esaminare gli attributi gruppo che verranno sincronizzati da Azure AD a Slack.</span><span class="sxs-lookup"><span data-stu-id="4be39-160">In the **Attribute Mappings** section, review the group attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="4be39-161">Si noti che gli attributi selezionati come proprietà **corrispondenti** verranno usati per trovare le corrispondenze con i gruppi in Slack per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="4be39-161">Note that the attributes selected as **Matching** properties will be used to match the groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="4be39-162">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="4be39-162">Click **Save**.</span></span>

<span data-ttu-id="4be39-163">Verrà così eseguita la sincronizzazione completa da Azure AD a Slack di tutti gli oggetti gruppo assegnati a Slack nella sezione **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4be39-163">This result in any group objects assigned to Slack in the **Users and Groups** section being fully synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="4be39-164">È possibile usare la sezione **Dettagli sincronizzazione** per monitorare lo stato di avanzamento e selezionare i collegamenti ai report delle attività di provisioning, che descrivono tutte le azioni eseguite dal servizio di provisioning sull'app Slack.</span><span class="sxs-lookup"><span data-stu-id="4be39-164">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4be39-165">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4be39-165">Additional Resources</span></span>

* [<span data-ttu-id="4be39-166">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="4be39-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="4be39-167">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4be39-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
