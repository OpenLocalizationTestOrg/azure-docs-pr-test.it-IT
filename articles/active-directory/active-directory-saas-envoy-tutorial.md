---
title: 'Esercitazione: Integrazione di Azure Active Directory con Envoy | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed Envoy.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 93add7c1f3cf1fc163acc505f11e34bd696c571c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="583cd-103">Esercitazione: Integrazione di Azure Active Directory con Envoy</span><span class="sxs-lookup"><span data-stu-id="583cd-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="583cd-104">In questa esercitazione, è illustrato come toointegrate Envoy con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="583cd-104">In this tutorial, you learn how toointegrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="583cd-105">Invio di integrazione con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="583cd-105">Integrating Envoy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="583cd-106">È possibile controllare in Azure AD che ha accesso tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="583cd-106">You can control in Azure AD who has access tooEnvoy.</span></span>
- <span data-ttu-id="583cd-107">È possibile abilitare l'utenti tooautomatically get connesso tooEnvoy (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="583cd-107">You can enable your users tooautomatically get signed-on tooEnvoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="583cd-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="583cd-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="583cd-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="583cd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="583cd-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="583cd-110">Prerequisites</span></span>

<span data-ttu-id="583cd-111">integrazione di Azure AD con Envoy tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="583cd-111">tooconfigure Azure AD integration with Envoy, you need hello following items:</span></span>

- <span data-ttu-id="583cd-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="583cd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="583cd-113">Sottoscrizione di Envoy abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="583cd-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="583cd-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="583cd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="583cd-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="583cd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="583cd-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="583cd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="583cd-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="583cd-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="583cd-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="583cd-118">Scenario description</span></span>
<span data-ttu-id="583cd-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="583cd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="583cd-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="583cd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="583cd-121">Aggiunta di invio dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="583cd-121">Adding Envoy from hello gallery</span></span>
2. <span data-ttu-id="583cd-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="583cd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-hello-gallery"></a><span data-ttu-id="583cd-123">Aggiunta di invio dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="583cd-123">Adding Envoy from hello gallery</span></span>
<span data-ttu-id="583cd-124">integrazione hello tooconfigure di invio in Azure AD, è necessario tooadd Envoy dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="583cd-124">tooconfigure hello integration of Envoy into Azure AD, you need tooadd Envoy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="583cd-125">**tooadd Envoy dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="583cd-125">**tooadd Envoy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="583cd-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="583cd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="583cd-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="583cd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="583cd-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="583cd-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="583cd-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="583cd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="583cd-133">Nella casella di ricerca hello, digitare **Envoy**selezionare **Envoy** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="583cd-133">In hello search box, type **Envoy**, select **Envoy** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="583cd-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="583cd-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="583cd-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Envoy in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="583cd-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="583cd-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Envoy è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="583cd-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Envoy is tooa user in Azure AD.</span></span> <span data-ttu-id="583cd-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Envoy richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="583cd-138">In other words, a link relationship between an Azure AD user and hello related user in Envoy needs toobe established.</span></span>

<span data-ttu-id="583cd-139">In Envoy, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="583cd-139">In Envoy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="583cd-140">tooconfigure e test Azure single sign-on AD con Envoy, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="583cd-140">tooconfigure and test Azure AD single sign-on with Envoy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="583cd-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="583cd-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="583cd-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="583cd-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="583cd-143">**[Creare un utente test Envoy](#create-an-envoy-test-user)**  -toohave un equivalente di Britta Simon in Envoy che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="583cd-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - toohave a counterpart of Britta Simon in Envoy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="583cd-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="583cd-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="583cd-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="583cd-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="583cd-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="583cd-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="583cd-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione di invio.</span><span class="sxs-lookup"><span data-stu-id="583cd-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="583cd-148">**Azure AD tooconfigure single sign-on con Envoy, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="583cd-148">**tooconfigure Azure AD single sign-on with Envoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="583cd-149">Nel portale di Azure su hello hello **Envoy** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="583cd-149">In hello Azure portal, on hello **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="583cd-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="583cd-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="583cd-153">In hello **Envoy dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="583cd-153">On hello **Envoy Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="583cd-155">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="583cd-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="583cd-156">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="583cd-156">This value is not real.</span></span> <span data-ttu-id="583cd-157">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="583cd-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="583cd-158">Contatto [team di supporto Client Envoy](https://envoy.com/contact/) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="583cd-158">Contact [Envoy Client support team](https://envoy.com/contact/) tooget this value.</span></span>

4. <span data-ttu-id="583cd-159">In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore del certificato...</span><span class="sxs-lookup"><span data-stu-id="583cd-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate..</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="583cd-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="583cd-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="583cd-163">In hello **Envoy configurazione** fare clic su **configurare Envoy** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="583cd-163">On hello **Envoy Configuration** section, click **Configure Envoy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="583cd-164">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="583cd-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="583cd-166">In un'altra finestra del Web browser accedere al sito aziendale di Envoy come amministratore.</span><span class="sxs-lookup"><span data-stu-id="583cd-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="583cd-167">Nella barra degli strumenti hello in primo piano hello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="583cd-167">In hello toolbar on hello top, click **Settings**.</span></span>

    <span data-ttu-id="583cd-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="583cd-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="583cd-169">Fare clic su **Azienda**.</span><span class="sxs-lookup"><span data-stu-id="583cd-169">Click **Company**.</span></span>

    <span data-ttu-id="583cd-170">![Azienda](./media/active-directory-saas-envoy-tutorial/ic776783.png "Azienda")</span><span class="sxs-lookup"><span data-stu-id="583cd-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="583cd-171">Fare clic su **SAML**.</span><span class="sxs-lookup"><span data-stu-id="583cd-171">Click **SAML**.</span></span>

    <span data-ttu-id="583cd-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="583cd-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="583cd-173">In hello **SAML Authentication** configurazione seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="583cd-173">In hello **SAML Authentication** configuration section, perform hello following steps:</span></span>

    <span data-ttu-id="583cd-174">![Autenticazione SAML](./media/active-directory-saas-envoy-tutorial/ic776785.png "Autenticazione SAML")</span><span class="sxs-lookup"><span data-stu-id="583cd-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="583cd-175">il valore di Hello per l'ID di posizione HQ hello viene automaticamente generato da un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="583cd-175">hello value for hello HQ location ID is auto generated by hello application.</span></span>
    
    <span data-ttu-id="583cd-176">a.</span><span class="sxs-lookup"><span data-stu-id="583cd-176">a.</span></span> <span data-ttu-id="583cd-177">In **impronta digitale** casella di testo, incollare hello **identificazione personale** valore del certificato, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="583cd-177">In **Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="583cd-178">b.</span><span class="sxs-lookup"><span data-stu-id="583cd-178">b.</span></span> <span data-ttu-id="583cd-179">Incolla **SAML Single Sign-On Service URL** valore, che è stato copiato modulo hello Azure portale in hello **IDENTITY PROVIDER HTTP SAML URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="583cd-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form hello Azure portal into hello **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="583cd-180">c.</span><span class="sxs-lookup"><span data-stu-id="583cd-180">c.</span></span> <span data-ttu-id="583cd-181">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="583cd-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="583cd-182">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="583cd-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="583cd-183">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="583cd-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="583cd-184">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="583cd-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="583cd-185">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="583cd-185">Create an Azure AD test user</span></span>

<span data-ttu-id="583cd-186">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="583cd-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="583cd-188">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="583cd-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="583cd-189">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="583cd-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="583cd-191">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="583cd-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="583cd-193">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="583cd-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="583cd-195">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="583cd-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="583cd-197">a.</span><span class="sxs-lookup"><span data-stu-id="583cd-197">a.</span></span> <span data-ttu-id="583cd-198">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="583cd-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="583cd-199">b.</span><span class="sxs-lookup"><span data-stu-id="583cd-199">b.</span></span> <span data-ttu-id="583cd-200">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="583cd-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="583cd-201">c.</span><span class="sxs-lookup"><span data-stu-id="583cd-201">c.</span></span> <span data-ttu-id="583cd-202">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="583cd-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="583cd-203">d.</span><span class="sxs-lookup"><span data-stu-id="583cd-203">d.</span></span> <span data-ttu-id="583cd-204">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="583cd-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="583cd-205">Creare un utente test di Envoy</span><span class="sxs-lookup"><span data-stu-id="583cd-205">Create an Envoy test user</span></span>

<span data-ttu-id="583cd-206">Non sono presenti elementi di azione per si tooconfigure di provisioning dell'utente tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="583cd-206">There is no action item for you tooconfigure user provisioning tooEnvoy.</span></span> <span data-ttu-id="583cd-207">Quando un utente assegnato tenta toolog a Envoy mediante il pannello di accesso di hello, Envoy verifica l'esistenza di utente hello.</span><span class="sxs-lookup"><span data-stu-id="583cd-207">When an assigned user tries toolog into Envoy using hello access panel, Envoy checks whether hello user exists.</span></span> <span data-ttu-id="583cd-208">Se l'account utente non è presente, Envoy lo crea automaticamente.</span><span class="sxs-lookup"><span data-stu-id="583cd-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="583cd-209">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="583cd-209">Assign hello Azure AD test user</span></span>

<span data-ttu-id="583cd-210">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="583cd-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEnvoy.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="583cd-212">**tooassign Britta Simon tooEnvoy, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="583cd-212">**tooassign Britta Simon tooEnvoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="583cd-213">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="583cd-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="583cd-215">Nell'elenco di applicazioni hello, selezionare **Envoy**.</span><span class="sxs-lookup"><span data-stu-id="583cd-215">In hello applications list, select **Envoy**.</span></span>

    ![collegamento Envoy Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="583cd-217">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="583cd-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="583cd-219">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="583cd-219">Click **Add** button.</span></span> <span data-ttu-id="583cd-220">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="583cd-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="583cd-222">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="583cd-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="583cd-223">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="583cd-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="583cd-224">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="583cd-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="583cd-225">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="583cd-225">Test single sign-on</span></span>

<span data-ttu-id="583cd-226">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="583cd-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="583cd-227">Quando si fa clic su riquadro Envoy hello in hello Pannello di accesso, è necessario ottenere applicazione Envoy tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="583cd-227">When you click hello Envoy tile in hello Access Panel, you should get automatically signed-on tooyour Envoy application.</span></span>
<span data-ttu-id="583cd-228">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="583cd-228">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="583cd-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="583cd-229">Additional resources</span></span>

* [<span data-ttu-id="583cd-230">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="583cd-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="583cd-231">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="583cd-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

