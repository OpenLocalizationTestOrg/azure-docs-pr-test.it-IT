---
title: 'Esercitazione: Configurare Workplace by Facebook per il provisioning degli utenti | Microsoft Docs'
description: Informazioni su come eseguire automaticamente il provisioning e il deprovisioning degli account utente da Azure AD a Workplace by Facebook.
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: a347eedbf5511dc83e1bc7721667441cfb87cb59
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="05d6a-103">Esercitazione: Configurare Workplace by Facebook per il provisioning degli utenti</span><span class="sxs-lookup"><span data-stu-id="05d6a-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="05d6a-104">Questa esercitazione illustra i passaggi necessari per effettuare automaticamente il provisioning e il deprovisioning degli account utente da Azure Active Directory (Azure AD) a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="05d6a-104">This tutorial shows you the steps necessary to automatically provision and de-provision user accounts from Azure Active Directory (Azure AD) to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05d6a-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="05d6a-105">Prerequisites</span></span>

<span data-ttu-id="05d6a-106">Per configurare l'integrazione di Azure AD con Workplace by Facebook, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="05d6a-106">To configure Azure AD integration with Workplace by Facebook, you need the following:</span></span>

- <span data-ttu-id="05d6a-107">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05d6a-107">An Azure AD subscription</span></span>
- <span data-ttu-id="05d6a-108">Una sottoscrizione a Workplace by Facebook abilitata per l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="05d6a-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="05d6a-109">A questo scopo, seguire queste indicazioni:</span><span class="sxs-lookup"><span data-stu-id="05d6a-109">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="05d6a-110">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="05d6a-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="05d6a-111">Se non si dispone di un ambiente di valutazione di Azure AD, è possibile ricevere un'[offerta di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05d6a-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-to-workplace-by-facebook"></a><span data-ttu-id="05d6a-112">Assegnare utenti a Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="05d6a-112">Assign users to Workplace by Facebook</span></span>

<span data-ttu-id="05d6a-113">Per determinare gli utenti che dovranno ricevere l'accesso alle app selezionate, Azure AD usa un concetto detto "assegnazioni".</span><span class="sxs-lookup"><span data-stu-id="05d6a-113">Azure AD uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="05d6a-114">Nel contesto del provisioning automatico degli account utente, vengono sincronizzati solo gli utenti e i gruppi che sono stati assegnati a un'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05d6a-114">In the context of automatic user account provisioning, only the users and groups that have been assigned to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="05d6a-115">Prima di configurare e abilitare il servizio di provisioning, stabilire quali utenti e gruppi in Azure AD rappresentano gli utenti che devono accedere all'app Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="05d6a-115">Before configuring and enabling the provisioning service, decide what users and groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="05d6a-116">Poi è possibile assegnare questi utenti all'app Workplace by Facebook seguendo le istruzioni riportate in [Assegnare un utente o un gruppo a un'app aziendale](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="05d6a-116">You can then assign these users to your Workplace by Facebook app by following the instructions in [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="05d6a-117">Testare la configurazione del provisioning tramite l'assegnazione di un singolo utente di Azure AD a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="05d6a-117">Test the provisioning configuration by assigning a single Azure AD user to Workplace by Facebook.</span></span> <span data-ttu-id="05d6a-118">Assegnare utenti e gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="05d6a-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="05d6a-119">Quando si assegna un utente a Workplace by Facebook, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="05d6a-119">When you assign a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="05d6a-120">Il ruolo di accesso predefinito non funziona per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="05d6a-120">The Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="05d6a-121">Abilitare il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="05d6a-121">Enable automated user provisioning</span></span>

<span data-ttu-id="05d6a-122">Questa sezione descrive la connessione di Azure AD all'API di provisioning dell'account utente di Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="05d6a-122">This section guides you through connecting your Azure AD to the user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="05d6a-123">Inoltre fornisce informazioni su come configurare il servizio di provisioning per creare, aggiornare e disabilitare gli account utente assegnati in Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="05d6a-123">You also learn how to configure the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="05d6a-124">Questo è basato sull'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05d6a-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="05d6a-125">È possibile anche scegliere di abilitare l'accesso SSO basato su SAML per Workplace by Facebook seguendo le istruzioni disponibili nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05d6a-125">You can also choose to enabled SAML-based SSO for Workplace by Facebook, by following the instructions provided in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="05d6a-126">L'accesso SSO può essere configurato indipendentemente dal provisioning automatico, anche se queste due funzionalità sono complementari.</span><span class="sxs-lookup"><span data-stu-id="05d6a-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="05d6a-127">Configurare l'account utente eseguendo il provisioning a Workplace by Facebook in Azure AD</span><span class="sxs-lookup"><span data-stu-id="05d6a-127">Configure user account provisioning to Workplace by Facebook in Azure AD</span></span>

<span data-ttu-id="05d6a-128">Azure AD consente di sincronizzare automaticamente i dettagli dell'account degli utenti assegnati a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="05d6a-128">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="05d6a-129">La sincronizzazione automatica consente a Workplace by Facebook di ottenere i dati necessari per autorizzare gli utenti ad accedere, prima che questi tentino di eseguire l'accesso per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="05d6a-129">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="05d6a-130">Esegue anche il deprovisioning degli utenti da Workplace by Facebook una volta che l'accesso viene revocato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05d6a-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="05d6a-131">Nel [portale di Azure](https://portal.azure.com) selezionare **Azure Active Directory** > **Enterprise Apps** (App aziendali)  > **Tutte le applicazioni** (Tutte le app).</span><span class="sxs-lookup"><span data-stu-id="05d6a-131">In the [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="05d6a-132">Se si è già configurato Workplace by Facebook per l'accesso SSO, cercare l'istanza di Workplace by Facebook usando il campo di ricerca.</span><span class="sxs-lookup"><span data-stu-id="05d6a-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using the search field.</span></span> <span data-ttu-id="05d6a-133">In caso contrario, selezionare **Aggiungi** e cercare **Workplace by Facebook** nella raccolta di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="05d6a-133">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="05d6a-134">Selezionare **Workplace by Facebook** nei risultati della ricerca e aggiungerlo all'elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="05d6a-134">Select **Workplace by Facebook** from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="05d6a-135">Selezionare l'istanza di Workplace by Facebook e quindi la scheda **Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="05d6a-135">Select your instance of Workplace by Facebook, and then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="05d6a-136">Impostare **Modalità di provisioning** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="05d6a-136">Set **Provisioning Mode** to **Automatic**.</span></span> 

    ![Screenshot delle opzioni di provisioning di Workplace by Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="05d6a-138">Nella sezione **Credenziali amministratore** inserire il **token segreto** e l'**URL tenant** dell'amministratore di Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="05d6a-138">Under the **Admin Credentials** section, enter the **Secret Token** and the **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="05d6a-139">Nel portale di Azure selezionare **Connessione di test** per verificare che Azure AD possa connettersi all'app Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="05d6a-139">In the Azure portal, select **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="05d6a-140">Se la connessione ha esito negativo, verificare che l'account Workplace by Facebook disponga delle autorizzazioni di amministratore del team.</span><span class="sxs-lookup"><span data-stu-id="05d6a-140">If the connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="05d6a-141">Immettere l'indirizzo di posta elettronica di una persona o un gruppo che dovrà ricevere le notifiche di errore relative al provisioning nel campo **Messaggio di posta elettronica di notifica** e selezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="05d6a-141">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the check box.</span></span>

8. <span data-ttu-id="05d6a-142">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="05d6a-142">Select **Save**.</span></span>

9. <span data-ttu-id="05d6a-143">Nella sezione Mapping selezionare **Synchronize Azure Active Directory Users to Workplace by Facebook** (Sincronizza utenti di Azure Active Directory in Workplace by Facebook).</span><span class="sxs-lookup"><span data-stu-id="05d6a-143">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook**.</span></span>

10. <span data-ttu-id="05d6a-144">Nella sezione **Mapping degli attributi** esaminare gli attributi utente che vengono sincronizzati da Azure AD a Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="05d6a-144">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="05d6a-145">Gli attributi selezionati come proprietà **Corrispondenti** vengono usati per trovare le corrispondenze con gli account utente in Workplace by Facebook per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="05d6a-145">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="05d6a-146">Per eseguire il commit di tutte le modifiche, selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="05d6a-146">To commit any changes, select **Save**.</span></span>

11. <span data-ttu-id="05d6a-147">Per abilitare il servizio di provisioning di Azure AD per Workplace by Facebook, nella sezione **Impostazioni** modificare lo **stato del provisioning** su **On**.</span><span class="sxs-lookup"><span data-stu-id="05d6a-147">To enable the Azure AD provisioning service for Workplace by Facebook, in the **Settings** section, change the **Provisioning Status** to **On**.</span></span>

12. <span data-ttu-id="05d6a-148">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="05d6a-148">Select **Save**.</span></span>

<span data-ttu-id="05d6a-149">Per altre informazioni su come configurare il provisioning automatico, vedere [la documentazione di Facebook](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="05d6a-149">For more information on how to configure automatic provisioning, see [the Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="05d6a-150">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="05d6a-150">You can now create a test account.</span></span> <span data-ttu-id="05d6a-151">Attendere 20 minuti per verificare che l'account sia stato sincronizzato con Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="05d6a-151">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="05d6a-152">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="05d6a-152">Additional resources</span></span>

* [<span data-ttu-id="05d6a-153">Gestione del provisioning degli account utente per le app aziendali</span><span class="sxs-lookup"><span data-stu-id="05d6a-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05d6a-154">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05d6a-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="05d6a-155">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="05d6a-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

