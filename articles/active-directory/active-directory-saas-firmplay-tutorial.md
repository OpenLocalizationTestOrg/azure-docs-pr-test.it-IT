---
title: 'Esercitazione: Integrazione di Azure Active Directory con FirmPlay - Employee Advocacy for Recruiting | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e FirmPlay - sostegno dipendente per assunzioni.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="9f527-103">Esercitazione: Integrazione di Azure Active Directory con FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="9f527-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="9f527-104">In questa esercitazione, è illustrato come toointegrate FirmPlay - sostegno dipendente per assunzioni con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9f527-104">In this tutorial, you learn how toointegrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f527-105">L'integrazione FirmPlay - sostegno dipendente per assunzioni con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="9f527-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9f527-106">È possibile controllare in Azure AD che ha accesso tooFirmPlay - sostegno dipendente per assunzioni</span><span class="sxs-lookup"><span data-stu-id="9f527-106">You can control in Azure AD who has access tooFirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="9f527-107">È possibile abilitare l'utenti tooautomatically get connesso tooFirmPlay - sostegno dipendente per assunzioni (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f527-107">You can enable your users tooautomatically get signed-on tooFirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9f527-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="9f527-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="9f527-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9f527-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f527-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9f527-110">Prerequisites</span></span>

<span data-ttu-id="9f527-111">tooconfigure integrazione di Azure AD con FirmPlay - sostegno dipendente per assunzioni, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="9f527-111">tooconfigure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need hello following items:</span></span>

- <span data-ttu-id="9f527-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f527-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9f527-113">Sottoscrizione di FirmPlay - Employee Advocacy for Recruiting abilitata per l'accesso Single-Sign On</span><span class="sxs-lookup"><span data-stu-id="9f527-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="9f527-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="9f527-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="9f527-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="9f527-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f527-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="9f527-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9f527-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f527-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="9f527-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="9f527-118">Scenario description</span></span>
<span data-ttu-id="9f527-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="9f527-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f527-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="9f527-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f527-121">Aggiunta di sostegno dipendente per assunzioni dalla raccolta hello FirmPlay-</span><span class="sxs-lookup"><span data-stu-id="9f527-121">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
2. <span data-ttu-id="9f527-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f527-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a><span data-ttu-id="9f527-123">Aggiunta di sostegno dipendente per assunzioni dalla raccolta hello FirmPlay-</span><span class="sxs-lookup"><span data-stu-id="9f527-123">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
<span data-ttu-id="9f527-124">integrazione di hello tooconfigure di FirmPlay - sostegno dipendente per assunzioni in Azure AD, è necessario tooadd FirmPlay - sostegno dipendente per assunzioni dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="9f527-124">tooconfigure hello integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9f527-125">**tooadd FirmPlay - sostegno dipendente per assunzioni dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9f527-125">**tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f527-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="9f527-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9f527-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="9f527-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9f527-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9f527-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="9f527-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="9f527-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="9f527-133">Nella casella di ricerca hello, digitare **FirmPlay - sostegno dipendente per assunzioni**.</span><span class="sxs-lookup"><span data-stu-id="9f527-133">In hello search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="9f527-135">Nel riquadro dei risultati hello, selezionare **FirmPlay - sostegno dipendente per assunzioni**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9f527-135">In hello results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9f527-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f527-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9f527-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con FirmPlay - Employee Advocacy for Recruiting con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9f527-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9f527-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in FirmPlay - sostegno dipendente per assunzioni è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f527-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FirmPlay - Employee Advocacy for Recruiting is tooa user in Azure AD.</span></span> <span data-ttu-id="9f527-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in FirmPlay - sostegno dipendente per assunzioni deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="9f527-140">In other words, a link relationship between an Azure AD user and hello related user in FirmPlay - Employee Advocacy for Recruiting needs toobe established.</span></span>

<span data-ttu-id="9f527-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in FirmPlay - sostegno dipendente per assunzioni.</span><span class="sxs-lookup"><span data-stu-id="9f527-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="9f527-142">tooconfigure e prova AD Azure single sign-on con FirmPlay - sostegno dipendente per assunzioni, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="9f527-142">tooconfigure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9f527-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9f527-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9f527-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9f527-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f527-145">**[Creazione di un FirmPlay - sostegno dipendente per l'utente test assunzioni](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  -toohave un equivalente di Britta Simon in FirmPlay: sostegno dipendente per la selezione che è collegato rappresentazione toohello Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9f527-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - toohave a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9f527-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9f527-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f527-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="9f527-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9f527-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f527-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9f527-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nel FirmPlay - sostegno dipendente per applicazione assunzioni.</span><span class="sxs-lookup"><span data-stu-id="9f527-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="9f527-150">**tooconfigure AD Azure single sign-on con FirmPlay - sostegno dipendente per assunzioni, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9f527-150">**tooconfigure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f527-151">Nel portale di gestione di Azure hello in hello **FirmPlay - sostegno dipendente per assunzioni** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9f527-151">In hello Azure Management portal, on hello **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="9f527-153">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9f527-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="9f527-155">In hello **FirmPlay - sostegno dipendente per la selezione di dominio e gli URL** della sezione hello **URL di accesso** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="9f527-155">On hello **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="9f527-157">Si noti che questo non è il valore reale hello.</span><span class="sxs-lookup"><span data-stu-id="9f527-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="9f527-158">È necessario tooupdate URL di accesso questo valore con hello effettivo.</span><span class="sxs-lookup"><span data-stu-id="9f527-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="9f527-159">Contatto [FirmPlay - sostegno dipendente per il team di supporto assunzioni](mailto:engineering@firmplay.com) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="9f527-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooget this value.</span></span> 

4. <span data-ttu-id="9f527-160">In hello **certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="9f527-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="9f527-162">In hello **creare nuovo certificato** finestra di dialogo, fare clic sull'icona calendario hello e selezionare un **data di scadenza**.</span><span class="sxs-lookup"><span data-stu-id="9f527-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="9f527-163">Fare quindi clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9f527-163">Then click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="9f527-165">In hello **certificato di firma SAML** selezionare **attivare di nuovo certificato** e fare clic su **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9f527-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="9f527-167">Nel menu a comparsa hello **il certificato di Rollover** finestra, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f527-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9f527-169">In hello **certificato di firma SAML** fare clic su **certificato (base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="9f527-169">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="9f527-171">In hello **FirmPlay - sostegno dipendente per la selezione configurazione** fare clic su **configurare FirmPlay - sostegno dipendente per assunzioni** tooopen **Configura sign-on**finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9f527-171">On hello **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** tooopen **Configure sign-on** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="9f527-174">tooget SSO è configurato per l'applicazione, contattare [FirmPlay - sostegno dipendente per il team di supporto assunzioni](mailto:engineering@firmplay.com) e fornire loro seguente hello:</span><span class="sxs-lookup"><span data-stu-id="9f527-174">tooget SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with hello following:</span></span> 

    <span data-ttu-id="9f527-175">• hello scaricato **file di certificato**</span><span class="sxs-lookup"><span data-stu-id="9f527-175">•  hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="9f527-176">• hello **SAML Single Sign-On Service URL**</span><span class="sxs-lookup"><span data-stu-id="9f527-176">•  hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="9f527-177">• hello **ID entità SAML**</span><span class="sxs-lookup"><span data-stu-id="9f527-177">•  hello **SAML Entity ID**</span></span>

    <span data-ttu-id="9f527-178">• hello **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="9f527-178">•  hello **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9f527-179">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f527-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="9f527-180">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9f527-180">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="9f527-182">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9f527-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f527-183">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="9f527-183">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9f527-185">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="9f527-185">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9f527-187">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9f527-187">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9f527-189">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9f527-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9f527-191">a.</span><span class="sxs-lookup"><span data-stu-id="9f527-191">a.</span></span> <span data-ttu-id="9f527-192">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9f527-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9f527-193">b.</span><span class="sxs-lookup"><span data-stu-id="9f527-193">b.</span></span> <span data-ttu-id="9f527-194">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9f527-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9f527-195">c.</span><span class="sxs-lookup"><span data-stu-id="9f527-195">c.</span></span> <span data-ttu-id="9f527-196">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="9f527-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9f527-197">d.</span><span class="sxs-lookup"><span data-stu-id="9f527-197">d.</span></span> <span data-ttu-id="9f527-198">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9f527-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="9f527-199">Creazione di un utente di test di FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="9f527-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="9f527-200">In questa sezione si crea un utente di nome Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="9f527-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="9f527-201">Rivolgersi [FirmPlay - sostegno dipendente per il team di supporto assunzioni](mailto:engineering@firmplay.com) utenti hello tooadd hello FirmPlay - sostegno dipendente per piattaforma assunzioni.</span><span class="sxs-lookup"><span data-stu-id="9f527-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooadd hello users in hello FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9f527-202">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f527-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9f527-203">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooFirmPlay proprio accesso - sostegno dipendente per assunzioni.</span><span class="sxs-lookup"><span data-stu-id="9f527-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFirmPlay - Employee Advocacy for Recruiting.</span></span>

![Assegna utente][200] 

<span data-ttu-id="9f527-205">**tooassign Britta Simon tooFirmPlay - sostegno dipendente per assunzioni, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9f527-205">**tooassign Britta Simon tooFirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f527-206">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9f527-206">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="9f527-208">Nell'elenco di applicazioni hello, selezionare **FirmPlay - sostegno dipendente per assunzioni**.</span><span class="sxs-lookup"><span data-stu-id="9f527-208">In hello applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="9f527-210">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9f527-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="9f527-212">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9f527-212">Click **Add** button.</span></span> <span data-ttu-id="9f527-213">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9f527-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="9f527-215">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="9f527-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9f527-216">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9f527-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f527-217">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9f527-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="9f527-218">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9f527-218">Testing single sign-on</span></span>

<span data-ttu-id="9f527-219">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="9f527-219">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9f527-220">Quando si fa clic hello FirmPlay - sostegno dipendente riquadro assunzioni in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour FirmPlay - sostegno dipendente per applicazione assunzioni.</span><span class="sxs-lookup"><span data-stu-id="9f527-220">When you click hello FirmPlay - Employee Advocacy for Recruiting tile in hello Access Panel, you should get automatically signed-on tooyour FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9f527-221">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9f527-221">Additional resources</span></span>

* [<span data-ttu-id="9f527-222">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f527-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f527-223">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f527-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png