---
title: 'Esercitazione: integrazione di Azure Active Directory con SAML SSO for Jira di resolution GmbH | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SAML SSO per Jira dalla risoluzione GmbH.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="4b26a-103">Esercitazione: integrazione di Azure Active Directory con SAML SSO for Jira di resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="4b26a-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="4b26a-104">In questa esercitazione, è illustrato come toointegrate SAML SSO per Jira dalla risoluzione GmbH con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b26a-104">In this tutorial, you learn how toointegrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b26a-105">L'integrazione di SAML SSO per Jira dalla risoluzione GmbH con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4b26a-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4b26a-106">È possibile controllare in Azure AD che ha accesso tooSAML SSO per Jira dalla risoluzione GmbH</span><span class="sxs-lookup"><span data-stu-id="4b26a-106">You can control in Azure AD who has access tooSAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="4b26a-107">È possibile abilitare l'utenti tooautomatically get connesso tooSAML SSO per Jira dalla risoluzione GmbH (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b26a-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b26a-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4b26a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4b26a-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b26a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b26a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4b26a-110">Prerequisites</span></span>

<span data-ttu-id="4b26a-111">integrazione di Azure AD con SAML SSO per Jira dalla risoluzione GmbH tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4b26a-111">tooconfigure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="4b26a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b26a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b26a-113">Una sottoscrizione attiva del Single Sign-On di SAML SSO for Jira di resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="4b26a-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b26a-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4b26a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b26a-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4b26a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b26a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4b26a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b26a-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b26a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b26a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4b26a-118">Scenario description</span></span>
<span data-ttu-id="4b26a-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4b26a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b26a-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4b26a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b26a-121">Aggiunta di SAML SSO per Jira dalla risoluzione GmbH dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4b26a-121">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="4b26a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b26a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="4b26a-123">Aggiunta di SAML SSO per Jira dalla risoluzione GmbH dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4b26a-123">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
<span data-ttu-id="4b26a-124">tooconfigure hello integrazione di SAML SSO per Jira dalla risoluzione GmbH in Azure AD, è necessario tooadd SAML SSO per Jira dalla risoluzione GmbH dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4b26a-124">tooconfigure hello integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need tooadd SAML SSO for Jira by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4b26a-125">**tooadd SAML SSO per Jira dalla risoluzione GmbH dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4b26a-125">**tooadd SAML SSO for Jira by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b26a-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4b26a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4b26a-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4b26a-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4b26a-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4b26a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4b26a-133">Nella casella di ricerca hello, digitare **SAML SSO per Jira dalla risoluzione GmbH**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-133">In hello search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="4b26a-135">Nel riquadro dei risultati hello, selezionare **SAML SSO per Jira dalla risoluzione GmbH**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4b26a-135">In hello results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b26a-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b26a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b26a-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAML SSO for Jira di resolution GmbH con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4b26a-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4b26a-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in SAML SSO per Jira dalla risoluzione GmbH è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b26a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Jira by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="4b26a-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato hello in SAML SSO per Jira dalla risoluzione GmbH deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="4b26a-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Jira by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="4b26a-141">SAML SSO per Jira dalla risoluzione GmbH, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="4b26a-141">In SAML SSO for Jira by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4b26a-142">tooconfigure ed eseguire test AD Azure single sign-on con SAML SSO per Jira dalla risoluzione GmbH, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4b26a-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4b26a-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4b26a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4b26a-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b26a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b26a-145">**[Creazione di un SAML SSO per Jira dall'utente di prova di risoluzione GmbH](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave un equivalente di Britta Simon SAML SSO per Jira dalla risoluzione GmbH che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4b26a-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b26a-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4b26a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b26a-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b26a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b26a-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b26a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b26a-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nel SAML SSO per Jira dalla risoluzione GmbH applicazione.</span><span class="sxs-lookup"><span data-stu-id="4b26a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="4b26a-150">**tooconfigure AD Azure single sign-on con SAML SSO per Jira dalla risoluzione GmbH, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4b26a-150">**tooconfigure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b26a-151">Nel portale di Azure su hello hello **SAML SSO per Jira dalla risoluzione GmbH** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-151">In hello Azure portal, on hello **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4b26a-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4b26a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="4b26a-155">In hello **SAML SSO per Jira dalla risoluzione GmbH dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="4b26a-155">On hello **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="4b26a-157">a.</span><span class="sxs-lookup"><span data-stu-id="4b26a-157">a.</span></span> <span data-ttu-id="4b26a-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="4b26a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="4b26a-159">b.</span><span class="sxs-lookup"><span data-stu-id="4b26a-159">b.</span></span> <span data-ttu-id="4b26a-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="4b26a-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="4b26a-161">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="4b26a-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="4b26a-162">Se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="4b26a-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="4b26a-164">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="4b26a-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="4b26a-165">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="4b26a-165">These values are not real.</span></span> <span data-ttu-id="4b26a-166">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="4b26a-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="4b26a-167">Contatto [team di supporto SAML SSO per Jira dalla risoluzione GmbH Client](https://www.resolution.de/go/support) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="4b26a-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="4b26a-168">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4b26a-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="4b26a-170">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4b26a-170">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="4b26a-172">In una finestra del web browser, accedere tooyour **SAML SSO per Jira dal portale di amministrazione di risoluzione GmbH** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4b26a-172">In a different web browser window, log in tooyour **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="4b26a-173">Passare il mouse su ruota dentata e scegliere hello **componenti aggiuntivi**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="4b26a-175">Si è reindirizzato tooAdministrator pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="4b26a-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="4b26a-176">Immettere hello **Password** e fare clic su **conferma** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4b26a-176">Enter hello **Password** and click **Confirm** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="4b26a-178">Nella sezione della scheda Add-ons (Componenti aggiuntivi) fare clic su **Find new add-ons** (Trova nuovi componenti aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="4b26a-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="4b26a-179">Ricerca **SAML Single Sign On (SSO) per JIRA** e fare clic su **installare** tooinstall pulsante hello nuovo plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="4b26a-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="4b26a-181">verrà avviata l'installazione di plug-in di Hello.</span><span class="sxs-lookup"><span data-stu-id="4b26a-181">hello plugin installation will start.</span></span> <span data-ttu-id="4b26a-182">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-182">Click **Close**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="4b26a-185">Fare clic su **Manage**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-185">Click **Manage**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="4b26a-187">Fare clic su **configura** tooconfigure hello nuovo plug-in.</span><span class="sxs-lookup"><span data-stu-id="4b26a-187">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="4b26a-189">In **SAML SingleSignOn plug-in configurazione** pagina, fare clic su **aggiungere Provider di identità aggiuntive** pulsante Impostazioni hello tooconfigure di Provider di identità.</span><span class="sxs-lookup"><span data-stu-id="4b26a-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="4b26a-191">In questa pagina eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4b26a-191">Perform following steps on this page:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="4b26a-193">a.</span><span class="sxs-lookup"><span data-stu-id="4b26a-193">a.</span></span> <span data-ttu-id="4b26a-194">Aggiungere **nome** di hello Provider di identità (ad esempio, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b26a-194">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="4b26a-195">b.</span><span class="sxs-lookup"><span data-stu-id="4b26a-195">b.</span></span> <span data-ttu-id="4b26a-196">Aggiungere **descrizione** di hello Provider di identità (ad esempio, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b26a-196">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="4b26a-197">c.</span><span class="sxs-lookup"><span data-stu-id="4b26a-197">c.</span></span> <span data-ttu-id="4b26a-198">Fare clic su **XML** e seleziona hello **metadati** file, che è stato scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b26a-198">Click **XML** and select hello **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="4b26a-199">d.</span><span class="sxs-lookup"><span data-stu-id="4b26a-199">d.</span></span> <span data-ttu-id="4b26a-200">Fare clic sul pulsante **Load** (Carica).</span><span class="sxs-lookup"><span data-stu-id="4b26a-200">Click **Load** button.</span></span>

    <span data-ttu-id="4b26a-201">e.</span><span class="sxs-lookup"><span data-stu-id="4b26a-201">e.</span></span> <span data-ttu-id="4b26a-202">Legge i metadati IdP hello e popola i campi di hello come evidenziato nella schermata di hello.</span><span class="sxs-lookup"><span data-stu-id="4b26a-202">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   

16. <span data-ttu-id="4b26a-203">Fare clic su **salvare impostazioni** pulsante Impostazioni hello toosave.</span><span class="sxs-lookup"><span data-stu-id="4b26a-203">Click **Save settings** button toosave hello settings.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="4b26a-205">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="4b26a-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4b26a-206">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="4b26a-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4b26a-207">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b26a-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b26a-208">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b26a-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b26a-209">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4b26a-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4b26a-211">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4b26a-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b26a-212">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4b26a-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b26a-214">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b26a-216">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="4b26a-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b26a-218">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4b26a-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b26a-220">a.</span><span class="sxs-lookup"><span data-stu-id="4b26a-220">a.</span></span> <span data-ttu-id="4b26a-221">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b26a-222">b.</span><span class="sxs-lookup"><span data-stu-id="4b26a-222">b.</span></span> <span data-ttu-id="4b26a-223">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4b26a-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b26a-224">c.</span><span class="sxs-lookup"><span data-stu-id="4b26a-224">c.</span></span> <span data-ttu-id="4b26a-225">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4b26a-226">d.</span><span class="sxs-lookup"><span data-stu-id="4b26a-226">d.</span></span> <span data-ttu-id="4b26a-227">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="4b26a-228">Creazione di un utente di test di SAML SSO for Jira di resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="4b26a-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="4b26a-229">toolog agli utenti di Azure AD tooenable in tooSAML SSO per Jira dalla risoluzione GmbH, è necessario eseguirne il provisioning in SAML SSO per Jira dalla risoluzione GmbH.</span><span class="sxs-lookup"><span data-stu-id="4b26a-229">tooenable Azure AD users toolog in tooSAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="4b26a-230">In SAML SSO for Jira di resolution GmbH il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="4b26a-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="4b26a-231">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4b26a-231">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b26a-232">Accedi tooyour SAML SSO per Jira dal sito di risoluzione GmbH aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4b26a-232">Log in tooyour SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="4b26a-233">Passare il mouse su ruota dentata e scegliere hello **Gestione utenti**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-233">Hover on cog and click hello **User management**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="4b26a-235">Si è reindirizzato tooAdministrator accesso pagina tooenter **Password** e fare clic su **conferma** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4b26a-235">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="4b26a-237">Nella sezione della scheda **User management** (Gestione utenti) fare clic su **Create user** (Crea utente).</span><span class="sxs-lookup"><span data-stu-id="4b26a-237">Under **User management** tab section, click **create user**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="4b26a-239">In hello **"Create new user"** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4b26a-239">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="4b26a-241">a.</span><span class="sxs-lookup"><span data-stu-id="4b26a-241">a.</span></span> <span data-ttu-id="4b26a-242">In hello **indirizzo di posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4b26a-242">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="4b26a-243">b.</span><span class="sxs-lookup"><span data-stu-id="4b26a-243">b.</span></span> <span data-ttu-id="4b26a-244">In hello **nome completo** casella di testo, nome completo del tipo di utente hello come Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b26a-244">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="4b26a-245">c.</span><span class="sxs-lookup"><span data-stu-id="4b26a-245">c.</span></span> <span data-ttu-id="4b26a-246">In hello **Username** casella Tipo hello email dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4b26a-246">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="4b26a-247">d.</span><span class="sxs-lookup"><span data-stu-id="4b26a-247">d.</span></span> <span data-ttu-id="4b26a-248">In hello **Password** casella di testo, digitare la password dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="4b26a-248">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="4b26a-249">e.</span><span class="sxs-lookup"><span data-stu-id="4b26a-249">e.</span></span> <span data-ttu-id="4b26a-250">Fare clic su **Create User** (Crea utente).</span><span class="sxs-lookup"><span data-stu-id="4b26a-250">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4b26a-251">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b26a-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4b26a-252">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSAML SSO per Jira dalla risoluzione GmbH.</span><span class="sxs-lookup"><span data-stu-id="4b26a-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Jira by resolution GmbH.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4b26a-254">**tooassign Britta Simon tooSAML SSO per Jira dalla risoluzione GmbH, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4b26a-254">**tooassign Britta Simon tooSAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b26a-255">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4b26a-257">Nell'elenco di applicazioni hello, selezionare **SAML SSO per Jira dalla risoluzione GmbH**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-257">In hello applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="4b26a-259">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4b26a-261">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-261">Click **Add** button.</span></span> <span data-ttu-id="4b26a-262">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4b26a-264">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="4b26a-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4b26a-265">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b26a-266">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4b26a-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b26a-267">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4b26a-267">Testing single sign-on</span></span>

<span data-ttu-id="4b26a-268">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4b26a-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4b26a-269">Quando si fa clic hello SAML SSO per Jira dal riquadro GmbH risoluzione in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato-on SAML SSO per Jira dalla risoluzione GmbH applicazione.</span><span class="sxs-lookup"><span data-stu-id="4b26a-269">When you click hello SAML SSO for Jira by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="4b26a-270">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4b26a-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4b26a-271">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4b26a-271">Additional resources</span></span>

* [<span data-ttu-id="4b26a-272">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b26a-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b26a-273">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b26a-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

