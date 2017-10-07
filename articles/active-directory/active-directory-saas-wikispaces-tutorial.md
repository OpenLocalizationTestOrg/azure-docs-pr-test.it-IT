---
title: 'Esercitazione: Integrazione di Azure Active Directory con Wikispaces | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Wikispaces.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: eb5b72e60b415cb657b70ba530df731ae14b0425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="25c89-103">Esercitazione: Integrazione di Azure Active Directory con Wikispaces</span><span class="sxs-lookup"><span data-stu-id="25c89-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>

<span data-ttu-id="25c89-104">In questa esercitazione, è illustrato come toointegrate Wikispaces con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="25c89-104">In this tutorial, you learn how toointegrate Wikispaces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="25c89-105">Integrazione di Wikispaces con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="25c89-105">Integrating Wikispaces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="25c89-106">È possibile controllare in Azure AD che ha accesso tooWikispaces</span><span class="sxs-lookup"><span data-stu-id="25c89-106">You can control in Azure AD who has access tooWikispaces</span></span>
- <span data-ttu-id="25c89-107">È possibile abilitare l'utenti tooautomatically get connesso tooWikispaces (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="25c89-107">You can enable your users tooautomatically get signed-on tooWikispaces (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="25c89-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="25c89-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="25c89-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="25c89-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25c89-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="25c89-110">Prerequisites</span></span>

<span data-ttu-id="25c89-111">integrazione di Azure AD con Wikispaces tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="25c89-111">tooconfigure Azure AD integration with Wikispaces, you need hello following items:</span></span>

- <span data-ttu-id="25c89-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c89-112">An Azure AD subscription</span></span>
- <span data-ttu-id="25c89-113">Sottoscrizione di Wikispaces abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="25c89-113">A Wikispaces single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="25c89-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="25c89-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="25c89-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="25c89-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="25c89-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="25c89-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="25c89-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="25c89-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="25c89-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="25c89-118">Scenario description</span></span>
<span data-ttu-id="25c89-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="25c89-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="25c89-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="25c89-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="25c89-121">Aggiunta di Wikispaces dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="25c89-121">Adding Wikispaces from hello gallery</span></span>
2. <span data-ttu-id="25c89-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="25c89-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wikispaces-from-hello-gallery"></a><span data-ttu-id="25c89-123">Aggiunta di Wikispaces dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="25c89-123">Adding Wikispaces from hello gallery</span></span>
<span data-ttu-id="25c89-124">integrazione hello tooconfigure di Wikispaces in Azure AD, è necessario tooadd Wikispaces dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="25c89-124">tooconfigure hello integration of Wikispaces into Azure AD, you need tooadd Wikispaces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="25c89-125">**tooadd Wikispaces dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="25c89-125">**tooadd Wikispaces from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="25c89-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="25c89-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="25c89-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="25c89-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="25c89-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="25c89-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="25c89-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="25c89-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="25c89-133">Nella casella di ricerca hello, digitare **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="25c89-133">In hello search box, type **Wikispaces**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_search.png)

5. <span data-ttu-id="25c89-135">Nel riquadro dei risultati hello, selezionare **Wikispaces**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="25c89-135">In hello results panel, select **Wikispaces**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="25c89-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="25c89-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="25c89-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Wikispaces usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="25c89-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="25c89-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Wikispaces è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c89-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wikispaces is tooa user in Azure AD.</span></span> <span data-ttu-id="25c89-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Wikispaces deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="25c89-140">In other words, a link relationship between an Azure AD user and hello related user in Wikispaces needs toobe established.</span></span>

<span data-ttu-id="25c89-141">In Wikispaces, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="25c89-141">In Wikispaces, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="25c89-142">tooconfigure e prova AD Azure single sign-on con Wikispaces, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="25c89-142">tooconfigure and test Azure AD single sign-on with Wikispaces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="25c89-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="25c89-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="25c89-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25c89-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="25c89-145">**[Creazione di un utente test Wikispaces](#creating-a-wikispaces-test-user)**  -toohave un equivalente di Britta Simon in Wikispaces che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="25c89-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - toohave a counterpart of Britta Simon in Wikispaces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="25c89-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="25c89-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="25c89-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="25c89-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="25c89-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="25c89-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="25c89-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="25c89-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wikispaces application.</span></span>

<span data-ttu-id="25c89-150">**Azure AD tooconfigure single sign-on con Wikispaces, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="25c89-150">**tooconfigure Azure AD single sign-on with Wikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="25c89-151">Nel portale di Azure su hello hello **Wikispaces** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="25c89-151">In hello Azure portal, on hello **Wikispaces** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="25c89-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="25c89-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

3. <span data-ttu-id="25c89-155">In hello **Wikispaces dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="25c89-155">On hello **Wikispaces Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_url.png)

    <span data-ttu-id="25c89-157">a.</span><span class="sxs-lookup"><span data-stu-id="25c89-157">a.</span></span> <span data-ttu-id="25c89-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.wikispaces.net`</span><span class="sxs-lookup"><span data-stu-id="25c89-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.wikispaces.net`</span></span>

    <span data-ttu-id="25c89-159">b.</span><span class="sxs-lookup"><span data-stu-id="25c89-159">b.</span></span> <span data-ttu-id="25c89-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://session.wikispaces.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="25c89-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://session.wikispaces.net/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="25c89-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="25c89-161">These values are not real.</span></span> <span data-ttu-id="25c89-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="25c89-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="25c89-163">Contatto [team di supporto di Wikispaces Client](https://www.wikispaces.com/site/help) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="25c89-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) tooget these values.</span></span> 

4. <span data-ttu-id="25c89-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="25c89-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

5. <span data-ttu-id="25c89-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="25c89-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wikispaces-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="25c89-168">tooconfigure single sign-on sul **Wikispaces** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto di Wikispaces](https://www.wikispaces.com/site/help).</span><span class="sxs-lookup"><span data-stu-id="25c89-168">tooconfigure single sign-on on **Wikispaces** side, you need toosend hello downloaded **Metadata XML** too[Wikispaces support team](https://www.wikispaces.com/site/help).</span></span> <span data-ttu-id="25c89-169">Si riceverà una notifica non appena la configurazione hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="25c89-169">You will get a notification as soon as hello configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="25c89-170">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="25c89-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="25c89-171">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="25c89-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="25c89-172">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="25c89-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="25c89-173">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="25c89-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="25c89-174">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="25c89-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="25c89-176">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="25c89-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="25c89-177">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="25c89-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="25c89-179">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="25c89-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="25c89-181">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="25c89-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="25c89-183">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="25c89-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="25c89-185">a.</span><span class="sxs-lookup"><span data-stu-id="25c89-185">a.</span></span> <span data-ttu-id="25c89-186">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="25c89-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="25c89-187">b.</span><span class="sxs-lookup"><span data-stu-id="25c89-187">b.</span></span> <span data-ttu-id="25c89-188">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="25c89-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="25c89-189">c.</span><span class="sxs-lookup"><span data-stu-id="25c89-189">c.</span></span> <span data-ttu-id="25c89-190">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="25c89-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="25c89-191">d.</span><span class="sxs-lookup"><span data-stu-id="25c89-191">d.</span></span> <span data-ttu-id="25c89-192">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="25c89-192">Click **Create**.</span></span>
 
### <a name="creating-a-wikispaces-test-user"></a><span data-ttu-id="25c89-193">Creazione di un utente di test di Wikispaces</span><span class="sxs-lookup"><span data-stu-id="25c89-193">Creating a Wikispaces test user</span></span>

<span data-ttu-id="25c89-194">In ordine tooenable Azure AD utenti toolog in tooWikispaces, è necessario eseguirne il provisioning in Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="25c89-194">In order tooenable Azure AD users toolog in tooWikispaces, they must be provisioned into Wikispaces.</span></span> <span data-ttu-id="25c89-195">Nel caso di hello di Wikispaces, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="25c89-195">In hello case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="25c89-196">eseguire un account utente, tooprovision hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="25c89-196">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="25c89-197">Accedi tooyour **Wikispaces** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="25c89-197">Log in tooyour **Wikispaces** company site as an administrator.</span></span>

2. <span data-ttu-id="25c89-198">Andare troppo**membri**.</span><span class="sxs-lookup"><span data-stu-id="25c89-198">Go too**Members**.</span></span>
   
    <span data-ttu-id="25c89-199">![Members](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Members")</span><span class="sxs-lookup"><span data-stu-id="25c89-199">![Members](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Members")</span></span>

3. <span data-ttu-id="25c89-200">Fare clic su hello **Invite People**.</span><span class="sxs-lookup"><span data-stu-id="25c89-200">Click hello **Invite People**.</span></span>
   
    <span data-ttu-id="25c89-201">![Invitare persone](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invitare persone")</span><span class="sxs-lookup"><span data-stu-id="25c89-201">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invite People")</span></span>

4. <span data-ttu-id="25c89-202">In hello **Invite People** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="25c89-202">In hello **Invite People** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="25c89-203">![Invitare persone](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invitare persone")</span><span class="sxs-lookup"><span data-stu-id="25c89-203">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invite People")</span></span>
   
    <span data-ttu-id="25c89-204">a.</span><span class="sxs-lookup"><span data-stu-id="25c89-204">a.</span></span> <span data-ttu-id="25c89-205">Hello tipo **nomi utente o l'indirizzo di posta elettronica** di un account aAd di cui si desidera tooprovision in hello relative caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="25c89-205">Type hello **Usernames or Email Address** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="25c89-206">b.</span><span class="sxs-lookup"><span data-stu-id="25c89-206">b.</span></span> <span data-ttu-id="25c89-207">Fare clic su **Send**.</span><span class="sxs-lookup"><span data-stu-id="25c89-207">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="25c89-208">titolare dell'account di Azure Active Directory Hello riceve un messaggio di posta elettronica tra un account di hello tooconfirm collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="25c89-208">hello Azure Active Directory account holder receives an email including a link tooconfirm hello account before it becomes active.</span></span>
    
> [!NOTE]
> <span data-ttu-id="25c89-209">È possibile usare qualsiasi altro Wikispaces utente account strumento di creazione o le API fornite da Wikispaces tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="25c89-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="25c89-210">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="25c89-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="25c89-211">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWikispaces.</span><span class="sxs-lookup"><span data-stu-id="25c89-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWikispaces.</span></span>

![Assegna utente][200] 

<span data-ttu-id="25c89-213">**tooassign Britta Simon tooWikispaces, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="25c89-213">**tooassign Britta Simon tooWikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="25c89-214">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="25c89-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="25c89-216">Nell'elenco di applicazioni hello, selezionare **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="25c89-216">In hello applications list, select **Wikispaces**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_app.png) 

3. <span data-ttu-id="25c89-218">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="25c89-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="25c89-220">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="25c89-220">Click **Add** button.</span></span> <span data-ttu-id="25c89-221">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="25c89-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="25c89-223">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="25c89-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="25c89-224">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="25c89-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="25c89-225">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="25c89-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="25c89-226">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="25c89-226">Testing single sign-on</span></span>

<span data-ttu-id="25c89-227">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="25c89-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="25c89-228">Quando si fa clic hello Wikispaces riquadro in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in Wikispaces applicazione.</span><span class="sxs-lookup"><span data-stu-id="25c89-228">When you click hello Wikispaces tile in hello Access Panel, you should get automatically signed-on tooyour Wikispaces application.</span></span>
<span data-ttu-id="25c89-229">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="25c89-229">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="25c89-230">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="25c89-230">Additional resources</span></span>

* [<span data-ttu-id="25c89-231">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25c89-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="25c89-232">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25c89-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_203.png

