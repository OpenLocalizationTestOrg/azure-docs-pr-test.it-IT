---
title: 'Esercitazione: Integrazione di Azure Active Directory con Expensify | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed Expensify.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: 141513ef27c90dae2d77a52ecab2f89c4e5a55ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="35f1e-103">Esercitazione: Integrazione di Azure Active Directory con Expensify</span><span class="sxs-lookup"><span data-stu-id="35f1e-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="35f1e-104">In questa esercitazione, è illustrato come toointegrate Expensify con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35f1e-104">In this tutorial, you learn how toointegrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35f1e-105">Integrazione Expensify con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="35f1e-105">Integrating Expensify with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="35f1e-106">È possibile controllare in Azure AD che ha accesso tooExpensify</span><span class="sxs-lookup"><span data-stu-id="35f1e-106">You can control in Azure AD who has access tooExpensify</span></span>
- <span data-ttu-id="35f1e-107">È possibile abilitare l'utenti tooautomatically get connesso tooExpensify (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="35f1e-107">You can enable your users tooautomatically get signed-on tooExpensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="35f1e-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="35f1e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="35f1e-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35f1e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35f1e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="35f1e-110">Prerequisites</span></span>

<span data-ttu-id="35f1e-111">integrazione di Azure AD con Expensify tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="35f1e-111">tooconfigure Azure AD integration with Expensify, you need hello following items:</span></span>

- <span data-ttu-id="35f1e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35f1e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="35f1e-113">Sottoscrizione di Expensify abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="35f1e-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="35f1e-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="35f1e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="35f1e-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="35f1e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="35f1e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="35f1e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="35f1e-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35f1e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="35f1e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="35f1e-118">Scenario description</span></span>
<span data-ttu-id="35f1e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="35f1e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="35f1e-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="35f1e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35f1e-121">Aggiunta di Expensify dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="35f1e-121">Adding Expensify from hello gallery</span></span>
2. <span data-ttu-id="35f1e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="35f1e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-hello-gallery"></a><span data-ttu-id="35f1e-123">Aggiunta di Expensify dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="35f1e-123">Adding Expensify from hello gallery</span></span>
<span data-ttu-id="35f1e-124">integrazione hello tooconfigure di Expensify in Azure AD, è necessario tooadd Expensify dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="35f1e-124">tooconfigure hello integration of Expensify into Azure AD, you need tooadd Expensify from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="35f1e-125">**tooadd Expensify dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="35f1e-125">**tooadd Expensify from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="35f1e-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="35f1e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="35f1e-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="35f1e-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="35f1e-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="35f1e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="35f1e-133">Nella casella di ricerca hello, digitare **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-133">In hello search box, type **Expensify**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="35f1e-135">Nel riquadro dei risultati hello, selezionare **Expensify**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="35f1e-135">In hello results panel, select **Expensify**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="35f1e-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="35f1e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="35f1e-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Expensify con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="35f1e-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="35f1e-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Expensify è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35f1e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Expensify is tooa user in Azure AD.</span></span> <span data-ttu-id="35f1e-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Expensify deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="35f1e-140">In other words, a link relationship between an Azure AD user and hello related user in Expensify needs toobe established.</span></span>

<span data-ttu-id="35f1e-141">In Expensify, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="35f1e-141">In Expensify, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="35f1e-142">tooconfigure e prova AD Azure single sign-on con Expensify, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="35f1e-142">tooconfigure and test Azure AD single sign-on with Expensify, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="35f1e-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="35f1e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="35f1e-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="35f1e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="35f1e-145">**[Creazione di un utente test Expensify](#creating-an-expensify-test-user)**  -toohave un equivalente di Britta Simon in Expensify che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="35f1e-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - toohave a counterpart of Britta Simon in Expensify that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="35f1e-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="35f1e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="35f1e-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="35f1e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="35f1e-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="35f1e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="35f1e-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Expensify.</span><span class="sxs-lookup"><span data-stu-id="35f1e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="35f1e-150">**Azure AD tooconfigure single sign-on con Expensify, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="35f1e-150">**tooconfigure Azure AD single sign-on with Expensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="35f1e-151">Nel portale di Azure su hello hello **Expensify** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-151">In hello Azure portal, on hello **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="35f1e-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="35f1e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="35f1e-155">In hello **Expensify dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="35f1e-155">On hello **Expensify Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="35f1e-157">a.</span><span class="sxs-lookup"><span data-stu-id="35f1e-157">a.</span></span> <span data-ttu-id="35f1e-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.expensify.com/authentication/saml/login`</span><span class="sxs-lookup"><span data-stu-id="35f1e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="35f1e-159">b.</span><span class="sxs-lookup"><span data-stu-id="35f1e-159">b.</span></span> <span data-ttu-id="35f1e-160">In hello **URL dell'identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="35f1e-160">In hello **Identifier URL** textbox, type a URL using hello following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="35f1e-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="35f1e-161">These values are not real.</span></span> <span data-ttu-id="35f1e-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore URL.</span><span class="sxs-lookup"><span data-stu-id="35f1e-162">Update these values with hello actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="35f1e-163">Contatto [team di supporto Client Expensify](mailto:help@expensify.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="35f1e-163">Contact [Expensify Client support team](mailto:help@expensify.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="35f1e-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="35f1e-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="35f1e-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="35f1e-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="35f1e-168">tooenable in Expensify SSO, è necessario innanzitutto tooenable **controllo dominio** in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="35f1e-168">tooenable SSO in Expensify, you first need tooenable **Domain Control** in hello application.</span></span> <span data-ttu-id="35f1e-169">È possibile abilitare il controllo di dominio in un'applicazione hello passaggi hello elencati [qui](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="35f1e-169">You can enable Domain Control in hello application through hello steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="35f1e-170">Per ulteriore supporto, contattare il [team di supporto clienti di Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="35f1e-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="35f1e-171">Dopo aver abilitato il controllo di dominio seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="35f1e-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="35f1e-173">a.</span><span class="sxs-lookup"><span data-stu-id="35f1e-173">a.</span></span> <span data-ttu-id="35f1e-174">Accesso tooyour Expensify applicazione.</span><span class="sxs-lookup"><span data-stu-id="35f1e-174">Sign on tooyour Expensify application.</span></span>
    
    <span data-ttu-id="35f1e-175">b.</span><span class="sxs-lookup"><span data-stu-id="35f1e-175">b.</span></span> <span data-ttu-id="35f1e-176">Nella barra degli strumenti hello in primo piano hello, fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-176">In hello toolbar on hello top, click **Admin**.</span></span>
    
    <span data-ttu-id="35f1e-177">c.</span><span class="sxs-lookup"><span data-stu-id="35f1e-177">c.</span></span> <span data-ttu-id="35f1e-178">Nel riquadro sinistro di hello, fare clic su **dominio**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-178">In hello left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="35f1e-179">d.</span><span class="sxs-lookup"><span data-stu-id="35f1e-179">d.</span></span> <span data-ttu-id="35f1e-180">Fare clic sul nome di dominio verificato.</span><span class="sxs-lookup"><span data-stu-id="35f1e-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="35f1e-181">e.</span><span class="sxs-lookup"><span data-stu-id="35f1e-181">e.</span></span> <span data-ttu-id="35f1e-182">Nel riquadro sinistro di hello, fare clic su **SAML**, quindi selezionare **abilitato**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-182">In hello left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="35f1e-183">f.</span><span class="sxs-lookup"><span data-stu-id="35f1e-183">f.</span></span> <span data-ttu-id="35f1e-184">Aprire hello scaricato i metadati della federazione da Azure AD nel blocco note, hello copia il contenuto e quindi incollarlo hello **i metadati del Provider di identità** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="35f1e-184">Open hello downloaded Federation Metadata from Azure AD in notepad, copy hello content, and then paste it into hello **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="35f1e-185">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="35f1e-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="35f1e-186">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="35f1e-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="35f1e-187">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="35f1e-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="35f1e-188">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="35f1e-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="35f1e-189">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="35f1e-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="35f1e-191">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="35f1e-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="35f1e-192">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="35f1e-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="35f1e-194">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="35f1e-196">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="35f1e-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="35f1e-198">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="35f1e-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="35f1e-200">a.</span><span class="sxs-lookup"><span data-stu-id="35f1e-200">a.</span></span> <span data-ttu-id="35f1e-201">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="35f1e-202">b.</span><span class="sxs-lookup"><span data-stu-id="35f1e-202">b.</span></span> <span data-ttu-id="35f1e-203">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="35f1e-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="35f1e-204">c.</span><span class="sxs-lookup"><span data-stu-id="35f1e-204">c.</span></span> <span data-ttu-id="35f1e-205">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="35f1e-206">d.</span><span class="sxs-lookup"><span data-stu-id="35f1e-206">d.</span></span> <span data-ttu-id="35f1e-207">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="35f1e-208">Creazione di un utente test di Expensify</span><span class="sxs-lookup"><span data-stu-id="35f1e-208">Creating an Expensify test user</span></span>

<span data-ttu-id="35f1e-209">In questa sezione viene creato un utente chiamato Britta Simon in Expensify.</span><span class="sxs-lookup"><span data-stu-id="35f1e-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="35f1e-210">Lavorare con [team di supporto Client Expensify](mailto:help@expensify.com) utenti hello tooadd nella piattaforma Expensify hello.</span><span class="sxs-lookup"><span data-stu-id="35f1e-210">Work with [Expensify Client support team](mailto:help@expensify.com) tooadd hello users in hello Expensify platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="35f1e-211">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="35f1e-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="35f1e-212">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooExpensify.</span><span class="sxs-lookup"><span data-stu-id="35f1e-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooExpensify.</span></span>

![Assegna utente][200] 

<span data-ttu-id="35f1e-214">**tooassign Britta Simon tooExpensify, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="35f1e-214">**tooassign Britta Simon tooExpensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="35f1e-215">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="35f1e-217">Nell'elenco di applicazioni hello, selezionare **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-217">In hello applications list, select **Expensify**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="35f1e-219">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="35f1e-221">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-221">Click **Add** button.</span></span> <span data-ttu-id="35f1e-222">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="35f1e-224">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="35f1e-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="35f1e-225">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="35f1e-226">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="35f1e-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="35f1e-227">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="35f1e-227">Testing single sign-on</span></span>

<span data-ttu-id="35f1e-228">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="35f1e-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="35f1e-229">Quando si fa clic su riquadro Expensify hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Expensify applicazione.</span><span class="sxs-lookup"><span data-stu-id="35f1e-229">When you click hello Expensify tile in hello Access Panel, you should get automatically signed-on tooyour Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="35f1e-230">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="35f1e-230">Additional resources</span></span>

* [<span data-ttu-id="35f1e-231">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35f1e-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35f1e-232">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35f1e-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

