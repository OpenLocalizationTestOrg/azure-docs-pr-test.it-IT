---
title: 'Esercitazione: Integrazione di Azure Active Directory con Greenhouse | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Greenhouse.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 1a7cdd00c4f2b15a1afc89522d79af22f4c5d866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="af039-103">Esercitazione: Integrazione di Azure Active Directory con Greenhouse</span><span class="sxs-lookup"><span data-stu-id="af039-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>

<span data-ttu-id="af039-104">In questa esercitazione, è illustrato come toointegrate Greenhouse con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="af039-104">In this tutorial, you learn how toointegrate Greenhouse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="af039-105">Integrazione di Greenhouse con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="af039-105">Integrating Greenhouse with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="af039-106">È possibile controllare in Azure AD che ha accesso tooGreenhouse.</span><span class="sxs-lookup"><span data-stu-id="af039-106">You can control in Azure AD who has access tooGreenhouse.</span></span>
- <span data-ttu-id="af039-107">È possibile abilitare l'utenti tooautomatically get connesso tooGreenhouse (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af039-107">You can enable your users tooautomatically get signed-on tooGreenhouse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="af039-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="af039-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="af039-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="af039-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af039-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="af039-110">Prerequisites</span></span>

<span data-ttu-id="af039-111">integrazione di Azure AD con Greenhouse tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="af039-111">tooconfigure Azure AD integration with Greenhouse, you need hello following items:</span></span>

- <span data-ttu-id="af039-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af039-112">An Azure AD subscription</span></span>
- <span data-ttu-id="af039-113">Sottoscrizione di Greenhouse abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="af039-113">A Greenhouse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="af039-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="af039-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="af039-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="af039-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="af039-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="af039-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="af039-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="af039-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="af039-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="af039-118">Scenario description</span></span>
<span data-ttu-id="af039-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="af039-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="af039-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="af039-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="af039-121">Aggiunta di Greenhouse dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="af039-121">Adding Greenhouse from hello gallery</span></span>
2. <span data-ttu-id="af039-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af039-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-greenhouse-from-hello-gallery"></a><span data-ttu-id="af039-123">Aggiunta di Greenhouse dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="af039-123">Adding Greenhouse from hello gallery</span></span>
<span data-ttu-id="af039-124">integrazione hello tooconfigure di Greenhouse in Azure AD, è necessario tooadd Greenhouse dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="af039-124">tooconfigure hello integration of Greenhouse into Azure AD, you need tooadd Greenhouse from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="af039-125">**tooadd Greenhouse dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="af039-125">**tooadd Greenhouse from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="af039-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="af039-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="af039-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="af039-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="af039-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="af039-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="af039-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="af039-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="af039-133">Nella casella di ricerca hello, digitare **Greenhouse**selezionare **Greenhouse** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="af039-133">In hello search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello Greenhouse](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="af039-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af039-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="af039-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Greenhouse in base a un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="af039-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="af039-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Greenhouse è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af039-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Greenhouse is tooa user in Azure AD.</span></span> <span data-ttu-id="af039-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Greenhouse deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="af039-138">In other words, a link relationship between an Azure AD user and hello related user in Greenhouse needs toobe established.</span></span>

<span data-ttu-id="af039-139">In Greenhouse, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="af039-139">In Greenhouse, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="af039-140">tooconfigure e prova AD Azure single sign-on con Greenhouse, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="af039-140">tooconfigure and test Azure AD single sign-on with Greenhouse, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="af039-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="af039-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="af039-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="af039-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="af039-143">**[Creare un utente test Greenhouse](#create-a-greenhouse-test-user)**  -toohave un equivalente di Britta Simon in Greenhouse che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="af039-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - toohave a counterpart of Britta Simon in Greenhouse that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="af039-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="af039-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="af039-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="af039-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="af039-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af039-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="af039-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="af039-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Greenhouse application.</span></span>

<span data-ttu-id="af039-148">**Azure AD tooconfigure single sign-on con Greenhouse, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="af039-148">**tooconfigure Azure AD single sign-on with Greenhouse, perform hello following steps:**</span></span>

1. <span data-ttu-id="af039-149">Nel portale di Azure su hello hello **Greenhouse** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="af039-149">In hello Azure portal, on hello **Greenhouse** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="af039-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="af039-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

3. <span data-ttu-id="af039-153">In hello **Greenhouse dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="af039-153">On hello **Greenhouse Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Greenhouse](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_url.png)

    <span data-ttu-id="af039-155">a.</span><span class="sxs-lookup"><span data-stu-id="af039-155">a.</span></span> <span data-ttu-id="af039-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="af039-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.greenhouse.io`</span></span>

    <span data-ttu-id="af039-157">b.</span><span class="sxs-lookup"><span data-stu-id="af039-157">b.</span></span> <span data-ttu-id="af039-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="af039-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.greenhouse.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="af039-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="af039-159">These values are not real.</span></span> <span data-ttu-id="af039-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="af039-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="af039-161">Contatto [team di supporto di Greenhouse Client](https://www.greenhouse.io/contact) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="af039-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) tooget these values.</span></span> 
 


4. <span data-ttu-id="af039-162">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="af039-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

5. <span data-ttu-id="af039-164">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="af039-164">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-greenhouse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="af039-166">tooconfigure single sign-on sul **Greenhouse** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto di Greenhouse](http://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="af039-166">tooconfigure single sign-on on **Greenhouse** side, you need toosend hello downloaded **Metadata XML** too[Greenhouse support team](http://www.greenhouse.io/contact).</span></span>

> [!TIP]
> <span data-ttu-id="af039-167">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="af039-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="af039-168">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="af039-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="af039-169">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="af039-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="af039-170">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="af039-170">Create an Azure AD test user</span></span>

<span data-ttu-id="af039-171">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="af039-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="af039-173">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="af039-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="af039-174">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="af039-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="af039-176">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="af039-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="af039-178">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="af039-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="af039-180">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="af039-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="af039-182">a.</span><span class="sxs-lookup"><span data-stu-id="af039-182">a.</span></span> <span data-ttu-id="af039-183">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="af039-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="af039-184">b.</span><span class="sxs-lookup"><span data-stu-id="af039-184">b.</span></span> <span data-ttu-id="af039-185">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="af039-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="af039-186">c.</span><span class="sxs-lookup"><span data-stu-id="af039-186">c.</span></span> <span data-ttu-id="af039-187">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="af039-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="af039-188">d.</span><span class="sxs-lookup"><span data-stu-id="af039-188">d.</span></span> <span data-ttu-id="af039-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="af039-189">Click **Create**.</span></span>
 
### <a name="create-a-greenhouse-test-user"></a><span data-ttu-id="af039-190">Creare un utente di test di Greenhouse</span><span class="sxs-lookup"><span data-stu-id="af039-190">Create a Greenhouse test user</span></span>

<span data-ttu-id="af039-191">In ordine tooenable Azure AD utenti toolog a Greenhouse, è necessario eseguirne il provisioning in Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="af039-191">In order tooenable Azure AD users toolog into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="af039-192">Nel caso di hello di Greenhouse, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="af039-192">In hello case of Greenhouse, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="af039-193">È possibile usare qualsiasi altro Greenhouse utente account strumento di creazione o le API fornite da Greenhouse tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="af039-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="af039-194">**eseguire un account utente, tooprovision hello i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="af039-194">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="af039-195">Accedi tooyour **Greenhouse** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="af039-195">Log in tooyour **Greenhouse** company site as an administrator.</span></span>

2. <span data-ttu-id="af039-196">Scegliere dal menu hello in primo piano hello **configura**, quindi fare clic su **utenti**.</span><span class="sxs-lookup"><span data-stu-id="af039-196">In hello menu on hello top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="af039-197">![Utenti](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="af039-197">![Users](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Users")</span></span>

3. <span data-ttu-id="af039-198">Fare clic su **Nuovi utenti**.</span><span class="sxs-lookup"><span data-stu-id="af039-198">Click **New Users**.</span></span>
   
   <span data-ttu-id="af039-199">![Nuovo utente](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="af039-199">![New User](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "New User")</span></span>

4. <span data-ttu-id="af039-200">In hello **Add New User** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="af039-200">In hello **Add New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="af039-201">![Aggiungi nuovo utente](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Aggiungi nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="af039-201">![Add New User](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Add New User")</span></span>

   <span data-ttu-id="af039-202">a.</span><span class="sxs-lookup"><span data-stu-id="af039-202">a.</span></span> <span data-ttu-id="af039-203">In hello **immettere messaggi di posta elettronica utente** casella di testo, digitare hello di indirizzo di posta elettronica di un account Azure Active Directory valido, si desidera tooprovision.</span><span class="sxs-lookup"><span data-stu-id="af039-203">In hello **Enter user emails** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision.</span></span>

   <span data-ttu-id="af039-204">b.</span><span class="sxs-lookup"><span data-stu-id="af039-204">b.</span></span> <span data-ttu-id="af039-205">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="af039-205">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="af039-206">i titolari dell'account Azure Active Directory Hello riceverà un messaggio di posta elettronica tra un account di hello tooconfirm collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="af039-206">hello Azure Active Directory account holders will receive an email including a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="af039-207">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="af039-207">Assign hello Azure AD test user</span></span>

<span data-ttu-id="af039-208">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooGreenhouse.</span><span class="sxs-lookup"><span data-stu-id="af039-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGreenhouse.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="af039-210">**tooassign Britta Simon tooGreenhouse, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="af039-210">**tooassign Britta Simon tooGreenhouse, perform hello following steps:**</span></span>

1. <span data-ttu-id="af039-211">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="af039-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="af039-213">Nell'elenco di applicazioni hello, selezionare **Greenhouse**.</span><span class="sxs-lookup"><span data-stu-id="af039-213">In hello applications list, select **Greenhouse**.</span></span>

    ![collegamento di Greenhouse Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_app.png)  

3. <span data-ttu-id="af039-215">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="af039-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="af039-217">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="af039-217">Click **Add** button.</span></span> <span data-ttu-id="af039-218">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="af039-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="af039-220">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="af039-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="af039-221">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="af039-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="af039-222">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="af039-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="af039-223">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="af039-223">Test single sign-on</span></span>

<span data-ttu-id="af039-224">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="af039-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="af039-225">Quando si fa clic su riquadro Greenhouse hello in hello Pannello di accesso, è necessario ottenere applicazione Greenhouse tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="af039-225">When you click hello Greenhouse tile in hello Access Panel, you should get automatically signed-on tooyour Greenhouse application.</span></span>
<span data-ttu-id="af039-226">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="af039-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="af039-227">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="af039-227">Additional resources</span></span>

* [<span data-ttu-id="af039-228">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af039-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="af039-229">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af039-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_203.png

