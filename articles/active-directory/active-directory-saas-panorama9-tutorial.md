---
title: 'Esercitazione: Integrazione di Azure Active Directory con Panorama9 | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Panorama9.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 548fb6434d920e076db98a0193f8dfdf8a958a91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="501a2-103">Esercitazione: Integrazione di Azure Active Directory con Panorama9</span><span class="sxs-lookup"><span data-stu-id="501a2-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="501a2-104">In questa esercitazione, è illustrato come toointegrate Panorama9 con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="501a2-104">In this tutorial, you learn how toointegrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="501a2-105">Integrazione di Panorama9 con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="501a2-105">Integrating Panorama9 with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="501a2-106">È possibile controllare in Azure AD che ha accesso tooPanorama9</span><span class="sxs-lookup"><span data-stu-id="501a2-106">You can control in Azure AD who has access tooPanorama9</span></span>
- <span data-ttu-id="501a2-107">È possibile abilitare il get tooautomatically utenti connesso tooPanorama9 (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="501a2-107">You can enable your users tooautomatically get signed-on tooPanorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="501a2-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="501a2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="501a2-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="501a2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="501a2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="501a2-110">Prerequisites</span></span>

<span data-ttu-id="501a2-111">integrazione di Azure AD con Panorama9 tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="501a2-111">tooconfigure Azure AD integration with Panorama9, you need hello following items:</span></span>

- <span data-ttu-id="501a2-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="501a2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="501a2-113">Sottoscrizione di Panorama9 abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="501a2-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="501a2-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="501a2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="501a2-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="501a2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="501a2-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="501a2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="501a2-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="501a2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="501a2-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="501a2-118">Scenario description</span></span>
<span data-ttu-id="501a2-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="501a2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="501a2-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="501a2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="501a2-121">Aggiunta di Panorama9 dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="501a2-121">Adding Panorama9 from hello gallery</span></span>
2. <span data-ttu-id="501a2-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="501a2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-hello-gallery"></a><span data-ttu-id="501a2-123">Aggiunta di Panorama9 dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="501a2-123">Adding Panorama9 from hello gallery</span></span>
<span data-ttu-id="501a2-124">integrazione hello tooconfigure di Panorama9 in Azure AD, è necessario tooadd Panorama9 dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="501a2-124">tooconfigure hello integration of Panorama9 into Azure AD, you need tooadd Panorama9 from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="501a2-125">**tooadd Panorama9 dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="501a2-125">**tooadd Panorama9 from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="501a2-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="501a2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="501a2-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="501a2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="501a2-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="501a2-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="501a2-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="501a2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="501a2-133">Nella casella di ricerca hello, digitare **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="501a2-133">In hello search box, type **Panorama9**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="501a2-135">Nel riquadro dei risultati hello, selezionare **Panorama9**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="501a2-135">In hello results panel, select **Panorama9**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="501a2-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="501a2-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="501a2-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Panorama9 con un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="501a2-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="501a2-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Panorama9 è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="501a2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panorama9 is tooa user in Azure AD.</span></span> <span data-ttu-id="501a2-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Panorama9 richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="501a2-140">In other words, a link relationship between an Azure AD user and hello related user in Panorama9 needs toobe established.</span></span>

<span data-ttu-id="501a2-141">In Panorama9, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="501a2-141">In Panorama9, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="501a2-142">tooconfigure e prova AD Azure single sign-on con Panorama9, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="501a2-142">tooconfigure and test Azure AD single sign-on with Panorama9, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="501a2-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="501a2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="501a2-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="501a2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="501a2-145">**[Creazione di un utente test Panorama9](#creating-a-panorama9-test-user)**  -toohave un equivalente di Britta Simon in Panorama9 che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="501a2-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - toohave a counterpart of Britta Simon in Panorama9 that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="501a2-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="501a2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="501a2-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="501a2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="501a2-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="501a2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="501a2-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Panorama9.</span><span class="sxs-lookup"><span data-stu-id="501a2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="501a2-150">**Azure AD tooconfigure single sign-on con Panorama9, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="501a2-150">**tooconfigure Azure AD single sign-on with Panorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="501a2-151">Nel portale di Azure su hello hello **Panorama9** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="501a2-151">In hello Azure portal, on hello **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="501a2-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="501a2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="501a2-155">In hello **Panorama9 dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="501a2-155">On hello **Panorama9 Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="501a2-157">a.</span><span class="sxs-lookup"><span data-stu-id="501a2-157">a.</span></span> <span data-ttu-id="501a2-158">In hello **Sign-on URL** casella di testo, digitare un URL come:`https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="501a2-158">In hello **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="501a2-159">b.</span><span class="sxs-lookup"><span data-stu-id="501a2-159">b.</span></span> <span data-ttu-id="501a2-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="501a2-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="501a2-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="501a2-161">These values are not real.</span></span> <span data-ttu-id="501a2-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="501a2-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="501a2-163">Contatto [team di supporto Client di Panorama9](https://support.panorama9.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="501a2-163">Contact [Panorama9 Client support team](https://support.panorama9.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="501a2-164">In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore del certificato.</span><span class="sxs-lookup"><span data-stu-id="501a2-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="501a2-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="501a2-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="501a2-168">In hello **Panorama9 configurazione** fare clic su **configurare Panorama9** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="501a2-168">On hello **Panorama9 Configuration** section, click **Configure Panorama9** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="501a2-169">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="501a2-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="501a2-171">In un'altra finestra del Web browser accedere al sito aziendale di Panorama9 come amministratore.</span><span class="sxs-lookup"><span data-stu-id="501a2-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="501a2-172">Nella barra degli strumenti hello in primo piano hello, fare clic su **Gestisci**, quindi fare clic su **estensioni**.</span><span class="sxs-lookup"><span data-stu-id="501a2-172">In hello toolbar on hello top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="501a2-173">![Estensioni](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Estensioni")</span><span class="sxs-lookup"><span data-stu-id="501a2-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="501a2-174">In hello **estensioni** finestra di dialogo, fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="501a2-174">On hello **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="501a2-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="501a2-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="501a2-176">In hello **impostazioni** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="501a2-176">In hello **Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="501a2-177">![Impostazioni](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="501a2-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="501a2-178">a.</span><span class="sxs-lookup"><span data-stu-id="501a2-178">a.</span></span> <span data-ttu-id="501a2-179">In **URL provider di identità** casella di testo, hello Incolla valore **URL servizio Single Sign-On**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="501a2-179">In **Identity provider URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="501a2-180">b.</span><span class="sxs-lookup"><span data-stu-id="501a2-180">b.</span></span> <span data-ttu-id="501a2-181">In **Certificate fingerprint** casella di testo, incollare hello **identificazione personale** valore del certificato, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="501a2-181">In **Certificate fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="501a2-182">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="501a2-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="501a2-183">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="501a2-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="501a2-184">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="501a2-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="501a2-185">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="501a2-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="501a2-186">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="501a2-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="501a2-187">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="501a2-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="501a2-189">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="501a2-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="501a2-190">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="501a2-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="501a2-192">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="501a2-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="501a2-194">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="501a2-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="501a2-196">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="501a2-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="501a2-198">a.</span><span class="sxs-lookup"><span data-stu-id="501a2-198">a.</span></span> <span data-ttu-id="501a2-199">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="501a2-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="501a2-200">b.</span><span class="sxs-lookup"><span data-stu-id="501a2-200">b.</span></span> <span data-ttu-id="501a2-201">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="501a2-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="501a2-202">c.</span><span class="sxs-lookup"><span data-stu-id="501a2-202">c.</span></span> <span data-ttu-id="501a2-203">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="501a2-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="501a2-204">d.</span><span class="sxs-lookup"><span data-stu-id="501a2-204">d.</span></span> <span data-ttu-id="501a2-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="501a2-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="501a2-206">Creazione di un utente di test di Panorama9</span><span class="sxs-lookup"><span data-stu-id="501a2-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="501a2-207">In ordine tooenable Azure AD utenti toolog a Panorama9, è necessario eseguirne il provisioning in Panorama9.</span><span class="sxs-lookup"><span data-stu-id="501a2-207">In order tooenable Azure AD users toolog into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="501a2-208">Nel caso di hello di Panorama9, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="501a2-208">In hello case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="501a2-209">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="501a2-209">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="501a2-210">Accedi tooyour **Panorama9** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="501a2-210">Log in tooyour **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="501a2-211">Scegliere dal menu hello in primo piano hello **Gestisci**, quindi fare clic su **utenti**.</span><span class="sxs-lookup"><span data-stu-id="501a2-211">In hello menu on hello top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="501a2-212">![Utenti](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="501a2-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="501a2-213">Nella sezione utenti hello, fare clic su  **+**  tooadd nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="501a2-213">In hello Users section, Click **+** tooadd new user.</span></span>

 <span data-ttu-id="501a2-214">![Utenti](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="501a2-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="501a2-215">Passa toohello sezione di dati utente, hello tipo indirizzo di posta elettronica di un utente di Azure Active Directory valido, si desidera tooprovision in hello **posta elettronica** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="501a2-215">Go toohello User data section, type hello email address of a valid Azure Active Directory user you want tooprovision into hello **Email** textbox.</span></span>

5. <span data-ttu-id="501a2-216">Provenire toohello sezione utenti, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="501a2-216">Come toohello Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="501a2-217">titolare dell'account di Azure Active Directory Hello riceve un messaggio di posta elettronica e segue il proprio account tooconfirm un collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="501a2-217">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="501a2-218">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="501a2-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="501a2-219">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPanorama9.</span><span class="sxs-lookup"><span data-stu-id="501a2-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanorama9.</span></span>

![Assegna utente][200] 

<span data-ttu-id="501a2-221">**tooassign Britta Simon tooPanorama9, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="501a2-221">**tooassign Britta Simon tooPanorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="501a2-222">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="501a2-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="501a2-224">Nell'elenco di applicazioni hello, selezionare **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="501a2-224">In hello applications list, select **Panorama9**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="501a2-226">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="501a2-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="501a2-228">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="501a2-228">Click **Add** button.</span></span> <span data-ttu-id="501a2-229">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="501a2-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="501a2-231">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="501a2-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="501a2-232">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="501a2-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="501a2-233">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="501a2-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="501a2-234">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="501a2-234">Testing single sign-on</span></span>

<span data-ttu-id="501a2-235">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="501a2-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="501a2-236">Quando si fa clic su riquadro hello Panorama9 in hello Pannello di accesso, è necessario ottenere tooPanorama9 automaticamente firmato in applicazione.</span><span class="sxs-lookup"><span data-stu-id="501a2-236">When you click hello Panorama9 tile in hello Access Panel, you should get automatically signed-on tooPanorama9 application.</span></span>
<span data-ttu-id="501a2-237">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="501a2-237">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="501a2-238">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="501a2-238">Additional resources</span></span>

* [<span data-ttu-id="501a2-239">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="501a2-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="501a2-240">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="501a2-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

