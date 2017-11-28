---
title: 'Esercitazione: Integrazione di Azure Active Directory con DocuSign | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e DocuSign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="e7164-103">Esercitazione: Integrazione di Azure Active Directory con DocuSign</span><span class="sxs-lookup"><span data-stu-id="e7164-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="e7164-104">In questa esercitazione, è illustrato come toointegrate DocuSign con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7164-104">In this tutorial, you learn how toointegrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7164-105">Integrazione di DocuSign con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="e7164-105">Integrating DocuSign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e7164-106">È possibile controllare in Azure AD che ha accesso tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="e7164-106">You can control in Azure AD who has access tooDocuSign</span></span>
- <span data-ttu-id="e7164-107">È possibile abilitare l'utenti tooautomatically get connesso tooDocuSign (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7164-107">You can enable your users tooautomatically get signed-on tooDocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7164-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e7164-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e7164-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7164-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7164-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e7164-110">Prerequisites</span></span>

<span data-ttu-id="e7164-111">integrazione di Azure AD con DocuSign tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="e7164-111">tooconfigure Azure AD integration with DocuSign, you need hello following items:</span></span>

- <span data-ttu-id="e7164-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7164-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7164-113">Una sottoscrizione di DocuSign abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e7164-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7164-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="e7164-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7164-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="e7164-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7164-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="e7164-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7164-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7164-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7164-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e7164-118">Scenario description</span></span>
<span data-ttu-id="e7164-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="e7164-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7164-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="e7164-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7164-121">Aggiunta di DocuSign dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e7164-121">Adding DocuSign from hello gallery</span></span>
2. <span data-ttu-id="e7164-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7164-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-hello-gallery"></a><span data-ttu-id="e7164-123">Aggiunta di DocuSign dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e7164-123">Adding DocuSign from hello gallery</span></span>
<span data-ttu-id="e7164-124">integrazione hello tooconfigure di DocuSign in Azure AD, è necessario tooadd DocuSign dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="e7164-124">tooconfigure hello integration of DocuSign into Azure AD, you need tooadd DocuSign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e7164-125">**tooadd DocuSign dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7164-125">**tooadd DocuSign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7164-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="e7164-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e7164-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="e7164-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e7164-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e7164-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="e7164-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="e7164-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="e7164-133">Nella casella di ricerca hello, digitare **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="e7164-133">In hello search box, type **DocuSign**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="e7164-135">Nel riquadro dei risultati hello, selezionare **DocuSign**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e7164-135">In hello results panel, select **DocuSign**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7164-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7164-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7164-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con DocuSign in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e7164-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e7164-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in DocuSign è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7164-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DocuSign is tooa user in Azure AD.</span></span> <span data-ttu-id="e7164-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in DocuSign deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="e7164-140">In other words, a link relationship between an Azure AD user and hello related user in DocuSign needs toobe established.</span></span>

<span data-ttu-id="e7164-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in DocuSign.</span><span class="sxs-lookup"><span data-stu-id="e7164-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in DocuSign.</span></span>

<span data-ttu-id="e7164-142">tooconfigure e test Azure single sign-on AD con DocuSign, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="e7164-142">tooconfigure and test Azure AD single sign-on with DocuSign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e7164-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e7164-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e7164-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7164-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7164-145">**[Creazione di un utente test DocuSign](#creating-a-docusign-test-user)**  -toohave un equivalente di Britta Simon in DocuSign che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e7164-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - toohave a counterpart of Britta Simon in DocuSign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7164-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e7164-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7164-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="e7164-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7164-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7164-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7164-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione DocuSign.</span><span class="sxs-lookup"><span data-stu-id="e7164-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="e7164-150">**Azure AD tooconfigure single sign-on con DocuSign, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7164-150">**tooconfigure Azure AD single sign-on with DocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7164-151">Nel portale di Azure su hello hello **DocuSign** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e7164-151">In hello Azure portal, on hello **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="e7164-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e7164-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="e7164-155">In hello **certificato di firma SAML** fare clic su **certificato (Base 64)** e quindi salvare il file di certificato nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="e7164-155">On hello **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="e7164-157">In hello **DocuSign configurazione** sezione del portale di Azure, fare clic su **DocuSign configurare** finestra tooopen Configura sign-on.</span><span class="sxs-lookup"><span data-stu-id="e7164-157">On hello **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** tooopen Configure sign-on window.</span></span> <span data-ttu-id="e7164-158">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="e7164-158">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="e7164-160">In una finestra del web browser, account di accesso tooyour **il portale di amministrazione di DocuSign** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e7164-160">In a different web browser window, login tooyour **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="e7164-161">Nel menu di navigazione hello hello sinistra, fare clic su **domini**.</span><span class="sxs-lookup"><span data-stu-id="e7164-161">In hello navigation menu on hello left, click **Domains**.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][51]

7. <span data-ttu-id="e7164-163">Nel riquadro di destra hello, fare clic su **dominio attestazione**.</span><span class="sxs-lookup"><span data-stu-id="e7164-163">On hello right pane, click **Claim Domain**.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][52]

8. <span data-ttu-id="e7164-165">In hello **un dominio di attestazioni** finestra di dialogo, in hello **nome di dominio** casella di testo, digitare il dominio aziendale e quindi fare clic su **attestazione**.</span><span class="sxs-lookup"><span data-stu-id="e7164-165">On hello **Claim a domain** dialog, in hello **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="e7164-166">Assicurarsi che si verifica il dominio di hello e hello stato sia attivo.</span><span class="sxs-lookup"><span data-stu-id="e7164-166">Make sure that you verify hello domain and hello status is active.</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][53]

9. <span data-ttu-id="e7164-168">Scegliere dal menu sul lato sinistro hello **provider di identità**</span><span class="sxs-lookup"><span data-stu-id="e7164-168">In menu on hello left side, click **Identity Providers**</span></span>  
   
    ![Configurazione dell'accesso Single Sign-On][54]
10. <span data-ttu-id="e7164-170">Nel riquadro di destra hello, fare clic su **Add Identity Provider**.</span><span class="sxs-lookup"><span data-stu-id="e7164-170">In hello right pane, click **Add Identity Provider**.</span></span> 
   
    ![Configurazione dell'accesso Single Sign-On][55]

11. <span data-ttu-id="e7164-172">In hello **impostazioni del Provider di identità** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e7164-172">On hello **Identity Provider Settings** page, perform hello following steps:</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][56]

    <span data-ttu-id="e7164-174">a.</span><span class="sxs-lookup"><span data-stu-id="e7164-174">a.</span></span> <span data-ttu-id="e7164-175">In hello **nome** casella di testo, digitare un nome univoco per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="e7164-175">In hello **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="e7164-176">Non usare spazi.</span><span class="sxs-lookup"><span data-stu-id="e7164-176">Do not use spaces.</span></span>

    <span data-ttu-id="e7164-177">b.</span><span class="sxs-lookup"><span data-stu-id="e7164-177">b.</span></span> <span data-ttu-id="e7164-178">Incolla **ID entità SAML** in hello **Identity Provider Issuer** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="e7164-178">Paste **SAML Entity ID** into hello **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="e7164-179">c.</span><span class="sxs-lookup"><span data-stu-id="e7164-179">c.</span></span> <span data-ttu-id="e7164-180">Incolla **SAML Single Sign-On Service URL** in hello **Identity Provider Login URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="e7164-180">Paste **SAML Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="e7164-181">d.</span><span class="sxs-lookup"><span data-stu-id="e7164-181">d.</span></span> <span data-ttu-id="e7164-182">Incolla **Sign-Out URL** in hello **Identity Provider Logout URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="e7164-182">Paste **Sign-Out URL** into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="e7164-183">e.</span><span class="sxs-lookup"><span data-stu-id="e7164-183">e.</span></span> <span data-ttu-id="e7164-184">Selezionare **Sign AuthN Request**(Firma richiesta di autenticazione).</span><span class="sxs-lookup"><span data-stu-id="e7164-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="e7164-185">f.</span><span class="sxs-lookup"><span data-stu-id="e7164-185">f.</span></span> <span data-ttu-id="e7164-186">Per **Invia richiesta di autenticazione da** selezionare **POST**.</span><span class="sxs-lookup"><span data-stu-id="e7164-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="e7164-187">g.</span><span class="sxs-lookup"><span data-stu-id="e7164-187">g.</span></span> <span data-ttu-id="e7164-188">Per **Invia richiesta di disconnessione da** selezionare **GET**.</span><span class="sxs-lookup"><span data-stu-id="e7164-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="e7164-189">In hello **Mapping di attributi personalizzati** , scegliere il campo hello desiderato toomap con Azure AD attestazioni.</span><span class="sxs-lookup"><span data-stu-id="e7164-189">In hello **Custom Attribute Mapping** section, choose hello field you want toomap with Azure AD Claim.</span></span> <span data-ttu-id="e7164-190">In questo esempio hello **emailaddress** viene eseguito il mapping di un'attestazione con valore hello **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="e7164-190">In this example, hello **emailaddress** claim is mapped with hello value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="e7164-191">Nome di attestazione predefinito hello da Azure AD per l'attestazione di posta elettronica è.</span><span class="sxs-lookup"><span data-stu-id="e7164-191">It is hello default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="e7164-192">Hello uso appropriato **identificatore utente** utente hello toomap dal mapping utente tooDocuSign di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7164-192">Use hello appropriate **User identifier** toomap hello user from Azure AD tooDocuSign user mapping.</span></span> <span data-ttu-id="e7164-193">Selezionare hello campo appropriato e immettere hello valore appropriato in base alle impostazioni dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="e7164-193">Select hello proper Field and enter hello appropriate value based on your organization settings.</span></span>
          
    ![Configurazione dell'accesso Single Sign-On][57]

13. <span data-ttu-id="e7164-195">In hello **Identity Provider Certificate** fare clic su **Aggiungi certificato**e quindi caricare il certificato di hello scaricato dal portale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7164-195">In hello **Identity Provider Certificate** section, click **Add Certificate**, and then upload hello certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Configurazione dell'accesso Single Sign-On][58]

14. <span data-ttu-id="e7164-197">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e7164-197">Click **Save**.</span></span>

15. <span data-ttu-id="e7164-198">In hello **provider di identità** fare clic su **azioni**, quindi fare clic su **endpoint**.</span><span class="sxs-lookup"><span data-stu-id="e7164-198">In hello **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Configurazione dell'accesso Single Sign-On][59]
 
16. <span data-ttu-id="e7164-200">In hello **Visualizza SAML 2.0 endpoint** sezione **il portale di amministrazione di DocuSign**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e7164-200">In hello **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform hello following steps:</span></span>
   
    ![Configurazione dell'accesso Single Sign-On][60]
   
    <span data-ttu-id="e7164-202">a.</span><span class="sxs-lookup"><span data-stu-id="e7164-202">a.</span></span> <span data-ttu-id="e7164-203">Hello copia **URL autorità di certificazione di servizio Provider**e quindi incollare in hello **identificatore** nella casella di testo **DocuSign dominio e gli URL** sezione di hello Azure hello seguente del portale motivo: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="e7164-203">Copy hello **Service Provider Issuer URL**, and then paste into hello **Identifier** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="e7164-204">b.</span><span class="sxs-lookup"><span data-stu-id="e7164-204">b.</span></span> <span data-ttu-id="e7164-205">Hello copia **Service Provider Login URL**e quindi incollare in hello **URL di accesso** nella casella di testo **DocuSign dominio e gli URL** sezione di hello Azure hello seguente del portale motivo: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="e7164-205">Copy hello **Service Provider Login URL**, and then paste into hello **Sign On URL** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="e7164-207">c.</span><span class="sxs-lookup"><span data-stu-id="e7164-207">c.</span></span>  <span data-ttu-id="e7164-208">Fare clic su **Close**</span><span class="sxs-lookup"><span data-stu-id="e7164-208">Click **Close**</span></span>
    
17. <span data-ttu-id="e7164-209">Nel portale di Azure hello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="e7164-209">On hello Azure portal, click **Save**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="e7164-211">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="e7164-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e7164-212">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="e7164-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e7164-213">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7164-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7164-214">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7164-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7164-215">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="e7164-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="e7164-217">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7164-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7164-218">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="e7164-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7164-220">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="e7164-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7164-222">Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="e7164-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7164-224">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e7164-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7164-226">a.</span><span class="sxs-lookup"><span data-stu-id="e7164-226">a.</span></span> <span data-ttu-id="e7164-227">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7164-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7164-228">b.</span><span class="sxs-lookup"><span data-stu-id="e7164-228">b.</span></span> <span data-ttu-id="e7164-229">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e7164-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7164-230">c.</span><span class="sxs-lookup"><span data-stu-id="e7164-230">c.</span></span> <span data-ttu-id="e7164-231">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="e7164-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e7164-232">d.</span><span class="sxs-lookup"><span data-stu-id="e7164-232">d.</span></span> <span data-ttu-id="e7164-233">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e7164-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="e7164-234">Creazione di un utente test di DocuSign</span><span class="sxs-lookup"><span data-stu-id="e7164-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="e7164-235">Supporta l'applicazione **immediatamente provisioning in-time utente** e dopo l'autenticazione degli utenti viene creato automaticamente in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e7164-235">Application supports **Just in time user provisioning** and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e7164-236">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7164-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e7164-237">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooDocuSign proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="e7164-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooDocuSign.</span></span>

![Assegna utente][200] 

<span data-ttu-id="e7164-239">**tooassign Britta Simon tooDocuSign, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7164-239">**tooassign Britta Simon tooDocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7164-240">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e7164-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="e7164-242">Nell'elenco di applicazioni hello, selezionare **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="e7164-242">In hello applications list, select **DocuSign**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="e7164-244">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e7164-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="e7164-246">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e7164-246">Click **Add** button.</span></span> <span data-ttu-id="e7164-247">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e7164-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="e7164-249">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="e7164-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e7164-250">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e7164-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7164-251">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e7164-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7164-252">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e7164-252">Testing single sign-on</span></span>

<span data-ttu-id="e7164-253">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="e7164-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e7164-254">Quando si fa clic su riquadro DocuSign hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in DocuSign applicazione.</span><span class="sxs-lookup"><span data-stu-id="e7164-254">When you click hello DocuSign tile in hello Access Panel, you should get automatically signed-on tooyour DocuSign application.</span></span>
<span data-ttu-id="e7164-255">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e7164-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e7164-256">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e7164-256">Additional resources</span></span>

* [<span data-ttu-id="e7164-257">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7164-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7164-258">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7164-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e7164-259">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="e7164-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

