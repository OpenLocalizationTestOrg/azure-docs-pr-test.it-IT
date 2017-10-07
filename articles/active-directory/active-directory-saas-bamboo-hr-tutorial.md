---
title: 'Esercitazione: Integrazione di Azure Active Directory con BambooHR | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e BambooHR.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: f9083f846beb3a4bf4cebbf18b42aba2dfef2472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="f629c-103">Esercitazione: Integrazione di Azure Active Directory con BambooHR</span><span class="sxs-lookup"><span data-stu-id="f629c-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="f629c-104">In questa esercitazione, è illustrato come toointegrate BambooHR con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f629c-104">In this tutorial, you learn how toointegrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f629c-105">Integrazione di BambooHR con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="f629c-105">Integrating BambooHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f629c-106">È possibile controllare in Azure AD che ha accesso tooBambooHR</span><span class="sxs-lookup"><span data-stu-id="f629c-106">You can control in Azure AD who has access tooBambooHR</span></span>
- <span data-ttu-id="f629c-107">È possibile abilitare l'utenti tooautomatically get connesso tooBambooHR (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="f629c-107">You can enable your users tooautomatically get signed-on tooBambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f629c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f629c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f629c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f629c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f629c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f629c-110">Prerequisites</span></span>

<span data-ttu-id="f629c-111">integrazione di Azure AD con BambooHR tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="f629c-111">tooconfigure Azure AD integration with BambooHR, you need hello following items:</span></span>

- <span data-ttu-id="f629c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f629c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f629c-113">Sottoscrizione di BambooHR abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f629c-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f629c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="f629c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f629c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="f629c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f629c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="f629c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f629c-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f629c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f629c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="f629c-118">Scenario description</span></span>
<span data-ttu-id="f629c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="f629c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f629c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="f629c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f629c-121">Aggiunta di BambooHR dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f629c-121">Adding BambooHR from hello gallery</span></span>
2. <span data-ttu-id="f629c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f629c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-hello-gallery"></a><span data-ttu-id="f629c-123">Aggiunta di BambooHR dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="f629c-123">Adding BambooHR from hello gallery</span></span>
<span data-ttu-id="f629c-124">integrazione hello tooconfigure di BambooHR in Azure AD, è necessario tooadd BambooHR dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="f629c-124">tooconfigure hello integration of BambooHR into Azure AD, you need tooadd BambooHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f629c-125">**tooadd BambooHR dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f629c-125">**tooadd BambooHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f629c-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f629c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f629c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="f629c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f629c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f629c-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="f629c-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="f629c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="f629c-133">Nella casella di ricerca hello, digitare **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="f629c-133">In hello search box, type **BambooHR**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="f629c-135">Nel riquadro dei risultati hello, selezionare **BambooHR**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f629c-135">In hello results panel, select **BambooHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f629c-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f629c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f629c-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con BambooHR usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f629c-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f629c-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in BambooHR è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f629c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BambooHR is tooa user in Azure AD.</span></span> <span data-ttu-id="f629c-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in BambooHR deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="f629c-140">In other words, a link relationship between an Azure AD user and hello related user in BambooHR needs toobe established.</span></span>

<span data-ttu-id="f629c-141">In BambooHR, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="f629c-141">In BambooHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f629c-142">tooconfigure e prova AD Azure single sign-on con BambooHR, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f629c-142">tooconfigure and test Azure AD single sign-on with BambooHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f629c-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="f629c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f629c-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f629c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f629c-145">**[Creazione di un utente test BambooHR](#creating-a-bamboohr-test-user)**  -toohave un equivalente di Britta Simon in BambooHR che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f629c-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - toohave a counterpart of Britta Simon in BambooHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f629c-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f629c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f629c-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="f629c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f629c-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f629c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f629c-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione BambooHR.</span><span class="sxs-lookup"><span data-stu-id="f629c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="f629c-150">**Azure AD tooconfigure single sign-on con BambooHR, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f629c-150">**tooconfigure Azure AD single sign-on with BambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="f629c-151">Nel portale di Azure su hello hello **BambooHR** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f629c-151">In hello Azure portal, on hello **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="f629c-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f629c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="f629c-155">In hello **BambooHR dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f629c-155">On hello **BambooHR Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="f629c-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="f629c-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="f629c-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="f629c-158">This value is not real.</span></span> <span data-ttu-id="f629c-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="f629c-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="f629c-160">Contatto [team di supporto Client di BambooHR](https://www.bamboohr.com/contact.php) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="f629c-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) tooget this value.</span></span> 
 
4. <span data-ttu-id="f629c-161">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f629c-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="f629c-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="f629c-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f629c-165">In hello **BambooHR configurazione** fare clic su **configurare BambooHR** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="f629c-165">On hello **BambooHR Configuration** section, click **Configure BambooHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f629c-166">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="f629c-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="f629c-168">In un'altra finestra del Web browser accedere al sito aziendale di BambooHR come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f629c-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="f629c-169">Nella home page di hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f629c-169">On hello homepage, perform hello following steps:</span></span>
   
    <span data-ttu-id="f629c-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="f629c-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="f629c-171">a.</span><span class="sxs-lookup"><span data-stu-id="f629c-171">a.</span></span> <span data-ttu-id="f629c-172">Fare clic su **App**.</span><span class="sxs-lookup"><span data-stu-id="f629c-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="f629c-173">b.</span><span class="sxs-lookup"><span data-stu-id="f629c-173">b.</span></span> <span data-ttu-id="f629c-174">Hello App dal menu a sinistra di hello, fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f629c-174">In hello apps menu on hello left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="f629c-175">c.</span><span class="sxs-lookup"><span data-stu-id="f629c-175">c.</span></span> <span data-ttu-id="f629c-176">Fare clic su **SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f629c-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="f629c-177">In hello **SAML Single Sign-On** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f629c-177">In hello **SAML Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f629c-178">![Single Sign-On SAML](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "Single Sign-On SAML")</span><span class="sxs-lookup"><span data-stu-id="f629c-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="f629c-179">a.</span><span class="sxs-lookup"><span data-stu-id="f629c-179">a.</span></span> <span data-ttu-id="f629c-180">Hello Incolla **SAML Single Sign-On Service URL** valore in hello **Url di accesso SSO** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="f629c-180">Paste hello **SAML Single Sign-On Service URL** value into hello **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="f629c-181">b.</span><span class="sxs-lookup"><span data-stu-id="f629c-181">b.</span></span> <span data-ttu-id="f629c-182">Aprire il certificato con codificato base 64 scaricato dal portale di Azure nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato x. 509** casella di testo</span><span class="sxs-lookup"><span data-stu-id="f629c-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="f629c-183">c.</span><span class="sxs-lookup"><span data-stu-id="f629c-183">c.</span></span> <span data-ttu-id="f629c-184">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f629c-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f629c-185">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="f629c-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f629c-186">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="f629c-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f629c-187">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f629c-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f629c-188">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="f629c-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="f629c-189">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f629c-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="f629c-191">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f629c-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f629c-192">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="f629c-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f629c-194">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f629c-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f629c-196">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="f629c-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f629c-198">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="f629c-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f629c-200">a.</span><span class="sxs-lookup"><span data-stu-id="f629c-200">a.</span></span> <span data-ttu-id="f629c-201">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f629c-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f629c-202">b.</span><span class="sxs-lookup"><span data-stu-id="f629c-202">b.</span></span> <span data-ttu-id="f629c-203">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f629c-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f629c-204">c.</span><span class="sxs-lookup"><span data-stu-id="f629c-204">c.</span></span> <span data-ttu-id="f629c-205">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="f629c-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f629c-206">d.</span><span class="sxs-lookup"><span data-stu-id="f629c-206">d.</span></span> <span data-ttu-id="f629c-207">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f629c-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="f629c-208">Creazione di un utente di test di BambooHR</span><span class="sxs-lookup"><span data-stu-id="f629c-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="f629c-209">toolog agli utenti di Azure AD tooenable in tooBambooHR, è necessario eseguirne il provisioning in BambooHR.</span><span class="sxs-lookup"><span data-stu-id="f629c-209">tooenable Azure AD users toolog in tooBambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="f629c-210">Nel caso di hello di BambooHR, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="f629c-210">In hello case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="f629c-211">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f629c-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="f629c-212">Accedi tooyour **BambooHR** sito come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f629c-212">Log in tooyour **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="f629c-213">Nella barra degli strumenti hello in primo piano hello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="f629c-213">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="f629c-214">![Impostazione](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Impostazione")</span><span class="sxs-lookup"><span data-stu-id="f629c-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="f629c-215">Fare clic su **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="f629c-215">Click **Overview**.</span></span>

4. <span data-ttu-id="f629c-216">Nel riquadro di spostamento a sinistra di hello, andare troppo**sicurezza \> utenti**.</span><span class="sxs-lookup"><span data-stu-id="f629c-216">In hello left navigation pane, go too**Security \> Users**.</span></span>

5. <span data-ttu-id="f629c-217">Digitare il nome utente hello, password e indirizzo di posta elettronica di un account aAd di cui che si desidera tooprovision in hello correlati nelle caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="f629c-217">Type hello user name, password, and email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

6. <span data-ttu-id="f629c-218">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f629c-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="f629c-219">È possibile usare qualsiasi altro BambooHR utente account strumento di creazione o le API fornite da BambooHR tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="f629c-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f629c-220">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f629c-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f629c-221">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBambooHR.</span><span class="sxs-lookup"><span data-stu-id="f629c-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBambooHR.</span></span>

![Assegna utente][200] 

<span data-ttu-id="f629c-223">**tooassign Britta Simon tooBambooHR, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="f629c-223">**tooassign Britta Simon tooBambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="f629c-224">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="f629c-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="f629c-226">Nell'elenco di applicazioni hello, selezionare **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="f629c-226">In hello applications list, select **BambooHR**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="f629c-228">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f629c-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="f629c-230">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f629c-230">Click **Add** button.</span></span> <span data-ttu-id="f629c-231">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f629c-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="f629c-233">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="f629c-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f629c-234">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="f629c-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f629c-235">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="f629c-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f629c-236">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f629c-236">Testing single sign-on</span></span>

<span data-ttu-id="f629c-237">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="f629c-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f629c-238">Quando si fa clic su riquadro BambooHR hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in BambooHR applicazione.</span><span class="sxs-lookup"><span data-stu-id="f629c-238">When you click hello BambooHR tile in hello Access Panel, you should get automatically signed-on tooyour BambooHR application.</span></span>
<span data-ttu-id="f629c-239">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f629c-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f629c-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="f629c-240">Additional resources</span></span>

* [<span data-ttu-id="f629c-241">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f629c-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f629c-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f629c-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png

