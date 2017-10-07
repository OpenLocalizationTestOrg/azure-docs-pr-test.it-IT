---
title: 'Esercitazione: Integrazione di Azure Active Directory con SmarterU | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SmarterU.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 95fe3212-d052-4ac8-87eb-ac5305227e85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: a3b81b557c47e31f09e61bcf75dd23f370e642e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-smarteru"></a><span data-ttu-id="a61bf-103">Esercitazione: Integrazione di Azure Active Directory con SmarterU</span><span class="sxs-lookup"><span data-stu-id="a61bf-103">Tutorial: Azure Active Directory integration with SmarterU</span></span>

<span data-ttu-id="a61bf-104">In questa esercitazione, è illustrato come toointegrate SmarterU con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a61bf-104">In this tutorial, you learn how toointegrate SmarterU with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a61bf-105">Integrazione SmarterU con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="a61bf-105">Integrating SmarterU with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a61bf-106">È possibile controllare in Azure AD che ha accesso tooSmarterU</span><span class="sxs-lookup"><span data-stu-id="a61bf-106">You can control in Azure AD who has access tooSmarterU</span></span>
- <span data-ttu-id="a61bf-107">È possibile abilitare l'utenti tooautomatically get connesso tooSmarterU (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="a61bf-107">You can enable your users tooautomatically get signed-on tooSmarterU (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a61bf-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a61bf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a61bf-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a61bf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a61bf-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a61bf-110">Prerequisites</span></span>

<span data-ttu-id="a61bf-111">integrazione di Azure AD con SmarterU tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="a61bf-111">tooconfigure Azure AD integration with SmarterU, you need hello following items:</span></span>

- <span data-ttu-id="a61bf-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a61bf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a61bf-113">Sottoscrizione di SmarterU abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a61bf-113">A SmarterU single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a61bf-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="a61bf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a61bf-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="a61bf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a61bf-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="a61bf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a61bf-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a61bf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a61bf-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="a61bf-118">Scenario description</span></span>
<span data-ttu-id="a61bf-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="a61bf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a61bf-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="a61bf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a61bf-121">Aggiunta di SmarterU dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="a61bf-121">Adding SmarterU from hello gallery</span></span>
2. <span data-ttu-id="a61bf-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a61bf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-smarteru-from-hello-gallery"></a><span data-ttu-id="a61bf-123">Aggiunta di SmarterU dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="a61bf-123">Adding SmarterU from hello gallery</span></span>
<span data-ttu-id="a61bf-124">integrazione hello tooconfigure di SmarterU in Azure AD, è necessario tooadd SmarterU dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="a61bf-124">tooconfigure hello integration of SmarterU into Azure AD, you need tooadd SmarterU from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a61bf-125">**tooadd SmarterU dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a61bf-125">**tooadd SmarterU from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a61bf-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="a61bf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a61bf-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a61bf-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="a61bf-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="a61bf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="a61bf-133">Nella casella di ricerca hello, digitare **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-133">In hello search box, type **SmarterU**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_search.png)

5. <span data-ttu-id="a61bf-135">Nel riquadro dei risultati hello, selezionare **SmarterU**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="a61bf-135">In hello results panel, select **SmarterU**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a61bf-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a61bf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a61bf-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SmarterU usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a61bf-138">In this section, you configure and test Azure AD single sign-on with SmarterU based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a61bf-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in SmarterU è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a61bf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SmarterU is tooa user in Azure AD.</span></span> <span data-ttu-id="a61bf-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in SmarterU deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="a61bf-140">In other words, a link relationship between an Azure AD user and hello related user in SmarterU needs toobe established.</span></span>

<span data-ttu-id="a61bf-141">In SmarterU, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="a61bf-141">In SmarterU, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a61bf-142">tooconfigure e test Azure single sign-on AD con SmarterU, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="a61bf-142">tooconfigure and test Azure AD single sign-on with SmarterU, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a61bf-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a61bf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a61bf-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a61bf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a61bf-145">**[Creazione di un utente test SmarterU](#creating-a-smarteru-test-user)**  -toohave un equivalente di Britta Simon in SmarterU che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="a61bf-145">**[Creating a SmarterU test user](#creating-a-smarteru-test-user)** - toohave a counterpart of Britta Simon in SmarterU that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a61bf-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a61bf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a61bf-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="a61bf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a61bf-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a61bf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a61bf-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione SmarterU.</span><span class="sxs-lookup"><span data-stu-id="a61bf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SmarterU application.</span></span>

<span data-ttu-id="a61bf-150">**Azure AD tooconfigure single sign-on con SmarterU, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a61bf-150">**tooconfigure Azure AD single sign-on with SmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="a61bf-151">Nel portale di Azure su hello hello **SmarterU** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-151">In hello Azure portal, on hello **SmarterU** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="a61bf-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a61bf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_samlbase.png)

3. <span data-ttu-id="a61bf-155">In hello **SmarterU dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a61bf-155">On hello **SmarterU Domain and URLs** section, perform hello following steps:</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_url.png)

    <span data-ttu-id="a61bf-157">In hello **identificatore** casella di testo, digitare l'URL hello:`https://www.smarteru.com/`</span><span class="sxs-lookup"><span data-stu-id="a61bf-157">In hello **Identifier** textbox, type hello URL: `https://www.smarteru.com/`</span></span>

4. <span data-ttu-id="a61bf-158">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="a61bf-158">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_certificate.png) 

5. <span data-ttu-id="a61bf-160">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="a61bf-160">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-smarteru-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a61bf-162">In una finestra del web browser, accedere come amministratore nel sito della società SmarterU di tooyour.</span><span class="sxs-lookup"><span data-stu-id="a61bf-162">In a different web browser window, log in tooyour SmarterU company site as an administrator.</span></span>

7. <span data-ttu-id="a61bf-163">Nella barra degli strumenti hello in primo piano hello, fare clic su **impostazioni Account**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-163">In hello toolbar on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="a61bf-164">![Impostazioni account](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Impostazioni account")</span><span class="sxs-lookup"><span data-stu-id="a61bf-164">![Account Settings](./media/active-directory-saas-smarteru-tutorial/IC777326.png "Account Settings")</span></span>

8. <span data-ttu-id="a61bf-165">Nella pagina di configurazione di account hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a61bf-165">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="a61bf-166">![Autorizzazione esterna](./media/active-directory-saas-smarteru-tutorial/IC777327.png "Autorizzazione esterna")</span><span class="sxs-lookup"><span data-stu-id="a61bf-166">![External Authorization](./media/active-directory-saas-smarteru-tutorial/IC777327.png "External Authorization")</span></span> 
 
      <span data-ttu-id="a61bf-167">a.</span><span class="sxs-lookup"><span data-stu-id="a61bf-167">a.</span></span> <span data-ttu-id="a61bf-168">Selezionare **Attiva autorizzazione esterna**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-168">Select **Enable External Authorization**.</span></span>
  
      <span data-ttu-id="a61bf-169">b.</span><span class="sxs-lookup"><span data-stu-id="a61bf-169">b.</span></span> <span data-ttu-id="a61bf-170">In hello **Master Login Control** sezione, seleziona hello **SmarterU** scheda.</span><span class="sxs-lookup"><span data-stu-id="a61bf-170">In hello **Master Login Control** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="a61bf-171">c.</span><span class="sxs-lookup"><span data-stu-id="a61bf-171">c.</span></span> <span data-ttu-id="a61bf-172">In hello **User Default Login** sezione, seleziona hello **SmarterU** scheda.</span><span class="sxs-lookup"><span data-stu-id="a61bf-172">In hello **User Default Login** section, select hello **SmarterU** tab.</span></span>
  
      <span data-ttu-id="a61bf-173">d.</span><span class="sxs-lookup"><span data-stu-id="a61bf-173">d.</span></span> <span data-ttu-id="a61bf-174">Selezionare **Attiva Okta**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-174">Select **Enable Okta**.</span></span>
  
      <span data-ttu-id="a61bf-175">e.</span><span class="sxs-lookup"><span data-stu-id="a61bf-175">e.</span></span> <span data-ttu-id="a61bf-176">Copiare il contenuto di hello del file di metadati scaricato hello e quindi incollarlo hello **Okta Metadata** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="a61bf-176">Copy hello content of hello downloaded metadata file, and then paste it into hello **Okta Metadata** textbox.</span></span>
  
      <span data-ttu-id="a61bf-177">f.</span><span class="sxs-lookup"><span data-stu-id="a61bf-177">f.</span></span> <span data-ttu-id="a61bf-178">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-178">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a61bf-179">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="a61bf-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a61bf-180">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="a61bf-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a61bf-181">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a61bf-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a61bf-182">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="a61bf-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="a61bf-183">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="a61bf-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="a61bf-185">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a61bf-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a61bf-186">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="a61bf-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a61bf-188">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a61bf-190">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="a61bf-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a61bf-192">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a61bf-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-smarteru-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a61bf-194">a.</span><span class="sxs-lookup"><span data-stu-id="a61bf-194">a.</span></span> <span data-ttu-id="a61bf-195">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a61bf-196">b.</span><span class="sxs-lookup"><span data-stu-id="a61bf-196">b.</span></span> <span data-ttu-id="a61bf-197">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a61bf-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a61bf-198">c.</span><span class="sxs-lookup"><span data-stu-id="a61bf-198">c.</span></span> <span data-ttu-id="a61bf-199">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a61bf-200">d.</span><span class="sxs-lookup"><span data-stu-id="a61bf-200">d.</span></span> <span data-ttu-id="a61bf-201">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-201">Click **Create**.</span></span>
 
### <a name="creating-a-smarteru-test-user"></a><span data-ttu-id="a61bf-202">Creazione di un utente di test di SmarterU</span><span class="sxs-lookup"><span data-stu-id="a61bf-202">Creating a SmarterU test user</span></span>

<span data-ttu-id="a61bf-203">toolog agli utenti di Azure AD tooenable in tooSmarterU, è necessario eseguirne il provisioning in SmarterU.</span><span class="sxs-lookup"><span data-stu-id="a61bf-203">tooenable Azure AD users toolog in tooSmarterU, they must be provisioned into SmarterU.</span></span>

<span data-ttu-id="a61bf-204">Nel caso di SmarterU, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="a61bf-204">When SmarterU, provisioning is a manual task.</span></span>

<span data-ttu-id="a61bf-205">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a61bf-205">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a61bf-206">Accedi tooyour **SmarterU** tenant.</span><span class="sxs-lookup"><span data-stu-id="a61bf-206">Log in tooyour **SmarterU** tenant.</span></span>

2. <span data-ttu-id="a61bf-207">Andare troppo**utenti**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-207">Go too**Users**.</span></span>

3. <span data-ttu-id="a61bf-208">Nella sezione utente hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="a61bf-208">In hello user section, perform hello following steps:</span></span>
   
    <span data-ttu-id="a61bf-209">![Nuovo utente](./media/active-directory-saas-smarteru-tutorial/IC777329.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="a61bf-209">![New User](./media/active-directory-saas-smarteru-tutorial/IC777329.png "New User")</span></span>  

    <span data-ttu-id="a61bf-210">a.</span><span class="sxs-lookup"><span data-stu-id="a61bf-210">a.</span></span> <span data-ttu-id="a61bf-211">Fare clic su **+Utente**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-211">Click **+User**.</span></span>
    
    <span data-ttu-id="a61bf-212">b.</span><span class="sxs-lookup"><span data-stu-id="a61bf-212">b.</span></span> <span data-ttu-id="a61bf-213">Hello tipo relativi valori di attributo dell'account utente di hello Azure AD in hello seguenti caselle di testo: **posta elettronica primario**, **ID dipendente**, **Password**,  **Verificare la Password**, **nome**, **Surname**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-213">Type hello related attribute values of hello Azure AD user account into hello following textboxes: **Primary Email**, **Employee ID**, **Password**, **Verify Password**, **Given Name**, **Surname**.</span></span>
    
    <span data-ttu-id="a61bf-214">c.</span><span class="sxs-lookup"><span data-stu-id="a61bf-214">c.</span></span> <span data-ttu-id="a61bf-215">Fare clic su **Attivo**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-215">Click **Active**.</span></span> 
    
    <span data-ttu-id="a61bf-216">d.</span><span class="sxs-lookup"><span data-stu-id="a61bf-216">d.</span></span> <span data-ttu-id="a61bf-217">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-217">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="a61bf-218">È possibile usare qualsiasi altro SmarterU utente account strumento di creazione o le API fornite da SmarterU tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="a61bf-218">You can use any other SmarterU user account creation tools or APIs provided by SmarterU tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a61bf-219">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a61bf-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a61bf-220">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSmarterU.</span><span class="sxs-lookup"><span data-stu-id="a61bf-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmarterU.</span></span>

![Assegna utente][200] 

<span data-ttu-id="a61bf-222">**tooassign Britta Simon tooSmarterU, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="a61bf-222">**tooassign Britta Simon tooSmarterU, perform hello following steps:**</span></span>

1. <span data-ttu-id="a61bf-223">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="a61bf-225">Nell'elenco di applicazioni hello, selezionare **SmarterU**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-225">In hello applications list, select **SmarterU**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-smarteru-tutorial/tutorial_smarteru_app.png) 

3. <span data-ttu-id="a61bf-227">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="a61bf-229">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-229">Click **Add** button.</span></span> <span data-ttu-id="a61bf-230">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="a61bf-232">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="a61bf-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a61bf-233">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a61bf-234">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="a61bf-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a61bf-235">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a61bf-235">Testing single sign-on</span></span>

<span data-ttu-id="a61bf-236">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="a61bf-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="a61bf-237">Quando si fa clic su riquadro SmarterU hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in SmarterU applicazione.</span><span class="sxs-lookup"><span data-stu-id="a61bf-237">When you click hello SmarterU tile in hello Access Panel, you should get automatically signed-on tooyour SmarterU application.</span></span>
<span data-ttu-id="a61bf-238">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a61bf-238">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 


## <a name="additional-resources"></a><span data-ttu-id="a61bf-239">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="a61bf-239">Additional resources</span></span>

* [<span data-ttu-id="a61bf-240">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a61bf-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a61bf-241">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a61bf-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smarteru-tutorial/tutorial_general_203.png

