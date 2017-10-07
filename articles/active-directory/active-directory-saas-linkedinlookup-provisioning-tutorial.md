---
title: 'Esercitazione: Configurazione di LinkedIn Lookup per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come tooconfigure Azure Active Directory tooautomatically il provisioning e il de-provisioning account utente di tooLinkedIn ricerca.
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 3e41abb8af00715f70e5a14d9d26ff600c10f492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a><span data-ttu-id="dc5ef-103">Esercitazione: Configurazione di LinkedIn Lookup per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="dc5ef-103">Tutorial: Configuring LinkedIn Lookup for Automatic User Provisioning</span></span>


<span data-ttu-id="dc5ef-104">obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform in ricerca di LinkedIn e Azure AD tooautomatically effettuare il provisioning e il de-provisioning degli account utente da Azure AD tooLinkedIn ricerca.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LinkedIn Lookup and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLinkedIn Lookup.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dc5ef-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dc5ef-105">Prerequisites</span></span>

<span data-ttu-id="dc5ef-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="dc5ef-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="dc5ef-107">Tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc5ef-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="dc5ef-108">Tenant di LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="dc5ef-108">A LinkedIn Lookup tenant</span></span> 
*   <span data-ttu-id="dc5ef-109">Un account di amministratore per la ricerca di LinkedIn con accesso toohello centro Account LinkedIn</span><span class="sxs-lookup"><span data-stu-id="dc5ef-109">An administrator account in LinkedIn Lookup with access toohello LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="dc5ef-110">Azure Active Directory si integra con ricerca di LinkedIn con hello [SCIM](http://www.simplecloud.info/) protocollo.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-110">Azure Active Directory integrates with LinkedIn Lookup using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toolinkedin-lookup"></a><span data-ttu-id="dc5ef-111">L'assegnazione di utenti tooLinkedIn ricerca</span><span class="sxs-lookup"><span data-stu-id="dc5ef-111">Assigning users tooLinkedIn Lookup</span></span>

<span data-ttu-id="dc5ef-112">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="dc5ef-113">Nel contesto di hello di provisioning dell'account utente automatica, verranno sincronizzati solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="dc5ef-114">Prima di configurare e abilitare hello provisioning del servizio, sarà necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano utenti hello bisogno di accesso tooLinkedIn ricerca.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooLinkedIn Lookup.</span></span> <span data-ttu-id="dc5ef-115">Una volta deciso, è possibile assegnare questi tooLinkedIn utenti ricerca seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="dc5ef-115">Once decided, you can assign these users tooLinkedIn Lookup by following hello instructions here:</span></span>

[<span data-ttu-id="dc5ef-116">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="dc5ef-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-lookup"></a><span data-ttu-id="dc5ef-117">Suggerimenti importanti per l'assegnazione di utenti tooLinkedIn ricerca</span><span class="sxs-lookup"><span data-stu-id="dc5ef-117">Important tips for assigning users tooLinkedIn Lookup</span></span>

*   <span data-ttu-id="dc5ef-118">È consigliabile che un singolo utente di Azure AD assegnare hello tootest di ricerca tooLinkedIn configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-118">It is recommended that a single Azure AD user be assigned tooLinkedIn Lookup tootest hello provisioning configuration.</span></span> <span data-ttu-id="dc5ef-119">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="dc5ef-120">Quando si assegna un tooLinkedIn utente ricerca, è necessario selezionare hello **utente** ruolo nella finestra di dialogo assegnazione hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-120">When assigning a user tooLinkedIn Lookup, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="dc5ef-121">ruolo di "accesso predefinita" Hello non funziona per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-toolinkedin-lookup"></a><span data-ttu-id="dc5ef-122">Configurazione di ricerca tooLinkedIn di provisioning dell'utente</span><span class="sxs-lookup"><span data-stu-id="dc5ef-122">Configuring user provisioning tooLinkedIn Lookup</span></span>

<span data-ttu-id="dc5ef-123">In questa sezione viene illustrata la connessione API di provisioning dell'account utente SCIM della ricerca tooLinkedIn Azure AD e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare l'utente assegnato conti nella ricerca di LinkedIn basati su utenti e gruppi assegnazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-123">This section guides you through connecting your Azure AD tooLinkedIn Lookup's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in LinkedIn Lookup based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="dc5ef-124">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per la ricerca di LinkedIn, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dc5ef-124">You may also choose tooenabled SAML-based Single Sign-On for LinkedIn Lookup, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="dc5ef-125">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-lookup-in-azure-ad"></a><span data-ttu-id="dc5ef-126">account utente automatico tooconfigure provisioning tooLinkedIn ricerca di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="dc5ef-126">tooconfigure automatic user account provisioning tooLinkedIn Lookup in Azure AD:</span></span>


<span data-ttu-id="dc5ef-127">primo passaggio Hello è tooretrieve il token di accesso di LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-127">hello first step is tooretrieve your LinkedIn access token.</span></span> <span data-ttu-id="dc5ef-128">Un amministratore dell'organizzazione può eseguire il provisioning automatico di un token di accesso.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="dc5ef-129">Nel centro account, Vai troppo**impostazioni &gt; impostazioni globali** e aprire hello **SCIM installazione** pannello.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-129">In your account center, go too**Settings &gt; Global Settings** and open hello **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="dc5ef-130">Se si accede centro account hello direttamente anziché tramite un collegamento, è possibile raggiungerli tramite hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-130">If you are accessing hello account center directly rather than through a link, you can reach it using hello following steps.</span></span>

1)  <span data-ttu-id="dc5ef-131">Accedi tooAccount Center.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-131">Sign in tooAccount Center.</span></span>

2)  <span data-ttu-id="dc5ef-132">Selezionare **Admin (Amministratore) &gt; Admin Settings** (Opzioni amministratore).</span><span class="sxs-lookup"><span data-stu-id="dc5ef-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="dc5ef-133">Fare clic su **avanzate integrazioni** intestazione laterale sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-133">Click **Advanced Integrations** on hello left sidebar.</span></span> <span data-ttu-id="dc5ef-134">Si è centro account toohello diretto.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-134">You are directed toohello account center.</span></span>

4)  <span data-ttu-id="dc5ef-135">Fare clic su **+ Aggiungi nuova configurazione di SCIM** e seguire la procedura hello compilando ogni campo.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-135">Click **+ Add new SCIM configuration** and follow hello procedure by filling in each field.</span></span>

> <span data-ttu-id="dc5ef-136">Se l'opzione di assegnazione automatica delle licenze non è abilitata, vengono sincronizzati solo i dati degli utenti.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![Provisioning di LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="dc5ef-138">Quando l'assegnazione autolicense è abilitato, è necessario toonote l'istanza dell'applicazione e tipo di licenza.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-138">When auto­license assignment is enabled, you need toonote the application instance and license type.</span></span> <span data-ttu-id="dc5ef-139">Assegnazione delle licenze in un primo arrivato, prima di servire base fino a quando non vengono eseguite tutte le licenze hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-139">Licenses are assigned on a first come, first serve basis until all hello licenses are taken.</span></span>

![Provisioning di LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="dc5ef-141">Fare clic su **Generate token** (Genera token).</span><span class="sxs-lookup"><span data-stu-id="dc5ef-141">Click **Generate token**.</span></span> <span data-ttu-id="dc5ef-142">Verrà visualizzata la visualizzazione del token di accesso in hello **token di accesso** campo.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-142">You should see your access token display under hello **Access token** field.</span></span>

6)  <span data-ttu-id="dc5ef-143">Salva negli Appunti tooyour token di accesso o nel computer prima di uscire dalla pagina hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-143">Save your access token tooyour clipboard or computer before leaving hello page.</span></span>

7) <span data-ttu-id="dc5ef-144">Successivamente, accedi toohello [portale di Azure](https://portal.azure.com)e passare toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-144">Next, sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="dc5ef-145">Se è già stato configurato LinkedIn ricerca per single sign-on, eseguire la ricerca per l'istanza di ricerca di LinkedIn con campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-145">If you have already configured LinkedIn Lookup for single sign-on, search for your instance of LinkedIn Lookup using hello search field.</span></span> <span data-ttu-id="dc5ef-146">In caso contrario, selezionare **Aggiungi** e cercare **LinkedIn ricerca** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-146">Otherwise, select **Add** and search for **LinkedIn Lookup** in hello application gallery.</span></span> <span data-ttu-id="dc5ef-147">Selezionare ricerca LinkedIn dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-147">Select LinkedIn Lookup from hello search results, and add it tooyour list of applications.</span></span>

9)  <span data-ttu-id="dc5ef-148">Selezionare l'istanza di LinkedIn ricerca, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-148">Select your instance of LinkedIn Lookup, then select hello **Provisioning** tab.</span></span>

10) <span data-ttu-id="dc5ef-149">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-149">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Provisioning di LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="dc5ef-151">Compilare hello seguenti campi in **credenziali di amministratore** :</span><span class="sxs-lookup"><span data-stu-id="dc5ef-151">Fill in hello following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="dc5ef-152">In hello **URL Tenant** immettere https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-152">In hello **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="dc5ef-153">In hello **segreto Token** campo, immettere il token di accesso hello generato nel passaggio 1 e fare clic su **Test connessione** .</span><span class="sxs-lookup"><span data-stu-id="dc5ef-153">In hello **Secret Token** field, enter hello access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="dc5ef-154">Vedrai una notifica di esito positivo sul lato upperright hello del portale.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-154">You should see a success notification on hello upper­right side of   your portal.</span></span>

12) <span data-ttu-id="dc5ef-155">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-155">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

13) <span data-ttu-id="dc5ef-156">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-156">Click **Save**.</span></span> 

14) <span data-ttu-id="dc5ef-157">In hello **mapping degli attributi** sezione, esaminare gli attributi utente e gruppo hello che verranno sincronizzati da Azure AD tooLinkedIn ricerca.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-157">In hello **Attribute Mappings** section, review hello user and group attributes that will be synchronized from Azure AD tooLinkedIn Lookup.</span></span> <span data-ttu-id="dc5ef-158">Si noti che gli attributi selezionati come hello **corrispondenza** proprietà saranno utilizzati toomatch hello account e gruppi utente nella ricerca di LinkedIn per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-158">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts and groups in LinkedIn Lookup for update operations.</span></span> <span data-ttu-id="dc5ef-159">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-159">Select hello Save button toocommit any changes.</span></span>

![Provisioning di LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="dc5ef-161">tooenable hello servizio provisioning di Azure AD per la ricerca di LinkedIn, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione</span><span class="sxs-lookup"><span data-stu-id="dc5ef-161">tooenable hello Azure AD provisioning service for LinkedIn Lookup, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

16) <span data-ttu-id="dc5ef-162">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-162">Click **Save**.</span></span> 

<span data-ttu-id="dc5ef-163">Verrà avviata la sincronizzazione iniziale di hello di tutti gli utenti e/o gruppi assegnati tooLinkedIn ricerca nella sezione utenti e gruppi di hello.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-163">This will start hello initial synchronization of any users and/or groups assigned tooLinkedIn Lookup in hello Users and Groups section.</span></span> <span data-ttu-id="dc5ef-164">Si noti che la sincronizzazione iniziale hello tooperform più lungo di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-164">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="dc5ef-165">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio nella tua app di ricerca di LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="dc5ef-165">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your LinkedIn Lookup app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="dc5ef-166">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="dc5ef-166">Additional Resources</span></span>

* [<span data-ttu-id="dc5ef-167">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="dc5ef-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="dc5ef-168">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc5ef-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
