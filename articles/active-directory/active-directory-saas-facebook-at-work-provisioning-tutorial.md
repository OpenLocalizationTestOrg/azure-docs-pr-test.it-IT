---
title: 'Esercitazione: Configurare Workplace by Facebook per il provisioning degli utenti | Microsoft Docs'
description: Informazioni su come degli account utente di effettuare il provisioning e la prestazione tooautomatically da Azure AD tooWorkplace da Facebook.
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="c6f44-103">Esercitazione: Configurare Workplace by Facebook per il provisioning degli utenti</span><span class="sxs-lookup"><span data-stu-id="c6f44-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="c6f44-104">Questa esercitazione si hello tooautomatically necessari passaggi è illustrato il provisioning e deprovisioning degli account utente da Azure Active Directory (Azure AD) tooWorkplace da Facebook.</span><span class="sxs-lookup"><span data-stu-id="c6f44-104">This tutorial shows you hello steps necessary tooautomatically provision and de-provision user accounts from Azure Active Directory (Azure AD) tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6f44-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c6f44-105">Prerequisites</span></span>

<span data-ttu-id="c6f44-106">integrazione di Azure AD con area di lavoro da Facebook tooconfigure, è necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c6f44-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following:</span></span>

- <span data-ttu-id="c6f44-107">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6f44-107">An Azure AD subscription</span></span>
- <span data-ttu-id="c6f44-108">Una sottoscrizione a Workplace by Facebook abilitata per l'accesso Single Sign-On (SSO)</span><span class="sxs-lookup"><span data-stu-id="c6f44-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="c6f44-109">passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:</span><span class="sxs-lookup"><span data-stu-id="c6f44-109">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="c6f44-110">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="c6f44-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c6f44-111">Se non si dispone di un ambiente di valutazione di Azure AD, è possibile ricevere un'[offerta di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c6f44-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-tooworkplace-by-facebook"></a><span data-ttu-id="c6f44-112">Assegnare gli utenti tooWorkplace da Facebook</span><span class="sxs-lookup"><span data-stu-id="c6f44-112">Assign users tooWorkplace by Facebook</span></span>

<span data-ttu-id="c6f44-113">Azure AD Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="c6f44-113">Azure AD uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="c6f44-114">Nel contesto di hello di provisioning dell'account utente automatico, vengono sincronizzati solo gli utenti di hello e i gruppi che sono stati assegnati tooan applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6f44-114">In hello context of automatic user account provisioning, only hello users and groups that have been assigned tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="c6f44-115">Prima configurazione o abilitazione del provisioning del servizio, hello decidere quali utenti e gruppi in Azure Active Directory rappresentano utenti hello bisogno di accesso tooyour all'area di lavoro da app Facebook.</span><span class="sxs-lookup"><span data-stu-id="c6f44-115">Before configuring and enabling hello provisioning service, decide what users and groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="c6f44-116">È quindi possibile assegnare questi utenti tooyour all'area di lavoro, da app Facebook seguendo hello istruzioni [assegnare un'applicazione aziendale tooan utente o gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="c6f44-116">You can then assign these users tooyour Workplace by Facebook app by following hello instructions in [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="c6f44-117">Hello test configurazione di provisioning mediante l'assegnazione di un singolo tooWorkplace utente Azure AD da Facebook.</span><span class="sxs-lookup"><span data-stu-id="c6f44-117">Test hello provisioning configuration by assigning a single Azure AD user tooWorkplace by Facebook.</span></span> <span data-ttu-id="c6f44-118">Assegnare utenti e gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="c6f44-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="c6f44-119">Quando si assegna un utente tooWorkplace da Facebook, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="c6f44-119">When you assign a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="c6f44-120">ruolo di accesso predefinito Hello non funziona per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="c6f44-120">hello Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="c6f44-121">Abilitare il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="c6f44-121">Enable automated user provisioning</span></span>

<span data-ttu-id="c6f44-122">In questa sezione descrive la connessione AD Azure toohello account utente provisioning API dell'area di lavoro da Facebook.</span><span class="sxs-lookup"><span data-stu-id="c6f44-122">This section guides you through connecting your Azure AD toohello user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="c6f44-123">Verrà inoltre descritto come tooconfigure hello provisioning servizio toocreate, aggiornare e disabilitare gli account utente assegnato nell'area di lavoro da Facebook.</span><span class="sxs-lookup"><span data-stu-id="c6f44-123">You also learn how tooconfigure hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="c6f44-124">Questo è basato sull'assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6f44-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="c6f44-125">È anche possibile scegliere tooenabled basato su SAML SSO per l'area di lavoro da Facebook, da seguendo le istruzioni di hello cui hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c6f44-125">You can also choose tooenabled SAML-based SSO for Workplace by Facebook, by following hello instructions provided in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c6f44-126">L'accesso SSO può essere configurato indipendentemente dal provisioning automatico, anche se queste due funzionalità sono complementari.</span><span class="sxs-lookup"><span data-stu-id="c6f44-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="c6f44-127">Configurare l'account utente di provisioning tooWorkplace da Facebook in Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6f44-127">Configure user account provisioning tooWorkplace by Facebook in Azure AD</span></span>

<span data-ttu-id="c6f44-128">Azure supporta AD hello possibilità tooautomatically sincronizzare i dettagli dell'account di hello assegnato tooWorkplace utenti da Facebook.</span><span class="sxs-lookup"><span data-stu-id="c6f44-128">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="c6f44-129">La sincronizzazione automatica consente all'area di lavoro da dati di Facebook hello tooget tooauthorize utenti per l'accesso, è necessario prima di usarle il tentativo di toosign in hello per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="c6f44-129">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="c6f44-130">Esegue anche il deprovisioning degli utenti da Workplace by Facebook una volta che l'accesso viene revocato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6f44-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="c6f44-131">In hello [portale di Azure](https://portal.azure.com)selezionare **Azure Active Directory** > **le app aziendali** > **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="c6f44-131">In hello [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="c6f44-132">Se è già stato configurato all'area di lavoro da Facebook per SSO, cercare l'istanza di una rete aziendale da Facebook tramite il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="c6f44-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using hello search field.</span></span> <span data-ttu-id="c6f44-133">In caso contrario, selezionare **Aggiungi** e cercare **all'area di lavoro da Facebook** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c6f44-133">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="c6f44-134">Selezionare **all'area di lavoro da Facebook** da hello risultati di ricerca e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c6f44-134">Select **Workplace by Facebook** from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="c6f44-135">Selezionare l'istanza di una rete aziendale da Facebook, quindi hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="c6f44-135">Select your instance of Workplace by Facebook, and then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="c6f44-136">Impostare **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="c6f44-136">Set **Provisioning Mode** too**Automatic**.</span></span> 

    ![Screenshot delle opzioni di provisioning di Workplace by Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="c6f44-138">In hello **credenziali di amministratore** immettere hello **segreto Token** hello e **URL Tenant** dell'area di lavoro dall'amministratore di Facebook.</span><span class="sxs-lookup"><span data-stu-id="c6f44-138">Under hello **Admin Credentials** section, enter hello **Secret Token** and hello **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="c6f44-139">Nel portale di Azure hello, selezionare **Test connessione** tooensure Azure AD può connettersi tooyour all'area di lavoro da app Facebook.</span><span class="sxs-lookup"><span data-stu-id="c6f44-139">In hello Azure portal, select **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="c6f44-140">Se la connessione hello non riesce, verificare che l'area di lavoro dall'account Facebook disponga delle autorizzazioni di amministratore di Team.</span><span class="sxs-lookup"><span data-stu-id="c6f44-140">If hello connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="c6f44-141">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e selezionare la casella di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="c6f44-141">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello check box.</span></span>

8. <span data-ttu-id="c6f44-142">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c6f44-142">Select **Save**.</span></span>

9. <span data-ttu-id="c6f44-143">Nella sezione mapping hello, selezionare **tooWorkplace sincronizzare Active Directory gli utenti di Azure da Facebook**.</span><span class="sxs-lookup"><span data-stu-id="c6f44-143">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook**.</span></span>

10. <span data-ttu-id="c6f44-144">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da Azure AD tooWorkplace da Facebook.</span><span class="sxs-lookup"><span data-stu-id="c6f44-144">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="c6f44-145">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello account utente nell'area di lavoro da Facebook per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c6f44-145">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="c6f44-146">Selezionare tutte le modifiche, toocommit **salvare**.</span><span class="sxs-lookup"><span data-stu-id="c6f44-146">toocommit any changes, select **Save**.</span></span>

11. <span data-ttu-id="c6f44-147">tooenable hello servizio provisioning di Azure AD per l'area di lavoro da Facebook, in hello **impostazioni** modificare hello **lo stato di Provisioning** troppo**su**.</span><span class="sxs-lookup"><span data-stu-id="c6f44-147">tooenable hello Azure AD provisioning service for Workplace by Facebook, in hello **Settings** section, change hello **Provisioning Status** too**On**.</span></span>

12. <span data-ttu-id="c6f44-148">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c6f44-148">Select **Save**.</span></span>

<span data-ttu-id="c6f44-149">Per ulteriori informazioni su come il provisioning, vedere tooconfigure automatico [hello Facebook documentazione](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="c6f44-149">For more information on how tooconfigure automatic provisioning, see [hello Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="c6f44-150">È ora possibile creare un account di test.</span><span class="sxs-lookup"><span data-stu-id="c6f44-150">You can now create a test account.</span></span> <span data-ttu-id="c6f44-151">Attendere che i minuti too20 tooverify che hello account è stato sincronizzato tooWorkplace da Facebook.</span><span class="sxs-lookup"><span data-stu-id="c6f44-151">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c6f44-152">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="c6f44-152">Additional resources</span></span>

* [<span data-ttu-id="c6f44-153">Gestione del provisioning degli account utente per le app aziendali</span><span class="sxs-lookup"><span data-stu-id="c6f44-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c6f44-154">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6f44-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c6f44-155">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c6f44-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

