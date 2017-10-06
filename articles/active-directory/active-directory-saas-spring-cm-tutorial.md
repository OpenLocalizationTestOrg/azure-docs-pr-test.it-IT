---
title: 'Esercitazione: Integrazione di Azure Active Directory con SpringCM | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SpringCM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 12c8ebe765e2c6e61115256e9343d90ec132e1f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="5bec1-103">Esercitazione: Integrazione di Azure Active Directory con SpringCM</span><span class="sxs-lookup"><span data-stu-id="5bec1-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="5bec1-104">In questa esercitazione, è illustrato come toointegrate SpringCM con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5bec1-104">In this tutorial, you learn how toointegrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5bec1-105">Integrazione di SpringCM con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="5bec1-105">Integrating SpringCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5bec1-106">È possibile controllare in Azure AD che ha accesso tooSpringCM</span><span class="sxs-lookup"><span data-stu-id="5bec1-106">You can control in Azure AD who has access tooSpringCM</span></span>
- <span data-ttu-id="5bec1-107">È possibile abilitare l'utenti tooautomatically get connesso tooSpringCM (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bec1-107">You can enable your users tooautomatically get signed-on tooSpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5bec1-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5bec1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5bec1-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5bec1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bec1-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5bec1-110">Prerequisites</span></span>

<span data-ttu-id="5bec1-111">integrazione di Azure AD con SpringCM tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5bec1-111">tooconfigure Azure AD integration with SpringCM, you need hello following items:</span></span>

- <span data-ttu-id="5bec1-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bec1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5bec1-113">Sottoscrizione di Spring CM abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5bec1-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5bec1-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5bec1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5bec1-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="5bec1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5bec1-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5bec1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5bec1-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5bec1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5bec1-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5bec1-118">Scenario description</span></span>
<span data-ttu-id="5bec1-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5bec1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5bec1-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="5bec1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5bec1-121">Aggiunta di SpringCM dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5bec1-121">Adding SpringCM from hello gallery</span></span>
2. <span data-ttu-id="5bec1-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bec1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-hello-gallery"></a><span data-ttu-id="5bec1-123">Aggiunta di SpringCM dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5bec1-123">Adding SpringCM from hello gallery</span></span>
<span data-ttu-id="5bec1-124">integrazione hello tooconfigure di SpringCM in Azure AD, è necessario tooadd SpringCM dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5bec1-124">tooconfigure hello integration of SpringCM into Azure AD, you need tooadd SpringCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5bec1-125">**tooadd SpringCM dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5bec1-125">**tooadd SpringCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bec1-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5bec1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5bec1-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5bec1-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5bec1-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5bec1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5bec1-133">Nella casella di ricerca hello, digitare **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-133">In hello search box, type **SpringCM**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="5bec1-135">Nel riquadro dei risultati hello, selezionare **SpringCM**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5bec1-135">In hello results panel, select **SpringCM**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5bec1-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bec1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5bec1-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SpringCM con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5bec1-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5bec1-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in SpringCM è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bec1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SpringCM is tooa user in Azure AD.</span></span> <span data-ttu-id="5bec1-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in SpringCM deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="5bec1-140">In other words, a link relationship between an Azure AD user and hello related user in SpringCM needs toobe established.</span></span>

<span data-ttu-id="5bec1-141">In SpringCM, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="5bec1-141">In SpringCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5bec1-142">tooconfigure e prova AD Azure single sign-on con SpringCM, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="5bec1-142">tooconfigure and test Azure AD single sign-on with SpringCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5bec1-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5bec1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5bec1-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5bec1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5bec1-145">**[Creazione di un utente test SpringCM](#creating-a-springcm-test-user)**  -toohave un equivalente di Britta Simon in SpringCM che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5bec1-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - toohave a counterpart of Britta Simon in SpringCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5bec1-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5bec1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5bec1-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="5bec1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5bec1-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bec1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5bec1-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione SpringCM.</span><span class="sxs-lookup"><span data-stu-id="5bec1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="5bec1-150">**Azure AD tooconfigure single sign-on con SpringCM, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5bec1-150">**tooconfigure Azure AD single sign-on with SpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bec1-151">Nel portale di Azure su hello hello **SpringCM** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-151">In hello Azure portal, on hello **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5bec1-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5bec1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="5bec1-155">In hello **SpringCM dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5bec1-155">On hello **SpringCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="5bec1-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="5bec1-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5bec1-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="5bec1-158">This value is not real.</span></span> <span data-ttu-id="5bec1-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5bec1-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5bec1-160">Contatto [team di supporto Client di SpringCM](https://knowledge.springcm.com/support) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="5bec1-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="5bec1-161">In hello **certificato di firma SAML** fare clic su **Certificate(Raw)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5bec1-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="5bec1-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5bec1-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5bec1-165">In hello **SpringCM configurazione** fare clic su **configurare SpringCM** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="5bec1-165">On hello **SpringCM Configuration** section, click **Configure SpringCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5bec1-166">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="5bec1-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="5bec1-168">In una finestra del web browser, accedere tooyour **SpringCM** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5bec1-168">In a different web browser window, sign on tooyour **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="5bec1-169">Scegliere hello menu nella parte superiore di hello **Vai a**, fare clic su **preferenze**, quindi nel hello **Preferenze Account** fare clic su **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-169">In hello menu on hello top, click **GO TO**, click **Preferences**, and then, in hello **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="5bec1-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span><span class="sxs-lookup"><span data-stu-id="5bec1-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="5bec1-171">Nella sezione di configurazione del Provider di identità hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5bec1-171">In hello Identity Provider Configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5bec1-172">![Configurazione del provider di identità](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Configurazione del provider di identità")</span><span class="sxs-lookup"><span data-stu-id="5bec1-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="5bec1-173">a.</span><span class="sxs-lookup"><span data-stu-id="5bec1-173">a.</span></span> <span data-ttu-id="5bec1-174">tooupload il certificato di Azure Active Directory scaricato, fare clic su **selezionare un certificato dell'autorità di certificazione** o **Change Issuer Certificate**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-174">tooupload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="5bec1-175">b.</span><span class="sxs-lookup"><span data-stu-id="5bec1-175">b.</span></span> <span data-ttu-id="5bec1-176">Incolla **ID entità SAML** valore, che è stato copiato dal portale di Azure in hello **dell'autorità di certificazione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="5bec1-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into hello **Issuer** textbox.</span></span>
    
    <span data-ttu-id="5bec1-177">c.</span><span class="sxs-lookup"><span data-stu-id="5bec1-177">c.</span></span> <span data-ttu-id="5bec1-178">Incolla **SAML Single Sign-On Service URL** valore, che è stato copiato dal portale di Azure hello in hello **Service Provider (SP) Initiated Endpoint** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="5bec1-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="5bec1-179">d.</span><span class="sxs-lookup"><span data-stu-id="5bec1-179">d.</span></span> <span data-ttu-id="5bec1-180">Selezionare **Abilitato SAML** in modo che sia **Abilitato**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="5bec1-181">e.</span><span class="sxs-lookup"><span data-stu-id="5bec1-181">e.</span></span> <span data-ttu-id="5bec1-182">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="5bec1-183">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="5bec1-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5bec1-184">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="5bec1-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5bec1-185">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5bec1-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5bec1-186">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bec1-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="5bec1-187">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5bec1-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5bec1-189">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5bec1-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bec1-190">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5bec1-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5bec1-192">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5bec1-194">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="5bec1-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5bec1-196">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5bec1-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5bec1-198">a.</span><span class="sxs-lookup"><span data-stu-id="5bec1-198">a.</span></span> <span data-ttu-id="5bec1-199">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5bec1-200">b.</span><span class="sxs-lookup"><span data-stu-id="5bec1-200">b.</span></span> <span data-ttu-id="5bec1-201">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5bec1-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5bec1-202">c.</span><span class="sxs-lookup"><span data-stu-id="5bec1-202">c.</span></span> <span data-ttu-id="5bec1-203">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5bec1-204">d.</span><span class="sxs-lookup"><span data-stu-id="5bec1-204">d.</span></span> <span data-ttu-id="5bec1-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="5bec1-206">Creazione di un utente di test di SpringCM</span><span class="sxs-lookup"><span data-stu-id="5bec1-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="5bec1-207">toolog agli utenti di Azure Active Directory tooenable in tooSpringCM, è necessario eseguirne il provisioning in SpringCM.</span><span class="sxs-lookup"><span data-stu-id="5bec1-207">tooenable Azure Active Directory users toolog in tooSpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="5bec1-208">Nel caso di hello di SpringCM, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="5bec1-208">In hello case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="5bec1-209">Per altre informazioni, vedere [Creare e modificare un utente SpringCM](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span><span class="sxs-lookup"><span data-stu-id="5bec1-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="5bec1-210">**tooprovision tooSpringCM un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5bec1-210">**tooprovision a user account tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bec1-211">Accedi tooyour **SpringCM** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5bec1-211">Log in tooyour **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="5bec1-212">Fare clic su **GOTO** e scegliere **RUBRICA**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="5bec1-213">![Crea utente](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Crea utente")</span><span class="sxs-lookup"><span data-stu-id="5bec1-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="5bec1-214">Fare clic su **Create User**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-214">Click **Create User**.</span></span>

4. <span data-ttu-id="5bec1-215">Selezionare un **Ruolo utente**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="5bec1-216">Selezionare **Invia messaggio di attivazione**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="5bec1-217">Tipo hello nome, cognome e indirizzo di posta elettronica di un account utente di Azure Active Directory valido desiderate tooprovision hello correlati nelle caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="5bec1-217">Type hello first name, last name, and email address of a valid Azure Active Directory user account you want tooprovision into hello related textboxes.</span></span>

7. <span data-ttu-id="5bec1-218">Aggiungere hello utente tooa **gruppo di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-218">Add hello user tooa **Security group**.</span></span>

8. <span data-ttu-id="5bec1-219">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="5bec1-220">È possibile usare qualsiasi altro SpringCM utente account strumento di creazione o le API fornite da SpringCM tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="5bec1-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM tooprovision AAD user accounts.</span></span>  
  > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5bec1-221">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bec1-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5bec1-222">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSpringCM.</span><span class="sxs-lookup"><span data-stu-id="5bec1-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringCM.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5bec1-224">**tooassign Britta Simon tooSpringCM, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5bec1-224">**tooassign Britta Simon tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bec1-225">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5bec1-227">Nell'elenco di applicazioni hello, selezionare **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-227">In hello applications list, select **SpringCM**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="5bec1-229">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5bec1-231">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-231">Click **Add** button.</span></span> <span data-ttu-id="5bec1-232">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5bec1-234">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="5bec1-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5bec1-235">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5bec1-236">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5bec1-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5bec1-237">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5bec1-237">Testing single sign-on</span></span>

<span data-ttu-id="5bec1-238">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5bec1-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="5bec1-239">Quando si fa clic su riquadro SpringCM hello in hello Pannello di accesso, è necessario ottenere applicazione SpringCM tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="5bec1-239">When you click hello SpringCM tile in hello Access Panel, you should get automatically signed-on tooyour SpringCM application.</span></span>

<span data-ttu-id="5bec1-240">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5bec1-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5bec1-241">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5bec1-241">Additional resources</span></span>

* [<span data-ttu-id="5bec1-242">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bec1-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5bec1-243">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bec1-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

