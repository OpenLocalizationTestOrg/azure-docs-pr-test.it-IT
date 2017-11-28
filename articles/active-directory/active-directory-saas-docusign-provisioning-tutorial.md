---
title: 'Esercitazione: Integrazione di Azure Active Directory con DocuSign | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e DocuSign.
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
ms.openlocfilehash: 8562a8f9e05fb72d3331507b7da5c6afee38f9b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a><span data-ttu-id="a8973-103">Esercitazione: Configurazione di DocuSign per il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="a8973-103">Tutorial: Configuring DocuSign for User Provisioning</span></span>

<span data-ttu-id="a8973-104">obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in DocuSign e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="a8973-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in DocuSign and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDocuSign.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8973-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a8973-105">Prerequisites</span></span>

<span data-ttu-id="a8973-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="a8973-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="a8973-107">Tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8973-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="a8973-108">Una sottoscrizione di DocuSign abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a8973-108">A DocuSign single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="a8973-109">Un account utente in DocuSign con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="a8973-109">A user account in DocuSign with Team Admin permissions.</span></span>

## <a name="assigning-users-toodocusign"></a><span data-ttu-id="a8973-110">L'assegnazione di utenti tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="a8973-110">Assigning users tooDocuSign</span></span>

<span data-ttu-id="a8973-111">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="a8973-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="a8973-112">Nel contesto di hello di provisioning dell'account utente automatico, vengono sincronizzati solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8973-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="a8973-113">Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour DocuSign app.</span><span class="sxs-lookup"><span data-stu-id="a8973-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour DocuSign app.</span></span> <span data-ttu-id="a8973-114">Una volta deciso, è possibile assegnare queste app di DocuSign tooyour utenti seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="a8973-114">Once decided, you can assign these users tooyour DocuSign app by following hello instructions here:</span></span>

[<span data-ttu-id="a8973-115">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="a8973-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodocusign"></a><span data-ttu-id="a8973-116">Suggerimenti importanti per l'assegnazione di utenti tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="a8973-116">Important tips for assigning users tooDocuSign</span></span>

*   <span data-ttu-id="a8973-117">È consigliabile che un singolo utente AD Azure viene assegnato hello tootest tooDocuSign configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="a8973-117">It is recommended that a single Azure AD user is assigned tooDocuSign tootest hello provisioning configuration.</span></span> <span data-ttu-id="a8973-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="a8973-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a8973-119">Quando si assegna un tooDocuSign utente, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="a8973-119">When assigning a user tooDocuSign, you must select a valid user role.</span></span> <span data-ttu-id="a8973-120">ruolo di "accesso predefinita" Hello non funziona per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="a8973-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="a8973-121">Abilitare il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="a8973-121">Enable User Provisioning</span></span>

<span data-ttu-id="a8973-122">Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooDocuSign il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in DocuSign in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8973-122">This section guides you through connecting your Azure AD tooDocuSign's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in DocuSign based on user and group assignment in Azure AD.</span></span>

> [!Tip]
> <span data-ttu-id="a8973-123">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per DocuSign, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a8973-123">You may also choose tooenabled SAML-based Single Sign-On for DocuSign, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a8973-124">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="a8973-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="a8973-125">tooconfigure provisioning dell'account utente:</span><span class="sxs-lookup"><span data-stu-id="a8973-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="a8973-126">obiettivo di Hello di questa sezione è toooutline tooenable provisioning utente dell'utente di Active Directory come account di tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="a8973-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooDocuSign.</span></span>

1. <span data-ttu-id="a8973-127">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="a8973-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="a8973-128">Se è già stato configurato DocuSign per single sign-on, eseguire la ricerca per l'istanza di DocuSign utilizzando il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="a8973-128">If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using hello search field.</span></span> <span data-ttu-id="a8973-129">In caso contrario, selezionare **Aggiungi** e cercare **DocuSign** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a8973-129">Otherwise, select **Add** and search for **DocuSign** in hello application gallery.</span></span> <span data-ttu-id="a8973-130">Selezionare DocuSign dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a8973-130">Select DocuSign from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="a8973-131">Selezionare l'istanza di DocuSign, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="a8973-131">Select your instance of DocuSign, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="a8973-132">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="a8973-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![provisioning](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="a8973-134">In hello **credenziali di amministratore** sezione, fornire hello le impostazioni di configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="a8973-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="a8973-135">a.</span><span class="sxs-lookup"><span data-stu-id="a8973-135">a.</span></span> <span data-ttu-id="a8973-136">In hello **nome utente amministratore** digitare un nome che è hello account DocuSign **amministratore di sistema** profilo in DocuSign.com assegnato.</span><span class="sxs-lookup"><span data-stu-id="a8973-136">In hello **Admin User Name** textbox, type a DocuSign account name that has hello **System Administrator** profile in DocuSign.com assigned.</span></span>
   
    <span data-ttu-id="a8973-137">b.</span><span class="sxs-lookup"><span data-stu-id="a8973-137">b.</span></span> <span data-ttu-id="a8973-138">In hello **Password amministratore** casella di testo, digitare la password hello per questo account.</span><span class="sxs-lookup"><span data-stu-id="a8973-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>

6. <span data-ttu-id="a8973-139">Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour DocuSign app.</span><span class="sxs-lookup"><span data-stu-id="a8973-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour DocuSign app.</span></span>

7. <span data-ttu-id="a8973-140">In hello **notifica tramite posta elettronica** immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning e casella di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="a8973-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="a8973-141">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a8973-141">Click **Save.**</span></span>

9. <span data-ttu-id="a8973-142">Nella sezione mapping hello, selezionare **tooDocuSign sincronizzare Active Directory gli utenti di Azure.**</span><span class="sxs-lookup"><span data-stu-id="a8973-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDocuSign.**</span></span>

10. <span data-ttu-id="a8973-143">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooDocuSign di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8973-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDocuSign.</span></span> <span data-ttu-id="a8973-144">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in DocuSign per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="a8973-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in DocuSign for update operations.</span></span> <span data-ttu-id="a8973-145">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="a8973-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="a8973-146">tooenable hello servizio provisioning di Azure AD per DocuSign, hello modifica **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello</span><span class="sxs-lookup"><span data-stu-id="a8973-146">tooenable hello Azure AD provisioning service for DocuSign, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="a8973-147">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a8973-147">Click **Save.**</span></span>

<span data-ttu-id="a8973-148">Avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooDocuSign in hello gli utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="a8973-148">It starts hello initial synchronization of any users and/or groups assigned tooDocuSign in hello Users and Groups section.</span></span> <span data-ttu-id="a8973-149">la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a8973-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="a8973-150">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite dal servizio nella tua app DocuSign hello.</span><span class="sxs-lookup"><span data-stu-id="a8973-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your DocuSign app.</span></span>

<span data-ttu-id="a8973-151">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="a8973-151">You can now create a test account.</span></span> <span data-ttu-id="a8973-152">Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="a8973-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooDocuSign.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a8973-153">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a8973-153">Additional resources</span></span>

* [<span data-ttu-id="a8973-154">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="a8973-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a8973-155">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8973-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a8973-156">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a8973-156">Configure Single Sign-on</span></span>](active-directory-saas-docusign-tutorial.md)