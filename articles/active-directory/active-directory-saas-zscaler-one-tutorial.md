---
title: 'Esercitazione: Integrazione di Azure Active Directory con Zscaler One | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Zscaler One.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f352e00d-68d3-4a77-bb92-717d055da56f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 5179cb2cc54482334d574951a1ac64e722e5f578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-one"></a><span data-ttu-id="107e9-103">Esercitazione: Integrazione di Azure Active Directory con Zscaler One</span><span class="sxs-lookup"><span data-stu-id="107e9-103">Tutorial: Azure Active Directory integration with Zscaler One</span></span>

<span data-ttu-id="107e9-104">In questa esercitazione, è illustrato come toointegrate Zscaler One con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="107e9-104">In this tutorial, you learn how toointegrate Zscaler One with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="107e9-105">Integrazione di Zscaler One con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="107e9-105">Integrating Zscaler One with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="107e9-106">È possibile controllare in Azure AD che ha accesso tooZscaler uno</span><span class="sxs-lookup"><span data-stu-id="107e9-106">You can control in Azure AD who has access tooZscaler One</span></span>
- <span data-ttu-id="107e9-107">È possibile abilitare l'utenti tooautomatically get connesso tooZscaler uno (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="107e9-107">You can enable your users tooautomatically get signed-on tooZscaler One (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="107e9-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="107e9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="107e9-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="107e9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="107e9-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="107e9-110">Prerequisites</span></span>

<span data-ttu-id="107e9-111">integrazione di Azure AD con Zscaler One tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="107e9-111">tooconfigure Azure AD integration with Zscaler One, you need hello following items:</span></span>

- <span data-ttu-id="107e9-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="107e9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="107e9-113">Sottoscrizione di Zscaler One abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="107e9-113">A Zscaler One single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="107e9-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="107e9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="107e9-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="107e9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="107e9-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="107e9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="107e9-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="107e9-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="107e9-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="107e9-118">Scenario description</span></span>
<span data-ttu-id="107e9-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="107e9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="107e9-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="107e9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="107e9-121">Aggiunta di Zscaler One dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="107e9-121">Adding Zscaler One from hello gallery</span></span>
2. <span data-ttu-id="107e9-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="107e9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-one-from-hello-gallery"></a><span data-ttu-id="107e9-123">Aggiunta di Zscaler One dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="107e9-123">Adding Zscaler One from hello gallery</span></span>
<span data-ttu-id="107e9-124">integrazione hello tooconfigure di Zscaler One in Azure AD, è necessario tooadd Zscaler One dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="107e9-124">tooconfigure hello integration of Zscaler One into Azure AD, you need tooadd Zscaler One from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="107e9-125">**tooadd Zscaler One dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="107e9-125">**tooadd Zscaler One from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="107e9-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="107e9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="107e9-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="107e9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="107e9-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="107e9-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="107e9-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="107e9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="107e9-133">Nella casella di ricerca hello, digitare **Zscaler One**.</span><span class="sxs-lookup"><span data-stu-id="107e9-133">In hello search box, type **Zscaler One**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_search.png)

5. <span data-ttu-id="107e9-135">Nel riquadro dei risultati hello, selezionare **Zscaler One**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="107e9-135">In hello results panel, select **Zscaler One**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="107e9-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="107e9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="107e9-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Zscaler One usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="107e9-138">In this section, you configure and test Azure AD single sign-on with Zscaler One based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="107e9-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Zscaler One è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="107e9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler One is tooa user in Azure AD.</span></span> <span data-ttu-id="107e9-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Zscaler One deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="107e9-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler One needs toobe established.</span></span>

<span data-ttu-id="107e9-141">In Zscaler One, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="107e9-141">In Zscaler One, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="107e9-142">tooconfigure e test Azure single sign-on AD con Zscaler One, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="107e9-142">tooconfigure and test Azure AD single sign-on with Zscaler One, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="107e9-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="107e9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="107e9-144">**[Configurazione delle impostazioni proxy](#configuring-proxy-settings)**  -impostazioni del proxy tooconfigure hello in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="107e9-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="107e9-145">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="107e9-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="107e9-146">**[Creazione di un utente test Zscaler One](#creating-a-zscaler-one-test-user)**  -toohave un equivalente di Britta Simon in Zscaler One che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="107e9-146">**[Creating a Zscaler One test user](#creating-a-zscaler-one-test-user)** - toohave a counterpart of Britta Simon in Zscaler One that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="107e9-147">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="107e9-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="107e9-148">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="107e9-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="107e9-149">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="107e9-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="107e9-150">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Zscaler One.</span><span class="sxs-lookup"><span data-stu-id="107e9-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler One application.</span></span>

<span data-ttu-id="107e9-151">**Azure AD tooconfigure single sign-on con Zscaler One, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="107e9-151">**tooconfigure Azure AD single sign-on with Zscaler One, perform hello following steps:**</span></span>

1. <span data-ttu-id="107e9-152">Nel portale di Azure su hello hello **Zscaler One** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="107e9-152">In hello Azure portal, on hello **Zscaler One** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="107e9-154">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="107e9-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_samlbase.png)

3. <span data-ttu-id="107e9-156">In hello **Zscaler un dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="107e9-156">On hello **Zscaler One Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_url.png)

    <span data-ttu-id="107e9-158">Nella casella di testo URL accesso hello digitare l'URL di hello usato da tooyour il toosign a utenti dell'applicazione Zscaler One.</span><span class="sxs-lookup"><span data-stu-id="107e9-158">In hello Sign-on URL textbox, type hello URL used by your users toosign-on tooyour Zscaler One application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="107e9-159">Si dispone di tooupdate questo valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="107e9-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="107e9-160">Contatto [team di supporto di Zscaler un Client](https://www.zscaler.com/company/contact) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="107e9-160">Contact [Zscaler One Client support team](https://www.zscaler.com/company/contact) tooget these values.</span></span>

4. <span data-ttu-id="107e9-161">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="107e9-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_certificate.png) 

5. <span data-ttu-id="107e9-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="107e9-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="107e9-165">In hello **una configurazione di Zscaler** fare clic su **configurare Zscaler One** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="107e9-165">On hello **Zscaler One Configuration** section, click **Configure Zscaler One** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="107e9-166">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="107e9-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_configure.png) 

7. <span data-ttu-id="107e9-168">In una finestra del web browser, accedere come amministratore nel sito della società Zscaler One tooyour.</span><span class="sxs-lookup"><span data-stu-id="107e9-168">In a different web browser window, log in tooyour Zscaler One company site as an administrator.</span></span>

8. <span data-ttu-id="107e9-169">Scegliere dal menu hello in primo piano hello **amministrazione**.</span><span class="sxs-lookup"><span data-stu-id="107e9-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="107e9-170">![Amministrazione](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="107e9-170">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="107e9-171">In **Manage Administrators & Roles** (Gestisci amministratori e ruoli) fare clic su **Manage Users & Authentication** (Gestisci utenti e autenticazione).</span><span class="sxs-lookup"><span data-stu-id="107e9-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="107e9-172">![Gestire utenti e autenticazione](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "Gestire utenti e autenticazione")</span><span class="sxs-lookup"><span data-stu-id="107e9-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-one-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="107e9-173">In hello **scegliere le opzioni di autenticazione per l'organizzazione** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="107e9-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="107e9-174">![Autenticazione](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "Autenticazione")</span><span class="sxs-lookup"><span data-stu-id="107e9-174">![Authentication](./media/active-directory-saas-zscaler-one-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="107e9-175">a.</span><span class="sxs-lookup"><span data-stu-id="107e9-175">a.</span></span> <span data-ttu-id="107e9-176">Selezionare **Authenticate using SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="107e9-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="107e9-177">b.</span><span class="sxs-lookup"><span data-stu-id="107e9-177">b.</span></span> <span data-ttu-id="107e9-178">Fare clic su **Configure SAML Single Sign-On Parameters**.</span><span class="sxs-lookup"><span data-stu-id="107e9-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="107e9-179">In hello **Configure SAML Single Sign-On Parameters** pagina eseguire hello alla procedura seguente e quindi fare clic su **eseguita**</span><span class="sxs-lookup"><span data-stu-id="107e9-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="107e9-180">![Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="107e9-180">![Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="107e9-181">a.</span><span class="sxs-lookup"><span data-stu-id="107e9-181">a.</span></span> <span data-ttu-id="107e9-182">Hello Incolla **SAML Single Sign-On Service URL** valore, che è stato copiato dal portale di Azure hello in hello **URL utenti toowhich del portale SAML hello vengono inviati per l'autenticazione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="107e9-182">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="107e9-183">b.</span><span class="sxs-lookup"><span data-stu-id="107e9-183">b.</span></span> <span data-ttu-id="107e9-184">In hello **attributo che contiene il nome di account di accesso** casella tipo **NameID**.</span><span class="sxs-lookup"><span data-stu-id="107e9-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="107e9-185">c.</span><span class="sxs-lookup"><span data-stu-id="107e9-185">c.</span></span> <span data-ttu-id="107e9-186">tooupload il certificato scaricato, fare clic su **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="107e9-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="107e9-187">d.</span><span class="sxs-lookup"><span data-stu-id="107e9-187">d.</span></span> <span data-ttu-id="107e9-188">Selezionare **Enable SAML Auto-Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="107e9-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="107e9-189">In hello **Configure User Authentication** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="107e9-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="107e9-190">![Amministrazione](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="107e9-190">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="107e9-191">a.</span><span class="sxs-lookup"><span data-stu-id="107e9-191">a.</span></span> <span data-ttu-id="107e9-192">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="107e9-192">Click **Save**.</span></span>

    <span data-ttu-id="107e9-193">b.</span><span class="sxs-lookup"><span data-stu-id="107e9-193">b.</span></span> <span data-ttu-id="107e9-194">Fare clic su **Attiva subito**.</span><span class="sxs-lookup"><span data-stu-id="107e9-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="107e9-195">Configurazione delle impostazioni proxy</span><span class="sxs-lookup"><span data-stu-id="107e9-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="107e9-196">impostazioni del proxy in Internet Explorer tooconfigure hello</span><span class="sxs-lookup"><span data-stu-id="107e9-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="107e9-197">Avviare **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="107e9-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="107e9-198">Selezionare **Opzioni Internet** da hello **strumenti** menu per aprire hello **Opzioni Internet** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="107e9-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="107e9-199">![Opzioni Internet](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "Opzioni Internet")</span><span class="sxs-lookup"><span data-stu-id="107e9-199">![Internet Options](./media/active-directory-saas-zscaler-one-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="107e9-200">Fare clic su hello **connessioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="107e9-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="107e9-201">![Connessioni](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "Connessioni")</span><span class="sxs-lookup"><span data-stu-id="107e9-201">![Connections](./media/active-directory-saas-zscaler-one-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="107e9-202">Fare clic su **impostazioni LAN** tooopen hello **impostazioni LAN** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="107e9-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="107e9-203">Nella sezione server Proxy hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="107e9-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="107e9-204">![Server proxy](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "Server proxy")</span><span class="sxs-lookup"><span data-stu-id="107e9-204">![Proxy server](./media/active-directory-saas-zscaler-one-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="107e9-205">a.</span><span class="sxs-lookup"><span data-stu-id="107e9-205">a.</span></span> <span data-ttu-id="107e9-206">Selezionare **Usa un server proxy per la LAN**.</span><span class="sxs-lookup"><span data-stu-id="107e9-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="107e9-207">b.</span><span class="sxs-lookup"><span data-stu-id="107e9-207">b.</span></span> <span data-ttu-id="107e9-208">Nella casella di testo indirizzo hello digitare **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="107e9-208">In hello Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="107e9-209">c.</span><span class="sxs-lookup"><span data-stu-id="107e9-209">c.</span></span> <span data-ttu-id="107e9-210">Nella casella di testo porta hello digitare **80**.</span><span class="sxs-lookup"><span data-stu-id="107e9-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="107e9-211">d.</span><span class="sxs-lookup"><span data-stu-id="107e9-211">d.</span></span> <span data-ttu-id="107e9-212">Selezionare **Ignora server proxy per indirizzi locali**.</span><span class="sxs-lookup"><span data-stu-id="107e9-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="107e9-213">e.</span><span class="sxs-lookup"><span data-stu-id="107e9-213">e.</span></span> <span data-ttu-id="107e9-214">Fare clic su **OK** tooclose hello **Impostazioni rete locale (LAN)** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="107e9-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="107e9-215">Fare clic su **OK** tooclose hello **Opzioni Internet** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="107e9-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="107e9-216">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="107e9-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="107e9-217">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="107e9-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="107e9-218">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="107e9-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="107e9-219">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="107e9-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="107e9-220">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="107e9-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="107e9-222">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="107e9-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="107e9-223">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="107e9-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="107e9-225">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="107e9-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="107e9-227">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="107e9-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="107e9-229">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="107e9-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-zscaler-one-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="107e9-231">a.</span><span class="sxs-lookup"><span data-stu-id="107e9-231">a.</span></span> <span data-ttu-id="107e9-232">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="107e9-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="107e9-233">b.</span><span class="sxs-lookup"><span data-stu-id="107e9-233">b.</span></span> <span data-ttu-id="107e9-234">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="107e9-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="107e9-235">c.</span><span class="sxs-lookup"><span data-stu-id="107e9-235">c.</span></span> <span data-ttu-id="107e9-236">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="107e9-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="107e9-237">d.</span><span class="sxs-lookup"><span data-stu-id="107e9-237">d.</span></span> <span data-ttu-id="107e9-238">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="107e9-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-one-test-user"></a><span data-ttu-id="107e9-239">Creazione di un utente di test di Zscaler One</span><span class="sxs-lookup"><span data-stu-id="107e9-239">Creating a Zscaler One test user</span></span>

<span data-ttu-id="107e9-240">toolog agli utenti di Azure AD tooenable in tooZscaler uno, devono essere sottoposte a provisioning tooZscaler uno.</span><span class="sxs-lookup"><span data-stu-id="107e9-240">tooenable Azure AD users toolog in tooZscaler One, they must be provisioned tooZscaler One.</span></span> <span data-ttu-id="107e9-241">Nel caso di hello di Zscaler One, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="107e9-241">In hello case of Zscaler One, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="107e9-242">tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="107e9-242">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="107e9-243">Accedi tooyour **Zscaler One** tenant.</span><span class="sxs-lookup"><span data-stu-id="107e9-243">Log in tooyour **Zscaler One** tenant.</span></span>

2. <span data-ttu-id="107e9-244">Fare clic su **Administration**.</span><span class="sxs-lookup"><span data-stu-id="107e9-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="107e9-245">![Amministrazione](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "Amministrazione")</span><span class="sxs-lookup"><span data-stu-id="107e9-245">![Administration](./media/active-directory-saas-zscaler-one-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="107e9-246">Fare clic su **User Management**.</span><span class="sxs-lookup"><span data-stu-id="107e9-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="107e9-247">![Aggiungi](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "Aggiungi")</span><span class="sxs-lookup"><span data-stu-id="107e9-247">![Add](./media/active-directory-saas-zscaler-one-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="107e9-248">In hello **utenti** scheda, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="107e9-248">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="107e9-249">![Aggiungi](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "Aggiungi")</span><span class="sxs-lookup"><span data-stu-id="107e9-249">![Add](./media/active-directory-saas-zscaler-one-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="107e9-250">Nella sezione Aggiungi utente hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="107e9-250">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="107e9-251">![Aggiungere un utente](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="107e9-251">![Add User](./media/active-directory-saas-zscaler-one-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="107e9-252">a.</span><span class="sxs-lookup"><span data-stu-id="107e9-252">a.</span></span> <span data-ttu-id="107e9-253">Hello tipo **UserID**, **nome visualizzato utente**, **Password**, **Conferma Password**, quindi selezionare **gruppi**hello e **reparto** di Azure un valido account di Active Directory, si desidera tooprovision.</span><span class="sxs-lookup"><span data-stu-id="107e9-253">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="107e9-254">b.</span><span class="sxs-lookup"><span data-stu-id="107e9-254">b.</span></span> <span data-ttu-id="107e9-255">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="107e9-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="107e9-256">È possibile usare qualsiasi altro Zscaler One account strumento di creazione utente o le API fornite da Zscaler One tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="107e9-256">You can use any other Zscaler One user account creation tools or APIs provided by Zscaler One tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="107e9-257">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="107e9-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="107e9-258">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooZscaler uno.</span><span class="sxs-lookup"><span data-stu-id="107e9-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler One.</span></span>

![Assegna utente][200] 

<span data-ttu-id="107e9-260">**tooassign tooZscaler Britta Simon uno, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="107e9-260">**tooassign Britta Simon tooZscaler One, perform hello following steps:**</span></span>

1. <span data-ttu-id="107e9-261">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="107e9-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="107e9-263">Nell'elenco di applicazioni hello, selezionare **Zscaler One**.</span><span class="sxs-lookup"><span data-stu-id="107e9-263">In hello applications list, select **Zscaler One**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-zscaler-one-tutorial/tutorial_zscalerone_app.png) 

3. <span data-ttu-id="107e9-265">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="107e9-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="107e9-267">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="107e9-267">Click **Add** button.</span></span> <span data-ttu-id="107e9-268">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="107e9-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="107e9-270">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="107e9-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="107e9-271">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="107e9-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="107e9-272">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="107e9-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="107e9-273">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="107e9-273">Testing single sign-on</span></span>

<span data-ttu-id="107e9-274">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="107e9-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="107e9-275">Quando si fa clic su riquadro di Zscaler One hello in hello Pannello di accesso, è necessario ottenere applicazione Zscaler One tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="107e9-275">When you click hello Zscaler One tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler One application.</span></span>
<span data-ttu-id="107e9-276">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="107e9-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="107e9-277">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="107e9-277">Additional resources</span></span>

* [<span data-ttu-id="107e9-278">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="107e9-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="107e9-279">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="107e9-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-one-tutorial/tutorial_general_203.png

