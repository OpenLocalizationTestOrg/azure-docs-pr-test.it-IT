---
title: 'Esercitazione: Integrazione di Azure Active Directory con Salesforce | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Salesforce.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a916be8dbf0b4c6173cda873936a53cd1f3ff12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a><span data-ttu-id="18d56-103">Esercitazione: Configurazione di Salesforce per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="18d56-103">Tutorial: Configuring Salesforce for Automatic User Provisioning</span></span>

<span data-ttu-id="18d56-104">obiettivo di Hello di questa esercitazione è tooshow tooperform necessari passaggi hello in Salesforce e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="18d56-104">hello objective of this tutorial is tooshow hello steps required tooperform in Salesforce and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSalesforce.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18d56-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="18d56-105">Prerequisites</span></span>

<span data-ttu-id="18d56-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="18d56-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="18d56-107">Tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="18d56-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="18d56-108">È necessario disporre di un tenant valido per Salesforce for Work o Salesforce for Education.</span><span class="sxs-lookup"><span data-stu-id="18d56-108">You must have a valid tenant for Salesforce for Work or Salesforce for Education.</span></span> <span data-ttu-id="18d56-109">È possibile usare un account della versione di valutazione gratuita per entrambi i servizi.</span><span class="sxs-lookup"><span data-stu-id="18d56-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="18d56-110">Account utente in Salesforce con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="18d56-110">A user account in Salesforce with Team Admin permissions.</span></span>

## <a name="assigning-users-toosalesforce"></a><span data-ttu-id="18d56-111">L'assegnazione di utenti tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="18d56-111">Assigning users tooSalesforce</span></span>

<span data-ttu-id="18d56-112">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="18d56-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="18d56-113">Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="18d56-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="18d56-114">Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour Salesforce app.</span><span class="sxs-lookup"><span data-stu-id="18d56-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Salesforce app.</span></span> <span data-ttu-id="18d56-115">Una volta deciso, è possibile assegnare queste app di Salesforce tooyour utenti seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="18d56-115">Once decided, you can assign these users tooyour Salesforce app by following hello instructions here:</span></span>

[<span data-ttu-id="18d56-116">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="18d56-116">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce"></a><span data-ttu-id="18d56-117">Suggerimenti importanti per l'assegnazione di utenti tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="18d56-117">Important tips for assigning users tooSalesforce</span></span>

*   <span data-ttu-id="18d56-118">È consigliabile che un singolo utente AD Azure viene assegnato hello tootest tooSalesforce configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="18d56-118">It is recommended that a single Azure AD user is assigned tooSalesforce tootest hello provisioning configuration.</span></span> <span data-ttu-id="18d56-119">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="18d56-119">Additional users and/or groups may be assigned later.</span></span>

*  <span data-ttu-id="18d56-120">Quando si assegna un tooSalesforce utente, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="18d56-120">When assigning a user tooSalesforce, you must select a valid user role.</span></span> <span data-ttu-id="18d56-121">ruolo di "accesso predefinita" Hello non funziona per il provisioning</span><span class="sxs-lookup"><span data-stu-id="18d56-121">hello "Default Access" role does not work for provisioning</span></span>

    > [!NOTE]
    > <span data-ttu-id="18d56-122">Questa app Importa ruoli personalizzati da Salesforce come parte del processo, il cliente che hello opportuno tooselect assegnare gli utenti di provisioning hello</span><span class="sxs-lookup"><span data-stu-id="18d56-122">This app imports custom roles from Salesforce as part of hello provisioning process, which hello customer may want tooselect when assigning users</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="18d56-123">Abilitare il provisioning utenti automatizzato</span><span class="sxs-lookup"><span data-stu-id="18d56-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="18d56-124">Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooSalesforce il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in Salesforce in base all'assegnazione di utenti e gruppi in Azure AD .</span><span class="sxs-lookup"><span data-stu-id="18d56-124">This section guides you through connecting your Azure AD tooSalesforce's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Salesforce based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="18d56-125">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Salesforce, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="18d56-125">You may also choose tooenabled SAML-based Single Sign-On for Salesforce, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="18d56-126">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="18d56-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="18d56-127">tooconfigure account il provisioning utente automatico:</span><span class="sxs-lookup"><span data-stu-id="18d56-127">tooconfigure automatic user account provisioning:</span></span>

<span data-ttu-id="18d56-128">obiettivo di Hello di questa sezione è toooutline tooenable provisioning utente dell'utente di Active Directory come account di tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="18d56-128">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce.</span></span>

1. <span data-ttu-id="18d56-129">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="18d56-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="18d56-130">Se è già stato configurato Salesforce per single sign-on, eseguire la ricerca per l'istanza di Salesforce utilizzando il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="18d56-130">If you have already configured Salesforce for single sign-on, search for your instance of Salesforce using hello search field.</span></span> <span data-ttu-id="18d56-131">In caso contrario, selezionare **Aggiungi** e cercare **Salesforce** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="18d56-131">Otherwise, select **Add** and search for **Salesforce** in hello application gallery.</span></span> <span data-ttu-id="18d56-132">Selezionare Salesforce dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="18d56-132">Select Salesforce from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="18d56-133">Selezionare l'istanza di Salesforce, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="18d56-133">Select your instance of Salesforce, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="18d56-134">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="18d56-134">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
<span data-ttu-id="18d56-135">![provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="18d56-135">![provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="18d56-136">In hello **credenziali di amministratore** sezione, fornire hello le impostazioni di configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="18d56-136">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="18d56-137">a.</span><span class="sxs-lookup"><span data-stu-id="18d56-137">a.</span></span> <span data-ttu-id="18d56-138">In hello **nome utente amministratore** digitare un nome che è hello account Salesforce **amministratore di sistema** profilo in Salesforce.com assegnato.</span><span class="sxs-lookup"><span data-stu-id="18d56-138">In hello **Admin User Name** textbox, type a Salesforce account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="18d56-139">b.</span><span class="sxs-lookup"><span data-stu-id="18d56-139">b.</span></span> <span data-ttu-id="18d56-140">In hello **Password amministratore** casella di testo, digitare la password hello per questo account.</span><span class="sxs-lookup"><span data-stu-id="18d56-140">In hello **Admin Password** textbox, type hello password for this account.</span></span>

6. <span data-ttu-id="18d56-141">tooget il token di sicurezza di Salesforce, aprire una nuova scheda e accedere a hello stesso account di amministratore di Salesforce.</span><span class="sxs-lookup"><span data-stu-id="18d56-141">tooget your Salesforce security token, open a new tab and sign into hello same Salesforce admin account.</span></span> <span data-ttu-id="18d56-142">Fare clic sul nome, hello angolo superiore destro della pagina hello e quindi fare clic su **impostazioni personali**.</span><span class="sxs-lookup"><span data-stu-id="18d56-142">On hello top right corner of hello page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="18d56-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="18d56-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="18d56-144">Nel riquadro di spostamento a sinistra di hello, fare clic su **personale** tooexpand hello sezione correlata e quindi fare clic su **Reimposta Token di sicurezza personale**.</span><span class="sxs-lookup"><span data-stu-id="18d56-144">On hello left navigation pane, click **Personal** tooexpand hello related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="18d56-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="18d56-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="18d56-146">In hello **Reimposta Token di sicurezza personale** pagina, fare clic su **Reimposta Token di sicurezza** pulsante.</span><span class="sxs-lookup"><span data-stu-id="18d56-146">On hello **Reset My Security Token** page, click **Reset Security Token** button.</span></span>

    <span data-ttu-id="18d56-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span><span class="sxs-lookup"><span data-stu-id="18d56-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="18d56-148">Controllare hello posta in arrivo associata all'account di amministratore.</span><span class="sxs-lookup"><span data-stu-id="18d56-148">Check hello email inbox associated with this admin account.</span></span> <span data-ttu-id="18d56-149">Cercare un messaggio di posta elettronica da Salesforce.com che contiene il nuovo token di sicurezza hello.</span><span class="sxs-lookup"><span data-stu-id="18d56-149">Look for an email from Salesforce.com that contains hello new security token.</span></span>
10. <span data-ttu-id="18d56-150">Hello tooyour di token, vedere la finestra di Azure AD copiare e incollare il codice in hello **Socket Token** campo.</span><span class="sxs-lookup"><span data-stu-id="18d56-150">Copy hello token, go tooyour Azure AD window, and paste it into hello **Socket Token** field.</span></span>

11. <span data-ttu-id="18d56-151">Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour Salesforce app.</span><span class="sxs-lookup"><span data-stu-id="18d56-151">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Salesforce app.</span></span>

12. <span data-ttu-id="18d56-152">In hello **notifica tramite posta elettronica** immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning e casella di controllo hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="18d56-152">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox below.</span></span>

13. <span data-ttu-id="18d56-153">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="18d56-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="18d56-154">Nella sezione mapping hello, selezionare **tooSalesforce sincronizzare Active Directory gli utenti di Azure.**</span><span class="sxs-lookup"><span data-stu-id="18d56-154">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSalesforce.**</span></span>

15. <span data-ttu-id="18d56-155">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooSalesforce di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18d56-155">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSalesforce.</span></span> <span data-ttu-id="18d56-156">Si noti che gli attributi selezionati come hello **corrispondenza** proprietà sono utilizzate toomatch hello account utente in Salesforce per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="18d56-156">Note that hello attributes selected as **Matching** properties are used toomatch hello user accounts in Salesforce for update operations.</span></span> <span data-ttu-id="18d56-157">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="18d56-157">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="18d56-158">tooenable hello servizio provisioning di Azure AD per Salesforce, hello modifica **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello</span><span class="sxs-lookup"><span data-stu-id="18d56-158">tooenable hello Azure AD provisioning service for Salesforce, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

17. <span data-ttu-id="18d56-159">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="18d56-159">Click **Save.**</span></span>

<span data-ttu-id="18d56-160">Verrà avviata la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooSalesforce in hello gli utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="18d56-160">This starts hello initial synchronization of any users and/or groups assigned tooSalesforce in hello Users and Groups section.</span></span> <span data-ttu-id="18d56-161">Si noti che la sincronizzazione iniziale hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="18d56-161">Note that hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="18d56-162">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio nella tua app di Salesforce.</span><span class="sxs-lookup"><span data-stu-id="18d56-162">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Salesforce app.</span></span>

<span data-ttu-id="18d56-163">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="18d56-163">You can now create a test account.</span></span> <span data-ttu-id="18d56-164">Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="18d56-164">Wait for up too20 minutes tooverify that hello account has been synchronized tooSalesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="18d56-165">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="18d56-165">Additional resources</span></span>

* [<span data-ttu-id="18d56-166">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="18d56-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18d56-167">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18d56-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="18d56-168">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="18d56-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforce-tutorial.md)