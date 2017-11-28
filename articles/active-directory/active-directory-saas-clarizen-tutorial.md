---
title: 'Esercitazione: Integrazione di Azure Active Directory con Clarizen | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Clarizen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="7630c-103">Esercitazione: Integrazione di Azure Active Directory con Clarizen</span><span class="sxs-lookup"><span data-stu-id="7630c-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="7630c-104">In questa esercitazione, è illustrato come toointegrate Azure Active Directory (Azure AD) con Clarizen.</span><span class="sxs-lookup"><span data-stu-id="7630c-104">In this tutorial, you learn how toointegrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="7630c-105">In questo modo di integrazione hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="7630c-105">This integration gives you hello following benefits:</span></span>

- <span data-ttu-id="7630c-106">È possibile controllare, in Azure AD, che dispone di accesso tooClarizen.</span><span class="sxs-lookup"><span data-stu-id="7630c-106">You can control, in Azure AD, who has access tooClarizen.</span></span>
- <span data-ttu-id="7630c-107">È possibile abilitare il toobe gli utenti connessi automaticamente tooClarizen (single sign-on) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7630c-107">You can enable your users toobe automatically signed in tooClarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7630c-108">È possibile gestire gli account in un'unica posizione centrale, hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7630c-108">You can manage your accounts in one central location, hello Azure portal.</span></span>

<span data-ttu-id="7630c-109">scenario di Hello in questa esercitazione è costituita da due attività principali:</span><span class="sxs-lookup"><span data-stu-id="7630c-109">hello scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="7630c-110">Aggiungere Clarizen dalla raccolta di hello.</span><span class="sxs-lookup"><span data-stu-id="7630c-110">Add Clarizen from hello gallery.</span></span>
2. <span data-ttu-id="7630c-111">Configurare e testare l'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7630c-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="7630c-112">Per altre informazioni sull'integrazione di app SaaS (Software as a Service) con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7630c-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7630c-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7630c-113">Prerequisites</span></span>
<span data-ttu-id="7630c-114">integrazione di Azure AD con Clarizen tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="7630c-114">tooconfigure Azure AD integration with Clarizen, you need hello following items:</span></span>

- <span data-ttu-id="7630c-115">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7630c-115">An Azure AD subscription</span></span>
- <span data-ttu-id="7630c-116">Una sottoscrizione di Clarizen abilitata per Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7630c-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="7630c-117">passaggi di hello tootest in questa esercitazione, seguire queste indicazioni:</span><span class="sxs-lookup"><span data-stu-id="7630c-117">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="7630c-118">Testare l'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="7630c-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7630c-119">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="7630c-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7630c-120">Se non è disponibile un ambiente di test di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7630c-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-hello-gallery"></a><span data-ttu-id="7630c-121">Aggiungere Clarizen dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="7630c-121">Add Clarizen from hello gallery</span></span>
<span data-ttu-id="7630c-122">integrazione di hello tooconfigure di Clarizen in Azure AD, aggiungere Clarizen hello raccolta tooyour elenco di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="7630c-122">tooconfigure hello integration of Clarizen into Azure AD, add Clarizen from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="7630c-123">In hello [portale di Azure](https://portal.azure.com)in hello riquadro sinistro, fare clic su hello **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="7630c-123">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Icona Azure Active Directory][1]

2. <span data-ttu-id="7630c-125">Fare clic su **Applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7630c-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="7630c-126">Fare quindi clic su **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7630c-126">Then click **All applications**.</span></span>

    ![Clic su "Applicazioni aziendali" e su "Tutte le applicazioni"][2]

3. <span data-ttu-id="7630c-128">Fare clic su hello **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="7630c-128">Click hello **Add** button at hello top of hello dialog box.</span></span>

    ![pulsante "Aggiungi" Hello][3]

4. <span data-ttu-id="7630c-130">Nella casella di ricerca hello, digitare **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="7630c-130">In hello search box, type **Clarizen**.</span></span>

    ![Digitare "Clarizen" nella casella di ricerca hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="7630c-132">Nel riquadro risultati hello selezionare **Clarizen**, quindi fare clic su **Aggiungi** tooadd un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7630c-132">In hello results pane, select **Clarizen**, and then click **Add** tooadd hello application.</span></span>

    ![Selezione di Clarizen nel riquadro dei risultati di hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7630c-134">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7630c-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="7630c-135">Nelle seguenti sezioni di hello, configurare e testare Azure AD single sign-on con Clarizen in base all'utente di test hello Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7630c-135">In hello following sections, you configure and test Azure AD single sign-on with Clarizen based on hello test user Britta Simon.</span></span>

<span data-ttu-id="7630c-136">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Clarizen è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7630c-136">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clarizen is tooa user in Azure AD.</span></span> <span data-ttu-id="7630c-137">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Clarizen deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="7630c-137">In other words, a link relationship between an Azure AD user and hello related user in Clarizen needs toobe established.</span></span> <span data-ttu-id="7630c-138">Per stabilire questa relazione di collegamento, assegnando il valore di hello del **nome utente** in Azure AD come valore hello **Username** in Clarizen.</span><span class="sxs-lookup"><span data-stu-id="7630c-138">You establish this link relationship by assigning hello value of **user name** in Azure AD as hello value of **Username** in Clarizen.</span></span>

<span data-ttu-id="7630c-139">tooconfigure e prova AD Azure single sign-on con Clarizen, hello completo seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="7630c-139">tooconfigure and test Azure AD single sign-on with Clarizen, complete hello following building blocks:</span></span>

1. <span data-ttu-id="7630c-140">**[Configurare Azure AD single sign-on](#configure-azure-ad-single-sign-on)**  tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7630c-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7630c-141">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7630c-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7630c-142">**[Creare un utente test Clarizen](#create-a-clarizen-test-user)**  toohave un equivalente di Britta Simon in Clarizen toohello collegato AD Azure rappresentazione in seguito.</span><span class="sxs-lookup"><span data-stu-id="7630c-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** toohave a counterpart of Britta Simon in Clarizen that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="7630c-143">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7630c-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7630c-144">**[Testare single sign-on](#test-single-sign-on)**  tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="7630c-144">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7630c-145">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7630c-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="7630c-146">Abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Clarizen.</span><span class="sxs-lookup"><span data-stu-id="7630c-146">Enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="7630c-147">Nel portale di Azure su hello hello **Clarizen** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7630c-147">In hello Azure portal, on hello **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Clic su "Single Sign-On"][4]

2. <span data-ttu-id="7630c-149">In hello **Single sign-on** nella finestra di dialogo per **modalità**selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7630c-149">In hello **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Selezione di "Accesso basato su SAML"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="7630c-151">In hello **Clarizen dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7630c-151">In hello **Clarizen Domain and URLs** section, perform hello following steps:</span></span>

    ![Caselle per identificatore e URL di risposta](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="7630c-153">a.</span><span class="sxs-lookup"><span data-stu-id="7630c-153">a.</span></span> <span data-ttu-id="7630c-154">In hello **identificatore** casella Tipo di un valore di hello: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="7630c-154">In hello **Identifier** box, type hello value as: **Clarizen**</span></span>

    <span data-ttu-id="7630c-155">b.</span><span class="sxs-lookup"><span data-stu-id="7630c-155">b.</span></span> <span data-ttu-id="7630c-156">In hello **URL di risposta** , digitare un URL con modello di hello: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="7630c-156">In hello **Reply URL** box, type a URL by using hello following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="7630c-157">Non sono valori reali hello.</span><span class="sxs-lookup"><span data-stu-id="7630c-157">These are not hello real values.</span></span> <span data-ttu-id="7630c-158">Si dispone di toouse hello effettivo identificatore e URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="7630c-158">You have toouse hello actual identifier and reply URL.</span></span> <span data-ttu-id="7630c-159">In questo caso è consigliabile utilizzare hello valore univoco di una stringa come identificatore hello.</span><span class="sxs-lookup"><span data-stu-id="7630c-159">Here we suggest that you use hello unique value of a string as hello identifier.</span></span> <span data-ttu-id="7630c-160">i valori effettivi, hello contatto di hello tooget [team di supporto di Clarizen](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="7630c-160">tooget hello actual values, contact hello [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="7630c-161">In hello **certificato di firma SAML** fare clic su **Crea nuovo certificato**.</span><span class="sxs-lookup"><span data-stu-id="7630c-161">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Clic su "Crea nuovo certificato"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="7630c-163">In hello **creare nuovo certificato** finestra di dialogo fare clic sull'icona calendario hello e selezionare una data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="7630c-163">In hello **Create New Certificate** dialog box, click hello calendar icon and select an expiry date.</span></span> <span data-ttu-id="7630c-164">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="7630c-164">Then click **Save**.</span></span>

    ![Selezione e salvataggio di una data di scadenza](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="7630c-166">In hello **certificato di firma SAML** sezione, selezionare **attivare di nuovo certificato**, quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="7630c-166">In hello **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Selezionando la casella di controllo hello per rendere il nuovo certificato di hello attivo](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="7630c-168">In hello **il certificato di Rollover** la finestra di dialogo, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="7630c-168">In hello **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Fare clic su "OK" tooconfirm che si desidera toomake hello certificato active](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7630c-170">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="7630c-170">In hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Fare clic su download di hello toostart "Certificato (Base64)"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="7630c-172">In hello **Clarizen configurazione** fare clic su **configurare Clarizen** tooopen hello **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="7630c-172">In hello **Clarizen Configuration** section, click **Configure Clarizen** tooopen hello **Configure sign-on** window.</span></span>

    ![Clic su "Configure Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Finestra "Configura accesso", con i file e gli URL](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="7630c-175">In una finestra del web browser, accedere come amministratore nel sito della società Clarizen di tooyour.</span><span class="sxs-lookup"><span data-stu-id="7630c-175">In a different web browser window, sign in tooyour Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="7630c-176">Fare clic sul nome utente e quindi su **Settings** (Impostazioni).</span><span class="sxs-lookup"><span data-stu-id="7630c-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="7630c-177">![Clic su "Settings" (Impostazioni) sotto il nome utente](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings (Impostazioni)")</span><span class="sxs-lookup"><span data-stu-id="7630c-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="7630c-178">Fare clic su hello **impostazioni globali** scheda. Quindi, Avanti troppo**autenticazione federata**, fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="7630c-178">Click hello **Global Settings** tab. Then, next too**Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="7630c-179">![Scheda "Global Settings" (Impostazioni globali)](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings (Impostazioni globali)")</span><span class="sxs-lookup"><span data-stu-id="7630c-179">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="7630c-180">In hello **autenticazione federata** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7630c-180">In hello **Federated Authentication** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="7630c-181">![Finestra di dialogo "Federated Authentication"(Autenticazione federata)](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication (Autenticazione federata)")</span><span class="sxs-lookup"><span data-stu-id="7630c-181">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="7630c-182">a.</span><span class="sxs-lookup"><span data-stu-id="7630c-182">a.</span></span> <span data-ttu-id="7630c-183">Selezionare **Enable Federated Authentication** (Abilita autenticazione federata).</span><span class="sxs-lookup"><span data-stu-id="7630c-183">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="7630c-184">b.</span><span class="sxs-lookup"><span data-stu-id="7630c-184">b.</span></span> <span data-ttu-id="7630c-185">Fare clic su **caricare** tooupload il certificato scaricato.</span><span class="sxs-lookup"><span data-stu-id="7630c-185">Click **Upload** tooupload your downloaded certificate.</span></span>

    <span data-ttu-id="7630c-186">c.</span><span class="sxs-lookup"><span data-stu-id="7630c-186">c.</span></span> <span data-ttu-id="7630c-187">In hello **URL di accesso** , immettere il valore di hello di **SAML Single Sign-On Service URL** dalla finestra di configurazione dell'applicazione hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7630c-187">In hello **Sign-in URL** box, enter hello value of **SAML Single Sign-On Service URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="7630c-188">d.</span><span class="sxs-lookup"><span data-stu-id="7630c-188">d.</span></span> <span data-ttu-id="7630c-189">In hello **Sign-Out URL** , immettere il valore di hello di **Sign-Out URL** dalla finestra di configurazione dell'applicazione hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7630c-189">In hello **Sign-out URL** box, enter hello value of **Sign-Out URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="7630c-190">e.</span><span class="sxs-lookup"><span data-stu-id="7630c-190">e.</span></span> <span data-ttu-id="7630c-191">Selezionare **Utilizza POST**.</span><span class="sxs-lookup"><span data-stu-id="7630c-191">Select **Use POST**.</span></span>

    <span data-ttu-id="7630c-192">f.</span><span class="sxs-lookup"><span data-stu-id="7630c-192">f.</span></span> <span data-ttu-id="7630c-193">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="7630c-193">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7630c-194">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7630c-194">Create an Azure AD test user</span></span>
<span data-ttu-id="7630c-195">Nel portale di Azure hello, creare un utente di test denominato Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7630c-195">In hello Azure portal, create a test user called Britta Simon.</span></span>

![Nome e l'indirizzo e-mail dell'utente di prova hello Azure AD][100]

1. <span data-ttu-id="7630c-197">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="7630c-197">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Icona Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7630c-199">Fare clic su **utenti e gruppi**, quindi fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="7630c-199">Click **Users and groups**, and then click **All users** toodisplay hello list of users.</span></span>

    ![Clic su "Utenti e gruppi" e su "Tutti gli utenti"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7630c-201">Nella parte superiore di hello della finestra di dialogo hello, fare clic su **Aggiungi** tooopen hello **utente** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7630c-201">At hello top of hello dialog box, click **Add** tooopen hello **User** dialog box.</span></span>

    ![pulsante "Aggiungi" Hello](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7630c-203">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7630c-203">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Finestra di dialogo "Utente" con nome, indirizzo di posta elettronica e password inseriti](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7630c-205">a.</span><span class="sxs-lookup"><span data-stu-id="7630c-205">a.</span></span> <span data-ttu-id="7630c-206">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7630c-206">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7630c-207">b.</span><span class="sxs-lookup"><span data-stu-id="7630c-207">b.</span></span> <span data-ttu-id="7630c-208">In hello **nome utente** casella Indirizzo di posta elettronica hello tipo di account di Britta Simon hello.</span><span class="sxs-lookup"><span data-stu-id="7630c-208">In hello **User name** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="7630c-209">c.</span><span class="sxs-lookup"><span data-stu-id="7630c-209">c.</span></span> <span data-ttu-id="7630c-210">Selezionare **Show Password** e annotare il valore di hello di **Password**.</span><span class="sxs-lookup"><span data-stu-id="7630c-210">Select **Show Password** and write down hello value of **Password**.</span></span>

    <span data-ttu-id="7630c-211">d.</span><span class="sxs-lookup"><span data-stu-id="7630c-211">d.</span></span> <span data-ttu-id="7630c-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7630c-212">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="7630c-213">Creare un utente di test di Clarizen</span><span class="sxs-lookup"><span data-stu-id="7630c-213">Create a Clarizen test user</span></span>
<span data-ttu-id="7630c-214">tooenable toosign agli utenti di Azure AD in tooClarizen, è necessario eseguire il provisioning degli account utente.</span><span class="sxs-lookup"><span data-stu-id="7630c-214">tooenable Azure AD users toosign in tooClarizen, you must provision user accounts.</span></span> <span data-ttu-id="7630c-215">Nel caso di hello di Clarizen, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="7630c-215">In hello case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="7630c-216">Accedi tooyour sito della società Clarizen come amministratore.</span><span class="sxs-lookup"><span data-stu-id="7630c-216">Sign in tooyour Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="7630c-217">Fare clic su **Persone**.</span><span class="sxs-lookup"><span data-stu-id="7630c-217">Click **People**.</span></span>

    <span data-ttu-id="7630c-218">![Clic su "People" (Persone)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People (Persone)")</span><span class="sxs-lookup"><span data-stu-id="7630c-218">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="7630c-219">Fare clic su **Invite User**.</span><span class="sxs-lookup"><span data-stu-id="7630c-219">Click **Invite User**.</span></span>

    <span data-ttu-id="7630c-220">![Pulsante "Invite User" (Invita l'utente)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invitare utenti")</span><span class="sxs-lookup"><span data-stu-id="7630c-220">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="7630c-221">In hello **Invite People** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7630c-221">In hello **Invite People** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="7630c-222">![Finestra di dialogo "Invite People" (Invita persone)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People (Invita persone)")</span><span class="sxs-lookup"><span data-stu-id="7630c-222">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="7630c-223">a.</span><span class="sxs-lookup"><span data-stu-id="7630c-223">a.</span></span> <span data-ttu-id="7630c-224">In hello **posta elettronica** casella Indirizzo di posta elettronica hello tipo di account di Britta Simon hello.</span><span class="sxs-lookup"><span data-stu-id="7630c-224">In hello **Email** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="7630c-225">b.</span><span class="sxs-lookup"><span data-stu-id="7630c-225">b.</span></span> <span data-ttu-id="7630c-226">Fare clic su **Invita**.</span><span class="sxs-lookup"><span data-stu-id="7630c-226">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7630c-227">titolare dell'account di Hello Azure Active Directory riceverà un messaggio di posta elettronica e seguire il proprio account tooconfirm un collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="7630c-227">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7630c-228">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7630c-228">Assign hello Azure AD test user</span></span>
<span data-ttu-id="7630c-229">Abilitare Britta Simon toouse single sign-on Azure concedendo tooClarizen proprio accesso.</span><span class="sxs-lookup"><span data-stu-id="7630c-229">Enable Britta Simon toouse Azure single sign-on by granting her access tooClarizen.</span></span>

![Utente di test assegnato][200]

1. <span data-ttu-id="7630c-231">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello visualizzazione directory toohello browse, fare clic su **applicazioni aziendali**, quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7630c-231">In hello Azure portal, open hello applications view, browse toohello directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Clic su "Applicazioni aziendali" e su "Tutte le applicazioni"][201]

2. <span data-ttu-id="7630c-233">Nell'elenco di applicazioni hello, selezionare **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="7630c-233">In hello applications list, select **Clarizen**.</span></span>

    ![Selezione di Clarizen nell'elenco di hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="7630c-235">Nel riquadro di sinistra hello, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7630c-235">In hello left pane, click **Users and groups**.</span></span>

    ![Clic su "Utenti e gruppi"][202]

4. <span data-ttu-id="7630c-237">Fare clic su hello **Aggiungi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7630c-237">Click hello **Add** button.</span></span> <span data-ttu-id="7630c-238">Quindi, nel hello **Aggiungi** nella finestra di dialogo **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7630c-238">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![pulsante "Aggiungi" Hello e finestra di dialogo "Aggiungi assegnazione" hello][203]

5. <span data-ttu-id="7630c-240">In hello **utenti e gruppi** nella finestra di dialogo **Britta Simon** elenco hello degli utenti.</span><span class="sxs-lookup"><span data-stu-id="7630c-240">In hello **Users and groups** dialog box, select **Britta Simon** in hello list of users.</span></span>

6. <span data-ttu-id="7630c-241">In hello **utenti e gruppi** finestra di dialogo fare clic su hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7630c-241">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="7630c-242">In hello **Aggiungi** finestra di dialogo fare clic su hello **assegnare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7630c-242">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="7630c-243">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7630c-243">Test single sign-on</span></span>
<span data-ttu-id="7630c-244">Test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7630c-244">Test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="7630c-245">Quando si fa clic su riquadro Clarizen hello in hello Pannello di accesso, devono essere connessi automaticamente tooyour applicazione Clarizen.</span><span class="sxs-lookup"><span data-stu-id="7630c-245">When you click hello Clarizen tile in hello Access Panel, you should be automatically signed in tooyour Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7630c-246">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7630c-246">Additional resources</span></span>

* [<span data-ttu-id="7630c-247">Elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7630c-247">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7630c-248">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7630c-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
