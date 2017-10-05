---
title: 'Esercitazione: Configurazione di Cerner Central per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come configurare Azure Active Directory per effettuare automaticamente il provisioning degli utenti in un elenco in Cerner Central.
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: 84613b7f8d7bd031d492a62da0bc53be96ac45a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="68732-103">Esercitazione: Configurazione di Cerner Central per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="68732-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="68732-104">Questa esercitazione descrive le procedure da eseguire in Cerner Central e Azure AD per effettuare automaticamente il provisioning e il deprovisioning degli account utente da Azure AD in un elenco di utenti in Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="68732-104">The objective of this tutorial is to show you the steps you need to perform in Cerner Central and Azure AD to automatically provision and de-provision user accounts from Azure AD to a user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="68732-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="68732-105">Prerequisites</span></span>

<span data-ttu-id="68732-106">Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="68732-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="68732-107">Tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68732-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="68732-108">Tenant di Cerner Central</span><span class="sxs-lookup"><span data-stu-id="68732-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="68732-109">Azure Active Directory si integra con Cerner Central usando il protocollo [SCIM](http://www.simplecloud.info/).</span><span class="sxs-lookup"><span data-stu-id="68732-109">Azure Active Directory integrates with Cerner Central using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-cerner-central"></a><span data-ttu-id="68732-110">Assegnazione di utenti a Cerner Central</span><span class="sxs-lookup"><span data-stu-id="68732-110">Assigning users to Cerner Central</span></span>

<span data-ttu-id="68732-111">Per determinare gli utenti che dovranno ricevere l'accesso alle app selezionate, Azure Active Directory usa il concetto delle "assegnazioni".</span><span class="sxs-lookup"><span data-stu-id="68732-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="68732-112">Nel contesto del provisioning automatico degli account utente, vengono sincronizzati solo gli utenti e i gruppi che sono stati "assegnati" a un'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68732-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="68732-113">Prima di configurare e abilitare il servizio di provisioning, è necessario stabilire quali utenti e/o gruppi in Azure AD rappresentano gli utenti che devono accedere a Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="68732-113">Before configuring and enabling the provisioning service, you should decide what users and/or groups in Azure AD represent the users who need access to Cerner Central.</span></span> <span data-ttu-id="68732-114">Dopo aver stabilito questo, è possibile assegnare tali utenti a Cerner Central seguendo le istruzioni riportate nell'articolo seguente:</span><span class="sxs-lookup"><span data-stu-id="68732-114">Once decided, you can assign these users to Cerner Central by following the instructions here:</span></span>

[<span data-ttu-id="68732-115">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="68732-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-cerner-central"></a><span data-ttu-id="68732-116">Suggerimenti importanti per l'assegnazione di utenti a Cerner Central</span><span class="sxs-lookup"><span data-stu-id="68732-116">Important tips for assigning users to Cerner Central</span></span>

*   <span data-ttu-id="68732-117">È consigliabile assegnare un singolo utente di Azure AD a Cerner Central per testare la configurazione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="68732-117">It is recommended that a single Azure AD user be assigned to Cerner Central to test the provisioning configuration.</span></span> <span data-ttu-id="68732-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="68732-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="68732-119">Al termine del test iniziale per un singolo utente, Cerner Central consiglia di assegnare l'intero elenco di utenti che devono accedere a qualsiasi soluzione Cerner (non solo Cerner Central) per effettuarne il provisioning nell'elenco di utenti di Cerner.</span><span class="sxs-lookup"><span data-stu-id="68732-119">Once initial testing is complete for a single user, Cerner Central recommends assigning the entire list of users intended to access any Cerner solution (not just Cerner Central) to be provisioned to Cerner’s user roster.</span></span>  <span data-ttu-id="68732-120">Altre soluzioni Cerner sfruttano questo elenco di utenti.</span><span class="sxs-lookup"><span data-stu-id="68732-120">Other Cerner solutions leverage this list of users in the user roster.</span></span>

*   <span data-ttu-id="68732-121">Quando si assegna un utente a Cerner Central, è necessario selezionare il ruolo **Utente** nella finestra di dialogo di assegnazione.</span><span class="sxs-lookup"><span data-stu-id="68732-121">When assigning a user to Cerner Central, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="68732-122">Gli utenti con il ruolo "Accesso predefinito" vengono esclusi dal provisioning.</span><span class="sxs-lookup"><span data-stu-id="68732-122">Users with the "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-to-cerner-central"></a><span data-ttu-id="68732-123">Configurazione del provisioning utenti in Cerner Central</span><span class="sxs-lookup"><span data-stu-id="68732-123">Configuring user provisioning to Cerner Central</span></span>

<span data-ttu-id="68732-124">Questa sezione illustra la connessione di Azure AD all'elenco di utenti di Cerner Central tramite l'API per il provisioning degli account utente SCIM di Cerner e la configurazione del servizio di provisioning per la creazione, l'aggiornamento e la disabilitazione degli account utente assegnati in Cerner Central in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68732-124">This section guides you through connecting your Azure AD to Cerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="68732-125">Si può anche scegliere di abilitare l'accesso Single Sign-On basato su SAML per Cerner Central, seguendo le istruzioni disponibili nel [portale di Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="68732-125">You may also choose to enabled SAML-based Single Sign-On for Cerner Central, following the instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="68732-126">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="68732-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="68732-127">Per altre informazioni, vedere l'[esercitazione sull'accesso Single Sign-On di Cerner Central](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="68732-127">For more information, see the [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-cerner-central-in-azure-ad"></a><span data-ttu-id="68732-128">Per configurare il provisioning automatico degli account utente in Cerner Central con Azure AD:</span><span class="sxs-lookup"><span data-stu-id="68732-128">To configure automatic user account provisioning to Cerner Central in Azure AD:</span></span>


<span data-ttu-id="68732-129">Per effettuare il provisioning degli account utente in Cerner Central, è necessario richiedere un account di sistema di Cerner Central e generare un token di connessione OAuth che possa essere usato da Azure AD per la connessione all'endpoint SCIM di Cerner.</span><span class="sxs-lookup"><span data-stu-id="68732-129">In order to provision user accounts to Cerner Central, you’ll need to request a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use to connect to Cerner's SCIM endpoint.</span></span> <span data-ttu-id="68732-130">È consigliabile anche eseguire l'integrazione in un ambiente sandbox Cerner prima della distribuzione in produzione.</span><span class="sxs-lookup"><span data-stu-id="68732-130">It is also recommended that the integration be performed in a Cerner sandbox environment before deploying to production.</span></span>

1.  <span data-ttu-id="68732-131">Il primo passaggio consiste nel garantire che le persone che gestiscono l'integrazione di Cerner e Azure AD abbiano un account CernerCare, obbligatorio per accedere alla documentazione necessaria per completare le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="68732-131">The first step is to ensure the people managing the Cerner and Azure AD integration have a CernerCare account, which is required to access the documentation necessary to complete the instructions.</span></span> <span data-ttu-id="68732-132">Se necessario, usare gli URL riportati di seguito per creare account CernerCare in ogni ambiente applicabile.</span><span class="sxs-lookup"><span data-stu-id="68732-132">If necessary, use the URLs below to create CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="68732-133">Sandbox: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="68732-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="68732-134">Produzione: https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="68732-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="68732-135">È quindi necessario creare un account di sistema per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68732-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="68732-136">Usare le istruzioni di seguito per richiedere un account di sistema per gli ambienti sandbox e di produzione.</span><span class="sxs-lookup"><span data-stu-id="68732-136">Use the instructions below to request a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="68732-137">Istruzioni: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="68732-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="68732-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="68732-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="68732-139">Produzione: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="68732-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="68732-140">Generare quindi un token di connessione OAuth per ogni account di sistema.</span><span class="sxs-lookup"><span data-stu-id="68732-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="68732-141">A questo scopo, seguire queste istruzioni.</span><span class="sxs-lookup"><span data-stu-id="68732-141">To do this, follow the instructions below.</span></span>

   * <span data-ttu-id="68732-142">Istruzioni: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="68732-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="68732-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="68732-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="68732-144">Produzione: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="68732-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="68732-145">È infine necessario acquisire gli ID dell'area autenticazione dell'elenco utenti sia per l'ambiente sandbox che per quello di produzione in Cerner per completare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="68732-145">Finally, you need to acquire User Roster Realm IDs for both the sandbox and production environments in Cerner to complete the configuration.</span></span> <span data-ttu-id="68732-146">Per informazioni su come acquisire tale ID, vedere: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="68732-146">For information on how to acquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="68732-147">È ora possibile configurare Azure AD per il provisioning degli account utente in Cerner.</span><span class="sxs-lookup"><span data-stu-id="68732-147">Now you can configure Azure AD to provision user accounts to Cerner.</span></span> <span data-ttu-id="68732-148">Accedere al [portale di Azure](https://portal.azure.com) e passare alla sezione **Azure Active Directory > App aziendali > Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="68732-148">Sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="68732-149">Se si è già configurato Cerner Central per l'accesso Single Sign-On, cercare l'istanza di Cerner Central usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="68732-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using the search field.</span></span> <span data-ttu-id="68732-150">In caso contrario, selezionare **Aggiungi** e cercare **Cerner Central** nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="68732-150">Otherwise, select **Add** and search for **Cerner Central** in the application gallery.</span></span> <span data-ttu-id="68732-151">Selezionare Cerner Central nei risultati della ricerca e aggiungerlo all'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="68732-151">Select Cerner Central from the search results, and add it to your list of applications.</span></span>

7.  <span data-ttu-id="68732-152">Selezionare l'istanza di Cerner Central e quindi la scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="68732-152">Select your instance of Cerner Central, then select the **Provisioning** tab.</span></span>

8.  <span data-ttu-id="68732-153">Impostare **Modalità di provisioning** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="68732-153">Set the **Provisioning Mode** to **Automatic**.</span></span>

   ![Provisioning in Cerner Central](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="68732-155">Compilare i campi seguenti in **Credenziali amministratore**:</span><span class="sxs-lookup"><span data-stu-id="68732-155">Fill in the following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="68732-156">Nel campo **URL tenant** immettere un URL nel formato seguente, sostituendo "ID-Area-Autenticazione-Roster-Utenti" con l'ID area autenticazione acquisito nel passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="68732-156">In the **Tenant URL** field, enter a URL in the format below, replacing "User-Roster-Realm-ID" with the realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="68732-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="68732-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="68732-158">Produzione: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="68732-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="68732-159">Nel campo **Token segreto** immettere il token di connessione OAuth generato nel passaggio 3 e fare clic su **Test connessione**.</span><span class="sxs-lookup"><span data-stu-id="68732-159">In the **Secret Token** field, enter the OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="68732-160">Nel lato superiore destro del portale verrà visualizzata una notifica di esito positivo.</span><span class="sxs-lookup"><span data-stu-id="68732-160">You should see a success notification on the upper­right side of your portal.</span></span>

10. <span data-ttu-id="68732-161">Immettere l'indirizzo di posta elettronica di una persona o un gruppo che riceverà le notifiche di errore relative al provisioning nel campo **Messaggio di posta elettronica di notifica** e selezionare la casella di controllo seguente.</span><span class="sxs-lookup"><span data-stu-id="68732-161">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

11. <span data-ttu-id="68732-162">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="68732-162">Click **Save**.</span></span> 

12. <span data-ttu-id="68732-163">Nella sezione **Mapping attributi** esaminare gli attributi di utenti e gruppi che verranno sincronizzati da Azure AD a Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="68732-163">In the **Attribute Mappings** section, review the user and group attributes to be synchronized from Azure AD to Cerner Central.</span></span> <span data-ttu-id="68732-164">Gli attributi selezionati come proprietà **corrispondenti** verranno usati per trovare le corrispondenze con gli account utente e i gruppi in Cerner Central per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="68732-164">The attributes selected as **Matching** properties are used to match the user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="68732-165">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="68732-165">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="68732-166">Per abilitare il servizio di provisioning di Azure AD per Cerner Central, impostare **Stato del provisioning** su **Sì** nella sezione **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="68732-166">To enable the Azure AD provisioning service for Cerner Central, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

14. <span data-ttu-id="68732-167">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="68732-167">Click **Save**.</span></span> 

<span data-ttu-id="68732-168">Verrà avviata la sincronizzazione iniziale di tutti gli utenti e/o i gruppi assegnati a Cerner Central nella sezione Utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="68732-168">This starts the initial synchronization of any users and/or groups assigned to Cerner Central in the Users and Groups section.</span></span> <span data-ttu-id="68732-169">La sincronizzazione iniziale richiede più tempo delle sincronizzazioni successive, che saranno eseguite circa ogni 20 minuti quando il servizio di provisioning di Azure AD è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="68732-169">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="68732-170">È possibile usare la sezione **Dettagli sincronizzazione** per monitorare lo stato di avanzamento e selezionare i collegamenti ai report delle attività di provisioning, che descrivono tutte le azioni eseguite dal servizio di provisioning sull'app Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="68732-170">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="68732-171">Per altre informazioni sulla lettura dei log di provisioning di Azure AD, vedere l'esercitazione relativa alla [creazione di report sul provisioning automatico degli account utente](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="68732-171">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="68732-172">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="68732-172">Additional resources</span></span>

* [<span data-ttu-id="68732-173">Cerner Central: Publishing identity data using Azure AD (Cerner Central: Pubblicazione dei dati sull'identità con Azure AD)</span><span class="sxs-lookup"><span data-stu-id="68732-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="68732-174">Esercitazione sulla configurazione di Cerner Central per l'accesso Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68732-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="68732-175">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="68732-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="68732-176">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68732-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="68732-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="68732-177">Next steps</span></span>
* <span data-ttu-id="68732-178">[Informazioni su come esaminare i log e ottenere report sulle attività di provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="68732-178">[Learn how to review logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
