---
title: 'Esercitazione: Integrazione di Azure Active Directory con Intralinks | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Intralinks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6fa49c932d0c48d4b48e04fe91af9fc86a0c1cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="281a0-103">Esercitazione: Integrazione di Azure Active Directory con Intralinks</span><span class="sxs-lookup"><span data-stu-id="281a0-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="281a0-104">In questa esercitazione, è illustrato come toointegrate Intralinks con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="281a0-104">In this tutorial, you learn how toointegrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="281a0-105">Integrazione Intralinks con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="281a0-105">Integrating Intralinks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="281a0-106">È possibile controllare in Azure AD che ha accesso tooIntralinks</span><span class="sxs-lookup"><span data-stu-id="281a0-106">You can control in Azure AD who has access tooIntralinks</span></span>
- <span data-ttu-id="281a0-107">È possibile abilitare l'utenti tooautomatically get connesso tooIntralinks (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="281a0-107">You can enable your users tooautomatically get signed-on tooIntralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="281a0-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="281a0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="281a0-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="281a0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="281a0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="281a0-110">Prerequisites</span></span>

<span data-ttu-id="281a0-111">integrazione di Azure AD con Intralinks tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="281a0-111">tooconfigure Azure AD integration with Intralinks, you need hello following items:</span></span>

- <span data-ttu-id="281a0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="281a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="281a0-113">Sottoscrizione Intralinks abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="281a0-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="281a0-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="281a0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="281a0-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="281a0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="281a0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="281a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="281a0-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="281a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="281a0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="281a0-118">Scenario description</span></span>
<span data-ttu-id="281a0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="281a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="281a0-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="281a0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="281a0-121">Aggiunta di Intralinks dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="281a0-121">Adding Intralinks from hello gallery</span></span>
2. <span data-ttu-id="281a0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="281a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-hello-gallery"></a><span data-ttu-id="281a0-123">Aggiunta di Intralinks dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="281a0-123">Adding Intralinks from hello gallery</span></span>
<span data-ttu-id="281a0-124">integrazione hello tooconfigure di Intralinks in Azure AD, è necessario tooadd Intralinks dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="281a0-124">tooconfigure hello integration of Intralinks into Azure AD, you need tooadd Intralinks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="281a0-125">**tooadd Intralinks dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="281a0-125">**tooadd Intralinks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="281a0-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="281a0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="281a0-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="281a0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="281a0-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="281a0-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="281a0-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="281a0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="281a0-133">Nella casella di ricerca hello, digitare **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="281a0-133">In hello search box, type **Intralinks**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="281a0-135">Nel riquadro dei risultati hello, selezionare **Intralinks**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="281a0-135">In hello results panel, select **Intralinks**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="281a0-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="281a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="281a0-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Intralinks con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="281a0-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="281a0-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Intralinks è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="281a0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intralinks is tooa user in Azure AD.</span></span> <span data-ttu-id="281a0-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Intralinks deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="281a0-140">In other words, a link relationship between an Azure AD user and hello related user in Intralinks needs toobe established.</span></span>

<span data-ttu-id="281a0-141">In Intralinks, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="281a0-141">In Intralinks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="281a0-142">tooconfigure e prova AD Azure single sign-on con Intralinks, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="281a0-142">tooconfigure and test Azure AD single sign-on with Intralinks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="281a0-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="281a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="281a0-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="281a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="281a0-145">**[Creazione di un utente test Intralinks](#creating-an-intralinks-test-user)**  -toohave un equivalente di Britta Simon in Intralinks che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="281a0-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - toohave a counterpart of Britta Simon in Intralinks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="281a0-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="281a0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="281a0-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="281a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="281a0-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="281a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="281a0-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Intralinks.</span><span class="sxs-lookup"><span data-stu-id="281a0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="281a0-150">**Azure AD tooconfigure single sign-on con Intralinks, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="281a0-150">**tooconfigure Azure AD single sign-on with Intralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="281a0-151">Nel portale di Azure su hello hello **Intralinks** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="281a0-151">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="281a0-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="281a0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="281a0-155">In hello **Intralinks dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="281a0-155">On hello **Intralinks Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="281a0-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="281a0-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="281a0-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="281a0-158">This value is not real.</span></span> <span data-ttu-id="281a0-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="281a0-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="281a0-160">Contatto [team di supporto Intralinks Client](https://www.intralinks.com/contact-1) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="281a0-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) tooget this value.</span></span> 
 
4. <span data-ttu-id="281a0-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="281a0-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="281a0-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="281a0-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="281a0-165">tooconfigure single sign-on sul **Intralinks** lato, è necessario hello toosend scaricato **Metadata XML** [Intralinks team di supporto](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="281a0-165">tooconfigure single sign-on on **Intralinks** side, you need toosend hello downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="281a0-166">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="281a0-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="281a0-167">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="281a0-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="281a0-168">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="281a0-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="281a0-169">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="281a0-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="281a0-170">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="281a0-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="281a0-171">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="281a0-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="281a0-173">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="281a0-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="281a0-174">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="281a0-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="281a0-176">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="281a0-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="281a0-178">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="281a0-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="281a0-180">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="281a0-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="281a0-182">a.</span><span class="sxs-lookup"><span data-stu-id="281a0-182">a.</span></span> <span data-ttu-id="281a0-183">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="281a0-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="281a0-184">b.</span><span class="sxs-lookup"><span data-stu-id="281a0-184">b.</span></span> <span data-ttu-id="281a0-185">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="281a0-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="281a0-186">c.</span><span class="sxs-lookup"><span data-stu-id="281a0-186">c.</span></span> <span data-ttu-id="281a0-187">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="281a0-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="281a0-188">d.</span><span class="sxs-lookup"><span data-stu-id="281a0-188">d.</span></span> <span data-ttu-id="281a0-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="281a0-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="281a0-190">Creazione di un utente test di Intralinks</span><span class="sxs-lookup"><span data-stu-id="281a0-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="281a0-191">In questa sezione viene creato un utente chiamato Britta Simon in Intralinks.</span><span class="sxs-lookup"><span data-stu-id="281a0-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="281a0-192">Rivolgersi [Intralinks team di supporto](https://www.intralinks.com/contact-1) utenti hello tooadd nella piattaforma Intralinks hello.</span><span class="sxs-lookup"><span data-stu-id="281a0-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) tooadd hello users in hello Intralinks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="281a0-193">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="281a0-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="281a0-194">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooIntralinks.</span><span class="sxs-lookup"><span data-stu-id="281a0-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntralinks.</span></span>

![Assegna utente][200] 

<span data-ttu-id="281a0-196">**tooassign Britta Simon tooIntralinks, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="281a0-196">**tooassign Britta Simon tooIntralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="281a0-197">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="281a0-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="281a0-199">Nell'elenco di applicazioni hello, selezionare **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="281a0-199">In hello applications list, select **Intralinks**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="281a0-201">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="281a0-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="281a0-203">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="281a0-203">Click **Add** button.</span></span> <span data-ttu-id="281a0-204">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="281a0-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="281a0-206">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="281a0-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="281a0-207">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="281a0-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="281a0-208">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="281a0-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="281a0-209">Aggiungere un'applicazione Intralinks VIA o Elite</span><span class="sxs-lookup"><span data-stu-id="281a0-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="281a0-210">Usa Intralinks hello stessa piattaforma di identità SSO per tutte le altre applicazioni Intralinks escludendo applicazione Nexus trattativa.</span><span class="sxs-lookup"><span data-stu-id="281a0-210">Intralinks uses hello same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="281a0-211">Se si prevede di qualsiasi altra applicazione Intralinks toouse quindi innanzitutto è necessario tooconfigure SSO per un'applicazione Intralinks primario descritto in precedenza nella procedura hello.</span><span class="sxs-lookup"><span data-stu-id="281a0-211">So if you plan toouse any other Intralinks application then first you have tooconfigure SSO for one Primary Intralinks application using hello procedure described above.</span></span>

<span data-ttu-id="281a0-212">Dopo che è possibile seguire hello seguito procedure tooadd un'altra applicazione Intralinks nel tenant di cui è possibile sfruttare questa applicazione principale per SSO.</span><span class="sxs-lookup"><span data-stu-id="281a0-212">After that you can follow hello below procedure tooadd another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="281a0-213">Questa funzionalità è disponibile solo tooAzure Active Directory Premium SKU i clienti e non è disponibile per i clienti gratuito o Basic SKU.</span><span class="sxs-lookup"><span data-stu-id="281a0-213">This feature is available only tooAzure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="281a0-214">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="281a0-214">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="281a0-216">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="281a0-216">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="281a0-217">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="281a0-217">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="281a0-219">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="281a0-219">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="281a0-221">Nella casella di ricerca hello, digitare **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="281a0-221">In hello search box, type **Intralinks**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="281a0-223">In **Intralinks Aggiungi app** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="281a0-223">On **Intralinks Add app** perform hello following steps:</span></span>

    ![Aggiunta di un'applicazione Intralinks VIA o Elite](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="281a0-225">a.</span><span class="sxs-lookup"><span data-stu-id="281a0-225">a.</span></span> <span data-ttu-id="281a0-226">In **nome** casella di testo, immettere un nome appropriato di un'applicazione hello, ad esempio **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="281a0-226">In **Name** textbox, enter appropriate name of hello application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="281a0-227">b.</span><span class="sxs-lookup"><span data-stu-id="281a0-227">b.</span></span> <span data-ttu-id="281a0-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="281a0-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="281a0-229">Nel portale di Azure su hello hello **Intralinks** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="281a0-229">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

7. <span data-ttu-id="281a0-231">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **collegato Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="281a0-231">On hello **Single sign-on** dialog, select **Mode** as   **Linked Sign-on**.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="281a0-233">Ottenere l'URL di SSO avviato hello SP hello da [Intralinks team](https://www.intralinks.com/contact-1) per hello un'altra applicazione Intralinks e immetterlo nel **Configura Sign-on URL** come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="281a0-233">Get hello hello SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for hello other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="281a0-235">Nella casella di testo URL accesso hello digitare l'URL di hello usato dall'applicazione Intralinks tooyour toosign-on agli utenti tramite hello seguente motivo:</span><span class="sxs-lookup"><span data-stu-id="281a0-235">In hello Sign On URL textbox, type hello URL used by your users toosign-on tooyour Intralinks application using hello following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="281a0-236">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="281a0-236">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="281a0-238">Assegnare toouser applicazione hello o i gruppi, come illustrato nella sezione hello  **[utente test hello Azure AD di assegnazione](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="281a0-238">Assign hello application toouser or groups as shown in hello section **[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="281a0-239">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="281a0-239">Testing single sign-on</span></span>

<span data-ttu-id="281a0-240">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="281a0-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="281a0-241">Quando si fa clic hello Intralinks riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Intralinks applicazione.</span><span class="sxs-lookup"><span data-stu-id="281a0-241">When you click hello Intralinks tile in hello Access Panel, you should get automatically signed-on tooyour Intralinks application.</span></span>
<span data-ttu-id="281a0-242">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="281a0-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="281a0-243">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="281a0-243">Additional resources</span></span>

* [<span data-ttu-id="281a0-244">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="281a0-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="281a0-245">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="281a0-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

