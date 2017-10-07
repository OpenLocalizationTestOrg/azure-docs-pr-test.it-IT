---
title: 'Esercitazione: Integrazione di Azure Active Directory con PolicyStat | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e PolicyStat.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="937ea-103">Esercitazione: Integrazione di Azure Active Directory con PolicyStat</span><span class="sxs-lookup"><span data-stu-id="937ea-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="937ea-104">In questa esercitazione, è illustrato come toointegrate PolicyStat con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="937ea-104">In this tutorial, you learn how toointegrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="937ea-105">Integrazione PolicyStat con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="937ea-105">Integrating PolicyStat with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="937ea-106">È possibile controllare in Azure AD che ha accesso tooPolicyStat</span><span class="sxs-lookup"><span data-stu-id="937ea-106">You can control in Azure AD who has access tooPolicyStat</span></span>
- <span data-ttu-id="937ea-107">È possibile abilitare l'utenti tooautomatically get connesso tooPolicyStat (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="937ea-107">You can enable your users tooautomatically get signed-on tooPolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="937ea-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="937ea-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="937ea-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="937ea-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="937ea-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="937ea-110">Prerequisites</span></span>

<span data-ttu-id="937ea-111">integrazione di Azure AD con PolicyStat tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="937ea-111">tooconfigure Azure AD integration with PolicyStat, you need hello following items:</span></span>

- <span data-ttu-id="937ea-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="937ea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="937ea-113">Sottoscrizione di PolicyStat abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="937ea-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="937ea-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="937ea-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="937ea-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="937ea-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="937ea-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="937ea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="937ea-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="937ea-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="937ea-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="937ea-118">Scenario description</span></span>
<span data-ttu-id="937ea-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="937ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="937ea-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="937ea-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="937ea-121">Aggiunta di PolicyStat dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="937ea-121">Adding PolicyStat from hello gallery</span></span>
2. <span data-ttu-id="937ea-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="937ea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-hello-gallery"></a><span data-ttu-id="937ea-123">Aggiunta di PolicyStat dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="937ea-123">Adding PolicyStat from hello gallery</span></span>
<span data-ttu-id="937ea-124">integrazione hello tooconfigure di PolicyStat in Azure AD, è necessario tooadd PolicyStat dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="937ea-124">tooconfigure hello integration of PolicyStat into Azure AD, you need tooadd PolicyStat from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="937ea-125">**tooadd PolicyStat dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="937ea-125">**tooadd PolicyStat from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="937ea-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="937ea-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="937ea-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="937ea-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="937ea-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="937ea-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="937ea-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="937ea-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="937ea-133">Nella casella di ricerca hello, digitare **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="937ea-133">In hello search box, type **PolicyStat**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="937ea-135">Nel riquadro dei risultati hello, selezionare **PolicyStat**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="937ea-135">In hello results panel, select **PolicyStat**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="937ea-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="937ea-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="937ea-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con PolicyStat con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="937ea-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="937ea-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in PolicyStat è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="937ea-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PolicyStat is tooa user in Azure AD.</span></span> <span data-ttu-id="937ea-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in PolicyStat deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="937ea-140">In other words, a link relationship between an Azure AD user and hello related user in PolicyStat needs toobe established.</span></span>

<span data-ttu-id="937ea-141">In PolicyStat, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="937ea-141">In PolicyStat, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="937ea-142">tooconfigure e prova AD Azure single sign-on con PolicyStat, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="937ea-142">tooconfigure and test Azure AD single sign-on with PolicyStat, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="937ea-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="937ea-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="937ea-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="937ea-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="937ea-145">**[Creazione di un utente test PolicyStat](#creating-a-policystat-test-user)**  -toohave un equivalente di Britta Simon in PolicyStat che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="937ea-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - toohave a counterpart of Britta Simon in PolicyStat that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="937ea-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="937ea-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="937ea-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="937ea-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="937ea-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="937ea-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="937ea-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="937ea-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="937ea-150">**Azure AD tooconfigure single sign-on con PolicyStat, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="937ea-150">**tooconfigure Azure AD single sign-on with PolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="937ea-151">Nel portale di Azure su hello hello **PolicyStat** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="937ea-151">In hello Azure portal, on hello **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="937ea-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="937ea-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="937ea-155">In hello **PolicyStat dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="937ea-155">On hello **PolicyStat Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="937ea-157">a.</span><span class="sxs-lookup"><span data-stu-id="937ea-157">a.</span></span> <span data-ttu-id="937ea-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="937ea-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="937ea-159">b.</span><span class="sxs-lookup"><span data-stu-id="937ea-159">b.</span></span> <span data-ttu-id="937ea-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="937ea-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="937ea-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="937ea-161">These values are not real.</span></span> <span data-ttu-id="937ea-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="937ea-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="937ea-163">Contatto [team di supporto PolicyStat Client](http://www.policystat.com/support/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="937ea-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="937ea-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="937ea-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="937ea-166">obiettivo di Hello di questa sezione è toooutline come tooenable utenti tooauthenticate tooPolicyStat con il proprio account in Azure AD usando la federazione basata sul protocollo SAML hello.</span><span class="sxs-lookup"><span data-stu-id="937ea-166">hello objective of this section is toooutline how tooenable users tooauthenticate tooPolicyStat with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="937ea-167">Hello PolicyStat applicazione prevede di asserzioni SAML hello in un formato specifico, che richiede il tooyour mapping di attributi personalizzati tooadd **attributi Token SAML** configurazione.</span><span class="sxs-lookup"><span data-stu-id="937ea-167">hello PolicyStat application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="937ea-168">Hello seguente schermata mostra un esempio di questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="937ea-168">hello following screenshot shows an example of this.</span></span>

     <span data-ttu-id="937ea-169">![Attributi](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributi")</span><span class="sxs-lookup"><span data-stu-id="937ea-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="937ea-170">mapping di attributi tooadd hello necessario, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="937ea-170">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="937ea-171">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="937ea-171">Attribute Name</span></span>    |   <span data-ttu-id="937ea-172">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="937ea-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="937ea-173">uid</span><span class="sxs-lookup"><span data-stu-id="937ea-173">uid</span></span> | <span data-ttu-id="937ea-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="937ea-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="937ea-175">a.</span><span class="sxs-lookup"><span data-stu-id="937ea-175">a.</span></span> <span data-ttu-id="937ea-176">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="937ea-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="937ea-179">b.</span><span class="sxs-lookup"><span data-stu-id="937ea-179">b.</span></span> <span data-ttu-id="937ea-180">In hello **nome dell'attributo** casella tipo **uid**.</span><span class="sxs-lookup"><span data-stu-id="937ea-180">In hello **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="937ea-181">c.</span><span class="sxs-lookup"><span data-stu-id="937ea-181">c.</span></span> <span data-ttu-id="937ea-182">In hello **valore dell'attributo** casella di testo, seleziona **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="937ea-182">In hello **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="937ea-183">d.</span><span class="sxs-lookup"><span data-stu-id="937ea-183">d.</span></span> <span data-ttu-id="937ea-184">Da hello **posta** elenco, selezionare **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="937ea-184">From hello **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="937ea-185">e.</span><span class="sxs-lookup"><span data-stu-id="937ea-185">e.</span></span> <span data-ttu-id="937ea-186">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="937ea-186">Click **Ok**</span></span>

7. <span data-ttu-id="937ea-187">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="937ea-187">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="937ea-189">In un'altra finestra del Web browser accedere al sito aziendale di PolicyStat come amministratore.</span><span class="sxs-lookup"><span data-stu-id="937ea-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="937ea-190">Fare clic su hello **Admin** scheda e quindi fare clic su **configurazione Single Sign-On** nel riquadro di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="937ea-190">Click hello **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="937ea-191">![Menu amministratore](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menu amministratore")</span><span class="sxs-lookup"><span data-stu-id="937ea-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="937ea-192">In hello **installazione** selezionare **integrazione Enable Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="937ea-192">In hello **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="937ea-193">![Configurazione Single Sign-on](./media/active-directory-saas-policystat-tutorial/ic808634.png "Configurazione Single Sign-on")</span><span class="sxs-lookup"><span data-stu-id="937ea-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="937ea-194">Fare clic su **configurazione attributi**, quindi nel hello **configurazione attributi** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="937ea-194">Click **Configure Attributes**, and then, in hello **Configure Attributes** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="937ea-195">![Configurazione Single Sign-on](./media/active-directory-saas-policystat-tutorial/ic808635.png "Configurazione Single Sign-on")</span><span class="sxs-lookup"><span data-stu-id="937ea-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="937ea-196">a.</span><span class="sxs-lookup"><span data-stu-id="937ea-196">a.</span></span> <span data-ttu-id="937ea-197">In hello **attributo Username** casella tipo **uid**.</span><span class="sxs-lookup"><span data-stu-id="937ea-197">In hello **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="937ea-198">b.</span><span class="sxs-lookup"><span data-stu-id="937ea-198">b.</span></span> <span data-ttu-id="937ea-199">In hello **First Name Attribute** casella tipo **firstname** dell'utente **Laura**.</span><span class="sxs-lookup"><span data-stu-id="937ea-199">In hello **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="937ea-200">c.</span><span class="sxs-lookup"><span data-stu-id="937ea-200">c.</span></span> <span data-ttu-id="937ea-201">In hello **Last Name Attribute** casella tipo **lastname** dell'utente **Simon**.</span><span class="sxs-lookup"><span data-stu-id="937ea-201">In hello **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="937ea-202">d.</span><span class="sxs-lookup"><span data-stu-id="937ea-202">d.</span></span> <span data-ttu-id="937ea-203">In hello **Email Attribute** casella tipo **emailaddress** dell'utente  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="937ea-203">In hello **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="937ea-204">e.</span><span class="sxs-lookup"><span data-stu-id="937ea-204">e.</span></span> <span data-ttu-id="937ea-205">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="937ea-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="937ea-206">Fare clic su **Your IDP Metadata**, quindi nel hello **Your IDP Metadata** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="937ea-206">Click **Your IDP Metadata**, and then, in hello **Your IDP Metadata** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="937ea-207">![Configurazione Single Sign-on](./media/active-directory-saas-policystat-tutorial/ic808636.png "Configurazione Single Sign-on")</span><span class="sxs-lookup"><span data-stu-id="937ea-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="937ea-208">a.</span><span class="sxs-lookup"><span data-stu-id="937ea-208">a.</span></span> <span data-ttu-id="937ea-209">Aprire il file di metadati scaricato, hello copia del contenuto e quindi incollarlo hello **i metadati del Provider di identità** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="937ea-209">Open your downloaded metadata file, copy hello content, and  then paste it into hello **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="937ea-210">b.</span><span class="sxs-lookup"><span data-stu-id="937ea-210">b.</span></span> <span data-ttu-id="937ea-211">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="937ea-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="937ea-212">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="937ea-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="937ea-213">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="937ea-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="937ea-214">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="937ea-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="937ea-215">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="937ea-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="937ea-216">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="937ea-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="937ea-218">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="937ea-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="937ea-219">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="937ea-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="937ea-221">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="937ea-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="937ea-223">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="937ea-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="937ea-225">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="937ea-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="937ea-227">a.</span><span class="sxs-lookup"><span data-stu-id="937ea-227">a.</span></span> <span data-ttu-id="937ea-228">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="937ea-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="937ea-229">b.</span><span class="sxs-lookup"><span data-stu-id="937ea-229">b.</span></span> <span data-ttu-id="937ea-230">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="937ea-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="937ea-231">c.</span><span class="sxs-lookup"><span data-stu-id="937ea-231">c.</span></span> <span data-ttu-id="937ea-232">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="937ea-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="937ea-233">d.</span><span class="sxs-lookup"><span data-stu-id="937ea-233">d.</span></span> <span data-ttu-id="937ea-234">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="937ea-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="937ea-235">Creazione di un utente di test di PolicyStat</span><span class="sxs-lookup"><span data-stu-id="937ea-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="937ea-236">In ordine tooenable Azure AD utenti toolog in PolicyStat, è necessario eseguirne il provisioning in PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="937ea-236">In order tooenable Azure AD users toolog into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="937ea-237">PolicyStat supporta solo il provisioning JIT dell'utente.</span><span class="sxs-lookup"><span data-stu-id="937ea-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="937ea-238">Ciò significa, non richiedono manualmente gli utenti di hello tooadd tooPolicyStat.</span><span class="sxs-lookup"><span data-stu-id="937ea-238">This means, you do not need tooadd hello users manually tooPolicyStat.</span></span> <span data-ttu-id="937ea-239">gli utenti di Hello verranno ottenere aggiunto automaticamente al primo accesso tramite SSO.</span><span class="sxs-lookup"><span data-stu-id="937ea-239">hello users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="937ea-240">È possibile usare qualsiasi altro PolicyStat utente account strumento di creazione o le API fornite da PolicyStat tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="937ea-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="937ea-241">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="937ea-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="937ea-242">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPolicyStat.</span><span class="sxs-lookup"><span data-stu-id="937ea-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPolicyStat.</span></span>

![Assegna utente][200] 

<span data-ttu-id="937ea-244">**tooassign Britta Simon tooPolicyStat, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="937ea-244">**tooassign Britta Simon tooPolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="937ea-245">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="937ea-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="937ea-247">Nell'elenco di applicazioni hello, selezionare **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="937ea-247">In hello applications list, select **PolicyStat**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="937ea-249">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="937ea-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="937ea-251">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="937ea-251">Click **Add** button.</span></span> <span data-ttu-id="937ea-252">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="937ea-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="937ea-254">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="937ea-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="937ea-255">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="937ea-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="937ea-256">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="937ea-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="937ea-257">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="937ea-257">Testing single sign-on</span></span>

<span data-ttu-id="937ea-258">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="937ea-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="937ea-259">Quando si fa clic su riquadro PolicyStat hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour PolicyStat applicazione.</span><span class="sxs-lookup"><span data-stu-id="937ea-259">When you click hello PolicyStat tile in hello Access Panel, you should get automatically signed-on tooyour PolicyStat application.</span></span>
<span data-ttu-id="937ea-260">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="937ea-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="937ea-261">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="937ea-261">Additional resources</span></span>

* [<span data-ttu-id="937ea-262">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="937ea-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="937ea-263">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="937ea-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

