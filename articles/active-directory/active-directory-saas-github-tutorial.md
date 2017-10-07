---
title: 'Esercitazione: Integrazione di Azure Active Directory con GitHub | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e GitHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="d5d65-103">Esercitazione: Integrazione di Azure Active Directory con GitHub</span><span class="sxs-lookup"><span data-stu-id="d5d65-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="d5d65-104">In questa esercitazione, è illustrato come toointegrate GitHub con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d5d65-104">In this tutorial, you learn how toointegrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d5d65-105">Integrazione di GitHub con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d5d65-105">Integrating GitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d5d65-106">È possibile controllare in Azure AD che ha accesso tooGitHub</span><span class="sxs-lookup"><span data-stu-id="d5d65-106">You can control in Azure AD who has access tooGitHub</span></span>
- <span data-ttu-id="d5d65-107">È possibile abilitare l'utenti tooautomatically get connesso tooGitHub (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5d65-107">You can enable your users tooautomatically get signed-on tooGitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d5d65-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="d5d65-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="d5d65-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d5d65-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5d65-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d5d65-110">Prerequisites</span></span>

<span data-ttu-id="d5d65-111">integrazione di Azure AD con GitHub tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d5d65-111">tooconfigure Azure AD integration with GitHub, you need hello following items:</span></span>

- <span data-ttu-id="d5d65-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5d65-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d5d65-113">Sottoscrizione di GitHub abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d5d65-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="d5d65-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d5d65-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="d5d65-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="d5d65-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d5d65-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d5d65-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d5d65-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d5d65-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="d5d65-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d5d65-118">Scenario description</span></span>
<span data-ttu-id="d5d65-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d5d65-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d5d65-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="d5d65-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d5d65-121">Aggiunta di GitHub dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d5d65-121">Adding GitHub from hello gallery</span></span>
2. <span data-ttu-id="d5d65-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5d65-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-hello-gallery"></a><span data-ttu-id="d5d65-123">Aggiunta di GitHub dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d5d65-123">Adding GitHub from hello gallery</span></span>
<span data-ttu-id="d5d65-124">integrazione hello tooconfigure di GitHub in Azure AD, è necessario tooadd GitHub dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d5d65-124">tooconfigure hello integration of GitHub into Azure AD, you need tooadd GitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d5d65-125">**tooadd GitHub dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d5d65-125">**tooadd GitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5d65-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d5d65-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d5d65-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d5d65-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d5d65-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="d5d65-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d5d65-133">Nella casella di ricerca hello, digitare **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-133">In hello search box, type **GitHub.com**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="d5d65-135">Nel riquadro dei risultati hello, selezionare **GitHub**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d5d65-135">In hello results panel, select **GitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d5d65-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5d65-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d5d65-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con GitHub in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d5d65-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d5d65-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in GitHub è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5d65-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="d5d65-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in GitHub deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="d5d65-140">In other words, a link relationship between an Azure AD user and hello related user in GitHub needs toobe established.</span></span>

<span data-ttu-id="d5d65-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in GitHub.</span><span class="sxs-lookup"><span data-stu-id="d5d65-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in GitHub.</span></span>

<span data-ttu-id="d5d65-142">tooconfigure e prova AD Azure single sign-on con GitHub, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="d5d65-142">tooconfigure and test Azure AD single sign-on with GitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d5d65-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d5d65-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d5d65-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d5d65-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d5d65-145">**[Creazione di un utente test GitHub](#creating-a-GitHub-test-user)**  -toohave un equivalente di Britta Simon in GitHub che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d5d65-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - toohave a counterpart of Britta Simon in GitHub that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="d5d65-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d5d65-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d5d65-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="d5d65-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d5d65-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5d65-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d5d65-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione GitHub.</span><span class="sxs-lookup"><span data-stu-id="d5d65-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="d5d65-150">**Azure AD tooconfigure single sign-on con GitHub, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d5d65-150">**tooconfigure Azure AD single sign-on with GitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5d65-151">Nel portale di gestione di Azure hello in hello **GitHub** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-151">In hello Azure Management portal, on hello **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d5d65-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d5d65-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="d5d65-155">In hello **GitHub dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d5d65-155">On hello **GitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="d5d65-157">a.</span><span class="sxs-lookup"><span data-stu-id="d5d65-157">a.</span></span> <span data-ttu-id="d5d65-158">In hello **Sign-on URL** casella di testo, tipo di valore hello di:`https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="d5d65-158">In hello **Sign-on URL** textbox, type hello value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="d5d65-159">b.</span><span class="sxs-lookup"><span data-stu-id="d5d65-159">b.</span></span> <span data-ttu-id="d5d65-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="d5d65-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d5d65-161">Si noti che queste non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="d5d65-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="d5d65-162">È necessario tooupdate questi valori con hello effettivo tramite URL e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="d5d65-162">You have tooupdate these values with hello actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="d5d65-163">In questo caso, è consigliabile si toouse hello valore univoco della stringa nell'identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="d5d65-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="d5d65-164">Passare tooGitHub Admin sezione tooretrieve questi valori.</span><span class="sxs-lookup"><span data-stu-id="d5d65-164">Go tooGitHub Admin section tooretrieve these values.</span></span> 

4. <span data-ttu-id="d5d65-165">In hello **gli attributi utente** selezionare **identificatore utente** come user.mail.</span><span class="sxs-lookup"><span data-stu-id="d5d65-165">On hello **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="d5d65-167">In hello **certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-167">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="d5d65-169">In hello **creare nuovo certificato** finestra di dialogo, fare clic sull'icona calendario hello e selezionare un **data di scadenza**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-169">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="d5d65-170">Fare quindi clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-170">Then click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="d5d65-172">In hello **certificato di firma SAML** selezionare **attivare di nuovo certificato** e fare clic su **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="d5d65-172">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="d5d65-174">Nel menu a comparsa hello **il certificato di Rollover** finestra, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-174">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="d5d65-176">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d5d65-176">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="d5d65-178">In hello **GitHub configurazione** fare clic su **configurazione di GitHub** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="d5d65-178">On hello **GitHub Configuration** section, click **Configure GitHub** tooopen **Configure sign-on** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="d5d65-181">In un'altra finestra del Web browser accedere al sito aziendale di GitHub come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d5d65-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="d5d65-182">Passare troppo**impostazioni** e fare clic su **sicurezza**</span><span class="sxs-lookup"><span data-stu-id="d5d65-182">Navigate too**Settings** and click **Security**</span></span>

    ![Impostazioni](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="d5d65-184">Controllare hello **Enable SAML authentication** casella rivelare hello Single Sign-on i campi della configurazione.</span><span class="sxs-lookup"><span data-stu-id="d5d65-184">Check hello **Enable SAML authentication** box, revealing hello Single Sign-on configuration fields.</span></span> <span data-ttu-id="d5d65-185">Utilizzare quindi hello single sign-on URL valore tooupdate hello URL Single sign-on nella configurazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5d65-185">Then, use hello single sign-on URL value tooupdate hello Single sign-on URL on Azure AD configuration.</span></span>

    ![Impostazioni](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="d5d65-187">Configurare hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="d5d65-187">Configure hello following fields:</span></span>

    <span data-ttu-id="d5d65-188">a.</span><span class="sxs-lookup"><span data-stu-id="d5d65-188">a.</span></span> <span data-ttu-id="d5d65-189">**URL di accesso**: immettere **SAML Single sign-on Service URL** da hello **configurazione di GitHub** sezione su Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5d65-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="d5d65-190">b.</span><span class="sxs-lookup"><span data-stu-id="d5d65-190">b.</span></span> <span data-ttu-id="d5d65-191">**Autorità di certificazione**: immettere **ID entità SAML** da hello **configurazione di GitHub** sezione su Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5d65-191">**Issuer**: Enter **SAML Entity ID** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="d5d65-192">c.</span><span class="sxs-lookup"><span data-stu-id="d5d65-192">c.</span></span> <span data-ttu-id="d5d65-193">**Certificato pubblico**: hello aprire scaricato certificato da Azure AD in un contenuto di hello in blocco note e copiare inclusi "BEGIN" e "Fine certificato"</span><span class="sxs-lookup"><span data-stu-id="d5d65-193">**Public Certificate**: Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Impostazioni](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="d5d65-195">Fare clic su **configurazione SAML del Test** tooconfirm che non gli errori di convalida o errori durante l'accesso SSO.</span><span class="sxs-lookup"><span data-stu-id="d5d65-195">Click on **Test SAML configuration** tooconfirm that no validation failures or errors during SSO.</span></span>

    ![Impostazioni](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="d5d65-197">Fare clic su **Save**</span><span class="sxs-lookup"><span data-stu-id="d5d65-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d5d65-198">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5d65-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="d5d65-199">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="d5d65-199">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d5d65-201">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d5d65-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5d65-202">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d5d65-202">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d5d65-204">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="d5d65-204">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d5d65-206">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d5d65-206">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d5d65-208">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d5d65-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d5d65-210">a.</span><span class="sxs-lookup"><span data-stu-id="d5d65-210">a.</span></span> <span data-ttu-id="d5d65-211">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d5d65-212">b.</span><span class="sxs-lookup"><span data-stu-id="d5d65-212">b.</span></span> <span data-ttu-id="d5d65-213">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d5d65-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d5d65-214">c.</span><span class="sxs-lookup"><span data-stu-id="d5d65-214">c.</span></span> <span data-ttu-id="d5d65-215">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d5d65-216">d.</span><span class="sxs-lookup"><span data-stu-id="d5d65-216">d.</span></span> <span data-ttu-id="d5d65-217">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="d5d65-218">Creazione di un utente test GitHub</span><span class="sxs-lookup"><span data-stu-id="d5d65-218">Creating a GitHub test user</span></span>

<span data-ttu-id="d5d65-219">In ordine tooenable Azure AD utenti toolog in GitHub, è necessario eseguirne il provisioning in GitHub.</span><span class="sxs-lookup"><span data-stu-id="d5d65-219">In order tooenable Azure AD users toolog into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="d5d65-220">Nel caso di hello di GitHub, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="d5d65-220">In hello case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="d5d65-221">**eseguire un account utente, tooprovision hello i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="d5d65-221">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5d65-222">Accedi tooyour sito aziendale GitHub come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d5d65-222">Log in tooyour GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="d5d65-223">Fare clic su **Persone**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-223">Click **People**.</span></span>

    <span data-ttu-id="d5d65-224">![Persone](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="d5d65-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="d5d65-225">Fare clic su **Invite member** (Invita membro).</span><span class="sxs-lookup"><span data-stu-id="d5d65-225">Click **Invite member**.</span></span>

    <span data-ttu-id="d5d65-226">![Invitare utenti](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invitare utenti")</span><span class="sxs-lookup"><span data-stu-id="d5d65-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="d5d65-227">In hello **membro invito** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d5d65-227">On hello **Invite member** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="d5d65-228">a.</span><span class="sxs-lookup"><span data-stu-id="d5d65-228">a.</span></span> <span data-ttu-id="d5d65-229">In hello **posta elettronica** casella di testo, digitare hello indirizzo di posta elettronica dell'account di Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d5d65-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="d5d65-230">![Invitare persone](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invitare persone")</span><span class="sxs-lookup"><span data-stu-id="d5d65-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="d5d65-231">b.</span><span class="sxs-lookup"><span data-stu-id="d5d65-231">b.</span></span> <span data-ttu-id="d5d65-232">Fare clic su **Send Invitation** (Invia invito).</span><span class="sxs-lookup"><span data-stu-id="d5d65-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="d5d65-233">![Invitare persone](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invitare persone")</span><span class="sxs-lookup"><span data-stu-id="d5d65-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="d5d65-234">titolare dell'account di Hello Azure Active Directory riceverà un messaggio di posta elettronica e seguire il proprio account tooconfirm un collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="d5d65-234">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d5d65-235">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5d65-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d5d65-236">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooGitHub proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="d5d65-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooGitHub.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d5d65-238">**tooassign Britta Simon tooGitHub, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d5d65-238">**tooassign Britta Simon tooGitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5d65-239">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-239">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d5d65-241">Nell'elenco di applicazioni hello, selezionare **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-241">In hello applications list, select **GitHub.com**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="d5d65-243">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d5d65-245">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-245">Click **Add** button.</span></span> <span data-ttu-id="d5d65-246">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d5d65-248">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="d5d65-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d5d65-249">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d5d65-250">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d5d65-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="d5d65-251">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d5d65-251">Testing single sign-on</span></span>

<span data-ttu-id="d5d65-252">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d5d65-252">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d5d65-253">Quando si fa clic su riquadro GitHub hello in hello Pannello di accesso, è necessario ottenere tooyour connesso GitHub applicazione.</span><span class="sxs-lookup"><span data-stu-id="d5d65-253">When you click hello GitHub tile in hello Access Panel, you should get signed-on tooyour GitHub application.</span></span> <span data-ttu-id="d5d65-254">Sarà possibile registrazione come un account aziendale ma toolog necessario con l'account personale.</span><span class="sxs-lookup"><span data-stu-id="d5d65-254">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d5d65-255">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d5d65-255">Additional resources</span></span>

* [<span data-ttu-id="d5d65-256">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5d65-256">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d5d65-257">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5d65-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
