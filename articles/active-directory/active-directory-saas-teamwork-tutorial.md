---
title: 'Esercitazione: Integrazione di Azure Active Directory con Teamwork | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e il lavoro del team.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f3a88a146f2a0a70de5ef58abd46f7f26b4104f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="9cea8-103">Esercitazione: Integrazione di Azure Active Directory con Teamwork</span><span class="sxs-lookup"><span data-stu-id="9cea8-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="9cea8-104">In questa esercitazione, è illustrato come toointegrate squadra con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9cea8-104">In this tutorial, you learn how toointegrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9cea8-105">Integrazione di lavoro in team con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="9cea8-105">Integrating Teamwork with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9cea8-106">È possibile controllare in Azure AD che ha accesso tooTeamwork</span><span class="sxs-lookup"><span data-stu-id="9cea8-106">You can control in Azure AD who has access tooTeamwork</span></span>
- <span data-ttu-id="9cea8-107">È possibile abilitare l'utenti tooautomatically get connesso tooTeamwork (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cea8-107">You can enable your users tooautomatically get signed-on tooTeamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9cea8-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="9cea8-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="9cea8-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9cea8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cea8-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9cea8-110">Prerequisites</span></span>

<span data-ttu-id="9cea8-111">tooconfigure integrazione di Azure AD con lavoro in team, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="9cea8-111">tooconfigure Azure AD integration with Teamwork, you need hello following items:</span></span>

- <span data-ttu-id="9cea8-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cea8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9cea8-113">Sottoscrizione di Teamwork abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9cea8-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="9cea8-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="9cea8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="9cea8-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="9cea8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9cea8-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="9cea8-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9cea8-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9cea8-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="9cea8-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="9cea8-118">Scenario description</span></span>
<span data-ttu-id="9cea8-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="9cea8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9cea8-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="9cea8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9cea8-121">Aggiunta di lavoro in team dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="9cea8-121">Adding Teamwork from hello gallery</span></span>
2. <span data-ttu-id="9cea8-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cea8-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-hello-gallery"></a><span data-ttu-id="9cea8-123">Aggiunta di lavoro in team dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="9cea8-123">Adding Teamwork from hello gallery</span></span>
<span data-ttu-id="9cea8-124">integrazione hello tooconfigure di lavoro di gruppo in Azure AD, è necessario tooadd squadra dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="9cea8-124">tooconfigure hello integration of Teamwork into Azure AD, you need tooadd Teamwork from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9cea8-125">**tooadd squadra dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9cea8-125">**tooadd Teamwork from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cea8-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="9cea8-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9cea8-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9cea8-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="9cea8-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="9cea8-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="9cea8-133">Nella casella di ricerca hello, digitare **squadra**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-133">In hello search box, type **Teamwork**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="9cea8-135">Nel riquadro dei risultati hello, selezionare **squadra**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9cea8-135">In hello results panel, select **Teamwork**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9cea8-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cea8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9cea8-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Teamwork in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9cea8-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9cea8-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in squadra è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cea8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamwork is tooa user in Azure AD.</span></span> <span data-ttu-id="9cea8-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e utente correlati hello squadra deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="9cea8-140">In other words, a link relationship between an Azure AD user and hello related user in Teamwork needs toobe established.</span></span>

<span data-ttu-id="9cea8-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="9cea8-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamwork.</span></span>

<span data-ttu-id="9cea8-142">tooconfigure e prova AD Azure single sign-on con lavoro in team, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="9cea8-142">tooconfigure and test Azure AD single sign-on with Teamwork, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9cea8-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9cea8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9cea8-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9cea8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9cea8-145">**[Creazione di un utente test squadra](#creating-a-teamwork-test-user)**  -toohave un equivalente di Britta Simon in gruppo che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9cea8-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - toohave a counterpart of Britta Simon in Teamwork that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9cea8-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9cea8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9cea8-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="9cea8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9cea8-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cea8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9cea8-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione il lavoro del team.</span><span class="sxs-lookup"><span data-stu-id="9cea8-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="9cea8-150">**Azure AD tooconfigure single sign-on con lavoro in team, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9cea8-150">**tooconfigure Azure AD single sign-on with Teamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cea8-151">Nel portale di gestione di Azure hello in hello **squadra** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-151">In hello Azure Management portal, on hello **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="9cea8-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9cea8-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="9cea8-155">In hello **squadra dominio e gli URL** della sezione hello **URL di accesso** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="9cea8-155">On hello **Teamwork Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="9cea8-157">Si noti che questo non è il valore reale hello.</span><span class="sxs-lookup"><span data-stu-id="9cea8-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="9cea8-158">È necessario tooupdate URL di accesso questo valore con hello effettivo.</span><span class="sxs-lookup"><span data-stu-id="9cea8-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="9cea8-159">Contatto [team di supporto di lavoro in Team](mailto:support@teamwork.com) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="9cea8-159">Contact [Teamwork support team](mailto:support@teamwork.com) tooget this value.</span></span> 

4. <span data-ttu-id="9cea8-160">In hello **certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="9cea8-162">In hello **creare nuovo certificato** finestra di dialogo, fare clic sull'icona calendario hello e selezionare un **data di scadenza**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="9cea8-163">Fare quindi clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-163">Then click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="9cea8-165">In hello **certificato di firma SAML** selezionare **attivare di nuovo certificato** e fare clic su **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9cea8-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="9cea8-167">Nel menu a comparsa hello **il certificato di Rollover** finestra, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9cea8-169">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="9cea8-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="9cea8-171">tooget SSO è configurato per l'applicazione, contattare [team di supporto di lavoro in Team](mailto:support@teamwork.com) e fornire loro hello scaricato **metadati**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-171">tooget SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with hello downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9cea8-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cea8-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="9cea8-173">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9cea8-173">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="9cea8-175">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9cea8-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cea8-176">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="9cea8-176">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9cea8-178">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="9cea8-178">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9cea8-180">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9cea8-180">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9cea8-182">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9cea8-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9cea8-184">a.</span><span class="sxs-lookup"><span data-stu-id="9cea8-184">a.</span></span> <span data-ttu-id="9cea8-185">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9cea8-186">b.</span><span class="sxs-lookup"><span data-stu-id="9cea8-186">b.</span></span> <span data-ttu-id="9cea8-187">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9cea8-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9cea8-188">c.</span><span class="sxs-lookup"><span data-stu-id="9cea8-188">c.</span></span> <span data-ttu-id="9cea8-189">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9cea8-190">d.</span><span class="sxs-lookup"><span data-stu-id="9cea8-190">d.</span></span> <span data-ttu-id="9cea8-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="9cea8-192">Creazione di un utente test Teamwork</span><span class="sxs-lookup"><span data-stu-id="9cea8-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="9cea8-193">In questa sezione viene creato un utente chiamato Britta Simon in Teamwork.</span><span class="sxs-lookup"><span data-stu-id="9cea8-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="9cea8-194">Rivolgersi [team di supporto di lavoro in Team](mailto:support@teamwork.com) utenti hello tooadd nella piattaforma di lavoro in team hello.</span><span class="sxs-lookup"><span data-stu-id="9cea8-194">Please work with [Teamwork support team](mailto:support@teamwork.com) tooadd hello users in hello Teamwork platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9cea8-195">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cea8-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9cea8-196">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooTeamwork proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="9cea8-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamwork.</span></span>

![Assegna utente][200] 

<span data-ttu-id="9cea8-198">**tooassign Britta Simon tooTeamwork, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9cea8-198">**tooassign Britta Simon tooTeamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cea8-199">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-199">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="9cea8-201">Nell'elenco di applicazioni hello, selezionare **squadra**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-201">In hello applications list, select **Teamwork**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="9cea8-203">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="9cea8-205">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-205">Click **Add** button.</span></span> <span data-ttu-id="9cea8-206">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="9cea8-208">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="9cea8-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9cea8-209">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9cea8-210">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9cea8-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="9cea8-211">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9cea8-211">Testing single sign-on</span></span>

<span data-ttu-id="9cea8-212">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="9cea8-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9cea8-213">Quando si fa clic su riquadro di lavoro in team hello in hello Pannello di accesso, è necessario ottenere applicazione squadra tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="9cea8-213">When you click hello Teamwork tile in hello Access Panel, you should get automatically signed-on tooyour Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9cea8-214">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9cea8-214">Additional resources</span></span>

* [<span data-ttu-id="9cea8-215">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9cea8-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9cea8-216">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9cea8-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png