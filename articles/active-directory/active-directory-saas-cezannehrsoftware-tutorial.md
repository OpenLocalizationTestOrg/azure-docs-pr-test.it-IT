---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cezanne HR Software | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e delle risorse Umane Cezanne software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="72b81-103">Esercitazione: Eseguire l'integrazione di Azure Active Directory con Cezanne HR Software</span><span class="sxs-lookup"><span data-stu-id="72b81-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="72b81-104">In questa esercitazione, è illustrato come toointegrate Cezanne HR software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="72b81-104">In this tutorial, you learn how toointegrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="72b81-105">Integrazione delle risorse Umane Cezanne software con Azure AD fornisce hello seguenti vantaggi.</span><span class="sxs-lookup"><span data-stu-id="72b81-105">Integrating Cezanne HR software with Azure AD provides you with hello following benefits.</span></span> <span data-ttu-id="72b81-106">È possibile:</span><span class="sxs-lookup"><span data-stu-id="72b81-106">You can:</span></span>

- <span data-ttu-id="72b81-107">Controllo di Azure AD che ha accesso tooCezanne software delle risorse Umane.</span><span class="sxs-lookup"><span data-stu-id="72b81-107">Control in Azure AD who has access tooCezanne HR software.</span></span>
- <span data-ttu-id="72b81-108">Abilitare l'accesso agli utenti tooautomatically software tooCezanne HR con single sign-on (SSO) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72b81-108">Enable your users tooautomatically sign in tooCezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="72b81-109">Gestire gli account in un'unica posizione centrale: hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="72b81-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="72b81-110">toolearn ulteriori informazioni su software come un servizio (SaaS) integrazione dell'applicazione con Azure AD, vedere [novità di accesso all'applicazione e SSO con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="72b81-110">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72b81-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="72b81-111">Prerequisites</span></span>

<span data-ttu-id="72b81-112">integrazione di Azure AD con HR Cezanne software tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="72b81-112">tooconfigure Azure AD integration with Cezanne HR software, you need hello following items:</span></span>

- <span data-ttu-id="72b81-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72b81-113">An Azure AD subscription</span></span>
- <span data-ttu-id="72b81-114">Sottoscrizione di Cezanne HR Software abilitata per l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="72b81-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="72b81-115">passaggi di hello tootest in questa esercitazione, è consigliabile non utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="72b81-115">tootest hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="72b81-116">passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:</span><span class="sxs-lookup"><span data-stu-id="72b81-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="72b81-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="72b81-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="72b81-118">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72b81-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="72b81-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="72b81-119">Scenario description</span></span>
<span data-ttu-id="72b81-120">In questa esercitazione viene testato l'accesso SSO di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="72b81-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="72b81-121">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="72b81-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="72b81-122">Aggiunta delle risorse Umane Cezanne software dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="72b81-122">Adding Cezanne HR software from hello gallery</span></span>
* <span data-ttu-id="72b81-123">Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="72b81-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-hello-gallery"></a><span data-ttu-id="72b81-124">Aggiungere Cezanne HR software dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="72b81-124">Add Cezanne HR software from hello gallery</span></span>
<span data-ttu-id="72b81-125">integrazione di hello tooconfigure di software Cezanne HR in Azure AD, aggiungere software Cezanne HR hello raccolta tooyour elenco di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="72b81-125">tooconfigure hello integration of Cezanne HR software into Azure AD, add Cezanne HR software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="72b81-126">tooadd Cezanne HR software dalla raccolta di hello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="72b81-126">tooadd Cezanne HR software from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="72b81-127">In hello  **[portale di Azure](https://portal.azure.com)**, nel riquadro sinistro di hello, selezionare hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="72b81-127">In hello **[Azure portal](https://portal.azure.com)**, in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![pulsante "Azure Active Directory" Hello][1]

2. <span data-ttu-id="72b81-129">Selezionare **Applicazioni aziendali** > **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="72b81-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![collegano Hello "Tutte le applicazioni"][2]
    
3. <span data-ttu-id="72b81-131">una nuova applicazione, nella parte superiore di hello di hello tooadd **tutte le applicazioni** nella finestra di dialogo **nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="72b81-131">tooadd a new application, at hello top of hello **All applications** dialog box, select **New application**.</span></span>

    !["Nuova applicazione" Hello pulsante][3]

4. <span data-ttu-id="72b81-133">Nella casella di ricerca hello, digitare **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="72b81-133">In hello search box, type **Cezanne HR Software**.</span></span>

    ![casella di ricerca Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="72b81-135">Selezionare dall'elenco risultati hello **Cezanne HR Software** e quindi selezionare hello **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="72b81-135">In hello results list, select **Cezanne HR Software** and then select hello **Add** button tooadd hello application.</span></span>

    ![elenco dei risultati Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="72b81-137">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="72b81-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="72b81-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Cezanne HR Software usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="72b81-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="72b81-139">Per toowork SSO, Azure AD deve tooknow hello HR Cezanne software controparte toohello Azure utente di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="72b81-139">For SSO toowork, Azure AD needs tooknow hello Cezanne HR software counterpart toohello Azure AD user.</span></span> <span data-ttu-id="72b81-140">In altre parole, è necessario stabilire una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello in hello HR Cezanne software.</span><span class="sxs-lookup"><span data-stu-id="72b81-140">In other words, you must establish a link relationship between an Azure AD user and hello related user in hello Cezanne HR software.</span></span>

<span data-ttu-id="72b81-141">relazione di collegamento hello tooestablish, assegnare hello software HR Cezanne **nome utente** valore come hello Azure AD **Username** valore.</span><span class="sxs-lookup"><span data-stu-id="72b81-141">tooestablish hello link relationship, assign hello Cezanne HR software **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="72b81-142">tooconfigure e SSO AD Azure tramite software Cezanne HR, hello completo seguenti blocchi predefiniti di test.</span><span class="sxs-lookup"><span data-stu-id="72b81-142">tooconfigure and test Azure AD SSO by using Cezanne HR software, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="72b81-143">Configurare l'accesso SSO di Azure AD</span><span class="sxs-lookup"><span data-stu-id="72b81-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="72b81-144">In questa sezione, è possibile abilitare SSO AD Azure nel portale di Azure hello e configurare SSO HR Cezanne nell'applicazione in uso eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="72b81-144">In this section, you can enable Azure AD SSO in hello Azure portal and configure SSO in your Cezanne HR software application by doing hello following:</span></span>

1. <span data-ttu-id="72b81-145">Nel portale di Azure su hello hello **Cezanne HR Software** pagina di integrazione dell'applicazione, seleziona **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="72b81-145">In hello Azure portal, on hello **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![comando "Single sign-on" Hello][4]

2. <span data-ttu-id="72b81-147">tooenable SSO, in hello **Single sign-on** la finestra di dialogo, seleziona hello **modalità** come **basato su SAML Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="72b81-147">tooenable SSO, in hello **Single sign-on** dialog box, select hello **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![casella "Modalità di" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="72b81-149">In **Cezanne HR Software dominio e gli URL**, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="72b81-149">Under **Cezanne HR Software Domain and URLs**, do hello following:</span></span>

    ![la sezione "Cezanne HR Software dominio e gli URL" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="72b81-151">a.</span><span class="sxs-lookup"><span data-stu-id="72b81-151">a.</span></span> <span data-ttu-id="72b81-152">In hello **Sign-on URL** casella, digitare un URL che ha hello la seguente sintassi:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="72b81-152">In hello **Sign-on URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="72b81-153">b.</span><span class="sxs-lookup"><span data-stu-id="72b81-153">b.</span></span> <span data-ttu-id="72b81-154">In hello **URL di risposta** casella, digitare un URL che ha hello la seguente sintassi:`https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="72b81-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="72b81-155">Hello valori precedenti non sono reali.</span><span class="sxs-lookup"><span data-stu-id="72b81-155">hello preceding values are not real.</span></span> <span data-ttu-id="72b81-156">Poterli aggiornare con l'URL di risposta effettivo hello e URL hello-sign-on.</span><span class="sxs-lookup"><span data-stu-id="72b81-156">Update them with hello actual reply URL and hello sign-on URL.</span></span> <span data-ttu-id="72b81-157">i valori hello tooobtain, hello contatto [team di supporto client software HR Cezanne](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="72b81-157">tooobtain hello values, contact hello [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="72b81-158">In **certificato di firma SAML**selezionare **certificato (Base64)**e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="72b81-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![la sezione "Certificato di firma SAML" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="72b81-160">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="72b81-160">Select **Save**.</span></span>

    ![pulsante "Salva" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="72b81-162">In **Cezanne HR Software configurazione**selezionare **Configura Cezanne HR Software** tooopen hello **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="72b81-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="72b81-163">Hello copia **ID entità SAML** e **SAML Single Sign-On Service** URL da hello **riferimento rapido** sezione.</span><span class="sxs-lookup"><span data-stu-id="72b81-163">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service** URL from hello **Quick Reference** section.</span></span>

    ![sezione "Configurazione di Software Cezanne HR" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="72b81-165">In una finestra del web browser, accedere tooyour Cezanne HR di tenant di software come amministratore.</span><span class="sxs-lookup"><span data-stu-id="72b81-165">In a different web browser window, sign on tooyour Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="72b81-166">Nel riquadro sinistro hello selezionare **installazione System**.</span><span class="sxs-lookup"><span data-stu-id="72b81-166">In hello left pane, select **System Setup**.</span></span> <span data-ttu-id="72b81-167">Selezionare **Security Settings** > **Single Sign-On Configuration** (Impostazioni di sicurezza > Configurazione Single Sign-on).</span><span class="sxs-lookup"><span data-stu-id="72b81-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![collegamento di "Configurazione Single Sign-On" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="72b81-169">In hello **consentire agli utenti toolog hello seguenti servizi Single Sign-On (SSO) con** riquadro, seleziona hello **SAML 2.0** casella di controllo e seleziona hello **configurazione avanzata** opzione.</span><span class="sxs-lookup"><span data-stu-id="72b81-169">In hello **Allow users toolog in using hello following Single Sign-On (SSO) services** pane, select hello **SAML 2.0** check box and select hello **Advanced Configuration** option.</span></span>

    ![Opzioni dei servizi Single Sign-On](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="72b81-171">Selezionare **Add New** (Aggiungi nuovo).</span><span class="sxs-lookup"><span data-stu-id="72b81-171">Select **Add New**.</span></span>

    ![pulsante "Aggiungi" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="72b81-173">In **provider di identità SAML 2.0**, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="72b81-173">Under **SAML 2.0 Identity Providers**, do hello following:</span></span>

    ![la sezione "Provider di identità SAML 2.0" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="72b81-175">a.</span><span class="sxs-lookup"><span data-stu-id="72b81-175">a.</span></span> <span data-ttu-id="72b81-176">In hello **nome visualizzato** , immettere il nome di hello del provider di identità.</span><span class="sxs-lookup"><span data-stu-id="72b81-176">In hello **Display Name** box, enter hello name of your identity provider.</span></span>

    <span data-ttu-id="72b81-177">b.</span><span class="sxs-lookup"><span data-stu-id="72b81-177">b.</span></span> <span data-ttu-id="72b81-178">In hello **identificatore dell'entità** incollare hello **ID entità SAML** copiato dalla hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="72b81-178">In hello **Entity Identifier** box, paste hello **SAML Entity ID** that you copied from hello Azure portal.</span></span> 

    <span data-ttu-id="72b81-179">c.</span><span class="sxs-lookup"><span data-stu-id="72b81-179">c.</span></span> <span data-ttu-id="72b81-180">In hello **SAML associazione** casella di riepilogo, seleziona **POST**.</span><span class="sxs-lookup"><span data-stu-id="72b81-180">In hello **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="72b81-181">d.</span><span class="sxs-lookup"><span data-stu-id="72b81-181">d.</span></span> <span data-ttu-id="72b81-182">In hello **Endpoint del servizio Token di sicurezza** incollare hello **servizio SAML Single Sign-On** URL copiato da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="72b81-182">In hello **Security Token Service Endpoint** box, paste hello **SAML Single Sign-On Service** URL that you copied from hello Azure portal.</span></span> 
    
    <span data-ttu-id="72b81-183">e.</span><span class="sxs-lookup"><span data-stu-id="72b81-183">e.</span></span> <span data-ttu-id="72b81-184">In hello **nome dell'attributo ID utente** immettere `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="72b81-184">In hello **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="72b81-185">f.</span><span class="sxs-lookup"><span data-stu-id="72b81-185">f.</span></span> <span data-ttu-id="72b81-186">hello tooupload scaricato certificato da Azure AD, seleziona hello **caricare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="72b81-186">tooupload hello downloaded certificate from Azure AD, select hello **Upload** button.</span></span>
    
    <span data-ttu-id="72b81-187">g.</span><span class="sxs-lookup"><span data-stu-id="72b81-187">g.</span></span> <span data-ttu-id="72b81-188">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="72b81-188">Select **OK**.</span></span> 

12. <span data-ttu-id="72b81-189">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="72b81-189">Select **Save**.</span></span>

    ![pulsante "Salva" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="72b81-191">Per la configurazione di app hello, è possibile leggere una versione di hello precedenti istruzioni in hello concisa [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="72b81-191">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="72b81-192">Dopo aver aggiunto l'applicazione hello da hello **Active Directory** > **applicazioni aziendali** sezione, seleziona hello **Single sign-on** scheda. Quindi hello accesso incorporati documentazione da hello **configurazione** sezione.</span><span class="sxs-lookup"><span data-stu-id="72b81-192">After you add hello app from hello **Active Directory** > **Enterprise applications** section, select hello **Single sign-on** tab. Then access hello embedded documentation from hello **Configuration** section.</span></span> 

<span data-ttu-id="72b81-193">toolearn più feature hello documentazione incorporati, vedere [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="72b81-193">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="72b81-194">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="72b81-194">Create an Azure AD test user</span></span>
<span data-ttu-id="72b81-195">In questa sezione è creare test utente Britta Simon hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="72b81-195">In this section, you create test user Britta Simon in hello Azure portal.</span></span>

![utente test hello Britta Simon][100]

<span data-ttu-id="72b81-197">un utente di prova in Azure AD, toocreate hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="72b81-197">toocreate a test user in Azure AD, do hello following:</span></span>

1. <span data-ttu-id="72b81-198">In hello **portale di Azure**, nel riquadro sinistro di hello, selezionare hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="72b81-198">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![pulsante "Azure Active Directory" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="72b81-200">elenco di hello toodisplay di utenti, selezionare **utenti e gruppi** > **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="72b81-200">toodisplay hello list of users, select **Users and groups** > **All users**.</span></span>
    
    ![collegano Hello "Tutti gli utenti"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="72b81-202">Hello **tutti gli utenti** verrà visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="72b81-202">hello **All users** dialog box opens.</span></span>

3. <span data-ttu-id="72b81-203">hello tooopen **utente** nella finestra di dialogo **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="72b81-203">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![pulsante "Aggiungi" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="72b81-205">In hello **utente** finestra di dialogo casella, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="72b81-205">In hello **User** dialog box, do hello following:</span></span>
 
    ![finestra di dialogo "User" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="72b81-207">a.</span><span class="sxs-lookup"><span data-stu-id="72b81-207">a.</span></span> <span data-ttu-id="72b81-208">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="72b81-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="72b81-209">b.</span><span class="sxs-lookup"><span data-stu-id="72b81-209">b.</span></span> <span data-ttu-id="72b81-210">In hello **nome utente** digitare utente Britta Simon **indirizzo di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="72b81-210">In hello **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="72b81-211">c.</span><span class="sxs-lookup"><span data-stu-id="72b81-211">c.</span></span> <span data-ttu-id="72b81-212">Seleziona hello **Show Password** casella di controllo, quindi valore hello si noti che è stato generato in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="72b81-212">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="72b81-213">d.</span><span class="sxs-lookup"><span data-stu-id="72b81-213">d.</span></span> <span data-ttu-id="72b81-214">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="72b81-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="72b81-215">Creare un utente di test di Cezanne HR Software</span><span class="sxs-lookup"><span data-stu-id="72b81-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="72b81-216">toosign agli utenti di Azure AD tooenable nel software tooCezanne HR, deve disporre delle risorse Umane Cezanne software.</span><span class="sxs-lookup"><span data-stu-id="72b81-216">tooenable Azure AD users toosign in tooCezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="72b81-217">In caso di hello del software Cezanne HR, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="72b81-217">In hello case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="72b81-218">Eseguire il provisioning di un account utente eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="72b81-218">Provision a user account by doing hello following:</span></span>

1.  <span data-ttu-id="72b81-219">Accedi tooyour Cezanne HR sito società di software come amministratore.</span><span class="sxs-lookup"><span data-stu-id="72b81-219">Sign in tooyour Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="72b81-220">Nel riquadro sinistro hello selezionare **installazione System** > **Gestisci utenti** > **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="72b81-220">In hello left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="72b81-221">![collegamento "Aggiungi nuovo utente" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="72b81-221">![hello "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="72b81-222">In **dettagli persona**, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="72b81-222">Under **Person Details**, do hello following:</span></span>

    <span data-ttu-id="72b81-223">![sezione "Dettagli persona" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="72b81-223">![hello "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="72b81-224">a.</span><span class="sxs-lookup"><span data-stu-id="72b81-224">a.</span></span> <span data-ttu-id="72b81-225">Impostare **Internal User** (Utente interno) su **OFF**.</span><span class="sxs-lookup"><span data-stu-id="72b81-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="72b81-226">b.</span><span class="sxs-lookup"><span data-stu-id="72b81-226">b.</span></span> <span data-ttu-id="72b81-227">In hello **nome** casella, tipo hello nome dell'utente, ad esempio, **Laura**.</span><span class="sxs-lookup"><span data-stu-id="72b81-227">In hello **First Name** box, type hello user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="72b81-228">c.</span><span class="sxs-lookup"><span data-stu-id="72b81-228">c.</span></span> <span data-ttu-id="72b81-229">In hello **cognome** casella, tipo hello cognome dell'utente, ad esempio, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="72b81-229">In hello **Last Name** box, type hello user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="72b81-230">d.</span><span class="sxs-lookup"><span data-stu-id="72b81-230">d.</span></span> <span data-ttu-id="72b81-231">In hello **posta elettronica** , digitare, ad esempio, l'indirizzo di posta elettronica dell'utente hello Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="72b81-231">In hello **E-mail** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="72b81-232">In **informazioni sull'Account**, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="72b81-232">Under **Account Information**, do hello following:</span></span>

    <span data-ttu-id="72b81-233">![la sezione "Informazioni sull'Account" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="72b81-233">![hello "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="72b81-234">a.</span><span class="sxs-lookup"><span data-stu-id="72b81-234">a.</span></span> <span data-ttu-id="72b81-235">In hello **Username** , digitare, ad esempio, l'indirizzo di posta elettronica dell'utente hello Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="72b81-235">In hello **Username** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="72b81-236">b.</span><span class="sxs-lookup"><span data-stu-id="72b81-236">b.</span></span> <span data-ttu-id="72b81-237">In hello **Password** , digitare la password dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="72b81-237">In hello **Password** box, type hello user's password.</span></span>
    
    <span data-ttu-id="72b81-238">c.</span><span class="sxs-lookup"><span data-stu-id="72b81-238">c.</span></span> <span data-ttu-id="72b81-239">In hello **ruolo di sicurezza** , quindi selezionare **Professional HR**.</span><span class="sxs-lookup"><span data-stu-id="72b81-239">In hello **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="72b81-240">d.</span><span class="sxs-lookup"><span data-stu-id="72b81-240">d.</span></span> <span data-ttu-id="72b81-241">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="72b81-241">Select **OK**.</span></span>

5. <span data-ttu-id="72b81-242">In hello **Single sign-on** scheda hello **identificatori di SAML 2.0** selezionare **Aggiungi nuovo**.</span><span class="sxs-lookup"><span data-stu-id="72b81-242">On hello **Single sign-on** tab, in hello **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="72b81-243">![pulsante "Aggiungi" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "utente")</span><span class="sxs-lookup"><span data-stu-id="72b81-243">![hello "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="72b81-244">In hello **Provider di identità** nella casella di riepilogo, selezionare il provider di identità.</span><span class="sxs-lookup"><span data-stu-id="72b81-244">In hello **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="72b81-245">In hello **identificatore utente** , immettere l'indirizzo di posta elettronica hello per account di prova utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="72b81-245">In hello **User Identifier** box, enter hello email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="72b81-246">![Hello caselle "Provider di identità" e "ID utente"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "utente")</span><span class="sxs-lookup"><span data-stu-id="72b81-246">![hello "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="72b81-247">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="72b81-247">Select **Save**.</span></span>

    <span data-ttu-id="72b81-248">![pulsante "Salva" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "utente")</span><span class="sxs-lookup"><span data-stu-id="72b81-248">![hello "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="72b81-249">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="72b81-249">Assign hello Azure AD test user</span></span>

<span data-ttu-id="72b81-250">In questa sezione per abilitare l'utente test Britta Simon toouse SSO di Azure concessione dell'accesso tooCezanne HR software.</span><span class="sxs-lookup"><span data-stu-id="72b81-250">In this section, you enable test user Britta Simon toouse Azure SSO by granting access tooCezanne HR software.</span></span>

![Accesso utente di test][200] 

1. <span data-ttu-id="72b81-252">Nel portale di Azure hello, aprire visualizzazione applicazioni hello e quindi passare visualizzazione directory toohello.</span><span class="sxs-lookup"><span data-stu-id="72b81-252">In hello Azure portal, open hello applications view and then go toohello directory view.</span></span> <span data-ttu-id="72b81-253">Selezionare **Applicazioni aziendali** > **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="72b81-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![collegano Hello "Tutte le applicazioni"][201] 

2. <span data-ttu-id="72b81-255">Nell'elenco di applicazioni hello, selezionare **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="72b81-255">In hello applications list, select **Cezanne HR Software**.</span></span>

    ![elenco di "applicazioni di" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="72b81-257">Dal menu hello hello sinistra, selezionare **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="72b81-257">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Assegnare utenti][202] 

4. <span data-ttu-id="72b81-259">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="72b81-259">Select **Add**.</span></span> <span data-ttu-id="72b81-260">Quindi in hello **Aggiungi** nella finestra di dialogo **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="72b81-260">Then in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Collegamento "Utenti e gruppi"][203]

5. <span data-ttu-id="72b81-262">In hello **utenti e gruppi** della finestra di dialogo hello **utenti** elenco, selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="72b81-262">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="72b81-263">In hello **utenti e gruppi** nella finestra di dialogo **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="72b81-263">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="72b81-264">In hello **Aggiungi** nella finestra di dialogo **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="72b81-264">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="72b81-265">Testare l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="72b81-265">Test SSO</span></span>

<span data-ttu-id="72b81-266">In questa sezione verificare la configurazione di SSO AD Azure tramite hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="72b81-266">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="72b81-267">Quando si seleziona riquadro software Cezanne HR di hello in hello Pannello di accesso, si accede da automaticamente tooyour applicazione software Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="72b81-267">When you select hello Cezanne HR software tile in hello Access Panel, you sign on automatically tooyour Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72b81-268">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="72b81-268">Next steps</span></span>

* [<span data-ttu-id="72b81-269">Elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72b81-269">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="72b81-270">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72b81-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

