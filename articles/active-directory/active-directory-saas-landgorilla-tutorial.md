---
title: 'Esercitazione: Integrazione di Azure Active Directory con Land Gorilla Client| Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Gorilla terreni.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: e95a30551e636108fe22a7ab6d1827bc12d7f9a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="7ee7c-103">Esercitazione: Integrazione di Azure Active Directory con Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="7ee7c-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="7ee7c-104">In questa esercitazione, è illustrato come toointegrate terreni Gorilla Client con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7ee7c-104">In this tutorial, you learn how toointegrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ee7c-105">Integrazione di terreni Gorilla Client con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="7ee7c-105">Integrating Land Gorilla Client with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7ee7c-106">È possibile controllare in Azure AD che ha accesso tooLand Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="7ee7c-106">You can control in Azure AD who has access tooLand Gorilla Client</span></span>
- <span data-ttu-id="7ee7c-107">È possibile abilitare l'utenti tooautomatically get connesso tooLand Client Gorilla (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ee7c-107">You can enable your users tooautomatically get signed-on tooLand Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ee7c-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="7ee7c-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="7ee7c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7ee7c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7ee7c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7ee7c-110">Prerequisites</span></span>

<span data-ttu-id="7ee7c-111">integrazione di Azure AD con Client di terreni Gorilla tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="7ee7c-111">tooconfigure Azure AD integration with Land Gorilla Client, you need hello following items:</span></span>

- <span data-ttu-id="7ee7c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ee7c-113">Sottoscrizione di Land Gorilla Client abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7ee7c-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="7ee7c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="7ee7c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="7ee7c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ee7c-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7ee7c-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ee7c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="7ee7c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="7ee7c-118">Scenario description</span></span>
<span data-ttu-id="7ee7c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ee7c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="7ee7c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ee7c-121">Aggiunta del Client di terreni Gorilla dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="7ee7c-121">Adding Land Gorilla Client from hello gallery</span></span>
2. <span data-ttu-id="7ee7c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ee7c-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-hello-gallery"></a><span data-ttu-id="7ee7c-123">Aggiunta del Client di terreni Gorilla dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="7ee7c-123">Adding Land Gorilla Client from hello gallery</span></span>
<span data-ttu-id="7ee7c-124">integrazione hello tooconfigure di terreni Gorilla Client in Azure AD, è necessario tooadd terreni Gorilla Client dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-124">tooconfigure hello integration of Land Gorilla Client into Azure AD, you need tooadd Land Gorilla Client from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7ee7c-125">**tooadd terreni Gorilla Client dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7ee7c-125">**tooadd Land Gorilla Client from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ee7c-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7ee7c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7ee7c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="7ee7c-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="7ee7c-133">Nella casella di ricerca hello, digitare **terreni Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-133">In hello search box, type **Land Gorilla Client**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="7ee7c-135">Nel riquadro dei risultati hello, selezionare **terreni Gorilla Client**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-135">In hello results panel, select **Land Gorilla Client**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7ee7c-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ee7c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7ee7c-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Land Gorilla Client in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7ee7c-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7ee7c-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello client Gorilla terreni è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Land Gorilla Client is tooa user in Azure AD.</span></span> <span data-ttu-id="7ee7c-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in terreni Gorilla Client deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-140">In other words, a link relationship between an Azure AD user and hello related user in Land Gorilla Client needs toobe established.</span></span>

<span data-ttu-id="7ee7c-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** terreni Gorilla client.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="7ee7c-142">tooconfigure e prova AD Azure single sign-on con terreni Gorilla Client, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="7ee7c-142">tooconfigure and test Azure AD single sign-on with Land Gorilla Client, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7ee7c-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7ee7c-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con gruppo limitato.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="7ee7c-145">**[Creazione di un utente test terreni Gorilla](#creating-a-land-gorilla-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="7ee7c-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ee7c-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7ee7c-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ee7c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7ee7c-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione Client Gorilla terreni.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="7ee7c-150">**tooconfigure AD Azure single sign-on con terreni Gorilla Client, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7ee7c-150">**tooconfigure Azure AD single sign-on with Land Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ee7c-151">Nel portale di gestione di Azure hello in hello **terreni Gorilla Client** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-151">In hello Azure Management portal, on hello **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="7ee7c-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="7ee7c-155">In hello **terreni Gorilla Client dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7ee7c-155">On hello **Land Gorilla Client Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="7ee7c-157">a.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-157">a.</span></span> <span data-ttu-id="7ee7c-158">In hello **identificatore** casella di testo, il valore di hello tipo utilizzando uno dei hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="7ee7c-158">In hello **Identifier** textbox, type hello value using one of hello following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="7ee7c-159">b.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-159">b.</span></span> <span data-ttu-id="7ee7c-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando un modello di hello:</span><span class="sxs-lookup"><span data-stu-id="7ee7c-160">In hello **Reply URL** textbox, type a URL using one of hello following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="7ee7c-161">Si noti che queste non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="7ee7c-162">È necessario tooupdate questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="7ee7c-163">In questo caso, è consigliabile si toouse hello valore univoco della stringa nell'identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="7ee7c-164">Contatto [team terreni Gorilla Client](https://www.landgorilla.com/support/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="7ee7c-165">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="7ee7c-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="7ee7c-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="7ee7c-169">configurazione di SSO tooget completo per l'applicazione alla fine di terreni Gorilla, contattare [team di supporto Client di terreni Gorilla](https://www.landgorilla.com/support/) e fornire loro hello scaricato **"Metadata XML** file.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-169">tooget SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with hello downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7ee7c-170">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ee7c-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="7ee7c-171">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-171">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="7ee7c-173">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7ee7c-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ee7c-174">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-174">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7ee7c-176">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-176">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7ee7c-178">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-178">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7ee7c-180">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7ee7c-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ee7c-182">a.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-182">a.</span></span> <span data-ttu-id="7ee7c-183">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ee7c-184">b.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-184">b.</span></span> <span data-ttu-id="7ee7c-185">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ee7c-186">c.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-186">c.</span></span> <span data-ttu-id="7ee7c-187">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7ee7c-188">d.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-188">d.</span></span> <span data-ttu-id="7ee7c-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="7ee7c-190">Creare un utente test di Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="7ee7c-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="7ee7c-191">Rivolgersi [team di supporto di terreni Gorilla](https://www.landgorilla.com/support/) utenti hello tooadd nella piattaforma di terreni Gorilla hello.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) tooadd hello users in hello Land Gorilla platform.</span></span>
    
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7ee7c-192">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ee7c-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7ee7c-193">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo proprio tooLand accesso Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLand Gorilla Client.</span></span>

![Assegna utente][200] 

<span data-ttu-id="7ee7c-195">**tooassign tooLand Britta Simon Gorilla Client, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7ee7c-195">**tooassign Britta Simon tooLand Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="7ee7c-196">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-196">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="7ee7c-198">Nell'elenco di applicazioni hello, selezionare **terreni Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-198">In hello applications list, select **Land Gorilla Client**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="7ee7c-200">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="7ee7c-202">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-202">Click **Add** button.</span></span> <span data-ttu-id="7ee7c-203">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="7ee7c-205">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7ee7c-206">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ee7c-207">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="7ee7c-208">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7ee7c-208">Testing single sign-on</span></span>

<span data-ttu-id="7ee7c-209">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-209">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7ee7c-210">Quando si fa clic su riquadro terreni Gorilla Client hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione terreni Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="7ee7c-210">When you click hello Land Gorilla Client tile in hello Access Panel, you should get automatically signed-on tooyour Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7ee7c-211">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7ee7c-211">Additional resources</span></span>

* [<span data-ttu-id="7ee7c-212">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ee7c-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ee7c-213">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ee7c-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
