---
title: 'Esercitazione: Integrazione di Azure Active Directory con Bime | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Bime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 1213725028dd8ce90f22fa6e9c50ffabebc8f3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="93293-103">Esercitazione: Integrazione di Azure Active Directory con Bime</span><span class="sxs-lookup"><span data-stu-id="93293-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="93293-104">In questa esercitazione, è illustrato come toointegrate Bime con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93293-104">In this tutorial, you learn how toointegrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93293-105">Integrazione Bime con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="93293-105">Integrating Bime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="93293-106">È possibile controllare in Azure AD che ha accesso tooBime</span><span class="sxs-lookup"><span data-stu-id="93293-106">You can control in Azure AD who has access tooBime</span></span>
- <span data-ttu-id="93293-107">È possibile abilitare l'utenti tooautomatically get connesso tooBime (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="93293-107">You can enable your users tooautomatically get signed-on tooBime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="93293-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="93293-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="93293-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="93293-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93293-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="93293-110">Prerequisites</span></span>

<span data-ttu-id="93293-111">integrazione di Azure AD con Bime tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="93293-111">tooconfigure Azure AD integration with Bime, you need hello following items:</span></span>

- <span data-ttu-id="93293-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93293-112">An Azure AD subscription</span></span>
- <span data-ttu-id="93293-113">Sottoscrizione di Bime abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="93293-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="93293-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="93293-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="93293-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="93293-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="93293-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="93293-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="93293-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="93293-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="93293-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="93293-118">Scenario description</span></span>
<span data-ttu-id="93293-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="93293-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="93293-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="93293-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93293-121">Aggiunta di Bime dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="93293-121">Adding Bime from hello gallery</span></span>
2. <span data-ttu-id="93293-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="93293-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-hello-gallery"></a><span data-ttu-id="93293-123">Aggiunta di Bime dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="93293-123">Adding Bime from hello gallery</span></span>
<span data-ttu-id="93293-124">integrazione hello tooconfigure di Bime in Azure AD, è necessario tooadd Bime dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="93293-124">tooconfigure hello integration of Bime into Azure AD, you need tooadd Bime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="93293-125">**tooadd Bime dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="93293-125">**tooadd Bime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="93293-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="93293-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="93293-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="93293-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="93293-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="93293-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="93293-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="93293-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="93293-133">Nella casella di ricerca hello, digitare **Bime**.</span><span class="sxs-lookup"><span data-stu-id="93293-133">In hello search box, type **Bime**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="93293-135">Nel riquadro dei risultati hello, selezionare **Bime**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="93293-135">In hello results panel, select **Bime**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="93293-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="93293-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="93293-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Bime in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="93293-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="93293-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Bime è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93293-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bime is tooa user in Azure AD.</span></span> <span data-ttu-id="93293-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Bime richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="93293-140">In other words, a link relationship between an Azure AD user and hello related user in Bime needs toobe established.</span></span>

<span data-ttu-id="93293-141">In Bime, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="93293-141">In Bime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="93293-142">tooconfigure e test Azure single sign-on AD con Bime, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="93293-142">tooconfigure and test Azure AD single sign-on with Bime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="93293-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="93293-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="93293-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93293-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="93293-145">**[Creazione di un utente test Bime](#creating-a-bime-test-user)**  -toohave un equivalente di Britta Simon in Bime che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="93293-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - toohave a counterpart of Britta Simon in Bime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="93293-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="93293-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="93293-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="93293-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="93293-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="93293-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="93293-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Bime.</span><span class="sxs-lookup"><span data-stu-id="93293-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="93293-150">**Azure AD tooconfigure single sign-on con Bime, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="93293-150">**tooconfigure Azure AD single sign-on with Bime, perform hello following steps:**</span></span>

1. <span data-ttu-id="93293-151">Nel portale di Azure su hello hello **Bime** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="93293-151">In hello Azure portal, on hello **Bime** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="93293-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="93293-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="93293-155">In hello **Bime dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="93293-155">On hello **Bime Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="93293-157">a.</span><span class="sxs-lookup"><span data-stu-id="93293-157">a.</span></span> <span data-ttu-id="93293-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="93293-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="93293-159">b.</span><span class="sxs-lookup"><span data-stu-id="93293-159">b.</span></span> <span data-ttu-id="93293-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="93293-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="93293-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="93293-161">These values are not real.</span></span> <span data-ttu-id="93293-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="93293-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="93293-163">Contatto [team di supporto Bime Client](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="93293-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget these values.</span></span> 
 
4. <span data-ttu-id="93293-164">In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore dal certificato hello.</span><span class="sxs-lookup"><span data-stu-id="93293-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="93293-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="93293-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="93293-168">In hello **Bime configurazione** fare clic su **configurare Bime** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="93293-168">On hello **Bime Configuration** section, click **Configure Bime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="93293-169">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="93293-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="93293-171">In un'altra finestra del Web browser accedere al sito aziendale di Bime come amministratore.</span><span class="sxs-lookup"><span data-stu-id="93293-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="93293-172">Nella barra degli strumenti hello, fare clic su **Admin**e quindi **Account**.</span><span class="sxs-lookup"><span data-stu-id="93293-172">In hello toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="93293-173">![Amministratore](./media/active-directory-saas-bime-tutorial/ic775558.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="93293-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="93293-174">Nella pagina di configurazione di account hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="93293-174">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="93293-175">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configurare l'accesso Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="93293-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="93293-176">a.</span><span class="sxs-lookup"><span data-stu-id="93293-176">a.</span></span> <span data-ttu-id="93293-177">Selezionare **Enable SAML authentication**.</span><span class="sxs-lookup"><span data-stu-id="93293-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="93293-178">b.</span><span class="sxs-lookup"><span data-stu-id="93293-178">b.</span></span> <span data-ttu-id="93293-179">In hello **URL accesso remoto** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="93293-179">In hello **Remote Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="93293-180">c.</span><span class="sxs-lookup"><span data-stu-id="93293-180">c.</span></span>  <span data-ttu-id="93293-181">Hello Incolla **identificazione personale** valore dal portale di Azure in hello **Certificate Fingerprint** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="93293-181">Paste hello **Thumbprint** value from Azure portal into hello **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="93293-182">d.</span><span class="sxs-lookup"><span data-stu-id="93293-182">d.</span></span> <span data-ttu-id="93293-183">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="93293-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="93293-184">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="93293-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="93293-185">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="93293-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="93293-186">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="93293-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="93293-187">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="93293-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="93293-188">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="93293-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="93293-190">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="93293-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="93293-191">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="93293-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="93293-193">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="93293-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="93293-195">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="93293-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="93293-197">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="93293-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="93293-199">a.</span><span class="sxs-lookup"><span data-stu-id="93293-199">a.</span></span> <span data-ttu-id="93293-200">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="93293-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="93293-201">b.</span><span class="sxs-lookup"><span data-stu-id="93293-201">b.</span></span> <span data-ttu-id="93293-202">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="93293-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="93293-203">c.</span><span class="sxs-lookup"><span data-stu-id="93293-203">c.</span></span> <span data-ttu-id="93293-204">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="93293-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="93293-205">d.</span><span class="sxs-lookup"><span data-stu-id="93293-205">d.</span></span> <span data-ttu-id="93293-206">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="93293-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="93293-207">Creazione di un utente test di Bime</span><span class="sxs-lookup"><span data-stu-id="93293-207">Creating a Bime test user</span></span>

<span data-ttu-id="93293-208">In ordine tooenable Azure AD utenti toolog in tooBime, è necessario eseguirne il provisioning in Bime.</span><span class="sxs-lookup"><span data-stu-id="93293-208">In order tooenable Azure AD users toolog in tooBime, they must be provisioned into Bime.</span></span> <span data-ttu-id="93293-209">Nel caso di hello di Bime, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="93293-209">In hello case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="93293-210">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="93293-210">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="93293-211">Accedi tooyour **Bime** tenant.</span><span class="sxs-lookup"><span data-stu-id="93293-211">Log in tooyour **Bime** tenant.</span></span>

2. <span data-ttu-id="93293-212">Nella barra degli strumenti hello, fare clic su **Admin**e quindi **utenti**.</span><span class="sxs-lookup"><span data-stu-id="93293-212">In hello toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="93293-213">![Amministratore](./media/active-directory-saas-bime-tutorial/ic775561.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="93293-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="93293-214">In hello **elenco utenti**, fare clic su **Add New User** ("+").</span><span class="sxs-lookup"><span data-stu-id="93293-214">In hello **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="93293-215">![Utenti](./media/active-directory-saas-bime-tutorial/ic775562.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="93293-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="93293-216">In hello **dettagli utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="93293-216">On hello **User Details** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="93293-217">![Dettagli utente](./media/active-directory-saas-bime-tutorial/ic775563.png "Dettagli utente")</span><span class="sxs-lookup"><span data-stu-id="93293-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="93293-218">a.</span><span class="sxs-lookup"><span data-stu-id="93293-218">a.</span></span> <span data-ttu-id="93293-219">In hello **nome** casella di testo, immettere nome hello dell'utente come **Laura**.</span><span class="sxs-lookup"><span data-stu-id="93293-219">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="93293-220">b.</span><span class="sxs-lookup"><span data-stu-id="93293-220">b.</span></span> <span data-ttu-id="93293-221">In hello **cognome** casella di testo immettere hello cognome dell'utente come **Simon**.</span><span class="sxs-lookup"><span data-stu-id="93293-221">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="93293-222">c.</span><span class="sxs-lookup"><span data-stu-id="93293-222">c.</span></span> <span data-ttu-id="93293-223">In hello **posta elettronica** casella di testo immettere hello email dell'utente come  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="93293-223">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="93293-224">d.</span><span class="sxs-lookup"><span data-stu-id="93293-224">d.</span></span> <span data-ttu-id="93293-225">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="93293-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="93293-226">È possibile usare qualsiasi altro Bime utente account strumento di creazione o le API fornite da Bime tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="93293-226">You can use any other Bime user account creation tools or APIs provided by Bime tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="93293-227">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="93293-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="93293-228">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBime.</span><span class="sxs-lookup"><span data-stu-id="93293-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBime.</span></span>

![Assegna utente][200] 

<span data-ttu-id="93293-230">**tooassign Britta Simon tooBime, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="93293-230">**tooassign Britta Simon tooBime, perform hello following steps:**</span></span>

1. <span data-ttu-id="93293-231">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="93293-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="93293-233">Nell'elenco di applicazioni hello, selezionare **Bime**.</span><span class="sxs-lookup"><span data-stu-id="93293-233">In hello applications list, select **Bime**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="93293-235">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="93293-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="93293-237">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="93293-237">Click **Add** button.</span></span> <span data-ttu-id="93293-238">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="93293-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="93293-240">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="93293-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="93293-241">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="93293-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="93293-242">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="93293-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="93293-243">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="93293-243">Testing single sign-on</span></span>

<span data-ttu-id="93293-244">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="93293-244">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="93293-245">Quando si fa clic su riquadro Bime hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in Bime applicazione.</span><span class="sxs-lookup"><span data-stu-id="93293-245">When you click hello Bime tile in hello Access Panel, you should get automatically signed-on tooyour Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="93293-246">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="93293-246">Additional resources</span></span>

* [<span data-ttu-id="93293-247">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93293-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93293-248">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93293-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

