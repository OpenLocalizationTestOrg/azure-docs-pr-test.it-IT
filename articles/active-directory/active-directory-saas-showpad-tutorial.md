---
title: 'Esercitazione: Integrazione di Azure Active Directory con Showpad | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Showpad.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2c8c306b4b94c368a93f92123d3abe9fe35167db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="2d709-103">Esercitazione: Integrazione di Azure Active Directory con Showpad</span><span class="sxs-lookup"><span data-stu-id="2d709-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="2d709-104">In questa esercitazione, è illustrato come toointegrate Showpad con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2d709-104">In this tutorial, you learn how toointegrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2d709-105">Integrazione Showpad con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="2d709-105">Integrating Showpad with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2d709-106">È possibile controllare in Azure AD che ha accesso tooShowpad</span><span class="sxs-lookup"><span data-stu-id="2d709-106">You can control in Azure AD who has access tooShowpad</span></span>
- <span data-ttu-id="2d709-107">È possibile abilitare l'utenti tooautomatically get connesso tooShowpad (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d709-107">You can enable your users tooautomatically get signed-on tooShowpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2d709-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2d709-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2d709-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2d709-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d709-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2d709-110">Prerequisites</span></span>

<span data-ttu-id="2d709-111">integrazione di Azure AD con Showpad tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="2d709-111">tooconfigure Azure AD integration with Showpad, you need hello following items:</span></span>

- <span data-ttu-id="2d709-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d709-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2d709-113">Sottoscrizione Showpad abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2d709-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2d709-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="2d709-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2d709-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="2d709-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2d709-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2d709-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2d709-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d709-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2d709-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2d709-118">Scenario description</span></span>
<span data-ttu-id="2d709-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2d709-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2d709-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="2d709-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d709-121">Aggiunta di Showpad dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="2d709-121">Adding Showpad from hello gallery</span></span>
2. <span data-ttu-id="2d709-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d709-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-hello-gallery"></a><span data-ttu-id="2d709-123">Aggiunta di Showpad dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="2d709-123">Adding Showpad from hello gallery</span></span>

<span data-ttu-id="2d709-124">integrazione hello tooconfigure di Showpad in Azure AD, è necessario tooadd Showpad dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2d709-124">tooconfigure hello integration of Showpad into Azure AD, you need tooadd Showpad from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2d709-125">**tooadd Showpad dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2d709-125">**tooadd Showpad from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d709-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="2d709-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2d709-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="2d709-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2d709-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2d709-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="2d709-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2d709-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="2d709-133">Nella casella di ricerca hello, digitare **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="2d709-133">In hello search box, type **Showpad**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_search.png)

5. <span data-ttu-id="2d709-135">Nel riquadro dei risultati hello, selezionare **Showpad**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2d709-135">In hello results panel, select **Showpad**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2d709-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d709-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="2d709-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Showpad in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2d709-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2d709-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Showpad è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d709-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Showpad is tooa user in Azure AD.</span></span> <span data-ttu-id="2d709-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Showpad deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="2d709-140">In other words, a link relationship between an Azure AD user and hello related user in Showpad needs toobe established.</span></span>

<span data-ttu-id="2d709-141">In Showpad, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="2d709-141">In Showpad, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2d709-142">tooconfigure e prova AD Azure single sign-on con Showpad, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="2d709-142">tooconfigure and test Azure AD single sign-on with Showpad, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2d709-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2d709-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2d709-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d709-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2d709-145">**[Creazione di un utente test Showpad](#creating-a-showpad-test-user)**  -toohave un equivalente di Britta Simon in Showpad che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2d709-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - toohave a counterpart of Britta Simon in Showpad that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2d709-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2d709-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2d709-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="2d709-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2d709-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d709-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2d709-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Showpad.</span><span class="sxs-lookup"><span data-stu-id="2d709-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="2d709-150">**Azure AD tooconfigure single sign-on con Showpad, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2d709-150">**tooconfigure Azure AD single sign-on with Showpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d709-151">Nel portale di Azure su hello hello **Showpad** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2d709-151">In hello Azure portal, on hello **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="2d709-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2d709-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_samlbase.png)

3. <span data-ttu-id="2d709-155">In hello **Showpad dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2d709-155">On hello **Showpad Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="2d709-157">a.</span><span class="sxs-lookup"><span data-stu-id="2d709-157">a.</span></span> <span data-ttu-id="2d709-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<comapany-name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="2d709-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="2d709-159">b.</span><span class="sxs-lookup"><span data-stu-id="2d709-159">b.</span></span> <span data-ttu-id="2d709-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company-name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="2d709-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2d709-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="2d709-161">These values are not real.</span></span> <span data-ttu-id="2d709-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="2d709-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2d709-163">Contatto [team di supporto Showpad](https://help.showpad.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="2d709-163">Contact [Showpad support team](https://help.showpad.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="2d709-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="2d709-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_certificate.png) 

5. <span data-ttu-id="2d709-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="2d709-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-showpad-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2d709-168">Sign-on tooyour Showpad tenant come amministratore.</span><span class="sxs-lookup"><span data-stu-id="2d709-168">Sign-on tooyour Showpad tenant as an administrator.</span></span>

7. <span data-ttu-id="2d709-169">Scegliere hello hello menu in alto hello **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="2d709-169">In hello menu on hello top, click hello **Settings**.</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

8. <span data-ttu-id="2d709-171">Passare troppo"**Single Sign-On**"e fare clic su"**abilitare**."</span><span class="sxs-lookup"><span data-stu-id="2d709-171">Navigate too"**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

9. <span data-ttu-id="2d709-173">In hello **aggiungere un servizio di SAML 2.0** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2d709-173">On hello **Add a SAML 2.0 Service** dialog, perform hello following steps:</span></span>
   
    ![Configurazione accesso Single Sign-On sul lato app](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="2d709-175">a.</span><span class="sxs-lookup"><span data-stu-id="2d709-175">a.</span></span> <span data-ttu-id="2d709-176">In hello **nome** casella di testo, nome del Provider di identificatore di tipo hello (ad esempio: il nome della società).</span><span class="sxs-lookup"><span data-stu-id="2d709-176">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="2d709-177">b.</span><span class="sxs-lookup"><span data-stu-id="2d709-177">b.</span></span> <span data-ttu-id="2d709-178">In **Metadata Source** (Origine metadati) selezionare **XML**.</span><span class="sxs-lookup"><span data-stu-id="2d709-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="2d709-179">c.</span><span class="sxs-lookup"><span data-stu-id="2d709-179">c.</span></span> <span data-ttu-id="2d709-180">Copiare il contenuto di hello del file XML dei metadati, che è stato scaricato dal portale di Azure hello, e quindi incollarlo hello **Metadata XML** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="2d709-180">Copy hello content of metadata XML file, which you have downloaded from hello Azure portal, and then paste it into hello **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="2d709-181">d.</span><span class="sxs-lookup"><span data-stu-id="2d709-181">d.</span></span> <span data-ttu-id="2d709-182">Selezionare **Auto-provision accounts for new users when they log in**.</span><span class="sxs-lookup"><span data-stu-id="2d709-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="2d709-183">e.</span><span class="sxs-lookup"><span data-stu-id="2d709-183">e.</span></span> <span data-ttu-id="2d709-184">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="2d709-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="2d709-185">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="2d709-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2d709-186">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="2d709-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2d709-187">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2d709-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2d709-188">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d709-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="2d709-189">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2d709-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="2d709-191">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2d709-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d709-192">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="2d709-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2d709-194">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="2d709-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2d709-196">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="2d709-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2d709-198">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2d709-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2d709-200">a.</span><span class="sxs-lookup"><span data-stu-id="2d709-200">a.</span></span> <span data-ttu-id="2d709-201">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2d709-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2d709-202">b.</span><span class="sxs-lookup"><span data-stu-id="2d709-202">b.</span></span> <span data-ttu-id="2d709-203">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2d709-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2d709-204">c.</span><span class="sxs-lookup"><span data-stu-id="2d709-204">c.</span></span> <span data-ttu-id="2d709-205">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="2d709-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2d709-206">d.</span><span class="sxs-lookup"><span data-stu-id="2d709-206">d.</span></span> <span data-ttu-id="2d709-207">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2d709-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="2d709-208">Creazione di un utente test di Showpad</span><span class="sxs-lookup"><span data-stu-id="2d709-208">Creating a Showpad test user</span></span>

<span data-ttu-id="2d709-209">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Showpad toocreate.</span><span class="sxs-lookup"><span data-stu-id="2d709-209">hello objective of this section is toocreate a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="2d709-210">Showpad supporta il provisioning just-in-time.</span><span class="sxs-lookup"><span data-stu-id="2d709-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="2d709-211">Il provisioning è stato abilitato in **[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="2d709-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="2d709-212">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="2d709-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2d709-213">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d709-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2d709-214">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooShowpad.</span><span class="sxs-lookup"><span data-stu-id="2d709-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooShowpad.</span></span>

![Assegna utente][200] 

<span data-ttu-id="2d709-216">**tooassign Britta Simon tooShowpad, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2d709-216">**tooassign Britta Simon tooShowpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="2d709-217">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2d709-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2d709-219">Nell'elenco di applicazioni hello, selezionare **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="2d709-219">In hello applications list, select **Showpad**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_app.png) 

3. <span data-ttu-id="2d709-221">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2d709-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="2d709-223">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2d709-223">Click **Add** button.</span></span> <span data-ttu-id="2d709-224">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2d709-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="2d709-226">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="2d709-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2d709-227">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2d709-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2d709-228">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2d709-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2d709-229">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2d709-229">Testing single sign-on</span></span>

<span data-ttu-id="2d709-230">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2d709-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2d709-231">Quando si fa clic su riquadro Showpad hello in hello Pannello di accesso, è necessario ottenere tooShowpad automaticamente firmato in applicazione.</span><span class="sxs-lookup"><span data-stu-id="2d709-231">When you click hello Showpad tile in hello Access Panel, you should get automatically signed-on tooShowpad application.</span></span>
<span data-ttu-id="2d709-232">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2d709-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2d709-233">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2d709-233">Additional resources</span></span>

* [<span data-ttu-id="2d709-234">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d709-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2d709-235">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d709-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_203.png

