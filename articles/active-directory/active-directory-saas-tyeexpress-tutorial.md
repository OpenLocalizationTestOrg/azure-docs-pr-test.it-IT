---
title: 'Esercitazione: Integrazione di Azure Active Directory con T&E Express| Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e T & E Express.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="d3459-103">Esercitazione: Integrazione di Azure Active Directory con T&E Express</span><span class="sxs-lookup"><span data-stu-id="d3459-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="d3459-104">In questa esercitazione, è illustrato come toointegrate T & E Express con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3459-104">In this tutorial, you learn how toointegrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3459-105">T & Express E l'integrazione con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d3459-105">Integrating T&E Express with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d3459-106">È possibile controllare in Azure AD che ha tooT accesso & E Express</span><span class="sxs-lookup"><span data-stu-id="d3459-106">You can control in Azure AD who has access tooT&E Express</span></span>
- <span data-ttu-id="d3459-107">È possibile abilitare le get connesso tooT tooautomatically di utenti & E Express (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3459-107">You can enable your users tooautomatically get signed-on tooT&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d3459-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="d3459-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="d3459-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d3459-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3459-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d3459-110">Prerequisites</span></span>

<span data-ttu-id="d3459-111">integrazione di Azure AD con T & E Express tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d3459-111">tooconfigure Azure AD integration with T&E Express, you need hello following items:</span></span>

- <span data-ttu-id="d3459-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3459-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3459-113">Sottoscrizione di T&E Express abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d3459-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3459-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d3459-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3459-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="d3459-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3459-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d3459-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d3459-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3459-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3459-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d3459-118">Scenario description</span></span>
<span data-ttu-id="d3459-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d3459-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3459-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="d3459-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3459-121">Aggiunta di T & Express E dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d3459-121">Adding T&E Express from hello gallery</span></span>
2. <span data-ttu-id="d3459-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3459-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-hello-gallery"></a><span data-ttu-id="d3459-123">Aggiunta di T & Express E dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d3459-123">Adding T&E Express from hello gallery</span></span>
<span data-ttu-id="d3459-124">integrazione hello tooconfigure di T & E Express in Azure AD, è necessario tooadd T & E Express dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d3459-124">tooconfigure hello integration of T&E Express into Azure AD, you need tooadd T&E Express from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d3459-125">**tooadd T & E Express dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d3459-125">**tooadd T&E Express from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3459-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d3459-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d3459-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d3459-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d3459-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d3459-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d3459-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="d3459-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d3459-133">Nella casella di ricerca hello, digitare **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="d3459-133">In hello search box, type **T&E Express**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="d3459-135">Nel riquadro dei risultati hello, selezionare **T & E Express**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d3459-135">In hello results panel, select **T&E Express**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d3459-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3459-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d3459-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con T&E Express usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d3459-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d3459-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in T & E Express è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3459-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in T&E Express is tooa user in Azure AD.</span></span> <span data-ttu-id="d3459-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in T & E Express toobe esigenze stabilita.</span><span class="sxs-lookup"><span data-stu-id="d3459-140">In other words, a link relationship between an Azure AD user and hello related user in T&E Express needs toobe established.</span></span>

<span data-ttu-id="d3459-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** T & E Express.</span><span class="sxs-lookup"><span data-stu-id="d3459-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in T&E Express.</span></span>

<span data-ttu-id="d3459-142">tooconfigure e prova AD Azure single sign-on con T & E Express, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="d3459-142">tooconfigure and test Azure AD single sign-on with T&E Express, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d3459-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d3459-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d3459-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3459-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3459-145">**[Creazione di un utente di test T & E Express](#creating-a-te-express-test-user)**  -toohave un equivalente di Britta Simon T & E Express che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d3459-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - toohave a counterpart of Britta Simon in T&E Express that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="d3459-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d3459-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3459-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="d3459-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d3459-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3459-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d3459-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione T & E Express.</span><span class="sxs-lookup"><span data-stu-id="d3459-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="d3459-150">**tooconfigure AD Azure single sign-on con T & E Express, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d3459-150">**tooconfigure Azure AD single sign-on with T&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3459-151">Nel portale di gestione di Azure hello in hello **T & E Express** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d3459-151">In hello Azure Management portal, on hello **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d3459-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d3459-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="d3459-155">In hello **T & E dominio di Express e URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d3459-155">On hello **T&E Express Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="d3459-157">a.</span><span class="sxs-lookup"><span data-stu-id="d3459-157">a.</span></span> <span data-ttu-id="d3459-158">In hello **identificatore** casella di testo, tipo di valore hello di:`https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="d3459-158">In hello **Identifier** textbox, type hello value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="d3459-159">b.</span><span class="sxs-lookup"><span data-stu-id="d3459-159">b.</span></span> <span data-ttu-id="d3459-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="d3459-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d3459-161">Si noti che queste non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="d3459-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="d3459-162">È necessario tooupdate questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="d3459-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="d3459-163">In questo caso, è consigliabile si toouse hello valore univoco della stringa nell'identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="d3459-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="d3459-164">Contatto [T & Express E team di supporto](http://www.tyeexpress.com/contacto.aspx) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="d3459-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) tooget these values.</span></span>

5. <span data-ttu-id="d3459-165">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file XML hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d3459-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="d3459-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d3459-167">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d3459-169">tooconfigure single sign-on sul **T & E Express** lato, account di accesso toohello T & applicazione rapido E senza SAML Single sign-on utilizzando le credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="d3459-169">tooconfigure single sign-on on **T&E Express** side, login toohello T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="d3459-170">In hello **Admin** scheda, fare clic su **dominio SAML** pagina Impostazioni di SAML hello tooOpen.</span><span class="sxs-lookup"><span data-stu-id="d3459-170">Under hello **Admin** Tab, Click on **SAML domain** tooOpen hello SAML settings page.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="d3459-172">Seleziona hello **Activar(Activate)** opzione **n** troppo**SI(Yes)**.</span><span class="sxs-lookup"><span data-stu-id="d3459-172">Select hello **Activar(Activate)** option from **No** too**SI(Yes)**.</span></span> <span data-ttu-id="d3459-173">In hello **i metadati del Provider di identità** casella di testo, XML cui si dispone di metadati di Incolla hello donwloaded dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d3459-173">In hello **Identity Provider Metadata** textbox, paste hello metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="d3459-175">Fare clic su hello **Guardar(Save)** pulsante Impostazioni hello toosave.</span><span class="sxs-lookup"><span data-stu-id="d3459-175">Click on hello **Guardar(Save)** button toosave hello settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d3459-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3459-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="d3459-177">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="d3459-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d3459-179">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d3459-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3459-180">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d3459-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d3459-182">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="d3459-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d3459-184">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d3459-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d3459-186">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d3459-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d3459-188">a.</span><span class="sxs-lookup"><span data-stu-id="d3459-188">a.</span></span> <span data-ttu-id="d3459-189">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d3459-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3459-190">b.</span><span class="sxs-lookup"><span data-stu-id="d3459-190">b.</span></span> <span data-ttu-id="d3459-191">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d3459-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d3459-192">c.</span><span class="sxs-lookup"><span data-stu-id="d3459-192">c.</span></span> <span data-ttu-id="d3459-193">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="d3459-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d3459-194">d.</span><span class="sxs-lookup"><span data-stu-id="d3459-194">d.</span></span> <span data-ttu-id="d3459-195">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d3459-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="d3459-196">Creare un utente test di T&E Express</span><span class="sxs-lookup"><span data-stu-id="d3459-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="d3459-197">In ordine tooenable Azure AD utenti toolog in T & E Express, è necessario essere il provisioning in T & E Express.</span><span class="sxs-lookup"><span data-stu-id="d3459-197">In order tooenable Azure AD users toolog into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="d3459-198">Nel caso di T&E Express, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="d3459-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="d3459-199">**eseguire un account utente, tooprovision hello i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="d3459-199">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3459-200">Accedi tooyour T & E Express sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d3459-200">Log in tooyour T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="d3459-201">Sotto il tag di amministrazione, fare clic su pagina master utenti hello tooopen gli utenti.</span><span class="sxs-lookup"><span data-stu-id="d3459-201">Under Admin tag, click on Users tooopen hello Users master page.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="d3459-203">Nella home page di hello, fare clic su  **+**  utenti hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d3459-203">On hello home page, click on **+** tooadd hello users.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="d3459-205">Immettere tutti i dettagli di obbligatorio hello come richiesto nel modulo hello e fare clic su hello Salva pulsante toosave hello dettagli.</span><span class="sxs-lookup"><span data-stu-id="d3459-205">Enter all hello mandatory details as asked in hello form and click hello save button toosave hello details.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Aggiungere un dipendente](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d3459-208">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3459-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d3459-209">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione proprio tooT accesso & E Express.</span><span class="sxs-lookup"><span data-stu-id="d3459-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooT&E Express.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d3459-211">**tooassign tooT Britta Simon & E Express, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d3459-211">**tooassign Britta Simon tooT&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="d3459-212">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d3459-212">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d3459-214">Nell'elenco di applicazioni hello, selezionare **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="d3459-214">In hello applications list, select **T&E Express**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="d3459-216">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d3459-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d3459-218">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d3459-218">Click **Add** button.</span></span> <span data-ttu-id="d3459-219">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d3459-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d3459-221">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="d3459-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d3459-222">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d3459-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d3459-223">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d3459-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d3459-224">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d3459-224">Testing single sign-on</span></span>

<span data-ttu-id="d3459-225">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d3459-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d3459-226">Quando si fa clic hello T & E Express porzione hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour T & Express E applicazione.</span><span class="sxs-lookup"><span data-stu-id="d3459-226">When you click hello T&E Express tile in hello Access Panel, you should get automatically signed-on tooyour T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d3459-227">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d3459-227">Additional resources</span></span>

* [<span data-ttu-id="d3459-228">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3459-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3459-229">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3459-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

