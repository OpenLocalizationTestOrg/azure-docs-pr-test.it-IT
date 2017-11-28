---
title: 'Esercitazione: integrazione di Azure Active Directory con SAML SSO for Confluence di resolution GmbH | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SAML SSO per confluenza dalla risoluzione GmbH.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: fe50636709857ec49023e24bdc8c6cd8c58e3c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a><span data-ttu-id="5da59-103">Esercitazione: integrazione di Azure Active Directory con SAML SSO for Confluence di resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="5da59-103">Tutorial: Azure Active Directory integration with SAML SSO for Confluence by resolution GmbH</span></span>

<span data-ttu-id="5da59-104">In questa esercitazione, è illustrato come toointegrate SAML SSO per confluenza dalla risoluzione GmbH con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5da59-104">In this tutorial, you learn how toointegrate SAML SSO for Confluence by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5da59-105">L'integrazione di SAML SSO per confluenza dalla risoluzione GmbH con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="5da59-105">Integrating SAML SSO for Confluence by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5da59-106">È possibile controllare in Azure AD che ha accesso tooSAML SSO per confluenza dalla risoluzione GmbH</span><span class="sxs-lookup"><span data-stu-id="5da59-106">You can control in Azure AD who has access tooSAML SSO for Confluence by resolution GmbH</span></span>
- <span data-ttu-id="5da59-107">È possibile abilitare l'utenti tooautomatically get connesso tooSAML SSO per confluenza dalla risoluzione GmbH (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5da59-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Confluence by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5da59-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5da59-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5da59-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5da59-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5da59-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5da59-110">Prerequisites</span></span>

<span data-ttu-id="5da59-111">integrazione di Azure AD con SAML SSO per confluenza dalla risoluzione GmbH tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5da59-111">tooconfigure Azure AD integration with SAML SSO for Confluence by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="5da59-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5da59-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5da59-113">Una sottoscrizione attiva del Single Sign-On di SAML SSO for Confluence di resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="5da59-113">A SAML SSO for Confluence by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5da59-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5da59-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5da59-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="5da59-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5da59-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5da59-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5da59-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5da59-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5da59-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5da59-118">Scenario description</span></span>
<span data-ttu-id="5da59-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5da59-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5da59-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="5da59-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5da59-121">Aggiunta di SAML SSO per confluenza dalla risoluzione GmbH dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5da59-121">Adding SAML SSO for Confluence by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="5da59-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5da59-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="5da59-123">Aggiunta di SAML SSO per confluenza dalla risoluzione GmbH dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5da59-123">Adding SAML SSO for Confluence by resolution GmbH from hello gallery</span></span>

<span data-ttu-id="5da59-124">tooconfigure hello integrazione di SAML SSO per confluenza dalla risoluzione GmbH in Azure AD, è necessario tooadd SAML SSO per confluenza dalla risoluzione GmbH dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5da59-124">tooconfigure hello integration of SAML SSO for Confluence by resolution GmbH into Azure AD, you need tooadd SAML SSO for Confluence by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5da59-125">**tooadd SAML SSO per confluenza dalla risoluzione GmbH dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5da59-125">**tooadd SAML SSO for Confluence by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5da59-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5da59-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5da59-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5da59-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5da59-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5da59-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5da59-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5da59-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5da59-133">Nella casella di ricerca hello, digitare **SAML SSO per confluenza dalla risoluzione GmbH**.</span><span class="sxs-lookup"><span data-stu-id="5da59-133">In hello search box, type **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. <span data-ttu-id="5da59-135">Nel riquadro dei risultati hello, selezionare **SAML SSO per confluenza dalla risoluzione GmbH**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5da59-135">In hello results panel, select **SAML SSO for Confluence by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5da59-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5da59-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="5da59-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAML SSO for Confluence di resolution GmbH con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5da59-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5da59-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in SAML SSO per confluenza dalla risoluzione GmbH è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5da59-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Confluence by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="5da59-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato hello in SAML SSO per confluenza dalla risoluzione GmbH deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="5da59-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Confluence by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="5da59-141">SAML SSO per confluenza dalla risoluzione GmbH, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="5da59-141">In SAML SSO for Confluence by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5da59-142">tooconfigure ed eseguire test AD Azure single sign-on con SAML SSO per confluenza dalla risoluzione GmbH, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="5da59-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5da59-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5da59-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5da59-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5da59-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5da59-145">**[Creazione di un SAML SSO per confluenza dall'utente di prova di risoluzione GmbH](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  -toohave un equivalente di Britta Simon SAML SSO per confluenza dalla risoluzione GmbH che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5da59-145">**[Creating a SAML SSO for Confluence by resolution GmbH test user](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Confluence by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5da59-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5da59-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5da59-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="5da59-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5da59-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5da59-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5da59-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nel SAML SSO per confluenza dalla risoluzione GmbH applicazione.</span><span class="sxs-lookup"><span data-stu-id="5da59-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Confluence by resolution GmbH application.</span></span>

<span data-ttu-id="5da59-150">**tooconfigure AD Azure single sign-on con SAML SSO per confluenza dalla risoluzione GmbH, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5da59-150">**tooconfigure Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="5da59-151">Nel portale di Azure su hello hello **SAML SSO per confluenza dalla risoluzione GmbH** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5da59-151">In hello Azure portal, on hello **SAML SSO for Confluence by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5da59-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5da59-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. <span data-ttu-id="5da59-155">In hello **SAML SSO per confluenza dalla risoluzione GmbH dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="5da59-155">On hello **SAML SSO for Confluence by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    <span data-ttu-id="5da59-157">a.</span><span class="sxs-lookup"><span data-stu-id="5da59-157">a.</span></span> <span data-ttu-id="5da59-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="5da59-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="5da59-159">b.</span><span class="sxs-lookup"><span data-stu-id="5da59-159">b.</span></span> <span data-ttu-id="5da59-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="5da59-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="5da59-161">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="5da59-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="5da59-162">Se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="5da59-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    <span data-ttu-id="5da59-164">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="5da59-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="5da59-165">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="5da59-165">These values are not real.</span></span> <span data-ttu-id="5da59-166">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5da59-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="5da59-167">Contatto [team di supporto SAML SSO per confluenza dalla risoluzione GmbH Client](https://www.resolution.de/go/support) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="5da59-167">Contact [SAML SSO for Confluence by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="5da59-168">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5da59-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. <span data-ttu-id="5da59-170">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5da59-170">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. <span data-ttu-id="5da59-172">In una finestra del web browser, accedere tooyour **SAML SSO per confluenza dal portale di amministrazione di risoluzione GmbH** come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5da59-172">In a different web browser window, log in tooyour **SAML SSO for Confluence by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="5da59-173">Passare il mouse su ruota dentata e scegliere hello **componenti aggiuntivi**.</span><span class="sxs-lookup"><span data-stu-id="5da59-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. <span data-ttu-id="5da59-175">Si è reindirizzato tooAdministrator pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="5da59-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="5da59-176">Immettere la password di hello e fare clic su **conferma** pulsante.</span><span class="sxs-lookup"><span data-stu-id="5da59-176">Enter hello password and click **Confirm** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. <span data-ttu-id="5da59-178">Nella scheda **ATLASSIAN MARKETPLACE** (MARKETPLACE DI ATLASSIAN) fare clic su **Find new add-ons** (Trova nuovi componenti aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="5da59-178">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. <span data-ttu-id="5da59-180">Ricerca **SAML Single Sign On (SSO) per la confluenza** e fare clic su **installare** tooinstall pulsante hello nuovo plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="5da59-180">Search **SAML Single Sign On (SSO) for Confluence** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. <span data-ttu-id="5da59-182">verrà avviata l'installazione di plug-in di Hello.</span><span class="sxs-lookup"><span data-stu-id="5da59-182">hello plugin installation will start.</span></span> <span data-ttu-id="5da59-183">Fare clic su **Close**.</span><span class="sxs-lookup"><span data-stu-id="5da59-183">Click **Close**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. <span data-ttu-id="5da59-186">Fare clic su **Manage**.</span><span class="sxs-lookup"><span data-stu-id="5da59-186">Click **Manage**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. <span data-ttu-id="5da59-188">Fare clic su **configura** tooconfigure hello nuovo plug-in.</span><span class="sxs-lookup"><span data-stu-id="5da59-188">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. <span data-ttu-id="5da59-190">Questo nuovo plug-in è disponibile anche nella scheda**USERS & SECURITY** (UTENTI E SICUREZZA).</span><span class="sxs-lookup"><span data-stu-id="5da59-190">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. <span data-ttu-id="5da59-192">In **SAML SingleSignOn plug-in configurazione** pagina, fare clic su **aggiungere Provider di identità aggiuntive** pulsante Impostazioni hello tooconfigure di Provider di identità.</span><span class="sxs-lookup"><span data-stu-id="5da59-192">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. <span data-ttu-id="5da59-194">In questa pagina eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5da59-194">Perform following steps on this page:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    <span data-ttu-id="5da59-196">a.</span><span class="sxs-lookup"><span data-stu-id="5da59-196">a.</span></span> <span data-ttu-id="5da59-197">Aggiungere **nome** di hello Provider di identità (ad esempio, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5da59-197">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="5da59-198">b.</span><span class="sxs-lookup"><span data-stu-id="5da59-198">b.</span></span> <span data-ttu-id="5da59-199">Aggiungere **descrizione** di hello Provider di identità (ad esempio, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5da59-199">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="5da59-200">c.</span><span class="sxs-lookup"><span data-stu-id="5da59-200">c.</span></span> <span data-ttu-id="5da59-201">Fare clic su **XML** e seleziona hello **metadati** file scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5da59-201">Click **XML** and select hello **Metadata** file that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="5da59-202">d.</span><span class="sxs-lookup"><span data-stu-id="5da59-202">d.</span></span> <span data-ttu-id="5da59-203">Fare clic sul pulsante **Load** (Carica).</span><span class="sxs-lookup"><span data-stu-id="5da59-203">Click **Load** button.</span></span>

    <span data-ttu-id="5da59-204">e.</span><span class="sxs-lookup"><span data-stu-id="5da59-204">e.</span></span> <span data-ttu-id="5da59-205">Legge i metadati IdP hello e popola i campi di hello come evidenziato nella schermata di hello.</span><span class="sxs-lookup"><span data-stu-id="5da59-205">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   
18. <span data-ttu-id="5da59-206">Fare clic su **salvare impostazioni** pulsante Impostazioni hello toosave.</span><span class="sxs-lookup"><span data-stu-id="5da59-206">Click **Save settings** button toosave hello settings.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="5da59-208">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="5da59-208">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5da59-209">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="5da59-209">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5da59-210">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5da59-210">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5da59-211">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5da59-211">Creating an Azure AD test user</span></span>
<span data-ttu-id="5da59-212">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5da59-212">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5da59-214">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5da59-214">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5da59-215">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5da59-215">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5da59-217">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="5da59-217">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5da59-219">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="5da59-219">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5da59-221">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5da59-221">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5da59-223">a.</span><span class="sxs-lookup"><span data-stu-id="5da59-223">a.</span></span> <span data-ttu-id="5da59-224">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5da59-224">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5da59-225">b.</span><span class="sxs-lookup"><span data-stu-id="5da59-225">b.</span></span> <span data-ttu-id="5da59-226">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5da59-226">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5da59-227">c.</span><span class="sxs-lookup"><span data-stu-id="5da59-227">c.</span></span> <span data-ttu-id="5da59-228">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="5da59-228">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5da59-229">d.</span><span class="sxs-lookup"><span data-stu-id="5da59-229">d.</span></span> <span data-ttu-id="5da59-230">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5da59-230">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a><span data-ttu-id="5da59-231">Creazione di un utente di test di SAML SSO for Confluence di resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="5da59-231">Creating a SAML SSO for Confluence by resolution GmbH test user</span></span>

<span data-ttu-id="5da59-232">toolog agli utenti di Azure AD tooenable in tooSAML SSO per confluenza dalla risoluzione GmbH, è necessario eseguirne il provisioning in SAML SSO per confluenza dalla risoluzione GmbH.</span><span class="sxs-lookup"><span data-stu-id="5da59-232">tooenable Azure AD users toolog in tooSAML SSO for Confluence by resolution GmbH, they must be provisioned into SAML SSO for Confluence by resolution GmbH.</span></span>  
<span data-ttu-id="5da59-233">In SAML SSO for Confluence di resolution GmbH il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="5da59-233">In SAML SSO for Confluence by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="5da59-234">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5da59-234">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="5da59-235">Accedi tooyour SAML SSO per confluenza dal sito di risoluzione GmbH aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5da59-235">Log in tooyour SAML SSO for Confluence by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="5da59-236">Passare il mouse su ruota dentata e scegliere hello **Gestione utenti**.</span><span class="sxs-lookup"><span data-stu-id="5da59-236">Hover on cog and click hello **User management**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. <span data-ttu-id="5da59-238">Nella sezione Users (Utenti) fare clic sula scheda **Add users** (Aggiungi utenti). In hello **"Aggiungi utente"** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5da59-238">Under Users section, click **Add users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    <span data-ttu-id="5da59-240">a.</span><span class="sxs-lookup"><span data-stu-id="5da59-240">a.</span></span> <span data-ttu-id="5da59-241">In hello **Username** casella di testo, posta elettronica hello tipo di utente come Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5da59-241">In hello **Username** textbox, type hello email of user like Britta Simon.</span></span>

    <span data-ttu-id="5da59-242">b.</span><span class="sxs-lookup"><span data-stu-id="5da59-242">b.</span></span> <span data-ttu-id="5da59-243">In hello **nome completo** casella di testo, nome completo del tipo hello dell'utente come Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5da59-243">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="5da59-244">c.</span><span class="sxs-lookup"><span data-stu-id="5da59-244">c.</span></span> <span data-ttu-id="5da59-245">In hello **posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="5da59-245">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="5da59-246">d.</span><span class="sxs-lookup"><span data-stu-id="5da59-246">d.</span></span> <span data-ttu-id="5da59-247">In hello **Password** casella di testo, digitare la password per Britta Simon hello.</span><span class="sxs-lookup"><span data-stu-id="5da59-247">In hello **Password** textbox, type hello password for Britta Simon.</span></span>

    <span data-ttu-id="5da59-248">e.</span><span class="sxs-lookup"><span data-stu-id="5da59-248">e.</span></span> <span data-ttu-id="5da59-249">Fare clic su **Conferma Password** digitare nuovamente la password di hello.</span><span class="sxs-lookup"><span data-stu-id="5da59-249">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="5da59-250">f.</span><span class="sxs-lookup"><span data-stu-id="5da59-250">f.</span></span> <span data-ttu-id="5da59-251">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5da59-251">Click **Add** button.</span></span>    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5da59-252">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5da59-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5da59-253">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSAML SSO per confluenza dalla risoluzione GmbH.</span><span class="sxs-lookup"><span data-stu-id="5da59-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Confluence by resolution GmbH.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5da59-255">**tooassign Britta Simon tooSAML SSO per confluenza dalla risoluzione GmbH, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5da59-255">**tooassign Britta Simon tooSAML SSO for Confluence by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="5da59-256">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5da59-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5da59-258">Nell'elenco di applicazioni hello, selezionare **SAML SSO per confluenza dalla risoluzione GmbH**.</span><span class="sxs-lookup"><span data-stu-id="5da59-258">In hello applications list, select **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. <span data-ttu-id="5da59-260">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5da59-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5da59-262">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5da59-262">Click **Add** button.</span></span> <span data-ttu-id="5da59-263">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5da59-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5da59-265">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="5da59-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5da59-266">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5da59-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5da59-267">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5da59-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5da59-268">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5da59-268">Testing single sign-on</span></span>

<span data-ttu-id="5da59-269">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5da59-269">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5da59-270">Quando si fa clic hello SAML SSO per confluenza dal riquadro GmbH risoluzione in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato-on SAML SSO per confluenza dalla risoluzione GmbH applicazione.</span><span class="sxs-lookup"><span data-stu-id="5da59-270">When you click hello SAML SSO for Confluence by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Confluence by resolution GmbH application.</span></span>
<span data-ttu-id="5da59-271">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5da59-271">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5da59-272">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5da59-272">Additional resources</span></span>

* [<span data-ttu-id="5da59-273">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5da59-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5da59-274">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5da59-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

