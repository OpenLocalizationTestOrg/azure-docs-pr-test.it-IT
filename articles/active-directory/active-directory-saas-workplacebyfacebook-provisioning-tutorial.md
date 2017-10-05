---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook | Microsoft Docs'
description: Informazioni su come configurare l'accesso Single Sign-On tra Azure Active Directory e Workplace by Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 9b22679c304248ed7ba7a6bd9eaf82b64f7143cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="bcefc-103">Esercitazione: Configurazione di Workplace by Facebook per il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="bcefc-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="bcefc-104">L'obiettivo di questa esercitazione è descrivere le procedure da eseguire in Workplace by Facebook e Azure AD per eseguire automaticamente il provisioning e il deprovisioning degli account utente da Azure AD a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bcefc-104">The objective of this tutorial is to show you the steps you need to perform in Workplace by Facebook and Azure AD to automatically provision and de-provision user accounts from Azure AD to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bcefc-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bcefc-105">Prerequisites</span></span>

<span data-ttu-id="bcefc-106">Per configurare l'integrazione di Azure AD con Workplace by Facebook, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bcefc-106">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="bcefc-107">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bcefc-107">An Azure AD subscription</span></span>
- <span data-ttu-id="bcefc-108">Una sottoscrizione di Workplace by Facebook abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bcefc-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bcefc-109">Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="bcefc-109">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bcefc-110">A questo scopo, è consigliabile seguire le indicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="bcefc-110">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bcefc-111">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="bcefc-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bcefc-112">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bcefc-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="bcefc-113">Assegnazione di utenti a Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="bcefc-113">Assigning users to Workplace by Facebook</span></span>

<span data-ttu-id="bcefc-114">Per determinare gli utenti che dovranno ricevere l'accesso alle app selezionate, Azure Active Directory usa il concetto delle "assegnazioni".</span><span class="sxs-lookup"><span data-stu-id="bcefc-114">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="bcefc-115">Nel contesto del provisioning automatico degli account utente, vengono sincronizzati solo gli utenti e i gruppi che sono stati "assegnati" a un'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bcefc-115">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="bcefc-116">Prima di configurare e abilitare il servizio di provisioning, è necessario stabilire quali utenti e/o gruppi in Azure AD rappresentano gli utenti che devono accedere all'app Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bcefc-116">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="bcefc-117">Dopo aver stabilito questo, è possibile assegnare tali utenti all'app Workplace by Facebook seguendo le istruzioni riportate nell'articolo seguente:</span><span class="sxs-lookup"><span data-stu-id="bcefc-117">Once decided, you can assign these users to your Workplace by Facebook app by following the instructions here:</span></span>

[<span data-ttu-id="bcefc-118">Assegnare un utente o gruppo a un'app aziendale</span><span class="sxs-lookup"><span data-stu-id="bcefc-118">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="bcefc-119">Suggerimenti importanti per l'assegnazione di utenti a Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="bcefc-119">Important tips for assigning users to Workplace by Facebook</span></span>

*   <span data-ttu-id="bcefc-120">È consigliabile assegnare un singolo utente di Azure AD a Workplace by Facebook per testare la configurazione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="bcefc-120">It is recommended that a single Azure AD user is assigned to Workplace by Facebook to test the provisioning configuration.</span></span> <span data-ttu-id="bcefc-121">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="bcefc-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="bcefc-122">Quando si assegna un utente a Workplace by Facebook, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="bcefc-122">When assigning a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="bcefc-123">Il ruolo "Default Access" (Accesso predefinito) non è applicabile per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="bcefc-123">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="bcefc-124">Abilitare il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="bcefc-124">Enable User Provisioning</span></span>

<span data-ttu-id="bcefc-125">Questa sezione illustra la connessione di Azure AD all'API per il provisioning degli account utente di Workplace by Facebook e la configurazione del servizio di provisioning per la creazione, l'aggiornamento e la disabilitazione degli account utente assegnati in Workplace by Facebook in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bcefc-125">This section guides you through connecting your Azure AD to Workplace by Facebook's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="bcefc-126">Si può anche scegliere di abilitare l'accesso Single Sign-On basato su SAML per Workplace by Facebook, seguendo le istruzioni disponibili nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bcefc-126">You may also choose to enabled SAML-based Single Sign-On for Workplace by Facebook, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bcefc-127">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="bcefc-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="bcefc-128">Per configurare l'account utente eseguendo il provisioning a Workplace by Facebook in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="bcefc-128">To configure user account provisioning to Workplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="bcefc-129">L'obiettivo di questa sezione è descrivere le modalità di abilitazione del provisioning utente per gli account utente di Active Directory in Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bcefc-129">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Workplace by Facebook.</span></span>

<span data-ttu-id="bcefc-130">Azure AD consente di sincronizzare automaticamente i dettagli dell'account degli utenti assegnati a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bcefc-130">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="bcefc-131">La sincronizzazione automatica consente a Workplace by Facebook di ottenere i dati necessari per autorizzare gli utenti ad accedere, prima che questi tentino di eseguire l'accesso per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="bcefc-131">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="bcefc-132">Esegue anche il deprovisioning degli utenti da Workplace by Facebook una volta che l'accesso viene revocato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bcefc-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="bcefc-133">Nel [portale di Azure](https://portal.azure.com) passare alla sezione **Azure Active Directory** > **App aziendali** > **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bcefc-133">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="bcefc-134">Se si è già configurato Workplace by Facebook per l'accesso Single Sign-On, cercare l'istanza di Workplace by Facebook usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="bcefc-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using the search field.</span></span> <span data-ttu-id="bcefc-135">In caso contrario, selezionare **Aggiungi** e cercare **Workplace by Facebook** nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="bcefc-135">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="bcefc-136">Selezionare Workplace by Facebook nei risultati della ricerca e aggiungerlo all'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="bcefc-136">Select Workplace by Facebook from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="bcefc-137">Selezionare l'istanza di Workplace by Facebook e quindi la scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="bcefc-137">Select your instance of Workplace by Facebook, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="bcefc-138">Impostare **Modalità di provisioning** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="bcefc-138">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![provisioning](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="bcefc-140">Nella sezione **Credenziali amministratore** inserire il token segreto e l'URL del tenant dell'amministratore di Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bcefc-140">Under the **Admin Credentials** section, enter the Secret Token and the Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="bcefc-141">Nel portale di Azure fare clic su **Connessione di test** per verificare che Azure AD possa connettersi all'app Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bcefc-141">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="bcefc-142">Se la connessione non riesce, verificare che l'account Workplace by Facebook abbia le autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="bcefc-142">If the connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="bcefc-143">Immettere l'indirizzo e-mail di una persona o un gruppo che riceverà le notifiche di errore relative al provisioning nel campo **Messaggio di posta elettronica di notifica** e selezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="bcefc-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="bcefc-144">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="bcefc-144">Click **Save.**</span></span>

9. <span data-ttu-id="bcefc-145">Nella sezione Mapping selezionare **Synchronize Azure Active Directory Users to Workplace by Facebook** (Sincronizza utenti di Azure Active Directory in Workplace by Facebook).</span><span class="sxs-lookup"><span data-stu-id="bcefc-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook.**</span></span>

10. <span data-ttu-id="bcefc-146">Nella sezione **Mapping degli attributi** esaminare gli attributi utente che vengono sincronizzati da Azure AD a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bcefc-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="bcefc-147">Gli attributi selezionati come proprietà **Corrispondenti** vengono usati per trovare le corrispondenze con gli account utente in Workplace by Facebook per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="bcefc-147">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="bcefc-148">Selezionare il pulsante Salva per eseguire il commit delle modifiche.</span><span class="sxs-lookup"><span data-stu-id="bcefc-148">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="bcefc-149">Per abilitare il servizio di provisioning di Azure AD per Workplace by Facebook, impostare **Stato del provisioning** su **Sì** nella sezione **Impostazioni**</span><span class="sxs-lookup"><span data-stu-id="bcefc-149">To enable the Azure AD provisioning service for Workplace by Facebook, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="bcefc-150">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="bcefc-150">Click **Save.**</span></span>

<span data-ttu-id="bcefc-151">Per altre informazioni su come configurare il provisioning automatico, vedere [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="bcefc-151">For more information on how to configure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="bcefc-152">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="bcefc-152">You can now create a test account.</span></span> <span data-ttu-id="bcefc-153">Attendere 20 minuti per verificare che l'account sia stato sincronizzato con Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bcefc-153">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bcefc-154">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="bcefc-154">Additional resources</span></span>

* [<span data-ttu-id="bcefc-155">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="bcefc-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bcefc-156">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bcefc-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="bcefc-157">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bcefc-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

