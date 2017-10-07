---
title: 'Esercitazione: Integrazione di Azure Active Directory con Halosys | Documentazione Microsoft'
description: Informazioni su come toouse Halosys con Azure Active Directory tooenable single sign-on, il provisioning automatizzato e molto altro!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="4ce81-103">Esercitazione: Integrazione di Azure Active Directory con Halosys</span><span class="sxs-lookup"><span data-stu-id="4ce81-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="4ce81-104">In questa esercitazione, è illustrato come toointegrate Halosys con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4ce81-104">In this tutorial, you learn how toointegrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4ce81-105">Integrazione Halosys con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4ce81-105">Integrating Halosys with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4ce81-106">È possibile controllare in Azure AD che ha accesso tooHalosys</span><span class="sxs-lookup"><span data-stu-id="4ce81-106">You can control in Azure AD who has access tooHalosys</span></span>
- <span data-ttu-id="4ce81-107">È possibile abilitare l'utenti tooautomatically get connesso tooHalosys (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ce81-107">You can enable your users tooautomatically get signed-on tooHalosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4ce81-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="4ce81-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="4ce81-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4ce81-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ce81-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4ce81-110">Prerequisites</span></span>

<span data-ttu-id="4ce81-111">integrazione di Azure AD con Halosys tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4ce81-111">tooconfigure Azure AD integration with Halosys, you need hello following items:</span></span>

- <span data-ttu-id="4ce81-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ce81-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4ce81-113">Sottoscrizione di Halosys abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4ce81-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="4ce81-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4ce81-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="4ce81-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4ce81-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4ce81-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4ce81-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="4ce81-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ce81-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="4ce81-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4ce81-118">Scenario description</span></span>
<span data-ttu-id="4ce81-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4ce81-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="4ce81-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4ce81-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4ce81-121">Aggiunta di Halosys dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4ce81-121">Adding Halosys from hello gallery</span></span>
2. <span data-ttu-id="4ce81-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ce81-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-hello-gallery"></a><span data-ttu-id="4ce81-123">Aggiunta di Halosys dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4ce81-123">Adding Halosys from hello gallery</span></span>
<span data-ttu-id="4ce81-124">integrazione hello tooconfigure di Halosys in Azure AD, è necessario tooadd Halosys dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4ce81-124">tooconfigure hello integration of Halosys into Azure AD, you need tooadd Halosys from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4ce81-125">**tooadd Halosys dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4ce81-125">**tooadd Halosys from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ce81-126">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="4ce81-128">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="4ce81-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="4ce81-129">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="4ce81-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Applicazioni][2]

4. <span data-ttu-id="4ce81-131">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="4ce81-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Applicazioni][3]

5. <span data-ttu-id="4ce81-133">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Applicazioni][4]

6. <span data-ttu-id="4ce81-135">Nella casella di ricerca hello, digitare **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-135">In hello search box, type **Halosys**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="4ce81-137">Nel riquadro risultati hello selezionare **Halosys**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="4ce81-137">In hello results pane, select **Halosys**, and then click **Complete** tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4ce81-139">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ce81-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4ce81-140">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Halosys usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4ce81-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4ce81-141">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Halosys è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ce81-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halosys is tooa user in Azure AD.</span></span> <span data-ttu-id="4ce81-142">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Halosys deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="4ce81-142">In other words, a link relationship between an Azure AD user and hello related user in Halosys needs toobe established.</span></span>

<span data-ttu-id="4ce81-143">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Halosys.</span><span class="sxs-lookup"><span data-stu-id="4ce81-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Halosys.</span></span>

<span data-ttu-id="4ce81-144">tooconfigure e prova AD Azure single sign-on con Halosys, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4ce81-144">tooconfigure and test Azure AD single sign-on with Halosys, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4ce81-145">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4ce81-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4ce81-146">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4ce81-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4ce81-147">**[Creazione di un utente test Halosys](#creating-a-halosys-test-user)**  -toohave un equivalente di Britta Simon in Halosys toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="4ce81-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - toohave a counterpart of Britta Simon in Halosys that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="4ce81-148">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4ce81-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4ce81-149">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4ce81-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4ce81-150">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ce81-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4ce81-151">In questa sezione, si abilita Azure AD single sign-on nel portale classico hello e configurare l'accesso single sign-on nell'applicazione Halosys.</span><span class="sxs-lookup"><span data-stu-id="4ce81-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="4ce81-152">**Azure AD tooconfigure single sign-on con Halosys, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4ce81-152">**tooconfigure Azure AD single sign-on with Halosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ce81-153">Nel portale classico hello in hello **Halosys** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4ce81-153">In hello classic portal, on hello **Halosys** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configura accesso Single Sign-On][6] 

2. <span data-ttu-id="4ce81-155">In hello **come si sarebbe ad esempio utenti toosign su tooHalosys** selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-155">On hello **How would you like users toosign on tooHalosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="4ce81-157">In hello **Configura impostazioni App** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4ce81-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="4ce81-159">a.</span><span class="sxs-lookup"><span data-stu-id="4ce81-159">a.</span></span> <span data-ttu-id="4ce81-160">In hello **URL di accesso** casella di testo, digitare l'URL hello usato dall'applicazione Halosys tooyour toosign-on agli utenti tramite hello seguente modello: `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="4ce81-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Halosys application using hello following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="4ce81-161">hello b.In **URL dell'identificatore** casella di testo, digitare l'URL nel modello di hello hello: `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="4ce81-161">b.In hello **Identifier URL** textbox, type hello URL in hello following pattern: `https://<company-name>.Halosys.com`.</span></span> 
         
4. <span data-ttu-id="4ce81-162">In hello **configurare single sign-on a Halosys** pagina, fare clic su **Scarica metadati**e quindi salvare il file hello nel computer in uso:</span><span class="sxs-lookup"><span data-stu-id="4ce81-162">On hello **Configure single sign-on at Halosys** page, click **Download metadata**, and then save hello file on your computer:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="4ce81-164">tooget SSO configurato per l'applicazione, contattare il team di supporto Halosys e fornire loro seguente hello:</span><span class="sxs-lookup"><span data-stu-id="4ce81-164">tooget SSO configured for your application, contact Halosys support team and provide them with hello following:</span></span>

    <span data-ttu-id="4ce81-165">• hello scaricato **file di metadati**</span><span class="sxs-lookup"><span data-stu-id="4ce81-165">• hello downloaded **metadata file**</span></span>
    
    <span data-ttu-id="4ce81-166">• hello **URL SSO SAML**</span><span class="sxs-lookup"><span data-stu-id="4ce81-166">• hello **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="4ce81-167">Nel portale classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-167">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Single Sign-On di Microsoft Azure AD][10]

7. <span data-ttu-id="4ce81-169">In hello **Single sign-on conferma** pagina, fare clic su **completa**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-169">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Single Sign-On di Microsoft Azure AD][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4ce81-171">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ce81-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="4ce81-172">In questa sezione creare un utente test nel portale classico di hello chiamato Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4ce81-172">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>


![Creare un utente di Azure AD][20]

<span data-ttu-id="4ce81-174">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4ce81-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ce81-175">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-175">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="4ce81-177">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="4ce81-177">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="4ce81-178">Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-178">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4ce81-180">hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-180">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="4ce81-182">In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente: ![creazione di un utente prova AD Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="4ce81-182">On hello **Tell us about this user** dialog page, perform hello following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="4ce81-183">a.</span><span class="sxs-lookup"><span data-stu-id="4ce81-183">a.</span></span> <span data-ttu-id="4ce81-184">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="4ce81-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="4ce81-185">b.</span><span class="sxs-lookup"><span data-stu-id="4ce81-185">b.</span></span> <span data-ttu-id="4ce81-186">In nome utente hello **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4ce81-187">c.</span><span class="sxs-lookup"><span data-stu-id="4ce81-187">c.</span></span> <span data-ttu-id="4ce81-188">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-188">Click **Next**.</span></span>

6.  <span data-ttu-id="4ce81-189">In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente: ![creazione di un utente prova AD Azure](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="4ce81-189">On hello **User Profile** dialog page, perform hello following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="4ce81-190">a.</span><span class="sxs-lookup"><span data-stu-id="4ce81-190">a.</span></span> <span data-ttu-id="4ce81-191">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-191">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="4ce81-192">b.</span><span class="sxs-lookup"><span data-stu-id="4ce81-192">b.</span></span> <span data-ttu-id="4ce81-193">In hello **cognome** casella di testo, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-193">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="4ce81-194">c.</span><span class="sxs-lookup"><span data-stu-id="4ce81-194">c.</span></span> <span data-ttu-id="4ce81-195">In hello **nome visualizzato** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-195">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="4ce81-196">d.</span><span class="sxs-lookup"><span data-stu-id="4ce81-196">d.</span></span> <span data-ttu-id="4ce81-197">In hello **ruolo** elenco, selezionare **utente**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-197">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="4ce81-198">e.</span><span class="sxs-lookup"><span data-stu-id="4ce81-198">e.</span></span> <span data-ttu-id="4ce81-199">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-199">Click **Next**.</span></span>

7. <span data-ttu-id="4ce81-200">In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-200">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="4ce81-202">In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4ce81-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="4ce81-204">a.</span><span class="sxs-lookup"><span data-stu-id="4ce81-204">a.</span></span> <span data-ttu-id="4ce81-205">Annotare il valore di hello di hello **nuova Password**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-205">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="4ce81-206">b.</span><span class="sxs-lookup"><span data-stu-id="4ce81-206">b.</span></span> <span data-ttu-id="4ce81-207">Fare clic su **Completa**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="4ce81-208">Creazione di un utente test per Halosys</span><span class="sxs-lookup"><span data-stu-id="4ce81-208">Creating a Halosys test user</span></span>

<span data-ttu-id="4ce81-209">In questa sezione viene creato un utente chiamato Britta Simon in Halosys.</span><span class="sxs-lookup"><span data-stu-id="4ce81-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="4ce81-210">Rivolgersi Halosys utenti tooadd hello team di supporto nella piattaforma Halosys hello.</span><span class="sxs-lookup"><span data-stu-id="4ce81-210">Please work with Halosys support team tooadd hello users in hello Halosys platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4ce81-211">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ce81-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4ce81-212">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo tooHalosys proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="4ce81-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHalosys.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4ce81-214">**tooassign Britta Simon tooHalosys, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4ce81-214">**tooassign Britta Simon tooHalosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ce81-215">Nel portale classico hello, fare clic su visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="4ce81-215">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4ce81-217">Nell'elenco di applicazioni hello, selezionare **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-217">In hello applications list, select **Halosys**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="4ce81-219">Scegliere dal menu hello in primo piano hello **utenti**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-219">In hello menu on hello top, click **Users**.</span></span>

    ![Assegna utente][203]

4. <span data-ttu-id="4ce81-221">Nell'elenco di utenti hello, selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-221">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="4ce81-222">Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="4ce81-222">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Assegna utente][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="4ce81-224">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4ce81-224">Testing single sign-on</span></span>

<span data-ttu-id="4ce81-225">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4ce81-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4ce81-226">Quando si fa clic hello Halosys riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Halosys applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ce81-226">When you click hello Halosys tile in hello Access Panel, you should get automatically signed-on tooyour Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4ce81-227">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4ce81-227">Additional resources</span></span>

* [<span data-ttu-id="4ce81-228">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ce81-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4ce81-229">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ce81-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
