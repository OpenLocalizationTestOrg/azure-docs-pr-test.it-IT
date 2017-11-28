---
title: 'Esercitazione: Integrazione di Azure Active Directory con Concur | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Concur.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="fd605-103">Esercitazione: Configurazione di Concur per il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="fd605-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="fd605-104">obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in Concur e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooConcur.</span><span class="sxs-lookup"><span data-stu-id="fd605-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Concur and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooConcur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd605-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fd605-105">Prerequisites</span></span>

<span data-ttu-id="fd605-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="fd605-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="fd605-107">Tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd605-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="fd605-108">Sottoscrizione di Concur abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="fd605-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="fd605-109">Account utente in Concur con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="fd605-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-tooconcur"></a><span data-ttu-id="fd605-110">L'assegnazione di utenti tooConcur</span><span class="sxs-lookup"><span data-stu-id="fd605-110">Assigning users tooConcur</span></span>

<span data-ttu-id="fd605-111">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="fd605-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="fd605-112">Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="fd605-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="fd605-113">Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour Concur app.</span><span class="sxs-lookup"><span data-stu-id="fd605-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Concur app.</span></span> <span data-ttu-id="fd605-114">Una volta deciso, è possibile assegnare queste app di Concur tooyour utenti seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="fd605-114">Once decided, you can assign these users tooyour Concur app by following hello instructions here:</span></span>

[<span data-ttu-id="fd605-115">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="fd605-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a><span data-ttu-id="fd605-116">Suggerimenti importanti per l'assegnazione di utenti tooConcur</span><span class="sxs-lookup"><span data-stu-id="fd605-116">Important tips for assigning users tooConcur</span></span>

*   <span data-ttu-id="fd605-117">È consigliabile che un singolo utente di Azure AD assegnare tooConcur tootest hello configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="fd605-117">It is recommended that a single Azure AD user be assigned tooConcur tootest hello provisioning configuration.</span></span> <span data-ttu-id="fd605-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="fd605-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="fd605-119">Quando si assegna un tooConcur utente, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="fd605-119">When assigning a user tooConcur, you must select a valid user role.</span></span> <span data-ttu-id="fd605-120">ruolo di "accesso predefinita" Hello non funziona per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="fd605-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="fd605-121">Abilitare il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="fd605-121">Enable user provisioning</span></span>

<span data-ttu-id="fd605-122">Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooConcur il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in Concur in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd605-122">This section guides you through connecting your Azure AD tooConcur's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="fd605-123">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Concur, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd605-123">You may also choose tooenabled SAML-based Single Sign-On for Concur, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fd605-124">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="fd605-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="fd605-125">tooconfigure provisioning dell'account utente:</span><span class="sxs-lookup"><span data-stu-id="fd605-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="fd605-126">obiettivo di Hello di questa sezione è toooutline tooenable provisioning dell'utente di Active Directory come account di tooConcur.</span><span class="sxs-lookup"><span data-stu-id="fd605-126">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooConcur.</span></span>

<span data-ttu-id="fd605-127">App tooenable in hello servizio Expense, è toobe corretta configurazione e l'utilizzo di un profilo di amministratore del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="fd605-127">tooenable apps in hello Expense Service, there has toobe proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="fd605-128">Non aggiungere hello amministratore ruolo tooyour profilo amministratore esistente utilizzato per le funzioni amministrative di T & E.</span><span class="sxs-lookup"><span data-stu-id="fd605-128">Don't add hello WS Admin role tooyour existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="fd605-129">I consulenti concur o amministratore client hello è necessario creare un profilo di amministratore del servizio Web distinti e messaggio per l'amministratore Client debba usare questo profilo per le funzioni hello amministratore dei servizi Web (ad esempio, l'abilitazione di App).</span><span class="sxs-lookup"><span data-stu-id="fd605-129">Concur Consultants or hello client administrator must create a distinct Web Service Administrator profile and hello Client administrator must use this profile for hello Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="fd605-130">Questi profili devono essere mantenuti separati dal profilo amministratore T & E giornaliero dell'amministratore di hello client (hello T & profilo di amministratore E non deve hello assegnato il ruolo).</span><span class="sxs-lookup"><span data-stu-id="fd605-130">These profiles must be kept separate from hello client administrator's daily T&E admin profile (hello T&E admin profile should not have hello WSAdmin role assigned).</span></span>

<span data-ttu-id="fd605-131">Quando si crea hello profilo toobe utilizzato per l'abilitazione di app hello, immettere il nome dell'amministratore di hello client nei campi di profilo utente hello.</span><span class="sxs-lookup"><span data-stu-id="fd605-131">When you create hello profile toobe used for enabling hello app, enter hello client administrator's name into hello user profile fields.</span></span> <span data-ttu-id="fd605-132">Ciò consente di assegnare il profilo toohello proprietà.</span><span class="sxs-lookup"><span data-stu-id="fd605-132">This assigns ownership toohello profile.</span></span> <span data-ttu-id="fd605-133">Dopo aver creato uno o più profili, i client di hello dovrà accedere con questo hello tooclick profilo "*abilitare*" pulsante per un'App Partner nel menu Web Services hello.</span><span class="sxs-lookup"><span data-stu-id="fd605-133">Once one or more profiles is created, hello client must log in with this profile tooclick hello "*Enable*" button for a Partner App within hello Web Services menu.</span></span>

<span data-ttu-id="fd605-134">Per i seguenti motivi di hello, questa azione non deve essere eseguita con il profilo di hello usato per la normale amministrazione T & E.</span><span class="sxs-lookup"><span data-stu-id="fd605-134">For hello following reasons, this action should not be done with hello profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="fd605-135">Hello client ha toobe hello che fa clic su "*Sì*" nella finestra di dialogo hello visualizzata dopo l'abilitazione di un'app.</span><span class="sxs-lookup"><span data-stu-id="fd605-135">hello client has toobe hello one that clicks "*Yes*" on hello dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="fd605-136">Fare clic su Invia un acknowledgement client hello viene disposto per hello Partner applicazione tooaccess i propri dati, pertanto si o hello Partner non è possibile fare clic su che pulsante Sì.</span><span class="sxs-lookup"><span data-stu-id="fd605-136">This click acknowledges hello client is willing for hello Partner application tooaccess their data, so you or hello Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="fd605-137">Se un amministratore client che ha abilitato un'app usando hello T & profilo di amministratore E lascia la società hello (risultante nel profilo hello viene disattivato), tutte le app abilitate tramite tale profilo non funzionare fino a quando l'applicazione hello è abilitata con un altro amministratore active profilo.</span><span class="sxs-lookup"><span data-stu-id="fd605-137">If a client administrator that has enabled an app using hello T&E admin profile leaves hello company (resulting in hello profile being inactivated), any apps enabled using that profile does not function until hello app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="fd605-138">È per questo motivo che si suppone toocreate distinct amministratore profili.</span><span class="sxs-lookup"><span data-stu-id="fd605-138">This is why you are supposed toocreate distinct WS Admin profiles.</span></span>

* <span data-ttu-id="fd605-139">Se un amministratore lascia la società hello, profilo di amministratore può essere amministratore di sostituzione toohello modificato se si desidera senza conseguenze hello abilitato app perché tale profilo non è necessario disattivata toohello hello associata.</span><span class="sxs-lookup"><span data-stu-id="fd605-139">If an administrator leaves hello company, hello name associated toohello WS Admin profile can be changed toohello replacement administrator if desired without impacting hello enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="fd605-140">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="fd605-140">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="fd605-141">Accesso tooyour **Concur** tenant.</span><span class="sxs-lookup"><span data-stu-id="fd605-141">Log on tooyour **Concur** tenant.</span></span>

2. <span data-ttu-id="fd605-142">Da hello **amministrazione** dal menu **servizi Web**.</span><span class="sxs-lookup"><span data-stu-id="fd605-142">From hello **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="fd605-143">![Tenant Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Tenant Concur")</span><span class="sxs-lookup"><span data-stu-id="fd605-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="fd605-144">Sul lato sinistro, da hello hello **servizi Web** riquadro, selezionare **Abilita applicazione Partner**.</span><span class="sxs-lookup"><span data-stu-id="fd605-144">On hello left side, from hello **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="fd605-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span><span class="sxs-lookup"><span data-stu-id="fd605-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="fd605-146">Da hello **Abilita applicazione** elenco, selezionare **Azure Active Directory**, quindi fare clic su **abilitare**.</span><span class="sxs-lookup"><span data-stu-id="fd605-146">From hello **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="fd605-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="fd605-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="fd605-148">Fare clic su **Sì** tooclose hello **conferma azione** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="fd605-148">Click **Yes** tooclose hello **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="fd605-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span><span class="sxs-lookup"><span data-stu-id="fd605-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="fd605-150">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="fd605-150">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="fd605-151">Se è già stato configurato Concur per single sign-on, eseguire la ricerca per l'istanza di Concur utilizzando il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="fd605-151">If you have already configured Concur for single sign-on, search for your instance of Concur using hello search field.</span></span> <span data-ttu-id="fd605-152">In caso contrario, selezionare **Aggiungi** e cercare **Concur** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="fd605-152">Otherwise, select **Add** and search for **Concur** in hello application gallery.</span></span> <span data-ttu-id="fd605-153">Selezionare Concur dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="fd605-153">Select Concur from hello search results, and add it tooyour list of applications.</span></span>

8. <span data-ttu-id="fd605-154">Selezionare l'istanza di Concur, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="fd605-154">Select your instance of Concur, then select hello **Provisioning** tab.</span></span>

9. <span data-ttu-id="fd605-155">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="fd605-155">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
 
    ![provisioning](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="fd605-157">In hello **credenziali di amministratore** immettere hello **nome utente** hello e **password** dell'amministratore di Concur.</span><span class="sxs-lookup"><span data-stu-id="fd605-157">Under hello **Admin Credentials** section, enter hello **user name** and hello **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="fd605-158">Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour Concur app.</span><span class="sxs-lookup"><span data-stu-id="fd605-158">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Concur app.</span></span> <span data-ttu-id="fd605-159">Se hello connessione non riesce, verificare che l'account di Concur disponga delle autorizzazioni di amministratore di Team.</span><span class="sxs-lookup"><span data-stu-id="fd605-159">If hello connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="fd605-160">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="fd605-160">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

13. <span data-ttu-id="fd605-161">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fd605-161">Click **Save.**</span></span>

14. <span data-ttu-id="fd605-162">Nella sezione mapping hello, selezionare **tooConcur sincronizzare Active Directory gli utenti di Azure.**</span><span class="sxs-lookup"><span data-stu-id="fd605-162">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooConcur.**</span></span>

15. <span data-ttu-id="fd605-163">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooConcur di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd605-163">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooConcur.</span></span> <span data-ttu-id="fd605-164">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello account utente in Concur per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="fd605-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Concur for update operations.</span></span> <span data-ttu-id="fd605-165">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="fd605-165">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="fd605-166">tooenable hello servizio provisioning di Azure AD per Concur, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione</span><span class="sxs-lookup"><span data-stu-id="fd605-166">tooenable hello Azure AD provisioning service for Concur, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

17. <span data-ttu-id="fd605-167">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fd605-167">Click **Save.**</span></span>

<span data-ttu-id="fd605-168">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="fd605-168">You can now create a test account.</span></span> <span data-ttu-id="fd605-169">Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooConcur.</span><span class="sxs-lookup"><span data-stu-id="fd605-169">Wait for up too20 minutes tooverify that hello account has been synchronized tooConcur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fd605-170">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="fd605-170">Additional resources</span></span>

* [<span data-ttu-id="fd605-171">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="fd605-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fd605-172">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd605-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="fd605-173">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="fd605-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

