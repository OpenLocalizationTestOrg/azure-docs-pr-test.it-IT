---
title: 'Esercitazione: Integrazione di Azure Active Directory con Kantega SSO for JIRA | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Kantega SSO per JIRA.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2af4891-e3c8-43b3-bdcb-0500c493e9b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 67894cc55ef91d0991c62e0e4f1be712723cb474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-jira"></a><span data-ttu-id="2ec47-103">Esercitazione: Integrazione di Azure Active Directory con Kantega SSO for JIRA</span><span class="sxs-lookup"><span data-stu-id="2ec47-103">Tutorial: Azure Active Directory integration with Kantega SSO for JIRA</span></span>

<span data-ttu-id="2ec47-104">In questa esercitazione, è illustrato come toointegrate Kantega SSO per JIRA con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2ec47-104">In this tutorial, you learn how toointegrate Kantega SSO for JIRA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2ec47-105">Integrazione Kantega SSO per JIRA con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="2ec47-105">Integrating Kantega SSO for JIRA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2ec47-106">È possibile controllare in Azure AD che ha accesso tooKantega SSO per JIRA</span><span class="sxs-lookup"><span data-stu-id="2ec47-106">You can control in Azure AD who has access tooKantega SSO for JIRA</span></span>
- <span data-ttu-id="2ec47-107">È possibile abilitare l'utenti tooautomatically get connesso tooKantega SSO per JIRA (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ec47-107">You can enable your users tooautomatically get signed-on tooKantega SSO for JIRA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2ec47-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2ec47-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2ec47-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2ec47-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ec47-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2ec47-110">Prerequisites</span></span>

<span data-ttu-id="2ec47-111">integrazione di Azure AD con SSO Kantega per JIRA tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="2ec47-111">tooconfigure Azure AD integration with Kantega SSO for JIRA, you need hello following items:</span></span>

- <span data-ttu-id="2ec47-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ec47-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2ec47-113">Sottoscrizione di Kantega SSO for JIRA abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2ec47-113">A Kantega SSO for JIRA single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2ec47-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="2ec47-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2ec47-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="2ec47-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2ec47-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2ec47-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2ec47-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ec47-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2ec47-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2ec47-118">Scenario description</span></span>
<span data-ttu-id="2ec47-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2ec47-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2ec47-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="2ec47-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2ec47-121">Aggiunta di SSO Kantega per JIRA dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="2ec47-121">Adding Kantega SSO for JIRA from hello gallery</span></span>
2. <span data-ttu-id="2ec47-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ec47-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-jira-from-hello-gallery"></a><span data-ttu-id="2ec47-123">Aggiunta di SSO Kantega per JIRA dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="2ec47-123">Adding Kantega SSO for JIRA from hello gallery</span></span>
<span data-ttu-id="2ec47-124">integrazione hello tooconfigure di Kantega SSO per JIRA in Azure AD, è necessario tooadd Kantega SSO per JIRA dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2ec47-124">tooconfigure hello integration of Kantega SSO for JIRA into Azure AD, you need tooadd Kantega SSO for JIRA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2ec47-125">**tooadd Kantega SSO per JIRA dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2ec47-125">**tooadd Kantega SSO for JIRA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ec47-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="2ec47-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2ec47-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2ec47-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="2ec47-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2ec47-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="2ec47-133">Nella casella di ricerca hello, digitare **Kantega SSO per JIRA**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-133">In hello search box, type **Kantega SSO for JIRA**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_search.png)

5. <span data-ttu-id="2ec47-135">Nel riquadro dei risultati hello, selezionare **Kantega SSO per JIRA**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2ec47-135">In hello results panel, select **Kantega SSO for JIRA**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2ec47-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ec47-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2ec47-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kantega SSO for JIRA mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2ec47-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for JIRA based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2ec47-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in SSO Kantega per JIRA è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2ec47-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for JIRA is tooa user in Azure AD.</span></span> <span data-ttu-id="2ec47-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in SSO Kantega per JIRA deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="2ec47-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for JIRA needs toobe established.</span></span>

<span data-ttu-id="2ec47-141">In Kantega SSO per JIRA, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="2ec47-141">In Kantega SSO for JIRA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2ec47-142">tooconfigure e prova AD Azure single sign-on con Kantega SSO per JIRA, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="2ec47-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for JIRA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2ec47-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2ec47-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2ec47-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ec47-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2ec47-145">**[Creazione di un SSO Kantega per utente test JIRA](#creating-a-kantega-sso-for-jira-test-user)**  -toohave un equivalente di Britta Simon Kantega SSO per JIRA che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2ec47-145">**[Creating a Kantega SSO for JIRA test user](#creating-a-kantega-sso-for-jira-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for JIRA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2ec47-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2ec47-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2ec47-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="2ec47-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2ec47-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ec47-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2ec47-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on in SSO il Kantega per applicazione JIRA.</span><span class="sxs-lookup"><span data-stu-id="2ec47-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for JIRA application.</span></span>

<span data-ttu-id="2ec47-150">**tooconfigure AD Azure single sign-on con SSO Kantega per JIRA, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2ec47-150">**tooconfigure Azure AD single sign-on with Kantega SSO for JIRA, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ec47-151">Nel portale di Azure su hello hello **Kantega SSO per JIRA** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-151">In hello Azure portal, on hello **Kantega SSO for JIRA** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="2ec47-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2ec47-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_samlbase.png)

3. <span data-ttu-id="2ec47-155">In **IDP** avviato modalità, hello **Kantega SSO per dominio JIRA e gli URL** sezione eseguire hello seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="2ec47-155">In **IDP** initiated mode, on hello **Kantega SSO for JIRA Domain and URLs** section perform hello following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url1.png)

    <span data-ttu-id="2ec47-157">a.</span><span class="sxs-lookup"><span data-stu-id="2ec47-157">a.</span></span> <span data-ttu-id="2ec47-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2ec47-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="2ec47-159">b.</span><span class="sxs-lookup"><span data-stu-id="2ec47-159">b.</span></span> <span data-ttu-id="2ec47-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2ec47-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="2ec47-161">In **SP** modalità avviata, controllo **Mostra URL impostazioni avanzate** ed eseguire hello seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="2ec47-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform hello following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url2.png)

    <span data-ttu-id="2ec47-163">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2ec47-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2ec47-164">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="2ec47-164">These values are not real.</span></span> <span data-ttu-id="2ec47-165">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="2ec47-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2ec47-166">Questi valori vengono ricevuti durante la configurazione del plug-in Jira, illustrato più avanti nell'esercitazione di hello hello.</span><span class="sxs-lookup"><span data-stu-id="2ec47-166">These values are received during hello configuration of Jira plugin, which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="2ec47-167">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="2ec47-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_certificate.png) 

6. <span data-ttu-id="2ec47-169">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="2ec47-169">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2ec47-171">In una finestra del web browser, accedere come amministratore in tooyour JIRA nel server locale.</span><span class="sxs-lookup"><span data-stu-id="2ec47-171">In a different web browser window, log in tooyour JIRA on premise server as an administrator.</span></span>

8. <span data-ttu-id="2ec47-172">Passare il mouse su ruota dentata e scegliere hello **componenti aggiuntivi**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon1.png)

9. <span data-ttu-id="2ec47-174">Nella sezione della scheda Add-ons (Componenti aggiuntivi) fare clic su **Find new add-ons** (Trova nuovi componenti aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="2ec47-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="2ec47-175">Ricerca **Kantega SSO per JIRA (SAML & Kerberos)** e fare clic su **installare** tooinstall pulsante hello nuovo plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="2ec47-175">Search **Kantega SSO for JIRA (SAML & Kerberos)** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon2.png)

10. <span data-ttu-id="2ec47-177">verrà avviata l'installazione di plug-in di Hello.</span><span class="sxs-lookup"><span data-stu-id="2ec47-177">hello plugin installation starts.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon3.png)

11. <span data-ttu-id="2ec47-179">Al termine dell'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="2ec47-179">Once hello installation is complete.</span></span> <span data-ttu-id="2ec47-180">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-180">Click **Close**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon33.png)

12. <span data-ttu-id="2ec47-182">Fare clic su **Manage**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-182">Click **Manage**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon34.png)
    
13. <span data-ttu-id="2ec47-184">Il nuovo plug-in è visualizzato in **INTEGRATIONS** (INTEGRAZIONI).</span><span class="sxs-lookup"><span data-stu-id="2ec47-184">New plugin is listed under **INTEGRATIONS**.</span></span> <span data-ttu-id="2ec47-185">Fare clic su **configura** tooconfigure hello nuovo plug-in.</span><span class="sxs-lookup"><span data-stu-id="2ec47-185">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon35.png)

14. <span data-ttu-id="2ec47-187">In hello **SAML** sezione.</span><span class="sxs-lookup"><span data-stu-id="2ec47-187">In hello **SAML** section.</span></span> <span data-ttu-id="2ec47-188">Selezionare **Azure Active Directory (Azure AD)** da hello **Aggiungi provider di identità** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="2ec47-188">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon4.png)

15. <span data-ttu-id="2ec47-190">Selezionare il livello di sottoscrizione **Basic** (Di base).</span><span class="sxs-lookup"><span data-stu-id="2ec47-190">Select subscription level as **Basic**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon5.png)     

16. <span data-ttu-id="2ec47-192">In hello **proprietà App** sezione, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2ec47-192">On hello **App properties** section, perform following steps:</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon6.png)

    <span data-ttu-id="2ec47-194">a.</span><span class="sxs-lookup"><span data-stu-id="2ec47-194">a.</span></span> <span data-ttu-id="2ec47-195">Hello copia **URI ID App** valore e utilizzarlo come **URL Sign-On, l'URL di risposta e identificatore** su hello **Kantega SSO per dominio JIRA e gli URL** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec47-195">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for JIRA Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="2ec47-196">b.</span><span class="sxs-lookup"><span data-stu-id="2ec47-196">b.</span></span> <span data-ttu-id="2ec47-197">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-197">Click **Next**.</span></span>

17. <span data-ttu-id="2ec47-198">In hello **importazione dei metadati** sezione, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2ec47-198">On hello **Metadata import** section, perform following steps:</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon7.png)

    <span data-ttu-id="2ec47-200">a.</span><span class="sxs-lookup"><span data-stu-id="2ec47-200">a.</span></span> <span data-ttu-id="2ec47-201">Selezionare **Metadata file on my computer** (File metadati in questo computer) e caricare il file di metadati scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec47-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="2ec47-202">b.</span><span class="sxs-lookup"><span data-stu-id="2ec47-202">b.</span></span> <span data-ttu-id="2ec47-203">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-203">Click **Next**.</span></span>

18. <span data-ttu-id="2ec47-204">In hello **nome e SSO percorso** sezione, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2ec47-204">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon8.png)
    
    <span data-ttu-id="2ec47-206">a.</span><span class="sxs-lookup"><span data-stu-id="2ec47-206">a.</span></span> <span data-ttu-id="2ec47-207">Aggiungi nome del Provider di identità hello in **nome provider di identità** casella di testo (ad esempio, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2ec47-207">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="2ec47-208">b.</span><span class="sxs-lookup"><span data-stu-id="2ec47-208">b.</span></span> <span data-ttu-id="2ec47-209">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-209">Click **Next**.</span></span>

19. <span data-ttu-id="2ec47-210">Verificare il certificato di firma hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-210">Verify hello Signing certificate and click **Next**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon9.png)

20. <span data-ttu-id="2ec47-212">In hello **gli account utente JIRA** sezione, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2ec47-212">On hello **JIRA user accounts** section, perform following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon10.png)

    <span data-ttu-id="2ec47-214">a.</span><span class="sxs-lookup"><span data-stu-id="2ec47-214">a.</span></span> <span data-ttu-id="2ec47-215">Selezionare **creare gli utenti nella Directory interna del JIRA eventualmente** e immettere il nome appropriato del gruppo di hello hello per gli utenti (può essere più no.</span><span class="sxs-lookup"><span data-stu-id="2ec47-215">Select **Create users in JIRA's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="2ec47-216">gruppi separati da virgola).</span><span class="sxs-lookup"><span data-stu-id="2ec47-216">of groups separated by comma).</span></span>

    <span data-ttu-id="2ec47-217">b.</span><span class="sxs-lookup"><span data-stu-id="2ec47-217">b.</span></span> <span data-ttu-id="2ec47-218">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-218">Click **Next**.</span></span>

21. <span data-ttu-id="2ec47-219">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-219">Click **Finish**.</span></span>   

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon11.png)

22. <span data-ttu-id="2ec47-221">In hello **noto domini per Azure AD** sezione, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2ec47-221">On hello **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/addon12.png)

    <span data-ttu-id="2ec47-223">a.</span><span class="sxs-lookup"><span data-stu-id="2ec47-223">a.</span></span> <span data-ttu-id="2ec47-224">Selezionare **noto domini** dal riquadro sinistro di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="2ec47-224">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="2ec47-225">b.</span><span class="sxs-lookup"><span data-stu-id="2ec47-225">b.</span></span> <span data-ttu-id="2ec47-226">Immettere un nome di dominio in hello **noto domini** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="2ec47-226">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="2ec47-227">c.</span><span class="sxs-lookup"><span data-stu-id="2ec47-227">c.</span></span> <span data-ttu-id="2ec47-228">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-228">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="2ec47-229">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="2ec47-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2ec47-230">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="2ec47-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2ec47-231">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2ec47-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2ec47-232">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ec47-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="2ec47-233">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2ec47-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="2ec47-235">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2ec47-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ec47-236">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="2ec47-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2ec47-238">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2ec47-240">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="2ec47-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2ec47-242">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2ec47-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2ec47-244">a.</span><span class="sxs-lookup"><span data-stu-id="2ec47-244">a.</span></span> <span data-ttu-id="2ec47-245">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2ec47-246">b.</span><span class="sxs-lookup"><span data-stu-id="2ec47-246">b.</span></span> <span data-ttu-id="2ec47-247">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2ec47-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2ec47-248">c.</span><span class="sxs-lookup"><span data-stu-id="2ec47-248">c.</span></span> <span data-ttu-id="2ec47-249">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2ec47-250">d.</span><span class="sxs-lookup"><span data-stu-id="2ec47-250">d.</span></span> <span data-ttu-id="2ec47-251">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-jira-test-user"></a><span data-ttu-id="2ec47-252">Creazione di un utente test di Kantega SSO for JIRA</span><span class="sxs-lookup"><span data-stu-id="2ec47-252">Creating a Kantega SSO for JIRA test user</span></span>

<span data-ttu-id="2ec47-253">toolog agli utenti di Azure AD tooenable in tooJIRA, è necessario eseguirne il provisioning in JIRA.</span><span class="sxs-lookup"><span data-stu-id="2ec47-253">tooenable Azure AD users toolog in tooJIRA, they must be provisioned into JIRA.</span></span> <span data-ttu-id="2ec47-254">In Kantega SSO for JIRA il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="2ec47-254">In Kantega SSO for JIRA, provisioning is a manual task.</span></span>

<span data-ttu-id="2ec47-255">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2ec47-255">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ec47-256">Accedere come amministratore tooyour JIRA nel server locale.</span><span class="sxs-lookup"><span data-stu-id="2ec47-256">Log in tooyour JIRA on premise server as an administrator.</span></span>

2. <span data-ttu-id="2ec47-257">Passare il mouse su ruota dentata e scegliere hello **Gestione utenti**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-257">Hover on cog and click hello **User management**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-kantegassoforjira-tutorial/user1.png) 

3. <span data-ttu-id="2ec47-259">Nella sezione della scheda **User management** (Gestione utenti) fare clic su **Create user** (Crea utente).</span><span class="sxs-lookup"><span data-stu-id="2ec47-259">Under **User management** tab section, click **Create user**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-kantegassoforjira-tutorial/user2.png) 

4. <span data-ttu-id="2ec47-261">In hello **"Create new user"** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2ec47-261">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-kantegassoforjira-tutorial/user3.png) 

    <span data-ttu-id="2ec47-263">a.</span><span class="sxs-lookup"><span data-stu-id="2ec47-263">a.</span></span> <span data-ttu-id="2ec47-264">In hello **indirizzo di posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2ec47-264">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="2ec47-265">b.</span><span class="sxs-lookup"><span data-stu-id="2ec47-265">b.</span></span> <span data-ttu-id="2ec47-266">In hello **nome completo** casella di testo, nome completo del tipo di utente hello come Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2ec47-266">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="2ec47-267">c.</span><span class="sxs-lookup"><span data-stu-id="2ec47-267">c.</span></span> <span data-ttu-id="2ec47-268">In hello **Username** casella Tipo hello email dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2ec47-268">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="2ec47-269">d.</span><span class="sxs-lookup"><span data-stu-id="2ec47-269">d.</span></span> <span data-ttu-id="2ec47-270">In hello **Password** casella di testo, digitare la password dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="2ec47-270">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="2ec47-271">e.</span><span class="sxs-lookup"><span data-stu-id="2ec47-271">e.</span></span> <span data-ttu-id="2ec47-272">Fare clic su **Create User** (Crea utente).</span><span class="sxs-lookup"><span data-stu-id="2ec47-272">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2ec47-273">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2ec47-273">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2ec47-274">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooKantega SSO per JIRA.</span><span class="sxs-lookup"><span data-stu-id="2ec47-274">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for JIRA.</span></span>

![Assegna utente][200] 

<span data-ttu-id="2ec47-276">**tooassign Britta Simon tooKantega SSO per JIRA, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2ec47-276">**tooassign Britta Simon tooKantega SSO for JIRA, perform hello following steps:**</span></span>

1. <span data-ttu-id="2ec47-277">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-277">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2ec47-279">Nell'elenco di applicazioni hello, selezionare **Kantega SSO per JIRA**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-279">In hello applications list, select **Kantega SSO for JIRA**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_app.png) 

3. <span data-ttu-id="2ec47-281">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-281">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="2ec47-283">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-283">Click **Add** button.</span></span> <span data-ttu-id="2ec47-284">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="2ec47-286">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="2ec47-286">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2ec47-287">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2ec47-288">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2ec47-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2ec47-289">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2ec47-289">Testing single sign-on</span></span>

<span data-ttu-id="2ec47-290">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2ec47-290">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2ec47-291">Quando si fa clic hello SSO Kantega riquadro JIRA in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Kantega SSO per l'applicazione JIRA.</span><span class="sxs-lookup"><span data-stu-id="2ec47-291">When you click hello Kantega SSO for JIRA tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for JIRA application.</span></span>
<span data-ttu-id="2ec47-292">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2ec47-292">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2ec47-293">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2ec47-293">Additional resources</span></span>

* [<span data-ttu-id="2ec47-294">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ec47-294">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2ec47-295">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2ec47-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_203.png

