---
title: 'Esercitazione: Integrazione di Azure Active Directory con Workrite | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Workrite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: a663374ae3c8b102b53d8cf05a9cb083b80dbb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="3e48d-103">Esercitazione: Integrazione di Azure Active Directory con Workrite</span><span class="sxs-lookup"><span data-stu-id="3e48d-103">Tutorial: Azure Active Directory integration with Workrite</span></span>

<span data-ttu-id="3e48d-104">In questa esercitazione, è illustrato come toointegrate Workrite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e48d-104">In this tutorial, you learn how toointegrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3e48d-105">Integrazione Workrite con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="3e48d-105">Integrating Workrite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3e48d-106">È possibile controllare in Azure AD che ha accesso tooWorkrite.</span><span class="sxs-lookup"><span data-stu-id="3e48d-106">You can control in Azure AD who has access tooWorkrite.</span></span>
- <span data-ttu-id="3e48d-107">È possibile abilitare l'utenti tooautomatically get connesso tooWorkrite (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e48d-107">You can enable your users tooautomatically get signed-on tooWorkrite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3e48d-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3e48d-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="3e48d-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3e48d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e48d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3e48d-110">Prerequisites</span></span>

<span data-ttu-id="3e48d-111">integrazione di Azure AD con Workrite tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="3e48d-111">tooconfigure Azure AD integration with Workrite, you need hello following items:</span></span>

- <span data-ttu-id="3e48d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e48d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3e48d-113">Sottoscrizione di Workrite abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3e48d-113">A Workrite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3e48d-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="3e48d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3e48d-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="3e48d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3e48d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="3e48d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3e48d-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e48d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3e48d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="3e48d-118">Scenario description</span></span>
<span data-ttu-id="3e48d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="3e48d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3e48d-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="3e48d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3e48d-121">Aggiunta di Workrite dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="3e48d-121">Adding Workrite from hello gallery</span></span>
2. <span data-ttu-id="3e48d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e48d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workrite-from-hello-gallery"></a><span data-ttu-id="3e48d-123">Aggiunta di Workrite dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="3e48d-123">Adding Workrite from hello gallery</span></span>
<span data-ttu-id="3e48d-124">integrazione hello tooconfigure di Workrite in Azure AD, è necessario tooadd Workrite dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="3e48d-124">tooconfigure hello integration of Workrite into Azure AD, you need tooadd Workrite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3e48d-125">**tooadd Workrite dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e48d-125">**tooadd Workrite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e48d-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="3e48d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="3e48d-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3e48d-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="3e48d-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="3e48d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="3e48d-133">Nella casella di ricerca hello, digitare **Workrite**selezionare **Workrite** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="3e48d-133">In hello search box, type **Workrite**, select **Workrite** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3e48d-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e48d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3e48d-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Workrite in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3e48d-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3e48d-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Workrite è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e48d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workrite is tooa user in Azure AD.</span></span> <span data-ttu-id="3e48d-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Workrite deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="3e48d-138">In other words, a link relationship between an Azure AD user and hello related user in Workrite needs toobe established.</span></span>

<span data-ttu-id="3e48d-139">In Workrite, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="3e48d-139">In Workrite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3e48d-140">tooconfigure e prova AD Azure single sign-on con Workrite, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="3e48d-140">tooconfigure and test Azure AD single sign-on with Workrite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3e48d-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3e48d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3e48d-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e48d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3e48d-143">**[Creare un utente test Workrite](#create-a-workrite-test-user)**  -toohave un equivalente di Britta Simon in Workrite che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3e48d-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - toohave a counterpart of Britta Simon in Workrite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3e48d-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3e48d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3e48d-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="3e48d-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3e48d-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e48d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3e48d-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Workrite.</span><span class="sxs-lookup"><span data-stu-id="3e48d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workrite application.</span></span>

<span data-ttu-id="3e48d-148">**Azure AD tooconfigure single sign-on con Workrite, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e48d-148">**tooconfigure Azure AD single sign-on with Workrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e48d-149">Nel portale di Azure su hello hello **Workrite** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-149">In hello Azure portal, on hello **Workrite** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="3e48d-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3e48d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_samlbase.png)

3. <span data-ttu-id="3e48d-153">In hello **Workrite dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3e48d-153">On hello **Workrite Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_url.png)

    <span data-ttu-id="3e48d-155">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="3e48d-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3e48d-156">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="3e48d-156">This value is not real.</span></span> <span data-ttu-id="3e48d-157">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="3e48d-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="3e48d-158">Contatto [team di supporto Workrite Client](mailto:support@workrite.co.uk) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="3e48d-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) tooget this value.</span></span>

4. <span data-ttu-id="3e48d-159">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="3e48d-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_certificate.png) 

5. <span data-ttu-id="3e48d-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="3e48d-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-workrite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3e48d-163">In hello **Workrite configurazione** fare clic su **configurare Workrite** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="3e48d-163">On hello **Workrite Configuration** section, click **Configure Workrite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3e48d-164">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="3e48d-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_configure.png) 

7. <span data-ttu-id="3e48d-166">tooconfigure single sign-on sul **Workrite** lato, è necessario hello toosend scaricato **Certificate(Base64), Sign-Out URL, ID entità SAML e SAML Single Sign-On Service URL** troppo[Workrite team di supporto](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="3e48d-166">tooconfigure single sign-on on **Workrite** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Workrite support team](mailto:support@workrite.co.uk).</span></span>

> [!TIP]
> <span data-ttu-id="3e48d-167">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="3e48d-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3e48d-168">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="3e48d-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3e48d-169">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3e48d-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3e48d-170">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e48d-170">Create an Azure AD test user</span></span>

<span data-ttu-id="3e48d-171">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="3e48d-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="3e48d-173">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e48d-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e48d-174">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="3e48d-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-workrite-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3e48d-176">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-workrite-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3e48d-178">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="3e48d-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-workrite-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3e48d-180">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3e48d-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-workrite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3e48d-182">a.</span><span class="sxs-lookup"><span data-stu-id="3e48d-182">a.</span></span> <span data-ttu-id="3e48d-183">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3e48d-184">b.</span><span class="sxs-lookup"><span data-stu-id="3e48d-184">b.</span></span> <span data-ttu-id="3e48d-185">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3e48d-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="3e48d-186">c.</span><span class="sxs-lookup"><span data-stu-id="3e48d-186">c.</span></span> <span data-ttu-id="3e48d-187">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="3e48d-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="3e48d-188">d.</span><span class="sxs-lookup"><span data-stu-id="3e48d-188">d.</span></span> <span data-ttu-id="3e48d-189">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-189">Click **Create**.</span></span>
 
### <a name="create-a-workrite-test-user"></a><span data-ttu-id="3e48d-190">Creare un utente test di Workrite</span><span class="sxs-lookup"><span data-stu-id="3e48d-190">Create a Workrite test user</span></span>

<span data-ttu-id="3e48d-191">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Workrite toocreate.</span><span class="sxs-lookup"><span data-stu-id="3e48d-191">hello objective of this section is toocreate a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="3e48d-192">**un utente denominato Britta Simon in Workrite, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e48d-192">**toocreate a user called Britta Simon in Workrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e48d-193">Accedere al sito della società workrite tooyour come amministratore.</span><span class="sxs-lookup"><span data-stu-id="3e48d-193">Sign on tooyour workrite company site as administrator.</span></span>

2. <span data-ttu-id="3e48d-194">Nel riquadro di spostamento hello, fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-194">In hello navigation pane, click **Admin**.</span></span>
   
    ![Controllo Admin][400]

3. <span data-ttu-id="3e48d-196">Vai tooQuick collegamenti e quindi fare clic su **creare un utente**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-196">Go tooQuick Links, and then click **Create a User**.</span></span>
   
    ![Sezione Create a User (Crea un utente)][401]

4. <span data-ttu-id="3e48d-198">In hello **Create User** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3e48d-198">On hello **Create User** dialog, perform hello following steps:</span></span>
   
    ![Finestra di dialogo Create User (Crea utente)][402]
    
    <span data-ttu-id="3e48d-200">a.</span><span class="sxs-lookup"><span data-stu-id="3e48d-200">a.</span></span> <span data-ttu-id="3e48d-201">In hello **posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3e48d-201">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="3e48d-202">b.</span><span class="sxs-lookup"><span data-stu-id="3e48d-202">b.</span></span> <span data-ttu-id="3e48d-203">In hello **nome** casella Tipo hello firstname dell'utente come Laura.</span><span class="sxs-lookup"><span data-stu-id="3e48d-203">In hello **First Name** textbox, type hello firstname of user like Britta.</span></span>

    <span data-ttu-id="3e48d-204">c.</span><span class="sxs-lookup"><span data-stu-id="3e48d-204">c.</span></span> <span data-ttu-id="3e48d-205">In hello **Surname** casella di testo surname hello tipo di utente come Simon.</span><span class="sxs-lookup"><span data-stu-id="3e48d-205">In hello **Surname** textbox, type hello surname of user like Simon.</span></span>
    
    <span data-ttu-id="3e48d-206">d.</span><span class="sxs-lookup"><span data-stu-id="3e48d-206">d.</span></span> <span data-ttu-id="3e48d-207">Selezionare **Client Administrator** in **Choose Role**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-207">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="3e48d-208">e.</span><span class="sxs-lookup"><span data-stu-id="3e48d-208">e.</span></span> <span data-ttu-id="3e48d-209">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-209">Click **Save**.</span></span>   

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="3e48d-210">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3e48d-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="3e48d-211">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWorkrite.</span><span class="sxs-lookup"><span data-stu-id="3e48d-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkrite.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="3e48d-213">**tooassign Britta Simon tooWorkrite, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="3e48d-213">**tooassign Britta Simon tooWorkrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="3e48d-214">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="3e48d-216">Nell'elenco di applicazioni hello, selezionare **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-216">In hello applications list, select **Workrite**.</span></span>

    ![collegamento Workrite Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_app.png)  

3. <span data-ttu-id="3e48d-218">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="3e48d-220">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-220">Click **Add** button.</span></span> <span data-ttu-id="3e48d-221">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="3e48d-223">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="3e48d-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3e48d-224">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3e48d-225">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="3e48d-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3e48d-226">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3e48d-226">Test single sign-on</span></span>

<span data-ttu-id="3e48d-227">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="3e48d-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="3e48d-228">Quando si fa clic su riquadro Workrite hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Workrite applicazione.</span><span class="sxs-lookup"><span data-stu-id="3e48d-228">When you click hello Workrite tile in hello Access Panel, you should get automatically signed-on tooyour Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3e48d-229">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="3e48d-229">Additional resources</span></span>

* [<span data-ttu-id="3e48d-230">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e48d-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3e48d-231">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e48d-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_400.png
[401]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_401.png
[402]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_402.png

