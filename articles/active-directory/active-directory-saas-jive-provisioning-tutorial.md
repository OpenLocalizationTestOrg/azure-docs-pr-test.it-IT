---
title: 'Esercitazione: Integrazione di Azure Active Directory con Jive | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Jive.
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
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="7e030-103">Esercitazione: Configurazione di Jive per il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="7e030-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="7e030-104">obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in Jive e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooJive.</span><span class="sxs-lookup"><span data-stu-id="7e030-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Jive and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooJive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e030-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7e030-105">Prerequisites</span></span>

<span data-ttu-id="7e030-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="7e030-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="7e030-107">Tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7e030-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="7e030-108">Una sottoscrizione di Jive abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="7e030-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="7e030-109">Un account utente in Jive con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="7e030-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-toojive"></a><span data-ttu-id="7e030-110">L'assegnazione di utenti tooJive</span><span class="sxs-lookup"><span data-stu-id="7e030-110">Assigning users tooJive</span></span>

<span data-ttu-id="7e030-111">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="7e030-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="7e030-112">Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="7e030-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="7e030-113">Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano utenti hello bisogno di accesso dell'applicazione Jive tooyour.</span><span class="sxs-lookup"><span data-stu-id="7e030-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Jive app.</span></span> <span data-ttu-id="7e030-114">Una volta deciso, è possibile assegnare queste app di Jive tooyour utenti seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="7e030-114">Once decided, you can assign these users tooyour Jive app by following hello instructions here:</span></span>

[<span data-ttu-id="7e030-115">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="7e030-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a><span data-ttu-id="7e030-116">Suggerimenti importanti per l'assegnazione di utenti tooJive</span><span class="sxs-lookup"><span data-stu-id="7e030-116">Important tips for assigning users tooJive</span></span>

*   <span data-ttu-id="7e030-117">È consigliabile che un singolo utente di Azure AD assegnare tooJive tootest hello configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="7e030-117">It is recommended that a single Azure AD user be assigned tooJive tootest hello provisioning configuration.</span></span> <span data-ttu-id="7e030-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="7e030-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="7e030-119">Quando si assegna un tooJive utente, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="7e030-119">When assigning a user tooJive, you must select a valid user role.</span></span> <span data-ttu-id="7e030-120">ruolo di "accesso predefinita" Hello non funziona per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="7e030-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="7e030-121">Abilitare il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="7e030-121">Enable User Provisioning</span></span>

<span data-ttu-id="7e030-122">Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooJive il Azure AD e configura provisioning servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in Jive in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e030-122">This section guides you through connecting your Azure AD tooJive's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="7e030-123">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Jive, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7e030-123">You may also choose tooenabled SAML-based Single Sign-On for Jive, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7e030-124">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="7e030-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="7e030-125">tooconfigure provisioning dell'account utente:</span><span class="sxs-lookup"><span data-stu-id="7e030-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="7e030-126">obiettivo di Hello di questa sezione è toooutline tooenable provisioning utente dell'utente di Active Directory come account di tooJive.</span><span class="sxs-lookup"><span data-stu-id="7e030-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooJive.</span></span>
<span data-ttu-id="7e030-127">Come parte di questa procedura, è necessario tooprovide un token di sicurezza utente è necessario toorequest a Jive.com.</span><span class="sxs-lookup"><span data-stu-id="7e030-127">As part of this procedure, you are required tooprovide a user security token you need toorequest from Jive.com.</span></span>

1. <span data-ttu-id="7e030-128">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="7e030-128">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="7e030-129">Se è già stato configurato Jive per single sign-on, eseguire la ricerca per l'istanza di tramite il campo di ricerca hello Jive.</span><span class="sxs-lookup"><span data-stu-id="7e030-129">If you have already configured Jive for single sign-on, search for your instance of Jive using hello search field.</span></span> <span data-ttu-id="7e030-130">In caso contrario, selezionare **Aggiungi** e cercare **Jive** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7e030-130">Otherwise, select **Add** and search for **Jive** in hello application gallery.</span></span> <span data-ttu-id="7e030-131">Selezionare Jive dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7e030-131">Select Jive from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="7e030-132">Selezionare l'istanza di Jive, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="7e030-132">Select your instance of Jive, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="7e030-133">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="7e030-133">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![provisioning](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="7e030-135">In hello **credenziali di amministratore** sezione, fornire hello le impostazioni di configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="7e030-135">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="7e030-136">a.</span><span class="sxs-lookup"><span data-stu-id="7e030-136">a.</span></span> <span data-ttu-id="7e030-137">In hello **nome utente amministratore Jive** casella di testo, digitare un Jive nome account cui ha hello **amministratore di sistema** profilo assegnato in Jive.com.</span><span class="sxs-lookup"><span data-stu-id="7e030-137">In hello **Jive Admin User Name** textbox, type a Jive account name that has hello **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="7e030-138">b.</span><span class="sxs-lookup"><span data-stu-id="7e030-138">b.</span></span> <span data-ttu-id="7e030-139">In hello **Password amministratore Jive** casella di testo, digitare la password hello per questo account.</span><span class="sxs-lookup"><span data-stu-id="7e030-139">In hello **Jive Admin Password** textbox, type hello password for this account.</span></span>
   
    <span data-ttu-id="7e030-140">c.</span><span class="sxs-lookup"><span data-stu-id="7e030-140">c.</span></span> <span data-ttu-id="7e030-141">In hello **URL Tenant Jive** casella di testo, digitare l'URL tenant Jive hello.</span><span class="sxs-lookup"><span data-stu-id="7e030-141">In hello **Jive Tenant URL** textbox, type hello Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="7e030-142">URL tenant Jive di Hello è utilizzato da toolog l'organizzazione in tooJive.</span><span class="sxs-lookup"><span data-stu-id="7e030-142">hello Jive tenant URL is URL that is used by your organization toolog in tooJive.</span></span>  
      > <span data-ttu-id="7e030-143">URL di hello include in genere hello seguente formato: **www.\< organizzazione\>. jive.com**.</span><span class="sxs-lookup"><span data-stu-id="7e030-143">Typically, hello URL has hello following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="7e030-144">Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour Jive app.</span><span class="sxs-lookup"><span data-stu-id="7e030-144">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Jive app.</span></span>

7. <span data-ttu-id="7e030-145">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7e030-145">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

8. <span data-ttu-id="7e030-146">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="7e030-146">Click **Save.**</span></span>

9. <span data-ttu-id="7e030-147">Nella sezione mapping hello, selezionare **tooJive sincronizzare Active Directory gli utenti di Azure.**</span><span class="sxs-lookup"><span data-stu-id="7e030-147">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooJive.**</span></span>

10. <span data-ttu-id="7e030-148">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooJive di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e030-148">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooJive.</span></span> <span data-ttu-id="7e030-149">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in Jive per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="7e030-149">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Jive for update operations.</span></span> <span data-ttu-id="7e030-150">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="7e030-150">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="7e030-151">tooenable hello servizio provisioning di Azure AD per Jive, hello modifica **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello</span><span class="sxs-lookup"><span data-stu-id="7e030-151">tooenable hello Azure AD provisioning service for Jive, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="7e030-152">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="7e030-152">Click **Save.**</span></span>

<span data-ttu-id="7e030-153">Avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooJive in hello gli utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="7e030-153">It starts hello initial synchronization of any users and/or groups assigned tooJive in hello Users and Groups section.</span></span> <span data-ttu-id="7e030-154">la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7e030-154">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="7e030-155">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio nella tua app Jive.</span><span class="sxs-lookup"><span data-stu-id="7e030-155">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Jive app.</span></span>

<span data-ttu-id="7e030-156">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="7e030-156">You can now create a test account.</span></span> <span data-ttu-id="7e030-157">Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooJive.</span><span class="sxs-lookup"><span data-stu-id="7e030-157">Wait for up too20 minutes tooverify that hello account has been synchronized tooJive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7e030-158">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7e030-158">Additional resources</span></span>

* [<span data-ttu-id="7e030-159">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="7e030-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e030-160">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e030-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="7e030-161">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7e030-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)