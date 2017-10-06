---
title: 'Esercitazione: Integrazione di Azure Active Directory con Blackboard Learn - Shibboleth | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e informazioni di lavagna - Shibboleth.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 40aa3ec5f42b93157af3c56daaadfa66203b21d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="737e1-103">Esercitazione: Integrazione di Azure Active Directory con Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="737e1-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>

<span data-ttu-id="737e1-104">In questa esercitazione, è illustrato come toointegrate Lavagna informazioni - Shibboleth con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="737e1-104">In this tutorial, you learn how toointegrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="737e1-105">L'integrazione delle informazioni di lavagna - Shibboleth con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="737e1-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="737e1-106">È possibile controllare in Azure AD che ha accesso tooBlackboard informazioni - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="737e1-106">You can control in Azure AD who has access tooBlackboard Learn - Shibboleth</span></span>
- <span data-ttu-id="737e1-107">È possibile abilitare l'utenti tooautomatically get connesso tooBlackboard informazioni - Shibboleth (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="737e1-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="737e1-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="737e1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="737e1-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="737e1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="737e1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="737e1-110">Prerequisites</span></span>

<span data-ttu-id="737e1-111">tooconfigure integrazione di Azure AD con informazioni Lavagna - Shibboleth, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="737e1-111">tooconfigure Azure AD integration with Blackboard Learn - Shibboleth, you need hello following items:</span></span>

- <span data-ttu-id="737e1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="737e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="737e1-113">Una sottoscrizione abilitata all'accesso Single Sign-On di Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="737e1-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="737e1-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="737e1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="737e1-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="737e1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="737e1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="737e1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="737e1-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="737e1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="737e1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="737e1-118">Scenario description</span></span>
<span data-ttu-id="737e1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="737e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="737e1-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="737e1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="737e1-121">Aggiunta di informazioni di lavagna - Shibboleth dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="737e1-121">Adding Blackboard Learn - Shibboleth from hello gallery</span></span>
2. <span data-ttu-id="737e1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="737e1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-hello-gallery"></a><span data-ttu-id="737e1-123">Aggiunta di informazioni di lavagna - Shibboleth dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="737e1-123">Adding Blackboard Learn - Shibboleth from hello gallery</span></span>
<span data-ttu-id="737e1-124">integrazione di hello tooconfigure di lavagna informazioni - Shibboleth in Azure AD, è necessario tooadd Lavagna informazioni - Shibboleth dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="737e1-124">tooconfigure hello integration of Blackboard Learn - Shibboleth into Azure AD, you need tooadd Blackboard Learn - Shibboleth from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="737e1-125">**informazioni su Lavagna - tooadd Shibboleth dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="737e1-125">**tooadd Blackboard Learn - Shibboleth from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="737e1-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="737e1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="737e1-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="737e1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="737e1-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="737e1-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="737e1-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="737e1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="737e1-133">Nella casella di ricerca hello, digitare **Lavagna informazioni - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="737e1-133">In hello search box, type **Blackboard Learn - Shibboleth**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

5. <span data-ttu-id="737e1-135">Nel riquadro dei risultati hello, selezionare **Lavagna informazioni - Shibboleth**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="737e1-135">In hello results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="737e1-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="737e1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="737e1-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Blackboard Learn - Shibboleth usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="737e1-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="737e1-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nella Lavagna informazioni - Shibboleth è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="737e1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn - Shibboleth is tooa user in Azure AD.</span></span> <span data-ttu-id="737e1-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato hello Lavagna informazioni - Shibboleth deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="737e1-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn - Shibboleth needs toobe established.</span></span>

<span data-ttu-id="737e1-141">In informazioni Lavagna - Shibboleth, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="737e1-141">In Blackboard Learn - Shibboleth, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="737e1-142">tooconfigure e prova AD Azure single sign-on con informazioni Lavagna - Shibboleth, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="737e1-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="737e1-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="737e1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="737e1-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="737e1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="737e1-145">**[Creazione di una lavagna informazioni - utente test Shibboleth](#creating-a-blackboard-learn---shibboleth-test-user)**  - toohave un equivalente di Britta Simon nella Lavagna informazioni - Shibboleth che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="737e1-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="737e1-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="737e1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="737e1-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="737e1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="737e1-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="737e1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="737e1-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nella Lavagna informazioni - applicazione di Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="737e1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="737e1-150">**Azure AD tooconfigure single sign-on con informazioni Lavagna - Shibboleth, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="737e1-150">**tooconfigure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform hello following steps:**</span></span>

1. <span data-ttu-id="737e1-151">Nel portale di Azure su hello hello **Lavagna informazioni - Shibboleth** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="737e1-151">In hello Azure portal, on hello **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="737e1-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="737e1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

3. <span data-ttu-id="737e1-155">In hello **Lavagna informazioni - URL e il dominio di Shibboleth** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="737e1-155">On hello **Blackboard Learn - Shibboleth Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    <span data-ttu-id="737e1-157">a.</span><span class="sxs-lookup"><span data-stu-id="737e1-157">a.</span></span> <span data-ttu-id="737e1-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span><span class="sxs-lookup"><span data-stu-id="737e1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span></span>

    <span data-ttu-id="737e1-159">b.</span><span class="sxs-lookup"><span data-stu-id="737e1-159">b.</span></span> <span data-ttu-id="737e1-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span><span class="sxs-lookup"><span data-stu-id="737e1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span></span>

    <span data-ttu-id="737e1-161">c.</span><span class="sxs-lookup"><span data-stu-id="737e1-161">c.</span></span> <span data-ttu-id="737e1-162">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span><span class="sxs-lookup"><span data-stu-id="737e1-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="737e1-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="737e1-163">These values are not real.</span></span> <span data-ttu-id="737e1-164">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="737e1-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="737e1-165">Contatto [Lavagna informazioni - team di supporto Client di Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="737e1-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="737e1-166">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="737e1-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

5. <span data-ttu-id="737e1-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="737e1-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="737e1-170">In hello **Lavagna informazioni - configurazione di Shibboleth** fare clic su **configurare informazioni Lavagna - Shibboleth** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="737e1-170">On hello **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="737e1-171">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="737e1-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

7. <span data-ttu-id="737e1-173">tooconfigure single sign-on sul **Lavagna informazioni - Shibboleth** lato, è necessario hello toosend scaricato **Metadata XML** e **Sign-Out URL, l'ID entità SAML e servizio SAML Single Sign-On URL** troppo[Lavagna informazioni - team di supporto di Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="737e1-173">tooconfigure single sign-on on **Blackboard Learn - Shibboleth** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="737e1-174">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="737e1-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="737e1-175">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="737e1-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="737e1-176">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="737e1-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="737e1-177">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="737e1-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="737e1-178">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="737e1-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="737e1-180">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="737e1-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="737e1-181">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="737e1-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="737e1-183">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="737e1-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="737e1-185">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="737e1-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="737e1-187">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="737e1-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="737e1-189">a.</span><span class="sxs-lookup"><span data-stu-id="737e1-189">a.</span></span> <span data-ttu-id="737e1-190">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="737e1-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="737e1-191">b.</span><span class="sxs-lookup"><span data-stu-id="737e1-191">b.</span></span> <span data-ttu-id="737e1-192">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="737e1-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="737e1-193">c.</span><span class="sxs-lookup"><span data-stu-id="737e1-193">c.</span></span> <span data-ttu-id="737e1-194">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="737e1-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="737e1-195">d.</span><span class="sxs-lookup"><span data-stu-id="737e1-195">d.</span></span> <span data-ttu-id="737e1-196">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="737e1-196">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="737e1-197">Creazione di un utente di test di Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="737e1-197">Creating a Blackboard Learn - Shibboleth test user</span></span>

<span data-ttu-id="737e1-198">In questa sezione viene creato un utente di nome Britta Simon in Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="737e1-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="737e1-199">Utilizzare il [Lavagna informazioni - team di supporto di Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) tooadd utenti hello hello Lavagna informazioni - piattaforma Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="737e1-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) tooadd hello users in hello Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="737e1-200">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="737e1-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="737e1-201">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBlackboard informazioni - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="737e1-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn - Shibboleth.</span></span>

![Assegna utente][200] 

<span data-ttu-id="737e1-203">**tooassign Britta Simon tooBlackboard informazioni - Shibboleth, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="737e1-203">**tooassign Britta Simon tooBlackboard Learn - Shibboleth, perform hello following steps:**</span></span>

1. <span data-ttu-id="737e1-204">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="737e1-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="737e1-206">Nell'elenco di applicazioni hello, selezionare **Lavagna informazioni - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="737e1-206">In hello applications list, select **Blackboard Learn - Shibboleth**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

3. <span data-ttu-id="737e1-208">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="737e1-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="737e1-210">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="737e1-210">Click **Add** button.</span></span> <span data-ttu-id="737e1-211">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="737e1-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="737e1-213">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="737e1-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="737e1-214">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="737e1-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="737e1-215">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="737e1-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="737e1-216">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="737e1-216">Testing single sign-on</span></span>

<span data-ttu-id="737e1-217">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="737e1-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="737e1-218">Quando si fa clic hello Lavagna informazioni - riquadro Shibboleth in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Lavagna informazioni - applicazione di Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="737e1-218">When you click hello Blackboard Learn - Shibboleth tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="737e1-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="737e1-219">Additional resources</span></span>

* [<span data-ttu-id="737e1-220">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="737e1-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="737e1-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="737e1-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png

