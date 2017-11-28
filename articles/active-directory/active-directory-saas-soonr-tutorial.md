---
title: 'Esercitazione: Integrazione di Azure Active Directory con Soonr Workplace | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Soonr all'area di lavoro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="2d316-103">Esercitazione: Integrazione di Azure Active Directory con Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="2d316-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="2d316-104">obiettivo di Hello di questa esercitazione è tooshow è come toointegrate Soonr all'area di lavoro con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2d316-104">hello objective of this tutorial is tooshow you how toointegrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="2d316-105">Integrazione Soonr all'area di lavoro con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="2d316-105">Integrating Soonr Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2d316-106">È possibile controllare in Azure AD che ha accesso tooSoonr all'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="2d316-106">You can control in Azure AD who has access tooSoonr Workplace</span></span>
- <span data-ttu-id="2d316-107">È possibile abilitare l'utenti tooautomatically get connesso tooSoonr all'area di lavoro (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d316-107">You can enable your users tooautomatically get signed-on tooSoonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2d316-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="2d316-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="2d316-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2d316-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d316-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2d316-110">Prerequisites</span></span>

<span data-ttu-id="2d316-111">tooconfigure integrazione di Azure AD con Soonr all'area di lavoro, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="2d316-111">tooconfigure Azure AD integration with Soonr Workplace, you need hello following items:</span></span>

- <span data-ttu-id="2d316-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d316-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2d316-113">Sottoscrizione di Soonr Workplace abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2d316-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="2d316-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="2d316-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="2d316-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="2d316-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2d316-116">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2d316-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2d316-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d316-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="2d316-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2d316-118">Scenario description</span></span>
<span data-ttu-id="2d316-119">obiettivo di Hello di questa esercitazione è tooenable si tootest AD Azure single sign-on in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2d316-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="2d316-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="2d316-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d316-121">Aggiunta all'area di lavoro Soonr dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="2d316-121">Adding Soonr Workplace from hello gallery</span></span>
2. <span data-ttu-id="2d316-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d316-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-hello-gallery"></a><span data-ttu-id="2d316-123">Aggiunta all'area di lavoro Soonr dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="2d316-123">Adding Soonr Workplace from hello gallery</span></span>
<span data-ttu-id="2d316-124">integrazione hello tooconfigure di Soonr all'area di lavoro in Azure AD, è necessario tooadd Soonr all'area di lavoro dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2d316-124">tooconfigure hello integration of Soonr Workplace into Azure AD, you need tooadd Soonr Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2d316-125">**tooadd Soonr all'area di lavoro Raccolta hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2d316-125">**tooadd Soonr Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d316-126">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2d316-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2d316-128">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="2d316-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="2d316-129">visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="2d316-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Applicazioni][2]

4. <span data-ttu-id="2d316-131">Fare clic su **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="2d316-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Applicazioni][3]

5. <span data-ttu-id="2d316-133">In hello **cosa si desidera toodo** finestra di dialogo, fare clic su **aggiungere un'applicazione dalla raccolta di hello**.</span><span class="sxs-lookup"><span data-stu-id="2d316-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
 
    ![Applicazioni][4]

6. <span data-ttu-id="2d316-135">Nella casella di ricerca hello, digitare **Soonr all'area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="2d316-135">In hello search box, type **Soonr Workplace**.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="2d316-137">Nel riquadro risultati hello selezionare **Soonr all'area di lavoro**, quindi fare clic su **completa** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2d316-137">In hello results pane, select **Soonr Workplace**, and then click **Complete** tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2d316-139">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d316-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2d316-140">obiettivo di Hello di questa sezione è tooshow come tooconfigure e prova AD Azure single sign-on con Soonr all'area di lavoro basato su un utente di test denominato "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2d316-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2d316-141">Per toowork di accesso singolo, Azure AD deve tooknow è quale utente controparte hello utente tooan Soonr all'area di lavoro in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d316-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Soonr Workplace tooan user in Azure AD is.</span></span> <span data-ttu-id="2d316-142">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello nell'area di lavoro Soonr deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="2d316-142">In other words, a link relationship between an Azure AD user and hello related user in Soonr Workplace needs toobe established.</span></span>  

<span data-ttu-id="2d316-143">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Soonr all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2d316-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="2d316-144">tooconfigure e prova AD Azure single sign-on con Soonr all'area di lavoro, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="2d316-144">tooconfigure and test Azure AD single sign-on with Soonr Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2d316-145">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2d316-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2d316-146">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d316-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2d316-147">**[Creazione di un utente di test all'area di lavoro Soonr](#creating-a-soonr-workplace-test-user)**  -toohave un equivalente di Britta Simon Soonr area di lavoro che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2d316-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - toohave a counterpart of Britta Simon in Soonr Workplace that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="2d316-148">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2d316-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2d316-149">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="2d316-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2d316-150">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d316-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2d316-151">In questa sezione, si abilita Azure AD single sign-on nel portale classico hello e configurare l'accesso single sign-on nell'applicazione Soonr all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2d316-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="2d316-152">**Azure AD tooconfigure single sign-on con Soonr all'area di lavoro, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2d316-152">**tooconfigure Azure AD single sign-on with Soonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d316-153">Nel portale di Azure classico, in hello hello **Soonr all'area di lavoro** pagina di integrazione dell'applicazione, fare clic su **configurare single sign-on** tooopen hello **configurare Single Sign-On**  finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2d316-153">In hello Azure classic portal, on hello **Soonr Workplace** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>

    ![Configura accesso Single Sign-On][6] 

2. <span data-ttu-id="2d316-155">In hello **come si sarebbe ad esempio utenti toosign su tooSoonr all'area di lavoro** selezionare **Azure Single Sign-On AD**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2d316-155">On hello **How would you like users toosign on tooSoonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="2d316-157">In hello **Configura impostazioni App** finestra di dialogo eseguire hello alla procedura seguente:.</span><span class="sxs-lookup"><span data-stu-id="2d316-157">On hello **Configure App Settings** dialog page, perform hello following steps:.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="2d316-159">a.</span><span class="sxs-lookup"><span data-stu-id="2d316-159">a.</span></span> <span data-ttu-id="2d316-160">In hello **URL di accesso** casella di testo, digitare un URL con modello di hello: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="2d316-160">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="2d316-161">b.</span><span class="sxs-lookup"><span data-stu-id="2d316-161">b.</span></span> <span data-ttu-id="2d316-162">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2d316-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2d316-163">Si noti che questo non è il valore reale hello.</span><span class="sxs-lookup"><span data-stu-id="2d316-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="2d316-164">È necessario tooupdate URL di accesso questo valore con hello effettivo.</span><span class="sxs-lookup"><span data-stu-id="2d316-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="2d316-165">Contattare tooget team di supporto Soonr all'area di lavoro di questo valore.</span><span class="sxs-lookup"><span data-stu-id="2d316-165">Contact Soonr Workplace support team tooget this value.</span></span>

4. <span data-ttu-id="2d316-166">In hello **Configura accesso single sign-on in luogo di lavoro Soonr** pagina, fare clic su **Scarica metadati** e quindi salvare il file hello nel computer in uso:</span><span class="sxs-lookup"><span data-stu-id="2d316-166">On hello **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save hello file on your computer:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="2d316-168">tooget SSO configurato per l'applicazione, contattare il team di supporto Soonr all'area di lavoro e fornire loro seguente hello:</span><span class="sxs-lookup"><span data-stu-id="2d316-168">tooget SSO configured for your application, contact your Soonr Workplace support team and provide them with hello following:</span></span> 

    <span data-ttu-id="2d316-169">• hello scaricato **metadati** file</span><span class="sxs-lookup"><span data-stu-id="2d316-169">•  hello downloaded **Metadata** file</span></span>

    <span data-ttu-id="2d316-170">• hello **URL autorità di certificazione**</span><span class="sxs-lookup"><span data-stu-id="2d316-170">•  hello **Issuer URL**</span></span>

    <span data-ttu-id="2d316-171">• hello **URL SSO SAML**</span><span class="sxs-lookup"><span data-stu-id="2d316-171">•  hello **SAML SSO URL**</span></span>

    <span data-ttu-id="2d316-172">• hello **URL del servizio Single Sign-Out**</span><span class="sxs-lookup"><span data-stu-id="2d316-172">•  hello **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="2d316-173">Questa applicazione è stata sostituita da <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask all'area di lavoro</a> e farvi riferimento <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">questo</a> esercitazione per la configurazione di un'applicazione hello con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d316-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring hello application with Azure AD.</span></span>
   
6. <span data-ttu-id="2d316-174">Nel portale di Azure classico hello, selezionare hello conferma della configurazione di single sign-on e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2d316-174">In hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Single Sign-On di Microsoft Azure AD][10]

7. <span data-ttu-id="2d316-176">In hello **Single sign-on conferma** pagina, fare clic su **completa**.</span><span class="sxs-lookup"><span data-stu-id="2d316-176">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Single Sign-On di Microsoft Azure AD][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2d316-178">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d316-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="2d316-179">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure classico chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2d316-179">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Creare un utente di Azure AD][20]

<span data-ttu-id="2d316-181">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2d316-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d316-182">In hello **portale di Azure classico**via hello riquadro di spostamento a sinistra, fare clic su **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2d316-182">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="2d316-184">Da hello **Directory** elenco, directory hello selezionare per il quale si desidera l'integrazione di directory tooenable.</span><span class="sxs-lookup"><span data-stu-id="2d316-184">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="2d316-185">Fare clic su elenco hello toodisplay di utenti, nel menu hello nella parte superiore di hello, **utenti**.</span><span class="sxs-lookup"><span data-stu-id="2d316-185">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2d316-187">hello tooopen **Aggiungi utente** finestra di dialogo, nella barra degli strumenti hello nella parte inferiore di hello, fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="2d316-187">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="2d316-189">In hello **informazioni sull'utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2d316-189">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="2d316-191">a.</span><span class="sxs-lookup"><span data-stu-id="2d316-191">a.</span></span> <span data-ttu-id="2d316-192">In Tipo di utente selezionare Nuovo utente nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="2d316-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="2d316-193">b.</span><span class="sxs-lookup"><span data-stu-id="2d316-193">b.</span></span> <span data-ttu-id="2d316-194">In nome utente hello **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2d316-194">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2d316-195">c.</span><span class="sxs-lookup"><span data-stu-id="2d316-195">c.</span></span> <span data-ttu-id="2d316-196">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2d316-196">Click **Next**.</span></span>

6.  <span data-ttu-id="2d316-197">In hello **profilo utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2d316-197">On hello **User Profile** dialog page, perform hello following steps:</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="2d316-199">a.</span><span class="sxs-lookup"><span data-stu-id="2d316-199">a.</span></span> <span data-ttu-id="2d316-200">In hello **nome** casella tipo **Laura**.</span><span class="sxs-lookup"><span data-stu-id="2d316-200">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="2d316-201">b.</span><span class="sxs-lookup"><span data-stu-id="2d316-201">b.</span></span> <span data-ttu-id="2d316-202">In hello **cognome** casella di testo, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2d316-202">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="2d316-203">c.</span><span class="sxs-lookup"><span data-stu-id="2d316-203">c.</span></span> <span data-ttu-id="2d316-204">In hello **nome visualizzato** casella tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2d316-204">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="2d316-205">d.</span><span class="sxs-lookup"><span data-stu-id="2d316-205">d.</span></span> <span data-ttu-id="2d316-206">In hello **ruolo** elenco, selezionare **utente**.</span><span class="sxs-lookup"><span data-stu-id="2d316-206">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="2d316-207">e.</span><span class="sxs-lookup"><span data-stu-id="2d316-207">e.</span></span> <span data-ttu-id="2d316-208">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2d316-208">Click **Next**.</span></span>

7. <span data-ttu-id="2d316-209">In hello **Ottieni password temporanea** nella pagina, fare clic su **creare**.</span><span class="sxs-lookup"><span data-stu-id="2d316-209">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="2d316-211">In hello **Ottieni password temporanea** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2d316-211">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="2d316-213">a.</span><span class="sxs-lookup"><span data-stu-id="2d316-213">a.</span></span> <span data-ttu-id="2d316-214">Annotare il valore di hello di hello **nuova Password**.</span><span class="sxs-lookup"><span data-stu-id="2d316-214">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="2d316-215">b.</span><span class="sxs-lookup"><span data-stu-id="2d316-215">b.</span></span> <span data-ttu-id="2d316-216">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="2d316-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="2d316-217">Creazione di un utente test di Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="2d316-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="2d316-218">obiettivo di Hello di questa sezione è un utente denominato Britta Simon nell'area di lavoro Soonr toocreate.</span><span class="sxs-lookup"><span data-stu-id="2d316-218">hello objective of this section is toocreate a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="2d316-219">Rivolgersi all'area di lavoro Soonr supporto team toocreate un utente nella piattaforma hello.</span><span class="sxs-lookup"><span data-stu-id="2d316-219">Please work with Soonr Workplace support team toocreate a user in hello platform.</span></span> <span data-ttu-id="2d316-220">È possibile generare il ticket di supporto hello con Soonr da <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">qui</a>.</span><span class="sxs-lookup"><span data-stu-id="2d316-220">You can raise hello support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2d316-221">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d316-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2d316-222">obiettivo di Hello di questa sezione è tooenabling toouse Britta Simon single sign-on Azure concedendo proprio tooSoonr accesso all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2d316-222">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSoonr Workplace.</span></span>

![Assegna utente][200] 

<span data-ttu-id="2d316-224">**tooassign Britta Simon tooSoonr all'area di lavoro, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2d316-224">**tooassign Britta Simon tooSoonr Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d316-225">In hello Azure portale classico, visualizzazione di applicazioni hello tooopen, nella visualizzazione directory hello, fare clic su **applicazioni** nel menu superiore hello.</span><span class="sxs-lookup"><span data-stu-id="2d316-225">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2d316-227">Nell'elenco di applicazioni hello, selezionare **Soonr all'area di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="2d316-227">In hello applications list, select **Soonr Workplace**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="2d316-229">Scegliere dal menu hello in primo piano hello **utenti**.</span><span class="sxs-lookup"><span data-stu-id="2d316-229">In hello menu on hello top, click **Users**.</span></span>

    ![Assegna utente][203] 

1. <span data-ttu-id="2d316-231">Nell'elenco di utenti hello, selezionare **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2d316-231">In hello Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="2d316-232">Nella barra degli strumenti di hello nella parte inferiore di hello, fare clic su **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="2d316-232">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Assegna utente][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="2d316-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2d316-234">Testing single sign-on</span></span>

<span data-ttu-id="2d316-235">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2d316-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="2d316-236">Quando si fa clic hello all'area di lavoro Soonr riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione Soonr all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="2d316-236">When you click hello Soonr Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2d316-237">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2d316-237">Additional resources</span></span>

* [<span data-ttu-id="2d316-238">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d316-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2d316-239">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d316-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
