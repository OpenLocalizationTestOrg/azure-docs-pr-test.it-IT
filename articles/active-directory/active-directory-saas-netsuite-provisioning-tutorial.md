---
title: 'Esercitazione: Integrazione di Azure Active Directory con NetSuite | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Netsuite.
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
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="82958-103">Esercitazione: Configurazione di Netsuite per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="82958-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="82958-104">obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in Netsuite e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="82958-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Netsuite and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooNetsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82958-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="82958-105">Prerequisites</span></span>

<span data-ttu-id="82958-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="82958-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="82958-107">Tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="82958-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="82958-108">Sottoscrizione di Netsuite abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="82958-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="82958-109">Account utente in Netsuite con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="82958-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-toonetsuite"></a><span data-ttu-id="82958-110">L'assegnazione di utenti tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="82958-110">Assigning users tooNetsuite</span></span>

<span data-ttu-id="82958-111">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="82958-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="82958-112">Nel contesto di hello di provisioning dell'account utente automatico, vengono sincronizzati solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82958-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="82958-113">Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour Netsuite app.</span><span class="sxs-lookup"><span data-stu-id="82958-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Netsuite app.</span></span> <span data-ttu-id="82958-114">Una volta deciso, è possibile assegnare queste app di Netsuite tooyour utenti seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="82958-114">Once decided, you can assign these users tooyour Netsuite app by following hello instructions here:</span></span>

[<span data-ttu-id="82958-115">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="82958-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a><span data-ttu-id="82958-116">Suggerimenti importanti per l'assegnazione di utenti tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="82958-116">Important tips for assigning users tooNetsuite</span></span>

*   <span data-ttu-id="82958-117">È consigliabile che un singolo utente AD Azure viene assegnato hello tootest tooNetsuite configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="82958-117">It is recommended that a single Azure AD user is assigned tooNetsuite tootest hello provisioning configuration.</span></span> <span data-ttu-id="82958-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="82958-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="82958-119">Quando si assegna un tooNetsuite utente, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="82958-119">When assigning a user tooNetsuite, you must select a valid user role.</span></span> <span data-ttu-id="82958-120">ruolo di "accesso predefinita" Hello non funziona per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="82958-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="82958-121">Abilitare il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="82958-121">Enable User Provisioning</span></span>

<span data-ttu-id="82958-122">Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooNetsuite il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in Netsuite in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82958-122">This section guides you through connecting your Azure AD tooNetsuite's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="82958-123">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Netsuite, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="82958-123">You may also choose tooenabled SAML-based Single Sign-On for Netsuite, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="82958-124">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="82958-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="82958-125">tooconfigure provisioning dell'account utente:</span><span class="sxs-lookup"><span data-stu-id="82958-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="82958-126">obiettivo di Hello di questa sezione è toooutline tooenable provisioning utente dell'utente di Active Directory come account di tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="82958-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooNetsuite.</span></span>

1. <span data-ttu-id="82958-127">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="82958-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="82958-128">Se è già stato configurato Netsuite per single sign-on, eseguire la ricerca per l'istanza di tramite il campo di ricerca hello Netsuite.</span><span class="sxs-lookup"><span data-stu-id="82958-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using hello search field.</span></span> <span data-ttu-id="82958-129">In caso contrario, selezionare **Aggiungi** e cercare **Netsuite** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="82958-129">Otherwise, select **Add** and search for **Netsuite** in hello application gallery.</span></span> <span data-ttu-id="82958-130">Selezionare Netsuite dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="82958-130">Select Netsuite from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="82958-131">Selezionare l'istanza di Netsuite, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="82958-131">Select your instance of Netsuite, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="82958-132">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="82958-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![provisioning](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="82958-134">In hello **credenziali di amministratore** sezione, fornire hello le impostazioni di configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="82958-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="82958-135">a.</span><span class="sxs-lookup"><span data-stu-id="82958-135">a.</span></span> <span data-ttu-id="82958-136">In hello **nome utente amministratore** casella di testo, digitare un Netsuite nome account cui ha hello **amministratore di sistema** profilo in Netsuite.com assegnato.</span><span class="sxs-lookup"><span data-stu-id="82958-136">In hello **Admin User Name** textbox, type a Netsuite account name that has hello **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="82958-137">b.</span><span class="sxs-lookup"><span data-stu-id="82958-137">b.</span></span> <span data-ttu-id="82958-138">In hello **Password amministratore** casella di testo, digitare la password hello per questo account.</span><span class="sxs-lookup"><span data-stu-id="82958-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>
      
6. <span data-ttu-id="82958-139">Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour Netsuite app.</span><span class="sxs-lookup"><span data-stu-id="82958-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Netsuite app.</span></span>

7. <span data-ttu-id="82958-140">In hello **notifica tramite posta elettronica** immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning e casella di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="82958-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="82958-141">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="82958-141">Click **Save.**</span></span>

9. <span data-ttu-id="82958-142">Nella sezione mapping hello, selezionare **tooNetsuite sincronizzare Active Directory gli utenti di Azure.**</span><span class="sxs-lookup"><span data-stu-id="82958-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooNetsuite.**</span></span>

10. <span data-ttu-id="82958-143">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooNetsuite di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82958-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooNetsuite.</span></span> <span data-ttu-id="82958-144">Si noti che gli attributi selezionati come hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in Netsuite per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="82958-144">Note that hello attributes selected as **Matching** properties are used toomatch hello user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="82958-145">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="82958-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="82958-146">tooenable hello servizio provisioning di Azure AD per Netsuite, hello modifica **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello</span><span class="sxs-lookup"><span data-stu-id="82958-146">tooenable hello Azure AD provisioning service for Netsuite, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="82958-147">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="82958-147">Click **Save.**</span></span>

<span data-ttu-id="82958-148">Avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooNetsuite in hello gli utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="82958-148">It starts hello initial synchronization of any users and/or groups assigned tooNetsuite in hello Users and Groups section.</span></span> <span data-ttu-id="82958-149">Si noti che la sincronizzazione iniziale hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="82958-149">Note that hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="82958-150">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite dal servizio nella tua app Netsuite hello.</span><span class="sxs-lookup"><span data-stu-id="82958-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="82958-151">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="82958-151">You can now create a test account.</span></span> <span data-ttu-id="82958-152">Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="82958-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooNetsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="82958-153">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="82958-153">Additional resources</span></span>

* [<span data-ttu-id="82958-154">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="82958-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="82958-155">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82958-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="82958-156">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="82958-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)