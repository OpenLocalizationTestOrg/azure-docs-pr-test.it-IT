---
title: 'Esercitazione: Configurazione di LucidChart per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come tooconfigure Azure Active Directory tooautomatically il provisioning e il de-provisioning account utente di tooLucidChart.
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
ms.openlocfilehash: d3af45141731215f2edc8942ad21b016468c1e38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="ef612-103">Esercitazione: Configurazione di LucidChart per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="ef612-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="ef612-104">obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in LucidChart e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooLucidChart.</span><span class="sxs-lookup"><span data-stu-id="ef612-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LucidChart and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ef612-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ef612-105">Prerequisites</span></span>

<span data-ttu-id="ef612-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ef612-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="ef612-107">Tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef612-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="ef612-108">Un tenant di LucidChart con hello [piano Enterprise](https://www.lucidchart.com/user/117598685#/subscriptionLevel) o meglio abilitato</span><span class="sxs-lookup"><span data-stu-id="ef612-108">A LucidChart tenant with hello [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="ef612-109">Un account utente in LucidChart con autorizzazioni di amministratore</span><span class="sxs-lookup"><span data-stu-id="ef612-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-toolucidchart"></a><span data-ttu-id="ef612-110">L'assegnazione di utenti tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="ef612-110">Assigning users tooLucidChart</span></span>

<span data-ttu-id="ef612-111">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="ef612-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="ef612-112">Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="ef612-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="ef612-113">Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour LucidChart app.</span><span class="sxs-lookup"><span data-stu-id="ef612-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour LucidChart app.</span></span> <span data-ttu-id="ef612-114">Una volta deciso, è possibile assegnare queste app di LucidChart tooyour utenti seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="ef612-114">Once decided, you can assign these users tooyour LucidChart app by following hello instructions here:</span></span>

[<span data-ttu-id="ef612-115">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="ef612-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolucidchart"></a><span data-ttu-id="ef612-116">Suggerimenti importanti per l'assegnazione di utenti tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="ef612-116">Important tips for assigning users tooLucidChart</span></span>

*   <span data-ttu-id="ef612-117">È consigliabile che un singolo utente AD Azure viene assegnato hello tootest tooLucidChart configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="ef612-117">It is recommended that a single Azure AD user is assigned tooLucidChart tootest hello provisioning configuration.</span></span> <span data-ttu-id="ef612-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="ef612-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="ef612-119">Quando si assegna un tooLucidChart utente, è necessario selezionare entrambi hello **utente** ruolo, o un altro valido specifici dell'applicazione, se disponibile, nella finestra di dialogo assegnazione hello.</span><span class="sxs-lookup"><span data-stu-id="ef612-119">When assigning a user tooLucidChart, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="ef612-120">Hello **accesso predefinito** ruolo non funziona per il provisioning e gli utenti vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="ef612-120">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toolucidchart"></a><span data-ttu-id="ef612-121">Configurazione tooLucidChart di provisioning dell'utente</span><span class="sxs-lookup"><span data-stu-id="ef612-121">Configuring user provisioning tooLucidChart</span></span> 

<span data-ttu-id="ef612-122">Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account del tooLucidChart di Azure AD utente e la configurazione di provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in LucidChart in base all'assegnazione di utenti e gruppi in Azure AD .</span><span class="sxs-lookup"><span data-stu-id="ef612-122">This section guides you through connecting your Azure AD tooLucidChart's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="ef612-123">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per LucidChart, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ef612-123">You may also choose tooenabled SAML-based Single Sign-On for LucidChart, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ef612-124">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="ef612-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toolucidchart-in-azure-ad"></a><span data-ttu-id="ef612-125">Configurare l'account utente automatico provisioning tooLucidChart in Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef612-125">Configure automatic user account provisioning tooLucidChart in Azure AD</span></span>


1. <span data-ttu-id="ef612-126">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="ef612-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="ef612-127">Se è già stato configurato LucidChart per single sign-on, eseguire la ricerca per l'istanza di LucidChart mediante il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="ef612-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using hello search field.</span></span> <span data-ttu-id="ef612-128">In caso contrario, selezionare **Aggiungi** e cercare **LucidChart** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ef612-128">Otherwise, select **Add** and search for **LucidChart** in hello application gallery.</span></span> <span data-ttu-id="ef612-129">Selezionare LucidChart dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ef612-129">Select LucidChart from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="ef612-130">Selezionare l'istanza di LucidChart, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="ef612-130">Select your instance of LucidChart, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="ef612-131">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="ef612-131">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Provisioning di LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="ef612-133">In hello **credenziali di amministratore** sezione, hello input **segreto Token** generato dall'account del LucidChart (è possibile trovare il token hello con l'account: **Team**  >  **Integrazione dell'applicazione** > **SCIM**).</span><span class="sxs-lookup"><span data-stu-id="ef612-133">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your LucidChart's account (you can find hello token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![Provisioning di LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="ef612-135">Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour LucidChart app.</span><span class="sxs-lookup"><span data-stu-id="ef612-135">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour LucidChart app.</span></span> <span data-ttu-id="ef612-136">Se hello connessione non riesce, verificare che l'account LucidChart disponga delle autorizzazioni di amministratore e riprovare a eseguire il passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="ef612-136">If hello connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="ef612-137">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e controllo hello casella di controllo "Invia una notifica di posta elettronica quando si verifica un errore".</span><span class="sxs-lookup"><span data-stu-id="ef612-137">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="ef612-138">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ef612-138">Click **Save**.</span></span> 

9. <span data-ttu-id="ef612-139">Nella sezione mapping hello, selezionare **tooLucidChart sincronizzare Active Directory gli utenti di Azure**.</span><span class="sxs-lookup"><span data-stu-id="ef612-139">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooLucidChart**.</span></span>

10. <span data-ttu-id="ef612-140">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooLucidChart di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef612-140">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooLucidChart.</span></span> <span data-ttu-id="ef612-141">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in LucidChart per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ef612-141">hello attributes selected as **Matching** properties are used toomatch hello user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="ef612-142">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="ef612-142">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="ef612-143">tooenable hello servizio provisioning di Azure AD per LucidChart, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione</span><span class="sxs-lookup"><span data-stu-id="ef612-143">tooenable hello Azure AD provisioning service for LucidChart, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="ef612-144">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ef612-144">Click **Save**.</span></span> 

<span data-ttu-id="ef612-145">Questa operazione avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooLucidChart in hello gli utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="ef612-145">This operation starts hello initial synchronization of any users and/or groups assigned tooLucidChart in hello Users and Groups section.</span></span> <span data-ttu-id="ef612-146">la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ef612-146">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="ef612-147">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio.</span><span class="sxs-lookup"><span data-stu-id="ef612-147">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="ef612-148">Per ulteriori informazioni sulla modalità di registrazione tooread provisioning di hello Azure AD, vedere [creazione di report per il provisioning utente automatico account](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="ef612-148">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ef612-149">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ef612-149">Additional resources</span></span>

* [<span data-ttu-id="ef612-150">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="ef612-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="ef612-151">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef612-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="ef612-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ef612-152">Next steps</span></span>

* [<span data-ttu-id="ef612-153">Informazioni su modalità di registrazione tooreview e ottengono report sull'attività di provisioning</span><span class="sxs-lookup"><span data-stu-id="ef612-153">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
