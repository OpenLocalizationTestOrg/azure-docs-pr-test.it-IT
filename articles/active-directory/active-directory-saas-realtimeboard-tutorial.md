---
title: 'Esercitazione: Integrazione di Azure Active Directory con RealtimeBoard | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e RealtimeBoard.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a37fc1c0-4bae-4173-989b-00de53a0076f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: jeedes
ms.openlocfilehash: 76644c9ba643d61a903295dea4d417716a47774a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-realtimeboard"></a><span data-ttu-id="cf68d-103">Esercitazione: Integrazione di Azure Active Directory con RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="cf68d-103">Tutorial: Azure Active Directory integration with RealtimeBoard</span></span>

<span data-ttu-id="cf68d-104">In questa esercitazione, è illustrato come toointegrate RealtimeBoard con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cf68d-104">In this tutorial, you learn how toointegrate RealtimeBoard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cf68d-105">Integrazione RealtimeBoard con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="cf68d-105">Integrating RealtimeBoard with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cf68d-106">È possibile controllare in Azure AD che ha accesso tooRealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="cf68d-106">You can control in Azure AD who has access tooRealtimeBoard.</span></span>
- <span data-ttu-id="cf68d-107">È possibile abilitare l'utenti tooautomatically get connesso tooRealtimeBoard (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf68d-107">You can enable your users tooautomatically get signed-on tooRealtimeBoard (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cf68d-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cf68d-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="cf68d-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cf68d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf68d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cf68d-110">Prerequisites</span></span>

<span data-ttu-id="cf68d-111">integrazione di Azure AD con RealtimeBoard tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="cf68d-111">tooconfigure Azure AD integration with RealtimeBoard, you need hello following items:</span></span>

- <span data-ttu-id="cf68d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf68d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cf68d-113">Sottoscrizione di RealtimeBoard abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cf68d-113">A RealtimeBoard single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cf68d-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="cf68d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cf68d-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="cf68d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cf68d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="cf68d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cf68d-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cf68d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cf68d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="cf68d-118">Scenario description</span></span>
<span data-ttu-id="cf68d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="cf68d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cf68d-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="cf68d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cf68d-121">Aggiunta di RealtimeBoard dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cf68d-121">Adding RealtimeBoard from hello gallery</span></span>
2. <span data-ttu-id="cf68d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf68d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-realtimeboard-from-hello-gallery"></a><span data-ttu-id="cf68d-123">Aggiunta di RealtimeBoard dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="cf68d-123">Adding RealtimeBoard from hello gallery</span></span>
<span data-ttu-id="cf68d-124">integrazione hello tooconfigure di RealtimeBoard in Azure AD, è necessario tooadd RealtimeBoard dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="cf68d-124">tooconfigure hello integration of RealtimeBoard into Azure AD, you need tooadd RealtimeBoard from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cf68d-125">**tooadd RealtimeBoard dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cf68d-125">**tooadd RealtimeBoard from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf68d-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="cf68d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="cf68d-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="cf68d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cf68d-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cf68d-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="cf68d-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cf68d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="cf68d-133">Nella casella di ricerca hello, digitare **RealtimeBoard**selezionare **RealtimeBoard** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cf68d-133">In hello search box, type **RealtimeBoard**, select **RealtimeBoard** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello RealtimeBoard](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cf68d-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf68d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cf68d-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con RealtimeBoard usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cf68d-136">In this section, you configure and test Azure AD single sign-on with RealtimeBoard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cf68d-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in RealtimeBoard è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf68d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RealtimeBoard is tooa user in Azure AD.</span></span> <span data-ttu-id="cf68d-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in RealtimeBoard deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="cf68d-138">In other words, a link relationship between an Azure AD user and hello related user in RealtimeBoard needs toobe established.</span></span>

<span data-ttu-id="cf68d-139">In RealtimeBoard, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="cf68d-139">In RealtimeBoard, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cf68d-140">tooconfigure e prova AD Azure single sign-on con RealtimeBoard, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="cf68d-140">tooconfigure and test Azure AD single sign-on with RealtimeBoard, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cf68d-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cf68d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cf68d-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf68d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cf68d-143">**[Creare un utente test RealtimeBoard](#create-a-realtimeboard-test-user)**  -toohave un equivalente di Britta Simon in RealtimeBoard che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cf68d-143">**[Create a RealtimeBoard test user](#create-a-realtimeboard-test-user)** - toohave a counterpart of Britta Simon in RealtimeBoard that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cf68d-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cf68d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cf68d-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="cf68d-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cf68d-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf68d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cf68d-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="cf68d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RealtimeBoard application.</span></span>

<span data-ttu-id="cf68d-148">**Azure AD tooconfigure single sign-on con RealtimeBoard, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cf68d-148">**tooconfigure Azure AD single sign-on with RealtimeBoard, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf68d-149">Nel portale di Azure su hello hello **RealtimeBoard** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cf68d-149">In hello Azure portal, on hello **RealtimeBoard** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="cf68d-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cf68d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_samlbase.png)

3. <span data-ttu-id="cf68d-153">In hello **RealtimeBoard dominio e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="cf68d-153">On hello **RealtimeBoard Domain and URLs** section, if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di RealtimeBoard](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url.png)

    <span data-ttu-id="cf68d-155">In hello **identificatore** casella di testo, digitare un URL come:`https://realtimeboard.com/`</span><span class="sxs-lookup"><span data-stu-id="cf68d-155">In hello **Identifier** textbox, type a URL as: `https://realtimeboard.com/`</span></span>

4. <span data-ttu-id="cf68d-156">Controllare **Mostra URL impostazioni avanzate**, se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="cf68d-156">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url2.png)

    <span data-ttu-id="cf68d-158">In hello **Sign-on URL** casella di testo, digitare un URL come:`https://realtimeboard.com/sso/saml`</span><span class="sxs-lookup"><span data-stu-id="cf68d-158">In hello **Sign-on URL** textbox, type a URL as: `https://realtimeboard.com/sso/saml`</span></span>

5. <span data-ttu-id="cf68d-159">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="cf68d-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_certificate.png) 

6. <span data-ttu-id="cf68d-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="cf68d-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="cf68d-163">tooconfigure single sign-on sul **RealtimeBoard** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto RealtimeBoard](mailto:support@realtimeboard.com).</span><span class="sxs-lookup"><span data-stu-id="cf68d-163">tooconfigure single sign-on on **RealtimeBoard** side, you need toosend hello downloaded **Metadata XML** too[RealtimeBoard support team](mailto:support@realtimeboard.com).</span></span> <span data-ttu-id="cf68d-164">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="cf68d-164">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="cf68d-165">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="cf68d-165">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cf68d-166">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="cf68d-166">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cf68d-167">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cf68d-167">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cf68d-168">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf68d-168">Create an Azure AD test user</span></span>

<span data-ttu-id="cf68d-169">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="cf68d-169">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="cf68d-171">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cf68d-171">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf68d-172">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="cf68d-172">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="cf68d-174">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="cf68d-174">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="cf68d-176">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="cf68d-176">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="cf68d-178">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cf68d-178">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_04.png)

    <span data-ttu-id="cf68d-180">a.</span><span class="sxs-lookup"><span data-stu-id="cf68d-180">a.</span></span> <span data-ttu-id="cf68d-181">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cf68d-181">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cf68d-182">b.</span><span class="sxs-lookup"><span data-stu-id="cf68d-182">b.</span></span> <span data-ttu-id="cf68d-183">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf68d-183">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="cf68d-184">c.</span><span class="sxs-lookup"><span data-stu-id="cf68d-184">c.</span></span> <span data-ttu-id="cf68d-185">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="cf68d-185">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="cf68d-186">d.</span><span class="sxs-lookup"><span data-stu-id="cf68d-186">d.</span></span> <span data-ttu-id="cf68d-187">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="cf68d-187">Click **Create**.</span></span>
 
### <a name="create-a-realtimeboard-test-user"></a><span data-ttu-id="cf68d-188">Creare un utente di test di RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="cf68d-188">Create a RealtimeBoard test user</span></span>

<span data-ttu-id="cf68d-189">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in RealtimeBoard toocreate.</span><span class="sxs-lookup"><span data-stu-id="cf68d-189">hello objective of this section is toocreate a user called Britta Simon in RealtimeBoard.</span></span> <span data-ttu-id="cf68d-190">RealtimeBoard supporta il provisioning JIT, abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="cf68d-190">RealtimeBoard supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="cf68d-191">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="cf68d-191">There is no action item for you in this section.</span></span> <span data-ttu-id="cf68d-192">Se un utente non esiste già nel RealtimeBoard, quando si tenta di tooaccess RealtimeBoard uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="cf68d-192">If a user doesn't already exist in RealtimeBoard, a new one is created when you attempt tooaccess RealtimeBoard.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="cf68d-193">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf68d-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="cf68d-194">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooRealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="cf68d-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRealtimeBoard.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="cf68d-196">**tooassign Britta Simon tooRealtimeBoard, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="cf68d-196">**tooassign Britta Simon tooRealtimeBoard, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf68d-197">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="cf68d-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="cf68d-199">Nell'elenco di applicazioni hello, selezionare **RealtimeBoard**.</span><span class="sxs-lookup"><span data-stu-id="cf68d-199">In hello applications list, select **RealtimeBoard**.</span></span>

    ![collegamento RealtimeBoard Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_app.png)  

3. <span data-ttu-id="cf68d-201">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cf68d-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="cf68d-203">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cf68d-203">Click **Add** button.</span></span> <span data-ttu-id="cf68d-204">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cf68d-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="cf68d-206">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="cf68d-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cf68d-207">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="cf68d-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cf68d-208">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="cf68d-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cf68d-209">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="cf68d-209">Test single sign-on</span></span>

<span data-ttu-id="cf68d-210">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="cf68d-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cf68d-211">Quando si fa clic su riquadro RealtimeBoard hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour RealtimeBoard applicazione.</span><span class="sxs-lookup"><span data-stu-id="cf68d-211">When you click hello RealtimeBoard tile in hello Access Panel, you should get automatically signed-on tooyour RealtimeBoard application.</span></span>
<span data-ttu-id="cf68d-212">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cf68d-212">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cf68d-213">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cf68d-213">Additional resources</span></span>

* [<span data-ttu-id="cf68d-214">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf68d-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cf68d-215">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf68d-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_203.png

