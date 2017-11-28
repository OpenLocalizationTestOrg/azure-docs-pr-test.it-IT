---
title: 'Esercitazione: Integrazione di Azure Active Directory con UserVoice | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e UserVoice.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="ab253-103">Esercitazione: Integrazione di Azure Active Directory con UserVoice</span><span class="sxs-lookup"><span data-stu-id="ab253-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="ab253-104">In questa esercitazione, è illustrato come toointegrate UserVoice con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ab253-104">In this tutorial, you learn how toointegrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ab253-105">Integrazione di UserVoice con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="ab253-105">Integrating UserVoice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ab253-106">È possibile controllare in Azure AD che ha accesso tooUserVoice.</span><span class="sxs-lookup"><span data-stu-id="ab253-106">You can control in Azure AD who has access tooUserVoice.</span></span>
- <span data-ttu-id="ab253-107">È possibile abilitare l'utenti tooautomatically get connesso tooUserVoice (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab253-107">You can enable your users tooautomatically get signed-on tooUserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ab253-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab253-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="ab253-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ab253-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab253-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ab253-110">Prerequisites</span></span>

<span data-ttu-id="ab253-111">integrazione di Azure AD con UserVoice tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ab253-111">tooconfigure Azure AD integration with UserVoice, you need hello following items:</span></span>

- <span data-ttu-id="ab253-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab253-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ab253-113">Sottoscrizione di UserVoice abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ab253-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ab253-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ab253-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ab253-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="ab253-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ab253-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ab253-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ab253-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ab253-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ab253-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ab253-118">Scenario description</span></span>
<span data-ttu-id="ab253-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ab253-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ab253-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="ab253-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ab253-121">Aggiunta di UserVoice dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ab253-121">Adding UserVoice from hello gallery</span></span>
2. <span data-ttu-id="ab253-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab253-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-hello-gallery"></a><span data-ttu-id="ab253-123">Aggiunta di UserVoice dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ab253-123">Adding UserVoice from hello gallery</span></span>
<span data-ttu-id="ab253-124">integrazione hello tooconfigure di UserVoice in Azure AD, è necessario tooadd UserVoice dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ab253-124">tooconfigure hello integration of UserVoice into Azure AD, you need tooadd UserVoice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ab253-125">**tooadd UserVoice dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ab253-125">**tooadd UserVoice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab253-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ab253-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="ab253-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ab253-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ab253-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ab253-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="ab253-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ab253-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="ab253-133">Nella casella di ricerca hello, digitare **UserVoice**selezionare **UserVoice** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ab253-133">In hello search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ab253-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab253-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ab253-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con UserVoice in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ab253-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ab253-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in UserVoice è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab253-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserVoice is tooa user in Azure AD.</span></span> <span data-ttu-id="ab253-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in UserVoice richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="ab253-138">In other words, a link relationship between an Azure AD user and hello related user in UserVoice needs toobe established.</span></span>

<span data-ttu-id="ab253-139">In UserVoice, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="ab253-139">In UserVoice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ab253-140">tooconfigure e prova AD Azure single sign-on con UserVoice, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="ab253-140">tooconfigure and test Azure AD single sign-on with UserVoice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ab253-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ab253-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ab253-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ab253-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ab253-143">**[Creare un utente test UserVoice](#create-a-uservoice-test-user)**  -toohave un equivalente di Britta Simon in UserVoice che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ab253-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - toohave a counterpart of Britta Simon in UserVoice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ab253-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ab253-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ab253-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="ab253-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ab253-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab253-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ab253-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione UserVoice.</span><span class="sxs-lookup"><span data-stu-id="ab253-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="ab253-148">**Azure AD tooconfigure single sign-on con UserVoice, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ab253-148">**tooconfigure Azure AD single sign-on with UserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab253-149">Nel portale di Azure su hello hello **UserVoice** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ab253-149">In hello Azure portal, on hello **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="ab253-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ab253-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="ab253-153">In hello **UserVoice dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ab253-153">On hello **UserVoice Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni sull'accesso Single Sign-On per URL e dominio di UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="ab253-155">a.</span><span class="sxs-lookup"><span data-stu-id="ab253-155">a.</span></span> <span data-ttu-id="ab253-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="ab253-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="ab253-157">b.</span><span class="sxs-lookup"><span data-stu-id="ab253-157">b.</span></span> <span data-ttu-id="ab253-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="ab253-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ab253-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="ab253-159">These values are not real.</span></span> <span data-ttu-id="ab253-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="ab253-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ab253-161">Contatto [team di supporto Client di UserVoice](https://www.uservoice.com/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="ab253-161">Contact [UserVoice Client support team](https://www.uservoice.com/) tooget these values.</span></span>

4. <span data-ttu-id="ab253-162">In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore del certificato.</span><span class="sxs-lookup"><span data-stu-id="ab253-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="ab253-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ab253-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ab253-166">In hello **UserVoice configurazione** fare clic su **configurare UserVoice** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="ab253-166">On hello **UserVoice Configuration** section, click **Configure UserVoice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ab253-167">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="ab253-167">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="ab253-169">In una finestra del web browser, accedere come amministratore nel sito aziendale UserVoice di tooyour.</span><span class="sxs-lookup"><span data-stu-id="ab253-169">In a different web browser window, log in tooyour UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="ab253-170">Nella barra degli strumenti hello in primo piano hello, fare clic su **impostazioni**, quindi selezionare **portale Web** dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="ab253-170">In hello toolbar on hello top, click **Settings**, and then select **Web portal** from hello menu.</span></span>
   
    <span data-ttu-id="ab253-171">![Sezione Impostazioni sul lato dell'app](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="ab253-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="ab253-172">In hello **portale Web** scheda hello **l'autenticazione utente** fare clic su **modifica** tooopen hello **Edit User Authentication** finestra di dialogo pagina.</span><span class="sxs-lookup"><span data-stu-id="ab253-172">On hello **Web portal** tab, in hello **User authentication** section, click **Edit** tooopen hello **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="ab253-173">![Scheda Portale Web](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Portale Web")</span><span class="sxs-lookup"><span data-stu-id="ab253-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="ab253-174">In hello **Edit User Authentication** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ab253-174">On hello **Edit User Authentication** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="ab253-175">![Modificare l'autenticazione utente](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Modificare l'autenticazione utente")</span><span class="sxs-lookup"><span data-stu-id="ab253-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="ab253-176">a.</span><span class="sxs-lookup"><span data-stu-id="ab253-176">a.</span></span> <span data-ttu-id="ab253-177">Fare clic su **Single Sign-On (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="ab253-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="ab253-178">b.</span><span class="sxs-lookup"><span data-stu-id="ab253-178">b.</span></span> <span data-ttu-id="ab253-179">Hello Incolla **SAML Single Sign-On Service URL** valore, che è stato copiato dal portale di Azure hello in hello **SSO Remote Sign-In** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ab253-179">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="ab253-180">c.</span><span class="sxs-lookup"><span data-stu-id="ab253-180">c.</span></span> <span data-ttu-id="ab253-181">Hello Incolla **Sign-Out URL** valore, che è stato copiato dal portale di Azure hello in hello **textbox SSO Remote Sign-Out**.</span><span class="sxs-lookup"><span data-stu-id="ab253-181">Paste hello **Sign-Out URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="ab253-182">d.</span><span class="sxs-lookup"><span data-stu-id="ab253-182">d.</span></span> <span data-ttu-id="ab253-183">Hello Incolla **identificazione personale** valore, dal portale di Azure in cui è stato copiato il **corrente impronta digitale SHA1 di certificato** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ab253-183">Paste hello **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="ab253-184">e.</span><span class="sxs-lookup"><span data-stu-id="ab253-184">e.</span></span> <span data-ttu-id="ab253-185">Fare clic su **Salva le impostazioni di autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="ab253-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="ab253-186">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="ab253-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ab253-187">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="ab253-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ab253-188">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ab253-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ab253-189">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab253-189">Create an Azure AD test user</span></span>

<span data-ttu-id="ab253-190">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ab253-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="ab253-192">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ab253-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab253-193">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ab253-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ab253-195">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ab253-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ab253-197">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ab253-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ab253-199">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ab253-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ab253-201">a.</span><span class="sxs-lookup"><span data-stu-id="ab253-201">a.</span></span> <span data-ttu-id="ab253-202">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ab253-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ab253-203">b.</span><span class="sxs-lookup"><span data-stu-id="ab253-203">b.</span></span> <span data-ttu-id="ab253-204">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ab253-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ab253-205">c.</span><span class="sxs-lookup"><span data-stu-id="ab253-205">c.</span></span> <span data-ttu-id="ab253-206">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="ab253-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ab253-207">d.</span><span class="sxs-lookup"><span data-stu-id="ab253-207">d.</span></span> <span data-ttu-id="ab253-208">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ab253-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="ab253-209">Creare un utente di test per UserVoice</span><span class="sxs-lookup"><span data-stu-id="ab253-209">Create a UserVoice test user</span></span>

<span data-ttu-id="ab253-210">toolog agli utenti di Azure AD tooenable in tooUserVoice, è necessario eseguirne il provisioning in UserVoice.</span><span class="sxs-lookup"><span data-stu-id="ab253-210">tooenable Azure AD users toolog in tooUserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="ab253-211">Nel caso di hello di UserVoice, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="ab253-211">In hello case of UserVoice, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="ab253-212">tooprovision un account utente, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ab253-212">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="ab253-213">Accedi tooyour **UserVoice** tenant.</span><span class="sxs-lookup"><span data-stu-id="ab253-213">Log in tooyour **UserVoice** tenant.</span></span>

2. <span data-ttu-id="ab253-214">Andare troppo**impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="ab253-214">Go too**Settings**.</span></span>
   
    <span data-ttu-id="ab253-215">![Impostazioni](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="ab253-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="ab253-216">Fare clic su **Generale**.</span><span class="sxs-lookup"><span data-stu-id="ab253-216">Click **General**.</span></span>

4. <span data-ttu-id="ab253-217">Fare clic su **Agents and permissions**.</span><span class="sxs-lookup"><span data-stu-id="ab253-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="ab253-218">![Agenti e autorizzazioni](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agenti e autorizzazioni")</span><span class="sxs-lookup"><span data-stu-id="ab253-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="ab253-219">Fare clic su **Aggiungi amministratori**.</span><span class="sxs-lookup"><span data-stu-id="ab253-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="ab253-220">![Aggiungere amministratori](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Aggiungere amministratori")</span><span class="sxs-lookup"><span data-stu-id="ab253-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="ab253-221">In hello **Invite admins** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ab253-221">On hello **Invite admins** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="ab253-222">![Invitare gli amministratori](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invitare gli amministratori")</span><span class="sxs-lookup"><span data-stu-id="ab253-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="ab253-223">a.</span><span class="sxs-lookup"><span data-stu-id="ab253-223">a.</span></span> <span data-ttu-id="ab253-224">Nella casella di testo con messaggi di posta elettronica di hello digitare l'indirizzo di posta elettronica hello di hello account desiderato tooprovision, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ab253-224">In hello Emails textbox, type hello email address of hello account you want tooprovision, and then click **Add**.</span></span>
   
    <span data-ttu-id="ab253-225">b.</span><span class="sxs-lookup"><span data-stu-id="ab253-225">b.</span></span> <span data-ttu-id="ab253-226">Fare clic su **Invita**.</span><span class="sxs-lookup"><span data-stu-id="ab253-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="ab253-227">È possibile usare qualsiasi altro UserVoice utente account strumento di creazione o le API fornite da UserVoice tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="ab253-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice tooprovision AAD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ab253-228">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab253-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ab253-229">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooUserVoice.</span><span class="sxs-lookup"><span data-stu-id="ab253-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserVoice.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="ab253-231">**tooassign Britta Simon tooUserVoice, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ab253-231">**tooassign Britta Simon tooUserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab253-232">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ab253-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ab253-234">Nell'elenco di applicazioni hello, selezionare **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="ab253-234">In hello applications list, select **UserVoice**.</span></span>

    ![collegamento di UserVoice Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="ab253-236">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ab253-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="ab253-238">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ab253-238">Click **Add** button.</span></span> <span data-ttu-id="ab253-239">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ab253-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="ab253-241">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="ab253-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ab253-242">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ab253-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ab253-243">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ab253-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ab253-244">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ab253-244">Test single sign-on</span></span>

<span data-ttu-id="ab253-245">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ab253-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ab253-246">Quando si fa clic su riquadro UserVoice hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour UserVoice applicazione.</span><span class="sxs-lookup"><span data-stu-id="ab253-246">When you click hello UserVoice tile in hello Access Panel, you should get automatically signed-on tooyour UserVoice application.</span></span>
<span data-ttu-id="ab253-247">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ab253-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ab253-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ab253-248">Additional resources</span></span>

* [<span data-ttu-id="ab253-249">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab253-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ab253-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab253-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

