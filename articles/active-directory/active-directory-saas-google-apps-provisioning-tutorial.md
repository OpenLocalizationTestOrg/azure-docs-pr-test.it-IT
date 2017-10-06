---
title: 'Esercitazione: configurazione di Google Apps per il provisioning utenti automatico in Azure | Microsoft Docs'
description: Informazioni su come degli account utente di effettuare il provisioning e la prestazione tooautomatically da Azure AD tooGoogle app.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="d546b-103">Esercitazione: configurazione di Google Apps per il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="d546b-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="d546b-104">obiettivo di Hello di questa esercitazione è tooshow che Hello passaggi è necessario tooperform riserva tooautomatically Google Apps e Azure AD e il deprovisioning degli account utente da Azure AD tooGoogle app.</span><span class="sxs-lookup"><span data-stu-id="d546b-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Google Apps and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGoogle Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d546b-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d546b-105">Prerequisites</span></span>

<span data-ttu-id="d546b-106">scenario Hello descritto in questa esercitazione si presuppone che si disponga già di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d546b-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="d546b-107">Tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d546b-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="d546b-108">È necessario disporre di un tenant valido per Google Apps for Work o Google Apps for Education.</span><span class="sxs-lookup"><span data-stu-id="d546b-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="d546b-109">È possibile usare un account della versione di valutazione gratuita per entrambi i servizi.</span><span class="sxs-lookup"><span data-stu-id="d546b-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="d546b-110">Account utente in Google Apps con autorizzazioni di amministratore di team.</span><span class="sxs-lookup"><span data-stu-id="d546b-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-toogoogle-apps"></a><span data-ttu-id="d546b-111">Assegnazione di utenti tooGoogle App</span><span class="sxs-lookup"><span data-stu-id="d546b-111">Assigning users tooGoogle Apps</span></span>

<span data-ttu-id="d546b-112">Azure Active Directory Usa il concetto di "assegnazioni" toodetermine gli utenti che devono ricevere le app tooselected di accesso.</span><span class="sxs-lookup"><span data-stu-id="d546b-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="d546b-113">Nel contesto di hello di provisioning dell'account utente automatico, solo gli utenti di hello e i gruppi "assegnati" tooan applicazione in Azure AD è sincronizzato.</span><span class="sxs-lookup"><span data-stu-id="d546b-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="d546b-114">Prima di configurare e abilitare hello provisioning del servizio, è necessario toodecide quali utenti e/o i gruppi in Azure AD rappresentano utenti hello necessitano accedere alle app di Google Apps tooyour.</span><span class="sxs-lookup"><span data-stu-id="d546b-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Google Apps app.</span></span> <span data-ttu-id="d546b-115">Una volta deciso, è possibile assegnare queste app di Google Apps tooyour utenti seguendo le istruzioni di hello qui: [assegnare un'applicazione aziendale tooan utente o gruppo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="d546b-115">Once decided, you can assign these users tooyour Google Apps app by following hello instructions here: [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="d546b-116">È consigliabile che un singolo utente di Azure AD assegnare hello tootest di App tooGoogle configurazione provisioning.</span><span class="sxs-lookup"><span data-stu-id="d546b-116">It is recommended that a single Azure AD user be assigned tooGoogle Apps tootest hello provisioning configuration.</span></span> <span data-ttu-id="d546b-117">È possibile assegnare utenti e/o gruppi aggiuntivi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="d546b-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="d546b-118">Quando si assegna un tooGoogle utente App, è necessario selezionare hello utente o ruolo di "Gruppo" nella finestra di dialogo assegnazione hello.</span><span class="sxs-lookup"><span data-stu-id="d546b-118">When assigning a user tooGoogle Apps, you must select hello User or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="d546b-119">ruolo di "accesso predefinita" Hello non funziona per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="d546b-119">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="d546b-120">Abilitare il provisioning utenti automatico</span><span class="sxs-lookup"><span data-stu-id="d546b-120">Enable automated user provisioning</span></span>

<span data-ttu-id="d546b-121">Questa sezione viene illustrato come tramite la connessione di account utente dell'Azure AD tooGoogle App API di provisioning e configurazione hello toocreate servizio di provisioning, aggiornare e disabilitare gli account utente assegnato in Google Apps in base all'assegnazione di utenti e gruppi in Azure AD .</span><span class="sxs-lookup"><span data-stu-id="d546b-121">This section guides you through connecting your Azure AD tooGoogle Apps's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="d546b-122">È inoltre possibile scegliere tooenabled basato su SAML Single Sign-On per Google Apps, attenendosi alle istruzioni hello fornite [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d546b-122">You may also choose tooenabled SAML-based Single Sign-On for Google Apps, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d546b-123">L'accesso Single Sign-On può essere configurato indipendentemente dal provisioning automatico, nonostante queste due funzionalità siano complementari.</span><span class="sxs-lookup"><span data-stu-id="d546b-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="d546b-124">Configurare il provisioning automatico degli account utente</span><span class="sxs-lookup"><span data-stu-id="d546b-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="d546b-125">Un'altra opzione valida per l'automazione delle applicazioni tooGoogle il provisioning degli utenti è toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) che esegue il provisioning del tooGoogle di identità di Active Directory locale app.</span><span class="sxs-lookup"><span data-stu-id="d546b-125">Another viable option for automating user provisioning tooGoogle Apps is toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities tooGoogle Apps.</span></span> <span data-ttu-id="d546b-126">Al contrario, la soluzione hello in questa esercitazione viene eseguito il provisioning gli utenti di Azure Active Directory (cloud) e i gruppi abilitati alla posta elettronica tooGoogle app.</span><span class="sxs-lookup"><span data-stu-id="d546b-126">In contrast, hello solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups tooGoogle Apps.</span></span> 

1. <span data-ttu-id="d546b-127">Sign in hello [Console di amministrazione di Google Apps](http://admin.google.com/) con l'account amministratore e fare clic su **sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="d546b-127">Sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="d546b-128">Se non viene visualizzato il collegamento hello, possono essere nascosti in hello **più controlli** menu in basso hello hello.</span><span class="sxs-lookup"><span data-stu-id="d546b-128">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Fare clic su sicurezza.][10]

2. <span data-ttu-id="d546b-130">In hello **sicurezza** pagina, fare clic su **riferimento all'API**.</span><span class="sxs-lookup"><span data-stu-id="d546b-130">On hello **Security** page, click **API Reference**.</span></span>
   
    ![Fare clic su Informazioni di riferimento sulle API.][15]

3. <span data-ttu-id="d546b-132">Selezionare **Enable API access**.</span><span class="sxs-lookup"><span data-stu-id="d546b-132">Select **Enable API access**.</span></span>
   
    ![Fare clic su Informazioni di riferimento sulle API.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="d546b-134">Per ogni utente che si desidera tooprovision tooGoogle App, il suo nome utente in Azure Active Directory *deve* essere abbinato tooa dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="d546b-134">For every user that you intend tooprovision tooGoogle Apps, their username in Azure Active Directory *must* be tied tooa custom domain.</span></span> <span data-ttu-id="d546b-135">Ad esempio, nomi utente simili a bob@contoso.onmicrosoft.com non verranno accettati da Google Apps, mentre bob@contoso.com verranno accettati.</span><span class="sxs-lookup"><span data-stu-id="d546b-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="d546b-136">È possibile modificare il dominio di un utente esistente modificandone le proprietà in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d546b-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="d546b-137">Istruzioni per come inclusi in un dominio personalizzato per Azure Active Directory e Google Apps tooset i passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="d546b-137">Instructions for how tooset a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="d546b-138">Se non sono stati aggiunti ancora un tooyour di nome di dominio personalizzato Azure Active Directory, quindi seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d546b-138">If you haven't added a custom domain name tooyour Azure Active Directory yet, then follow hello following steps:</span></span>
  
    <span data-ttu-id="d546b-139">a.</span><span class="sxs-lookup"><span data-stu-id="d546b-139">a.</span></span> <span data-ttu-id="d546b-140">In hello [portale di Azure](https://portal.azure.com)via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d546b-140">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="d546b-141">Nell'elenco di directory hello, selezionare la directory.</span><span class="sxs-lookup"><span data-stu-id="d546b-141">In hello directory list, select your directory.</span></span> 

    <span data-ttu-id="d546b-142">b.</span><span class="sxs-lookup"><span data-stu-id="d546b-142">b.</span></span> <span data-ttu-id="d546b-143">Fare clic su **nome domini** hello riquadro di spostamento a sinistra e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d546b-143">Click **Domains name** on hello left navigation pane, and then click **Add**.</span></span>
     
     ![dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![aggiunta del dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="d546b-146">c.</span><span class="sxs-lookup"><span data-stu-id="d546b-146">c.</span></span> <span data-ttu-id="d546b-147">Digitare il nome di dominio in hello **nome di dominio** campo.</span><span class="sxs-lookup"><span data-stu-id="d546b-147">Type your domain name into hello **Domain name** field.</span></span> <span data-ttu-id="d546b-148">Il nome di dominio deve essere hello stesso nome di dominio che si desidera toouse per Google Apps.</span><span class="sxs-lookup"><span data-stu-id="d546b-148">This domain name should be hello same domain name that you intend toouse for Google Apps.</span></span> <span data-ttu-id="d546b-149">Quando si è pronti, fare clic su hello **Aggiungi dominio** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d546b-149">When ready, click hello **Add Domain** button.</span></span>
     
     ![nome di dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="d546b-151">d.</span><span class="sxs-lookup"><span data-stu-id="d546b-151">d.</span></span> <span data-ttu-id="d546b-152">Fare clic su **Avanti** toogo toohello pagina di verifica.</span><span class="sxs-lookup"><span data-stu-id="d546b-152">Click **Next** toogo toohello verification page.</span></span> <span data-ttu-id="d546b-153">tooverify che si è proprietari di questo dominio, è necessario modificare i record DNS del dominio hello in base a valori toohello forniti in questa pagina.</span><span class="sxs-lookup"><span data-stu-id="d546b-153">tooverify that you own this domain, you must edit hello domain's DNS records according toohello values provided on this page.</span></span> <span data-ttu-id="d546b-154">È possibile scegliere tooverify utilizzando **record MX** o **record TXT**, a seconda della selezione per hello **tipo di Record** opzione.</span><span class="sxs-lookup"><span data-stu-id="d546b-154">You may choose tooverify using either **MX records** or **TXT records**, depending on what you select for hello **Record Type** option.</span></span> <span data-ttu-id="d546b-155">Per istruzioni più complete su come nome di dominio tooverify con Azure AD, vedere [aggiungere la propria tooAzure nome di dominio Active Directory](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="d546b-155">For more comprehensive instructions on how tooverify domain name with Azure AD, refer [Add your own domain name tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![dominio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="d546b-157">e.</span><span class="sxs-lookup"><span data-stu-id="d546b-157">e.</span></span> <span data-ttu-id="d546b-158">Ripetere i passaggi per tutti i domini di hello che si desidera tooadd tooyour directory precedenti hello.</span><span class="sxs-lookup"><span data-stu-id="d546b-158">Repeat hello preceding steps for all hello domains that you intend tooadd tooyour directory.</span></span>

5. <span data-ttu-id="d546b-159">Ora che tutti i domini sono stati verificati con Azure AD, è necessario verificarli nuovamente con Google Apps.</span><span class="sxs-lookup"><span data-stu-id="d546b-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="d546b-160">Per ogni dominio che non è già registrata con Google Apps, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d546b-160">For each domain that isn't already registered with Google Apps, perform hello following steps:</span></span>
   
    <span data-ttu-id="d546b-161">a.</span><span class="sxs-lookup"><span data-stu-id="d546b-161">a.</span></span> <span data-ttu-id="d546b-162">In hello [Console di amministrazione di Google Apps](http://admin.google.com/), fare clic su **domini**.</span><span class="sxs-lookup"><span data-stu-id="d546b-162">In hello [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![Fare clic su Domini][20]

    <span data-ttu-id="d546b-164">b.</span><span class="sxs-lookup"><span data-stu-id="d546b-164">b.</span></span> <span data-ttu-id="d546b-165">Fare clic su **Add a domain or a domain alias**.</span><span class="sxs-lookup"><span data-stu-id="d546b-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![Aggiungere un nuovo dominio][21]

    <span data-ttu-id="d546b-167">c.</span><span class="sxs-lookup"><span data-stu-id="d546b-167">c.</span></span> <span data-ttu-id="d546b-168">Selezionare **aggiungere un altro dominio**e digitare il nome di hello del dominio hello che si desidera tooadd.</span><span class="sxs-lookup"><span data-stu-id="d546b-168">Select **Add another domain**, and type in hello name of hello domain that you would like tooadd.</span></span>
     
     ![Digitare il nome di dominio][22]

    <span data-ttu-id="d546b-170">d.</span><span class="sxs-lookup"><span data-stu-id="d546b-170">d.</span></span> <span data-ttu-id="d546b-171">Fare clic su **Continue and verify domain ownership** (Continua e verifica la proprietà del dominio).</span><span class="sxs-lookup"><span data-stu-id="d546b-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="d546b-172">Seguire quindi hello passaggi tooverify che si è proprietari di nome di dominio hello.</span><span class="sxs-lookup"><span data-stu-id="d546b-172">Then follow hello steps tooverify that you own hello domain name.</span></span> <span data-ttu-id="d546b-173">Per istruzioni dettagliate su come tooverify del dominio con Google Apps, vedere.</span><span class="sxs-lookup"><span data-stu-id="d546b-173">For comprehensive instructions on how tooverify your domain with Google Apps, see.</span></span> <span data-ttu-id="d546b-174">[Verificare la proprietà del sito con Google Apps](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="d546b-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="d546b-175">e.</span><span class="sxs-lookup"><span data-stu-id="d546b-175">e.</span></span> <span data-ttu-id="d546b-176">Ripetere i passaggi per tutti i domini aggiuntivi che si desidera tooadd tooGoogle App precedenti hello.</span><span class="sxs-lookup"><span data-stu-id="d546b-176">Repeat hello preceding steps for any additional domains that you intend tooadd tooGoogle Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="d546b-177">Se si modifica il dominio primario hello del tenant di Google Apps, e se è già configurato single sign-on con Azure AD e aver toorepeat passaggio #3 nella sezione [passaggio 2: abilitare Single Sign-On](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="d546b-177">If you change hello primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have toorepeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="d546b-178">In hello [Console di amministrazione di Google Apps](http://admin.google.com/), fare clic su **ruoli di amministratore**.</span><span class="sxs-lookup"><span data-stu-id="d546b-178">In hello [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Fare clic su Google Apps][26]

7. <span data-ttu-id="d546b-180">Determinare quale amministratore account desideri toouse toomanage provisioning degli utenti.</span><span class="sxs-lookup"><span data-stu-id="d546b-180">Determine which admin account you would like toouse toomanage user provisioning.</span></span> <span data-ttu-id="d546b-181">Per hello **ruolo admin** di tale account, modificare hello **privilegi** per tale ruolo.</span><span class="sxs-lookup"><span data-stu-id="d546b-181">For hello **admin role** of that account, edit hello **Privileges** for that role.</span></span> <span data-ttu-id="d546b-182">Assicurarsi che tutti hello **privilegi di amministratore API** abilitato in modo che questo account può essere usato per il provisioning.</span><span class="sxs-lookup"><span data-stu-id="d546b-182">Make sure it has all hello **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Fare clic su Google Apps][27]
   
    > [!NOTE]
    > <span data-ttu-id="d546b-184">Se si sta configurando un ambiente di produzione, hello consiglia toocreate un account di amministratore in Google Apps in modo specifico per questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="d546b-184">If you are configuring a production environment, hello best practice is toocreate an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="d546b-185">Questi account devono avere un ruolo di amministratore associato che disponga dei privilegi di API necessari hello.</span><span class="sxs-lookup"><span data-stu-id="d546b-185">These accounts must have an admin role associated with it that has hello necessary API privileges.</span></span>
     
8. <span data-ttu-id="d546b-186">In hello [portale di Azure](https://portal.azure.com), Sfoglia toohello **Azure Active Directory > App aziendali > tutte le applicazioni** sezione.</span><span class="sxs-lookup"><span data-stu-id="d546b-186">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="d546b-187">Se è già stato configurato Google Apps per single sign-on, eseguire la ricerca per l'istanza di Google Apps utilizzando il campo di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="d546b-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using hello search field.</span></span> <span data-ttu-id="d546b-188">In caso contrario, selezionare **Aggiungi** e cercare **Google Apps** nella raccolta di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d546b-188">Otherwise, select **Add** and search for **Google Apps** in hello application gallery.</span></span> <span data-ttu-id="d546b-189">Selezionare Google Apps dai risultati della ricerca hello e aggiungerlo tooyour elenco delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d546b-189">Select Google Apps from hello search results, and add it tooyour list of applications.</span></span>

10. <span data-ttu-id="d546b-190">Selezionare l'istanza di Google Apps, quindi selezionare hello **Provisioning** scheda.</span><span class="sxs-lookup"><span data-stu-id="d546b-190">Select your instance of Google Apps, then select hello **Provisioning** tab.</span></span>

11. <span data-ttu-id="d546b-191">Set hello **modalità di Provisioning** troppo**automatica**.</span><span class="sxs-lookup"><span data-stu-id="d546b-191">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

     ![provisioning](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="d546b-193">In hello **credenziali di amministratore** fare clic su **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="d546b-193">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="d546b-194">Verrà aperta una finestra di dialogo di autorizzazione di Google Apps in una nuova finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="d546b-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="d546b-195">Confermare che si desidera toogive Azure Active Directory toomake le modifiche alle autorizzazioni che tenant tooyour Google Apps.</span><span class="sxs-lookup"><span data-stu-id="d546b-195">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Google Apps tenant.</span></span> <span data-ttu-id="d546b-196">Fare clic **Accept**.</span><span class="sxs-lookup"><span data-stu-id="d546b-196">Click **Accept**.</span></span>
    
     ![Verificare le autorizzazioni.][28]

14. <span data-ttu-id="d546b-198">Nel portale di Azure hello, fare clic su **Test connessione** tooensure Azure AD può connettersi tooyour app di Google Apps.</span><span class="sxs-lookup"><span data-stu-id="d546b-198">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Google Apps app.</span></span> <span data-ttu-id="d546b-199">Se hello connessione non riesce, verificare che l'account Google Apps ha autorizzazioni di amministratore di Team e provare a hello **"Autorizza"** esegue nuovamente l'istruzione.</span><span class="sxs-lookup"><span data-stu-id="d546b-199">If hello connection fails, ensure your Google Apps account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

15. <span data-ttu-id="d546b-200">Immettere l'indirizzo di posta elettronica hello di una persona o il gruppo che deve ricevere le notifiche degli errori di provisioning in hello **notifica tramite posta elettronica** campo e casella di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="d546b-200">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

16. <span data-ttu-id="d546b-201">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d546b-201">Click **Save.**</span></span>

17. <span data-ttu-id="d546b-202">Nella sezione mapping hello, selezionare **tooGoogle sincronizzare Active Directory gli utenti di Azure app.**</span><span class="sxs-lookup"><span data-stu-id="d546b-202">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGoogle Apps.**</span></span>

18. <span data-ttu-id="d546b-203">In hello **mapping degli attributi** sezione, esaminare gli attributi utente hello che vengono sincronizzati da Azure AD tooGoogle app.</span><span class="sxs-lookup"><span data-stu-id="d546b-203">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGoogle Apps.</span></span> <span data-ttu-id="d546b-204">gli attributi selezionati come Hello **corrispondenza** proprietà sono utilizzate toomatch hello gli account utente in Google Apps per operazioni di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="d546b-204">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="d546b-205">Selezionare hello Salva pulsante toocommit tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d546b-205">Select hello Save button toocommit any changes.</span></span>

19. <span data-ttu-id="d546b-206">tooenable hello servizio provisioning di Azure AD per Google Apps, hello modifica **lo stato di Provisioning** troppo**su** nella sezione Impostazioni hello</span><span class="sxs-lookup"><span data-stu-id="d546b-206">tooenable hello Azure AD provisioning service for Google Apps, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

20. <span data-ttu-id="d546b-207">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d546b-207">Click **Save.**</span></span>

<span data-ttu-id="d546b-208">Avviare la sincronizzazione iniziale di hello di tutti gli utenti e/o gruppi assegnati App tooGoogle nella sezione utenti e gruppi di hello.</span><span class="sxs-lookup"><span data-stu-id="d546b-208">It starts hello initial synchronization of any users and/or groups assigned tooGoogle Apps in hello Users and Groups section.</span></span> <span data-ttu-id="d546b-209">la sincronizzazione iniziale Hello accetta più tooperform di sincronizzazioni successive, che si verificano ogni 20 minuti circa, purché hello servizio è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d546b-209">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="d546b-210">È possibile utilizzare hello **i dettagli della sincronizzazione** sezione toomonitor lo stato di avanzamento e seguire i collegamenti tooprovisioning attività i report, che descrivono tutte le azioni eseguite da hello provisioning del servizio nella tua app di Google Apps.</span><span class="sxs-lookup"><span data-stu-id="d546b-210">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d546b-211">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d546b-211">Additional resources</span></span>

* [<span data-ttu-id="d546b-212">Gestione del provisioning degli account utente per app aziendali</span><span class="sxs-lookup"><span data-stu-id="d546b-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d546b-213">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d546b-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d546b-214">Configurare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d546b-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png