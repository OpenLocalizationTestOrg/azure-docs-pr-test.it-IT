---
title: 'Esercitazione: Integrazione di Azure Active Directory con Adobe Sign | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e il segno di Adobe.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="afa47-103">Esercitazione: Integrazione di Azure Active Directory con Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="afa47-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="afa47-104">In questa esercitazione, è illustrato come toointegrate Adobe accedere con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="afa47-104">In this tutorial, you learn how toointegrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="afa47-105">Integrazione di Adobe accesso con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="afa47-105">Integrating Adobe Sign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="afa47-106">È possibile controllare in Azure AD che ha accesso tooAdobe Sign</span><span class="sxs-lookup"><span data-stu-id="afa47-106">You can control in Azure AD who has access tooAdobe Sign</span></span>
- <span data-ttu-id="afa47-107">È possibile abilitare l'utenti tooautomatically get connesso tooAdobe Sign (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa47-107">You can enable your users tooautomatically get signed-on tooAdobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="afa47-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="afa47-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="afa47-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="afa47-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afa47-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="afa47-110">Prerequisites</span></span>

<span data-ttu-id="afa47-111">integrazione di Azure AD con il segno di Adobe tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="afa47-111">tooconfigure Azure AD integration with Adobe Sign, you need hello following items:</span></span>

- <span data-ttu-id="afa47-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afa47-112">An Azure AD subscription</span></span>
- <span data-ttu-id="afa47-113">Sottoscrizione di Adobe Sign abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="afa47-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="afa47-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="afa47-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="afa47-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="afa47-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="afa47-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="afa47-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="afa47-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="afa47-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="afa47-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="afa47-118">Scenario description</span></span>
<span data-ttu-id="afa47-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="afa47-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="afa47-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="afa47-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="afa47-121">Aggiunta di accesso Adobe dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="afa47-121">Adding Adobe Sign from hello gallery</span></span>
2. <span data-ttu-id="afa47-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa47-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-hello-gallery"></a><span data-ttu-id="afa47-123">Aggiunta di accesso Adobe dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="afa47-123">Adding Adobe Sign from hello gallery</span></span>
<span data-ttu-id="afa47-124">integrazione hello tooconfigure di Adobe Sign in Azure AD, è necessario tooadd Adobe accesso dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="afa47-124">tooconfigure hello integration of Adobe Sign into Azure AD, you need tooadd Adobe Sign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="afa47-125">**tooadd accesso Adobe dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="afa47-125">**tooadd Adobe Sign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="afa47-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="afa47-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="afa47-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="afa47-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="afa47-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="afa47-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="afa47-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="afa47-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="afa47-133">Nella casella di ricerca hello, digitare **accesso Adobe**.</span><span class="sxs-lookup"><span data-stu-id="afa47-133">In hello search box, type **Adobe Sign**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="afa47-135">Nel riquadro dei risultati hello, selezionare **accesso Adobe**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="afa47-135">In hello results panel, select **Adobe Sign**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="afa47-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa47-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="afa47-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Adobe Sign usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="afa47-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="afa47-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello Adobe segno è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afa47-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Sign is tooa user in Azure AD.</span></span> <span data-ttu-id="afa47-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e utente correlato di hello in Adobe Sign richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="afa47-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Sign needs toobe established.</span></span>

<span data-ttu-id="afa47-141">Segno di Adobe, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="afa47-141">In Adobe Sign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="afa47-142">tooconfigure e prova AD Azure single sign-on con il segno di Adobe, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="afa47-142">tooconfigure and test Azure AD single sign-on with Adobe Sign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="afa47-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="afa47-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="afa47-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="afa47-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="afa47-145">**[Creazione di un utente di test di accesso Adobe](#creating-an-adobe-sign-test-user)**  -toohave un equivalente di Britta Simon segno Adobe che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="afa47-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - toohave a counterpart of Britta Simon in Adobe Sign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="afa47-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="afa47-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="afa47-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="afa47-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="afa47-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa47-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="afa47-149">In questa sezione si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="afa47-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="afa47-150">**tooconfigure AD Azure single sign-on con il segno di Adobe, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="afa47-150">**tooconfigure Azure AD single sign-on with Adobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="afa47-151">Nel portale di Azure su hello hello **accesso Adobe** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="afa47-151">In hello Azure portal, on hello **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="afa47-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="afa47-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="afa47-155">In hello **URL e il dominio di accesso Adobe** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="afa47-155">On hello **Adobe Sign Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="afa47-157">a.</span><span class="sxs-lookup"><span data-stu-id="afa47-157">a.</span></span> <span data-ttu-id="afa47-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="afa47-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="afa47-159">b.</span><span class="sxs-lookup"><span data-stu-id="afa47-159">b.</span></span> <span data-ttu-id="afa47-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="afa47-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="afa47-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="afa47-161">These values are not real.</span></span> <span data-ttu-id="afa47-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="afa47-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="afa47-163">Contatto [team di supporto Client di accesso Adobe](https://helpx.adobe.com/in/contact/support.html) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="afa47-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="afa47-164">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="afa47-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="afa47-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="afa47-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="afa47-168">In hello **configurazione accesso Adobe** fare clic su **configurare accesso Adobe** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="afa47-168">On hello **Adobe Sign Configuration** section, click **Configure Adobe Sign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="afa47-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="afa47-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="afa47-171">In una finestra del web browser, accedere come amministratore nel sito della società di accesso Adobe tooyour.</span><span class="sxs-lookup"><span data-stu-id="afa47-171">In a different web browser window, log in tooyour Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="afa47-172">Scegliere hello menu in alto hello **Account**, quindi, nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **impostazioni SAML** in **impostazioni Account**.</span><span class="sxs-lookup"><span data-stu-id="afa47-172">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="afa47-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span><span class="sxs-lookup"><span data-stu-id="afa47-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="afa47-174">Nella sezione Impostazioni SAML hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="afa47-174">In hello SAML Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="afa47-175">![Impostazioni SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "Impostazioni SAML")</span><span class="sxs-lookup"><span data-stu-id="afa47-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="afa47-176">a.</span><span class="sxs-lookup"><span data-stu-id="afa47-176">a.</span></span> <span data-ttu-id="afa47-177">Per **SAML Mode** (Modalità SAML), selezionare **SAML Mandatory** (SAML obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="afa47-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="afa47-178">b.</span><span class="sxs-lookup"><span data-stu-id="afa47-178">b.</span></span> <span data-ttu-id="afa47-179">Selezionare **toolog Allow EchoSign Account Administrators con le credenziali EchoSign**.</span><span class="sxs-lookup"><span data-stu-id="afa47-179">Select **Allow EchoSign Account Administrators toolog in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="afa47-180">c.</span><span class="sxs-lookup"><span data-stu-id="afa47-180">c.</span></span> <span data-ttu-id="afa47-181">In **User Creation** (Creazione utente), selezionare **Automatically add users authenticated through SAML** (Aggiungi automaticamente gli utenti autenticati tramite SAML).</span><span class="sxs-lookup"><span data-stu-id="afa47-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="afa47-182">Spostare, eseguire hello seguendo i passaggi:</span><span class="sxs-lookup"><span data-stu-id="afa47-182">Move on, performing hello following steps:</span></span>

       <span data-ttu-id="afa47-183">![Impostazioni SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "Impostazioni SAML")</span><span class="sxs-lookup"><span data-stu-id="afa47-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="afa47-184">a.</span><span class="sxs-lookup"><span data-stu-id="afa47-184">a.</span></span> <span data-ttu-id="afa47-185">Incolla **ID entità SAML**, che è stato copiato dal portale di Azure in hello **IdP Entity ID** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="afa47-185">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="afa47-186">b.</span><span class="sxs-lookup"><span data-stu-id="afa47-186">b.</span></span> <span data-ttu-id="afa47-187">Incolla **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure in hello **IdP Login URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="afa47-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into hello **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="afa47-188">c.</span><span class="sxs-lookup"><span data-stu-id="afa47-188">c.</span></span> <span data-ttu-id="afa47-189">Incolla **Sign-Out URL**, che è stato copiato dal portale di Azure in hello **IdP Logout URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="afa47-189">Paste **Sign-Out URL**, which you have copied from Azure portal into hello **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="afa47-190">d.</span><span class="sxs-lookup"><span data-stu-id="afa47-190">d.</span></span> <span data-ttu-id="afa47-191">Aprire lo scaricato **Certificate(Base64)** file nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **IdP Certificate** casella di testo</span><span class="sxs-lookup"><span data-stu-id="afa47-191">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Certificate** textbox</span></span>

    <span data-ttu-id="afa47-192">e.</span><span class="sxs-lookup"><span data-stu-id="afa47-192">e.</span></span> <span data-ttu-id="afa47-193">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="afa47-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="afa47-194">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="afa47-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="afa47-195">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="afa47-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="afa47-196">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="afa47-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="afa47-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa47-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="afa47-198">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="afa47-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="afa47-200">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="afa47-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="afa47-201">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="afa47-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="afa47-203">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="afa47-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="afa47-205">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="afa47-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="afa47-207">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="afa47-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="afa47-209">a.</span><span class="sxs-lookup"><span data-stu-id="afa47-209">a.</span></span> <span data-ttu-id="afa47-210">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="afa47-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="afa47-211">b.</span><span class="sxs-lookup"><span data-stu-id="afa47-211">b.</span></span> <span data-ttu-id="afa47-212">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="afa47-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="afa47-213">c.</span><span class="sxs-lookup"><span data-stu-id="afa47-213">c.</span></span> <span data-ttu-id="afa47-214">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="afa47-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="afa47-215">d.</span><span class="sxs-lookup"><span data-stu-id="afa47-215">d.</span></span> <span data-ttu-id="afa47-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="afa47-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="afa47-217">Creazione di un utente di test di Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="afa47-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="afa47-218">toolog agli utenti di Azure AD tooenable in tooAdobe Sign, è necessario eseguirne il provisioning in Adobe Sign.</span><span class="sxs-lookup"><span data-stu-id="afa47-218">tooenable Azure AD users toolog in tooAdobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="afa47-219">In caso di hello del segno di Adobe, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="afa47-219">In hello case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="afa47-220">È possibile usare qualsiasi altro accesso Adobe utente account strumento di creazione o qualsiasi API fornita da Adobe Sign tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="afa47-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="afa47-221">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="afa47-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="afa47-222">Accedi tooyour **accesso Adobe** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="afa47-222">Log in tooyour **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="afa47-223">Scegliere dal menu hello in primo piano hello **Account**, quindi, nel riquadro di spostamento hello sul lato sinistro di hello, fare clic su **utenti e gruppi**e quindi fare clic su **creare un nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="afa47-223">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="afa47-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span><span class="sxs-lookup"><span data-stu-id="afa47-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="afa47-225">In hello **Create New User** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="afa47-225">In hello **Create New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="afa47-226">![Crea utente](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Crea utente")</span><span class="sxs-lookup"><span data-stu-id="afa47-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="afa47-227">a.</span><span class="sxs-lookup"><span data-stu-id="afa47-227">a.</span></span> <span data-ttu-id="afa47-228">Hello tipo **indirizzo di posta elettronica**, **nome**, e **cognome** di un account aAd di cui si desidera tooprovision in hello relative caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="afa47-228">Type hello **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="afa47-229">b.</span><span class="sxs-lookup"><span data-stu-id="afa47-229">b.</span></span> <span data-ttu-id="afa47-230">Fare clic su **Create User**.</span><span class="sxs-lookup"><span data-stu-id="afa47-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="afa47-231">titolare dell'account di Azure Active Directory Hello riceve un messaggio di posta elettronica che include un account di hello tooconfirm collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="afa47-231">hello Azure Active Directory account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="afa47-232">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa47-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="afa47-233">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooAdobe Sign.</span><span class="sxs-lookup"><span data-stu-id="afa47-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdobe Sign.</span></span>

![Assegna utente][200] 

<span data-ttu-id="afa47-235">**tooassign Britta Simon tooAdobe Sign, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="afa47-235">**tooassign Britta Simon tooAdobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="afa47-236">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="afa47-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="afa47-238">Nell'elenco di applicazioni hello, selezionare **accesso Adobe**.</span><span class="sxs-lookup"><span data-stu-id="afa47-238">In hello applications list, select **Adobe Sign**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="afa47-240">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="afa47-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="afa47-242">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="afa47-242">Click **Add** button.</span></span> <span data-ttu-id="afa47-243">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="afa47-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="afa47-245">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="afa47-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="afa47-246">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="afa47-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="afa47-247">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="afa47-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="afa47-248">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="afa47-248">Testing single sign-on</span></span>

<span data-ttu-id="afa47-249">Quando si fa clic hello accesso Adobe riquadro in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in applicazioni di accesso di Adobe.</span><span class="sxs-lookup"><span data-stu-id="afa47-249">When you click hello Adobe Sign tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Sign application.</span></span>
<span data-ttu-id="afa47-250">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="afa47-250">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="afa47-251">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="afa47-251">Additional resources</span></span>

* [<span data-ttu-id="afa47-252">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="afa47-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="afa47-253">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="afa47-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

