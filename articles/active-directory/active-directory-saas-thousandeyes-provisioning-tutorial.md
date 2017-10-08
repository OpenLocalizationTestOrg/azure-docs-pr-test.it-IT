---
title: 'Esercitazione: Configurazione di ThousandEyes per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come tooconfigure Azure Active Directory tooautomatically il provisioning e il de-provisioning account utente di tooThousandEyes.
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
ms.openlocfilehash: f31883ab685d0ffcd9a830aa4a7d43c056f5f4cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="9070f-103">Esercitazione: Configurazione di ThousandEyes per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="9070f-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="9070f-104">obiettivo di Hello di questa esercitazione è tooshow che Hello passaggi è necessario tooperform riserva tooautomatically ThousandEyes e Azure AD e il deprovisioning degli account utente da Azure AD tooThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="9070f-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ThousandEyes and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9070f-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9070f-105">Prerequisites</span></span>

<span data-ttu-id="9070f-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="9070f-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="9070f-107">Tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9070f-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="9070f-108">Un tenant di ThousandEyes con hello [piano Standard](https://www.thousandeyes.com/pricing) o meglio abilitato</span><span class="sxs-lookup"><span data-stu-id="9070f-108">A ThousandEyes tenant with hello [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="9070f-109">Un account utente in ThousandEyes con autorizzazioni di amministratore</span><span class="sxs-lookup"><span data-stu-id="9070f-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="9070f-110">Hello provisioning integrazione di Azure AD si basa su hello [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), ovvero i team tooThousandEyes disponibili nel piano Standard hello o migliori.</span><span class="sxs-lookup"><span data-stu-id="9070f-110">hello Azure AD provisioning integration relies on hello [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available tooThousandEyes teams on hello Standard plan or better.</span></span>

## <a name="assigning-users-toothousandeyes"></a><span data-ttu-id="9070f-111">L'assegnazione di utenti tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="9070f-111">Assigning users tooThousandEyes</span></span>

<span data-ttu-id="9070f-112">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="9070f-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="9070f-113">Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="9070f-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="9070f-114">Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano hello utenti devono accedere tooyour ThousandEyes app.</span><span class="sxs-lookup"><span data-stu-id="9070f-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ThousandEyes app.</span></span> <span data-ttu-id="9070f-115">Una volta deciso, è possibile assegnare queste app di ThousandEyes tooyour utenti seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="9070f-115">Once decided, you can assign these users tooyour ThousandEyes app by following hello instructions here:</span></span>

[<span data-ttu-id="9070f-116">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="9070f-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toothousandeyes"></a><span data-ttu-id="9070f-117">Suggerimenti importanti per l'assegnazione di utenti tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="9070f-117">Important tips for assigning users tooThousandEyes</span></span>

*   <span data-ttu-id="9070f-118">È consigliabile che un singolo utente AD Azure viene assegnato hello tootest tooThousandEyes configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="9070f-118">It is recommended that a single Azure AD user is assigned tooThousandEyes tootest hello provisioning configuration.</span></span> <span data-ttu-id="9070f-119">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="9070f-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="9070f-120">Quando si assegna un tooThousandEyes utente, è necessario selezionare entrambi hello **utente** ruolo, o un altro valido specifici dell'applicazione, se disponibile, nella finestra di dialogo assegnazione hello.</span><span class="sxs-lookup"><span data-stu-id="9070f-120">When assigning a user tooThousandEyes, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="9070f-121">Hello **accesso predefinito** ruolo non funziona per il provisioning e gli utenti vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="9070f-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toothousandeyes"></a><span data-ttu-id="9070f-122">Configurazione tooThousandEyes di provisioning dell'utente</span><span class="sxs-lookup"><span data-stu-id="9070f-122">Configuring user provisioning tooThousandEyes</span></span> 

<span data-ttu-id="9070f-123">Questa sezione viene illustrato come tramite la connessione API di provisioning dell'account utente del tooThousandEyes il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare gli account utente assegnato in base all'assegnazione di utenti e gruppi in ThousandEyes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9070f-123">This section guides you through connecting your Azure AD tooThousandEyes's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="9070f-124">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per ThousandEyes, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9070f-124">You may also choose tooenabled SAML-based Single Sign-On for ThousandEyes, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9070f-125">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="9070f-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toothousandeyes-in-azure-ad"></a><span data-ttu-id="9070f-126">Configurare l'account utente automatico provisioning tooThousandEyes in Azure AD</span><span class="sxs-lookup"><span data-stu-id="9070f-126">Configure automatic user account provisioning tooThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="9070f-127">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="9070f-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="9070f-128">Se è già stato configurato ThousandEyes per single sign-on, eseguire la ricerca per l'istanza di ThousandEyes usando il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="9070f-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using hello search field.</span></span> <span data-ttu-id="9070f-129">In caso contrario, selezionare **Aggiungi** e cercare **ThousandEyes** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9070f-129">Otherwise, select **Add** and search for **ThousandEyes** in hello application gallery.</span></span> <span data-ttu-id="9070f-130">Selezionare ThousandEyes dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="9070f-130">Select ThousandEyes from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="9070f-131">Selezionare l'istanza di ThousandEyes, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="9070f-131">Select your instance of ThousandEyes, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="9070f-132">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="9070f-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Provisioning di ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="9070f-134">In hello **credenziali di amministratore** sezione, hello input **segreto Token** generato dall'account di ThousandEyes (è possibile trovare il token hello con l'account di ThousandEyes: **sicurezza & Autenticazione**).</span><span class="sxs-lookup"><span data-stu-id="9070f-134">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your ThousandEyes's account (you can find hello token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![Provisioning di ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="9070f-136">Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour ThousandEyes app.</span><span class="sxs-lookup"><span data-stu-id="9070f-136">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ThousandEyes app.</span></span> <span data-ttu-id="9070f-137">Se hello connessione non riesce, verificare che l'account di ThousandEyes disponga delle autorizzazioni di amministratore e riprovare a eseguire il passaggio 5.</span><span class="sxs-lookup"><span data-stu-id="9070f-137">If hello connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="9070f-138">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e controllo hello casella di controllo "Invia una notifica di posta elettronica quando si verifica un errore".</span><span class="sxs-lookup"><span data-stu-id="9070f-138">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="9070f-139">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9070f-139">Click **Save**.</span></span> 

9. <span data-ttu-id="9070f-140">Nella sezione mapping hello, selezionare **tooThousandEyes sincronizzare Active Directory gli utenti di Azure**.</span><span class="sxs-lookup"><span data-stu-id="9070f-140">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooThousandEyes**.</span></span>

10. <span data-ttu-id="9070f-141">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da tooThousandEyes di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9070f-141">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooThousandEyes.</span></span> <span data-ttu-id="9070f-142">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in ThousandEyes per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="9070f-142">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="9070f-143">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="9070f-143">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="9070f-144">tooenable hello servizio provisioning di Azure AD per ThousandEyes, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione</span><span class="sxs-lookup"><span data-stu-id="9070f-144">tooenable hello Azure AD provisioning service for ThousandEyes, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="9070f-145">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9070f-145">Click **Save**.</span></span> 

<span data-ttu-id="9070f-146">Questa operazione avvia la sincronizzazione iniziale di hello di eventuali utenti o gruppi assegnati tooThousandEyes in hello gli utenti e gruppi.</span><span class="sxs-lookup"><span data-stu-id="9070f-146">This operation starts hello initial synchronization of any users and/or groups assigned tooThousandEyes in hello Users and Groups section.</span></span> <span data-ttu-id="9070f-147">la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9070f-147">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="9070f-148">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio.</span><span class="sxs-lookup"><span data-stu-id="9070f-148">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="9070f-149">Per ulteriori informazioni sulla modalità di registrazione tooread provisioning di hello Azure AD, vedere [creazione di report per il provisioning utente automatico account](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="9070f-149">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9070f-150">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9070f-150">Additional resources</span></span>

* [<span data-ttu-id="9070f-151">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="9070f-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="9070f-152">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9070f-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="9070f-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9070f-153">Next steps</span></span>

* [<span data-ttu-id="9070f-154">Informazioni su modalità di registrazione tooreview e ottengono report sull'attività di provisioning</span><span class="sxs-lookup"><span data-stu-id="9070f-154">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
