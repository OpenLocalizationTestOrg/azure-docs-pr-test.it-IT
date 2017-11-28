---
title: 'Esercitazione: Integrazione di Azure Active Directory con Learning at Work | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e l'apprendimento al lavoro.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d607174-bea1-4f40-8233-54cabe02c66a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: fa09d585d57932a95cadba9a66029765d7df3694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-at-work"></a><span data-ttu-id="8068b-103">Esercitazione: Integrazione di Azure Active Directory con Learning at Work</span><span class="sxs-lookup"><span data-stu-id="8068b-103">Tutorial: Azure Active Directory integration with Learning at Work</span></span>

<span data-ttu-id="8068b-104">In questa esercitazione, è illustrato come toointegrate apprendimento al lavoro con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8068b-104">In this tutorial, you learn how toointegrate Learning at Work with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8068b-105">Apprendimento al lavoro di integrazione con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="8068b-105">Integrating Learning at Work with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8068b-106">È possibile controllare in Azure AD che ha accesso tooLearning al lavoro</span><span class="sxs-lookup"><span data-stu-id="8068b-106">You can control in Azure AD who has access tooLearning at Work</span></span>
- <span data-ttu-id="8068b-107">È possibile abilitare l'utenti tooautomatically get connesso tooLearning al lavoro (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="8068b-107">You can enable your users tooautomatically get signed-on tooLearning at Work (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8068b-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8068b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8068b-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8068b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8068b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8068b-110">Prerequisites</span></span>

<span data-ttu-id="8068b-111">tooconfigure integrazione di Azure AD con Learning al lavoro, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="8068b-111">tooconfigure Azure AD integration with Learning at Work, you need hello following items:</span></span>

- <span data-ttu-id="8068b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8068b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8068b-113">Sottoscrizione di Learning at Work abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8068b-113">A Learning at Work single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8068b-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="8068b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8068b-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="8068b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8068b-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="8068b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8068b-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8068b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8068b-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="8068b-118">Scenario description</span></span>
<span data-ttu-id="8068b-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="8068b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8068b-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="8068b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8068b-121">Aggiunta di apprendimento in lavoro dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8068b-121">Adding Learning at Work from hello gallery</span></span>
2. <span data-ttu-id="8068b-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8068b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-at-work-from-hello-gallery"></a><span data-ttu-id="8068b-123">Aggiunta di apprendimento in lavoro dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="8068b-123">Adding Learning at Work from hello gallery</span></span>
<span data-ttu-id="8068b-124">integrazione di hello tooconfigure di apprendimento al lavoro in Azure AD, è necessario tooadd apprendimento al lavoro dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="8068b-124">tooconfigure hello integration of Learning at Work into Azure AD, you need tooadd Learning at Work from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8068b-125">**tooadd apprendimento al lavoro dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8068b-125">**tooadd Learning at Work from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8068b-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8068b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8068b-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="8068b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8068b-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8068b-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="8068b-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="8068b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="8068b-133">Nella casella di ricerca hello, digitare **apprendimento al lavoro**.</span><span class="sxs-lookup"><span data-stu-id="8068b-133">In hello search box, type **Learning at Work**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_search.png)

5. <span data-ttu-id="8068b-135">Nel riquadro dei risultati hello, selezionare **apprendimento al lavoro**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8068b-135">In hello results panel, select **Learning at Work**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8068b-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8068b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8068b-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Learning at Work usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8068b-138">In this section, you configure and test Azure AD single sign-on with Learning at Work based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8068b-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Learning al lavoro è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8068b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learning at Work is tooa user in Azure AD.</span></span> <span data-ttu-id="8068b-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Learning al lavoro necessario toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="8068b-140">In other words, a link relationship between an Azure AD user and hello related user in Learning at Work needs toobe established.</span></span>

<span data-ttu-id="8068b-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in Learning al lavoro.</span><span class="sxs-lookup"><span data-stu-id="8068b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Learning at Work.</span></span>

<span data-ttu-id="8068b-142">tooconfigure e prova AD Azure single sign-on con Learning al lavoro, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="8068b-142">tooconfigure and test Azure AD single sign-on with Learning at Work, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8068b-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8068b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8068b-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8068b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8068b-145">**[Creazione di un apprendimento all'utente di prova lavoro](#creating-a-learning-at-work-test-user)**  -toohave un equivalente di Britta Simon in Learning al lavoro che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8068b-145">**[Creating a Learning at Work test user](#creating-a-learning-at-work-test-user)** - toohave a counterpart of Britta Simon in Learning at Work that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8068b-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8068b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8068b-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="8068b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8068b-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8068b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8068b-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nella formazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8068b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learning at Work application.</span></span>

<span data-ttu-id="8068b-150">**Azure AD tooconfigure single sign-on con Learning al lavoro, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8068b-150">**tooconfigure Azure AD single sign-on with Learning at Work, perform hello following steps:**</span></span>

1. <span data-ttu-id="8068b-151">Nel portale di Azure su hello hello **apprendimento al lavoro** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8068b-151">In hello Azure portal, on hello **Learning at Work** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="8068b-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8068b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_samlbase.png)

3. <span data-ttu-id="8068b-155">In hello **al dominio di lavoro e gli URL di apprendimento** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8068b-155">On hello **Learning at Work Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_url.png)

    <span data-ttu-id="8068b-157">a.</span><span class="sxs-lookup"><span data-stu-id="8068b-157">a.</span></span> <span data-ttu-id="8068b-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span><span class="sxs-lookup"><span data-stu-id="8068b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span></span>

    <span data-ttu-id="8068b-159">b.</span><span class="sxs-lookup"><span data-stu-id="8068b-159">b.</span></span> <span data-ttu-id="8068b-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span><span class="sxs-lookup"><span data-stu-id="8068b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8068b-161">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="8068b-161">These values are not hello real.</span></span> <span data-ttu-id="8068b-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="8068b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8068b-163">Contatto [al team di supporto Client di lavoro di apprendimento](https://www.learninga-z.com/site/contact/support) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="8068b-163">Contact [Learning at Work Client support team](https://www.learninga-z.com/site/contact/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="8068b-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="8068b-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_certificate.png) 

5. <span data-ttu-id="8068b-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="8068b-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8068b-168">In hello **apprendimento configurazione lavoro** fare clic su **configurare Learning al lavoro** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="8068b-168">On hello **Learning at Work Configuration** section, click **Configure Learning at Work** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8068b-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="8068b-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_configure.png) 

7. <span data-ttu-id="8068b-171">tooconfigure single sign-on sul **apprendimento al lavoro** lato, è necessario hello toosend scaricato **Metadata XML**, **ID entità SAML**, **SAML Single Sign-On URL del servizio**, e **Sign-Out URL** troppo[al supporto tecnico di lavoro di apprendimento](https://www.learninga-z.com/site/contact/support).</span><span class="sxs-lookup"><span data-stu-id="8068b-171">tooconfigure single sign-on on **Learning at Work** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL** too[Learning at Work support](https://www.learninga-z.com/site/contact/support).</span></span>

> [!TIP]
> <span data-ttu-id="8068b-172">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="8068b-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8068b-173">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="8068b-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8068b-174">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8068b-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8068b-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="8068b-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="8068b-176">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8068b-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="8068b-178">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8068b-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8068b-179">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="8068b-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8068b-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="8068b-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8068b-183">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="8068b-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8068b-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8068b-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8068b-187">a.</span><span class="sxs-lookup"><span data-stu-id="8068b-187">a.</span></span> <span data-ttu-id="8068b-188">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8068b-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8068b-189">b.</span><span class="sxs-lookup"><span data-stu-id="8068b-189">b.</span></span> <span data-ttu-id="8068b-190">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8068b-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8068b-191">c.</span><span class="sxs-lookup"><span data-stu-id="8068b-191">c.</span></span> <span data-ttu-id="8068b-192">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="8068b-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8068b-193">d.</span><span class="sxs-lookup"><span data-stu-id="8068b-193">d.</span></span> <span data-ttu-id="8068b-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8068b-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-at-work-test-user"></a><span data-ttu-id="8068b-195">Creazione di un utente test di Learning at Work</span><span class="sxs-lookup"><span data-stu-id="8068b-195">Creating a Learning at Work test user</span></span>

<span data-ttu-id="8068b-196">In questa sezione viene creato un utente di nome Britta Simon in Learning at Work.</span><span class="sxs-lookup"><span data-stu-id="8068b-196">In this section, you create a user called Britta Simon in Learning at Work.</span></span> <span data-ttu-id="8068b-197">Lavorare con [al supporto tecnico di lavoro di apprendimento](https://www.learninga-z.com/site/contact/support) utenti hello tooadd hello Learning alla piattaforma di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8068b-197">Work with [Learning at Work support](https://www.learninga-z.com/site/contact/support) tooadd hello users in hello Learning at Work platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8068b-198">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8068b-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8068b-199">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLearning al lavoro.</span><span class="sxs-lookup"><span data-stu-id="8068b-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearning at Work.</span></span>

![Assegna utente][200] 

<span data-ttu-id="8068b-201">**tooassign Britta Simon tooLearning al lavoro, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="8068b-201">**tooassign Britta Simon tooLearning at Work, perform hello following steps:**</span></span>

1. <span data-ttu-id="8068b-202">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="8068b-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="8068b-204">Nell'elenco di applicazioni hello, selezionare **apprendimento al lavoro**.</span><span class="sxs-lookup"><span data-stu-id="8068b-204">In hello applications list, select **Learning at Work**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_app.png) 

3. <span data-ttu-id="8068b-206">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8068b-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="8068b-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8068b-208">Click **Add** button.</span></span> <span data-ttu-id="8068b-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8068b-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="8068b-211">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="8068b-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8068b-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="8068b-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8068b-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="8068b-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8068b-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8068b-214">Testing single sign-on</span></span>

<span data-ttu-id="8068b-215">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="8068b-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8068b-216">Quando si fa clic hello apprendimento nel riquadro di lavoro in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato-on all'applicazione di lavoro di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="8068b-216">When you click hello Learning at Work tile in hello Access Panel, you should get automatically signed-on tooyour Learning at Work application.</span></span>
<span data-ttu-id="8068b-217">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8068b-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8068b-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8068b-218">Additional resources</span></span>

* [<span data-ttu-id="8068b-219">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8068b-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8068b-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8068b-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_203.png

