---
title: 'Esercitazione: Integrazione di Azure Active Directory con 15Five | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e 15Five.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 9e531615c16331ce000e285d13d9adce13735a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="75871-103">Esercitazione: Integrazione di Azure Active Directory con 15Five</span><span class="sxs-lookup"><span data-stu-id="75871-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="75871-104">In questa esercitazione, è illustrato come toointegrate 15Five con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="75871-104">In this tutorial, you learn how toointegrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="75871-105">Integrazione di 15Five con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="75871-105">Integrating 15Five with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="75871-106">È possibile controllare in Azure AD che ha accesso too15Five</span><span class="sxs-lookup"><span data-stu-id="75871-106">You can control in Azure AD who has access too15Five</span></span>
- <span data-ttu-id="75871-107">È possibile abilitare il get tooautomatically utenti connesso too15Five (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="75871-107">You can enable your users tooautomatically get signed-on too15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="75871-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="75871-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="75871-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="75871-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75871-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="75871-110">Prerequisites</span></span>

<span data-ttu-id="75871-111">integrazione di Azure AD con 15Five tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="75871-111">tooconfigure Azure AD integration with 15Five, you need hello following items:</span></span>

- <span data-ttu-id="75871-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75871-112">An Azure AD subscription</span></span>
- <span data-ttu-id="75871-113">Sottoscrizione di 15Five abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="75871-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="75871-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="75871-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="75871-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="75871-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="75871-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="75871-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="75871-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75871-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="75871-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="75871-118">Scenario description</span></span>
<span data-ttu-id="75871-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="75871-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="75871-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="75871-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="75871-121">Aggiunta di 15Five dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="75871-121">Adding 15Five from hello gallery</span></span>
2. <span data-ttu-id="75871-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="75871-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-hello-gallery"></a><span data-ttu-id="75871-123">Aggiunta di 15Five dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="75871-123">Adding 15Five from hello gallery</span></span>
<span data-ttu-id="75871-124">integrazione hello tooconfigure di 15Five in Azure AD, è necessario 15Five tooadd dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="75871-124">tooconfigure hello integration of 15Five into Azure AD, you need tooadd 15Five from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="75871-125">**15Five tooadd dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="75871-125">**tooadd 15Five from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="75871-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="75871-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="75871-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="75871-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="75871-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="75871-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="75871-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="75871-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="75871-133">Nella casella di ricerca hello, digitare **15Five**.</span><span class="sxs-lookup"><span data-stu-id="75871-133">In hello search box, type **15Five**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="75871-135">Nel riquadro dei risultati hello, selezionare **15Five**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="75871-135">In hello results panel, select **15Five**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="75871-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="75871-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="75871-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con 15Five con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="75871-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="75871-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in 15Five è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75871-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 15Five is tooa user in Azure AD.</span></span> <span data-ttu-id="75871-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in 15Five deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="75871-140">In other words, a link relationship between an Azure AD user and hello related user in 15Five needs toobe established.</span></span>

<span data-ttu-id="75871-141">In 15Five, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="75871-141">In 15Five, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="75871-142">tooconfigure e prova AD Azure single sign-on con 15Five, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="75871-142">tooconfigure and test Azure AD single sign-on with 15Five, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="75871-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="75871-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="75871-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="75871-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="75871-145">**[Creazione di un utente test 15Five](#creating-a-15five-test-user)**  -toohave un equivalente di Britta Simon in 15Five che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="75871-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - toohave a counterpart of Britta Simon in 15Five that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="75871-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="75871-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="75871-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="75871-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="75871-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="75871-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="75871-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione 15Five.</span><span class="sxs-lookup"><span data-stu-id="75871-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="75871-150">**Azure AD tooconfigure single sign-on con 15Five, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="75871-150">**tooconfigure Azure AD single sign-on with 15Five, perform hello following steps:**</span></span>

1. <span data-ttu-id="75871-151">Nel portale di Azure su hello hello **15Five** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="75871-151">In hello Azure portal, on hello **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="75871-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="75871-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="75871-155">In hello **15Five dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="75871-155">On hello **15Five Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="75871-157">a.</span><span class="sxs-lookup"><span data-stu-id="75871-157">a.</span></span> <span data-ttu-id="75871-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.15five.com`</span><span class="sxs-lookup"><span data-stu-id="75871-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="75871-159">b.</span><span class="sxs-lookup"><span data-stu-id="75871-159">b.</span></span> <span data-ttu-id="75871-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="75871-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="75871-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="75871-161">These values are not real.</span></span> <span data-ttu-id="75871-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="75871-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="75871-163">Contatto [team di supporto di 15Five Client](https://www.15five.com/contact/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="75871-163">Contact [15Five Client support team](https://www.15five.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="75871-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="75871-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="75871-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="75871-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="75871-168">tooconfigure single sign-on sul **15Five** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto di 15Five](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="75871-168">tooconfigure single sign-on on **15Five** side, you need toosend hello downloaded **Metadata XML** too[15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="75871-169">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="75871-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="75871-170">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="75871-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="75871-171">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="75871-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="75871-172">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="75871-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="75871-173">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="75871-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="75871-175">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="75871-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="75871-176">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="75871-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="75871-178">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="75871-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="75871-180">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="75871-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="75871-182">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="75871-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="75871-184">a.</span><span class="sxs-lookup"><span data-stu-id="75871-184">a.</span></span> <span data-ttu-id="75871-185">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="75871-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="75871-186">b.</span><span class="sxs-lookup"><span data-stu-id="75871-186">b.</span></span> <span data-ttu-id="75871-187">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="75871-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="75871-188">c.</span><span class="sxs-lookup"><span data-stu-id="75871-188">c.</span></span> <span data-ttu-id="75871-189">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="75871-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="75871-190">d.</span><span class="sxs-lookup"><span data-stu-id="75871-190">d.</span></span> <span data-ttu-id="75871-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="75871-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="75871-192">Creazione di un utente di test di 15Five</span><span class="sxs-lookup"><span data-stu-id="75871-192">Creating a 15Five test user</span></span>

<span data-ttu-id="75871-193">toolog agli utenti di Azure AD tooenable in too15Five, è necessario eseguirne il provisioning in 15Five.</span><span class="sxs-lookup"><span data-stu-id="75871-193">tooenable Azure AD users toolog in too15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="75871-194">Nel caso di 15Five, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="75871-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="75871-195">tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="75871-195">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="75871-196">Accedi tooyour **15Five** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="75871-196">Log in tooyour **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="75871-197">Andare troppo**Gestisci società**.</span><span class="sxs-lookup"><span data-stu-id="75871-197">Go too**Manage Company**.</span></span>
   
    <span data-ttu-id="75871-198">![Gestire una società](./media/active-directory-saas-15five-tutorial/IC784675.png "Gestire una società")</span><span class="sxs-lookup"><span data-stu-id="75871-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="75871-199">Andare troppo**persone \> aggiungere utenti**.</span><span class="sxs-lookup"><span data-stu-id="75871-199">Go too**People \> Add People**.</span></span>
   
    <span data-ttu-id="75871-200">![Persone](./media/active-directory-saas-15five-tutorial/IC784676.png "Persone")</span><span class="sxs-lookup"><span data-stu-id="75871-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="75871-201">Nella sezione Add New Person hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="75871-201">In hello Add New Person section, perform hello following steps:</span></span>
   
    <span data-ttu-id="75871-202">![Aggiungere una nuova persona](./media/active-directory-saas-15five-tutorial/IC784677.png "Aggiungere una nuova persona")</span><span class="sxs-lookup"><span data-stu-id="75871-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="75871-203">a.</span><span class="sxs-lookup"><span data-stu-id="75871-203">a.</span></span> <span data-ttu-id="75871-204">Hello tipo **nome**, **cognome**, **titolo**, **indirizzo di posta elettronica** di un account Azure Active Directory valido, si desidera tooprovision in Hello relative caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="75871-204">Type hello **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="75871-205">b.</span><span class="sxs-lookup"><span data-stu-id="75871-205">b.</span></span> <span data-ttu-id="75871-206">Fare clic su **Done**.</span><span class="sxs-lookup"><span data-stu-id="75871-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="75871-207">Hello account Azure AD titolare riceve un messaggio di posta elettronica tra un account di hello tooconfirm collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="75871-207">hello Azure AD account holder receives an email including a link tooconfirm hello account before it becomes active.</span></span>
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="75871-208">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="75871-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="75871-209">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso too15Five.</span><span class="sxs-lookup"><span data-stu-id="75871-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too15Five.</span></span>

![Assegna utente][200] 

<span data-ttu-id="75871-211">**tooassign Britta Simon too15Five, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="75871-211">**tooassign Britta Simon too15Five, perform hello following steps:**</span></span>

1. <span data-ttu-id="75871-212">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="75871-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="75871-214">Nell'elenco di applicazioni hello, selezionare **15Five**.</span><span class="sxs-lookup"><span data-stu-id="75871-214">In hello applications list, select **15Five**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="75871-216">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="75871-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="75871-218">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="75871-218">Click **Add** button.</span></span> <span data-ttu-id="75871-219">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="75871-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="75871-221">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="75871-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="75871-222">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="75871-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="75871-223">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="75871-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="75871-224">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="75871-224">Testing single sign-on</span></span>

<span data-ttu-id="75871-225">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="75871-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="75871-226">Quando si fa clic su riquadro 15Five hello in hello Pannello di accesso, è necessario ottenere la pagina di accesso dell'applicazione di 15Five.</span><span class="sxs-lookup"><span data-stu-id="75871-226">When you click hello 15Five tile in hello Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="75871-227">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="75871-227">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="75871-228">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="75871-228">Additional resources</span></span>

* [<span data-ttu-id="75871-229">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="75871-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="75871-230">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="75871-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

