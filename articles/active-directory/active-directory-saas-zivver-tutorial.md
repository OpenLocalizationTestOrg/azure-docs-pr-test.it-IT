---
title: 'Esercitazione: Integrazione di Azure Active Directory con ZIVVER | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ZIVVER.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 64cb7ea0-df6c-4963-84d8-6f435980e2de
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 0928abcc4dcbd97b892298f4919c8d44e1a058a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zivver"></a><span data-ttu-id="9a14c-103">Esercitazione: Integrazione di Azure Active Directory con ZIVVER</span><span class="sxs-lookup"><span data-stu-id="9a14c-103">Tutorial: Azure Active Directory integration with ZIVVER</span></span>

<span data-ttu-id="9a14c-104">In questa esercitazione, è illustrato come toointegrate ZIVVER con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a14c-104">In this tutorial, you learn how toointegrate ZIVVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a14c-105">Integrazione ZIVVER con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="9a14c-105">Integrating ZIVVER with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9a14c-106">È possibile controllare in Azure AD che ha accesso tooZIVVER.</span><span class="sxs-lookup"><span data-stu-id="9a14c-106">You can control in Azure AD who has access tooZIVVER.</span></span>
- <span data-ttu-id="9a14c-107">È possibile abilitare l'utenti tooautomatically get connesso tooZIVVER (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a14c-107">You can enable your users tooautomatically get signed-on tooZIVVER (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9a14c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9a14c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="9a14c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a14c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a14c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9a14c-110">Prerequisites</span></span>

<span data-ttu-id="9a14c-111">integrazione di Azure AD con ZIVVER tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="9a14c-111">tooconfigure Azure AD integration with ZIVVER, you need hello following items:</span></span>

- <span data-ttu-id="9a14c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a14c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a14c-113">Sottoscrizione di ZIVVER abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9a14c-113">A ZIVVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a14c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="9a14c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a14c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="9a14c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a14c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="9a14c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a14c-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a14c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a14c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="9a14c-118">Scenario description</span></span>
<span data-ttu-id="9a14c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="9a14c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a14c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="9a14c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a14c-121">Aggiunta di ZIVVER dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="9a14c-121">Adding ZIVVER from hello gallery</span></span>
2. <span data-ttu-id="9a14c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a14c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zivver-from-hello-gallery"></a><span data-ttu-id="9a14c-123">Aggiunta di ZIVVER dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="9a14c-123">Adding ZIVVER from hello gallery</span></span>
<span data-ttu-id="9a14c-124">integrazione hello tooconfigure di ZIVVER in Azure AD, è necessario tooadd ZIVVER dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="9a14c-124">tooconfigure hello integration of ZIVVER into Azure AD, you need tooadd ZIVVER from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9a14c-125">**tooadd ZIVVER dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9a14c-125">**tooadd ZIVVER from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a14c-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="9a14c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="9a14c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="9a14c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9a14c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9a14c-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="9a14c-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9a14c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="9a14c-133">Nella casella di ricerca hello, digitare **ZIVVER**selezionare **ZIVVER** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9a14c-133">In hello search box, type **ZIVVER**, select **ZIVVER** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello ZIVVER](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9a14c-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a14c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9a14c-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ZIVVER usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9a14c-136">In this section, you configure and test Azure AD single sign-on with ZIVVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a14c-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ZIVVER è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a14c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ZIVVER is tooa user in Azure AD.</span></span> <span data-ttu-id="9a14c-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in ZIVVER deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="9a14c-138">In other words, a link relationship between an Azure AD user and hello related user in ZIVVER needs toobe established.</span></span>

<span data-ttu-id="9a14c-139">In ZIVVER, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="9a14c-139">In ZIVVER, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9a14c-140">tooconfigure e prova AD Azure single sign-on con ZIVVER, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="9a14c-140">tooconfigure and test Azure AD single sign-on with ZIVVER, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9a14c-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9a14c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9a14c-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a14c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a14c-143">**[Creare un utente test ZIVVER](#create-a-zivver-test-user)**  -toohave un equivalente di Britta Simon in ZIVVER che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9a14c-143">**[Create a ZIVVER test user](#create-a-zivver-test-user)** - toohave a counterpart of Britta Simon in ZIVVER that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a14c-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9a14c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a14c-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="9a14c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9a14c-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a14c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9a14c-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="9a14c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ZIVVER application.</span></span>

<span data-ttu-id="9a14c-148">**Azure AD tooconfigure single sign-on con ZIVVER, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9a14c-148">**tooconfigure Azure AD single sign-on with ZIVVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a14c-149">Nel portale di Azure su hello hello **ZIVVER** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9a14c-149">In hello Azure portal, on hello **ZIVVER** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="9a14c-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9a14c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_samlbase.png)

3. <span data-ttu-id="9a14c-153">In hello **ZIVVER dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9a14c-153">On hello **ZIVVER Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di ZIVVER](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_url.png)

    <span data-ttu-id="9a14c-155">In hello **identificatore** casella di testo, digitare l'URL hello:`https://app.zivver.com/SAML/Zivver`</span><span class="sxs-lookup"><span data-stu-id="9a14c-155">In hello **Identifier** textbox, type hello URL: `https://app.zivver.com/SAML/Zivver`</span></span>

4. <span data-ttu-id="9a14c-156">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="9a14c-156">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_certificate.png) 

5. <span data-ttu-id="9a14c-158">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="9a14c-158">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-zivver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9a14c-160">tooconfigure single sign-on sul **ZIVVER** lato, è necessario hello toosend scaricato **Metadata XML** troppo[ZIVVER team di supporto](https://support.zivver.com).</span><span class="sxs-lookup"><span data-stu-id="9a14c-160">tooconfigure single sign-on on **ZIVVER** side, you need toosend hello downloaded **Metadata XML** too[ZIVVER support team](https://support.zivver.com).</span></span> <span data-ttu-id="9a14c-161">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="9a14c-161">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9a14c-162">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="9a14c-162">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9a14c-163">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="9a14c-163">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9a14c-164">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9a14c-164">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9a14c-165">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a14c-165">Create an Azure AD test user</span></span>

<span data-ttu-id="9a14c-166">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="9a14c-166">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="9a14c-168">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9a14c-168">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a14c-169">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="9a14c-169">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-zivver-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9a14c-171">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="9a14c-171">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-zivver-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9a14c-173">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9a14c-173">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-zivver-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9a14c-175">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9a14c-175">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-zivver-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9a14c-177">a.</span><span class="sxs-lookup"><span data-stu-id="9a14c-177">a.</span></span> <span data-ttu-id="9a14c-178">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a14c-178">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a14c-179">b.</span><span class="sxs-lookup"><span data-stu-id="9a14c-179">b.</span></span> <span data-ttu-id="9a14c-180">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a14c-180">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="9a14c-181">c.</span><span class="sxs-lookup"><span data-stu-id="9a14c-181">c.</span></span> <span data-ttu-id="9a14c-182">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="9a14c-182">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="9a14c-183">d.</span><span class="sxs-lookup"><span data-stu-id="9a14c-183">d.</span></span> <span data-ttu-id="9a14c-184">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9a14c-184">Click **Create**.</span></span>
  
### <a name="create-a-zivver-test-user"></a><span data-ttu-id="9a14c-185">Creare un utente di test di ZIVVER</span><span class="sxs-lookup"><span data-stu-id="9a14c-185">Create a ZIVVER test user</span></span>

<span data-ttu-id="9a14c-186">In questa sezione viene creato un utente di nome Britta Simon in ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="9a14c-186">In this section, you create a user called Britta Simon in ZIVVER.</span></span> <span data-ttu-id="9a14c-187">Lavorare con [ZIVVER team di supporto](https://support.zivver.com) utenti hello tooadd nella piattaforma ZIVVER hello.</span><span class="sxs-lookup"><span data-stu-id="9a14c-187">Work with [ZIVVER support team](https://support.zivver.com) tooadd hello users in hello ZIVVER platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9a14c-188">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a14c-188">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9a14c-189">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooZIVVER.</span><span class="sxs-lookup"><span data-stu-id="9a14c-189">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZIVVER.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="9a14c-191">**tooassign Britta Simon tooZIVVER, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="9a14c-191">**tooassign Britta Simon tooZIVVER, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a14c-192">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9a14c-192">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="9a14c-194">Nell'elenco di applicazioni hello, selezionare **ZIVVER**.</span><span class="sxs-lookup"><span data-stu-id="9a14c-194">In hello applications list, select **ZIVVER**.</span></span>

    ![collegamento ZIVVER Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_app.png)  

3. <span data-ttu-id="9a14c-196">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9a14c-196">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="9a14c-198">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9a14c-198">Click **Add** button.</span></span> <span data-ttu-id="9a14c-199">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9a14c-199">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="9a14c-201">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="9a14c-201">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9a14c-202">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="9a14c-202">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a14c-203">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="9a14c-203">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9a14c-204">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="9a14c-204">Test single sign-on</span></span>

<span data-ttu-id="9a14c-205">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="9a14c-205">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9a14c-206">Quando si fa clic hello ZIVVER riquadro in hello Pannello di accesso, è necessario ottenere applicazione ZIVVER tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="9a14c-206">When you click hello ZIVVER tile in hello Access Panel, you should get automatically signed-on tooyour ZIVVER application.</span></span>
<span data-ttu-id="9a14c-207">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9a14c-207">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9a14c-208">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9a14c-208">Additional resources</span></span>

* [<span data-ttu-id="9a14c-209">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a14c-209">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a14c-210">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a14c-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_203.png

