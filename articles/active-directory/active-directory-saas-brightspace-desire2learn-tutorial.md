---
title: 'Esercitazione: Integrazione di Azure Active Directory con Brightspace by Desire2Learn | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Brightspace by Desire2Learn.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2d3065b-1f6c-4c45-af78-0d5da3266999
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 99d03dc50defcb291a651a5415e30baab39e1e77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-brightspace-by-desire2learn"></a><span data-ttu-id="598f4-103">Esercitazione: Integrazione di Azure Active Directory con Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="598f4-103">Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn</span></span>

<span data-ttu-id="598f4-104">In questa esercitazione, è illustrato come toointegrate Brightspace by Desire2Learn con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="598f4-104">In this tutorial, you learn how toointegrate Brightspace by Desire2Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="598f4-105">Integrazione di Brightspace by Desire2Learn con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="598f4-105">Integrating Brightspace by Desire2Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="598f4-106">È possibile controllare in Azure AD che ha accesso tooBrightspace da Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="598f4-106">You can control in Azure AD who has access tooBrightspace by Desire2Learn</span></span>
- <span data-ttu-id="598f4-107">È possibile abilitare l'utenti tooautomatically get connesso tooBrightspace da Desire2Learn (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="598f4-107">You can enable your users tooautomatically get signed-on tooBrightspace by Desire2Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="598f4-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="598f4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="598f4-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="598f4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="598f4-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="598f4-110">Prerequisites</span></span>

<span data-ttu-id="598f4-111">integrazione di Azure AD con Brightspace by Desire2Learn tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="598f4-111">tooconfigure Azure AD integration with Brightspace by Desire2Learn, you need hello following items:</span></span>

- <span data-ttu-id="598f4-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="598f4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="598f4-113">Sottoscrizione di Brightspace by Desire2Learn abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="598f4-113">A Brightspace by Desire2Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="598f4-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="598f4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="598f4-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="598f4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="598f4-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="598f4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="598f4-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="598f4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="598f4-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="598f4-118">Scenario description</span></span>
<span data-ttu-id="598f4-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="598f4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="598f4-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="598f4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="598f4-121">Aggiunta di Brightspace by Desire2Learn dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="598f4-121">Adding Brightspace by Desire2Learn from hello gallery</span></span>
2. <span data-ttu-id="598f4-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="598f4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-brightspace-by-desire2learn-from-hello-gallery"></a><span data-ttu-id="598f4-123">Aggiunta di Brightspace by Desire2Learn dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="598f4-123">Adding Brightspace by Desire2Learn from hello gallery</span></span>
<span data-ttu-id="598f4-124">integrazione hello tooconfigure di Brightspace by Desire2Learn in Azure AD, è necessario tooadd Brightspace by Desire2Learn dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="598f4-124">tooconfigure hello integration of Brightspace by Desire2Learn into Azure AD, you need tooadd Brightspace by Desire2Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="598f4-125">**tooadd Brightspace by Desire2Learn dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="598f4-125">**tooadd Brightspace by Desire2Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="598f4-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="598f4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="598f4-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="598f4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="598f4-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="598f4-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="598f4-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="598f4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="598f4-133">Nella casella di ricerca hello, digitare **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="598f4-133">In hello search box, type **Brightspace by Desire2Learn**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_search.png)

5. <span data-ttu-id="598f4-135">Nel riquadro dei risultati hello, selezionare **Brightspace by Desire2Learn**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="598f4-135">In hello results panel, select **Brightspace by Desire2Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="598f4-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="598f4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="598f4-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Brightspace by Desire2Learn usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="598f4-138">In this section, you configure and test Azure AD single sign-on with Brightspace by Desire2Learn based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="598f4-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Brightspace by Desire2Learn è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="598f4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Brightspace by Desire2Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="598f4-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Brightspace by Desire2Learn deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="598f4-140">In other words, a link relationship between an Azure AD user and hello related user in Brightspace by Desire2Learn needs toobe established.</span></span>

<span data-ttu-id="598f4-141">In Brightspace by Desire2Learn, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="598f4-141">In Brightspace by Desire2Learn, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="598f4-142">tooconfigure e prova AD Azure single sign-on con Brightspace by Desire2Learn, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="598f4-142">tooconfigure and test Azure AD single sign-on with Brightspace by Desire2Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="598f4-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="598f4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="598f4-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="598f4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="598f4-145">**[Creazione di Brightspace by Desire2Learn test utente](#creating-a-brightspace-by-desire2learn-test-user)**  -toohave un equivalente di Britta Simon in Brightspace by Desire2Learn che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="598f4-145">**[Creating a Brightspace by Desire2Learn test user](#creating-a-brightspace-by-desire2learn-test-user)** - toohave a counterpart of Britta Simon in Brightspace by Desire2Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="598f4-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="598f4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="598f4-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="598f4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="598f4-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="598f4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="598f4-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on di Brightspace, dall'applicazione Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="598f4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Brightspace by Desire2Learn application.</span></span>

<span data-ttu-id="598f4-150">**Azure AD tooconfigure single sign-on con Brightspace by Desire2Learn, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="598f4-150">**tooconfigure Azure AD single sign-on with Brightspace by Desire2Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="598f4-151">Nel portale di Azure su hello hello **Brightspace by Desire2Learn** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="598f4-151">In hello Azure portal, on hello **Brightspace by Desire2Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="598f4-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="598f4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_samlbase.png)

3. <span data-ttu-id="598f4-155">In hello **Brightspace by Desire2Learn dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="598f4-155">On hello **Brightspace by Desire2Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_url.png)

    <span data-ttu-id="598f4-157">a.</span><span class="sxs-lookup"><span data-stu-id="598f4-157">a.</span></span> <span data-ttu-id="598f4-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="598f4-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.tenants.brightspace.com/samlLogin`|
    | `https://<companyname>.desire2learn.com/shibboleth-sp`|

    <span data-ttu-id="598f4-159">b.</span><span class="sxs-lookup"><span data-stu-id="598f4-159">b.</span></span> <span data-ttu-id="598f4-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span><span class="sxs-lookup"><span data-stu-id="598f4-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="598f4-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="598f4-161">These values are not real.</span></span> <span data-ttu-id="598f4-162">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="598f4-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="598f4-163">Contatto [Brightspace by Desire2Learn team di supporto](https://www.d2l.com/contact/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="598f4-163">Contact [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/) tooget these values.</span></span>
 


4. <span data-ttu-id="598f4-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="598f4-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_certificate.png) 

5. <span data-ttu-id="598f4-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="598f4-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="598f4-168">tooconfigure single sign-on sul **Brightspace by Desire2Learn** lato, è necessario hello toosend scaricato **Metadata XML** troppo[Brightspace by Desire2Learn team di supporto](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="598f4-168">tooconfigure single sign-on on **Brightspace by Desire2Learn** side, you need toosend hello downloaded **Metadata XML** too[Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="598f4-169">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="598f4-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="598f4-170">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="598f4-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="598f4-171">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="598f4-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="598f4-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="598f4-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="598f4-173">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="598f4-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="598f4-175">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="598f4-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="598f4-176">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="598f4-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="598f4-178">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="598f4-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="598f4-180">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="598f4-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="598f4-182">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="598f4-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="598f4-184">a.</span><span class="sxs-lookup"><span data-stu-id="598f4-184">a.</span></span> <span data-ttu-id="598f4-185">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="598f4-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="598f4-186">b.</span><span class="sxs-lookup"><span data-stu-id="598f4-186">b.</span></span> <span data-ttu-id="598f4-187">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="598f4-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="598f4-188">c.</span><span class="sxs-lookup"><span data-stu-id="598f4-188">c.</span></span> <span data-ttu-id="598f4-189">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="598f4-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="598f4-190">d.</span><span class="sxs-lookup"><span data-stu-id="598f4-190">d.</span></span> <span data-ttu-id="598f4-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="598f4-191">Click **Create**.</span></span>
 
### <a name="creating-a-brightspace-by-desire2learn-test-user"></a><span data-ttu-id="598f4-192">Creazione di un utente di test di Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="598f4-192">Creating a Brightspace by Desire2Learn test user</span></span>

<span data-ttu-id="598f4-193">In ordine tooenable Azure AD utenti toolog a Brightspace by Desire2Learn, è necessario il provisioning in Brightspace da Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="598f4-193">In order tooenable Azure AD users toolog into Brightspace by Desire2Learn, they must be provisioned into Brightspace by Desire2Learn.</span></span>  

<span data-ttu-id="598f4-194">Nel caso di hello di Brightspace by Desire2Learn, gli account utente di hello necessitano toobe creati il [Brightspace by Desire2Learn team di supporto](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="598f4-194">In hello case of Brightspace by Desire2Learn, hello user accounts need toobe created by your [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

>[!NOTE]
><span data-ttu-id="598f4-195">È possibile usare qualsiasi altro Brightspace da strumento di creazione di account utente Desire2Learn o le API fornite da Brightspace da Desire2Learn tooprovision Azure Active Directory gli account utente.</span><span class="sxs-lookup"><span data-stu-id="598f4-195">You can use any other Brightspace by Desire2Learn user account creation tools or APIs provided by Brightspace by Desire2Learn tooprovision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="598f4-196">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="598f4-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="598f4-197">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBrightspace da Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="598f4-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBrightspace by Desire2Learn.</span></span>

![Assegna utente][200] 

<span data-ttu-id="598f4-199">**tooassign Britta Simon tooBrightspace da Desire2Learn, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="598f4-199">**tooassign Britta Simon tooBrightspace by Desire2Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="598f4-200">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="598f4-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="598f4-202">Nell'elenco di applicazioni hello, selezionare **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="598f4-202">In hello applications list, select **Brightspace by Desire2Learn**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_app.png) 

3. <span data-ttu-id="598f4-204">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="598f4-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="598f4-206">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="598f4-206">Click **Add** button.</span></span> <span data-ttu-id="598f4-207">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="598f4-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="598f4-209">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="598f4-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="598f4-210">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="598f4-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="598f4-211">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="598f4-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="598f4-212">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="598f4-212">Testing single sign-on</span></span>

<span data-ttu-id="598f4-213">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="598f4-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="598f4-214">Quando si fa clic hello Brightspace dal riquadro Desire2Learn in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Brightspace dall'applicazione Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="598f4-214">When you click hello Brightspace by Desire2Learn tile in hello Access Panel, you should get automatically signed-on tooyour Brightspace by Desire2Learn application.</span></span>
<span data-ttu-id="598f4-215">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="598f4-215">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="598f4-216">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="598f4-216">Additional resources</span></span>

* [<span data-ttu-id="598f4-217">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="598f4-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="598f4-218">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="598f4-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_203.png

