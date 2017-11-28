---
title: 'Esercitazione: Integrazione di Azure Active Directory con Picturepark | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Picturepark.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="1e88e-103">Esercitazione: Integrazione di Azure Active Directory con Picturepark</span><span class="sxs-lookup"><span data-stu-id="1e88e-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="1e88e-104">In questa esercitazione, è illustrato come toointegrate Picturepark con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e88e-104">In this tutorial, you learn how toointegrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e88e-105">Integrazione Picturepark con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="1e88e-105">Integrating Picturepark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1e88e-106">È possibile controllare in Azure AD che ha accesso tooPicturepark</span><span class="sxs-lookup"><span data-stu-id="1e88e-106">You can control in Azure AD who has access tooPicturepark</span></span>
- <span data-ttu-id="1e88e-107">È possibile abilitare l'utenti tooautomatically get connesso tooPicturepark (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e88e-107">You can enable your users tooautomatically get signed-on tooPicturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e88e-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1e88e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1e88e-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e88e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e88e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1e88e-110">Prerequisites</span></span>

<span data-ttu-id="1e88e-111">integrazione di Azure AD con Picturepark tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1e88e-111">tooconfigure Azure AD integration with Picturepark, you need hello following items:</span></span>

- <span data-ttu-id="1e88e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e88e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e88e-113">Sottoscrizione di Picturepark abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1e88e-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e88e-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1e88e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e88e-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="1e88e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e88e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1e88e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e88e-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e88e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e88e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1e88e-118">Scenario description</span></span>
<span data-ttu-id="1e88e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1e88e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e88e-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="1e88e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e88e-121">Aggiunta di Picturepark dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1e88e-121">Adding Picturepark from hello gallery</span></span>
2. <span data-ttu-id="1e88e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e88e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-hello-gallery"></a><span data-ttu-id="1e88e-123">Aggiunta di Picturepark dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1e88e-123">Adding Picturepark from hello gallery</span></span>
<span data-ttu-id="1e88e-124">integrazione hello tooconfigure di Picturepark in Azure AD, è necessario tooadd Picturepark dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1e88e-124">tooconfigure hello integration of Picturepark into Azure AD, you need tooadd Picturepark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1e88e-125">**tooadd Picturepark dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1e88e-125">**tooadd Picturepark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e88e-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1e88e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1e88e-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1e88e-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1e88e-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1e88e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1e88e-133">Nella casella di ricerca hello, digitare **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-133">In hello search box, type **Picturepark**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="1e88e-135">Nel riquadro dei risultati hello, selezionare **Picturepark**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1e88e-135">In hello results panel, select **Picturepark**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1e88e-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e88e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1e88e-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Picturepark in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1e88e-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1e88e-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Picturepark è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e88e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Picturepark is tooa user in Azure AD.</span></span> <span data-ttu-id="1e88e-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Picturepark richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="1e88e-140">In other words, a link relationship between an Azure AD user and hello related user in Picturepark needs toobe established.</span></span>

<span data-ttu-id="1e88e-141">In Picturepark, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="1e88e-141">In Picturepark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1e88e-142">tooconfigure e prova AD Azure single sign-on con Picturepark, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1e88e-142">tooconfigure and test Azure AD single sign-on with Picturepark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1e88e-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1e88e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1e88e-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e88e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e88e-145">**[Creazione di un utente test Picturepark](#creating-a-picturepark-test-user)**  -toohave un equivalente di Britta Simon in Picturepark che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1e88e-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - toohave a counterpart of Britta Simon in Picturepark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e88e-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1e88e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e88e-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1e88e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1e88e-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e88e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1e88e-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Picturepark.</span><span class="sxs-lookup"><span data-stu-id="1e88e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="1e88e-150">**Azure AD tooconfigure single sign-on con Picturepark, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1e88e-150">**tooconfigure Azure AD single sign-on with Picturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e88e-151">Nel portale di Azure su hello hello **Picturepark** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-151">In hello Azure portal, on hello **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1e88e-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1e88e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="1e88e-155">In hello **Picturepark dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1e88e-155">On hello **Picturepark Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="1e88e-157">a.</span><span class="sxs-lookup"><span data-stu-id="1e88e-157">a.</span></span> <span data-ttu-id="1e88e-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="1e88e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="1e88e-159">b.</span><span class="sxs-lookup"><span data-stu-id="1e88e-159">b.</span></span> <span data-ttu-id="1e88e-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="1e88e-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="1e88e-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="1e88e-161">These values are not real.</span></span> <span data-ttu-id="1e88e-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="1e88e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1e88e-163">Contatto [team di supporto Picturepark Client](https://picturepark.com/about/contact/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="1e88e-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="1e88e-164">In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore del certificato.</span><span class="sxs-lookup"><span data-stu-id="1e88e-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="1e88e-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1e88e-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1e88e-168">In hello **Picturepark configurazione** fare clic su **configurare Picturepark** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="1e88e-168">On hello **Picturepark Configuration** section, click **Configure Picturepark** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1e88e-169">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="1e88e-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="1e88e-171">In un'altra finestra del Web browser accedere al sito aziendale di Picturepark come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1e88e-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="1e88e-172">Nella barra degli strumenti hello in primo piano hello, fare clic su **strumenti di amministrazione**, quindi fare clic su **Console di gestione**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-172">In hello toolbar on hello top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="1e88e-173">![Console di gestione](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Console di gestione")</span><span class="sxs-lookup"><span data-stu-id="1e88e-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="1e88e-174">Fare clic su **Autenticazione**, quindi su **Provider di identità**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="1e88e-175">![Autenticazione](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Autenticazione")</span><span class="sxs-lookup"><span data-stu-id="1e88e-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="1e88e-176">In hello **configurazione del provider di identità** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1e88e-176">In hello **Identity provider configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1e88e-177">![Configurazione del provider di identità](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Configurazione del provider di identità")</span><span class="sxs-lookup"><span data-stu-id="1e88e-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="1e88e-178">a.</span><span class="sxs-lookup"><span data-stu-id="1e88e-178">a.</span></span> <span data-ttu-id="1e88e-179">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-179">Click **Add**.</span></span>
  
    <span data-ttu-id="1e88e-180">b.</span><span class="sxs-lookup"><span data-stu-id="1e88e-180">b.</span></span> <span data-ttu-id="1e88e-181">Digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="1e88e-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="1e88e-182">c.</span><span class="sxs-lookup"><span data-stu-id="1e88e-182">c.</span></span> <span data-ttu-id="1e88e-183">Selezionare **Imposta come predefinito**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="1e88e-184">d.</span><span class="sxs-lookup"><span data-stu-id="1e88e-184">d.</span></span> <span data-ttu-id="1e88e-185">In **Issuer URI** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e88e-185">In **Issuer URI** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="1e88e-186">e.</span><span class="sxs-lookup"><span data-stu-id="1e88e-186">e.</span></span> <span data-ttu-id="1e88e-187">In **Trusted Issuer Thumb Print** casella di testo, hello Incolla valore **identificazione personale** che è stato copiato da **certificato di firma SAML** sezione.</span><span class="sxs-lookup"><span data-stu-id="1e88e-187">In **Trusted Issuer Thumb Print** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="1e88e-188">Fare clic su **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="1e88e-189">hello tooset **Emailaddress** attributo hello **attestazione** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-189">tooset hello **Emailaddress** attribute in hello **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="1e88e-190">![Configurazione](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configurazione")</span><span class="sxs-lookup"><span data-stu-id="1e88e-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="1e88e-191">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="1e88e-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1e88e-192">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="1e88e-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1e88e-193">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e88e-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1e88e-194">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e88e-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="1e88e-195">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1e88e-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1e88e-197">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1e88e-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e88e-198">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1e88e-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1e88e-200">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1e88e-202">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="1e88e-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e88e-204">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1e88e-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1e88e-206">a.</span><span class="sxs-lookup"><span data-stu-id="1e88e-206">a.</span></span> <span data-ttu-id="1e88e-207">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e88e-208">b.</span><span class="sxs-lookup"><span data-stu-id="1e88e-208">b.</span></span> <span data-ttu-id="1e88e-209">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1e88e-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1e88e-210">c.</span><span class="sxs-lookup"><span data-stu-id="1e88e-210">c.</span></span> <span data-ttu-id="1e88e-211">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1e88e-212">d.</span><span class="sxs-lookup"><span data-stu-id="1e88e-212">d.</span></span> <span data-ttu-id="1e88e-213">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="1e88e-214">Creazione di un utente test di Picturepark</span><span class="sxs-lookup"><span data-stu-id="1e88e-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="1e88e-215">In ordine tooenable Azure AD utenti toolog a Picturepark, è necessario eseguirne il provisioning in Picturepark.</span><span class="sxs-lookup"><span data-stu-id="1e88e-215">In order tooenable Azure AD users toolog into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="1e88e-216">Nel caso di hello di Picturepark, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="1e88e-216">In hello case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="1e88e-217">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1e88e-217">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e88e-218">Accedi tooyour **Picturepark** tenant.</span><span class="sxs-lookup"><span data-stu-id="1e88e-218">Log in tooyour **Picturepark** tenant.</span></span>

2. <span data-ttu-id="1e88e-219">Nella barra degli strumenti hello in primo piano hello, fare clic su **strumenti di amministrazione**, quindi fare clic su **utenti**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-219">In hello toolbar on hello top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="1e88e-220">![Utenti](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="1e88e-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="1e88e-221">In hello **Cenni preliminari sugli utenti** scheda, fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-221">In hello **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="1e88e-222">![Gestione degli utenti](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Gestione degli utenti")</span><span class="sxs-lookup"><span data-stu-id="1e88e-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="1e88e-223">In hello **Create User** finestra di dialogo, hello eseguire i passaggi di un utente valido delle Directory Azure Active seguenti si desidera tooprovision:</span><span class="sxs-lookup"><span data-stu-id="1e88e-223">On hello **Create User** dialog, perform hello following steps of a valid Azure Active Directory User you want tooprovision:</span></span>
   
    <span data-ttu-id="1e88e-224">![Crea utente](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Crea utente")</span><span class="sxs-lookup"><span data-stu-id="1e88e-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="1e88e-225">a.</span><span class="sxs-lookup"><span data-stu-id="1e88e-225">a.</span></span> <span data-ttu-id="1e88e-226">In hello **indirizzo di posta elettronica** casella di testo, hello tipo **indirizzo di posta elettronica** dell'utente hello  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="1e88e-226">In hello **Email Address** textbox, type hello **email address** of hello user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="1e88e-227">b.</span><span class="sxs-lookup"><span data-stu-id="1e88e-227">b.</span></span> <span data-ttu-id="1e88e-228">In hello **Password** e **Conferma Password** nelle caselle di testo, hello tipo **password** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1e88e-228">In hello **Password** and **Confirm Password** textboxes, type hello **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="1e88e-229">c.</span><span class="sxs-lookup"><span data-stu-id="1e88e-229">c.</span></span> <span data-ttu-id="1e88e-230">In hello **nome** casella di testo, hello tipo **nome** dell'utente hello **Laura**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-230">In hello **First Name** textbox, type hello **First Name** of hello user **Britta**.</span></span> 
   
    <span data-ttu-id="1e88e-231">d.</span><span class="sxs-lookup"><span data-stu-id="1e88e-231">d.</span></span> <span data-ttu-id="1e88e-232">In hello **cognome** casella di testo, hello tipo **cognome** dell'utente hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-232">In hello **Last Name** textbox, type hello **Last Name** of hello user **Simon**.</span></span>
   
    <span data-ttu-id="1e88e-233">e.</span><span class="sxs-lookup"><span data-stu-id="1e88e-233">e.</span></span> <span data-ttu-id="1e88e-234">In hello **aziendale** casella di testo, hello tipo **nome società** dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="1e88e-234">In hello **Company** textbox, type hello **Company name** of hello user.</span></span> 
   
    <span data-ttu-id="1e88e-235">f.</span><span class="sxs-lookup"><span data-stu-id="1e88e-235">f.</span></span> <span data-ttu-id="1e88e-236">In hello **paese** casella di testo, seleziona hello **paese** dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="1e88e-236">In hello **Country** textbox, select hello **Country** of hello user.</span></span>
  
    <span data-ttu-id="1e88e-237">g.</span><span class="sxs-lookup"><span data-stu-id="1e88e-237">g.</span></span> <span data-ttu-id="1e88e-238">In hello **ZIP** casella di testo, hello tipo **CAP** di città hello.</span><span class="sxs-lookup"><span data-stu-id="1e88e-238">In hello **ZIP** textbox, type hello **ZIP code** of hello city.</span></span>
   
    <span data-ttu-id="1e88e-239">h.</span><span class="sxs-lookup"><span data-stu-id="1e88e-239">h.</span></span> <span data-ttu-id="1e88e-240">In hello **Città** casella di testo, hello tipo **Città** dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="1e88e-240">In hello **City** textbox, type hello **City name** of hello user.</span></span>

    <span data-ttu-id="1e88e-241">i.</span><span class="sxs-lookup"><span data-stu-id="1e88e-241">i.</span></span> <span data-ttu-id="1e88e-242">Selezionare una **Language**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="1e88e-243">j.</span><span class="sxs-lookup"><span data-stu-id="1e88e-243">j.</span></span> <span data-ttu-id="1e88e-244">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="1e88e-245">È possibile usare qualsiasi altro Picturepark utente account strumento di creazione o le API fornite da Picturepark tooprovision degli account utente di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e88e-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1e88e-246">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e88e-246">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1e88e-247">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPicturepark.</span><span class="sxs-lookup"><span data-stu-id="1e88e-247">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPicturepark.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1e88e-249">**tooassign Britta Simon tooPicturepark, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1e88e-249">**tooassign Britta Simon tooPicturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e88e-250">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-250">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1e88e-252">Nell'elenco di applicazioni hello, selezionare **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-252">In hello applications list, select **Picturepark**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="1e88e-254">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-254">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1e88e-256">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-256">Click **Add** button.</span></span> <span data-ttu-id="1e88e-257">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1e88e-259">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1e88e-259">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1e88e-260">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e88e-261">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1e88e-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1e88e-262">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1e88e-262">Testing single sign-on</span></span>

<span data-ttu-id="1e88e-263">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1e88e-263">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1e88e-264">Quando si fa clic su riquadro Picturepark hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in Picturepark applicazione.</span><span class="sxs-lookup"><span data-stu-id="1e88e-264">When you click hello Picturepark tile in hello Access Panel, you should get automatically signed-on tooyour Picturepark application.</span></span> <span data-ttu-id="1e88e-265">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1e88e-265">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1e88e-266">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1e88e-266">Additional resources</span></span>

* [<span data-ttu-id="1e88e-267">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e88e-267">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e88e-268">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e88e-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

