---
title: 'Esercitazione: Eseguire l''integrazione di Azure Active Directory con vxMaintain | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e vxMaintain.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a><span data-ttu-id="8b465-103">Esercitazione: Eseguire l'integrazione di Azure Active Directory con vxMaintain</span><span class="sxs-lookup"><span data-stu-id="8b465-103">Tutorial: Integrate Azure Active Directory with vxMaintain</span></span>

<span data-ttu-id="8b465-104">In questa esercitazione, è illustrato come vxMaintain toointegrate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b465-104">In this tutorial, you learn how toointegrate vxMaintain with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b465-105">Questa integrazione offre diversi vantaggi importanti.</span><span class="sxs-lookup"><span data-stu-id="8b465-105">This integration provides several important benefits.</span></span> <span data-ttu-id="8b465-106">È possibile:</span><span class="sxs-lookup"><span data-stu-id="8b465-106">You can:</span></span>

- <span data-ttu-id="8b465-107">Controllo di Azure AD che dispone dell'accesso toovxMaintain.</span><span class="sxs-lookup"><span data-stu-id="8b465-107">Control in Azure AD who has access toovxMaintain.</span></span>
- <span data-ttu-id="8b465-108">Abilitare l'accesso agli utenti tooautomatically toovxMaintain con single sign-on (SSO) utilizzando gli account di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b465-108">Enable your users tooautomatically sign in toovxMaintain with single sign-on (SSO) by using their Azure AD accounts.</span></span>
- <span data-ttu-id="8b465-109">Gestire gli account in un'unica posizione centrale: hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8b465-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="8b465-110">toolearn più sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8b465-110">toolearn more about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b465-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8b465-111">Prerequisites</span></span>

<span data-ttu-id="8b465-112">integrazione di Azure AD con vxMaintain tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8b465-112">tooconfigure Azure AD integration with vxMaintain, you need hello following items:</span></span>

- <span data-ttu-id="8b465-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b465-113">An Azure AD subscription</span></span>
- <span data-ttu-id="8b465-114">Sottoscrizione di vxMaintain abilitata per l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="8b465-114">A vxMaintain SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b465-115">Quando si testano passaggi hello in questa esercitazione, è consigliabile non utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8b465-115">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="8b465-116">passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:</span><span class="sxs-lookup"><span data-stu-id="8b465-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="8b465-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8b465-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8b465-118">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b465-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b465-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8b465-119">Scenario description</span></span>
<span data-ttu-id="8b465-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8b465-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="8b465-121">scenario di Hello cui sono illustrati in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="8b465-121">hello scenario that this tutorial outlines consists of two main building blocks:</span></span>

* <span data-ttu-id="8b465-122">Aggiunta di vxMaintain dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8b465-122">Adding vxMaintain from hello gallery</span></span>
* <span data-ttu-id="8b465-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b465-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-vxmaintain-from-hello-gallery"></a><span data-ttu-id="8b465-124">Aggiungere vxMaintain dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="8b465-124">Add vxMaintain from hello gallery</span></span>
<span data-ttu-id="8b465-125">integrazione di hello tooconfigure di vxMaintain con Azure AD, è necessario vxMaintain tooadd dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8b465-125">tooconfigure hello integration of vxMaintain with Azure AD, you need tooadd vxMaintain from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8b465-126">vxMaintain tooadd dalla raccolta di hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b465-126">tooadd vxMaintain from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="8b465-127">In hello [portale di Azure](https://portal.azure.com), nel riquadro sinistro di hello, selezionare hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8b465-127">In hello [Azure portal](https://portal.azure.com), in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="8b465-129">Selezionare **Applicazioni aziendali** > **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8b465-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![riquadro "Applicazioni aziendali" Hello][2]
    
3. <span data-ttu-id="8b465-131">un'applicazione, in hello tooadd **tutte le applicazioni** nella finestra di dialogo **nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="8b465-131">tooadd an application, in hello **All applications** dialog box, select **New application**.</span></span>

    !["Nuova applicazione" Hello pulsante][3]

4. <span data-ttu-id="8b465-133">Nella casella di ricerca hello, digitare **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="8b465-133">In hello search box, type **vxMaintain**.</span></span>

    ![elenco a discesa "Modalità Single Sign-on" Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. <span data-ttu-id="8b465-135">Selezionare dall'elenco risultati hello **vxMaintain**, quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8b465-135">In hello results list, select **vxMaintain**, and then select **Add**.</span></span>

    ![collegamento vxMaintain Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8b465-137">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b465-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8b465-138">In questa sezione viene configurato e testato l'accesso SSO di Azure AD con vxMaintain usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8b465-138">In this section, you configure and test Azure AD SSO by using vxMaintain, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8b465-139">Per toowork SSO, Azure AD deve utente di Azure AD toohello vxMaintain controparte tooknow hello.</span><span class="sxs-lookup"><span data-stu-id="8b465-139">For SSO toowork, Azure AD needs tooknow hello vxMaintain counterpart toohello Azure AD user.</span></span> <span data-ttu-id="8b465-140">Ovvero, è necessario stabilire una relazione di collegamento tra utenti di Azure AD hello e utente vxMaintain corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="8b465-140">That is, you must establish a link relationship between hello Azure AD user and hello corresponding vxMaintain user.</span></span>

<span data-ttu-id="8b465-141">relazione di collegamento hello tooestablish, assegnare hello vxMaintain **nome utente** valore come hello Azure AD **Username** valore.</span><span class="sxs-lookup"><span data-stu-id="8b465-141">tooestablish hello link relationship, assign hello vxMaintain **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="8b465-142">tooconfigure e SSO AD Azure tramite vxMaintain, hello completo seguenti blocchi predefiniti di test.</span><span class="sxs-lookup"><span data-stu-id="8b465-142">tooconfigure and test Azure AD SSO by using vxMaintain, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="8b465-143">Configurare l'accesso SSO di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b465-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="8b465-144">In questa sezione, è possibile abilitare SSO AD Azure nel portale di Azure hello e configurare SSO nell'applicazione vxMaintain eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b465-144">In this section, you can both enable Azure AD SSO in hello Azure portal and configure SSO in your vxMaintain application by doing hello following:</span></span>

1. <span data-ttu-id="8b465-145">Nel portale di Azure su hello hello **vxMaintain** pagina di integrazione dell'applicazione, seleziona **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8b465-145">In hello Azure portal, on hello **vxMaintain** application integration page, select **Single sign-on**.</span></span>

    ![comando "Single sign-on" Hello][4]

2. <span data-ttu-id="8b465-147">tooenable SSO, in hello **modalità Single Sign-on** elenco a discesa, seleziona **basato su SAML Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8b465-147">tooenable SSO, in hello **Single Sign-on Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![comando "SAML-Sign-on basato su" Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. <span data-ttu-id="8b465-149">In **vxMaintain dominio e gli URL**, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b465-149">Under **vxMaintain Domain and URLs**, do hello following:</span></span>

    ![Hello vxMaintain sezione URL e di dominio](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    <span data-ttu-id="8b465-151">a.</span><span class="sxs-lookup"><span data-stu-id="8b465-151">a.</span></span> <span data-ttu-id="8b465-152">In hello **identificatore** casella, digitare un URL che ha hello la seguente sintassi:`https://<company name>.verisae.com`</span><span class="sxs-lookup"><span data-stu-id="8b465-152">In hello **Identifier** box, type a URL that has hello following syntax: `https://<company name>.verisae.com`</span></span>

    <span data-ttu-id="8b465-153">b.</span><span class="sxs-lookup"><span data-stu-id="8b465-153">b.</span></span> <span data-ttu-id="8b465-154">In hello **URL di risposta** casella, digitare un URL che ha hello la seguente sintassi:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span><span class="sxs-lookup"><span data-stu-id="8b465-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8b465-155">Hello valori precedenti non sono reali.</span><span class="sxs-lookup"><span data-stu-id="8b465-155">hello preceding values are not real.</span></span> <span data-ttu-id="8b465-156">Aggiornarli con identificatore effettivo hello e URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="8b465-156">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="8b465-157">i valori hello tooobtain, hello contatto [team di supporto vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="8b465-157">tooobtain hello values, contact hello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>
 
4. <span data-ttu-id="8b465-158">In **certificato di firma SAML**selezionare **Metadata XML**e quindi salvare computer tooyour file dei metadati di hello.</span><span class="sxs-lookup"><span data-stu-id="8b465-158">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file tooyour computer.</span></span>

    ![la sezione "Certificato di firma SAML" Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. <span data-ttu-id="8b465-160">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8b465-160">Select **Save**.</span></span>

    ![pulsante Salva Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8b465-162">tooconfigure **vxMaintain** SSO, hello trasmissione scaricato **Metadata XML** file toohello [team di supporto vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="8b465-162">tooconfigure **vxMaintain** SSO, send hello downloaded **Metadata XML** file toohello [vxMaintain support team](http://www.verisae.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="8b465-163">Per la configurazione di app hello, è possibile leggere una versione di hello precedenti istruzioni in hello concisa [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8b465-163">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8b465-164">Dopo aver aggiunto l'applicazione hello da hello **Active Directory** > **applicazioni aziendali** sezione, seleziona hello **Single Sign-On** e quindi hello accesso documentazione fornita dal hello incorporato **configurazione** sezione.</span><span class="sxs-lookup"><span data-stu-id="8b465-164">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab, and then access hello embedded documentation from hello **Configuration** section.</span></span> 
>
><span data-ttu-id="8b465-165">toolearn più feature hello documentazione incorporati, vedere [gestione di single sign-on per le app aziendali](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="8b465-165">toolearn more about hello embedded documentation feature, see [Managing single sign-on for enterprise apps](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8b465-166">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b465-166">Create an Azure AD test user</span></span>
<span data-ttu-id="8b465-167">In questa sezione è creare utente test Britta Simon nel portale di Azure hello eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b465-167">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![utente test hello Azure AD][100]

1. <span data-ttu-id="8b465-169">In hello **portale di Azure**, nel riquadro sinistro di hello, selezionare hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8b465-169">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![pulsante "Azure Active Directory" Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8b465-171">toodisplay un elenco di utenti, andare troppo**utenti e gruppi** > **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="8b465-171">toodisplay a list of users, go too**Users and groups** > **All users**.</span></span>
    
    <span data-ttu-id="8b465-172">![collegano Hello "Tutti gli utenti"](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span><span class="sxs-lookup"><span data-stu-id="8b465-172">![hello "All users" link](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)</span></span>  
    <span data-ttu-id="8b465-173">Hello **tutti gli utenti** verrà visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8b465-173">hello **All users** dialog box opens.</span></span> 

3. <span data-ttu-id="8b465-174">hello tooopen **utente** nella finestra di dialogo **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8b465-174">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8b465-176">In hello **utente** finestra di dialogo casella, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b465-176">In hello **User** dialog box, do hello following:</span></span>
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8b465-178">a.</span><span class="sxs-lookup"><span data-stu-id="8b465-178">a.</span></span> <span data-ttu-id="8b465-179">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8b465-179">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b465-180">b.</span><span class="sxs-lookup"><span data-stu-id="8b465-180">b.</span></span> <span data-ttu-id="8b465-181">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente di prova Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8b465-181">In hello **User name** box, type hello email address of test user Britta Simon.</span></span>

    <span data-ttu-id="8b465-182">c.</span><span class="sxs-lookup"><span data-stu-id="8b465-182">c.</span></span> <span data-ttu-id="8b465-183">Seleziona hello **Show Password** casella di controllo, quindi valore hello si noti che è stato generato in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="8b465-183">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="8b465-184">d.</span><span class="sxs-lookup"><span data-stu-id="8b465-184">d.</span></span> <span data-ttu-id="8b465-185">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8b465-185">Select **Create**.</span></span>
 
### <a name="create-a-vxmaintain-test-user"></a><span data-ttu-id="8b465-186">Creare un utente di test di vxMaintain</span><span class="sxs-lookup"><span data-stu-id="8b465-186">Create a vxMaintain test user</span></span>

<span data-ttu-id="8b465-187">In questa sezione viene creato un utente di test di nome Britta Simon in vxMaintain.</span><span class="sxs-lookup"><span data-stu-id="8b465-187">In this section, you create test user Britta Simon in vxMaintain.</span></span> <span data-ttu-id="8b465-188">gli utenti tooadd nella piattaforma vxMaintain hello, utilizzare il [team di supporto vxMaintain](http://www.verisae.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="8b465-188">tooadd users in hello vxMaintain platform, work with the [vxMaintain support team](http://www.verisae.com/contact-us).</span></span> <span data-ttu-id="8b465-189">Prima di utilizzare SSO, creare e attivare gli utenti di hello.</span><span class="sxs-lookup"><span data-stu-id="8b465-189">Before you use SSO, create and activate hello users.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8b465-190">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b465-190">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8b465-191">In questa sezione per abilitare l'utente test Britta Simon toouse SSO di Azure concessione dell'accesso toovxMaintain.</span><span class="sxs-lookup"><span data-stu-id="8b465-191">In this section, you enable test user Britta Simon toouse Azure SSO by granting access toovxMaintain.</span></span> <span data-ttu-id="8b465-192">toodo in tal caso, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8b465-192">toodo so, do hello following:</span></span>

![Utente test nell'elenco nome visualizzato hello][200] 

1. <span data-ttu-id="8b465-194">Nel portale di Azure hello **applicazioni** visualizzare, andare troppo**Directory** Vista > **applicazioni aziendali** > **tutteleapplicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8b465-194">In hello Azure portal **Applications** view, go too**Directory** view > **Enterprise applications** > **All applications**.</span></span>

    ![collegano Hello "Tutte le applicazioni"][201] 

2. <span data-ttu-id="8b465-196">In hello **applicazioni** elenco, selezionare **vxMaintain**.</span><span class="sxs-lookup"><span data-stu-id="8b465-196">In hello **Applications** list, select **vxMaintain**.</span></span>

    ![collegamento vxMaintain Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. <span data-ttu-id="8b465-198">Nel riquadro sinistro hello selezionare **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8b465-198">In hello left pane, select **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. <span data-ttu-id="8b465-200">Selezionare **Aggiungi** e quindi nel hello **Aggiungi** riquadro, selezionare **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8b465-200">Select **Add** and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][203]

5. <span data-ttu-id="8b465-202">In hello **utenti e gruppi** della finestra di dialogo hello **utenti** elenco, selezionare **Britta Simon**, quindi selezionare hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8b465-202">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**, and then select hello **Select** button.</span></span>

7. <span data-ttu-id="8b465-203">In hello **Aggiungi** nella finestra di dialogo **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="8b465-203">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-your-azure-ad-single-sign-on"></a><span data-ttu-id="8b465-204">Testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b465-204">Test your Azure AD single sign-on</span></span>

<span data-ttu-id="8b465-205">In questa sezione verificare la configurazione di SSO AD Azure tramite hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8b465-205">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="8b465-206">Se si seleziona hello **vxMaintain** riquadro nel Pannello di accesso hello deve eseguire l'accesso tooyour vxMaintain applicazione automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8b465-206">Selecting hello **vxMaintain** tile in hello Access Panel should sign you in tooyour vxMaintain application automatically.</span></span>

<span data-ttu-id="8b465-207">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8b465-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b465-208">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8b465-208">Next steps</span></span>

* [<span data-ttu-id="8b465-209">Elenco di esercitazioni sull'integrazione delle app SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b465-209">List of tutorials on integrating SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b465-210">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b465-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

