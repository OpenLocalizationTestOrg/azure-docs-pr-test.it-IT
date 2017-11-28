---
title: 'Esercitazione: Integrazione di Azure Active Directory con Adaptive Suite | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e i gruppi di test adattivo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="946a0-103">Esercitazione: Integrazione di Azure Active Directory con Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="946a0-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="946a0-104">In questa esercitazione, è illustrato come toointegrate Suite adattivo con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="946a0-104">In this tutorial, you learn how toointegrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="946a0-105">Integrazione Suite adattivo con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="946a0-105">Integrating Adaptive Suite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="946a0-106">È possibile controllare in Azure AD che ha accesso tooAdaptive Suite</span><span class="sxs-lookup"><span data-stu-id="946a0-106">You can control in Azure AD who has access tooAdaptive Suite</span></span>
- <span data-ttu-id="946a0-107">È possibile abilitare l'utenti tooautomatically get connesso tooAdaptive Suite (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="946a0-107">You can enable your users tooautomatically get signed-on tooAdaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="946a0-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="946a0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="946a0-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="946a0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="946a0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="946a0-110">Prerequisites</span></span>

<span data-ttu-id="946a0-111">integrazione di Azure AD con Suite adattivo tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="946a0-111">tooconfigure Azure AD integration with Adaptive Suite, you need hello following items:</span></span>

- <span data-ttu-id="946a0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="946a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="946a0-113">Sottoscrizione di Adaptive Suite abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="946a0-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="946a0-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="946a0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="946a0-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="946a0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="946a0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="946a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="946a0-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="946a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="946a0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="946a0-118">Scenario description</span></span>
<span data-ttu-id="946a0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="946a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="946a0-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="946a0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="946a0-121">Aggiunta gruppo adattivo dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="946a0-121">Adding Adaptive Suite from hello gallery</span></span>
2. <span data-ttu-id="946a0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="946a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-hello-gallery"></a><span data-ttu-id="946a0-123">Aggiunta gruppo adattivo dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="946a0-123">Adding Adaptive Suite from hello gallery</span></span>
<span data-ttu-id="946a0-124">integrazione hello tooconfigure di Suite adattiva in Azure AD, è necessario tooadd Suite adattivo dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="946a0-124">tooconfigure hello integration of Adaptive Suite into Azure AD, you need tooadd Adaptive Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="946a0-125">**tooadd adattivo Suite dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="946a0-125">**tooadd Adaptive Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="946a0-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="946a0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="946a0-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="946a0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="946a0-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="946a0-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="946a0-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="946a0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="946a0-133">Nella casella di ricerca hello, digitare **Suite adattivo**.</span><span class="sxs-lookup"><span data-stu-id="946a0-133">In hello search box, type **Adaptive Suite**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="946a0-135">Nel riquadro dei risultati hello, selezionare **Suite adattivo**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="946a0-135">In hello results panel, select **Adaptive Suite**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="946a0-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="946a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="946a0-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Adaptive Suite con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="946a0-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="946a0-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello Suite adattivo è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="946a0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adaptive Suite is tooa user in Azure AD.</span></span> <span data-ttu-id="946a0-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e utente correlato di hello Suite adattivo deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="946a0-140">In other words, a link relationship between an Azure AD user and hello related user in Adaptive Suite needs toobe established.</span></span>

<span data-ttu-id="946a0-141">Adattivo Suite, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="946a0-141">In Adaptive Suite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="946a0-142">tooconfigure e test Azure AD single sign-on con adattivo Suite, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="946a0-142">tooconfigure and test Azure AD single sign-on with Adaptive Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="946a0-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="946a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="946a0-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="946a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="946a0-145">**[Creazione di un utente test Suite adattivo](#creating-an-adaptive-suite-test-user)**  -toohave un equivalente di Britta Simon Suite adattivo rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="946a0-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - toohave a counterpart of Britta Simon in Adaptive Suite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="946a0-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="946a0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="946a0-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="946a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="946a0-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="946a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="946a0-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Suite adattivo.</span><span class="sxs-lookup"><span data-stu-id="946a0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="946a0-150">**Azure AD tooconfigure single sign-on con adattivo Suite, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="946a0-150">**tooconfigure Azure AD single sign-on with Adaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="946a0-151">Nel portale di Azure su hello hello **Suite adattivo** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="946a0-151">In hello Azure portal, on hello **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="946a0-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="946a0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="946a0-155">In hello **adattivo gruppo di dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="946a0-155">On hello **Adaptive Suite Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="946a0-157">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="946a0-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="946a0-158">È possibile ottenere questo valore dalla Suite adattivo hello **SAML SSO Settings** pagina.</span><span class="sxs-lookup"><span data-stu-id="946a0-158">You can get this value from hello Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="946a0-159">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="946a0-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="946a0-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="946a0-161">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="946a0-163">In hello **adattivo configurazione Suite** fare clic su **configurare adattivo Suite** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="946a0-163">On hello **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="946a0-164">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="946a0-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="946a0-166">In una finestra del web browser, accedere come amministratore nel sito della società di tooyour Suite adattivo.</span><span class="sxs-lookup"><span data-stu-id="946a0-166">In a different web browser window, log in tooyour Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="946a0-167">Andare troppo**Admin**.</span><span class="sxs-lookup"><span data-stu-id="946a0-167">Go too**Admin**.</span></span>
   
    <span data-ttu-id="946a0-168">![Amministratore](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="946a0-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="946a0-169">In hello **utenti e ruoli** fare clic su **gestire le impostazioni di SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="946a0-169">In hello **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="946a0-170">![Gestire le impostazioni SSO SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Gestire le impostazioni SSO SAML")</span><span class="sxs-lookup"><span data-stu-id="946a0-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="946a0-171">In hello **SAML SSO Settings** eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="946a0-171">On hello **SAML SSO Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="946a0-172">![Impostazioni SSO SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "Impostazioni SSO SAML")</span><span class="sxs-lookup"><span data-stu-id="946a0-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="946a0-173">a.</span><span class="sxs-lookup"><span data-stu-id="946a0-173">a.</span></span> <span data-ttu-id="946a0-174">In hello **nome provider di identità** casella di testo, digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="946a0-174">In hello **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="946a0-175">b.</span><span class="sxs-lookup"><span data-stu-id="946a0-175">b.</span></span> <span data-ttu-id="946a0-176">Hello Incolla **ID entità SAML** valore copiato dal portale di Azure in hello **provider di identità, ID entità** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="946a0-176">Paste hello **SAML Entity ID** value copied from Azure portal into hello **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="946a0-177">c.</span><span class="sxs-lookup"><span data-stu-id="946a0-177">c.</span></span> <span data-ttu-id="946a0-178">Hello Incolla **SAML Single Sign-On Service URL** valore copiato dal portale di Azure in hello **Identity provider URL SSO** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="946a0-178">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="946a0-179">d.</span><span class="sxs-lookup"><span data-stu-id="946a0-179">d.</span></span> <span data-ttu-id="946a0-180">Hello Incolla **SAML Single Sign-On Service URL** valore copiato dal portale di Azure in hello **URL di disconnessione personalizzato** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="946a0-180">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="946a0-181">e.</span><span class="sxs-lookup"><span data-stu-id="946a0-181">e.</span></span> <span data-ttu-id="946a0-182">tooupload il certificato scaricato, fare clic su **Choose file**.</span><span class="sxs-lookup"><span data-stu-id="946a0-182">tooupload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="946a0-183">f.</span><span class="sxs-lookup"><span data-stu-id="946a0-183">f.</span></span> <span data-ttu-id="946a0-184">Selezionare la seguente hello, per:</span><span class="sxs-lookup"><span data-stu-id="946a0-184">Select hello following, for:</span></span>
    * <span data-ttu-id="946a0-185">**SAML user id** (ID utente SAML), selezionare **User's Adaptive Insights user name** (Nome utente dell'utente di Adaptive Insights).</span><span class="sxs-lookup"><span data-stu-id="946a0-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="946a0-186">**SAML user id location** (Posizione ID utente SAML), selezionare **User id in NameID of Subject** (ID utente in NameID of Subject).</span><span class="sxs-lookup"><span data-stu-id="946a0-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="946a0-187">**SAML NameID format** (Formato NameID SAML), selezionare **Email address** (Indirizzo di posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="946a0-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="946a0-188">**Abilita SAML** selezionare **Allow SAML SSO and direct Adaptive Insights login** (Consenti SSO SAML e accesso diretto ad Adaptive Insights).</span><span class="sxs-lookup"><span data-stu-id="946a0-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="946a0-189">g.</span><span class="sxs-lookup"><span data-stu-id="946a0-189">g.</span></span> <span data-ttu-id="946a0-190">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="946a0-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="946a0-191">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="946a0-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="946a0-192">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="946a0-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="946a0-193">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="946a0-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="946a0-194">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="946a0-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="946a0-195">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="946a0-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="946a0-197">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="946a0-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="946a0-198">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="946a0-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="946a0-200">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="946a0-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="946a0-202">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="946a0-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="946a0-204">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="946a0-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="946a0-206">a.</span><span class="sxs-lookup"><span data-stu-id="946a0-206">a.</span></span> <span data-ttu-id="946a0-207">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="946a0-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="946a0-208">b.</span><span class="sxs-lookup"><span data-stu-id="946a0-208">b.</span></span> <span data-ttu-id="946a0-209">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="946a0-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="946a0-210">c.</span><span class="sxs-lookup"><span data-stu-id="946a0-210">c.</span></span> <span data-ttu-id="946a0-211">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="946a0-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="946a0-212">d.</span><span class="sxs-lookup"><span data-stu-id="946a0-212">d.</span></span> <span data-ttu-id="946a0-213">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="946a0-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="946a0-214">Creazione di un utente di test di Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="946a0-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="946a0-215">toolog agli utenti di Azure AD tooenable in tooAdaptive Suite, è necessario eseguirne il provisioning in gruppo adattivo.</span><span class="sxs-lookup"><span data-stu-id="946a0-215">tooenable Azure AD users toolog in tooAdaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="946a0-216">In caso di hello della Suite adattiva, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="946a0-216">In hello case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="946a0-217">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="946a0-217">**tooconfigure user provisioning, perform hello following steps:**</span></span> 

1. <span data-ttu-id="946a0-218">Accedi tooyour **Suite adattivo** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="946a0-218">Log in tooyour **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="946a0-219">Andare troppo**Admin**.</span><span class="sxs-lookup"><span data-stu-id="946a0-219">Go too**Admin**.</span></span>
   
   <span data-ttu-id="946a0-220">![Amministratore](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="946a0-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="946a0-221">In hello **utenti e ruoli** fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="946a0-221">In hello **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="946a0-222">![Aggiungere un utente](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="946a0-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="946a0-223">In hello **nuovo utente** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="946a0-223">In hello **New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="946a0-224">![Invio](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Invio")</span><span class="sxs-lookup"><span data-stu-id="946a0-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="946a0-225">a.</span><span class="sxs-lookup"><span data-stu-id="946a0-225">a.</span></span> <span data-ttu-id="946a0-226">Hello tipo **nome**, **accesso**, **posta elettronica**, **Password** di un utente di Azure Active Directory valido desiderate tooprovision hello correlato nelle caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="946a0-226">Type hello **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
  
   <span data-ttu-id="946a0-227">b.</span><span class="sxs-lookup"><span data-stu-id="946a0-227">b.</span></span> <span data-ttu-id="946a0-228">Selezionare un valore in **Role**.</span><span class="sxs-lookup"><span data-stu-id="946a0-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="946a0-229">c.</span><span class="sxs-lookup"><span data-stu-id="946a0-229">c.</span></span> <span data-ttu-id="946a0-230">Fare clic su **Submit**.</span><span class="sxs-lookup"><span data-stu-id="946a0-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="946a0-231">È possibile usare qualsiasi altro gruppo adattivo utente account strumento di creazione o le API fornite da tooprovision Suite adattivo account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="946a0-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="946a0-232">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="946a0-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="946a0-233">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAdaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="946a0-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdaptive Suite.</span></span>

![Assegna utente][200] 

<span data-ttu-id="946a0-235">**tooassign Britta Simon tooAdaptive Suite, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="946a0-235">**tooassign Britta Simon tooAdaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="946a0-236">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="946a0-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="946a0-238">Nell'elenco di applicazioni hello, selezionare **Suite adattivo**.</span><span class="sxs-lookup"><span data-stu-id="946a0-238">In hello applications list, select **Adaptive Suite**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="946a0-240">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="946a0-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="946a0-242">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="946a0-242">Click **Add** button.</span></span> <span data-ttu-id="946a0-243">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="946a0-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="946a0-245">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="946a0-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="946a0-246">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="946a0-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="946a0-247">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="946a0-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="946a0-248">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="946a0-248">Testing single sign-on</span></span>

<span data-ttu-id="946a0-249">obiettivo di Hello di questa sezione è tootest il servizio Microsoft Azure AD Single Sign-On configuration utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="946a0-249">hello objective of this section is tootest your Microsoft Azure AD Single Sign-On configuration using hello Access Panel.</span></span>

<span data-ttu-id="946a0-250">Quando si fa clic su riquadro Suite adattivo hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in un'applicazione Suite adattivo.</span><span class="sxs-lookup"><span data-stu-id="946a0-250">When you click hello Adaptive Suite tile in hello Access Panel, you should get automatically signed-on tooyour Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="946a0-251">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="946a0-251">Additional resources</span></span>

* [<span data-ttu-id="946a0-252">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="946a0-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="946a0-253">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="946a0-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

