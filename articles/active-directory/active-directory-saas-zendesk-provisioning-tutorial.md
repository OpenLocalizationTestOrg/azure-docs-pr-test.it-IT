---
title: 'Esercitazione: Configurazione di ZenDesk per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come configurare Azure Active Directory per effettuare automaticamente il provisioning e il deprovisioning degli account utente in ZenDesk.
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
ms.openlocfilehash: 1a1414eefd20e6d7c025da08cfd5ae7c45daad33
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a><span data-ttu-id="d759c-103">Esercitazione: Configurazione di ZenDesk per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="d759c-103">Tutorial: Configuring ZenDesk for Automatic User Provisioning</span></span>


<span data-ttu-id="d759c-104">Questa esercitazione descrive le procedure da eseguire in ZenDesk e Azure AD per effettuare automaticamente il provisioning e il deprovisioning degli account utente da Azure AD a ZenDesk.</span><span class="sxs-lookup"><span data-stu-id="d759c-104">The objective of this tutorial is to show you the steps you need to perform in ZenDesk and Azure AD to automatically provision and de-provision user accounts from Azure AD to ZenDesk.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d759c-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d759c-105">Prerequisites</span></span>

<span data-ttu-id="d759c-106">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="d759c-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="d759c-107">Tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d759c-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="d759c-108">Tenant di ZenDesk con il [piano Enterprise](https://www.zendesk.com/product/pricing/) o superiore abilitato</span><span class="sxs-lookup"><span data-stu-id="d759c-108">A ZenDesk tenant with the [Enterprise plan](https://www.zendesk.com/product/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="d759c-109">Account utente in ZenDesk con autorizzazioni di amministratore</span><span class="sxs-lookup"><span data-stu-id="d759c-109">A user account in ZenDesk with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="d759c-110">L'integrazione del provisioning di Azure AD è basata sull'[API REST di ZenDesk](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api) disponibile per i team ZenDesk con piano Essential o superiore.</span><span class="sxs-lookup"><span data-stu-id="d759c-110">The Azure AD provisioning integration relies on the [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), which is available to ZenDesk teams on the Essential plan or better.</span></span>

## <a name="assigning-users-to-zendesk"></a><span data-ttu-id="d759c-111">Assegnazione di utenti a ZenDesk</span><span class="sxs-lookup"><span data-stu-id="d759c-111">Assigning users to ZenDesk</span></span>

<span data-ttu-id="d759c-112">Per determinare gli utenti che dovranno ricevere l'accesso alle app selezionate, Azure Active Directory usa il concetto delle "assegnazioni".</span><span class="sxs-lookup"><span data-stu-id="d759c-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="d759c-113">Nel contesto del provisioning automatico degli account utente, vengono sincronizzati solo gli utenti e i gruppi che sono stati "assegnati" a un'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d759c-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="d759c-114">Prima di configurare e abilitare il servizio di provisioning, è necessario stabilire quali utenti e/o gruppi in Azure AD rappresentano gli utenti che devono accedere all'app ZenDesk.</span><span class="sxs-lookup"><span data-stu-id="d759c-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your ZenDesk app.</span></span> <span data-ttu-id="d759c-115">Dopo averlo stabilito, è possibile assegnare gli utenti all'app ZenDesk seguendo le istruzioni riportate in:</span><span class="sxs-lookup"><span data-stu-id="d759c-115">Once decided, you can assign these users to your ZenDesk app by following the instructions here:</span></span>

[<span data-ttu-id="d759c-116">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="d759c-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-zendesk"></a><span data-ttu-id="d759c-117">Suggerimenti importanti per l'assegnazione di utenti a ZenDesk</span><span class="sxs-lookup"><span data-stu-id="d759c-117">Important tips for assigning users to ZenDesk</span></span>

*   <span data-ttu-id="d759c-118">È consigliabile assegnare un singolo utente di Azure AD a ZenDesk per testare la configurazione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="d759c-118">It is recommended that a single Azure AD user is assigned to ZenDesk to test the provisioning configuration.</span></span> <span data-ttu-id="d759c-119">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="d759c-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="d759c-120">Quando si assegna un utente a ZenDesk, è necessario selezionare il ruolo **Utente** o un altro ruolo specifico dell'applicazione valido, se disponibile, nella finestra di dialogo di assegnazione.</span><span class="sxs-lookup"><span data-stu-id="d759c-120">When assigning a user to ZenDesk, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="d759c-121">Poiché il ruolo **Accesso predefinito** non è applicabile per il provisioning, i relativi utenti vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="d759c-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="d759c-122">Per praticità, il servizio di provisioning legge tutti i ruoli personalizzati definiti in ZenDesk e li importa in Azure AD dove è possibile selezionarli nella finestra di dialogo Seleziona ruolo.</span><span class="sxs-lookup"><span data-stu-id="d759c-122">As an added feature, the provisioning service reads any custom roles defined in Zendesk, and imports them into Azure AD where they can be selected in the Select Role dialog.</span></span> <span data-ttu-id="d759c-123">Questi ruoli saranno visibili nel portale di Azure dopo l'abilitazione del servizio di provisioning e l'esecuzione di un ciclo di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="d759c-123">These roles will be visible in the Azure portal after the provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-to-zendesk"></a><span data-ttu-id="d759c-124">Configurazione del provisioning utenti in ZenDesk</span><span class="sxs-lookup"><span data-stu-id="d759c-124">Configuring user provisioning to ZenDesk</span></span> 

<span data-ttu-id="d759c-125">Questa sezione illustra la connessione di Azure AD all'API per il provisioning degli account utente di ZenDesk e la configurazione del servizio di provisioning per la creazione, l'aggiornamento e la disabilitazione degli account utente assegnati in ZenDesk in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d759c-125">This section guides you through connecting your Azure AD to ZenDesk's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in ZenDesk based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="d759c-126">Si può anche scegliere di abilitare l'accesso Single Sign-On basato su SAML per ZenDesk, seguendo le istruzioni disponibili nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d759c-126">You may also choose to enabled SAML-based Single Sign-On for ZenDesk, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d759c-127">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="d759c-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-zendesk-in-azure-ad"></a><span data-ttu-id="d759c-128">Configurare il provisioning automatico degli account utente in ZenDesk in Azure AD</span><span class="sxs-lookup"><span data-stu-id="d759c-128">Configure automatic user account provisioning to ZenDesk in Azure AD</span></span>


1. <span data-ttu-id="d759c-129">Nel [portale di Azure](https://portal.azure.com) passare alla sezione **Azure Active Directory > App aziendali > Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d759c-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="d759c-130">Se ZenDesk è già stato configurato per l'accesso Single Sign-On, cercare l'istanza di ZenDesk usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="d759c-130">If you have already configured ZenDesk for single sign-on, search for your instance of ZenDesk using the search field.</span></span> <span data-ttu-id="d759c-131">In caso contrario, selezionare **Aggiungi** e cercare **ZenDesk** nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d759c-131">Otherwise, select **Add** and search for **ZenDesk** in the application gallery.</span></span> <span data-ttu-id="d759c-132">Selezionare ZenDesk nei risultati della ricerca e aggiungerlo all'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d759c-132">Select ZenDesk from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="d759c-133">Selezionare l'istanza di ZenDesk e quindi la scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="d759c-133">Select your instance of ZenDesk, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="d759c-134">Impostare **Modalità di provisioning** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="d759c-134">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Provisioning di ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. <span data-ttu-id="d759c-136">Nella sezione **Credenziali amministratore** immettere il **nome utente amministratore, la chiave del token e il dominio** generati dall'account ZenDesk. È possibile trovare il token nell'account: **Amministrazione** > **API** > **Impostazioni**).</span><span class="sxs-lookup"><span data-stu-id="d759c-136">Under the **Admin Credentials** section, input the **Admin Username&tokenkey&Domain** generated by your ZenDesk's account (you can find the token under your account: **Admin** > **API** > **Settings**).</span></span> 

    ![Provisioning di ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. <span data-ttu-id="d759c-138">Nel portale di Azure fare clic su **Test connessione** per verificare che Azure AD possa connettersi all'app ZenDesk.</span><span class="sxs-lookup"><span data-stu-id="d759c-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your ZenDesk app.</span></span> <span data-ttu-id="d759c-139">Se la connessione non riesce, verificare che l'account ZenDesk abbia autorizzazioni di amministratore e ripetere il passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="d759c-139">If the connection fails, ensure your ZenDesk account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="d759c-140">Immettere l'indirizzo di posta elettronica di una persona o un gruppo che riceverà le notifiche di errore relative al provisioning nel campo **Messaggio di posta elettronica di notifica** e selezionare la casella di controllo "Invia una notifica di posta elettronica in caso di errore".</span><span class="sxs-lookup"><span data-stu-id="d759c-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="d759c-141">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d759c-141">Click **Save**.</span></span> 

9. <span data-ttu-id="d759c-142">Nella sezione Mapping selezionare **Synchronize Azure Active Directory Users to ZenDesk** (Sincronizza utenti di Azure Active Directory in ZenDesk).</span><span class="sxs-lookup"><span data-stu-id="d759c-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to ZenDesk**.</span></span>

10. <span data-ttu-id="d759c-143">Nella sezione **Mapping degli attributi** esaminare gli attributi utente che vengono sincronizzati da Azure AD a ZenDesk.</span><span class="sxs-lookup"><span data-stu-id="d759c-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to ZenDesk.</span></span> <span data-ttu-id="d759c-144">Gli attributi selezionati come proprietà **corrispondenti** vengono usati per trovare le corrispondenze con gli account utente in ZenDesk per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="d759c-144">The attributes selected as **Matching** properties are used to match the user accounts in ZenDesk for update operations.</span></span> <span data-ttu-id="d759c-145">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="d759c-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="d759c-146">Per abilitare il servizio di provisioning di Azure AD per ZenDesk, impostare **Stato del provisioning** su **Sì** nella sezione **Impostazioni**</span><span class="sxs-lookup"><span data-stu-id="d759c-146">To enable the Azure AD provisioning service for ZenDesk, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="d759c-147">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d759c-147">Click **Save**.</span></span> 

<span data-ttu-id="d759c-148">L'operazione avvia la sincronizzazione iniziale di tutti gli utenti e/o i gruppi assegnati a ZenDesk nella sezione Utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="d759c-148">This operation starts the initial synchronization of any users and/or groups assigned to ZenDesk in the Users and Groups section.</span></span> <span data-ttu-id="d759c-149">La sincronizzazione iniziale richiede più tempo delle sincronizzazioni successive, che saranno eseguite circa ogni 20 minuti per tutto il tempo che il servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d759c-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="d759c-150">È possibile usare la sezione **Dettagli sincronizzazione** per monitorare lo stato di avanzamento e selezionare i collegamenti ai report delle attività di provisioning che descrivono tutte le azioni eseguite dal servizio di provisioning.</span><span class="sxs-lookup"><span data-stu-id="d759c-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="d759c-151">Per altre informazioni sulla lettura dei log di provisioning di Azure AD, vedere [Esercitazione: creazione di report sul provisioning automatico degli account utente](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="d759c-151">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d759c-152">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d759c-152">Additional resources</span></span>

* [<span data-ttu-id="d759c-153">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="d759c-153">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="d759c-154">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d759c-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="d759c-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d759c-155">Next steps</span></span>

* [<span data-ttu-id="d759c-156">Informazioni su come esaminare i log e ottenere report sulle attività di provisioning</span><span class="sxs-lookup"><span data-stu-id="d759c-156">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
