---
title: 'Esercitazione: Integrazione di Azure Active Directory con NetSuite | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Netsuite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 277c393536615fc8bfe8af0bc6d487115f04776c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="be5fa-103">Esercitazione: Configurazione di Netsuite per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="be5fa-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="be5fa-104">Questa esercitazione descrive le procedure da eseguire in Netsuite e Azure AD per effettuare automaticamente il provisioning e il deprovisioning degli account utente da Azure AD a Netsuite.</span><span class="sxs-lookup"><span data-stu-id="be5fa-104">The objective of this tutorial is to show you the steps you need to perform in Netsuite and Azure AD to automatically provision and de-provision user accounts from Azure AD to Netsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be5fa-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="be5fa-105">Prerequisites</span></span>

<span data-ttu-id="be5fa-106">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="be5fa-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="be5fa-107">Tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="be5fa-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="be5fa-108">Sottoscrizione di Netsuite abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="be5fa-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="be5fa-109">Account utente in Netsuite con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="be5fa-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-to-netsuite"></a><span data-ttu-id="be5fa-110">Assegnazione di utenti a Netsuite</span><span class="sxs-lookup"><span data-stu-id="be5fa-110">Assigning users to Netsuite</span></span>

<span data-ttu-id="be5fa-111">Per determinare gli utenti che dovranno ricevere l'accesso alle app selezionate, Azure Active Directory usa il concetto delle "assegnazioni".</span><span class="sxs-lookup"><span data-stu-id="be5fa-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="be5fa-112">Nel contesto del provisioning automatico degli account utente, vengono sincronizzati solo gli utenti e i gruppi che sono stati "assegnati" a un'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be5fa-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="be5fa-113">Prima di configurare e abilitare il servizio di provisioning, è necessario stabilire quali utenti e/o gruppi in Azure AD rappresentano gli utenti che devono accedere all'app Netsuite.</span><span class="sxs-lookup"><span data-stu-id="be5fa-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Netsuite app.</span></span> <span data-ttu-id="be5fa-114">Dopo averlo stabilito, è possibile assegnare gli utenti all'app Netsuite seguendo le istruzioni riportate in:</span><span class="sxs-lookup"><span data-stu-id="be5fa-114">Once decided, you can assign these users to your Netsuite app by following the instructions here:</span></span>

[<span data-ttu-id="be5fa-115">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="be5fa-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-netsuite"></a><span data-ttu-id="be5fa-116">Suggerimenti importanti per l'assegnazione di utenti a Netsuite</span><span class="sxs-lookup"><span data-stu-id="be5fa-116">Important tips for assigning users to Netsuite</span></span>

*   <span data-ttu-id="be5fa-117">È consigliabile assegnare un singolo utente di Azure AD a Netsuite per testare la configurazione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="be5fa-117">It is recommended that a single Azure AD user is assigned to Netsuite to test the provisioning configuration.</span></span> <span data-ttu-id="be5fa-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="be5fa-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="be5fa-119">Quando si assegna un utente a Netsuite, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="be5fa-119">When assigning a user to Netsuite, you must select a valid user role.</span></span> <span data-ttu-id="be5fa-120">Il ruolo "Default Access" (Accesso predefinito) non è applicabile per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="be5fa-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="be5fa-121">Abilitare il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="be5fa-121">Enable User Provisioning</span></span>

<span data-ttu-id="be5fa-122">Questa sezione illustra la connessione di Azure AD all'API per il provisioning degli account utente di Netsuite e la configurazione del servizio di provisioning per la creazione, l'aggiornamento e la disabilitazione degli account utente assegnati in Netsuite in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be5fa-122">This section guides you through connecting your Azure AD to Netsuite's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="be5fa-123">Si può anche scegliere di abilitare l'accesso Single Sign-On basato su SAML per Netsuite, seguendo le istruzioni disponibili nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="be5fa-123">You may also choose to enabled SAML-based Single Sign-On for Netsuite, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="be5fa-124">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="be5fa-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="be5fa-125">Per configurare il provisioning degli account utente:</span><span class="sxs-lookup"><span data-stu-id="be5fa-125">To configure user account provisioning:</span></span>

<span data-ttu-id="be5fa-126">Questa sezione descrive come abilitare il provisioning degli account utente di Active Directory in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="be5fa-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Netsuite.</span></span>

1. <span data-ttu-id="be5fa-127">Nel [portale di Azure](https://portal.azure.com) passare alla sezione **Azure Active Directory > App aziendali > Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="be5fa-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="be5fa-128">Se si è già configurato Netsuite per l'accesso Single Sign-On, cercare l'istanza di Netsuite usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="be5fa-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using the search field.</span></span> <span data-ttu-id="be5fa-129">In caso contrario, selezionare **Aggiungi** e cercare **Netsuite** nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="be5fa-129">Otherwise, select **Add** and search for **Netsuite** in the application gallery.</span></span> <span data-ttu-id="be5fa-130">Selezionare Netsuite nei risultati della ricerca e aggiungerlo all'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="be5fa-130">Select Netsuite from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="be5fa-131">Selezionare l'istanza di Netsuite e quindi la scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="be5fa-131">Select your instance of Netsuite, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="be5fa-132">Impostare **Modalità di provisioning** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="be5fa-132">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisioning](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="be5fa-134">Nella sezione **Credenziali di amministratore** specificare le impostazioni di configurazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="be5fa-134">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="be5fa-135">a.</span><span class="sxs-lookup"><span data-stu-id="be5fa-135">a.</span></span> <span data-ttu-id="be5fa-136">Nella casella di testo **Nome utente amministratore** digitare un nome di account Netsuite che abbia il profilo **Amministratore di sistema** assegnato in Netsuite.com.</span><span class="sxs-lookup"><span data-stu-id="be5fa-136">In the **Admin User Name** textbox, type a Netsuite account name that has the **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="be5fa-137">b.</span><span class="sxs-lookup"><span data-stu-id="be5fa-137">b.</span></span> <span data-ttu-id="be5fa-138">Nella casella di testo **Password amministratore** digitare la password per questo account.</span><span class="sxs-lookup"><span data-stu-id="be5fa-138">In the **Admin Password** textbox, type the password for this account.</span></span>
      
6. <span data-ttu-id="be5fa-139">Nel portale di Azure fare clic su **Test connessione** per verificare che Azure AD possa connettersi all'app Netsuite.</span><span class="sxs-lookup"><span data-stu-id="be5fa-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Netsuite app.</span></span>

7. <span data-ttu-id="be5fa-140">Nel campo **Messaggio di posta elettronica di notifica** immettere l'indirizzo di posta elettronica di una persona o un gruppo che riceverà le notifiche di errore relative al provisioning e selezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="be5fa-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

8. <span data-ttu-id="be5fa-141">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="be5fa-141">Click **Save.**</span></span>

9. <span data-ttu-id="be5fa-142">Nella sezione Mapping selezionare **Synchronize Azure Active Directory Users to Netsuite** (Sincronizza utenti di Azure Active Directory in Netsuite).</span><span class="sxs-lookup"><span data-stu-id="be5fa-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Netsuite.**</span></span>

10. <span data-ttu-id="be5fa-143">Nella sezione **Mapping degli attributi** esaminare gli attributi utente che vengono sincronizzati da Azure AD a Netsuite.</span><span class="sxs-lookup"><span data-stu-id="be5fa-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Netsuite.</span></span> <span data-ttu-id="be5fa-144">Si noti che gli attributi selezionati come proprietà **corrispondenti** vengono usati per trovare le corrispondenze con gli account utente in Netsuite per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="be5fa-144">Note that the attributes selected as **Matching** properties are used to match the user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="be5fa-145">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="be5fa-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="be5fa-146">Per abilitare il servizio di provisioning di Azure AD per Netsuite, impostare **Stato del provisioning** su **Sì** nella sezione Impostazioni</span><span class="sxs-lookup"><span data-stu-id="be5fa-146">To enable the Azure AD provisioning service for Netsuite, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="be5fa-147">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="be5fa-147">Click **Save.**</span></span>

<span data-ttu-id="be5fa-148">Viene avviata la sincronizzazione iniziale di tutti gli utenti e/o i gruppi assegnati a Netsuite nella sezione Utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="be5fa-148">It starts the initial synchronization of any users and/or groups assigned to Netsuite in the Users and Groups section.</span></span> <span data-ttu-id="be5fa-149">Notare che la sincronizzazione iniziale richiede più tempo delle sincronizzazioni successive, che saranno eseguite circa ogni 20 minuti per tutto il tempo che il servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="be5fa-149">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="be5fa-150">È possibile usare la sezione **Dettagli sincronizzazione** per monitorare lo stato di avanzamento e selezionare i collegamenti ai report delle attività di provisioning, che descrivono tutte le azioni eseguite dal servizio di provisioning sull'app Netsuite.</span><span class="sxs-lookup"><span data-stu-id="be5fa-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="be5fa-151">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="be5fa-151">You can now create a test account.</span></span> <span data-ttu-id="be5fa-152">Attendere 20 minuti per verificare che l'account sia stato sincronizzato con Netsuite.</span><span class="sxs-lookup"><span data-stu-id="be5fa-152">Wait for up to 20 minutes to verify that the account has been synchronized to Netsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="be5fa-153">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="be5fa-153">Additional resources</span></span>

* [<span data-ttu-id="be5fa-154">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="be5fa-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="be5fa-155">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be5fa-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="be5fa-156">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="be5fa-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)