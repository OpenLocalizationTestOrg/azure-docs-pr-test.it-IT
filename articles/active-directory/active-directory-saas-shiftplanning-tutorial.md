---
title: 'Esercitazione: Integrazione di Azure Active Directory con Humanity | Microsoft Docs'
description: "Informazioni su come tooconfigure single sign-on tra Azure Active Directory e umanità."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d8a04a2eb3c997f86f1e199c47809fa3dad60e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="ad212-103">Esercitazione: integrazione di Azure Active Directory con Humanity</span><span class="sxs-lookup"><span data-stu-id="ad212-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="ad212-104">In questa esercitazione, è illustrato come toointegrate umanità con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad212-104">In this tutorial, you learn how toointegrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad212-105">Integrazione umanità con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="ad212-105">Integrating Humanity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ad212-106">È possibile controllare in Azure AD che ha accesso tooHumanity</span><span class="sxs-lookup"><span data-stu-id="ad212-106">You can control in Azure AD who has access tooHumanity</span></span>
- <span data-ttu-id="ad212-107">È possibile abilitare l'utenti tooautomatically get connesso tooHumanity (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad212-107">You can enable your users tooautomatically get signed-on tooHumanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ad212-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ad212-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ad212-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad212-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad212-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ad212-110">Prerequisites</span></span>

<span data-ttu-id="ad212-111">integrazione di Azure AD con umanità tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ad212-111">tooconfigure Azure AD integration with Humanity, you need hello following items:</span></span>

- <span data-ttu-id="ad212-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad212-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad212-113">Sottoscrizione di Humanity abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ad212-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad212-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ad212-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad212-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="ad212-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad212-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ad212-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ad212-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad212-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad212-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ad212-118">Scenario description</span></span>
<span data-ttu-id="ad212-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ad212-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad212-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="ad212-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad212-121">Aggiunta di umanità dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ad212-121">Adding Humanity from hello gallery</span></span>
2. <span data-ttu-id="ad212-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad212-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-hello-gallery"></a><span data-ttu-id="ad212-123">Aggiunta di umanità dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ad212-123">Adding Humanity from hello gallery</span></span>
<span data-ttu-id="ad212-124">integrazione di hello tooconfigure di umanità in Azure AD, è necessario tooadd umanità dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ad212-124">tooconfigure hello integration of Humanity into Azure AD, you need tooadd Humanity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ad212-125">**tooadd umanità dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ad212-125">**tooadd Humanity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad212-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ad212-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ad212-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ad212-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ad212-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ad212-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="ad212-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ad212-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="ad212-133">Nella casella di ricerca hello, digitare **umanità**.</span><span class="sxs-lookup"><span data-stu-id="ad212-133">In hello search box, type **Humanity**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="ad212-135">Nel riquadro dei risultati hello, selezionare **umanità**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ad212-135">In hello results panel, select **Humanity**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ad212-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad212-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ad212-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Humanity usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ad212-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ad212-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in umanità è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad212-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Humanity is tooa user in Azure AD.</span></span> <span data-ttu-id="ad212-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato hello umanità deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="ad212-140">In other words, a link relationship between an Azure AD user and hello related user in Humanity needs toobe established.</span></span>

<span data-ttu-id="ad212-141">In umanità, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="ad212-141">In Humanity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ad212-142">tooconfigure e prova AD Azure single sign-on con umanità, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="ad212-142">tooconfigure and test Azure AD single sign-on with Humanity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ad212-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ad212-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ad212-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad212-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad212-145">**[Creazione di un utente test umanità](#creating-a-humanity-test-user)**  -toohave un equivalente di Britta Simon in umanità che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ad212-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - toohave a counterpart of Britta Simon in Humanity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ad212-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ad212-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad212-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="ad212-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ad212-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad212-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ad212-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione umanità.</span><span class="sxs-lookup"><span data-stu-id="ad212-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="ad212-150">**Azure AD tooconfigure single sign-on con umanità, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ad212-150">**tooconfigure Azure AD single sign-on with Humanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad212-151">Nel portale di Azure su hello hello **umanità** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ad212-151">In hello Azure portal, on hello **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="ad212-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ad212-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="ad212-155">In hello **umanità dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ad212-155">On hello **Humanity Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="ad212-157">a.</span><span class="sxs-lookup"><span data-stu-id="ad212-157">a.</span></span> <span data-ttu-id="ad212-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="ad212-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="ad212-159">b.</span><span class="sxs-lookup"><span data-stu-id="ad212-159">b.</span></span> <span data-ttu-id="ad212-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="ad212-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ad212-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="ad212-161">These values are not real.</span></span> <span data-ttu-id="ad212-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="ad212-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ad212-163">Contatto [team di supporto Client umanità](https://www.humanity.com/support/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="ad212-163">Contact [Humanity Client support team](https://www.humanity.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="ad212-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="ad212-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="ad212-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ad212-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ad212-168">In hello **configurazione umanità** fare clic su **configurare umanità** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="ad212-168">On hello **Humanity Configuration** section, click **Configure Humanity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ad212-169">Hello copia **SAML Single Sign-On Service URL e Sign-Out URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="ad212-169">Copy hello **SAML Single Sign-On Service URL, and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="ad212-171">In una finestra del web browser, accedere tooyour **umanità** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ad212-171">In a different web browser window, log in tooyour **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="ad212-172">Scegliere dal menu hello in primo piano hello **Admin**.</span><span class="sxs-lookup"><span data-stu-id="ad212-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="ad212-173">![Amministratore](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="ad212-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="ad212-174">In **Integrazione** fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="ad212-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="ad212-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ad212-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="ad212-176">In hello **Single Sign-On** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ad212-176">In hello **Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ad212-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ad212-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="ad212-178">a.</span><span class="sxs-lookup"><span data-stu-id="ad212-178">a.</span></span> <span data-ttu-id="ad212-179">Selezionare **Abilitato SAML**.</span><span class="sxs-lookup"><span data-stu-id="ad212-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="ad212-180">b.</span><span class="sxs-lookup"><span data-stu-id="ad212-180">b.</span></span> <span data-ttu-id="ad212-181">Selezionare **Allow Password Login** (Consenti accesso tramite password).</span><span class="sxs-lookup"><span data-stu-id="ad212-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="ad212-182">c.</span><span class="sxs-lookup"><span data-stu-id="ad212-182">c.</span></span> <span data-ttu-id="ad212-183">Hello Incolla **SAML Single Sign-On Service URL** valore in hello **SAML Issuer URL** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ad212-183">Paste hello **SAML Single Sign-On Service URL** value into hello **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="ad212-184">d.</span><span class="sxs-lookup"><span data-stu-id="ad212-184">d.</span></span> <span data-ttu-id="ad212-185">Hello Incolla **Sign-Out URL** valore in hello **URL disconnessione remota** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ad212-185">Paste hello **Sign-Out URL** value into hello **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="ad212-186">e.</span><span class="sxs-lookup"><span data-stu-id="ad212-186">e.</span></span> <span data-ttu-id="ad212-187">Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollarlo toohello **certificato x. 509** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ad212-187">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="ad212-188">Fare clic su **Salva impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="ad212-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="ad212-189">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="ad212-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ad212-190">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="ad212-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ad212-191">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ad212-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ad212-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad212-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="ad212-193">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ad212-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="ad212-195">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ad212-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad212-196">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ad212-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ad212-198">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ad212-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ad212-200">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="ad212-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ad212-202">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ad212-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad212-204">a.</span><span class="sxs-lookup"><span data-stu-id="ad212-204">a.</span></span> <span data-ttu-id="ad212-205">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad212-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad212-206">b.</span><span class="sxs-lookup"><span data-stu-id="ad212-206">b.</span></span> <span data-ttu-id="ad212-207">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ad212-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad212-208">c.</span><span class="sxs-lookup"><span data-stu-id="ad212-208">c.</span></span> <span data-ttu-id="ad212-209">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="ad212-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ad212-210">d.</span><span class="sxs-lookup"><span data-stu-id="ad212-210">d.</span></span> <span data-ttu-id="ad212-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ad212-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="ad212-212">Creazione di un utente di test di Humanity</span><span class="sxs-lookup"><span data-stu-id="ad212-212">Creating a Humanity test user</span></span>

<span data-ttu-id="ad212-213">In ordine tooenable Azure AD utenti toolog in tooHumanity, è necessario eseguirne il provisioning in umanità.</span><span class="sxs-lookup"><span data-stu-id="ad212-213">In order tooenable Azure AD users toolog in tooHumanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="ad212-214">Nel caso di hello di umanità, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="ad212-214">In hello case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="ad212-215">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ad212-215">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad212-216">Accedi tooyour **umanità** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ad212-216">Log in tooyour **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="ad212-217">Fare clic su **Admin**.</span><span class="sxs-lookup"><span data-stu-id="ad212-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="ad212-218">![Amministratore](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Amministratore")</span><span class="sxs-lookup"><span data-stu-id="ad212-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="ad212-219">Fare clic su **Personale**.</span><span class="sxs-lookup"><span data-stu-id="ad212-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="ad212-220">![Personale](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Personale")</span><span class="sxs-lookup"><span data-stu-id="ad212-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="ad212-221">In **Actions** (Azioni) fare clic su **Add Employees** (Aggiungi dipendenti).</span><span class="sxs-lookup"><span data-stu-id="ad212-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="ad212-222">![Aggiungi dipendenti](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Aggiungi dipendenti")</span><span class="sxs-lookup"><span data-stu-id="ad212-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="ad212-223">In hello **Add Employees** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ad212-223">In hello **Add Employees** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ad212-224">![Salvare i dipendenti](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Salvare i dipendenti")</span><span class="sxs-lookup"><span data-stu-id="ad212-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="ad212-225">a.</span><span class="sxs-lookup"><span data-stu-id="ad212-225">a.</span></span> <span data-ttu-id="ad212-226">Hello tipo **nome**, **cognome**, e **posta elettronica** di un account aAd di cui si desidera tooprovision in hello relative caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="ad212-226">Type hello **First Name**, **Last Name**, and **Email** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="ad212-227">b.</span><span class="sxs-lookup"><span data-stu-id="ad212-227">b.</span></span> <span data-ttu-id="ad212-228">Fare clic su **Salva dipendenti**.</span><span class="sxs-lookup"><span data-stu-id="ad212-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="ad212-229">È possibile usare qualsiasi altro umanità utente account strumento di creazione o le API fornite da tooprovision umanità account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="ad212-229">You can use any other Humanity user account creation tools or APIs provided by Humanity tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ad212-230">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad212-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ad212-231">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooHumanity.</span><span class="sxs-lookup"><span data-stu-id="ad212-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHumanity.</span></span>

![Assegna utente][200] 

<span data-ttu-id="ad212-233">**tooassign Britta Simon tooHumanity, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ad212-233">**tooassign Britta Simon tooHumanity, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad212-234">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ad212-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ad212-236">Nell'elenco di applicazioni hello, selezionare **umanità**.</span><span class="sxs-lookup"><span data-stu-id="ad212-236">In hello applications list, select **Humanity**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="ad212-238">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ad212-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="ad212-240">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ad212-240">Click **Add** button.</span></span> <span data-ttu-id="ad212-241">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ad212-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="ad212-243">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="ad212-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ad212-244">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ad212-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad212-245">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ad212-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ad212-246">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ad212-246">Testing single sign-on</span></span>

<span data-ttu-id="ad212-247">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ad212-247">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ad212-248">Quando si fa clic su riquadro umanità hello in hello Pannello di accesso, è necessario ottenere applicazione umanità tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="ad212-248">When you click hello Humanity tile in hello Access Panel, you should get automatically signed-on tooyour Humanity application.</span></span>
<span data-ttu-id="ad212-249">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ad212-249">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad212-250">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ad212-250">Additional resources</span></span>

* [<span data-ttu-id="ad212-251">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad212-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad212-252">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad212-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

