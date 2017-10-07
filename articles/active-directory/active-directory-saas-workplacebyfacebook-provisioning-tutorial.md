---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workplace by Facebook | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e all'area di lavoro da Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="35f88-103">Esercitazione: Configurazione di Workplace by Facebook per il Provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="35f88-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="35f88-104">obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform nell'area di lavoro da Facebook e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooWorkplace da Facebook.</span><span class="sxs-lookup"><span data-stu-id="35f88-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Workplace by Facebook and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35f88-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="35f88-105">Prerequisites</span></span>

<span data-ttu-id="35f88-106">integrazione di Azure AD con area di lavoro da Facebook tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="35f88-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="35f88-107">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35f88-107">An Azure AD subscription</span></span>
- <span data-ttu-id="35f88-108">Una sottoscrizione di Workplace by Facebook abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="35f88-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="35f88-109">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="35f88-109">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="35f88-110">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="35f88-110">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="35f88-111">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="35f88-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="35f88-112">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35f88-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="35f88-113">L'assegnazione di utenti tooWorkplace da Facebook</span><span class="sxs-lookup"><span data-stu-id="35f88-113">Assigning users tooWorkplace by Facebook</span></span>

<span data-ttu-id="35f88-114">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="35f88-114">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="35f88-115">Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="35f88-115">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="35f88-116">Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano utenti hello bisogno di accesso tooyour all'area di lavoro da app Facebook.</span><span class="sxs-lookup"><span data-stu-id="35f88-116">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="35f88-117">Una volta deciso, è possibile assegnare questi utenti tooyour all'area di lavoro, da app Facebook seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="35f88-117">Once decided, you can assign these users tooyour Workplace by Facebook app by following hello instructions here:</span></span>

[<span data-ttu-id="35f88-118">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="35f88-118">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="35f88-119">Suggerimenti importanti per l'assegnazione di utenti tooWorkplace da Facebook</span><span class="sxs-lookup"><span data-stu-id="35f88-119">Important tips for assigning users tooWorkplace by Facebook</span></span>

*   <span data-ttu-id="35f88-120">È consigliabile che un singolo utente di Azure Active Directory assegnato da Facebook tootest hello configurazione provisioning tooWorkplace.</span><span class="sxs-lookup"><span data-stu-id="35f88-120">It is recommended that a single Azure AD user is assigned tooWorkplace by Facebook tootest hello provisioning configuration.</span></span> <span data-ttu-id="35f88-121">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="35f88-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="35f88-122">Quando si assegna un utente tooWorkplace da Facebook, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="35f88-122">When assigning a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="35f88-123">ruolo di "accesso predefinita" Hello non funziona per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="35f88-123">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="35f88-124">Abilitare il provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="35f88-124">Enable User Provisioning</span></span>

<span data-ttu-id="35f88-125">Questa sezione viene illustrato come tramite connessione il tooWorkplace di Azure AD tramite API di provisioning dell'account utente Facebook e hello provisioning toocreate servizio di configurazione, aggiornare e disabilitare gli account utente assegnato nell'area di lavoro da Facebook in base a utenti e gruppi assegnazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35f88-125">This section guides you through connecting your Azure AD tooWorkplace by Facebook's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="35f88-126">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per l'area di lavoro da Facebook, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="35f88-126">You may also choose tooenabled SAML-based Single Sign-On for Workplace by Facebook, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="35f88-127">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="35f88-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="35f88-128">account utente tooconfigure provisioning tooWorkplace da Facebook in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="35f88-128">tooconfigure user account provisioning tooWorkplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="35f88-129">obiettivo di Hello di questa sezione è toooutline tooenable provisioning dell'utente di Active Directory come account di tooWorkplace da Facebook.</span><span class="sxs-lookup"><span data-stu-id="35f88-129">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooWorkplace by Facebook.</span></span>

<span data-ttu-id="35f88-130">Azure supporta AD hello possibilità tooautomatically sincronizzare i dettagli dell'account di hello assegnato tooWorkplace utenti da Facebook.</span><span class="sxs-lookup"><span data-stu-id="35f88-130">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="35f88-131">La sincronizzazione automatica consente all'area di lavoro da dati di Facebook hello tooget tooauthorize utenti per l'accesso, è necessario prima di usarle il tentativo di toosign in hello per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="35f88-131">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="35f88-132">Esegue anche il deprovisioning degli utenti da Workplace by Facebook una volta che l'accesso viene revocato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35f88-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="35f88-133">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory** > **le app aziendali** > **tutteleapplicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="35f88-133">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="35f88-134">Se è già stato configurato all'area di lavoro da Facebook per single sign-on, eseguire la ricerca per l'istanza di una rete aziendale da Facebook tramite il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="35f88-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using hello search field.</span></span> <span data-ttu-id="35f88-135">In caso contrario, selezionare **Aggiungi** e cercare **all'area di lavoro da Facebook** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="35f88-135">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="35f88-136">Selezionare l'area di lavoro da Facebook dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="35f88-136">Select Workplace by Facebook from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="35f88-137">Selezionare l'istanza di una rete aziendale da Facebook, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="35f88-137">Select your instance of Workplace by Facebook, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="35f88-138">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="35f88-138">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![provisioning](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="35f88-140">In hello **credenziali di amministratore** sezione, immettere il Token segreto hello e hello URL Tenant dell'area di lavoro dall'amministratore di Facebook.</span><span class="sxs-lookup"><span data-stu-id="35f88-140">Under hello **Admin Credentials** section, enter hello Secret Token and hello Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="35f88-141">Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour all'area di lavoro da app Facebook.</span><span class="sxs-lookup"><span data-stu-id="35f88-141">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="35f88-142">Se hello connessione non riesce, verificare il che area di lavoro dall'account di Facebook con autorizzazioni di amministratore di Team.</span><span class="sxs-lookup"><span data-stu-id="35f88-142">If hello connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="35f88-143">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="35f88-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="35f88-144">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="35f88-144">Click **Save.**</span></span>

9. <span data-ttu-id="35f88-145">Nella sezione mapping hello, selezionare **tooWorkplace sincronizzare Active Directory gli utenti di Azure da Facebook.**</span><span class="sxs-lookup"><span data-stu-id="35f88-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook.**</span></span>

10. <span data-ttu-id="35f88-146">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da Azure AD tooWorkplace da Facebook.</span><span class="sxs-lookup"><span data-stu-id="35f88-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="35f88-147">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello account utente nell'area di lavoro da Facebook per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="35f88-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="35f88-148">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="35f88-148">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="35f88-149">tooenable hello servizio provisioning di Azure AD per l'area di lavoro da Facebook, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione</span><span class="sxs-lookup"><span data-stu-id="35f88-149">tooenable hello Azure AD provisioning service for Workplace by Facebook, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="35f88-150">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="35f88-150">Click **Save.**</span></span>

<span data-ttu-id="35f88-151">Per ulteriori informazioni su come il provisioning, vedere tooconfigure automatico [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="35f88-151">For more information on how tooconfigure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="35f88-152">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="35f88-152">You can now create a test account.</span></span> <span data-ttu-id="35f88-153">Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooWorkplace da Facebook.</span><span class="sxs-lookup"><span data-stu-id="35f88-153">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="35f88-154">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="35f88-154">Additional resources</span></span>

* [<span data-ttu-id="35f88-155">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="35f88-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35f88-156">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35f88-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="35f88-157">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="35f88-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

