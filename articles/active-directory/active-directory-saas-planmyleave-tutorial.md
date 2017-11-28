---
title: 'Esercitazione: Integrazione di Azure Active Directory con PlanMyLeave | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e PlanMyLeave.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="2064e-103">Esercitazione: Integrazione di Azure Active Directory con PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="2064e-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="2064e-104">In questa esercitazione, è illustrato come toointegrate PlanMyLeave con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2064e-104">In this tutorial, you learn how toointegrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2064e-105">Integrazione PlanMyLeave con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="2064e-105">Integrating PlanMyLeave with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2064e-106">È possibile controllare in Azure AD che ha accesso tooPlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="2064e-106">You can control in Azure AD who has access tooPlanMyLeave</span></span>
- <span data-ttu-id="2064e-107">È possibile abilitare l'utenti tooautomatically get connesso tooPlanMyLeave (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="2064e-107">You can enable your users tooautomatically get signed-on tooPlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2064e-108">È possibile gestire gli account in un'unica posizione centrale - portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="2064e-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="2064e-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2064e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2064e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2064e-110">Prerequisites</span></span>

<span data-ttu-id="2064e-111">integrazione di Azure AD con PlanMyLeave tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="2064e-111">tooconfigure Azure AD integration with PlanMyLeave, you need hello following items:</span></span>

- <span data-ttu-id="2064e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2064e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2064e-113">Sottoscrizione di PlanMyLeave abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2064e-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="2064e-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="2064e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="2064e-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="2064e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2064e-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2064e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2064e-117">Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2064e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="2064e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2064e-118">Scenario description</span></span>
<span data-ttu-id="2064e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2064e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2064e-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="2064e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2064e-121">Aggiunta di PlanMyLeave dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="2064e-121">Adding PlanMyLeave from hello gallery</span></span>
2. <span data-ttu-id="2064e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2064e-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-hello-gallery"></a><span data-ttu-id="2064e-123">Aggiunta di PlanMyLeave dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="2064e-123">Adding PlanMyLeave from hello gallery</span></span>
<span data-ttu-id="2064e-124">integrazione hello tooconfigure di PlanMyLeave in Azure AD, è necessario tooadd PlanMyLeave dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2064e-124">tooconfigure hello integration of PlanMyLeave into Azure AD, you need tooadd PlanMyLeave from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2064e-125">**tooadd PlanMyLeave dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2064e-125">**tooadd PlanMyLeave from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2064e-126">In hello  **[il portale di gestione di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="2064e-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2064e-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="2064e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2064e-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2064e-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="2064e-131">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="2064e-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="2064e-133">Nella casella di ricerca hello, digitare **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="2064e-133">In hello search box, type **PlanMyLeave**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="2064e-135">Nel riquadro dei risultati hello, selezionare **PlanMyLeave**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2064e-135">In hello results panel, select **PlanMyLeave**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2064e-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2064e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2064e-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con PlanMyLeave in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2064e-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2064e-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in PlanMyLeave è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2064e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PlanMyLeave is tooa user in Azure AD.</span></span> <span data-ttu-id="2064e-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in PlanMyLeave deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="2064e-140">In other words, a link relationship between an Azure AD user and hello related user in PlanMyLeave needs toobe established.</span></span>

<span data-ttu-id="2064e-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="2064e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="2064e-142">tooconfigure e prova AD Azure single sign-on con PlanMyLeave, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="2064e-142">tooconfigure and test Azure AD single sign-on with PlanMyLeave, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2064e-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2064e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2064e-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2064e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2064e-145">**[Creazione di un utente test PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave un equivalente di Britta Simon in PlanMyLeave toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="2064e-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - toohave a counterpart of Britta Simon in PlanMyLeave that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="2064e-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2064e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2064e-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="2064e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2064e-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2064e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2064e-149">In questa sezione, si abilita Azure AD single sign-on nel portale di gestione di Azure hello e configurare l'accesso single sign-on nell'applicazione PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="2064e-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="2064e-150">**Azure AD tooconfigure single sign-on con PlanMyLeave, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2064e-150">**tooconfigure Azure AD single sign-on with PlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="2064e-151">Nel portale di gestione di Azure hello in hello **PlanMyLeave** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2064e-151">In hello Azure Management portal, on hello **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="2064e-153">In hello **Single sign-on** nella pagina, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2064e-153">On hello **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="2064e-155">In hello **PlanMyLeave dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2064e-155">On hello **PlanMyLeave Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="2064e-157">a.</span><span class="sxs-lookup"><span data-stu-id="2064e-157">a.</span></span> <span data-ttu-id="2064e-158">In hello **URL di accesso** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="2064e-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="2064e-159">b.</span><span class="sxs-lookup"><span data-stu-id="2064e-159">b.</span></span> <span data-ttu-id="2064e-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="2064e-160">In hello **Identifer** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2064e-161">Si noti che queste non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="2064e-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="2064e-162">È necessario tooupdate questi valori con hello effettivo accesso URL e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="2064e-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="2064e-163">Contatto [team di supporto PlanMyLeave](mailto:support@planmyleave.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="2064e-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) tooget these values.</span></span>

4. <span data-ttu-id="2064e-164">In hello **certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="2064e-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="2064e-166">In hello **creare nuovo certificato** finestra di dialogo, fare clic sull'icona calendario hello e selezionare un **data di scadenza**.</span><span class="sxs-lookup"><span data-stu-id="2064e-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="2064e-167">Fare quindi clic sul pulsante **Salva**.</span><span class="sxs-lookup"><span data-stu-id="2064e-167">Then click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="2064e-169">In hello **certificato di firma SAML** selezionare **attivare di nuovo certificato** e fare clic su **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="2064e-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="2064e-171">Nel menu a comparsa hello **il certificato di Rollover** finestra, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2064e-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2064e-173">In hello **certificato di firma SAML** fare clic su **certificato (base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="2064e-173">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="2064e-175">In hello **PlanMyLeave configurazione** fare clic su **configurare PlanMyLeave** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="2064e-175">On hello **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** tooopen **Configure sign-on** window.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="2064e-178">In un'altra finestra del browser Web accedere al tenant di PlanMyLeave come amministratore.</span><span class="sxs-lookup"><span data-stu-id="2064e-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="2064e-179">Andare troppo**installazione System**.</span><span class="sxs-lookup"><span data-stu-id="2064e-179">Go too**System Setup**.</span></span> <span data-ttu-id="2064e-180">Quindi, nella hello **gestione della sicurezza** fare clic su sezione **impostazioni società SAML** .</span><span class="sxs-lookup"><span data-stu-id="2064e-180">Then on hello **Security Management** section click **Company SAML settings** .</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="2064e-182">In hello **impostazioni SAML** sezione fare clic sull'icona di editor.</span><span class="sxs-lookup"><span data-stu-id="2064e-182">On hello **SAML Settings** section, click editor icon.</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="2064e-184">In hello **impostazioni SAML Update** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2064e-184">On hello **Update SAML Settings** section, perform hello following steps:</span></span>

    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="2064e-186">a.</span><span class="sxs-lookup"><span data-stu-id="2064e-186">a.</span></span>  <span data-ttu-id="2064e-187">In hello **URL di accesso** casella di testo, inserire il valore di hello di **SAML Single Sign-On Service URL** dalla finestra di configurazione dell'applicazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2064e-187">In hello **Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="2064e-188">b.</span><span class="sxs-lookup"><span data-stu-id="2064e-188">b.</span></span>  <span data-ttu-id="2064e-189">Aprire il file del certificato scaricato nel blocco note, copiare solo il contenuto di hello tra hello---inizio certificato--- e ---fine certificato---ne negli Appunti e quindi incollarlo toohello **certificato** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="2064e-189">Open your downloaded certificate file in notepad, copy only hello content between hello ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>

    <span data-ttu-id="2064e-190">c.</span><span class="sxs-lookup"><span data-stu-id="2064e-190">c.</span></span> <span data-ttu-id="2064e-191">Impostare"**è Enable**"troppo"**Sì**".</span><span class="sxs-lookup"><span data-stu-id="2064e-191">Set "**Is Enable**" too"**Yes**".</span></span>

    <span data-ttu-id="2064e-192">d.</span><span class="sxs-lookup"><span data-stu-id="2064e-192">d.</span></span> <span data-ttu-id="2064e-193">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="2064e-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2064e-194">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2064e-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="2064e-195">obiettivo di Hello di questa sezione è un utente di test nel portale di gestione di Azure hello chiamato Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="2064e-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="2064e-197">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2064e-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2064e-198">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="2064e-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2064e-200">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="2064e-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2064e-202">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2064e-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2064e-204">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2064e-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2064e-206">a.</span><span class="sxs-lookup"><span data-stu-id="2064e-206">a.</span></span> <span data-ttu-id="2064e-207">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2064e-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2064e-208">b.</span><span class="sxs-lookup"><span data-stu-id="2064e-208">b.</span></span> <span data-ttu-id="2064e-209">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2064e-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2064e-210">c.</span><span class="sxs-lookup"><span data-stu-id="2064e-210">c.</span></span> <span data-ttu-id="2064e-211">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="2064e-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2064e-212">d.</span><span class="sxs-lookup"><span data-stu-id="2064e-212">d.</span></span> <span data-ttu-id="2064e-213">Fare clic su **Create**(Crea).</span><span class="sxs-lookup"><span data-stu-id="2064e-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="2064e-214">Creazione di un utente test di PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="2064e-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="2064e-215">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in PlanMyLeave toocreate.</span><span class="sxs-lookup"><span data-stu-id="2064e-215">hello objective of this section is toocreate a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="2064e-216">PlanMyLeave supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2064e-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="2064e-217">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="2064e-217">There is no action item for you in this section.</span></span> <span data-ttu-id="2064e-218">Verrà creato un nuovo utente durante una tooaccess tentativo PlanMyLeave se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="2064e-218">A new user will be created during an attempt tooaccess PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="2064e-219">Se è necessario un utente toocreate manualmente, è necessario toocontact [team di supporto PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="2064e-219">If you need toocreate an user manually, you need toocontact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2064e-220">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2064e-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2064e-221">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooPlanMyLeave proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="2064e-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPlanMyLeave.</span></span>

![Assegna utente][200] 

<span data-ttu-id="2064e-223">**tooassign Britta Simon tooPlanMyLeave, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2064e-223">**tooassign Britta Simon tooPlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="2064e-224">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2064e-224">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2064e-226">Nell'elenco di applicazioni hello, selezionare **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="2064e-226">In hello applications list, select **PlanMyLeave**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="2064e-228">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2064e-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="2064e-230">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2064e-230">Click **Add** button.</span></span> <span data-ttu-id="2064e-231">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2064e-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="2064e-233">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="2064e-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2064e-234">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2064e-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2064e-235">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2064e-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="2064e-236">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2064e-236">Testing single sign-on</span></span>

<span data-ttu-id="2064e-237">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2064e-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2064e-238">Quando si fa clic su riquadro PlanMyLeave hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour PlanMyLeave applicazione.</span><span class="sxs-lookup"><span data-stu-id="2064e-238">When you click hello PlanMyLeave tile in hello Access Panel, you should get automatically signed-on tooyour PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2064e-239">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2064e-239">Additional resources</span></span>

* [<span data-ttu-id="2064e-240">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2064e-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2064e-241">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2064e-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png