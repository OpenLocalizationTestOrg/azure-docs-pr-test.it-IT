---
title: 'Esercitazione: Integrazione di Azure Active Directory con Inkling | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Inkling.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 544101f1972ec16222406b761d2b6f4987458df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="4b588-103">Esercitazione: Integrazione di Azure Active Directory con Inkling</span><span class="sxs-lookup"><span data-stu-id="4b588-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="4b588-104">In questa esercitazione, è illustrato come toointegrate Inkling con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b588-104">In this tutorial, you learn how toointegrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b588-105">Integrazione Inkling con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4b588-105">Integrating Inkling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4b588-106">È possibile controllare in Azure AD che ha accesso tooInkling</span><span class="sxs-lookup"><span data-stu-id="4b588-106">You can control in Azure AD who has access tooInkling</span></span>
- <span data-ttu-id="4b588-107">È possibile abilitare l'utenti tooautomatically get connesso tooInkling (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b588-107">You can enable your users tooautomatically get signed-on tooInkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b588-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="4b588-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="4b588-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b588-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b588-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4b588-110">Prerequisites</span></span>

<span data-ttu-id="4b588-111">integrazione di Azure AD con Inkling tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4b588-111">tooconfigure Azure AD integration with Inkling, you need hello following items:</span></span>

- <span data-ttu-id="4b588-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b588-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b588-113">Sottoscrizione di Inkling abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4b588-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="4b588-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4b588-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="4b588-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4b588-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b588-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4b588-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="4b588-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b588-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="4b588-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4b588-118">Scenario description</span></span>
<span data-ttu-id="4b588-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4b588-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b588-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4b588-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b588-121">Aggiunta di Inkling dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4b588-121">Adding Inkling from hello gallery</span></span>
2. <span data-ttu-id="4b588-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b588-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-hello-gallery"></a><span data-ttu-id="4b588-123">Aggiunta di Inkling dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4b588-123">Adding Inkling from hello gallery</span></span>
<span data-ttu-id="4b588-124">integrazione hello tooconfigure di Inkling in Azure AD, è necessario tooadd Inkling dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4b588-124">tooconfigure hello integration of Inkling into Azure AD, you need tooadd Inkling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4b588-125">**tooadd Inkling dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4b588-125">**tooadd Inkling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b588-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4b588-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4b588-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4b588-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4b588-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4b588-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4b588-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="4b588-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4b588-133">Nella casella di ricerca hello, digitare **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="4b588-133">In hello search box, type **Inkling**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="4b588-135">Nel riquadro dei risultati hello, selezionare **Inkling**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4b588-135">In hello results panel, select **Inkling**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b588-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b588-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b588-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Inkling in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4b588-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4b588-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Inkling è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b588-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Inkling is tooa user in Azure AD.</span></span> <span data-ttu-id="4b588-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Inkling deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="4b588-140">In other words, a link relationship between an Azure AD user and hello related user in Inkling needs toobe established.</span></span>

<span data-ttu-id="4b588-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Inkling.</span><span class="sxs-lookup"><span data-stu-id="4b588-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Inkling.</span></span>

<span data-ttu-id="4b588-142">tooconfigure e prova AD Azure single sign-on con Inkling, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4b588-142">tooconfigure and test Azure AD single sign-on with Inkling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4b588-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4b588-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4b588-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b588-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b588-145">**[Creazione di un utente test Inkling](#creating-an-inkling-test-user)**  -toohave un equivalente di Britta Simon in Inkling toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="4b588-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - toohave a counterpart of Britta Simon in Inkling that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="4b588-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4b588-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b588-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b588-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b588-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b588-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b588-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione Inkling.</span><span class="sxs-lookup"><span data-stu-id="4b588-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="4b588-150">**Azure AD tooconfigure single sign-on con Inkling, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4b588-150">**tooconfigure Azure AD single sign-on with Inkling, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b588-151">Nel portale di gestione di Azure hello in hello **Inkling** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4b588-151">In hello Azure Management portal, on hello **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4b588-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4b588-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="4b588-155">In hello **Inkling dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4b588-155">On hello **Inkling Domain and URLs** section, perform hello following steps:</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="4b588-157">a.</span><span class="sxs-lookup"><span data-stu-id="4b588-157">a.</span></span> <span data-ttu-id="4b588-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="4b588-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="4b588-159">b.</span><span class="sxs-lookup"><span data-stu-id="4b588-159">b.</span></span> <span data-ttu-id="4b588-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="4b588-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b588-161">Si noti che queste non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="4b588-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="4b588-162">È necessario tooupdate questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="4b588-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="4b588-163">Contatto [team di supporto Inkling](mailto:press@inkling.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="4b588-163">Contact [Inkling support team](mailto:press@inkling.com) tooget these values.</span></span>

4. <span data-ttu-id="4b588-164">In hello **certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="4b588-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="4b588-166">In hello **creare nuovo certificato** finestra di dialogo, fare clic sull'icona calendario hello e selezionare un **data di scadenza**.</span><span class="sxs-lookup"><span data-stu-id="4b588-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="4b588-167">Fare quindi clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="4b588-167">Then click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="4b588-169">In hello **certificato di firma SAML** selezionare **attivare di nuovo certificato** e fare clic su **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4b588-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="4b588-171">Nel menu a comparsa hello **il certificato di Rollover** finestra, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b588-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="4b588-173">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4b588-173">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="4b588-175">tooget SSO è configurato per l'applicazione, contattare [team di supporto Inkling](mailto:press@inkling.com) e fornire loro con scaricato **metadati**.</span><span class="sxs-lookup"><span data-stu-id="4b588-175">tooget SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b588-176">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b588-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b588-177">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="4b588-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4b588-179">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4b588-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b588-180">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4b588-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b588-182">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="4b588-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b588-184">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4b588-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b588-186">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4b588-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b588-188">a.</span><span class="sxs-lookup"><span data-stu-id="4b588-188">a.</span></span> <span data-ttu-id="4b588-189">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b588-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b588-190">b.</span><span class="sxs-lookup"><span data-stu-id="4b588-190">b.</span></span> <span data-ttu-id="4b588-191">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4b588-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b588-192">c.</span><span class="sxs-lookup"><span data-stu-id="4b588-192">c.</span></span> <span data-ttu-id="4b588-193">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="4b588-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4b588-194">d.</span><span class="sxs-lookup"><span data-stu-id="4b588-194">d.</span></span> <span data-ttu-id="4b588-195">Fare clic su **Create**(Crea).</span><span class="sxs-lookup"><span data-stu-id="4b588-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="4b588-196">Creazione di un utente di test di Inkling</span><span class="sxs-lookup"><span data-stu-id="4b588-196">Creating an Inkling test user</span></span>

<span data-ttu-id="4b588-197">In questa sezione viene creato un utente chiamato Britta Simon in Inkling.</span><span class="sxs-lookup"><span data-stu-id="4b588-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="4b588-198">Rivolgersi [team di supporto Inkling](mailto:press@inkling.com) utenti hello tooadd nella piattaforma Inkling hello.</span><span class="sxs-lookup"><span data-stu-id="4b588-198">Please work with [Inkling support team](mailto:press@inkling.com) tooadd hello users in hello Inkling platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4b588-199">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b588-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4b588-200">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooInkling proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="4b588-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooInkling.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4b588-202">**tooassign Britta Simon tooInkling, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4b588-202">**tooassign Britta Simon tooInkling, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b588-203">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4b588-203">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4b588-205">Nell'elenco di applicazioni hello, selezionare **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="4b588-205">In hello applications list, select **Inkling**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="4b588-207">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4b588-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4b588-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4b588-209">Click **Add** button.</span></span> <span data-ttu-id="4b588-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4b588-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4b588-212">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="4b588-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4b588-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4b588-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b588-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4b588-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="4b588-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4b588-215">Testing single sign-on</span></span>

<span data-ttu-id="4b588-216">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4b588-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4b588-217">Quando si fa clic su riquadro Inkling hello in hello Pannello di accesso, è necessario ottenere applicazione Inkling tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="4b588-217">When you click hello Inkling tile in hello Access Panel, you should get automatically signed-on tooyour Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4b588-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4b588-218">Additional resources</span></span>

* [<span data-ttu-id="4b588-219">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b588-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b588-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b588-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png