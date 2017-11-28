---
title: 'Esercitazione: Integrazione di Azure Active Directory con Springer Link | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e collegamento Benedetti.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 58cdf029-bdc0-43c4-a469-b921c2a669bd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: jeedes
ms.openlocfilehash: dabd2f72b3a195fc359826a4863a197e5019f5c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springer-link"></a><span data-ttu-id="ba046-103">Esercitazione: Integrazione di Azure Active Directory con Springer Link</span><span class="sxs-lookup"><span data-stu-id="ba046-103">Tutorial: Azure Active Directory integration with Springer Link</span></span>

<span data-ttu-id="ba046-104">In questa esercitazione, è illustrato come toointegrate Benedetti collegare con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ba046-104">In this tutorial, you learn how toointegrate Springer Link with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ba046-105">Integrazione di collegamento Benedetti con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="ba046-105">Integrating Springer Link with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ba046-106">È possibile controllare in Azure AD che ha accesso tooSpringer collegamento.</span><span class="sxs-lookup"><span data-stu-id="ba046-106">You can control in Azure AD who has access tooSpringer Link.</span></span>
- <span data-ttu-id="ba046-107">È possibile abilitare l'utenti tooautomatically get connesso tooSpringer collegamento (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba046-107">You can enable your users tooautomatically get signed-on tooSpringer Link (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ba046-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba046-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="ba046-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ba046-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba046-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ba046-110">Prerequisites</span></span>

<span data-ttu-id="ba046-111">integrazione di Azure AD con collegamento Benedetti tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ba046-111">tooconfigure Azure AD integration with Springer Link, you need hello following items:</span></span>

- <span data-ttu-id="ba046-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba046-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ba046-113">Sottoscrizione di Springer Link abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ba046-113">A Springer Link single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ba046-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ba046-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ba046-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="ba046-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ba046-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ba046-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ba046-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ba046-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ba046-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ba046-118">Scenario description</span></span>
<span data-ttu-id="ba046-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ba046-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ba046-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="ba046-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ba046-121">L'aggiunta di collegamento Benedetti dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ba046-121">Adding Springer Link from hello gallery</span></span>
2. <span data-ttu-id="ba046-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba046-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springer-link-from-hello-gallery"></a><span data-ttu-id="ba046-123">L'aggiunta di collegamento Benedetti dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ba046-123">Adding Springer Link from hello gallery</span></span>
<span data-ttu-id="ba046-124">integrazione hello tooconfigure di collegamento Benedetti in Azure AD, è necessario tooadd Benedetti collegamento dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ba046-124">tooconfigure hello integration of Springer Link into Azure AD, you need tooadd Springer Link from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ba046-125">**tooadd collegamento Benedetti dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ba046-125">**tooadd Springer Link from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba046-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ba046-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="ba046-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ba046-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ba046-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ba046-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="ba046-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ba046-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="ba046-133">Nella casella di ricerca hello, digitare **collegamento Benedetti**selezionare **collegamento Benedetti** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ba046-133">In hello search box, type **Springer Link**, select **Springer Link** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Collegamento Benedetti nell'elenco risultati hello](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ba046-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba046-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ba046-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Springer Link con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ba046-136">In this section, you configure and test Azure AD single sign-on with Springer Link based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ba046-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nel collegamento Benedetti è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba046-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Springer Link is tooa user in Azure AD.</span></span> <span data-ttu-id="ba046-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e utente correlato di hello nel collegamento Benedetti deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="ba046-138">In other words, a link relationship between an Azure AD user and hello related user in Springer Link needs toobe established.</span></span>

<span data-ttu-id="ba046-139">Nel collegamento Benedetti, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="ba046-139">In Springer Link, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ba046-140">tooconfigure e prova AD Azure single sign-on con Benedetti collegamento, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="ba046-140">tooconfigure and test Azure AD single sign-on with Springer Link, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ba046-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ba046-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ba046-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ba046-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ba046-143">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ba046-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="ba046-144">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="ba046-144">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ba046-145">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba046-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ba046-146">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Benedetti collegamento.</span><span class="sxs-lookup"><span data-stu-id="ba046-146">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Springer Link application.</span></span>

<span data-ttu-id="ba046-147">**Azure AD tooconfigure single sign-on con collegamento Benedetti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ba046-147">**tooconfigure Azure AD single sign-on with Springer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba046-148">Nel portale di Azure su hello hello **collegamento Benedetti** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ba046-148">In hello Azure portal, on hello **Springer Link** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="ba046-150">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ba046-150">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_samlbase.png)

3. <span data-ttu-id="ba046-152">In hello **Benedetti collegamento dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="ba046-152">On hello **Springer Link Domain and URLs** section,  If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Informazioni su URL e dominio Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url1.png)

    <span data-ttu-id="ba046-154">a.</span><span class="sxs-lookup"><span data-stu-id="ba046-154">a.</span></span> <span data-ttu-id="ba046-155">In hello **identificatore** casella di testo, digitare l'URL hello:`https://fsso.springer.com`</span><span class="sxs-lookup"><span data-stu-id="ba046-155">In hello **Identifier** textbox, type hello URL: `https://fsso.springer.com`</span></span>

    <span data-ttu-id="ba046-156">b.</span><span class="sxs-lookup"><span data-stu-id="ba046-156">b.</span></span> <span data-ttu-id="ba046-157">In hello **URL di risposta** casella di testo, digitare l'URL hello:`https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="ba046-157">In hello **Reply URL** textbox, type hello URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

4. <span data-ttu-id="ba046-158">Selezionare **Mostra impostazioni URL avanzate**</span><span class="sxs-lookup"><span data-stu-id="ba046-158">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="ba046-159">Se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="ba046-159">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Informazioni su URL e dominio Springer Link](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url.png)

    <span data-ttu-id="ba046-161">In hello **Sign-on URL** casella di testo, digitare l'URL hello:`https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="ba046-161">In hello **Sign-on URL** textbox, type hello URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

5. <span data-ttu-id="ba046-162">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ba046-162">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-springerlink-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ba046-164">hello toogenerate **metadati** url, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ba046-164">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="ba046-165">a.</span><span class="sxs-lookup"><span data-stu-id="ba046-165">a.</span></span> <span data-ttu-id="ba046-166">Fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="ba046-166">Click **App registrations**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appregistrations.png)
   
    <span data-ttu-id="ba046-168">b.</span><span class="sxs-lookup"><span data-stu-id="ba046-168">b.</span></span> <span data-ttu-id="ba046-169">Fare clic su **endpoint** tooopen **endpoint** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ba046-169">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpointicon.png)

    <span data-ttu-id="ba046-171">c.</span><span class="sxs-lookup"><span data-stu-id="ba046-171">c.</span></span> <span data-ttu-id="ba046-172">Fare clic su hello copia pulsante toocopy **documento metadati federazione** url e incollarlo nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="ba046-172">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpoint.png)
     
    <span data-ttu-id="ba046-174">d.</span><span class="sxs-lookup"><span data-stu-id="ba046-174">d.</span></span> <span data-ttu-id="ba046-175">Ora passare toohello pagina delle proprietà di **collegamento Benedetti** e hello copia **Id applicazione** utilizzando **copia** pulsante e incollarlo nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="ba046-175">Now go toohello property page of **Springer Link** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appid.png)

    <span data-ttu-id="ba046-177">e.</span><span class="sxs-lookup"><span data-stu-id="ba046-177">e.</span></span> <span data-ttu-id="ba046-178">Generare hello **URL dei metadati** utilizzando hello seguente motivo:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="ba046-178">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="ba046-179">tooconfigure single sign-on sul **collegamento Benedetti** lato, è necessario hello toosend generato **URL dei metadati** troppo[team di supporto Benedetti collegamento](mailto:identity@springernature.com).</span><span class="sxs-lookup"><span data-stu-id="ba046-179">tooconfigure single sign-on on **Springer Link** side, you need toosend hello generated **Metadata URL** too[Springer Link support team](mailto:identity@springernature.com).</span></span>

> [!TIP]
> <span data-ttu-id="ba046-180">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="ba046-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ba046-181">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="ba046-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ba046-182">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ba046-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ba046-183">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba046-183">Create an Azure AD test user</span></span>

<span data-ttu-id="ba046-184">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ba046-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="ba046-186">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ba046-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba046-187">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ba046-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-springerlink-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ba046-189">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ba046-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-springerlink-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ba046-191">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ba046-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-springerlink-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ba046-193">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ba046-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-springerlink-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ba046-195">a.</span><span class="sxs-lookup"><span data-stu-id="ba046-195">a.</span></span> <span data-ttu-id="ba046-196">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ba046-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ba046-197">b.</span><span class="sxs-lookup"><span data-stu-id="ba046-197">b.</span></span> <span data-ttu-id="ba046-198">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ba046-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ba046-199">c.</span><span class="sxs-lookup"><span data-stu-id="ba046-199">c.</span></span> <span data-ttu-id="ba046-200">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="ba046-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ba046-201">d.</span><span class="sxs-lookup"><span data-stu-id="ba046-201">d.</span></span> <span data-ttu-id="ba046-202">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ba046-202">Click **Create**.</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ba046-203">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba046-203">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ba046-204">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSpringer collegamento.</span><span class="sxs-lookup"><span data-stu-id="ba046-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringer Link.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="ba046-206">**tooassign Britta Simon tooSpringer collegamento, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ba046-206">**tooassign Britta Simon tooSpringer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba046-207">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ba046-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ba046-209">Nell'elenco di applicazioni hello, selezionare **collegamento Benedetti**.</span><span class="sxs-lookup"><span data-stu-id="ba046-209">In hello applications list, select **Springer Link**.</span></span>

    ![Hello Benedetti collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_app.png)  

3. <span data-ttu-id="ba046-211">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ba046-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="ba046-213">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ba046-213">Click **Add** button.</span></span> <span data-ttu-id="ba046-214">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ba046-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="ba046-216">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="ba046-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ba046-217">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ba046-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ba046-218">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ba046-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ba046-219">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ba046-219">Test single sign-on</span></span>

<span data-ttu-id="ba046-220">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ba046-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ba046-221">Quando si fa clic su riquadro Benedetti collegamento hello in hello Pannello di accesso, è necessario ottenere applicazione Benedetti collegamento tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="ba046-221">When you click hello Springer Link tile in hello Access Panel, you should get automatically signed-on tooyour Springer Link application.</span></span>
<span data-ttu-id="ba046-222">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ba046-222">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ba046-223">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ba046-223">Additional resources</span></span>

* [<span data-ttu-id="ba046-224">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba046-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ba046-225">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba046-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_203.png

