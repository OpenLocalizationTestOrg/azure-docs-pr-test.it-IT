---
title: 'Esercitazione: Configurazione di Samanage per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come tooconfigure Azure Active Directory tooautomatically il provisioning e il de-provisioning account utente di tooSamanage.
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
ms.openlocfilehash: 6cb36d2cc6ce33da4f8ebba65d138bfd4f2aca9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="5e180-103">Esercitazione: Configurazione di Samanage per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="5e180-103">Tutorial: Configuring Samanage for Automatic User Provisioning</span></span>


<span data-ttu-id="5e180-104">obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in Samanage e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="5e180-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Samanage and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSamanage.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5e180-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5e180-105">Prerequisites</span></span>

<span data-ttu-id="5e180-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5e180-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="5e180-107">Tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e180-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="5e180-108">Un tenant di Samanage con hello [piano Professional](https://www.samanage.com/pricing/) o meglio abilitato</span><span class="sxs-lookup"><span data-stu-id="5e180-108">A Samanage tenant with hello [Professional plan](https://www.samanage.com/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="5e180-109">Account utente in Samanage con autorizzazioni di amministratore</span><span class="sxs-lookup"><span data-stu-id="5e180-109">A user account in Samanage with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="5e180-110">Hello provisioning integrazione di Azure AD si basa su hello [API REST di Samanage](https://www.samanage.com/api/), ovvero team tooSamanage disponibile sulla hello Professional pianificare o, meglio.</span><span class="sxs-lookup"><span data-stu-id="5e180-110">hello Azure AD provisioning integration relies on hello [Samanage REST API](https://www.samanage.com/api/), which is available tooSamanage teams on hello Professional plan or better.</span></span>

## <a name="assigning-users-toosamanage"></a><span data-ttu-id="5e180-111">L'assegnazione di utenti tooSamanage</span><span class="sxs-lookup"><span data-stu-id="5e180-111">Assigning users tooSamanage</span></span>

<span data-ttu-id="5e180-112">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="5e180-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="5e180-113">Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="5e180-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="5e180-114">Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour Samanage app.</span><span class="sxs-lookup"><span data-stu-id="5e180-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Samanage app.</span></span> <span data-ttu-id="5e180-115">Una volta deciso, è possibile assegnare queste app di Samanage tooyour utenti seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="5e180-115">Once decided, you can assign these users tooyour Samanage app by following hello instructions here:</span></span>

[<span data-ttu-id="5e180-116">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="5e180-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toosamanage"></a><span data-ttu-id="5e180-117">Suggerimenti importanti per l'assegnazione di utenti tooSamanage</span><span class="sxs-lookup"><span data-stu-id="5e180-117">Important tips for assigning users tooSamanage</span></span>

*   <span data-ttu-id="5e180-118">È consigliabile che un singolo utente AD Azure viene assegnato hello tootest tooSamanage configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="5e180-118">It is recommended that a single Azure AD user is assigned tooSamanage tootest hello provisioning configuration.</span></span> <span data-ttu-id="5e180-119">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="5e180-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="5e180-120">Quando si assegna un tooSamanage utente, è necessario selezionare entrambi hello **utente** ruolo, o un altro valido specifici dell'applicazione, se disponibile, nella finestra di dialogo assegnazione hello.</span><span class="sxs-lookup"><span data-stu-id="5e180-120">When assigning a user tooSamanage, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="5e180-121">Hello **accesso predefinito** ruolo non funziona per il provisioning e gli utenti vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="5e180-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="5e180-122">Come funzionalità di aggiunta, hello provisioning servizio legge eventuali ruoli personalizzati definiti in Samanage e le Importa in Azure Active Directory in cui può essere selezionati nella finestra di dialogo selezionare il ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="5e180-122">As an added feature, hello provisioning service reads any custom roles defined in Samanage, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="5e180-123">Questi ruoli saranno visibili nel portale di Azure hello dopo hello provisioning del servizio è abilitata e un ciclo di sincronizzazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="5e180-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toosamanage"></a><span data-ttu-id="5e180-124">Configurazione tooSamanage di provisioning dell'utente</span><span class="sxs-lookup"><span data-stu-id="5e180-124">Configuring user provisioning tooSamanage</span></span> 

<span data-ttu-id="5e180-125">Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooSamanage il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in Samanage in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e180-125">This section guides you through connecting your Azure AD tooSamanage's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Samanage based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="5e180-126">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Samanage, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5e180-126">You may also choose tooenabled SAML-based Single Sign-On for Samanage, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5e180-127">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="5e180-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toosamanage-in-azure-ad"></a><span data-ttu-id="5e180-128">Configurare l'account utente automatico provisioning tooSamanage in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="5e180-128">Configure automatic user account provisioning tooSamanage in Azure AD:</span></span>


1. <span data-ttu-id="5e180-129">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="5e180-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="5e180-130">Se è già stato configurato Samanage per single sign-on, eseguire la ricerca per l'istanza di Samanage usando il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="5e180-130">If you have already configured Samanage for single sign-on, search for your instance of Samanage using hello search field.</span></span> <span data-ttu-id="5e180-131">In caso contrario, selezionare **Aggiungi** e cercare **Samanage** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5e180-131">Otherwise, select **Add** and search for **Samanage** in hello application gallery.</span></span> <span data-ttu-id="5e180-132">Selezionare Samanage dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5e180-132">Select Samanage from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="5e180-133">Selezionare l'istanza di Samanage, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="5e180-133">Select your instance of Samanage, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="5e180-134">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="5e180-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Provisioning di Samanage](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. <span data-ttu-id="5e180-136">In hello **credenziali di amministratore** sezione, hello input **Admin Username e Password amministratore** dell'account di Samanage.</span><span class="sxs-lookup"><span data-stu-id="5e180-136">Under hello **Admin Credentials** section, input hello **Admin Username&Admin Password** of your Samanage's account.</span></span> 

6. <span data-ttu-id="5e180-137">Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour Samanage app.</span><span class="sxs-lookup"><span data-stu-id="5e180-137">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Samanage app.</span></span> <span data-ttu-id="5e180-138">Se hello connessione non riesce, verificare che l'account di Samanage disponga delle autorizzazioni di amministratore e riprovare a eseguire il passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="5e180-138">If hello connection fails, ensure your Samanage account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="5e180-139">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e controllo hello casella di controllo "Invia una notifica di posta elettronica quando si verifica un errore".</span><span class="sxs-lookup"><span data-stu-id="5e180-139">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="5e180-140">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5e180-140">Click **Save**.</span></span> 

9. <span data-ttu-id="5e180-141">Nella sezione mapping hello, selezionare **tooSamanage sincronizzare Active Directory gli utenti di Azure**.</span><span class="sxs-lookup"><span data-stu-id="5e180-141">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSamanage**.</span></span>

10. <span data-ttu-id="5e180-142">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooSamanage di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e180-142">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSamanage.</span></span> <span data-ttu-id="5e180-143">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in Samanage per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="5e180-143">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Samanage for update operations.</span></span> <span data-ttu-id="5e180-144">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="5e180-144">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="5e180-145">tooenable hello servizio provisioning di Azure AD per Samanage, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione</span><span class="sxs-lookup"><span data-stu-id="5e180-145">tooenable hello Azure AD provisioning service for Samanage, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="5e180-146">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5e180-146">Click **Save**.</span></span> 

<span data-ttu-id="5e180-147">Questa operazione avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooSamanage in hello gli utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="5e180-147">This operation starts hello initial synchronization of any users and/or groups assigned tooSamanage in hello Users and Groups section.</span></span> <span data-ttu-id="5e180-148">la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5e180-148">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="5e180-149">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio.</span><span class="sxs-lookup"><span data-stu-id="5e180-149">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="5e180-150">Per ulteriori informazioni sulla modalità di registrazione tooread provisioning di hello Azure AD, vedere [creazione di report per il provisioning utente automatico account](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="5e180-150">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5e180-151">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5e180-151">Additional resources</span></span>

* [<span data-ttu-id="5e180-152">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="5e180-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="5e180-153">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e180-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="5e180-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5e180-154">Next steps</span></span>

* [<span data-ttu-id="5e180-155">Informazioni su modalità di registrazione tooreview e ottengono report sull'attività di provisioning</span><span class="sxs-lookup"><span data-stu-id="5e180-155">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
