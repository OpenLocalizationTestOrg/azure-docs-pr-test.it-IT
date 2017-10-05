---
title: 'Esercitazione: Integrazione di Azure Active Directory con Jive | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Jive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 957b152fdd40d08a867e788b0cb9f7d57ed481e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="bb707-103">Esercitazione: Configurazione di Jive per il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="bb707-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="bb707-104">Questa esercitazione descrive le procedure da eseguire in Jive e Azure AD per effettuare automaticamente il provisioning e il deprovisioning degli account utente da Azure AD a Jive.</span><span class="sxs-lookup"><span data-stu-id="bb707-104">The objective of this tutorial is to show you the steps you need to perform in Jive and Azure AD to automatically provision and de-provision user accounts from Azure AD to Jive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb707-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bb707-105">Prerequisites</span></span>

<span data-ttu-id="bb707-106">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="bb707-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="bb707-107">Un tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bb707-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="bb707-108">Una sottoscrizione di Jive abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="bb707-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="bb707-109">Un account utente in Jive con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="bb707-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-to-jive"></a><span data-ttu-id="bb707-110">Assegnazione di utenti a Jive</span><span class="sxs-lookup"><span data-stu-id="bb707-110">Assigning users to Jive</span></span>

<span data-ttu-id="bb707-111">Per determinare gli utenti che dovranno ricevere l'accesso alle app selezionate, Azure Active Directory usa il concetto delle "assegnazioni".</span><span class="sxs-lookup"><span data-stu-id="bb707-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="bb707-112">Nel contesto del provisioning automatico degli account utente, vengono sincronizzati solo gli utenti e i gruppi che sono stati "assegnati" a un'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb707-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="bb707-113">Prima di configurare e abilitare il servizio di provisioning, è necessario stabilire quali utenti e/o gruppi in Azure AD rappresentano gli utenti che devono accedere all'app Jive.</span><span class="sxs-lookup"><span data-stu-id="bb707-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Jive app.</span></span> <span data-ttu-id="bb707-114">Dopo aver stabilito questo, è possibile assegnare tali utenti all'app Jive seguendo le istruzioni riportate nell'articolo seguente:</span><span class="sxs-lookup"><span data-stu-id="bb707-114">Once decided, you can assign these users to your Jive app by following the instructions here:</span></span>

[<span data-ttu-id="bb707-115">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="bb707-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-jive"></a><span data-ttu-id="bb707-116">Suggerimenti importanti per l'assegnazione di utenti a Jive</span><span class="sxs-lookup"><span data-stu-id="bb707-116">Important tips for assigning users to Jive</span></span>

*   <span data-ttu-id="bb707-117">È consigliabile assegnare un singolo utente di Azure AD a Jive per testare la configurazione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="bb707-117">It is recommended that a single Azure AD user be assigned to Jive to test the provisioning configuration.</span></span> <span data-ttu-id="bb707-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="bb707-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="bb707-119">Quando si assegna un utente a Jive, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="bb707-119">When assigning a user to Jive, you must select a valid user role.</span></span> <span data-ttu-id="bb707-120">Il ruolo "Default Access" (Accesso predefinito) non è applicabile per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="bb707-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="bb707-121">Abilitare il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="bb707-121">Enable User Provisioning</span></span>

<span data-ttu-id="bb707-122">Questa sezione illustra la connessione di Azure AD all'API per il provisioning degli account utente di Jive e la configurazione del servizio di provisioning per la creazione, l'aggiornamento e la disabilitazione degli account utente assegnati in Jive in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb707-122">This section guides you through connecting your Azure AD to Jive's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="bb707-123">Si può anche scegliere di abilitare l'accesso Single Sign-On basato su SAML per Jive, seguendo le istruzioni disponibili nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bb707-123">You may also choose to enabled SAML-based Single Sign-On for Jive, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bb707-124">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="bb707-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="bb707-125">Per configurare il provisioning degli account utente:</span><span class="sxs-lookup"><span data-stu-id="bb707-125">To configure user account provisioning:</span></span>

<span data-ttu-id="bb707-126">Questa sezione descrive come abilitare il provisioning degli account utente di Active Directory in Jive.</span><span class="sxs-lookup"><span data-stu-id="bb707-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Jive.</span></span>
<span data-ttu-id="bb707-127">Come parte di questa procedura, specificare un token di sicurezza utente da richiedere a Jive.com.</span><span class="sxs-lookup"><span data-stu-id="bb707-127">As part of this procedure, you are required to provide a user security token you need to request from Jive.com.</span></span>

1. <span data-ttu-id="bb707-128">Nel [portale di Azure](https://portal.azure.com) passare alla sezione **Azure Active Directory > App aziendali > Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bb707-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="bb707-129">Se si è già configurato Jive per l'accesso Single Sign-On, cercare l'istanza di Jive usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="bb707-129">If you have already configured Jive for single sign-on, search for your instance of Jive using the search field.</span></span> <span data-ttu-id="bb707-130">In caso contrario, selezionare **Aggiungi** e cercare **Jive** nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="bb707-130">Otherwise, select **Add** and search for **Jive** in the application gallery.</span></span> <span data-ttu-id="bb707-131">Selezionare Jive nei risultati della ricerca e aggiungerlo all'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="bb707-131">Select Jive from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="bb707-132">Selezionare l'istanza di Jive e quindi la scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="bb707-132">Select your instance of Jive, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="bb707-133">Impostare **Modalità di provisioning** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="bb707-133">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisioning](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="bb707-135">Nella sezione **Credenziali di amministratore** specificare le impostazioni di configurazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb707-135">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="bb707-136">a.</span><span class="sxs-lookup"><span data-stu-id="bb707-136">a.</span></span> <span data-ttu-id="bb707-137">Nella casella di testo **Jive Admin User Name** (Nome utente amministratore Jive) digitare un nome di account Jive che abbia il profilo **Amministratore di sistema** assegnato in Jive.com.</span><span class="sxs-lookup"><span data-stu-id="bb707-137">In the **Jive Admin User Name** textbox, type a Jive account name that has the **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="bb707-138">b.</span><span class="sxs-lookup"><span data-stu-id="bb707-138">b.</span></span> <span data-ttu-id="bb707-139">Nella casella di testo **Password amministratore Jive** digitare la password per questo account.</span><span class="sxs-lookup"><span data-stu-id="bb707-139">In the **Jive Admin Password** textbox, type the password for this account.</span></span>
   
    <span data-ttu-id="bb707-140">c.</span><span class="sxs-lookup"><span data-stu-id="bb707-140">c.</span></span> <span data-ttu-id="bb707-141">Nella casella di testo **URL tenant di Jive** digitare l'URL del tenant di Jive.</span><span class="sxs-lookup"><span data-stu-id="bb707-141">In the **Jive Tenant URL** textbox, type the Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="bb707-142">L'URL del tenant di Jive è l'URL usato dall'organizzazione per accedere a Jive.</span><span class="sxs-lookup"><span data-stu-id="bb707-142">The Jive tenant URL is URL that is used by your organization to log in to Jive.</span></span>  
      > <span data-ttu-id="bb707-143">L'URL in genere ha il formato seguente: **www.\<organizzazione\>.jive.com**.</span><span class="sxs-lookup"><span data-stu-id="bb707-143">Typically, the URL has the following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="bb707-144">Nel portale di Azure fare clic su **Test connessione** per verificare che Azure AD possa connettersi all'app Jive.</span><span class="sxs-lookup"><span data-stu-id="bb707-144">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Jive app.</span></span>

7. <span data-ttu-id="bb707-145">Immettere l'indirizzo di posta elettronica di una persona o un gruppo che riceverà le notifiche di errore relative al provisioning nel campo **Messaggio di posta elettronica di notifica** e selezionare la casella di controllo seguente.</span><span class="sxs-lookup"><span data-stu-id="bb707-145">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

8. <span data-ttu-id="bb707-146">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="bb707-146">Click **Save.**</span></span>

9. <span data-ttu-id="bb707-147">Nella sezione Mapping selezionare **Synchronize Azure Active Directory Users to Jive** (Sincronizza utenti di Azure Active Directory in Jive).</span><span class="sxs-lookup"><span data-stu-id="bb707-147">Under the Mappings section, select **Synchronize Azure Active Directory Users to Jive.**</span></span>

10. <span data-ttu-id="bb707-148">Nella sezione **Mapping degli attributi** esaminare gli attributi utente che vengono sincronizzati da Azure AD a Jive.</span><span class="sxs-lookup"><span data-stu-id="bb707-148">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Jive.</span></span> <span data-ttu-id="bb707-149">Gli attributi selezionati come proprietà **corrispondenti** vengono usati per trovare le corrispondenze con gli account utente in Jive per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="bb707-149">The attributes selected as **Matching** properties are used to match the user accounts in Jive for update operations.</span></span> <span data-ttu-id="bb707-150">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="bb707-150">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="bb707-151">Per abilitare il servizio di provisioning di Azure AD per Jive, impostare **Stato del provisioning** su **Sì** nella sezione Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="bb707-151">To enable the Azure AD provisioning service for Jive, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="bb707-152">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="bb707-152">Click **Save.**</span></span>

<span data-ttu-id="bb707-153">Viene avviata la sincronizzazione iniziale di tutti gli utenti e/o i gruppi assegnati a Jive nella sezione Utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="bb707-153">It starts the initial synchronization of any users and/or groups assigned to Jive in the Users and Groups section.</span></span> <span data-ttu-id="bb707-154">La sincronizzazione iniziale richiede più tempo delle sincronizzazioni successive, che saranno eseguite circa ogni 20 minuti per tutto il tempo che il servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="bb707-154">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="bb707-155">È possibile usare la sezione **Dettagli sincronizzazione** per monitorare lo stato di avanzamento e selezionare i collegamenti ai report delle attività di provisioning, che descrivono tutte le azioni eseguite dal servizio di provisioning sull'app Jive.</span><span class="sxs-lookup"><span data-stu-id="bb707-155">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Jive app.</span></span>

<span data-ttu-id="bb707-156">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="bb707-156">You can now create a test account.</span></span> <span data-ttu-id="bb707-157">Attendere 20 minuti per verificare che l'account sia stato sincronizzato con Jive.</span><span class="sxs-lookup"><span data-stu-id="bb707-157">Wait for up to 20 minutes to verify that the account has been synchronized to Jive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb707-158">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="bb707-158">Additional resources</span></span>

* [<span data-ttu-id="bb707-159">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="bb707-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb707-160">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb707-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="bb707-161">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bb707-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)