---
title: 'Esercitazione: Integrazione di Azure Active Directory con RightAnswers | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e RightAnswers.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7f09e25a-a716-41e1-8ca3-fd00e3d1b8cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 745e7ed5a13291afeed8f48a595e95b27d4b0e58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightanswers"></a><span data-ttu-id="70b9c-103">Esercitazione: Integrazione di Azure Active Directory con RightAnswers</span><span class="sxs-lookup"><span data-stu-id="70b9c-103">Tutorial: Azure Active Directory integration with RightAnswers</span></span>

<span data-ttu-id="70b9c-104">In questa esercitazione, è illustrato come toointegrate RightAnswers con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70b9c-104">In this tutorial, you learn how toointegrate RightAnswers with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70b9c-105">Integrazione RightAnswers con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="70b9c-105">Integrating RightAnswers with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="70b9c-106">È possibile controllare in Azure AD che ha accesso tooRightAnswers</span><span class="sxs-lookup"><span data-stu-id="70b9c-106">You can control in Azure AD who has access tooRightAnswers</span></span>
- <span data-ttu-id="70b9c-107">È possibile abilitare l'utenti tooautomatically get connesso tooRightAnswers (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="70b9c-107">You can enable your users tooautomatically get signed-on tooRightAnswers (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70b9c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="70b9c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="70b9c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70b9c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70b9c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="70b9c-110">Prerequisites</span></span>

<span data-ttu-id="70b9c-111">integrazione di Azure AD con RightAnswers tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="70b9c-111">tooconfigure Azure AD integration with RightAnswers, you need hello following items:</span></span>

- <span data-ttu-id="70b9c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70b9c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70b9c-113">Sottoscrizione di RightAnswers abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="70b9c-113">A RightAnswers single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70b9c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="70b9c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70b9c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="70b9c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70b9c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="70b9c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70b9c-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70b9c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70b9c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="70b9c-118">Scenario description</span></span>
<span data-ttu-id="70b9c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="70b9c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70b9c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="70b9c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70b9c-121">Aggiunta di RightAnswers dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="70b9c-121">Adding RightAnswers from hello gallery</span></span>
2. <span data-ttu-id="70b9c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="70b9c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightanswers-from-hello-gallery"></a><span data-ttu-id="70b9c-123">Aggiunta di RightAnswers dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="70b9c-123">Adding RightAnswers from hello gallery</span></span>
<span data-ttu-id="70b9c-124">integrazione hello tooconfigure di RightAnswers in Azure AD, è necessario tooadd RightAnswers dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="70b9c-124">tooconfigure hello integration of RightAnswers into Azure AD, you need tooadd RightAnswers from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="70b9c-125">**tooadd RightAnswers dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="70b9c-125">**tooadd RightAnswers from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="70b9c-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="70b9c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70b9c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="70b9c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="70b9c-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="70b9c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="70b9c-133">Nella casella di ricerca hello, digitare **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-133">In hello search box, type **RightAnswers**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_search.png)

5. <span data-ttu-id="70b9c-135">Nel riquadro dei risultati hello, selezionare **RightAnswers**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="70b9c-135">In hello results panel, select **RightAnswers**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70b9c-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="70b9c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70b9c-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con RightAnswers usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="70b9c-138">In this section, you configure and test Azure AD single sign-on with RightAnswers based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="70b9c-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in RightAnswers è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70b9c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RightAnswers is tooa user in Azure AD.</span></span> <span data-ttu-id="70b9c-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in RightAnswers deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="70b9c-140">In other words, a link relationship between an Azure AD user and hello related user in RightAnswers needs toobe established.</span></span>

<span data-ttu-id="70b9c-141">In RightAnswers, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="70b9c-141">In RightAnswers, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="70b9c-142">tooconfigure e prova AD Azure single sign-on con RightAnswers, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="70b9c-142">tooconfigure and test Azure AD single sign-on with RightAnswers, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="70b9c-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="70b9c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="70b9c-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70b9c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70b9c-145">**[Creazione di un utente test RightAnswers](#creating-a-rightanswers-test-user)**  -toohave un equivalente di Britta Simon in RightAnswers che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="70b9c-145">**[Creating a RightAnswers test user](#creating-a-rightanswers-test-user)** - toohave a counterpart of Britta Simon in RightAnswers that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="70b9c-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="70b9c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70b9c-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="70b9c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70b9c-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="70b9c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70b9c-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="70b9c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RightAnswers application.</span></span>

<span data-ttu-id="70b9c-150">**Azure AD tooconfigure single sign-on con RightAnswers, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="70b9c-150">**tooconfigure Azure AD single sign-on with RightAnswers, perform hello following steps:**</span></span>

1. <span data-ttu-id="70b9c-151">Nel portale di Azure su hello hello **RightAnswers** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-151">In hello Azure portal, on hello **RightAnswers** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="70b9c-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="70b9c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_samlbase.png)

3. <span data-ttu-id="70b9c-155">In hello **RightAnswers dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="70b9c-155">On hello **RightAnswers Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_url.png)

    <span data-ttu-id="70b9c-157">a.</span><span class="sxs-lookup"><span data-stu-id="70b9c-157">a.</span></span> <span data-ttu-id="70b9c-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.rightanswers.com/portal/ss/`</span><span class="sxs-lookup"><span data-stu-id="70b9c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.rightanswers.com/portal/ss/`</span></span>

    <span data-ttu-id="70b9c-159">b.</span><span class="sxs-lookup"><span data-stu-id="70b9c-159">b.</span></span> <span data-ttu-id="70b9c-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.rightanswers.com:<identifier>/portal`</span><span class="sxs-lookup"><span data-stu-id="70b9c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.rightanswers.com:<identifier>/portal`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="70b9c-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="70b9c-161">These values are not real.</span></span> <span data-ttu-id="70b9c-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="70b9c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="70b9c-163">Contatto [team di supporto RightAnswers Client](https://www.rightanswers.com/contact-us/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="70b9c-163">Contact [RightAnswers Client support team](https://www.rightanswers.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="70b9c-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="70b9c-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_certificate.png) 

5. <span data-ttu-id="70b9c-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="70b9c-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightanswers-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="70b9c-168">tooconfigure single sign-on sul **RightAnswers** lato, è necessario hello toosend scaricato **Metadata XML** troppo[RightAnswers team di supporto](https://www.rightanswers.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="70b9c-168">tooconfigure single sign-on on **RightAnswers** side, you need toosend hello downloaded **Metadata XML** too[RightAnswers support team](https://www.rightanswers.com/contact-us/).</span></span>

    >[!NOTE]
    ><span data-ttu-id="70b9c-169">Il team di supporto RightAnswers dispone di configurazione di SSO toodo hello effettivo.</span><span class="sxs-lookup"><span data-stu-id="70b9c-169">Your RightAnswers support team has toodo hello actual SSO configuration.</span></span>
    ><span data-ttu-id="70b9c-170">Una volta completata l'abilitazione dell'accesso Single Sign-On per la sottoscrizione, si riceverà una notifica.</span><span class="sxs-lookup"><span data-stu-id="70b9c-170">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="70b9c-171">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="70b9c-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="70b9c-172">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="70b9c-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="70b9c-173">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70b9c-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70b9c-174">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="70b9c-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="70b9c-175">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="70b9c-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="70b9c-177">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="70b9c-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="70b9c-178">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="70b9c-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70b9c-180">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70b9c-182">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="70b9c-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70b9c-184">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="70b9c-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70b9c-186">a.</span><span class="sxs-lookup"><span data-stu-id="70b9c-186">a.</span></span> <span data-ttu-id="70b9c-187">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70b9c-188">b.</span><span class="sxs-lookup"><span data-stu-id="70b9c-188">b.</span></span> <span data-ttu-id="70b9c-189">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="70b9c-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70b9c-190">c.</span><span class="sxs-lookup"><span data-stu-id="70b9c-190">c.</span></span> <span data-ttu-id="70b9c-191">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="70b9c-192">d.</span><span class="sxs-lookup"><span data-stu-id="70b9c-192">d.</span></span> <span data-ttu-id="70b9c-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-193">Click **Create**.</span></span>
 
### <a name="creating-a-rightanswers-test-user"></a><span data-ttu-id="70b9c-194">Creazione di un utente di test di RightAnswers</span><span class="sxs-lookup"><span data-stu-id="70b9c-194">Creating a RightAnswers test user</span></span>

<span data-ttu-id="70b9c-195">toolog agli utenti di Azure AD tooenable in tooRightAnswers, è necessario eseguirne il provisioning in RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="70b9c-195">tooenable Azure AD users toolog in tooRightAnswers, they must be provisioned into RightAnswers.</span></span> <span data-ttu-id="70b9c-196">Nel caso di RightAnswers, il provisioning è un'attività automatica e non è quindi necessario alcun intervento dell'utente.</span><span class="sxs-lookup"><span data-stu-id="70b9c-196">When RightAnswers, provisioning is an automated task so there is no action item for you.</span></span>

<span data-ttu-id="70b9c-197">Gli utenti vengono creati automaticamente se necessario, durante hello primo single sign-on tentativo.</span><span class="sxs-lookup"><span data-stu-id="70b9c-197">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="70b9c-198">È possibile usare qualsiasi altro RightAnswers utente account strumento di creazione o le API fornite da RightAnswers tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="70b9c-198">You can use any other RightAnswers user account creation tools or APIs provided by RightAnswers tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="70b9c-199">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="70b9c-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="70b9c-200">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooRightAnswers.</span><span class="sxs-lookup"><span data-stu-id="70b9c-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRightAnswers.</span></span>

![Assegna utente][200] 

<span data-ttu-id="70b9c-202">**tooassign Britta Simon tooRightAnswers, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="70b9c-202">**tooassign Britta Simon tooRightAnswers, perform hello following steps:**</span></span>

1. <span data-ttu-id="70b9c-203">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="70b9c-205">Nell'elenco di applicazioni hello, selezionare **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-205">In hello applications list, select **RightAnswers**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_app.png) 

3. <span data-ttu-id="70b9c-207">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="70b9c-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-209">Click **Add** button.</span></span> <span data-ttu-id="70b9c-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="70b9c-212">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="70b9c-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="70b9c-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70b9c-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="70b9c-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70b9c-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="70b9c-215">Testing single sign-on</span></span>

<span data-ttu-id="70b9c-216">Se si desiderano tootest le impostazioni SSO, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="70b9c-216">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="70b9c-217">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="70b9c-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>
## <a name="additional-resources"></a><span data-ttu-id="70b9c-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="70b9c-218">Additional resources</span></span>

* [<span data-ttu-id="70b9c-219">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70b9c-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70b9c-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70b9c-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_203.png

