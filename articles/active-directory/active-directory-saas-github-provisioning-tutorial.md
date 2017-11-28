---
title: 'Esercitazione: Configurazione di GitHub per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come tooconfigure Azure Active Directory tooautomatically il provisioning e il de-provisioning account utente di tooGitHub.
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
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a><span data-ttu-id="be732-103">Esercitazione: Configurazione di GitHub per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="be732-103">Tutorial: Configuring GitHub for Automatic User Provisioning</span></span>


<span data-ttu-id="be732-104">obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in GitHub e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooGitHub.</span><span class="sxs-lookup"><span data-stu-id="be732-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in GitHub and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="be732-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="be732-105">Prerequisites</span></span>

<span data-ttu-id="be732-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="be732-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="be732-107">Tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be732-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="be732-108">Un tenant di Github con hello [piano aziendale](https://help.github.com/articles/organization-billing-plans/#business-plan) o meglio abilitato</span><span class="sxs-lookup"><span data-stu-id="be732-108">A Github tenant with hello [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="be732-109">Account utente in GitHub con autorizzazioni di amministratore</span><span class="sxs-lookup"><span data-stu-id="be732-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="be732-110">Hello provisioning integrazione di Azure AD si basa su hello [GitHub SCIM API](https://developer.github.com/v3/scim/), ovvero i team tooGithub disponibili nel piano aziendale hello o migliori.</span><span class="sxs-lookup"><span data-stu-id="be732-110">hello Azure AD provisioning integration relies on hello [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available tooGithub teams on hello Business plan or better.</span></span>

## <a name="assigning-users-toogithub"></a><span data-ttu-id="be732-111">L'assegnazione di utenti tooGitHub</span><span class="sxs-lookup"><span data-stu-id="be732-111">Assigning users tooGitHub</span></span>

<span data-ttu-id="be732-112">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="be732-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="be732-113">Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="be732-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="be732-114">Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour GitHub app.</span><span class="sxs-lookup"><span data-stu-id="be732-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour GitHub app.</span></span> <span data-ttu-id="be732-115">Una volta deciso, è possibile assegnare queste app di GitHub tooyour utenti seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="be732-115">Once decided, you can assign these users tooyour GitHub app by following hello instructions here:</span></span>

[<span data-ttu-id="be732-116">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="be732-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a><span data-ttu-id="be732-117">Suggerimenti importanti per l'assegnazione di utenti tooGitHub</span><span class="sxs-lookup"><span data-stu-id="be732-117">Important tips for assigning users tooGitHub</span></span>

*   <span data-ttu-id="be732-118">È consigliabile che un singolo utente AD Azure viene assegnato hello tootest tooGitHub configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="be732-118">It is recommended that a single Azure AD user is assigned tooGitHub tootest hello provisioning configuration.</span></span> <span data-ttu-id="be732-119">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="be732-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="be732-120">Quando si assegna un tooGitHub utente, è necessario selezionare entrambi hello **utente** ruolo, o un altro valido specifici dell'applicazione, se disponibile, nella finestra di dialogo assegnazione hello.</span><span class="sxs-lookup"><span data-stu-id="be732-120">When assigning a user tooGitHub, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="be732-121">Hello **accesso predefinito** ruolo non funziona per il provisioning e gli utenti vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="be732-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toogithub"></a><span data-ttu-id="be732-122">Configurazione tooGitHub di provisioning dell'utente</span><span class="sxs-lookup"><span data-stu-id="be732-122">Configuring user provisioning tooGitHub</span></span> 

<span data-ttu-id="be732-123">Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooGitHub il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in GitHub in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be732-123">This section guides you through connecting your Azure AD tooGitHub's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="be732-124">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per GitHub, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="be732-124">You may also choose tooenabled SAML-based Single Sign-On for GitHub, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="be732-125">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="be732-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a><span data-ttu-id="be732-126">Configurare l'account utente automatico provisioning tooGitHub in Azure AD</span><span class="sxs-lookup"><span data-stu-id="be732-126">Configure automatic user account provisioning tooGitHub in Azure AD</span></span>


1. <span data-ttu-id="be732-127">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="be732-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="be732-128">Se è già stato configurato GitHub per single sign-on, eseguire la ricerca per l'istanza di GitHub usando il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="be732-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using hello search field.</span></span> <span data-ttu-id="be732-129">In caso contrario, selezionare **Aggiungi** e cercare **GitHub** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="be732-129">Otherwise, select **Add** and search for **GitHub** in hello application gallery.</span></span> <span data-ttu-id="be732-130">Selezionare GitHub dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="be732-130">Select GitHub from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="be732-131">Selezionare l'istanza di GitHub, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="be732-131">Select your instance of GitHub, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="be732-132">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="be732-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Provisioning di GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="be732-134">In hello **credenziali di amministratore** fare clic su **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="be732-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="be732-135">Viene aperta una finestra di dialogo di autorizzazione di GitHub in una nuova finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="be732-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="be732-136">In nuova finestra hello, accedere a GitHub utilizzando l'account amministratore.</span><span class="sxs-lookup"><span data-stu-id="be732-136">In hello new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="be732-137">Nella finestra di dialogo autorizzazione hello risultante selezionare team di GitHub hello che si desidera tooenable provisioning per e quindi selezionare **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="be732-137">In hello resulting authorization dialog, select hello GitHub team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="be732-138">Hello toocomplete portale Azure toohello restituito, una volta completato il provisioning di configurazione.</span><span class="sxs-lookup"><span data-stu-id="be732-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

    ![Finestra di dialogo di autorizzazione](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="be732-140">Nel portale di Azure hello, input **URL Tenant** e fare clic su **Test connessione** tooensure Azure AD può connettersi app GitHub tooyour.</span><span class="sxs-lookup"><span data-stu-id="be732-140">In hello Azure portal, input **Tenant URL** and click **Test Connection** tooensure Azure AD can connect tooyour GitHub app.</span></span> <span data-ttu-id="be732-141">Se hello connessione non riesce, verificare che l'account GitHub abbia autorizzazioni di amministratore e **URl Tenant** immesso è corretto, quindi provare a hello "Autorizza" esegue nuovamente l'istruzione (è possibile costituiscono **URL Tenant** dalla regola: "https : //api.github.com/scim/v2/organizations/ + < Organizations_name > ", è possibile trovare le organizzazioni con l'account GitHub: **impostazioni** > **organizzazioni**).</span><span class="sxs-lookup"><span data-stu-id="be732-141">If hello connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try hello "Authorize" step again (you can constitute **Tenant URL** by rule: "https://api.github.com/scim/v2/organizations/ + <Organizations_name>", you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![Finestra di dialogo di autorizzazione](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="be732-143">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e controllo hello casella di controllo "Invia una notifica di posta elettronica quando si verifica un errore".</span><span class="sxs-lookup"><span data-stu-id="be732-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="be732-144">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="be732-144">Click **Save**.</span></span> 

10. <span data-ttu-id="be732-145">Nella sezione mapping hello, selezionare **tooGitHub sincronizzare Active Directory gli utenti di Azure**.</span><span class="sxs-lookup"><span data-stu-id="be732-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGitHub**.</span></span>

11. <span data-ttu-id="be732-146">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooGitHub di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be732-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGitHub.</span></span> <span data-ttu-id="be732-147">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello account utente in GitHub per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="be732-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in GitHub for update operations.</span></span> <span data-ttu-id="be732-148">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="be732-148">Select hello Save button toocommit any changes.</span></span>

12. <span data-ttu-id="be732-149">tooenable hello servizio provisioning di Azure AD per GitHub, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione</span><span class="sxs-lookup"><span data-stu-id="be732-149">tooenable hello Azure AD provisioning service for GitHub, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13. <span data-ttu-id="be732-150">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="be732-150">Click **Save**.</span></span> 

<span data-ttu-id="be732-151">Questa operazione avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooGitHub in hello gli utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="be732-151">This operation starts hello initial synchronization of any users and/or groups assigned tooGitHub in hello Users and Groups section.</span></span> <span data-ttu-id="be732-152">la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="be732-152">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="be732-153">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio.</span><span class="sxs-lookup"><span data-stu-id="be732-153">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="be732-154">Per ulteriori informazioni sulla modalità di registrazione tooread provisioning di hello Azure AD, vedere [creazione di report per il provisioning utente automatico account](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="be732-154">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="be732-155">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="be732-155">Additional resources</span></span>

* [<span data-ttu-id="be732-156">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="be732-156">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="be732-157">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be732-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="be732-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="be732-158">Next steps</span></span>

* [<span data-ttu-id="be732-159">Informazioni su modalità di registrazione tooreview e ottengono report sull'attività di provisioning</span><span class="sxs-lookup"><span data-stu-id="be732-159">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
