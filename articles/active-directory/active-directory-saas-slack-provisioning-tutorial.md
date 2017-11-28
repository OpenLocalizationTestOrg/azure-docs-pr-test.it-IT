---
title: 'Esercitazione: Configurazione di Slack per il provisioning utenti automatico con Azure Active Directory | Documentazione Microsoft'
description: Informazioni su come tooconfigure Azure Active Directory tooautomatically il provisioning e il de-provisioning account utente di tooSlack.
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="c273c-103">Esercitazione: Configurazione di Slack per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="c273c-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="c273c-104">obiettivo di questa esercitazione Hello è tooshow hello passaggi che è necessario tooperform in Slack e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooSlack.</span><span class="sxs-lookup"><span data-stu-id="c273c-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Slack and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSlack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c273c-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c273c-105">Prerequisites</span></span>

<span data-ttu-id="c273c-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="c273c-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="c273c-107">Tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c273c-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="c273c-108">Il margine di flessibilità tenant hello [Plus piano](https://aadsyncfabric.slack.com/pricing) o meglio abilitato</span><span class="sxs-lookup"><span data-stu-id="c273c-108">A Slack tenant with hello [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="c273c-109">Account utente in Slack con autorizzazioni di amministratore di team</span><span class="sxs-lookup"><span data-stu-id="c273c-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="c273c-110">Nota: hello provisioning integrazione di Azure AD si basa su hello [Slack SCIM API](https://api.slack.com/scim) ovvero team tooSlack disponibile sulla hello più piano o migliori.</span><span class="sxs-lookup"><span data-stu-id="c273c-110">Note: hello Azure AD provisioning integration relies on hello [Slack SCIM API](https://api.slack.com/scim) which is available tooSlack teams on hello Plus plan or better.</span></span>

## <a name="assigning-users-tooslack"></a><span data-ttu-id="c273c-111">L'assegnazione di utenti tooSlack</span><span class="sxs-lookup"><span data-stu-id="c273c-111">Assigning users tooSlack</span></span>

<span data-ttu-id="c273c-112">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="c273c-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="c273c-113">Nel contesto di hello di provisioning dell'account utente automatica, verranno sincronizzati solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c273c-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="c273c-114">Prima di configurare e abilitare hello provisioning del servizio, sarà necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour Slack app.</span><span class="sxs-lookup"><span data-stu-id="c273c-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Slack app.</span></span> <span data-ttu-id="c273c-115">Una volta deciso, è possibile assegnare queste app di Slack tooyour utenti seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="c273c-115">Once decided, you can assign these users tooyour Slack app by following hello instructions here:</span></span>

[<span data-ttu-id="c273c-116">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="c273c-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a><span data-ttu-id="c273c-117">Suggerimenti importanti per l'assegnazione di utenti tooSlack</span><span class="sxs-lookup"><span data-stu-id="c273c-117">Important tips for assigning users tooSlack</span></span>

*   <span data-ttu-id="c273c-118">È consigliabile che un singolo utente di Azure AD assegnare tooSlack tootest hello configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="c273c-118">It is recommended that a single Azure AD user be assigned tooSlack tootest hello provisioning configuration.</span></span> <span data-ttu-id="c273c-119">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="c273c-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="c273c-120">Quando si assegna un tooSlack utente, è necessario selezionare hello **utente** o il ruolo di "Gruppo" nella finestra di dialogo assegnazione hello.</span><span class="sxs-lookup"><span data-stu-id="c273c-120">When assigning a user tooSlack, you must select hello **User** or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="c273c-121">ruolo di "accesso predefinita" Hello non funziona per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="c273c-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-tooslack"></a><span data-ttu-id="c273c-122">Configurazione tooSlack di provisioning dell'utente</span><span class="sxs-lookup"><span data-stu-id="c273c-122">Configuring user provisioning tooSlack</span></span> 

<span data-ttu-id="c273c-123">Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooSlack il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in Slack in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c273c-123">This section guides you through connecting your Azure AD tooSlack's user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="c273c-124">**Suggerimento:** tooenabled basato su SAML Single Sign-On per Slack, attenendosi alle istruzioni hello cui (portale di Azure) è possibile scegliere [https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="c273c-124">**Tip:** You may also choose tooenabled SAML-based Single Sign-On for Slack, following hello instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="c273c-125">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="c273c-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a><span data-ttu-id="c273c-126">account utente automatico tooconfigure tooSlack il provisioning in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c273c-126">tooconfigure automatic user account provisioning tooSlack in Azure AD:</span></span>


1)  <span data-ttu-id="c273c-127">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="c273c-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="c273c-128">Se è già stato configurato il margine di flessibilità per single sign-on, eseguire la ricerca per l'istanza di Slack usando il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="c273c-128">If you have already configured Slack for single sign-on, search for your instance of Slack using hello search field.</span></span> <span data-ttu-id="c273c-129">In caso contrario, selezionare **Aggiungi** e cercare **Slack** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c273c-129">Otherwise, select **Add** and search for **Slack** in hello application gallery.</span></span> <span data-ttu-id="c273c-130">Selezionare il margine di flessibilità dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c273c-130">Select Slack from hello search results, and add it tooyour list of applications.</span></span>

3)  <span data-ttu-id="c273c-131">Selezionare l'istanza di un margine di flessibilità, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="c273c-131">Select your instance of Slack, then select hello **Provisioning** tab.</span></span>

4)  <span data-ttu-id="c273c-132">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="c273c-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Provisioning in Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="c273c-134">In hello **credenziali di amministratore** fare clic su **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="c273c-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="c273c-135">Verrà aperta una finestra di dialogo di autorizzazione di Slack in una nuova finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="c273c-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="c273c-136">Nella nuova finestra hello, accedere a Slack utilizzando l'account amministratore di Team.</span><span class="sxs-lookup"><span data-stu-id="c273c-136">In hello new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="c273c-137">Nella finestra di dialogo autorizzazione hello risultante selezionare hello Slack team che si desidera tooenable provisioning per e quindi selezionare **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="c273c-137">in hello resulting authorization dialog, select hello Slack team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="c273c-138">Hello toocomplete portale Azure toohello restituito, una volta completato il provisioning di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c273c-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

![Finestra di dialogo di autorizzazione](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="c273c-140">Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour Slack app.</span><span class="sxs-lookup"><span data-stu-id="c273c-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Slack app.</span></span> <span data-ttu-id="c273c-141">Se hello connessione non riesce, verificare che l'account Slack disponga delle autorizzazioni di amministratore di Team e provare hello che esegue nuovamente l'istruzione "Autorizza".</span><span class="sxs-lookup"><span data-stu-id="c273c-141">If hello connection fails, ensure your Slack account has Team Admin permissions and try hello "Authorize" step again.</span></span>

8) <span data-ttu-id="c273c-142">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c273c-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

9) <span data-ttu-id="c273c-143">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c273c-143">Click **Save**.</span></span> 

10) <span data-ttu-id="c273c-144">Nella sezione mapping hello, selezionare **tooSlack sincronizzare Active Directory gli utenti di Azure**.</span><span class="sxs-lookup"><span data-stu-id="c273c-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSlack**.</span></span>

11) <span data-ttu-id="c273c-145">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che verranno sincronizzati da tooSlack di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c273c-145">In hello **Attribute Mappings** section, review hello user attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="c273c-146">Si noti che gli attributi selezionati come hello **corrispondenza** proprietà saranno gli account utente hello toomatch utilizzata nel margine di flessibilità per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c273c-146">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts in Slack for update operations.</span></span> <span data-ttu-id="c273c-147">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="c273c-147">Select hello Save button toocommit any changes.</span></span>

12) <span data-ttu-id="c273c-148">tooenable hello servizio provisioning di Azure AD per Slack, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione</span><span class="sxs-lookup"><span data-stu-id="c273c-148">tooenable hello Azure AD provisioning service for Slack, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13) <span data-ttu-id="c273c-149">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c273c-149">Click **Save**.</span></span> 

<span data-ttu-id="c273c-150">Verrà avviata la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooSlack in hello gli utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="c273c-150">This will start hello initial synchronization of any users and/or groups assigned tooSlack in hello Users and Groups section.</span></span> <span data-ttu-id="c273c-151">Si noti che la sincronizzazione iniziale hello tooperform più lungo di sincronizzazioni successive, che si verificano ogni 10 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c273c-151">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 10 minutes as long as hello service is running.</span></span> <span data-ttu-id="c273c-152">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite dal servizio nella tua app Slack hello.</span><span class="sxs-lookup"><span data-stu-id="c273c-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-tooslack"></a><span data-ttu-id="c273c-153">[Facoltativo] Configurazione oggetto gruppo provisioning tooSlack</span><span class="sxs-lookup"><span data-stu-id="c273c-153">[Optional] Configuring group object provisioning tooSlack</span></span> 

<span data-ttu-id="c273c-154">Facoltativamente, è possibile abilitare il provisioning degli oggetti di gruppo da Azure AD tooSlack hello.</span><span class="sxs-lookup"><span data-stu-id="c273c-154">Optionally, you can enable hello provisioning of group objects from Azure AD tooSlack.</span></span> <span data-ttu-id="c273c-155">Questo comportamento è diverso da "assegnazione dei gruppi di utenti", in tale oggetto gruppo effettivo di hello inoltre tooits membri verranno replicati dai tooSlack di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c273c-155">This is different from "assigning groups of users", in that hello actual group object in addition tooits members will be replicated from Azure AD tooSlack.</span></span> <span data-ttu-id="c273c-156">Se si ha un gruppo denominato "Gruppo personale" in Azure AD, ad esempio, in Slack verrà creato un identico gruppo denominato "Gruppo personale".</span><span class="sxs-lookup"><span data-stu-id="c273c-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="tooenable-provisioning-of-group-objects"></a><span data-ttu-id="c273c-157">tooenable provisioning degli oggetti di gruppo:</span><span class="sxs-lookup"><span data-stu-id="c273c-157">tooenable provisioning of group objects:</span></span>

1) <span data-ttu-id="c273c-158">Nella sezione mapping hello, selezionare **tooSlack sincronizzare Azure gruppi di Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c273c-158">Under hello Mappings section, select **Synchronize Azure Active Directory Groups tooSlack**.</span></span>

2) <span data-ttu-id="c273c-159">Nel Pannello di mappatura attributi hello, impostare tooYes abilitato.</span><span class="sxs-lookup"><span data-stu-id="c273c-159">In hello Attribute Mapping blade, set Enabled tooYes.</span></span>

3) <span data-ttu-id="c273c-160">In hello **mapping degli attributi** sezione, verificare hello gruppo attributi che verranno sincronizzati da tooSlack di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c273c-160">In hello **Attribute Mappings** section, review hello group attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="c273c-161">Si noti che gli attributi selezionati come hello **corrispondenza** proprietà saranno i gruppi di hello toomatch utilizzata nel margine di flessibilità per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c273c-161">Note that hello attributes selected as **Matching** properties will be used toomatch hello groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="c273c-162">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c273c-162">Click **Save**.</span></span>

<span data-ttu-id="c273c-163">Questo risultato in qualsiasi tooSlack di oggetti assegnati gruppo in hello **utenti e gruppi** sezione completamente sincronizzati da tooSlack di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c273c-163">This result in any group objects assigned tooSlack in hello **Users and Groups** section being fully synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="c273c-164">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite dal servizio nella tua app Slack hello.</span><span class="sxs-lookup"><span data-stu-id="c273c-164">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c273c-165">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c273c-165">Additional Resources</span></span>

* [<span data-ttu-id="c273c-166">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="c273c-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="c273c-167">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c273c-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
