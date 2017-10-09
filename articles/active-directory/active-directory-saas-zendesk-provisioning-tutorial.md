---
title: 'Esercitazione: Configurazione di ZenDesk per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come tooconfigure Azure Active Directory tooautomatically il provisioning e il de-provisioning account utente di tooZenDesk.
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
ms.openlocfilehash: 200e8790ec1755f5cf927274ceb38527dd993f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a><span data-ttu-id="e9587-103">Esercitazione: Configurazione di ZenDesk per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="e9587-103">Tutorial: Configuring ZenDesk for Automatic User Provisioning</span></span>


<span data-ttu-id="e9587-104">obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in ZenDesk e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooZenDesk.</span><span class="sxs-lookup"><span data-stu-id="e9587-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ZenDesk and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooZenDesk.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e9587-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e9587-105">Prerequisites</span></span>

<span data-ttu-id="e9587-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="e9587-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="e9587-107">Tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9587-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="e9587-108">Un tenant di ZenDesk con hello [piano Enterprise](https://www.zendesk.com/product/pricing/) o meglio abilitato</span><span class="sxs-lookup"><span data-stu-id="e9587-108">A ZenDesk tenant with hello [Enterprise plan](https://www.zendesk.com/product/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="e9587-109">Account utente in ZenDesk con autorizzazioni di amministratore</span><span class="sxs-lookup"><span data-stu-id="e9587-109">A user account in ZenDesk with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="e9587-110">Hello provisioning integrazione di Azure AD si basa su hello [API REST di ZenDesk](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), ovvero i team tooZenDesk disponibili nel piano essenziali hello o migliori.</span><span class="sxs-lookup"><span data-stu-id="e9587-110">hello Azure AD provisioning integration relies on hello [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), which is available tooZenDesk teams on hello Essential plan or better.</span></span>

## <a name="assigning-users-toozendesk"></a><span data-ttu-id="e9587-111">L'assegnazione di utenti tooZenDesk</span><span class="sxs-lookup"><span data-stu-id="e9587-111">Assigning users tooZenDesk</span></span>

<span data-ttu-id="e9587-112">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="e9587-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="e9587-113">Nel contesto di hello di provisioning dell'account utente automatico, vengono sincronizzati solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9587-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="e9587-114">Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere app ZenDesk tooyour.</span><span class="sxs-lookup"><span data-stu-id="e9587-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ZenDesk app.</span></span> <span data-ttu-id="e9587-115">Una volta deciso, è possibile assegnare queste app di ZenDesk tooyour utenti seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="e9587-115">Once decided, you can assign these users tooyour ZenDesk app by following hello instructions here:</span></span>

[<span data-ttu-id="e9587-116">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="e9587-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toozendesk"></a><span data-ttu-id="e9587-117">Suggerimenti importanti per l'assegnazione di utenti tooZenDesk</span><span class="sxs-lookup"><span data-stu-id="e9587-117">Important tips for assigning users tooZenDesk</span></span>

*   <span data-ttu-id="e9587-118">È consigliabile che un singolo utente AD Azure viene assegnato hello tootest tooZenDesk configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="e9587-118">It is recommended that a single Azure AD user is assigned tooZenDesk tootest hello provisioning configuration.</span></span> <span data-ttu-id="e9587-119">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="e9587-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="e9587-120">Quando si assegna un tooZenDesk utente, è necessario selezionare entrambi hello **utente** ruolo, o un altro valido specifici dell'applicazione, se disponibile, nella finestra di dialogo assegnazione hello.</span><span class="sxs-lookup"><span data-stu-id="e9587-120">When assigning a user tooZenDesk, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="e9587-121">Hello **accesso predefinito** ruolo non funziona per il provisioning e gli utenti vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="e9587-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="e9587-122">Come funzionalità di aggiunta, hello provisioning servizio legge eventuali ruoli personalizzati definiti in Zendesk e le Importa in Azure Active Directory in cui può essere selezionati nella finestra di dialogo selezionare il ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="e9587-122">As an added feature, hello provisioning service reads any custom roles defined in Zendesk, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="e9587-123">Questi ruoli saranno visibili nel portale di Azure hello dopo hello provisioning del servizio è abilitata e un ciclo di sincronizzazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="e9587-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toozendesk"></a><span data-ttu-id="e9587-124">Configurazione tooZenDesk di provisioning dell'utente</span><span class="sxs-lookup"><span data-stu-id="e9587-124">Configuring user provisioning tooZenDesk</span></span> 

<span data-ttu-id="e9587-125">Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooZenDesk il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in ZenDesk in base all'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9587-125">This section guides you through connecting your Azure AD tooZenDesk's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ZenDesk based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="e9587-126">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per ZenDesk, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e9587-126">You may also choose tooenabled SAML-based Single Sign-On for ZenDesk, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e9587-127">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="e9587-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toozendesk-in-azure-ad"></a><span data-ttu-id="e9587-128">Configurare l'account utente automatico provisioning tooZenDesk in Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9587-128">Configure automatic user account provisioning tooZenDesk in Azure AD</span></span>


1. <span data-ttu-id="e9587-129">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="e9587-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="e9587-130">Se è già stato configurato ZenDesk per single sign-on, eseguire la ricerca per l'istanza di ZenDesk con il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="e9587-130">If you have already configured ZenDesk for single sign-on, search for your instance of ZenDesk using hello search field.</span></span> <span data-ttu-id="e9587-131">In caso contrario, selezionare **Aggiungi** e cercare **ZenDesk** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e9587-131">Otherwise, select **Add** and search for **ZenDesk** in hello application gallery.</span></span> <span data-ttu-id="e9587-132">Selezionare ZenDesk dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e9587-132">Select ZenDesk from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="e9587-133">Selezionare l'istanza di ZenDesk, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="e9587-133">Select your instance of ZenDesk, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="e9587-134">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="e9587-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Provisioning di ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. <span data-ttu-id="e9587-136">In hello **credenziali di amministratore** sezione, hello input **Admin Username & tokenkey & dominio** generato dall'account di ZenDesk (è possibile trovare il token hello con l'account: **Admin**   >  **API** > **impostazioni**).</span><span class="sxs-lookup"><span data-stu-id="e9587-136">Under hello **Admin Credentials** section, input hello **Admin Username&tokenkey&Domain** generated by your ZenDesk's account (you can find hello token under your account: **Admin** > **API** > **Settings**).</span></span> 

    ![Provisioning di ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. <span data-ttu-id="e9587-138">Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi app ZenDesk tooyour.</span><span class="sxs-lookup"><span data-stu-id="e9587-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ZenDesk app.</span></span> <span data-ttu-id="e9587-139">Se hello connessione non riesce, verificare che l'account ZenDesk disponga delle autorizzazioni di amministratore e riprovare a eseguire il passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="e9587-139">If hello connection fails, ensure your ZenDesk account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="e9587-140">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e controllo hello casella di controllo "Invia una notifica di posta elettronica quando si verifica un errore".</span><span class="sxs-lookup"><span data-stu-id="e9587-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="e9587-141">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e9587-141">Click **Save**.</span></span> 

9. <span data-ttu-id="e9587-142">Nella sezione mapping hello, selezionare **tooZenDesk sincronizzare Active Directory gli utenti di Azure**.</span><span class="sxs-lookup"><span data-stu-id="e9587-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooZenDesk**.</span></span>

10. <span data-ttu-id="e9587-143">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooZenDesk di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9587-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooZenDesk.</span></span> <span data-ttu-id="e9587-144">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in ZenDesk per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="e9587-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ZenDesk for update operations.</span></span> <span data-ttu-id="e9587-145">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="e9587-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="e9587-146">tooenable hello servizio provisioning di Azure AD per ZenDesk, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione</span><span class="sxs-lookup"><span data-stu-id="e9587-146">tooenable hello Azure AD provisioning service for ZenDesk, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="e9587-147">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e9587-147">Click **Save**.</span></span> 

<span data-ttu-id="e9587-148">Questa operazione avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooZenDesk in hello gli utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="e9587-148">This operation starts hello initial synchronization of any users and/or groups assigned tooZenDesk in hello Users and Groups section.</span></span> <span data-ttu-id="e9587-149">la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e9587-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="e9587-150">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio.</span><span class="sxs-lookup"><span data-stu-id="e9587-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="e9587-151">Per ulteriori informazioni sulla modalità di registrazione tooread provisioning di hello Azure AD, vedere [creazione di report per il provisioning utente automatico account](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="e9587-151">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e9587-152">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e9587-152">Additional resources</span></span>

* [<span data-ttu-id="e9587-153">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="e9587-153">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="e9587-154">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9587-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="e9587-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e9587-155">Next steps</span></span>

* [<span data-ttu-id="e9587-156">Informazioni su modalità di registrazione tooreview e ottengono report sull'attività di provisioning</span><span class="sxs-lookup"><span data-stu-id="e9587-156">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
