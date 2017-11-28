---
title: 'Esercitazione: Integrazione di Azure Active Directory con Dropbox for Business | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Dropbox for Business.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="8c165-103">Esercitazione: Configurazione di Dropbox for Business per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="8c165-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="8c165-104">obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in Dropbox per Business e Azure AD tooautomatically effettuare il provisioning e il de-provisioning degli account utente da Azure AD tooDropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="8c165-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Dropbox for Business and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c165-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8c165-105">Prerequisites</span></span>

<span data-ttu-id="8c165-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8c165-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="8c165-107">Tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c165-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="8c165-108">Sottoscrizione di Dropbox for Business abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="8c165-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="8c165-109">Account utente in Dropbox for Business con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="8c165-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-toodropbox-for-business"></a><span data-ttu-id="8c165-110">L'assegnazione di utenti tooDropbox for Business</span><span class="sxs-lookup"><span data-stu-id="8c165-110">Assigning users tooDropbox for Business</span></span>

<span data-ttu-id="8c165-111">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="8c165-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="8c165-112">Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="8c165-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="8c165-113">Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano utenti hello bisogno di accesso tooyour Dropbox per app di Business.</span><span class="sxs-lookup"><span data-stu-id="8c165-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Dropbox for Business app.</span></span> <span data-ttu-id="8c165-114">Una volta deciso, è possibile assegnare questi tooyour utenti Dropbox App Business seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="8c165-114">Once decided, you can assign these users tooyour Dropbox for Business app by following hello instructions here:</span></span>

[<span data-ttu-id="8c165-115">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="8c165-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a><span data-ttu-id="8c165-116">Suggerimenti importanti per l'assegnazione di utenti tooDropbox for Business</span><span class="sxs-lookup"><span data-stu-id="8c165-116">Important tips for assigning users tooDropbox for Business</span></span>

*   <span data-ttu-id="8c165-117">È consigliabile che un singolo utente AD Azure viene assegnato tooDropbox per hello tootest Business configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="8c165-117">It is recommended that a single Azure AD user is assigned tooDropbox for Business tootest hello provisioning configuration.</span></span> <span data-ttu-id="8c165-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="8c165-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="8c165-119">Quando si assegna un tooDropbox utente per le aziende, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="8c165-119">When assigning a user tooDropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="8c165-120">ruolo di "accesso predefinita" Hello non funziona per il provisioning...</span><span class="sxs-lookup"><span data-stu-id="8c165-120">hello "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="8c165-121">Abilitare il provisioning utenti automatizzato</span><span class="sxs-lookup"><span data-stu-id="8c165-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="8c165-122">In questa sezione viene illustrata la connessione del tooDropbox di Azure AD per l'API di provisioning dell'account utente di Business e hello provisioning toocreate servizio di configurazione, aggiornare e disabilitare gli account utente assegnato in Dropbox for Business in base a utenti e gruppi assegnazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c165-122">This section guides you through connecting your Azure AD tooDropbox for Business's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="8c165-123">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Dropbox for Business, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c165-123">You may also choose tooenabled SAML-based Single Sign-On for Dropbox for Business, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8c165-124">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="8c165-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="8c165-125">tooconfigure account il provisioning utente automatico:</span><span class="sxs-lookup"><span data-stu-id="8c165-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="8c165-126">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="8c165-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="8c165-127">Se è già stato configurato Dropbox for Business per single sign-on, eseguire la ricerca per l'istanza di Dropbox for Business utilizzando il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="8c165-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using hello search field.</span></span> <span data-ttu-id="8c165-128">In caso contrario, selezionare **Aggiungi** e cercare **Dropbox for Business** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8c165-128">Otherwise, select **Add** and search for **Dropbox for Business** in hello application gallery.</span></span> <span data-ttu-id="8c165-129">Selezionare Dropbox for Business dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8c165-129">Select Dropbox for Business from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="8c165-130">Selezionare l'istanza di Dropbox for Business, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="8c165-130">Select your instance of Dropbox for Business, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="8c165-131">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="8c165-131">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="8c165-133">In hello **credenziali di amministratore** fare clic su **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="8c165-133">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="8c165-134">Viene aperta una finestra di dialogo di accesso di Dropbox for Business in una nuova finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="8c165-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="8c165-135">In hello **Accedi tooDropbox toolink con Azure AD** finestra di dialogo di accesso tooyour Dropbox per il tenant di Business.</span><span class="sxs-lookup"><span data-stu-id="8c165-135">On hello **Sign-in tooDropbox toolink with Azure AD** dialog, sign in tooyour Dropbox for Business tenant.</span></span>

     <span data-ttu-id="8c165-136">![Provisioning degli utenti](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Provisioning degli utenti")</span><span class="sxs-lookup"><span data-stu-id="8c165-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="8c165-137">Confermare che si desidera toogive Azure Active Directory autorizzazione toomake modifiche tooyour Dropbox per il tenant di Business.</span><span class="sxs-lookup"><span data-stu-id="8c165-137">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Dropbox for Business tenant.</span></span> <span data-ttu-id="8c165-138">Fare clic su **Consenti**.</span><span class="sxs-lookup"><span data-stu-id="8c165-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="8c165-139">![Provisioning degli utenti](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Provisioning degli utenti")</span><span class="sxs-lookup"><span data-stu-id="8c165-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="8c165-140">Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour Dropbox per app di Business.</span><span class="sxs-lookup"><span data-stu-id="8c165-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Dropbox for Business app.</span></span> <span data-ttu-id="8c165-141">Se hello connessione non riesce, assicurarsi di Dropbox per conto di Business con autorizzazioni di amministratore di Team e provare a hello **"Autorizza"** esegue nuovamente l'istruzione.</span><span class="sxs-lookup"><span data-stu-id="8c165-141">If hello connection fails, ensure your Dropbox for Business account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

9. <span data-ttu-id="8c165-142">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="8c165-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

10. <span data-ttu-id="8c165-143">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8c165-143">Click **Save.**</span></span>

11. <span data-ttu-id="8c165-144">Nella sezione mapping hello, selezionare **tooDropbox sincronizzare Active Directory gli utenti di Azure per le aziende.**</span><span class="sxs-lookup"><span data-stu-id="8c165-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDropbox for Business.**</span></span>

12. <span data-ttu-id="8c165-145">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da Azure AD tooDropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="8c165-145">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDropbox for Business.</span></span> <span data-ttu-id="8c165-146">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello account utente in Dropbox for Business per le operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="8c165-146">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="8c165-147">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="8c165-147">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="8c165-148">tooenable hello servizio provisioning di Azure AD per Dropbox for Business, hello modifica **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello</span><span class="sxs-lookup"><span data-stu-id="8c165-148">tooenable hello Azure AD provisioning service for Dropbox for Business, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

14. <span data-ttu-id="8c165-149">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8c165-149">Click **Save.**</span></span>

<span data-ttu-id="8c165-150">Avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooDropbox for Business in hello gli utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="8c165-150">It starts hello initial synchronization of any users and/or groups assigned tooDropbox for Business in hello Users and Groups section.</span></span> <span data-ttu-id="8c165-151">la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8c165-151">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="8c165-152">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio in Dropbox per app di Business.</span><span class="sxs-lookup"><span data-stu-id="8c165-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="8c165-153">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="8c165-153">You can now create a test account.</span></span> <span data-ttu-id="8c165-154">Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooDropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="8c165-154">Wait for up too20 minutes tooverify that hello account has been synchronized tooDropbox for Business.</span></span>

<span data-ttu-id="8c165-155">Un ciclo di provisioning utenti completato correttamente è indicato da uno stato correlato.</span><span class="sxs-lookup"><span data-stu-id="8c165-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="8c165-156">![Assegnare utenti](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assegnare utenti")</span><span class="sxs-lookup"><span data-stu-id="8c165-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8c165-157">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8c165-157">Additional resources</span></span>

* [<span data-ttu-id="8c165-158">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="8c165-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8c165-159">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c165-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="8c165-160">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8c165-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)