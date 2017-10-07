---
title: 'Esercitazione: Integrazione di Azure Active Directory con Direct | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e diretto.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ac663070b39e55eade2c43814b63a9d0374c7316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="15962-103">Esercitazione: Integrazione di Azure Active Directory con Direct</span><span class="sxs-lookup"><span data-stu-id="15962-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="15962-104">In questa esercitazione, è illustrato come toointegrate diretta con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="15962-104">In this tutorial, you learn how toointegrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="15962-105">Integrazione diretta con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="15962-105">Integrating Direct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="15962-106">È possibile controllare in Azure AD che ha accesso tooDirect</span><span class="sxs-lookup"><span data-stu-id="15962-106">You can control in Azure AD who has access tooDirect</span></span>
- <span data-ttu-id="15962-107">È possibile abilitare l'utenti tooautomatically get connesso tooDirect (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="15962-107">You can enable your users tooautomatically get signed-on tooDirect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="15962-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="15962-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="15962-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="15962-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15962-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="15962-110">Prerequisites</span></span>

<span data-ttu-id="15962-111">integrazione di Azure AD tooconfigure con Direct, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="15962-111">tooconfigure Azure AD integration with Direct, you need hello following items:</span></span>

- <span data-ttu-id="15962-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15962-112">An Azure AD subscription</span></span>
- <span data-ttu-id="15962-113">Sottoscrizione di Direct abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="15962-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="15962-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="15962-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="15962-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="15962-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="15962-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="15962-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="15962-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="15962-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="15962-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="15962-118">Scenario description</span></span>
<span data-ttu-id="15962-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="15962-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="15962-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="15962-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="15962-121">Aggiunta diretta dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="15962-121">Adding Direct from hello gallery</span></span>
2. <span data-ttu-id="15962-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="15962-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-hello-gallery"></a><span data-ttu-id="15962-123">Aggiunta diretta dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="15962-123">Adding Direct from hello gallery</span></span>
<span data-ttu-id="15962-124">integrazione hello tooconfigure di diretto in Azure AD, è necessario tooadd direttamente dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="15962-124">tooconfigure hello integration of Direct into Azure AD, you need tooadd Direct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="15962-125">**tooadd direttamente dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="15962-125">**tooadd Direct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="15962-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="15962-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="15962-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="15962-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="15962-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="15962-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="15962-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="15962-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="15962-133">Nella casella di ricerca hello, digitare **diretto**.</span><span class="sxs-lookup"><span data-stu-id="15962-133">In hello search box, type **Direct**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="15962-135">Nel riquadro dei risultati hello, selezionare **diretto**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="15962-135">In hello results panel, select **Direct**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="15962-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="15962-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="15962-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Direct mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="15962-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="15962-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in diretta è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15962-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Direct is tooa user in Azure AD.</span></span> <span data-ttu-id="15962-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in diretta esigenze toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="15962-140">In other words, a link relationship between an Azure AD user and hello related user in Direct needs toobe established.</span></span>

<span data-ttu-id="15962-141">In diretta, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="15962-141">In Direct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="15962-142">tooconfigure e test di Azure AD accesso single sign-on con Direct, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="15962-142">tooconfigure and test Azure AD single sign-on with Direct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="15962-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="15962-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="15962-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="15962-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="15962-145">**[Creazione di un utente test diretto](#creating-a-direct-test-user)**  -toohave un equivalente di Britta Simon in diretta che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="15962-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - toohave a counterpart of Britta Simon in Direct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="15962-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="15962-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="15962-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="15962-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="15962-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="15962-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="15962-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione diretta.</span><span class="sxs-lookup"><span data-stu-id="15962-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="15962-150">**tooconfigure AD Azure single sign-on con Direct, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="15962-150">**tooconfigure Azure AD single sign-on with Direct, perform hello following steps:**</span></span>

1. <span data-ttu-id="15962-151">Nel portale di Azure su hello hello **diretto** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="15962-151">In hello Azure portal, on hello **Direct** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="15962-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="15962-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="15962-155">In hello **dominio diretto e gli URL** sezione, se si desidera in un'applicazione hello tooconfigure **IDP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="15962-155">On hello **Direct Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="15962-157">In hello **identificatore** casella di testo, digitare l'URL hello:`https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="15962-157">In hello **Identifier** textbox, type hello URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="15962-158">Controllare **Mostra URL impostazioni avanzate**, se si desidera in un'applicazione hello tooconfigure **SP** modalità iniziata da:</span><span class="sxs-lookup"><span data-stu-id="15962-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="15962-160">In hello **Sign-on URL** casella di testo, digitare l'URL hello:`https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="15962-160">In hello **Sign-on URL** textbox, type hello URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="15962-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="15962-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="15962-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="15962-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="15962-165">tooconfigure single sign-on sul **diretto** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto diretto](https://direct4b.com/ja/support.html#inquiry).</span><span class="sxs-lookup"><span data-stu-id="15962-165">tooconfigure single sign-on on **Direct** side, you need toosend hello downloaded **Metadata XML** too[Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="15962-166">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="15962-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="15962-167">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="15962-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="15962-168">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="15962-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="15962-169">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="15962-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="15962-170">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="15962-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="15962-172">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="15962-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="15962-173">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="15962-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="15962-175">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="15962-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="15962-177">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="15962-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="15962-179">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="15962-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="15962-181">a.</span><span class="sxs-lookup"><span data-stu-id="15962-181">a.</span></span> <span data-ttu-id="15962-182">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="15962-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="15962-183">b.</span><span class="sxs-lookup"><span data-stu-id="15962-183">b.</span></span> <span data-ttu-id="15962-184">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="15962-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="15962-185">c.</span><span class="sxs-lookup"><span data-stu-id="15962-185">c.</span></span> <span data-ttu-id="15962-186">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="15962-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="15962-187">d.</span><span class="sxs-lookup"><span data-stu-id="15962-187">d.</span></span> <span data-ttu-id="15962-188">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="15962-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="15962-189">Creazione di un utente test di Direct</span><span class="sxs-lookup"><span data-stu-id="15962-189">Creating a Direct test user</span></span>

<span data-ttu-id="15962-190">In questa sezione si crea un utente con nome Britta Simon in Direct.</span><span class="sxs-lookup"><span data-stu-id="15962-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="15962-191">Lavorare con [team di supporto diretto](https://direct4b.com/ja/support.html#inquiry) per aggiungere gli utenti di hello nella piattaforma diretto hello.</span><span class="sxs-lookup"><span data-stu-id="15962-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add hello users in hello Direct platform.</span></span> <span data-ttu-id="15962-192">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="15962-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="15962-193">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="15962-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="15962-194">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooDirect.</span><span class="sxs-lookup"><span data-stu-id="15962-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDirect.</span></span>

![Assegna utente][200] 

<span data-ttu-id="15962-196">**tooassign Britta Simon tooDirect, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="15962-196">**tooassign Britta Simon tooDirect, perform hello following steps:**</span></span>

1. <span data-ttu-id="15962-197">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="15962-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="15962-199">Nell'elenco di applicazioni hello, selezionare **diretto**.</span><span class="sxs-lookup"><span data-stu-id="15962-199">In hello applications list, select **Direct**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="15962-201">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="15962-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="15962-203">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="15962-203">Click **Add** button.</span></span> <span data-ttu-id="15962-204">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="15962-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="15962-206">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="15962-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="15962-207">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="15962-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="15962-208">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="15962-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="15962-209">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="15962-209">Testing single sign-on</span></span>

<span data-ttu-id="15962-210">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="15962-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="15962-211">Se si desidera tootest in **modalità avviato dal provider di identità**:</span><span class="sxs-lookup"><span data-stu-id="15962-211">If you wish tootest in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="15962-212">Quando si fa clic su hello **diretto** hello di riquadro nel Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour **diretto** dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="15962-212">When you click hello **Direct** tile in hello Access Panel, you should get automatically signed-on tooyour **Direct** application.</span></span>

2. <span data-ttu-id="15962-213">Se si desidera tootest in **modalità avviata SP**:</span><span class="sxs-lookup"><span data-stu-id="15962-213">If you wish tootest in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="15962-214">a.</span><span class="sxs-lookup"><span data-stu-id="15962-214">a.</span></span> <span data-ttu-id="15962-215">Fare clic su hello **diretto** riquadro nel Pannello di accesso hello e sarà reindirizzato toohello sign-on pagina dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="15962-215">Click on hello **Direct** tile in hello Access Panel and you will be redirected toohello application sign-on page.</span></span>

    <span data-ttu-id="15962-216">b.</span><span class="sxs-lookup"><span data-stu-id="15962-216">b.</span></span> <span data-ttu-id="15962-217">Input del `subdomain` nella casella di testo hello visualizzata e premere '次へ (Avanti)' e si deve ottenere automaticamente firmato in tooyour **diretto** applicazione.</span><span class="sxs-lookup"><span data-stu-id="15962-217">Input your `subdomain` in hello textbox displayed and press '次へ (Next)' and you should get automatically signed-on tooyour **Direct** application .</span></span>
    
<span data-ttu-id="15962-218">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="15962-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="15962-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="15962-219">Additional resources</span></span>

* [<span data-ttu-id="15962-220">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15962-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="15962-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15962-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

