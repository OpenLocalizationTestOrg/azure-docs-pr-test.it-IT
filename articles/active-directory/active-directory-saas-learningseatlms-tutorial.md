---
title: 'Esercitazione: Integrazione di Azure Active Directory con Learning Seat LMS | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e l'apprendimento postazione LMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: dc08aa444b85f35a4458768ac560ec663baa1c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="38f6d-103">Esercitazione: Integrazione di Azure Active Directory con Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="38f6d-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="38f6d-104">In questa esercitazione, è illustrato come toointegrate Learning postazione LMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="38f6d-104">In this tutorial, you learn how toointegrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38f6d-105">Integrazione di apprendimento postazione LMS con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="38f6d-105">Integrating Learning Seat LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="38f6d-106">È possibile controllare in Azure AD che ha accesso tooLearning LMS postazione</span><span class="sxs-lookup"><span data-stu-id="38f6d-106">You can control in Azure AD who has access tooLearning Seat LMS</span></span>
- <span data-ttu-id="38f6d-107">È possibile abilitare l'utenti tooautomatically get connesso tooLearning postazione LMS (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="38f6d-107">You can enable your users tooautomatically get signed-on tooLearning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="38f6d-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="38f6d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="38f6d-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere.</span><span class="sxs-lookup"><span data-stu-id="38f6d-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="38f6d-110">[Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="38f6d-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38f6d-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="38f6d-111">Prerequisites</span></span>

<span data-ttu-id="38f6d-112">integrazione di Azure AD con Learning postazione LMS tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="38f6d-112">tooconfigure Azure AD integration with Learning Seat LMS, you need hello following items:</span></span>

- <span data-ttu-id="38f6d-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38f6d-113">An Azure AD subscription</span></span>
- <span data-ttu-id="38f6d-114">Sottoscrizione di Learning Seat LMS abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="38f6d-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="38f6d-115">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="38f6d-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="38f6d-116">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="38f6d-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38f6d-117">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="38f6d-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="38f6d-118">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38f6d-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38f6d-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="38f6d-119">Scenario description</span></span>
<span data-ttu-id="38f6d-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="38f6d-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38f6d-121">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="38f6d-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38f6d-122">Aggiunta di apprendimento postazione LMS dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="38f6d-122">Adding Learning Seat LMS from hello gallery</span></span>
2. <span data-ttu-id="38f6d-123">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="38f6d-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-hello-gallery"></a><span data-ttu-id="38f6d-124">Aggiunta di apprendimento postazione LMS dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="38f6d-124">Adding Learning Seat LMS from hello gallery</span></span>
<span data-ttu-id="38f6d-125">integrazione hello tooconfigure di LMS postazione di apprendimento in Azure AD, è necessario tooadd Learning postazione LMS dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="38f6d-125">tooconfigure hello integration of Learning Seat LMS into Azure AD, you need tooadd Learning Seat LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="38f6d-126">**tooadd Learning postazione LMS dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="38f6d-126">**tooadd Learning Seat LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="38f6d-127">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="38f6d-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="38f6d-129">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="38f6d-130">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-130">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="38f6d-132">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="38f6d-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="38f6d-134">Nella casella di ricerca hello, digitare **Learning postazione LMS**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-134">In hello search box, type **Learning Seat LMS**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. <span data-ttu-id="38f6d-136">Nel riquadro dei risultati hello, selezionare **Learning postazione LMS**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="38f6d-136">In hello results panel, select **Learning Seat LMS**, and then click **Add** button tooadd hello application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38f6d-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="38f6d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38f6d-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Learning Seat LMS usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="38f6d-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="38f6d-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Learning postazione LMS è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38f6d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learning Seat LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="38f6d-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e utente correlati hello Learning postazione LMS deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="38f6d-140">In other words, a link relationship between an Azure AD user and hello related user in Learning Seat LMS needs toobe established.</span></span>

<span data-ttu-id="38f6d-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nell'apprendimento postazione LMS.</span><span class="sxs-lookup"><span data-stu-id="38f6d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="38f6d-142">tooconfigure e prova AD Azure single sign-on con Learning postazione LMS, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="38f6d-142">tooconfigure and test Azure AD single sign-on with Learning Seat LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="38f6d-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="38f6d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="38f6d-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="38f6d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38f6d-145">**[Creazione di un utente test Learning postazione LMS](#creating-a-learnconnect-test-user)**  -toohave un equivalente di Britta Simon in LMS postazione di apprendimento che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="38f6d-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - toohave a counterpart of Britta Simon in Learning Seat LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="38f6d-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="38f6d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38f6d-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="38f6d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="38f6d-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="38f6d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="38f6d-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Learning postazione LMS.</span><span class="sxs-lookup"><span data-stu-id="38f6d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="38f6d-150">**tooconfigure AD Azure single sign-on con Learning postazione LMS, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="38f6d-150">**tooconfigure Azure AD single sign-on with Learning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="38f6d-151">Nel portale di Azure su hello hello **Learning postazione LMS** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-151">In hello Azure portal, on hello **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="38f6d-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="38f6d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. <span data-ttu-id="38f6d-155">In hello **Learning postazione LMS dominio e gli URL** seguire hello procedura seguente se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="38f6d-155">On hello **Learning Seat LMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="38f6d-157">a.</span><span class="sxs-lookup"><span data-stu-id="38f6d-157">a.</span></span> <span data-ttu-id="38f6d-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="38f6d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="38f6d-159">b.</span><span class="sxs-lookup"><span data-stu-id="38f6d-159">b.</span></span> <span data-ttu-id="38f6d-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="38f6d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

4. <span data-ttu-id="38f6d-161">Controllare **Mostra URL impostazioni avanzate**, se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="38f6d-161">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="38f6d-163">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="38f6d-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="38f6d-164">Questi valori non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="38f6d-164">These values are not hello real values.</span></span> <span data-ttu-id="38f6d-165">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="38f6d-165">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="38f6d-166">Contatto [team di supporto di apprendimento postazione](http://help.learningseatlms.com/help) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="38f6d-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) tooget these values.</span></span> 

5. <span data-ttu-id="38f6d-167">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="38f6d-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. <span data-ttu-id="38f6d-169">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="38f6d-169">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="38f6d-171">tooconfigure single sign-on sul **Learning postazione LMS** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto di apprendimento postazione](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="38f6d-171">tooconfigure single sign-on on **Learning Seat LMS** side, you need toosend hello downloaded **Metadata XML** too[Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="38f6d-172">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="38f6d-172">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="38f6d-173">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="38f6d-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="38f6d-174">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="38f6d-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38f6d-175">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="38f6d-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="38f6d-176">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="38f6d-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="38f6d-178">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="38f6d-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="38f6d-179">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="38f6d-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="38f6d-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="38f6d-183">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="38f6d-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38f6d-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="38f6d-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="38f6d-187">a.</span><span class="sxs-lookup"><span data-stu-id="38f6d-187">a.</span></span> <span data-ttu-id="38f6d-188">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38f6d-189">b.</span><span class="sxs-lookup"><span data-stu-id="38f6d-189">b.</span></span> <span data-ttu-id="38f6d-190">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="38f6d-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="38f6d-191">c.</span><span class="sxs-lookup"><span data-stu-id="38f6d-191">c.</span></span> <span data-ttu-id="38f6d-192">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="38f6d-193">d.</span><span class="sxs-lookup"><span data-stu-id="38f6d-193">d.</span></span> <span data-ttu-id="38f6d-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="38f6d-195">Creazione di un utente di test di Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="38f6d-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="38f6d-196">In questa sezione viene creato un utente di nome Britta Simon in Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="38f6d-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="38f6d-197">Contatto [team di supporto di apprendimento postazione](http://help.learningseatlms.com/help) con tutti hello utente informazioni tooadd hello gli utenti nell'applicazione di apprendimento postazione LMS hello.</span><span class="sxs-lookup"><span data-stu-id="38f6d-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all hello user information tooadd hello users in hello Learning Seat LMS application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="38f6d-198">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="38f6d-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="38f6d-199">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLearning LMS postazione.</span><span class="sxs-lookup"><span data-stu-id="38f6d-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearning Seat LMS.</span></span>

![Assegna utente][200] 

<span data-ttu-id="38f6d-201">**tooassign Britta Simon tooLearning LMS postazioni, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="38f6d-201">**tooassign Britta Simon tooLearning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="38f6d-202">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="38f6d-204">Nell'elenco di applicazioni hello, selezionare **Learning postazione LMS**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-204">In hello applications list, select **Learning Seat LMS**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. <span data-ttu-id="38f6d-206">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="38f6d-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-208">Click **Add** button.</span></span> <span data-ttu-id="38f6d-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="38f6d-211">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="38f6d-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="38f6d-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38f6d-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="38f6d-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="38f6d-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="38f6d-214">Testing single sign-on</span></span>

<span data-ttu-id="38f6d-215">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="38f6d-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> 

<span data-ttu-id="38f6d-216">Fare clic su hello Learning postazione LMS riquadro nel Pannello di accesso, hello sarà applicazione Learning postazione LMS tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="38f6d-216">Click hello Learning Seat LMS tile in hello Access Panel, you will be automatically signed-on tooyour Learning Seat LMS application.</span></span> <span data-ttu-id="38f6d-217">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="38f6d-217">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="38f6d-218">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="38f6d-218">Additional resources</span></span>

* [<span data-ttu-id="38f6d-219">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38f6d-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38f6d-220">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38f6d-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png

