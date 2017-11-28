---
title: 'Esercitazione: Integrazione di Azure Active Directory con Aha! | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Aha!.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="d5077-104">Esercitazione: Integrazione di Azure Active Directory con Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="d5077-105">In questa esercitazione, è illustrato come toointegrate Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-105">In this tutorial, you learn how toointegrate Aha!</span></span> <span data-ttu-id="d5077-106">con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d5077-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d5077-107">L'integrazione di Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-107">Integrating Aha!</span></span> <span data-ttu-id="d5077-108">con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d5077-108">with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d5077-109">È possibile controllare in Azure AD che ha accesso tooAha!</span><span class="sxs-lookup"><span data-stu-id="d5077-109">You can control in Azure AD who has access tooAha!</span></span>
- <span data-ttu-id="d5077-110">È possibile abilitare il get tooautomatically utenti connesso tooAha!</span><span class="sxs-lookup"><span data-stu-id="d5077-110">You can enable your users tooautomatically get signed-on tooAha!</span></span> <span data-ttu-id="d5077-111">(Single Sign-On) con gli account Azure AD personali</span><span class="sxs-lookup"><span data-stu-id="d5077-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d5077-112">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d5077-112">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d5077-113">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d5077-113">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5077-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d5077-114">Prerequisites</span></span>

<span data-ttu-id="d5077-115">tooconfigure integrazione di Azure AD con Aha!, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d5077-115">tooconfigure Azure AD integration with Aha!, you need hello following items:</span></span>

- <span data-ttu-id="d5077-116">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5077-116">An Azure AD subscription</span></span>
- <span data-ttu-id="d5077-117">Sottoscrizione Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-117">An Aha!</span></span> <span data-ttu-id="d5077-118">abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d5077-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d5077-119">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d5077-119">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d5077-120">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="d5077-120">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d5077-121">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d5077-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d5077-122">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d5077-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d5077-123">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d5077-123">Scenario description</span></span>
<span data-ttu-id="d5077-124">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d5077-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d5077-125">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="d5077-125">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d5077-126">Aggiunta di Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-126">Adding Aha!</span></span> <span data-ttu-id="d5077-127">dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d5077-127">from hello gallery</span></span>
2. <span data-ttu-id="d5077-128">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5077-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-hello-gallery"></a><span data-ttu-id="d5077-129">Aggiunta di Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-129">Adding Aha!</span></span> <span data-ttu-id="d5077-130">dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d5077-130">from hello gallery</span></span>
<span data-ttu-id="d5077-131">integrazione di hello tooconfigure di Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-131">tooconfigure hello integration of Aha!</span></span> <span data-ttu-id="d5077-132">in Azure AD, è necessario tooadd Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-132">into Azure AD, you need tooadd Aha!</span></span> <span data-ttu-id="d5077-133">dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d5077-133">from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d5077-134">**tooadd Aha! dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d5077-134">**tooadd Aha! from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5077-135">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d5077-135">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d5077-137">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d5077-137">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d5077-138">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d5077-138">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d5077-140">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d5077-140">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d5077-142">Nella casella di ricerca hello, digitare **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="d5077-142">In hello search box, type **Aha!**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="d5077-144">Nel riquadro dei risultati hello, selezionare **Aha!**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d5077-144">In hello results panel, select **Aha!**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d5077-146">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5077-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d5077-147">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="d5077-148">usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d5077-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d5077-149">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Aha!</span></span> <span data-ttu-id="d5077-150">è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5077-150">is tooa user in Azure AD.</span></span> <span data-ttu-id="d5077-151">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-151">In other words, a link relationship between an Azure AD user and hello related user in Aha!</span></span> <span data-ttu-id="d5077-152">è necessario toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="d5077-152">needs toobe established.</span></span>

<span data-ttu-id="d5077-153">In Aha!, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="d5077-153">In Aha!, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d5077-154">tooconfigure e test di Azure AD accesso single sign-on con Aha!, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="d5077-154">tooconfigure and test Azure AD single sign-on with Aha!, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d5077-155">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d5077-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d5077-156">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d5077-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d5077-157">**[Creazione di un Aha! utente test](#creating-an-aha-test-user)**  -toohave un equivalente di Britta Simon in Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - toohave a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="d5077-158">che è collegato toohello rappresentazione in forma di Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d5077-158">that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d5077-159">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d5077-159">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d5077-160">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="d5077-160">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d5077-161">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5077-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d5077-162">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nel Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-162">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="d5077-163">nell'applicazione Aha!.</span><span class="sxs-lookup"><span data-stu-id="d5077-163">application.</span></span>

<span data-ttu-id="d5077-164">**tooconfigure AD Azure single sign-on con Aha!, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d5077-164">**tooconfigure Azure AD single sign-on with Aha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5077-165">Nel portale di Azure su hello hello **Aha!**</span><span class="sxs-lookup"><span data-stu-id="d5077-165">In hello Azure portal, on hello **Aha!**</span></span> <span data-ttu-id="d5077-166">del portale di Azure fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d5077-166">application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d5077-168">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d5077-168">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="d5077-170">In hello **Aha! Dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d5077-170">On hello **Aha! Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="d5077-172">a.</span><span class="sxs-lookup"><span data-stu-id="d5077-172">a.</span></span> <span data-ttu-id="d5077-173">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="d5077-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="d5077-174">b.</span><span class="sxs-lookup"><span data-stu-id="d5077-174">b.</span></span> <span data-ttu-id="d5077-175">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="d5077-175">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d5077-176">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="d5077-176">These values are not real.</span></span> <span data-ttu-id="d5077-177">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="d5077-177">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d5077-178">Per ottenere questi valori, contattare il [team di supporto Il team di supporto client](https://www.aha.io/company/contact) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="d5077-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="d5077-179">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d5077-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="d5077-181">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d5077-181">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d5077-183">In una finestra del web browser, accedere tooyour Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-183">In a different web browser window, log in tooyour Aha!</span></span> <span data-ttu-id="d5077-184">come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d5077-184">company site as an administrator.</span></span>

7. <span data-ttu-id="d5077-185">Scegliere dal menu hello in primo piano hello **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="d5077-185">In hello menu on hello top, click **Settings**.</span></span>

    <span data-ttu-id="d5077-186">![Impostazioni](./media/active-directory-saas-aha-tutorial/IC798950.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="d5077-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="d5077-187">Fare clic su **Account**.</span><span class="sxs-lookup"><span data-stu-id="d5077-187">Click **Account**.</span></span>
   
    <span data-ttu-id="d5077-188">![Profilo](./media/active-directory-saas-aha-tutorial/IC798951.png "Profilo")</span><span class="sxs-lookup"><span data-stu-id="d5077-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="d5077-189">Fare clic su **Sicurezza e single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d5077-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="d5077-190">![Sicurezza e Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798952.png "Sicurezza e Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d5077-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="d5077-191">Nella sezione **Single Sign-On** in **Identity Provider** (Provider di identità) selezionare **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="d5077-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="d5077-192">![Sicurezza e Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798953.png "Sicurezza e Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d5077-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="d5077-193">In hello **Single Sign-On** configurazione eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d5077-193">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
    
    <span data-ttu-id="d5077-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="d5077-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="d5077-195">a.</span><span class="sxs-lookup"><span data-stu-id="d5077-195">a.</span></span> <span data-ttu-id="d5077-196">In hello **nome** casella di testo, digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="d5077-196">In hello **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="d5077-197">b.</span><span class="sxs-lookup"><span data-stu-id="d5077-197">b.</span></span> <span data-ttu-id="d5077-198">Per **Configure using** (Configura mediante) selezionare **Metadata File** (File di metadati).</span><span class="sxs-lookup"><span data-stu-id="d5077-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="d5077-199">c.</span><span class="sxs-lookup"><span data-stu-id="d5077-199">c.</span></span> <span data-ttu-id="d5077-200">tooupload file di metadati scaricato, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="d5077-200">tooupload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="d5077-201">d.</span><span class="sxs-lookup"><span data-stu-id="d5077-201">d.</span></span> <span data-ttu-id="d5077-202">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="d5077-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="d5077-203">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="d5077-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d5077-204">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="d5077-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d5077-205">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d5077-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d5077-206">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5077-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="d5077-207">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d5077-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d5077-209">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d5077-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5077-210">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d5077-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d5077-212">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="d5077-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d5077-214">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="d5077-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d5077-216">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d5077-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d5077-218">a.</span><span class="sxs-lookup"><span data-stu-id="d5077-218">a.</span></span> <span data-ttu-id="d5077-219">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d5077-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d5077-220">b.</span><span class="sxs-lookup"><span data-stu-id="d5077-220">b.</span></span> <span data-ttu-id="d5077-221">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d5077-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d5077-222">c.</span><span class="sxs-lookup"><span data-stu-id="d5077-222">c.</span></span> <span data-ttu-id="d5077-223">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="d5077-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d5077-224">d.</span><span class="sxs-lookup"><span data-stu-id="d5077-224">d.</span></span> <span data-ttu-id="d5077-225">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d5077-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="d5077-226">Creazione di un</span><span class="sxs-lookup"><span data-stu-id="d5077-226">Creating an Aha!</span></span> <span data-ttu-id="d5077-227">utente di test di Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-227">test user</span></span>

<span data-ttu-id="d5077-228">Azure AD tooenable utenti toolog in tooAha!, è necessario eseguirne il provisioning in Aha!.</span><span class="sxs-lookup"><span data-stu-id="d5077-228">tooenable Azure AD users toolog in tooAha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="d5077-229">Nel caso di hello di Aha!, il provisioning è un'attività automatica.</span><span class="sxs-lookup"><span data-stu-id="d5077-229">In hello case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="d5077-230">Non è necessario eseguire alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="d5077-230">There is no action item for you.</span></span>

<span data-ttu-id="d5077-231">Gli utenti vengono creati automaticamente se necessario, durante hello primo single sign-on tentativo.</span><span class="sxs-lookup"><span data-stu-id="d5077-231">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="d5077-232">È possibile usare qualsiasi altro</span><span class="sxs-lookup"><span data-stu-id="d5077-232">You can use any other Aha!</span></span> <span data-ttu-id="d5077-233">strumento di creazione di account utente Aha! o qualsiasi altra API disponibile in Aha!</span><span class="sxs-lookup"><span data-stu-id="d5077-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="d5077-234">account utente di AAD tooprovision.</span><span class="sxs-lookup"><span data-stu-id="d5077-234">tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d5077-235">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5077-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d5077-236">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAha!.</span><span class="sxs-lookup"><span data-stu-id="d5077-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAha!.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d5077-238">**tooassign Britta Simon tooAha!, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d5077-238">**tooassign Britta Simon tooAha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5077-239">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d5077-239">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d5077-241">Nell'elenco di applicazioni hello, selezionare **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="d5077-241">In hello applications list, select **Aha!**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="d5077-243">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d5077-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d5077-245">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d5077-245">Click **Add** button.</span></span> <span data-ttu-id="d5077-246">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d5077-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d5077-248">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="d5077-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d5077-249">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d5077-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d5077-250">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d5077-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d5077-251">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d5077-251">Testing single sign-on</span></span>

<span data-ttu-id="d5077-252">Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="d5077-252">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="d5077-253">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d5077-253">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d5077-254">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d5077-254">Additional resources</span></span>

* [<span data-ttu-id="d5077-255">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5077-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d5077-256">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5077-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

