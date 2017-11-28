---
title: 'Esercitazione: Integrazione di Azure Active Directory con Kantega SSO for Confluence | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Kantega SSO per confluenza.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d0d99c14-a6ca-45f2-bb84-633126095e7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: b35eb8757e41e86228a3a9ee10869086cc801c9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-confluence"></a><span data-ttu-id="2e815-103">Esercitazione: Integrazione di Azure Active Directory con Kantega SSO for Confluence</span><span class="sxs-lookup"><span data-stu-id="2e815-103">Tutorial: Azure Active Directory integration with Kantega SSO for Confluence</span></span>

<span data-ttu-id="2e815-104">In questa esercitazione, è illustrato come toointegrate Kantega SSO per confluenza con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e815-104">In this tutorial, you learn how toointegrate Kantega SSO for Confluence with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e815-105">Kantega SSO per la confluenza di integrazione con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="2e815-105">Integrating Kantega SSO for Confluence with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2e815-106">È possibile controllare in Azure AD che ha accesso tooKantega SSO per confluenza</span><span class="sxs-lookup"><span data-stu-id="2e815-106">You can control in Azure AD who has access tooKantega SSO for Confluence</span></span>
- <span data-ttu-id="2e815-107">È possibile abilitare l'utenti tooautomatically get connesso tooKantega SSO per confluenza (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e815-107">You can enable your users tooautomatically get signed-on tooKantega SSO for Confluence (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2e815-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2e815-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2e815-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e815-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e815-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2e815-110">Prerequisites</span></span>

<span data-ttu-id="2e815-111">integrazione di Azure AD con Kantega SSO per confluenza tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="2e815-111">tooconfigure Azure AD integration with Kantega SSO for Confluence, you need hello following items:</span></span>

- <span data-ttu-id="2e815-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e815-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e815-113">Sottoscrizione di Kantega SSO for Confluence abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2e815-113">A Kantega SSO for Confluence single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e815-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="2e815-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2e815-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="2e815-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e815-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2e815-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2e815-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e815-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e815-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2e815-118">Scenario description</span></span>
<span data-ttu-id="2e815-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2e815-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e815-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="2e815-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e815-121">Aggiunta di Kantega SSO per confluenza dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="2e815-121">Adding Kantega SSO for Confluence from hello gallery</span></span>
2. <span data-ttu-id="2e815-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e815-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-confluence-from-hello-gallery"></a><span data-ttu-id="2e815-123">Aggiunta di Kantega SSO per confluenza dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="2e815-123">Adding Kantega SSO for Confluence from hello gallery</span></span>
<span data-ttu-id="2e815-124">integrazione di hello tooconfigure di Kantega SSO per confluenza in Azure AD, è necessario tooadd Kantega SSO per confluenza dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2e815-124">tooconfigure hello integration of Kantega SSO for Confluence into Azure AD, you need tooadd Kantega SSO for Confluence from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2e815-125">**tooadd Kantega SSO per confluenza dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2e815-125">**tooadd Kantega SSO for Confluence from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e815-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="2e815-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2e815-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="2e815-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2e815-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2e815-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="2e815-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2e815-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="2e815-133">Nella casella di ricerca hello, digitare **Kantega SSO per confluenza**.</span><span class="sxs-lookup"><span data-stu-id="2e815-133">In hello search box, type **Kantega SSO for Confluence**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_search.png)

5. <span data-ttu-id="2e815-135">Nel riquadro dei risultati hello, selezionare **Kantega SSO per confluenza**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2e815-135">In hello results panel, select **Kantega SSO for Confluence**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2e815-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e815-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2e815-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kantega SSO for Confluence mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2e815-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Confluence based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e815-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Kantega SSO per confluenza è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e815-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for Confluence is tooa user in Azure AD.</span></span> <span data-ttu-id="2e815-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Kantega SSO per confluenza deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="2e815-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for Confluence needs toobe established.</span></span>

<span data-ttu-id="2e815-141">In Kantega SSO per confluenza, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="2e815-141">In Kantega SSO for Confluence, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2e815-142">tooconfigure e prova AD Azure single sign-on con Kantega SSO per confluenza, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="2e815-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for Confluence, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2e815-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2e815-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2e815-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e815-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e815-145">**[Creazione di un SSO Kantega per utente test confluenza](#creating-a-kantega-sso-for-confluence-test-user)**  -toohave un equivalente di Britta Simon Kantega SSO per la confluenza di rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2e815-145">**[Creating a Kantega SSO for Confluence test user](#creating-a-kantega-sso-for-confluence-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for Confluence that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2e815-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2e815-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e815-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="2e815-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2e815-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e815-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2e815-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on in SSO il Kantega per applicazione confluenza.</span><span class="sxs-lookup"><span data-stu-id="2e815-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for Confluence application.</span></span>

<span data-ttu-id="2e815-150">**tooconfigure AD Azure single sign-on con Kantega SSO per confluenza, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2e815-150">**tooconfigure Azure AD single sign-on with Kantega SSO for Confluence, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e815-151">Nel portale di Azure su hello hello **Kantega SSO per confluenza** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2e815-151">In hello Azure portal, on hello **Kantega SSO for Confluence** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="2e815-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2e815-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_samlbase.png)

3. <span data-ttu-id="2e815-155">In **IDP** avviato modalità, hello **Kantega SSO per confluenza dominio e gli URL** sezione eseguire hello seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="2e815-155">In **IDP** initiated mode, on hello **Kantega SSO for Confluence Domain and URLs** section perform hello following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url1.png)

    <span data-ttu-id="2e815-157">a.</span><span class="sxs-lookup"><span data-stu-id="2e815-157">a.</span></span> <span data-ttu-id="2e815-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2e815-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="2e815-159">b.</span><span class="sxs-lookup"><span data-stu-id="2e815-159">b.</span></span> <span data-ttu-id="2e815-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2e815-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="2e815-161">In **SP** modalità avviata, controllo **Mostra URL impostazioni avanzate** ed eseguire hello seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="2e815-161">In **SP** initiated mode, check **Show advanced URL settings** and perform hello following step:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url2.png)

    <span data-ttu-id="2e815-163">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2e815-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2e815-164">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="2e815-164">These values are not real.</span></span> <span data-ttu-id="2e815-165">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="2e815-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2e815-166">Questi valori vengono ricevuti durante la configurazione del plug-in confluenza, illustrato più avanti nell'esercitazione di hello hello.</span><span class="sxs-lookup"><span data-stu-id="2e815-166">These values are received during hello configuration of Confluence plugin, which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="2e815-167">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="2e815-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_certificate.png) 

6. <span data-ttu-id="2e815-169">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="2e815-169">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2e815-171">In una finestra del web browser, accedere tooyour **portale di amministrazione confluenza** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="2e815-171">In a different web browser window, log in tooyour **Confluence admin portal** as an administrator.</span></span>

8. <span data-ttu-id="2e815-172">Passare il mouse su ruota dentata e scegliere hello **componenti aggiuntivi**.</span><span class="sxs-lookup"><span data-stu-id="2e815-172">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon1.png)

9. <span data-ttu-id="2e815-174">Nella scheda **ATLASSIAN MARKETPLACE** (MARKETPLACE DI ATLASSIAN) fare clic su **Find new add-ons** (Trova nuovi componenti aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="2e815-174">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon.png)

10. <span data-ttu-id="2e815-176">Ricerca **Kantega SSO per Kerberos SAML confluenza** e fare clic su **installare** tooinstall pulsante hello nuovo plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="2e815-176">Search **Kantega SSO for Confluence SAML Kerberos** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon2.png)

11. <span data-ttu-id="2e815-178">verrà avviata l'installazione di plug-in di Hello.</span><span class="sxs-lookup"><span data-stu-id="2e815-178">hello plugin installation starts.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon3.png)

12. <span data-ttu-id="2e815-180">Al termine dell'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="2e815-180">Once hello installation is complete.</span></span> <span data-ttu-id="2e815-181">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="2e815-181">Click **Close**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon33.png)

13. <span data-ttu-id="2e815-183">Fare clic su **Manage**.</span><span class="sxs-lookup"><span data-stu-id="2e815-183">Click **Manage**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon34.png)
    
14. <span data-ttu-id="2e815-185">Fare clic su **configura** tooconfigure hello nuovo plug-in.</span><span class="sxs-lookup"><span data-stu-id="2e815-185">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon35.png)

15. <span data-ttu-id="2e815-187">Questo nuovo plug-in è disponibile anche nella scheda**USERS & SECURITY** (UTENTI E SICUREZZA).</span><span class="sxs-lookup"><span data-stu-id="2e815-187">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon36.png)
    
16. <span data-ttu-id="2e815-189">In hello **SAML** sezione.</span><span class="sxs-lookup"><span data-stu-id="2e815-189">In hello **SAML** section.</span></span> <span data-ttu-id="2e815-190">Selezionare **Azure Active Directory (Azure AD)** da hello **Aggiungi provider di identità** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="2e815-190">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon4.png)

17. <span data-ttu-id="2e815-192">Selezionare il livello di sottoscrizione **Basic** (Di base).</span><span class="sxs-lookup"><span data-stu-id="2e815-192">Select subscription level as **Basic**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon5.png)       

18. <span data-ttu-id="2e815-194">In hello **proprietà App** sezione, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2e815-194">On hello **App properties** section, perform following steps:</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon6.png)

    <span data-ttu-id="2e815-196">a.</span><span class="sxs-lookup"><span data-stu-id="2e815-196">a.</span></span> <span data-ttu-id="2e815-197">Hello copia **URI ID App** valore e utilizzarlo come **URL Sign-On, l'URL di risposta e identificatore** su hello **Kantega SSO per confluenza dominio e gli URL** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e815-197">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for Confluence Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="2e815-198">b.</span><span class="sxs-lookup"><span data-stu-id="2e815-198">b.</span></span> <span data-ttu-id="2e815-199">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2e815-199">Click **Next**.</span></span>

19. <span data-ttu-id="2e815-200">In hello **importazione dei metadati** sezione, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2e815-200">On hello **Metadata import** section, perform following steps:</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon7.png)

    <span data-ttu-id="2e815-202">a.</span><span class="sxs-lookup"><span data-stu-id="2e815-202">a.</span></span> <span data-ttu-id="2e815-203">Selezionare **Metadata file on my computer** (File metadati in questo computer) e caricare il file di metadati scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e815-203">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="2e815-204">b.</span><span class="sxs-lookup"><span data-stu-id="2e815-204">b.</span></span> <span data-ttu-id="2e815-205">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2e815-205">Click **Next**.</span></span>

20. <span data-ttu-id="2e815-206">In hello **nome e SSO percorso** sezione, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2e815-206">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon8.png)
    
    <span data-ttu-id="2e815-208">a.</span><span class="sxs-lookup"><span data-stu-id="2e815-208">a.</span></span> <span data-ttu-id="2e815-209">Aggiungi nome del Provider di identità hello in **nome provider di identità** casella di testo (ad esempio, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e815-209">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="2e815-210">b.</span><span class="sxs-lookup"><span data-stu-id="2e815-210">b.</span></span> <span data-ttu-id="2e815-211">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2e815-211">Click **Next**.</span></span>

21. <span data-ttu-id="2e815-212">Verificare il certificato di firma hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2e815-212">Verify hello Signing certificate and click **Next**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon9.png)

22. <span data-ttu-id="2e815-214">In hello **gli account utente confluenza** sezione, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2e815-214">On hello **Confluence user accounts** section, perform following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon10.png)

    <span data-ttu-id="2e815-216">a.</span><span class="sxs-lookup"><span data-stu-id="2e815-216">a.</span></span> <span data-ttu-id="2e815-217">Selezionare **creare gli utenti nella Directory interna del confluenza eventualmente** e immettere il nome appropriato del gruppo di hello hello per gli utenti (può essere più no.</span><span class="sxs-lookup"><span data-stu-id="2e815-217">Select **Create users in Confluence's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="2e815-218">gruppi separati da virgola).</span><span class="sxs-lookup"><span data-stu-id="2e815-218">of groups separated by comma).</span></span>

    <span data-ttu-id="2e815-219">b.</span><span class="sxs-lookup"><span data-stu-id="2e815-219">b.</span></span> <span data-ttu-id="2e815-220">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2e815-220">Click **Next**.</span></span>

23. <span data-ttu-id="2e815-221">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="2e815-221">Click **Finish**.</span></span>   

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon11.png)

24. <span data-ttu-id="2e815-223">In hello **noto domini per Azure AD** sezione, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2e815-223">On hello **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon12.png)

    <span data-ttu-id="2e815-225">a.</span><span class="sxs-lookup"><span data-stu-id="2e815-225">a.</span></span> <span data-ttu-id="2e815-226">Selezionare **noto domini** dal riquadro sinistro di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="2e815-226">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="2e815-227">b.</span><span class="sxs-lookup"><span data-stu-id="2e815-227">b.</span></span> <span data-ttu-id="2e815-228">Immettere un nome di dominio in hello **noto domini** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="2e815-228">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="2e815-229">c.</span><span class="sxs-lookup"><span data-stu-id="2e815-229">c.</span></span> <span data-ttu-id="2e815-230">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="2e815-230">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="2e815-231">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="2e815-231">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2e815-232">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="2e815-232">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2e815-233">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2e815-233">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2e815-234">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e815-234">Creating an Azure AD test user</span></span>
<span data-ttu-id="2e815-235">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2e815-235">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="2e815-237">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2e815-237">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e815-238">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="2e815-238">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2e815-240">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="2e815-240">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2e815-242">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="2e815-242">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2e815-244">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2e815-244">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2e815-246">a.</span><span class="sxs-lookup"><span data-stu-id="2e815-246">a.</span></span> <span data-ttu-id="2e815-247">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e815-247">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e815-248">b.</span><span class="sxs-lookup"><span data-stu-id="2e815-248">b.</span></span> <span data-ttu-id="2e815-249">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2e815-249">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2e815-250">c.</span><span class="sxs-lookup"><span data-stu-id="2e815-250">c.</span></span> <span data-ttu-id="2e815-251">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="2e815-251">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2e815-252">d.</span><span class="sxs-lookup"><span data-stu-id="2e815-252">d.</span></span> <span data-ttu-id="2e815-253">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2e815-253">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-confluence-test-user"></a><span data-ttu-id="2e815-254">Creazione di un utente test di Kantega SSO for Confluence</span><span class="sxs-lookup"><span data-stu-id="2e815-254">Creating a Kantega SSO for Confluence test user</span></span>

<span data-ttu-id="2e815-255">toolog agli utenti di Azure AD tooenable in tooConfluence, è necessario eseguirne il provisioning in confluenza.</span><span class="sxs-lookup"><span data-stu-id="2e815-255">tooenable Azure AD users toolog in tooConfluence, they must be provisioned into Confluence.</span></span> <span data-ttu-id="2e815-256">In caso di hello Kantega SSO per confluenza, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="2e815-256">In hello case of Kantega SSO for Confluence, provisioning is a manual task.</span></span>

<span data-ttu-id="2e815-257">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2e815-257">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e815-258">Accedere come amministratore tooyour Kantega SSO per il sito della società confluenza.</span><span class="sxs-lookup"><span data-stu-id="2e815-258">Log in tooyour Kantega SSO for Confluence company site as an administrator.</span></span>

2. <span data-ttu-id="2e815-259">Passare il mouse su ruota dentata e scegliere hello **Gestione utenti**.</span><span class="sxs-lookup"><span data-stu-id="2e815-259">Hover on cog and click hello **User management**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-kantegassoforconfluence-tutorial/user1.png) 

3. <span data-ttu-id="2e815-261">Nella sezione Users (Utenti) fare clic sula scheda **Add users** (Aggiungi utenti). In hello **"Aggiungi utente"** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2e815-261">Under Users section, click **Add Users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-kantegassoforconfluence-tutorial/user2.png) 

    <span data-ttu-id="2e815-263">a.</span><span class="sxs-lookup"><span data-stu-id="2e815-263">a.</span></span> <span data-ttu-id="2e815-264">In hello **Username** casella Tipo hello email dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2e815-264">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="2e815-265">b.</span><span class="sxs-lookup"><span data-stu-id="2e815-265">b.</span></span> <span data-ttu-id="2e815-266">In hello **nome completo** casella di testo, nome completo del tipo hello dell'utente come Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e815-266">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="2e815-267">c.</span><span class="sxs-lookup"><span data-stu-id="2e815-267">c.</span></span> <span data-ttu-id="2e815-268">In hello **posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2e815-268">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="2e815-269">d.</span><span class="sxs-lookup"><span data-stu-id="2e815-269">d.</span></span> <span data-ttu-id="2e815-270">In hello **Password** casella di testo, digitare la password per l'utente hello.</span><span class="sxs-lookup"><span data-stu-id="2e815-270">In hello **Password** textbox, type hello password for user.</span></span>

    <span data-ttu-id="2e815-271">e.</span><span class="sxs-lookup"><span data-stu-id="2e815-271">e.</span></span> <span data-ttu-id="2e815-272">Fare clic su **Conferma Password** digitare nuovamente la password di hello.</span><span class="sxs-lookup"><span data-stu-id="2e815-272">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="2e815-273">f.</span><span class="sxs-lookup"><span data-stu-id="2e815-273">f.</span></span> <span data-ttu-id="2e815-274">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2e815-274">Click **Add** button.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2e815-275">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e815-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2e815-276">In questa sezione per abilitare Britta Simon toouse single sign-on Azure tooKantega accesso SSO per la confluenza di concessione.</span><span class="sxs-lookup"><span data-stu-id="2e815-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for Confluence.</span></span>

![Assegna utente][200] 

<span data-ttu-id="2e815-278">**tooassign Britta Simon tooKantega SSO per confluenza, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2e815-278">**tooassign Britta Simon tooKantega SSO for Confluence, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e815-279">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2e815-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2e815-281">Nell'elenco di applicazioni hello, selezionare **Kantega SSO per confluenza**.</span><span class="sxs-lookup"><span data-stu-id="2e815-281">In hello applications list, select **Kantega SSO for Confluence**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_app.png) 

3. <span data-ttu-id="2e815-283">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2e815-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="2e815-285">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2e815-285">Click **Add** button.</span></span> <span data-ttu-id="2e815-286">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2e815-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="2e815-288">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="2e815-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2e815-289">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2e815-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2e815-290">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2e815-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2e815-291">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2e815-291">Testing single sign-on</span></span>

<span data-ttu-id="2e815-292">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2e815-292">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2e815-293">Quando si fa clic hello Kantega SSO riquadro confluenza in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Kantega SSO per applicazione confluenza.</span><span class="sxs-lookup"><span data-stu-id="2e815-293">When you click hello Kantega SSO for Confluence tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for Confluence application.</span></span>
<span data-ttu-id="2e815-294">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2e815-294">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2e815-295">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2e815-295">Additional resources</span></span>

* [<span data-ttu-id="2e815-296">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e815-296">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e815-297">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e815-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_203.png

