---
title: 'Esercitazione: Integrazione di Azure Active Directory con Citrix GoToMeeting | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Citrix GoToMeeting.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="628ca-103">Esercitazione: Configurazione di Citrix GoToMeeting per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="628ca-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="628ca-104">obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in Citrix GoToMeeting e Azure AD tooautomatically il provisioning e il de-provisioning degli account utente da Azure AD tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="628ca-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Citrix GoToMeeting and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooCitrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="628ca-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="628ca-105">Prerequisites</span></span>

<span data-ttu-id="628ca-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="628ca-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="628ca-107">Tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="628ca-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="628ca-108">Una sottoscrizione di Citrix GoToMeeting abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="628ca-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="628ca-109">Un account utente in Citrix GoToMeeting con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="628ca-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="628ca-110">L'assegnazione di utenti tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="628ca-110">Assigning users tooCitrix GoToMeeting</span></span>

<span data-ttu-id="628ca-111">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="628ca-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="628ca-112">Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="628ca-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="628ca-113">Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano utenti hello bisogno di accesso tooyour app Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="628ca-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="628ca-114">Una volta deciso, è possibile assegnare questi tooyour utenti Citrix GoToMeeting app seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="628ca-114">Once decided, you can assign these users tooyour Citrix GoToMeeting app by following hello instructions here:</span></span>

[<span data-ttu-id="628ca-115">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="628ca-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="628ca-116">Suggerimenti importanti per l'assegnazione di utenti tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="628ca-116">Important tips for assigning users tooCitrix GoToMeeting</span></span>

*   <span data-ttu-id="628ca-117">È consigliabile che un singolo utente AD Azure viene assegnato tooCitrix GoToMeeting tootest hello configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="628ca-117">It is recommended that a single Azure AD user is assigned tooCitrix GoToMeeting tootest hello provisioning configuration.</span></span> <span data-ttu-id="628ca-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="628ca-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="628ca-119">Quando si assegna un tooCitrix utente GoToMeeting, è necessario selezionare un ruolo utente valido.</span><span class="sxs-lookup"><span data-stu-id="628ca-119">When assigning a user tooCitrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="628ca-120">ruolo di "accesso predefinita" Hello non funziona per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="628ca-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="628ca-121">Abilitare il provisioning utenti automatizzato</span><span class="sxs-lookup"><span data-stu-id="628ca-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="628ca-122">In questa sezione viene illustrata la connessione API di provisioning dell'account utente del GoToMeeting tooCitrix il Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare l'utente assegnato conti in Citrix GoToMeeting basati su utenti e gruppi assegnazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="628ca-122">This section guides you through connecting your Azure AD tooCitrix GoToMeeting's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="628ca-123">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Citrix GoToMeeting, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="628ca-123">You may also choose tooenabled SAML-based Single Sign-On for Citrix GoToMeeting, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="628ca-124">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="628ca-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="628ca-125">tooconfigure account il provisioning utente automatico:</span><span class="sxs-lookup"><span data-stu-id="628ca-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="628ca-126">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="628ca-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="628ca-127">Se è già stato configurato Citrix GoToMeeting per single sign-on, eseguire la ricerca per l'istanza di Citrix GoToMeeting con il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="628ca-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using hello search field.</span></span> <span data-ttu-id="628ca-128">In caso contrario, selezionare **Aggiungi** e cercare **Citrix GoToMeeting** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="628ca-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in hello application gallery.</span></span> <span data-ttu-id="628ca-129">Selezionare Citrix GoToMeeting dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="628ca-129">Select Citrix GoToMeeting from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="628ca-130">Selezionare l'istanza di Citrix GoToMeeting e quindi hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="628ca-130">Select your instance of Citrix GoToMeeting, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="628ca-131">Set hello **Provisioning** modalità troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="628ca-131">Set hello **Provisioning** Mode too**Automatic**.</span></span> 

    ![provisioning](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="628ca-133">In hello sezione credenziali di amministratore, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="628ca-133">Under hello Admin Credentials section, perform hello following steps:</span></span>
   
    <span data-ttu-id="628ca-134">a.</span><span class="sxs-lookup"><span data-stu-id="628ca-134">a.</span></span> <span data-ttu-id="628ca-135">In hello **nome di utente amministratore Citrix GoToMeeting** casella di testo, digitare il nome utente hello di un amministratore.</span><span class="sxs-lookup"><span data-stu-id="628ca-135">In hello **Citrix GoToMeeting Admin User Name** textbox, type hello user name of an administrator.</span></span>

    <span data-ttu-id="628ca-136">b.</span><span class="sxs-lookup"><span data-stu-id="628ca-136">b.</span></span> <span data-ttu-id="628ca-137">In hello **Password amministratore Citrix GoToMeeting** casella di testo, la password dell'amministratore di hello.</span><span class="sxs-lookup"><span data-stu-id="628ca-137">In hello **Citrix GoToMeeting Admin Password** textbox, hello administrator's password.</span></span>

6. <span data-ttu-id="628ca-138">Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour app Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="628ca-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="628ca-139">Se hello connessione non riesce, verificare che l'account Citrix GoToMeeting con autorizzazioni di amministratore di Team e provare a hello **"Credenziali di amministratore"** esegue nuovamente l'istruzione.</span><span class="sxs-lookup"><span data-stu-id="628ca-139">If hello connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try hello **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="628ca-140">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="628ca-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="628ca-141">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="628ca-141">Click **Save.**</span></span>

9. <span data-ttu-id="628ca-142">Nella sezione mapping hello, selezionare **tooCitrix sincronizzare Active Directory gli utenti di Azure GoToMeeting.**</span><span class="sxs-lookup"><span data-stu-id="628ca-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooCitrix GoToMeeting.**</span></span>

10. <span data-ttu-id="628ca-143">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da Azure AD tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="628ca-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooCitrix GoToMeeting.</span></span> <span data-ttu-id="628ca-144">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in Citrix GoToMeeting per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="628ca-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="628ca-145">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="628ca-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="628ca-146">tooenable hello servizio provisioning di Azure AD per Citrix GoToMeeting, hello modifica **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello</span><span class="sxs-lookup"><span data-stu-id="628ca-146">tooenable hello Azure AD provisioning service for Citrix GoToMeeting, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="628ca-147">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="628ca-147">Click **Save.**</span></span>

<span data-ttu-id="628ca-148">Avviare la sincronizzazione iniziale di hello di tutti gli utenti e/o gruppi assegnati tooCitrix GoToMeeting nella sezione utenti e gruppi di hello.</span><span class="sxs-lookup"><span data-stu-id="628ca-148">It starts hello initial synchronization of any users and/or groups assigned tooCitrix GoToMeeting in hello Users and Groups section.</span></span> <span data-ttu-id="628ca-149">la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="628ca-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="628ca-150">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio nella tua app di Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="628ca-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="628ca-151">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="628ca-151">Additional resources</span></span>

* [<span data-ttu-id="628ca-152">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="628ca-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="628ca-153">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="628ca-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="628ca-154">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="628ca-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


