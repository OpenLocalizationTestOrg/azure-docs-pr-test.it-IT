---
title: 'Esercitazione: Configurazione di Cerner Central per il provisioning utenti automatico con Azure Active Directory | Microsoft Docs'
description: Informazioni su come il provisioning di roster tooa gli utenti nel centro Cerner tooconfigure tooautomatically di Azure Active Directory.
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="786e6-103">Esercitazione: Configurazione di Cerner Central per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="786e6-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="786e6-104">obiettivo di Hello di questa esercitazione è tooshow hello passaggi che è necessario tooperform Cerner centrale e Azure AD tooautomatically il provisioning e il de-provisioning account utente dall'elenco di utenti di Azure AD tooa nella Cerner centrale.</span><span class="sxs-lookup"><span data-stu-id="786e6-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Cerner Central and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooa user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="786e6-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="786e6-105">Prerequisites</span></span>

<span data-ttu-id="786e6-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="786e6-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="786e6-107">Tenant di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="786e6-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="786e6-108">Tenant di Cerner Central</span><span class="sxs-lookup"><span data-stu-id="786e6-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="786e6-109">Azure Active Directory si integra con Cerner centrale utilizzando hello [SCIM](http://www.simplecloud.info/) protocollo.</span><span class="sxs-lookup"><span data-stu-id="786e6-109">Azure Active Directory integrates with Cerner Central using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toocerner-central"></a><span data-ttu-id="786e6-110">L'assegnazione di utenti tooCerner centrale</span><span class="sxs-lookup"><span data-stu-id="786e6-110">Assigning users tooCerner Central</span></span>

<span data-ttu-id="786e6-111">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="786e6-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="786e6-112">Nel contesto di hello di provisioning dell'account utente automatico, vengono sincronizzati solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="786e6-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="786e6-113">Prima di configurare e abilitare hello provisioning del servizio, è necessario decidere quali utenti e/o i gruppi in Azure AD rappresentano utenti hello bisogno di accesso centrale tooCerner.</span><span class="sxs-lookup"><span data-stu-id="786e6-113">Before configuring and enabling hello provisioning service, you should decide what users and/or groups in Azure AD represent hello users who need access tooCerner Central.</span></span> <span data-ttu-id="786e6-114">Una volta deciso, è possibile assegnare questi tooCerner utenti centrale seguendo le istruzioni di hello qui:</span><span class="sxs-lookup"><span data-stu-id="786e6-114">Once decided, you can assign these users tooCerner Central by following hello instructions here:</span></span>

[<span data-ttu-id="786e6-115">Assegnare un'applicazione aziendale tooan utente o gruppo</span><span class="sxs-lookup"><span data-stu-id="786e6-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a><span data-ttu-id="786e6-116">Suggerimenti importanti per l'assegnazione di utenti tooCerner centrale</span><span class="sxs-lookup"><span data-stu-id="786e6-116">Important tips for assigning users tooCerner Central</span></span>

*   <span data-ttu-id="786e6-117">È consigliabile che un singolo utente di Azure AD assegnare tooCerner tootest centrale hello configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="786e6-117">It is recommended that a single Azure AD user be assigned tooCerner Central tootest hello provisioning configuration.</span></span> <span data-ttu-id="786e6-118">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="786e6-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="786e6-119">Al termine del test iniziale per un singolo utente, Cerner centrale consiglia di assegnare hello intero elenco utenti destinati tooaccess roster utente del tooCerner toobe provisioning qualsiasi Cerner soluzione (non solo Cerner centrale).</span><span class="sxs-lookup"><span data-stu-id="786e6-119">Once initial testing is complete for a single user, Cerner Central recommends assigning hello entire list of users intended tooaccess any Cerner solution (not just Cerner Central) toobe provisioned tooCerner’s user roster.</span></span>  <span data-ttu-id="786e6-120">Altre soluzioni Cerner sfruttano questo elenco di utenti nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="786e6-120">Other Cerner solutions leverage this list of users in hello user roster.</span></span>

*   <span data-ttu-id="786e6-121">Quando si assegna un tooCerner utente centrale, è necessario selezionare hello **utente** ruolo nella finestra di dialogo assegnazione hello.</span><span class="sxs-lookup"><span data-stu-id="786e6-121">When assigning a user tooCerner Central, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="786e6-122">Gli utenti con ruolo di "accesso predefinita" hello vengono esclusi dal provisioning.</span><span class="sxs-lookup"><span data-stu-id="786e6-122">Users with hello "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-toocerner-central"></a><span data-ttu-id="786e6-123">Configurazione tooCerner centrale di provisioning dell'utente</span><span class="sxs-lookup"><span data-stu-id="786e6-123">Configuring user provisioning tooCerner Central</span></span>

<span data-ttu-id="786e6-124">In questa sezione in modo semplificato Roster utente del centro del tooCerner Azure AD tramite API di provisioning dell'account utente SCIM della Cerner connessione e configura il provisioning del servizio toocreate hello, aggiornare e disabilitare l'utente assegnato account Cerner centrale in base assegnazione di utenti e gruppi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="786e6-124">This section guides you through connecting your Azure AD tooCerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="786e6-125">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per sedi centrali Cerner, attenendosi alle istruzioni hello fornite in [portale di Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="786e6-125">You may also choose tooenabled SAML-based Single Sign-On for Cerner Central, following hello instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="786e6-126">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="786e6-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="786e6-127">Per ulteriori informazioni, vedere hello [esercitazione centrale Cerner single sign-on](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="786e6-127">For more information, see hello [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a><span data-ttu-id="786e6-128">account utente automatico tooconfigure provisioning tooCerner centrale in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="786e6-128">tooconfigure automatic user account provisioning tooCerner Central in Azure AD:</span></span>


<span data-ttu-id="786e6-129">In ordine tooprovision utente account tooCerner centrale, sarà necessario un account di sistema centrale Cerner da Cerner toorequest e generare un token di connessione OAuth che Azure AD è possibile utilizzare endpoint SCIM del tooCerner tooconnect.</span><span class="sxs-lookup"><span data-stu-id="786e6-129">In order tooprovision user accounts tooCerner Central, you’ll need toorequest a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use tooconnect tooCerner's SCIM endpoint.</span></span> <span data-ttu-id="786e6-130">È inoltre consigliabile eseguire integrazione hello in un ambiente sandbox Cerner prima di distribuire tooproduction.</span><span class="sxs-lookup"><span data-stu-id="786e6-130">It is also recommended that hello integration be performed in a Cerner sandbox environment before deploying tooproduction.</span></span>

1.  <span data-ttu-id="786e6-131">primo passaggio Hello è persone hello tooensure gestione hello Cerner e integrazione di Azure AD avere un account CernerCare, che è necessario tooaccess hello documentazione necessari toocomplete hello istruzioni.</span><span class="sxs-lookup"><span data-stu-id="786e6-131">hello first step is tooensure hello people managing hello Cerner and Azure AD integration have a CernerCare account, which is required tooaccess hello documentation necessary toocomplete hello instructions.</span></span> <span data-ttu-id="786e6-132">Se necessario, utilizzare l'URL di hello sotto toocreate CernerCare account in ogni ambiente applicabile.</span><span class="sxs-lookup"><span data-stu-id="786e6-132">If necessary, use hello URLs below toocreate CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="786e6-133">Sandbox: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="786e6-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="786e6-134">Produzione: https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="786e6-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="786e6-135">È quindi necessario creare un account di sistema per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="786e6-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="786e6-136">Usare le istruzioni di hello sotto toorequest un Account di sistema per gli ambienti sandbox e di produzione.</span><span class="sxs-lookup"><span data-stu-id="786e6-136">Use hello instructions below toorequest a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="786e6-137">Istruzioni: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="786e6-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="786e6-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="786e6-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="786e6-139">Produzione: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="786e6-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="786e6-140">Generare quindi un token di connessione OAuth per ogni account di sistema.</span><span class="sxs-lookup"><span data-stu-id="786e6-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="786e6-141">toodo, seguire hello istruzioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="786e6-141">toodo this, follow hello instructions below.</span></span>

   * <span data-ttu-id="786e6-142">Istruzioni: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="786e6-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="786e6-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="786e6-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="786e6-144">Produzione: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="786e6-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="786e6-145">Infine, è necessario tooacquire utente Roster dell'area di autenticazione per entrambi gli ambienti sandbox e di produzione di hello nella configurazione di hello toocomplete Cerner.</span><span class="sxs-lookup"><span data-stu-id="786e6-145">Finally, you need tooacquire User Roster Realm IDs for both hello sandbox and production environments in Cerner toocomplete hello configuration.</span></span> <span data-ttu-id="786e6-146">Per informazioni su come tooacquire questa operazione, vedere: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="786e6-146">For information on how tooacquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="786e6-147">È ora possibile configurare tooCerner gli account utente di Azure AD tooprovision.</span><span class="sxs-lookup"><span data-stu-id="786e6-147">Now you can configure Azure AD tooprovision user accounts tooCerner.</span></span> <span data-ttu-id="786e6-148">Accedi toohello [portale di Azure](https://portal.azure.com)e passare toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="786e6-148">Sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="786e6-149">Se Cerner centrale già stato configurato per single sign-on, la ricerca per l'istanza del sito centrale Cerner usando il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="786e6-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using hello search field.</span></span> <span data-ttu-id="786e6-150">In caso contrario, selezionare **Aggiungi** e cercare **Cerner centrale** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="786e6-150">Otherwise, select **Add** and search for **Cerner Central** in hello application gallery.</span></span> <span data-ttu-id="786e6-151">Selezionare Cerner centrale dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="786e6-151">Select Cerner Central from hello search results, and add it tooyour list of applications.</span></span>

7.  <span data-ttu-id="786e6-152">Selezionare l'istanza di Cerner centrale, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="786e6-152">Select your instance of Cerner Central, then select hello **Provisioning** tab.</span></span>

8.  <span data-ttu-id="786e6-153">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="786e6-153">Set hello **Provisioning Mode** too**Automatic**.</span></span>

   ![Provisioning in Cerner Central](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="786e6-155">Compilare hello seguenti campi in **credenziali di amministratore**:</span><span class="sxs-lookup"><span data-stu-id="786e6-155">Fill in hello following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="786e6-156">In hello **URL Tenant** immettere un URL nel formato hello seguito, sostituendo "Roster-area di autenticazione-ID utente" con ID area di autenticazione hello acquisite nel passaggio &#4;.</span><span class="sxs-lookup"><span data-stu-id="786e6-156">In hello **Tenant URL** field, enter a URL in hello format below, replacing "User-Roster-Realm-ID" with hello realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="786e6-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="786e6-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="786e6-158">Produzione: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="786e6-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="786e6-159">In hello **segreto Token** campo immettere i token di connessione OAuth hello generato nel passaggio &#3;, quindi scegliere **Test connessione**.</span><span class="sxs-lookup"><span data-stu-id="786e6-159">In hello **Secret Token** field, enter hello OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="786e6-160">Vedrai una notifica di esito positivo sul lato upperright hello del portale.</span><span class="sxs-lookup"><span data-stu-id="786e6-160">You should see a success notification on hello upper­right side of your portal.</span></span>

10. <span data-ttu-id="786e6-161">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="786e6-161">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

11. <span data-ttu-id="786e6-162">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="786e6-162">Click **Save**.</span></span> 

12. <span data-ttu-id="786e6-163">In hello **mapping degli attributi** sezione, esaminare utente hello e gruppo attributi toobe sincronizzati da Azure AD tooCerner centrale.</span><span class="sxs-lookup"><span data-stu-id="786e6-163">In hello **Attribute Mappings** section, review hello user and group attributes toobe synchronized from Azure AD tooCerner Central.</span></span> <span data-ttu-id="786e6-164">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello utente account e gruppi nel centro Cerner per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="786e6-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="786e6-165">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="786e6-165">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="786e6-166">tooenable hello servizio provisioning di Azure AD per sedi centrali Cerner, hello modifica **lo stato di Provisioning** troppo**su** in hello **impostazioni** sezione</span><span class="sxs-lookup"><span data-stu-id="786e6-166">tooenable hello Azure AD provisioning service for Cerner Central, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

14. <span data-ttu-id="786e6-167">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="786e6-167">Click **Save**.</span></span> 

<span data-ttu-id="786e6-168">Verrà avviata la sincronizzazione iniziale di hello di tutti gli utenti e/o gruppi assegnati tooCerner Central nella sezione utenti e gruppi di hello.</span><span class="sxs-lookup"><span data-stu-id="786e6-168">This starts hello initial synchronization of any users and/or groups assigned tooCerner Central in hello Users and Groups section.</span></span> <span data-ttu-id="786e6-169">la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio provisioning di Azure AD è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="786e6-169">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello Azure AD provisioning service is running.</span></span> <span data-ttu-id="786e6-170">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio nella tua app Cerner centrale.</span><span class="sxs-lookup"><span data-stu-id="786e6-170">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="786e6-171">Per ulteriori informazioni sulla modalità di registrazione tooread provisioning di hello Azure AD, vedere [creazione di report per il provisioning utente automatico account](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="786e6-171">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="786e6-172">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="786e6-172">Additional resources</span></span>

* [<span data-ttu-id="786e6-173">Cerner Central: Publishing identity data using Azure AD (Cerner Central: Pubblicazione dei dati sull'identità con Azure AD)</span><span class="sxs-lookup"><span data-stu-id="786e6-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="786e6-174">Esercitazione sulla configurazione di Cerner Central per l'accesso Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="786e6-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="786e6-175">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="786e6-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="786e6-176">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="786e6-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="786e6-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="786e6-177">Next steps</span></span>
* <span data-ttu-id="786e6-178">[Informazioni su modalità di registrazione tooreview e ottenere report sull'attività di provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="786e6-178">[Learn how tooreview logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
