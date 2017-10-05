---
title: 'Esercitazione: Integrazione di Azure Active Directory con Citrix GoToMeeting | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Citrix GoToMeeting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1ddfcd991431a11e5c3e306bd5905003d094ac18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="b01da-103">Esercitazione: Configurazione di Citrix GoToMeeting per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="b01da-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="b01da-104">Questa esercitazione descrive le procedure da eseguire in Citrix GoToMeeting e Azure AD per effettuare automaticamente il provisioning e il deprovisioning degli account utente da Azure AD a Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="b01da-104">The objective of this tutorial is to show you the steps you need to perform in Citrix GoToMeeting and Azure AD to automatically provision and de-provision user accounts from Azure AD to Citrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b01da-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b01da-105">Prerequisites</span></span>

<span data-ttu-id="b01da-106">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b01da-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="b01da-107">Un tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b01da-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="b01da-108">Una sottoscrizione di Citrix GoToMeeting abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b01da-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="b01da-109">Un account utente in Citrix GoToMeeting con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="b01da-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="b01da-110">Assegnazione di utenti a Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="b01da-110">Assigning users to Citrix GoToMeeting</span></span>

<span data-ttu-id="b01da-111">Per determinare gli utenti che dovranno ricevere l'accesso alle app selezionate, Azure Active Directory usa il concetto delle "assegnazioni".</span><span class="sxs-lookup"><span data-stu-id="b01da-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="b01da-112">Nel contesto del provisioning automatico degli account utente, vengono sincronizzati solo gli utenti e i gruppi che sono stati "assegnati" a un'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b01da-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="b01da-113">Prima di configurare e abilitare il servizio di provisioning, è necessario stabilire quali utenti e/o gruppi in Azure AD rappresentano gli utenti che devono accedere all'app Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="b01da-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="b01da-114">Dopo aver stabilito questo, è possibile assegnare tali utenti all'app Citrix GoToMeeting seguendo le istruzioni riportate nell'articolo seguente:</span><span class="sxs-lookup"><span data-stu-id="b01da-114">Once decided, you can assign these users to your Citrix GoToMeeting app by following the instructions here:</span></span>

[<span data-ttu-id="b01da-115">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="b01da-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="b01da-116">Suggerimenti importanti per l'assegnazione di utenti a Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="b01da-116">Important tips for assigning users to Citrix GoToMeeting</span></span>

*   <span data-ttu-id="b01da-117">È consigliabile assegnare un singolo utente di Azure AD a Citrix GoToMeeting per testare la configurazione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="b01da-117">It is recommended that a single Azure AD user is assigned to Citrix GoToMeeting to test the provisioning configuration.</span></span> <span data-ttu-id="b01da-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="b01da-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="b01da-119">Quando si assegna un utente a Citrix GoToMeeting, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="b01da-119">When assigning a user to Citrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="b01da-120">Il ruolo "Default Access" (Accesso predefinito) non è applicabile per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="b01da-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="b01da-121">Abilitare il provisioning utenti automatizzato</span><span class="sxs-lookup"><span data-stu-id="b01da-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="b01da-122">Questa sezione illustra la connessione di Azure AD all'API per il provisioning degli account utente di Citrix GoToMeeting e la configurazione del servizio di provisioning per la creazione, l'aggiornamento e la disabilitazione degli account utente assegnati in Citrix GoToMeeting in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b01da-122">This section guides you through connecting your Azure AD to Citrix GoToMeeting's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="b01da-123">Si può anche scegliere di abilitare l'accesso Single Sign-On basato su SAML per Citrix GoToMeeting, seguendo le istruzioni disponibili nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b01da-123">You may also choose to enabled SAML-based Single Sign-On for Citrix GoToMeeting, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b01da-124">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="b01da-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="b01da-125">Per configurare il provisioning automatico degli account utente:</span><span class="sxs-lookup"><span data-stu-id="b01da-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="b01da-126">Nel [portale di Azure](https://portal.azure.com) passare alla sezione **Azure Active Directory > App aziendali > Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b01da-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="b01da-127">Se si è già configurato Citrix GoToMeeting per l'accesso Single Sign-On, cercare l'istanza di Citrix GoToMeeting usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="b01da-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using the search field.</span></span> <span data-ttu-id="b01da-128">In caso contrario, selezionare **Aggiungi** e cercare **Citrix GoToMeeting** nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b01da-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in the application gallery.</span></span> <span data-ttu-id="b01da-129">Selezionare Citrix GoToMeeting nei risultati della ricerca e aggiungerlo all'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b01da-129">Select Citrix GoToMeeting from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="b01da-130">Selezionare l'istanza di Citrix GoToMeeting e quindi la scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="b01da-130">Select your instance of Citrix GoToMeeting, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="b01da-131">Impostare **Modalità di provisioning** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="b01da-131">Set the **Provisioning** Mode to **Automatic**.</span></span> 

    ![provisioning](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="b01da-133">Nella sezione Credenziali amministratore, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b01da-133">Under the Admin Credentials section, perform the following steps:</span></span>
   
    <span data-ttu-id="b01da-134">a.</span><span class="sxs-lookup"><span data-stu-id="b01da-134">a.</span></span> <span data-ttu-id="b01da-135">Nella casella di testo **Nome utente amministratore Citrix GoToMeeting** digitare il nome utente di un amministratore.</span><span class="sxs-lookup"><span data-stu-id="b01da-135">In the **Citrix GoToMeeting Admin User Name** textbox, type the user name of an administrator.</span></span>

    <span data-ttu-id="b01da-136">b.</span><span class="sxs-lookup"><span data-stu-id="b01da-136">b.</span></span> <span data-ttu-id="b01da-137">Nella casella di testo **Password amministratore Citrix GoToMeeting** digitare la password dell'amministratore.</span><span class="sxs-lookup"><span data-stu-id="b01da-137">In the **Citrix GoToMeeting Admin Password** textbox, the administrator's password.</span></span>

6. <span data-ttu-id="b01da-138">Nel portale di Azure fare clic su **Test connessione** per verificare che Azure AD possa connettersi all'app Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="b01da-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="b01da-139">Se la connessione non riesce, verificare che l'account Citrix GoToMeeting abbia autorizzazioni di amministratore di team e ripetere il passaggio **Credenziali amministratore**.</span><span class="sxs-lookup"><span data-stu-id="b01da-139">If the connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try the **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="b01da-140">Immettere l'indirizzo di posta elettronica di una persona o un gruppo che riceverà le notifiche di errore relative al provisioning nel campo **Messaggio di posta elettronica di notifica** e selezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="b01da-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="b01da-141">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b01da-141">Click **Save.**</span></span>

9. <span data-ttu-id="b01da-142">Nella sezione Mapping selezionare **Synchronize Azure Active Directory Users to Citrix GoToMeeting** (Sincronizza utenti di Azure Active Directory in Citrix GoToMeeting).</span><span class="sxs-lookup"><span data-stu-id="b01da-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Citrix GoToMeeting.**</span></span>

10. <span data-ttu-id="b01da-143">Nella sezione **Mapping degli attributi** esaminare gli attributi utente che vengono sincronizzati da Azure AD a Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="b01da-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Citrix GoToMeeting.</span></span> <span data-ttu-id="b01da-144">Gli attributi selezionati come proprietà **corrispondenti** vengono usati per trovare le corrispondenze con gli account utente in Citrix GoToMeeting per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="b01da-144">The attributes selected as **Matching** properties are used to match the user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="b01da-145">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="b01da-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="b01da-146">Per abilitare il servizio di provisioning di Azure AD per Citrix GoToMeeting, impostare **Stato del provisioning** su **Sì** nella sezione Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="b01da-146">To enable the Azure AD provisioning service for Citrix GoToMeeting, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="b01da-147">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b01da-147">Click **Save.**</span></span>

<span data-ttu-id="b01da-148">Viene avviata la sincronizzazione iniziale di tutti gli utenti e/o i gruppi assegnati a Citrix GoToMeeting nella sezione Utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="b01da-148">It starts the initial synchronization of any users and/or groups assigned to Citrix GoToMeeting in the Users and Groups section.</span></span> <span data-ttu-id="b01da-149">La sincronizzazione iniziale richiede più tempo delle sincronizzazioni successive, che saranno eseguite circa ogni 20 minuti per tutto il tempo che il servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b01da-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="b01da-150">È possibile usare la sezione **Dettagli sincronizzazione** per monitorare lo stato di avanzamento e selezionare i collegamenti ai report delle attività di provisioning, che descrivono tutte le azioni eseguite dal servizio di provisioning sull'app Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="b01da-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b01da-151">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b01da-151">Additional resources</span></span>

* [<span data-ttu-id="b01da-152">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="b01da-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b01da-153">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b01da-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b01da-154">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b01da-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


