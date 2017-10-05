---
title: 'Esercitazione: Configurazione di LucidChart per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come configurare Azure Active Directory per effettuare automaticamente il provisioning e il deprovisioning degli account utente in LucidChart.
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: 1f9344a5e750360e21ed7dc8e3ed013c2c2e1a45
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="8def7-103">Esercitazione: Configurazione di LucidChart per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="8def7-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="8def7-104">Questa esercitazione descrive le procedure da eseguire in LucidChart e Azure AD per effettuare automaticamente il provisioning e il deprovisioning degli account utente da Azure AD a LucidChart.</span><span class="sxs-lookup"><span data-stu-id="8def7-104">The objective of this tutorial is to show you the steps you need to perform in LucidChart and Azure AD to automatically provision and de-provision user accounts from Azure AD to LucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8def7-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8def7-105">Prerequisites</span></span>

<span data-ttu-id="8def7-106">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="8def7-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="8def7-107">Un tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8def7-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="8def7-108">Un tenant di LucidChart con il [piano Enterprise](https://www.lucidchart.com/user/117598685#/subscriptionLevel) o superiore abilitato</span><span class="sxs-lookup"><span data-stu-id="8def7-108">A LucidChart tenant with the [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="8def7-109">Un account utente in LucidChart con autorizzazioni di amministratore</span><span class="sxs-lookup"><span data-stu-id="8def7-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-to-lucidchart"></a><span data-ttu-id="8def7-110">Assegnazione di utenti a LucidChart</span><span class="sxs-lookup"><span data-stu-id="8def7-110">Assigning users to LucidChart</span></span>

<span data-ttu-id="8def7-111">Per determinare gli utenti che dovranno ricevere l'accesso alle app selezionate, Azure Active Directory usa il concetto delle "assegnazioni".</span><span class="sxs-lookup"><span data-stu-id="8def7-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="8def7-112">Nel contesto del provisioning automatico degli account utente, vengono sincronizzati solo gli utenti e i gruppi che sono stati "assegnati" a un'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8def7-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="8def7-113">Prima di configurare e abilitare il servizio di provisioning, è necessario stabilire quali utenti e/o gruppi in Azure AD rappresentano gli utenti che devono accedere all'app LucidChart.</span><span class="sxs-lookup"><span data-stu-id="8def7-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your LucidChart app.</span></span> <span data-ttu-id="8def7-114">Dopo aver stabilito questo, è possibile assegnare tali utenti all'app LucidChart seguendo le istruzioni riportate nell'articolo seguente:</span><span class="sxs-lookup"><span data-stu-id="8def7-114">Once decided, you can assign these users to your LucidChart app by following the instructions here:</span></span>

[<span data-ttu-id="8def7-115">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="8def7-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-lucidchart"></a><span data-ttu-id="8def7-116">Suggerimenti importanti per l'assegnazione di utenti a LucidChart</span><span class="sxs-lookup"><span data-stu-id="8def7-116">Important tips for assigning users to LucidChart</span></span>

*   <span data-ttu-id="8def7-117">È consigliabile assegnare un singolo utente di Azure AD a LucidChart per testare la configurazione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="8def7-117">It is recommended that a single Azure AD user is assigned to LucidChart to test the provisioning configuration.</span></span> <span data-ttu-id="8def7-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="8def7-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="8def7-119">Quando si assegna un utente a LucidChart, è necessario selezionare il ruolo **Utente** o un altro ruolo specifico dell'applicazione valido, se disponibile, nella finestra di dialogo di assegnazione.</span><span class="sxs-lookup"><span data-stu-id="8def7-119">When assigning a user to LucidChart, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="8def7-120">Poiché il ruolo **Accesso predefinito** non è applicabile per il provisioning, i relativi utenti vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="8def7-120">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-lucidchart"></a><span data-ttu-id="8def7-121">Configurazione del provisioning utenti in LucidChart</span><span class="sxs-lookup"><span data-stu-id="8def7-121">Configuring user provisioning to LucidChart</span></span> 

<span data-ttu-id="8def7-122">Questa sezione illustra la connessione di Azure AD all'API per il provisioning degli account utente di LucidChart e la configurazione del servizio di provisioning per la creazione, l'aggiornamento e la disabilitazione degli account utente assegnati in LucidChart in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8def7-122">This section guides you through connecting your Azure AD to LucidChart's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="8def7-123">Si può anche scegliere di abilitare l'accesso Single Sign-On basato su SAML per LucidChart, seguendo le istruzioni disponibili nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8def7-123">You may also choose to enabled SAML-based Single Sign-On for LucidChart, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8def7-124">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="8def7-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-lucidchart-in-azure-ad"></a><span data-ttu-id="8def7-125">Configurare il provisioning automatico degli account utente in LucidChart con Azure AD</span><span class="sxs-lookup"><span data-stu-id="8def7-125">Configure automatic user account provisioning to LucidChart in Azure AD</span></span>


1. <span data-ttu-id="8def7-126">Nel [portale di Azure](https://portal.azure.com) passare alla sezione **Azure Active Directory > App aziendali > Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8def7-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="8def7-127">Se si è già configurato LucidChart per l'accesso Single Sign-On, cercare l'istanza di LucidChart usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="8def7-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using the search field.</span></span> <span data-ttu-id="8def7-128">In caso contrario, selezionare **Aggiungi** e cercare **LucidChart** nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8def7-128">Otherwise, select **Add** and search for **LucidChart** in the application gallery.</span></span> <span data-ttu-id="8def7-129">Selezionare LucidChart nei risultati della ricerca e aggiungerlo all'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8def7-129">Select LucidChart from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="8def7-130">Selezionare l'istanza di LucidChart e quindi la scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="8def7-130">Select your instance of LucidChart, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="8def7-131">Impostare **Modalità di provisioning** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="8def7-131">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Provisioning di LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="8def7-133">Nella sezione **Credenziali amministratore** immettere il **Token segreto** generato dall'account di LucidChart. È possibile trovare il token nell'account: **Team** > **App Integration** > **SCIM** (Team, Integrazione app, SCIM).</span><span class="sxs-lookup"><span data-stu-id="8def7-133">Under the **Admin Credentials** section, input the **Secret Token** generated by your LucidChart's account (you can find the token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![Provisioning di LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="8def7-135">Nel portale di Azure fare clic su **Test connessione** per verificare che Azure AD possa connettersi all'app LucidChart.</span><span class="sxs-lookup"><span data-stu-id="8def7-135">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your LucidChart app.</span></span> <span data-ttu-id="8def7-136">Se la connessione non riesce, verificare che l'account LucidChart abbia autorizzazioni di amministratore e ripetere il passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="8def7-136">If the connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="8def7-137">Immettere l'indirizzo di posta elettronica di una persona o un gruppo che riceverà le notifiche di errore relative al provisioning nel campo **Messaggio di posta elettronica di notifica** e selezionare la casella di controllo "Invia una notifica di posta elettronica in caso di errore".</span><span class="sxs-lookup"><span data-stu-id="8def7-137">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="8def7-138">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8def7-138">Click **Save**.</span></span> 

9. <span data-ttu-id="8def7-139">Nella sezione Mapping selezionare **Synchronize Azure Active Directory Users to LucidChart** (Sincronizza utenti di Azure Active Directory in LucidChart).</span><span class="sxs-lookup"><span data-stu-id="8def7-139">Under the Mappings section, select **Synchronize Azure Active Directory Users to LucidChart**.</span></span>

10. <span data-ttu-id="8def7-140">Nella sezione **Mapping degli attributi** esaminare gli attributi utente che vengono sincronizzati da Azure AD a LucidChart.</span><span class="sxs-lookup"><span data-stu-id="8def7-140">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to LucidChart.</span></span> <span data-ttu-id="8def7-141">Gli attributi selezionati come proprietà **corrispondenti** vengono usati per trovare le corrispondenze con gli account utente in LucidChart per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="8def7-141">The attributes selected as **Matching** properties are used to match the user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="8def7-142">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="8def7-142">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="8def7-143">Per abilitare il servizio di provisioning di Azure AD per LucidChart, impostare **Stato del provisioning** su **Sì** nella sezione **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="8def7-143">To enable the Azure AD provisioning service for LucidChart, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="8def7-144">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8def7-144">Click **Save**.</span></span> 

<span data-ttu-id="8def7-145">L'operazione avvia la sincronizzazione iniziale di tutti gli utenti e/o i gruppi assegnati a LucidChart nella sezione Utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="8def7-145">This operation starts the initial synchronization of any users and/or groups assigned to LucidChart in the Users and Groups section.</span></span> <span data-ttu-id="8def7-146">La sincronizzazione iniziale richiede più tempo delle sincronizzazioni successive, che saranno eseguite circa ogni 20 minuti per tutto il tempo che il servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8def7-146">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="8def7-147">È possibile usare la sezione **Dettagli sincronizzazione** per monitorare lo stato di avanzamento e selezionare i collegamenti ai report delle attività di provisioning che descrivono tutte le azioni eseguite dal servizio di provisioning.</span><span class="sxs-lookup"><span data-stu-id="8def7-147">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="8def7-148">Per altre informazioni sulla lettura dei log di provisioning di Azure AD, vedere [Esercitazione: creazione di report sul provisioning automatico degli account utente](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="8def7-148">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8def7-149">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8def7-149">Additional resources</span></span>

* [<span data-ttu-id="8def7-150">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="8def7-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="8def7-151">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8def7-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="8def7-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8def7-152">Next steps</span></span>

* [<span data-ttu-id="8def7-153">Informazioni su come esaminare i log e ottenere report sulle attività di provisioning</span><span class="sxs-lookup"><span data-stu-id="8def7-153">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
