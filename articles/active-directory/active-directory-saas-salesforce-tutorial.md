---
title: 'Esercitazione: Integrazione di Azure Active Directory con Salesforce | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Salesforce.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="ea915-103">Esercitazione: Integrazione di Azure Active Directory con Salesforce</span><span class="sxs-lookup"><span data-stu-id="ea915-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="ea915-104">In questa esercitazione, è illustrato come toointegrate Salesforce con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ea915-104">In this tutorial, you learn how toointegrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea915-105">Integrazione di Salesforce con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="ea915-105">Integrating Salesforce with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ea915-106">È possibile controllare in Azure AD che ha accesso tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="ea915-106">You can control in Azure AD who has access tooSalesforce</span></span>
- <span data-ttu-id="ea915-107">È possibile abilitare l'utenti tooautomatically get connesso tooSalesforce (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea915-107">You can enable your users tooautomatically get signed-on tooSalesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ea915-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ea915-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ea915-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ea915-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea915-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ea915-110">Prerequisites</span></span>

<span data-ttu-id="ea915-111">integrazione di Azure AD con Salesforce tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ea915-111">tooconfigure Azure AD integration with Salesforce, you need hello following items:</span></span>

- <span data-ttu-id="ea915-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea915-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ea915-113">Sottoscrizione di Salesforce abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ea915-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ea915-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ea915-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ea915-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="ea915-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ea915-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ea915-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ea915-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea915-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea915-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ea915-118">Scenario description</span></span>
<span data-ttu-id="ea915-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ea915-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ea915-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="ea915-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ea915-121">Aggiunta di Salesforce da raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ea915-121">Adding Salesforce from hello gallery</span></span>
2. <span data-ttu-id="ea915-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea915-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-hello-gallery"></a><span data-ttu-id="ea915-123">Aggiunta di Salesforce da raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ea915-123">Adding Salesforce from hello gallery</span></span>
<span data-ttu-id="ea915-124">integrazione hello tooconfigure di Salesforce in Azure AD, è necessario tooadd Salesforce dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ea915-124">tooconfigure hello integration of Salesforce into Azure AD, you need tooadd Salesforce from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ea915-125">**tooadd Salesforce dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ea915-125">**tooadd Salesforce from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea915-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ea915-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ea915-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ea915-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ea915-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ea915-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="ea915-131">Fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="ea915-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="ea915-133">Nella casella di ricerca hello, digitare **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="ea915-133">In hello search box, type **Salesforce**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="ea915-135">Nel riquadro dei risultati hello, selezionare **Salesforce**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ea915-135">In hello results panel, select **Salesforce**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ea915-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea915-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ea915-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Salesforce in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ea915-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ea915-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Salesforce è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea915-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce is tooa user in Azure AD.</span></span> <span data-ttu-id="ea915-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Salesforce richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="ea915-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce needs toobe established.</span></span>

<span data-ttu-id="ea915-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ea915-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce.</span></span>

<span data-ttu-id="ea915-142">tooconfigure e test Azure single sign-on AD con Salesforce, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="ea915-142">tooconfigure and test Azure AD single sign-on with Salesforce, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ea915-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ea915-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ea915-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea915-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ea915-145">**[Creazione di un utente test Salesforce](#creating-a-salesforce-test-user)**  -toohave un equivalente di Britta Simon in Salesforce che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ea915-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - toohave a counterpart of Britta Simon in Salesforce that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ea915-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ea915-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ea915-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="ea915-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ea915-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea915-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ea915-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ea915-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="ea915-150">**Azure AD tooconfigure single sign-on con Salesforce, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ea915-150">**tooconfigure Azure AD single sign-on with Salesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea915-151">Nel portale di Azure su hello hello **Salesforce** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ea915-151">In hello Azure portal, on hello **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="ea915-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ea915-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="ea915-155">In hello **URL e il dominio di Salesforce** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ea915-155">On hello **Salesforce Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="ea915-157">In hello **Sign-on URL** casella di testo, valore di tipo hello utilizzando hello modello:</span><span class="sxs-lookup"><span data-stu-id="ea915-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern:</span></span> 
   * <span data-ttu-id="ea915-158">Account aziendale: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="ea915-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="ea915-159">Account sviluppatore: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="ea915-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ea915-160">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="ea915-160">These values are not hello real.</span></span> <span data-ttu-id="ea915-161">Aggiornare questi valori con URL hello effettivo Sign-on.</span><span class="sxs-lookup"><span data-stu-id="ea915-161">Update these values with hello actual Sign-on URL.</span></span> <span data-ttu-id="ea915-162">Contatto [team di supporto Client di Salesforce](https://help.salesforce.com/support) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="ea915-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="ea915-163">In hello **certificato di firma SAML** fare clic su **certificato** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="ea915-163">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="ea915-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ea915-165">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ea915-167">In hello **configurazione Salesforce** fare clic su **configurare Salesforce** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="ea915-167">On hello **Salesforce Configuration** section, click **Configure Salesforce** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ea915-168">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="ea915-168">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    <span data-ttu-id="ea915-169">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="ea915-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="ea915-170">Aprire una nuova scheda nel browser e accedere tooyour account amministratore Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ea915-170">Open a new tab in your browser and log in tooyour Salesforce administrator account.</span></span>

8.  <span data-ttu-id="ea915-171">In hello **amministratore** riquadro di spostamento, fare clic su **controlli di sicurezza** tooexpand hello correlati sezione.</span><span class="sxs-lookup"><span data-stu-id="ea915-171">Under hello **Administrator** navigation pane, click **Security Controls** tooexpand hello related section.</span></span> <span data-ttu-id="ea915-172">Fare quindi clic su **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="ea915-172">Then click **Single Sign-On Settings**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="ea915-174">In hello **Single Sign-On Settings** pagina, fare clic su hello **modifica** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ea915-174">On hello **Single Sign-On Settings** page, click hello **Edit** button.</span></span>
    <span data-ttu-id="ea915-175">![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="ea915-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="ea915-176">Se si è grado tooenable Single Sign-On le impostazioni per l'account di Salesforce, potrebbe essere necessario toocontact [team di supporto Client di Salesforce](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="ea915-176">If you are unable tooenable Single Sign-On settings for your Salesforce account, you may need toocontact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="ea915-177">Selezionare **SAML Enabled**, quindi fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="ea915-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="ea915-179">Fare clic su SAML single sign-on impostazioni, tooconfigure **New**.</span><span class="sxs-lookup"><span data-stu-id="ea915-179">tooconfigure your SAML single sign-on settings, click **New**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="ea915-181">In hello **SAML Single Sign-On Setting Edit** pagina, assicurarsi di hello seguenti configurazioni:</span><span class="sxs-lookup"><span data-stu-id="ea915-181">On hello **SAML Single Sign-On Setting Edit** page, make hello following configurations:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="ea915-183">a.</span><span class="sxs-lookup"><span data-stu-id="ea915-183">a.</span></span> <span data-ttu-id="ea915-184">Per hello **nome** , digitare un nome descrittivo per questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="ea915-184">For hello **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="ea915-185">Fornisce un valore per **nome** popolare automaticamente hello **nome API** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ea915-185">Providing a value for **Name** automatically populate hello **API Name** textbox.</span></span>

    <span data-ttu-id="ea915-186">b.</span><span class="sxs-lookup"><span data-stu-id="ea915-186">b.</span></span> <span data-ttu-id="ea915-187">Incolla **ID entità SMAL** valore in hello **dell'autorità di certificazione** campo Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ea915-187">Paste **SMAL Entity ID** value into hello **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="ea915-188">c.</span><span class="sxs-lookup"><span data-stu-id="ea915-188">c.</span></span> <span data-ttu-id="ea915-189">In hello **Id entità textbox**, digitare il nome di dominio di Salesforce utilizzando hello seguente motivo:</span><span class="sxs-lookup"><span data-stu-id="ea915-189">In hello **Entity Id textbox**, type your Salesforce domain name using hello following pattern:</span></span>
      
      * <span data-ttu-id="ea915-190">Account aziendale: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="ea915-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="ea915-191">Account sviluppatore: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="ea915-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="ea915-192">d.</span><span class="sxs-lookup"><span data-stu-id="ea915-192">d.</span></span> <span data-ttu-id="ea915-193">Fare clic su **Sfoglia** o **Scegli File** tooopen hello **tooUpload Scegli File** finestra di dialogo, selezionare il certificato Salesforce e quindi fare clic su **aprire**certificato hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="ea915-193">Click **Browse** or **Choose File** tooopen hello **Choose File tooUpload** dialog, select your Salesforce certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="ea915-194">e.</span><span class="sxs-lookup"><span data-stu-id="ea915-194">e.</span></span> <span data-ttu-id="ea915-195">In **SAML Identity Type** selezionare **Assertion contains User's salesforce.com username**.</span><span class="sxs-lookup"><span data-stu-id="ea915-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="ea915-196">f.</span><span class="sxs-lookup"><span data-stu-id="ea915-196">f.</span></span> <span data-ttu-id="ea915-197">Per **SAML Identity Location**selezionare **identità si trova nell'elemento NameIdentifier hello di hello istruzione dell'oggetto**</span><span class="sxs-lookup"><span data-stu-id="ea915-197">For **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**</span></span>

    <span data-ttu-id="ea915-198">g.</span><span class="sxs-lookup"><span data-stu-id="ea915-198">g.</span></span> <span data-ttu-id="ea915-199">Incolla **URL servizio Single Sign-On** in hello **Identity Provider Login URL** campo Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ea915-199">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="ea915-200">h.</span><span class="sxs-lookup"><span data-stu-id="ea915-200">h.</span></span> <span data-ttu-id="ea915-201">Per **Service Provider Initiated Request Binding** selezionare **HTTP Redirect**.</span><span class="sxs-lookup"><span data-stu-id="ea915-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="ea915-202">i.</span><span class="sxs-lookup"><span data-stu-id="ea915-202">i.</span></span> <span data-ttu-id="ea915-203">Infine, fare clic su **salvare** tooapply SAML single sign-on impostazioni.</span><span class="sxs-lookup"><span data-stu-id="ea915-203">Finally, click **Save** tooapply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="ea915-204">Nel riquadro di spostamento a sinistra hello in Salesforce, fare clic su **Gestione dominio** tooexpand hello sezione correlata e quindi fare clic su **My Domain**.</span><span class="sxs-lookup"><span data-stu-id="ea915-204">On hello left navigation pane in Salesforce, click **Domain Management** tooexpand hello related section, and then click **My Domain**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="ea915-206">Scorrere verso il basso toohello **configurazione dell'autenticazione** sezione e fare clic su hello **modifica** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ea915-206">Scroll down toohello **Authentication Configuration** section, and click hello **Edit** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="ea915-208">In hello **servizio di autenticazione** sezione, selezionare il nome descrittivo della configurazione SSO SAML hello e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="ea915-208">In hello **Authentication Service** section, select hello friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="ea915-210">Se più di un servizio di autenticazione è selezionato, gli utenti sono richieste tooselect quale servizio di autenticazione che desiderano toosign con durante l'avvio di single sign-on tooyour Salesforce ambiente.</span><span class="sxs-lookup"><span data-stu-id="ea915-210">If more than one authentication service is selected, users are prompted tooselect which authentication service they like toosign in with while initiating single sign-on tooyour Salesforce environment.</span></span> <span data-ttu-id="ea915-211">Se non si desidera che toohappen, quindi è necessario **lasciare deselezionata tutti gli altri servizi di autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="ea915-211">If you don’t want it toohappen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="ea915-212">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="ea915-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ea915-213">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="ea915-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ea915-214">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ea915-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ea915-215">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea915-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="ea915-216">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ea915-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="ea915-218">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ea915-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea915-219">Nel riquadro di spostamento a sinistra di hello hello **portale di Azure**, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ea915-219">On hello left navigation pane in hello **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ea915-221">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ea915-221">toodisplay hello list of users, Go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ea915-223">Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ea915-223">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ea915-225">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ea915-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ea915-227">a.</span><span class="sxs-lookup"><span data-stu-id="ea915-227">a.</span></span> <span data-ttu-id="ea915-228">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ea915-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ea915-229">b.</span><span class="sxs-lookup"><span data-stu-id="ea915-229">b.</span></span> <span data-ttu-id="ea915-230">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ea915-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ea915-231">c.</span><span class="sxs-lookup"><span data-stu-id="ea915-231">c.</span></span> <span data-ttu-id="ea915-232">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="ea915-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ea915-233">d.</span><span class="sxs-lookup"><span data-stu-id="ea915-233">d.</span></span> <span data-ttu-id="ea915-234">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ea915-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="ea915-235">Creazione di un utente test di Salesforce</span><span class="sxs-lookup"><span data-stu-id="ea915-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="ea915-236">In questa sezione si crea un utente di nome Britta Simon in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ea915-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="ea915-237">Salesforce supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="ea915-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="ea915-238">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="ea915-238">There is no action item for you in this section.</span></span> <span data-ttu-id="ea915-239">Se un utente non esiste già in Salesforce, viene creato uno nuovo quando si tenta di tooaccess Salesforce.</span><span class="sxs-lookup"><span data-stu-id="ea915-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt tooaccess Salesforce.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ea915-240">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea915-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ea915-241">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="ea915-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce.</span></span>

![Assegna utente][200] 

<span data-ttu-id="ea915-243">**tooassign Britta Simon tooSalesforce, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ea915-243">**tooassign Britta Simon tooSalesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea915-244">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ea915-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ea915-246">Nell'elenco di applicazioni hello, selezionare **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="ea915-246">In hello applications list, select **Salesforce**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="ea915-248">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ea915-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="ea915-250">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ea915-250">Click **Add** button.</span></span> <span data-ttu-id="ea915-251">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ea915-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="ea915-253">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="ea915-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ea915-254">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ea915-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ea915-255">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ea915-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ea915-256">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ea915-256">Testing single sign-on</span></span>

<span data-ttu-id="ea915-257">tootest le impostazioni single sign-on, aprire il pannello di accesso a hello [https://myapps.microsoft.com](https://myapps.microsoft.com/), quindi accedere all'account di prova hello e fare clic su **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="ea915-257">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into hello test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ea915-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ea915-258">Additional resources</span></span>

* [<span data-ttu-id="ea915-259">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea915-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea915-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea915-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ea915-261">Configura provisioning utenti</span><span class="sxs-lookup"><span data-stu-id="ea915-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

