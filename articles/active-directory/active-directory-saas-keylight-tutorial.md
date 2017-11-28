---
title: 'Esercitazione: Integrazione di Azure Active Directory con LockPath Keyligh | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e LockPath Keylight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="d523d-103">Esercitazione: Integrazione di Azure Active Directory con LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="d523d-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="d523d-104">In questa esercitazione, è illustrato come toointegrate LockPath Keylight con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d523d-104">In this tutorial, you learn how toointegrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d523d-105">Integrazione LockPath Keylight con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d523d-105">Integrating LockPath Keylight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d523d-106">È possibile controllare in Azure AD che ha accesso tooLockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="d523d-106">You can control in Azure AD who has access tooLockPath Keylight</span></span>
- <span data-ttu-id="d523d-107">È possibile abilitare l'utenti tooautomatically get connesso tooLockPath Keylight (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d523d-107">You can enable your users tooautomatically get signed-on tooLockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d523d-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d523d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d523d-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d523d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d523d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d523d-110">Prerequisites</span></span>

<span data-ttu-id="d523d-111">integrazione di Azure AD con LockPath Keylight tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d523d-111">tooconfigure Azure AD integration with LockPath Keylight, you need hello following items:</span></span>

- <span data-ttu-id="d523d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d523d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d523d-113">Sottoscrizione di LockPath Keylight abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d523d-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d523d-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d523d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d523d-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="d523d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d523d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d523d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d523d-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d523d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d523d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d523d-118">Scenario description</span></span>
<span data-ttu-id="d523d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d523d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d523d-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="d523d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d523d-121">Aggiunta di LockPath Keylight dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d523d-121">Adding LockPath Keylight from hello gallery</span></span>
2. <span data-ttu-id="d523d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d523d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-hello-gallery"></a><span data-ttu-id="d523d-123">Aggiunta di LockPath Keylight dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d523d-123">Adding LockPath Keylight from hello gallery</span></span>
<span data-ttu-id="d523d-124">integrazione hello tooconfigure di LockPath Keylight in Azure AD, è necessario tooadd LockPath Keylight dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d523d-124">tooconfigure hello integration of LockPath Keylight into Azure AD, you need tooadd LockPath Keylight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d523d-125">**tooadd LockPath Keylight dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d523d-125">**tooadd LockPath Keylight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d523d-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d523d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d523d-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d523d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d523d-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d523d-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d523d-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d523d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d523d-133">Nella casella di ricerca hello, digitare **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="d523d-133">In hello search box, type **LockPath Keylight**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="d523d-135">Nel riquadro dei risultati hello, selezionare **LockPath Keylight**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d523d-135">In hello results panel, select **LockPath Keylight**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d523d-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d523d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d523d-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LockPath Keylight in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d523d-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d523d-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in LockPath Keylight è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d523d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LockPath Keylight is tooa user in Azure AD.</span></span> <span data-ttu-id="d523d-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in LockPath Keylight deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="d523d-140">In other words, a link relationship between an Azure AD user and hello related user in LockPath Keylight needs toobe established.</span></span>

<span data-ttu-id="d523d-141">In LockPath Keylight, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="d523d-141">In LockPath Keylight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d523d-142">tooconfigure e prova AD Azure single sign-on con LockPath Keylight, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="d523d-142">tooconfigure and test Azure AD single sign-on with LockPath Keylight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d523d-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d523d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d523d-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d523d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d523d-145">**[Creazione di un utente test LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  -toohave un equivalente di Britta Simon in LockPath Keylight che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d523d-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - toohave a counterpart of Britta Simon in LockPath Keylight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d523d-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d523d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d523d-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="d523d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d523d-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d523d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d523d-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="d523d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="d523d-150">**Azure AD tooconfigure single sign-on con LockPath Keylight, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d523d-150">**tooconfigure Azure AD single sign-on with LockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="d523d-151">Nel portale di Azure su hello hello **LockPath Keylight** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d523d-151">In hello Azure portal, on hello **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d523d-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d523d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="d523d-155">In hello **LockPath Keylight dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d523d-155">On hello **LockPath Keylight Domain and URLs** section, perform hello following steps::</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="d523d-157">a.</span><span class="sxs-lookup"><span data-stu-id="d523d-157">a.</span></span> <span data-ttu-id="d523d-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="d523d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="d523d-159">b.</span><span class="sxs-lookup"><span data-stu-id="d523d-159">b.</span></span> <span data-ttu-id="d523d-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="d523d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="d523d-161">c.</span><span class="sxs-lookup"><span data-stu-id="d523d-161">c.</span></span> <span data-ttu-id="d523d-162">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="d523d-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="d523d-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="d523d-163">These values are not real.</span></span> <span data-ttu-id="d523d-164">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="d523d-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="d523d-165">Contatto [team di supporto Keylight Client LockPath](https://www.lockpath.com/contact/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="d523d-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="d523d-166">In hello **certificato di firma SAML** fare clic su **Certificate(Raw)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d523d-166">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="d523d-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d523d-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="d523d-170">In hello **LockPath Keylight configurazione** fare clic su **configurare LockPath Keylight** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="d523d-170">On hello **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d523d-171">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="d523d-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="d523d-173">tooenable SSO in LockPath Keylight, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d523d-173">tooenable SSO in LockPath Keylight, perform hello following steps:</span></span>
   
    <span data-ttu-id="d523d-174">a.</span><span class="sxs-lookup"><span data-stu-id="d523d-174">a.</span></span> <span data-ttu-id="d523d-175">Sign-on tooyour LockPath Keylight account come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d523d-175">Sign-on tooyour LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="d523d-176">b.</span><span class="sxs-lookup"><span data-stu-id="d523d-176">b.</span></span> <span data-ttu-id="d523d-177">Scegliere dal menu hello in primo piano hello **persona**e selezionare **Keylight installazione**.</span><span class="sxs-lookup"><span data-stu-id="d523d-177">In hello menu on hello top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="d523d-179">c.</span><span class="sxs-lookup"><span data-stu-id="d523d-179">c.</span></span> <span data-ttu-id="d523d-180">Nella visualizzazione albero hello hello sinistra, fare clic su **SAML**.</span><span class="sxs-lookup"><span data-stu-id="d523d-180">In hello treeview on hello left, click **SAML**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="d523d-182">d.</span><span class="sxs-lookup"><span data-stu-id="d523d-182">d.</span></span> <span data-ttu-id="d523d-183">In hello **impostazioni SAML** finestra di dialogo, fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="d523d-183">On hello **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="d523d-185">In hello **Modifica impostazioni di SAML** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d523d-185">On hello **Edit SAML Settings** dialog page, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="d523d-187">a.</span><span class="sxs-lookup"><span data-stu-id="d523d-187">a.</span></span> <span data-ttu-id="d523d-188">Impostare **SAML authentication** troppo**Active**.</span><span class="sxs-lookup"><span data-stu-id="d523d-188">Set **SAML authentication** too**Active**.</span></span>

    <span data-ttu-id="d523d-189">b.</span><span class="sxs-lookup"><span data-stu-id="d523d-189">b.</span></span> <span data-ttu-id="d523d-190">Hello Incolla **SAML Single Sign-On Service URL** valore a cui è stato copiato dal portale di Azure hello in hello **Identity Provider Login URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="d523d-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="d523d-191">c.</span><span class="sxs-lookup"><span data-stu-id="d523d-191">c.</span></span> <span data-ttu-id="d523d-192">Hello Incolla **URL del servizio Single Sign-Out** valore a cui è stato copiato dal portale di Azure hello in hello **Identity Provider Logout URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="d523d-192">Paste hello **Single Sign-Out Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="d523d-193">d.</span><span class="sxs-lookup"><span data-stu-id="d523d-193">d.</span></span> <span data-ttu-id="d523d-194">Fare clic su **Scegli File** tooselect certificato i LockPath Keylight scaricato, quindi fare clic su **aprire** certificato hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="d523d-194">Click **Choose File** tooselect your downloaded LockPath Keylight certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="d523d-195">e.</span><span class="sxs-lookup"><span data-stu-id="d523d-195">e.</span></span> <span data-ttu-id="d523d-196">Impostare **Id utente SAML location** troppo**elemento NameIdentifier dell'istruzione subject hello**.</span><span class="sxs-lookup"><span data-stu-id="d523d-196">Set **SAML User Id location** too**NameIdentifier element of hello subject statement**.</span></span>
    
    <span data-ttu-id="d523d-197">f.</span><span class="sxs-lookup"><span data-stu-id="d523d-197">f.</span></span> <span data-ttu-id="d523d-198">Fornire hello **Provider del servizio Keylight** utilizzando hello seguente modello: **https://&lt;CompanyName&gt;. keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="d523d-198">Provide hello **Keylight Service Provider** using hello following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="d523d-199">g.</span><span class="sxs-lookup"><span data-stu-id="d523d-199">g.</span></span> <span data-ttu-id="d523d-200">Impostare **agli utenti di eseguire il provisioning automatico** troppo**Active**.</span><span class="sxs-lookup"><span data-stu-id="d523d-200">Set **Auto-provision users** too**Active**.</span></span>

    <span data-ttu-id="d523d-201">h.</span><span class="sxs-lookup"><span data-stu-id="d523d-201">h.</span></span> <span data-ttu-id="d523d-202">Impostare **il tipo di account di provisioning automatico** troppo**utente completa**.</span><span class="sxs-lookup"><span data-stu-id="d523d-202">Set **Auto-provision account type** too**Full User**.</span></span>

    <span data-ttu-id="d523d-203">i.</span><span class="sxs-lookup"><span data-stu-id="d523d-203">i.</span></span> <span data-ttu-id="d523d-204">Impostare **Auto-provision security role** (Ruolo di sicurezza del provisioning automatico) selezionando **Standard User with SAML** (Utente standard con SAML).</span><span class="sxs-lookup"><span data-stu-id="d523d-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="d523d-205">j.</span><span class="sxs-lookup"><span data-stu-id="d523d-205">j.</span></span> <span data-ttu-id="d523d-206">Impostare **Auto-provision security config** (Configurazione di sicurezza del provisioning automatico) selezionando **Standard User Configuration** (Configurazione utente standard).</span><span class="sxs-lookup"><span data-stu-id="d523d-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="d523d-207">k.</span><span class="sxs-lookup"><span data-stu-id="d523d-207">k.</span></span> <span data-ttu-id="d523d-208">In hello **Email attribute** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="d523d-208">In hello **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="d523d-209">l.</span><span class="sxs-lookup"><span data-stu-id="d523d-209">l.</span></span> <span data-ttu-id="d523d-210">In hello **nome attributo** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="d523d-210">In hello **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="d523d-211">m.</span><span class="sxs-lookup"><span data-stu-id="d523d-211">m.</span></span> <span data-ttu-id="d523d-212">In hello **ultimo attributo nome** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="d523d-212">In hello **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="d523d-213">n.</span><span class="sxs-lookup"><span data-stu-id="d523d-213">n.</span></span> <span data-ttu-id="d523d-214">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d523d-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d523d-215">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="d523d-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d523d-216">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="d523d-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d523d-217">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d523d-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d523d-218">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d523d-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="d523d-219">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d523d-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d523d-221">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d523d-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d523d-222">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d523d-222">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d523d-224">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="d523d-224">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d523d-226">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="d523d-226">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d523d-228">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d523d-228">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d523d-230">a.</span><span class="sxs-lookup"><span data-stu-id="d523d-230">a.</span></span> <span data-ttu-id="d523d-231">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d523d-231">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d523d-232">b.</span><span class="sxs-lookup"><span data-stu-id="d523d-232">b.</span></span> <span data-ttu-id="d523d-233">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d523d-233">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d523d-234">c.</span><span class="sxs-lookup"><span data-stu-id="d523d-234">c.</span></span> <span data-ttu-id="d523d-235">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="d523d-235">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d523d-236">d.</span><span class="sxs-lookup"><span data-stu-id="d523d-236">d.</span></span> <span data-ttu-id="d523d-237">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d523d-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="d523d-238">Creazione di un utente test di LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="d523d-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="d523d-239">In questa sezione si crea un utente chiamato Britta Simon in LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="d523d-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="d523d-240">LockPath Keylight supporta il provisioning JIT, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d523d-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="d523d-241">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="d523d-241">There is no action item for you in this section.</span></span> <span data-ttu-id="d523d-242">Quando si accede a LockPath Keylight se utente hello non esiste ancora, viene creato un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="d523d-242">A new user is created when accessing LockPath Keylight if hello user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="d523d-243">Se è necessario un utente toocreate manualmente, è necessario hello toocontact [team di supporto Keylight Client LockPath](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="d523d-243">If you need toocreate a user manually, you need toocontact hello [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d523d-244">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d523d-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d523d-245">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="d523d-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLockPath Keylight.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d523d-247">**tooassign Britta Simon tooLockPath Keylight, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d523d-247">**tooassign Britta Simon tooLockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="d523d-248">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d523d-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d523d-250">Nell'elenco di applicazioni hello, selezionare **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="d523d-250">In hello applications list, select **LockPath Keylight**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="d523d-252">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d523d-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d523d-254">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d523d-254">Click **Add** button.</span></span> <span data-ttu-id="d523d-255">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d523d-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d523d-257">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="d523d-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d523d-258">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d523d-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d523d-259">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d523d-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d523d-260">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d523d-260">Testing single sign-on</span></span>

<span data-ttu-id="d523d-261">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d523d-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d523d-262">Quando si fa clic hello LockPath Keylight riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour LockPath Keylight applicazione.</span><span class="sxs-lookup"><span data-stu-id="d523d-262">When you click hello LockPath Keylight tile in hello Access Panel, you should get automatically signed-on tooyour LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d523d-263">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d523d-263">Additional resources</span></span>

* [<span data-ttu-id="d523d-264">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d523d-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d523d-265">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d523d-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

