---
title: 'Esercitazione: Integrazione di Azure Active Directory con DocuSign | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e DocuSign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 294cd6b8-74d7-44bc-92bc-020ccd13ff12
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 3b509ffa934949200277ae431761d2accd4a02d6
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a><span data-ttu-id="ea2c2-103">Esercitazione: Configurazione di DocuSign per il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="ea2c2-103">Tutorial: Configuring DocuSign for User Provisioning</span></span>

<span data-ttu-id="ea2c2-104">Questa esercitazione descrive le procedure da eseguire in DocuSign e Azure AD per effettuare automaticamente il provisioning e il deprovisioning degli account utente da Azure AD a DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-104">The objective of this tutorial is to show you the steps you need to perform in DocuSign and Azure AD to automatically provision and de-provision user accounts from Azure AD to DocuSign.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea2c2-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ea2c2-105">Prerequisites</span></span>

<span data-ttu-id="ea2c2-106">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ea2c2-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="ea2c2-107">Un tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="ea2c2-108">Una sottoscrizione di DocuSign abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-108">A DocuSign single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="ea2c2-109">Un account utente in DocuSign con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-109">A user account in DocuSign with Team Admin permissions.</span></span>

## <a name="assigning-users-to-docusign"></a><span data-ttu-id="ea2c2-110">Assegnazione di utenti a DocuSign</span><span class="sxs-lookup"><span data-stu-id="ea2c2-110">Assigning users to DocuSign</span></span>

<span data-ttu-id="ea2c2-111">Per determinare gli utenti che dovranno ricevere l'accesso alle app selezionate, Azure Active Directory usa il concetto delle "assegnazioni".</span><span class="sxs-lookup"><span data-stu-id="ea2c2-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="ea2c2-112">Nel contesto del provisioning automatico degli account utente, vengono sincronizzati solo gli utenti e i gruppi che sono stati "assegnati" a un'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="ea2c2-113">Prima di configurare e abilitare il servizio di provisioning, è necessario stabilire quali utenti e/o gruppi in Azure AD rappresentano gli utenti che devono accedere all'app DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your DocuSign app.</span></span> <span data-ttu-id="ea2c2-114">Dopo aver stabilito questo, è possibile assegnare tali utenti all'app DocuSign seguendo le istruzioni riportate nell'articolo seguente:</span><span class="sxs-lookup"><span data-stu-id="ea2c2-114">Once decided, you can assign these users to your DocuSign app by following the instructions here:</span></span>

[<span data-ttu-id="ea2c2-115">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="ea2c2-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-docusign"></a><span data-ttu-id="ea2c2-116">Suggerimenti importanti per l'assegnazione di utenti a DocuSign</span><span class="sxs-lookup"><span data-stu-id="ea2c2-116">Important tips for assigning users to DocuSign</span></span>

*   <span data-ttu-id="ea2c2-117">È consigliabile assegnare un singolo utente di Azure AD a DocuSign per testare la configurazione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-117">It is recommended that a single Azure AD user is assigned to DocuSign to test the provisioning configuration.</span></span> <span data-ttu-id="ea2c2-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="ea2c2-119">Quando si assegna un utente a DocuSign, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-119">When assigning a user to DocuSign, you must select a valid user role.</span></span> <span data-ttu-id="ea2c2-120">Il ruolo "Default Access" (Accesso predefinito) non è applicabile per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="ea2c2-121">Abilitare il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="ea2c2-121">Enable User Provisioning</span></span>

<span data-ttu-id="ea2c2-122">Questa sezione illustra la connessione di Azure AD all'API per il provisioning degli account utente di DocuSign e la configurazione del servizio di provisioning per la creazione, l'aggiornamento e la disabilitazione degli account utente assegnati in DocuSign in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-122">This section guides you through connecting your Azure AD to DocuSign's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in DocuSign based on user and group assignment in Azure AD.</span></span>

> [!Tip]
> <span data-ttu-id="ea2c2-123">Si può anche scegliere di abilitare l'accesso Single Sign-On basato su SAML per DocuSign, seguendo le istruzioni disponibili nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ea2c2-123">You may also choose to enabled SAML-based Single Sign-On for DocuSign, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ea2c2-124">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="ea2c2-125">Per configurare il provisioning degli account utente:</span><span class="sxs-lookup"><span data-stu-id="ea2c2-125">To configure user account provisioning:</span></span>

<span data-ttu-id="ea2c2-126">Questa sezione descrive come abilitare il provisioning degli account utente di Active Directory in DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to DocuSign.</span></span>

1. <span data-ttu-id="ea2c2-127">Nel [portale di Azure](https://portal.azure.com) passare alla sezione **Azure Active Directory > App aziendali > Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="ea2c2-128">Se si è già configurato DocuSign per l'accesso Single Sign-On, cercare l'istanza di DocuSign usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-128">If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using the search field.</span></span> <span data-ttu-id="ea2c2-129">In caso contrario, selezionare **Aggiungi** e cercare **DocuSign** nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-129">Otherwise, select **Add** and search for **DocuSign** in the application gallery.</span></span> <span data-ttu-id="ea2c2-130">Selezionare DocuSign nei risultati della ricerca e aggiungerlo all'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-130">Select DocuSign from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="ea2c2-131">Selezionare l'istanza di DocuSign e quindi la scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-131">Select your instance of DocuSign, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="ea2c2-132">Impostare **Modalità di provisioning** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-132">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisioning](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="ea2c2-134">Nella sezione **Credenziali di amministratore** specificare le impostazioni di configurazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="ea2c2-134">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="ea2c2-135">a.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-135">a.</span></span> <span data-ttu-id="ea2c2-136">Nella casella di testo **Nome utente amministratore** digitare un nome di account DocuSign che abbia il profilo **Amministratore di sistema** assegnato in DocuSign.com.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-136">In the **Admin User Name** textbox, type a DocuSign account name that has the **System Administrator** profile in DocuSign.com assigned.</span></span>
   
    <span data-ttu-id="ea2c2-137">b.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-137">b.</span></span> <span data-ttu-id="ea2c2-138">Nella casella di testo **Password amministratore** digitare la password per questo account.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-138">In the **Admin Password** textbox, type the password for this account.</span></span>

6. <span data-ttu-id="ea2c2-139">Nel portale di Azure fare clic su **Test connessione** per verificare che Azure AD possa connettersi all'app DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your DocuSign app.</span></span>

7. <span data-ttu-id="ea2c2-140">Nel campo **Messaggio di posta elettronica di notifica** immettere l'indirizzo di posta elettronica di una persona o un gruppo che riceverà le notifiche di errore relative al provisioning e selezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

8. <span data-ttu-id="ea2c2-141">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-141">Click **Save.**</span></span>

9. <span data-ttu-id="ea2c2-142">Nella sezione Mapping selezionare **Synchronize Azure Active Directory Users to DocuSign** (Sincronizza utenti di Azure Active Directory in DocuSign).</span><span class="sxs-lookup"><span data-stu-id="ea2c2-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to DocuSign.**</span></span>

10. <span data-ttu-id="ea2c2-143">Nella sezione **Mapping degli attributi** esaminare gli attributi utente che vengono sincronizzati da Azure AD a DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to DocuSign.</span></span> <span data-ttu-id="ea2c2-144">Gli attributi selezionati come proprietà **corrispondenti** vengono usati per trovare le corrispondenze con gli account utente in DocuSign per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-144">The attributes selected as **Matching** properties are used to match the user accounts in DocuSign for update operations.</span></span> <span data-ttu-id="ea2c2-145">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="ea2c2-146">Per abilitare il servizio di provisioning di Azure AD per DocuSign, impostare **Stato del provisioning** su **Sì** nella sezione Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-146">To enable the Azure AD provisioning service for DocuSign, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="ea2c2-147">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-147">Click **Save.**</span></span>

<span data-ttu-id="ea2c2-148">Viene avviata la sincronizzazione iniziale di tutti gli utenti e/o i gruppi assegnati a DocuSign nella sezione Utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-148">It starts the initial synchronization of any users and/or groups assigned to DocuSign in the Users and Groups section.</span></span> <span data-ttu-id="ea2c2-149">La sincronizzazione iniziale richiede più tempo delle sincronizzazioni successive, che saranno eseguite circa ogni 20 minuti per tutto il tempo che il servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="ea2c2-150">È possibile usare la sezione **Dettagli sincronizzazione** per monitorare lo stato di avanzamento e selezionare i collegamenti ai report delle attività di provisioning, che descrivono tutte le azioni eseguite dal servizio di provisioning sull'app DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your DocuSign app.</span></span>

<span data-ttu-id="ea2c2-151">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-151">You can now create a test account.</span></span> <span data-ttu-id="ea2c2-152">Attendere 20 minuti per verificare che l'account sia stato sincronizzato con DocuSign.</span><span class="sxs-lookup"><span data-stu-id="ea2c2-152">Wait for up to 20 minutes to verify that the account has been synchronized to DocuSign.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ea2c2-153">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ea2c2-153">Additional resources</span></span>

* [<span data-ttu-id="ea2c2-154">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="ea2c2-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea2c2-155">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea2c2-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ea2c2-156">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ea2c2-156">Configure Single Sign-on</span></span>](active-directory-saas-docusign-tutorial.md)