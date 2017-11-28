---
title: 'Esercitazione: Integrazione di Azure Active Directory con xMatters OnDemand | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e xMatters OnDemand.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="81162-103">Esercitazione: Integrazione di Azure Active Directory con xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="81162-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="81162-104">In questa esercitazione, è illustrato come toointegrate xMatters OnDemand con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="81162-104">In this tutorial, you learn how toointegrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81162-105">Integrazione di xMatters OnDemand con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="81162-105">Integrating xMatters OnDemand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="81162-106">È possibile controllare in Azure AD che ha accesso tooxMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="81162-106">You can control in Azure AD who has access tooxMatters OnDemand</span></span>
- <span data-ttu-id="81162-107">È possibile abilitare l'utenti tooautomatically get connesso tooxMatters OnDemand (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="81162-107">You can enable your users tooautomatically get signed-on tooxMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81162-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="81162-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="81162-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81162-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81162-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="81162-110">Prerequisites</span></span>

<span data-ttu-id="81162-111">integrazione di Azure AD con xMatters OnDemand tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="81162-111">tooconfigure Azure AD integration with xMatters OnDemand, you need hello following items:</span></span>

- <span data-ttu-id="81162-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81162-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81162-113">Sottoscrizione di xMatters OnDemand abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="81162-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81162-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="81162-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81162-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="81162-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81162-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="81162-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81162-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81162-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81162-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="81162-118">Scenario description</span></span>
<span data-ttu-id="81162-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="81162-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81162-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="81162-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81162-121">Aggiunta di xMatters OnDemand dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="81162-121">Adding xMatters OnDemand from hello gallery</span></span>
2. <span data-ttu-id="81162-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="81162-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a><span data-ttu-id="81162-123">Aggiunta di xMatters OnDemand dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="81162-123">Adding xMatters OnDemand from hello gallery</span></span>
<span data-ttu-id="81162-124">integrazione hello tooconfigure di xMatters OnDemand in Azure AD, è necessario tooadd xMatters OnDemand dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="81162-124">tooconfigure hello integration of xMatters OnDemand into Azure AD, you need tooadd xMatters OnDemand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="81162-125">**tooadd xMatters OnDemand dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="81162-125">**tooadd xMatters OnDemand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="81162-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="81162-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="81162-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="81162-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="81162-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="81162-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="81162-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="81162-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="81162-133">Nella casella di ricerca hello, digitare **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="81162-133">In hello search box, type **xMatters OnDemand**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="81162-135">Nel riquadro dei risultati hello, selezionare **xMatters OnDemand**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="81162-135">In hello results panel, select **xMatters OnDemand**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="81162-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="81162-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="81162-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con xMatters OnDemand usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="81162-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="81162-139">Per toowork di accesso singolo, Azure AD deve tooknow quali hello utente corrispondente in xMatters OnDemand è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81162-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in xMatters OnDemand is tooa user in Azure AD.</span></span> <span data-ttu-id="81162-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in xMatters OnDemand deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="81162-140">In other words, a link relationship between an Azure AD user and hello related user in xMatters OnDemand needs toobe established.</span></span>

<span data-ttu-id="81162-141">In xMatters OnDemand, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="81162-141">In xMatters OnDemand, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="81162-142">tooconfigure e test Azure single sign-on AD con xMatters OnDemand, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="81162-142">tooconfigure and test Azure AD single sign-on with xMatters OnDemand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="81162-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="81162-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="81162-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81162-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81162-145">**[Creazione di un utente di xMatters OnDemand test](#creating-a-xmatters-ondemand-test-user)**  -toohave un equivalente di Britta Simon in xMatters OnDemand che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="81162-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - toohave a counterpart of Britta Simon in xMatters OnDemand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="81162-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="81162-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81162-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="81162-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="81162-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="81162-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="81162-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nel xMatters OnDemand applicazione.</span><span class="sxs-lookup"><span data-stu-id="81162-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="81162-150">**Azure AD tooconfigure single sign-on con xMatters OnDemand, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="81162-150">**tooconfigure Azure AD single sign-on with xMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="81162-151">Nel portale di Azure su hello hello **xMatters OnDemand** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="81162-151">In hello Azure portal, on hello **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="81162-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="81162-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="81162-155">In hello **xMatters OnDemand dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="81162-155">On hello **xMatters OnDemand Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="81162-157">a.</span><span class="sxs-lookup"><span data-stu-id="81162-157">a.</span></span> <span data-ttu-id="81162-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="81162-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="81162-159">b.</span><span class="sxs-lookup"><span data-stu-id="81162-159">b.</span></span> <span data-ttu-id="81162-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="81162-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="81162-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="81162-161">These values are not real.</span></span> <span data-ttu-id="81162-162">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="81162-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="81162-163">Contatto [team di supporto xMatters OnDemand](https://www.xmatters.com/company/contact-us/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="81162-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="81162-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare hello file del certificato localmente come **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="81162-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="81162-166">È necessario tooforward hello certificato toohello [team di supporto xMatters OnDemand](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="81162-166">You need tooforward hello certificate toohello [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="81162-167">certificato Hello deve toobe caricato dal team di supporto xMatters hello per poter completare configurazione hello single sign-on.</span><span class="sxs-lookup"><span data-stu-id="81162-167">hello certificate needs toobe uploaded by hello xMatters support team before you can finalize hello single sign-on configuration.</span></span> 

5. <span data-ttu-id="81162-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="81162-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="81162-170">In hello **xMatters OnDemand configurazione** fare clic su **configurare xMatters OnDemand** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="81162-170">On hello **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="81162-171">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="81162-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="81162-173">In una finestra del web browser, accedere tooyour sito della società XMatters OnDemand come amministratore.</span><span class="sxs-lookup"><span data-stu-id="81162-173">In a different web browser window, log in tooyour XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="81162-174">Nella barra degli strumenti hello in primo piano hello, fare clic su **Admin**, quindi fare clic su **i dettagli della società** sulla barra di navigazione hello hello lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="81162-174">In hello toolbar on hello top, click **Admin**, and then click **Company Details** in hello navigation bar on hello left side.</span></span>
   
    <span data-ttu-id="81162-175">![Amministratore](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="81162-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="81162-176">In hello **configurazione SAML** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="81162-176">On hello **SAML Configuration** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="81162-177">![Configurazione SAML](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "Configurazione SAML")</span><span class="sxs-lookup"><span data-stu-id="81162-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="81162-178">a.</span><span class="sxs-lookup"><span data-stu-id="81162-178">a.</span></span> <span data-ttu-id="81162-179">Selezionare **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="81162-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="81162-180">b.</span><span class="sxs-lookup"><span data-stu-id="81162-180">b.</span></span> <span data-ttu-id="81162-181">Incolla **ID entità SAML**, che è stato copiato dal portale di Azure hello in hello **ID Provider di identità** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="81162-181">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="81162-182">c.</span><span class="sxs-lookup"><span data-stu-id="81162-182">c.</span></span> <span data-ttu-id="81162-183">Incolla **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure hello in hello **Single Sign On URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="81162-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="81162-184">d.</span><span class="sxs-lookup"><span data-stu-id="81162-184">d.</span></span> <span data-ttu-id="81162-185">Incolla **Sign-Out URL**, che è stato copiato dal portale di Azure hello in hello **Single Logout URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="81162-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="81162-186">e.</span><span class="sxs-lookup"><span data-stu-id="81162-186">e.</span></span> <span data-ttu-id="81162-187">Nella pagina Company Details hello, nella parte superiore di hello, fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="81162-187">On hello Company Details page, at hello top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="81162-188">![Dettagli dell'azienda](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Dettagli dell'azienda")</span><span class="sxs-lookup"><span data-stu-id="81162-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="81162-189">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="81162-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="81162-190">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="81162-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="81162-191">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81162-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="81162-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="81162-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="81162-193">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="81162-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="81162-195">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="81162-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="81162-196">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="81162-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81162-198">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="81162-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81162-200">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="81162-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81162-202">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="81162-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81162-204">a.</span><span class="sxs-lookup"><span data-stu-id="81162-204">a.</span></span> <span data-ttu-id="81162-205">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81162-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81162-206">b.</span><span class="sxs-lookup"><span data-stu-id="81162-206">b.</span></span> <span data-ttu-id="81162-207">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="81162-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81162-208">c.</span><span class="sxs-lookup"><span data-stu-id="81162-208">c.</span></span> <span data-ttu-id="81162-209">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="81162-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="81162-210">d.</span><span class="sxs-lookup"><span data-stu-id="81162-210">d.</span></span> <span data-ttu-id="81162-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="81162-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="81162-212">Creazione di un utente test di xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="81162-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="81162-213">In ordine tooenable Azure AD utenti toolog in tooXMatters OnDemand, è necessario eseguirne il provisioning in XMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="81162-213">In order tooenable Azure AD users toolog in tooXMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="81162-214">Nel caso di hello di XMatters OnDemand, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="81162-214">In hello case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="81162-215">eseguire un account utente, tooprovision hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="81162-215">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="81162-216">Accedi tooyour **XMatters OnDemand** tenant.</span><span class="sxs-lookup"><span data-stu-id="81162-216">Log in tooyour **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="81162-217">Fare clic su **utenti** scheda e quindi fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="81162-217">Click **Users** tab. and then click **Add User**.</span></span>
  
    <span data-ttu-id="81162-218">![Utenti](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="81162-218">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="81162-219">In hello **aggiungere un utente** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="81162-219">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="81162-220">![Aggiungere un utente](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="81162-220">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="81162-221">a.</span><span class="sxs-lookup"><span data-stu-id="81162-221">a.</span></span> <span data-ttu-id="81162-222">Selezionare **Active**.</span><span class="sxs-lookup"><span data-stu-id="81162-222">Select **Active**.</span></span>

    <span data-ttu-id="81162-223">b.</span><span class="sxs-lookup"><span data-stu-id="81162-223">b.</span></span> <span data-ttu-id="81162-224">In hello **ID utente** casella Tipo hello l'id dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="81162-224">In hello **User ID** textbox, type hello user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="81162-225">c.</span><span class="sxs-lookup"><span data-stu-id="81162-225">c.</span></span> <span data-ttu-id="81162-226">In hello **nome** casella di testo Nome tipo di utente hello come Laura.</span><span class="sxs-lookup"><span data-stu-id="81162-226">In hello **First Name** textbox, type first name of hello user like Britta.</span></span>

    <span data-ttu-id="81162-227">d.</span><span class="sxs-lookup"><span data-stu-id="81162-227">d.</span></span> <span data-ttu-id="81162-228">In hello **cognome** casella di testo, digitare cognome dell'utente hello come Simon.</span><span class="sxs-lookup"><span data-stu-id="81162-228">In hello **Last Name** textbox, type last name of hello user like Simon.</span></span>
    
    <span data-ttu-id="81162-229">e.</span><span class="sxs-lookup"><span data-stu-id="81162-229">e.</span></span> <span data-ttu-id="81162-230">In hello **sito** sito valido hello di invio di un valido Azure casella account di Active Directory, si desidera tooprovision.</span><span class="sxs-lookup"><span data-stu-id="81162-230">In hello **Site** textbox, Enter hello valid site of a valid Azure AD account you want tooprovision.</span></span>
    
    <span data-ttu-id="81162-231">f.</span><span class="sxs-lookup"><span data-stu-id="81162-231">f.</span></span> <span data-ttu-id="81162-232">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="81162-232">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="81162-233">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="81162-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="81162-234">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooxMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="81162-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooxMatters OnDemand.</span></span>

![Assegna utente][200] 

<span data-ttu-id="81162-236">**tooassign Britta Simon tooxMatters OnDemand, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="81162-236">**tooassign Britta Simon tooxMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="81162-237">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="81162-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="81162-239">Nell'elenco di applicazioni hello, selezionare **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="81162-239">In hello applications list, select **xMatters OnDemand**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="81162-241">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="81162-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="81162-243">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="81162-243">Click **Add** button.</span></span> <span data-ttu-id="81162-244">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="81162-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="81162-246">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="81162-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="81162-247">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="81162-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81162-248">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="81162-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="81162-249">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="81162-249">Testing single sign-on</span></span>

<span data-ttu-id="81162-250">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="81162-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="81162-251">Quando si fa clic hello xMatters OnDemand porzione hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in xMatters OnDemand applicazione.</span><span class="sxs-lookup"><span data-stu-id="81162-251">When you click hello xMatters OnDemand tile in hello Access Panel, you should get automatically signed-on tooyour xMatters OnDemand application.</span></span>
<span data-ttu-id="81162-252">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="81162-252">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81162-253">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="81162-253">Additional resources</span></span>

* [<span data-ttu-id="81162-254">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81162-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81162-255">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81162-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

