---
title: 'Esercitazione: Integrazione di Azure Active Directory con Tableau Online | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Tableau Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="b0d3a-103">Esercitazione: Integrazione di Azure Active Directory con Tableau Online</span><span class="sxs-lookup"><span data-stu-id="b0d3a-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="b0d3a-104">In questa esercitazione, è illustrato come toointegrate Tableau Online con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0d3a-104">In this tutorial, you learn how toointegrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0d3a-105">Integrazione Tableau Online con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="b0d3a-105">Integrating Tableau Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b0d3a-106">È possibile controllare in Azure AD che ha accesso tooTableau Online</span><span class="sxs-lookup"><span data-stu-id="b0d3a-106">You can control in Azure AD who has access tooTableau Online</span></span>
- <span data-ttu-id="b0d3a-107">È possibile abilitare l'utenti tooautomatically get connesso tooTableau Online (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0d3a-107">You can enable your users tooautomatically get signed-on tooTableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b0d3a-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b0d3a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b0d3a-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b0d3a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0d3a-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b0d3a-110">Prerequisites</span></span>

<span data-ttu-id="b0d3a-111">tooconfigure integrazione di Azure AD con Tableau Online, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="b0d3a-111">tooconfigure Azure AD integration with Tableau Online, you need hello following items:</span></span>

- <span data-ttu-id="b0d3a-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0d3a-113">Sottoscrizione di Tableau Online abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b0d3a-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0d3a-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0d3a-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="b0d3a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0d3a-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0d3a-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0d3a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0d3a-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b0d3a-118">Scenario description</span></span>
<span data-ttu-id="b0d3a-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0d3a-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="b0d3a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0d3a-121">Aggiunta di Tableau Online dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b0d3a-121">Adding Tableau Online from hello gallery</span></span>
2. <span data-ttu-id="b0d3a-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0d3a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-hello-gallery"></a><span data-ttu-id="b0d3a-123">Aggiunta di Tableau Online dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b0d3a-123">Adding Tableau Online from hello gallery</span></span>
<span data-ttu-id="b0d3a-124">integrazione hello tooconfigure di Tableau Online in Azure AD, è necessario tooadd Tableau Online dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-124">tooconfigure hello integration of Tableau Online into Azure AD, you need tooadd Tableau Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b0d3a-125">**tooadd Tableau Online dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b0d3a-125">**tooadd Tableau Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0d3a-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b0d3a-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b0d3a-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="b0d3a-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="b0d3a-133">Nella casella di ricerca hello, digitare **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-133">In hello search box, type **Tableau Online**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="b0d3a-135">Nel riquadro dei risultati hello, selezionare **Tableau Online**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-135">In hello results panel, select **Tableau Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b0d3a-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0d3a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b0d3a-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Tableau Online usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b0d3a-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b0d3a-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Tableau Online è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Online is tooa user in Azure AD.</span></span> <span data-ttu-id="b0d3a-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Tableau Online richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Online needs toobe established.</span></span>

<span data-ttu-id="b0d3a-141">In linea Tableau, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-141">In Tableau Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b0d3a-142">tooconfigure e prova AD Azure single sign-on con Tableau Online, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="b0d3a-142">tooconfigure and test Azure AD single sign-on with Tableau Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b0d3a-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b0d3a-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0d3a-145">**[Creazione di un utente test Online Tableau](#creating-a-tableau-online-test-user)**  -toohave un equivalente di Britta Simon in Tableau Online è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - toohave a counterpart of Britta Simon in Tableau Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b0d3a-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0d3a-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b0d3a-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0d3a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b0d3a-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="b0d3a-150">**Azure AD tooconfigure single sign-on con Tableau Online, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b0d3a-150">**tooconfigure Azure AD single sign-on with Tableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0d3a-151">Nel portale di Azure su hello hello **Tableau Online** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-151">In hello Azure portal, on hello **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="b0d3a-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="b0d3a-155">In hello **Tableau Online dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b0d3a-155">On hello **Tableau Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="b0d3a-157">a.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-157">a.</span></span> <span data-ttu-id="b0d3a-158">In hello **Sign-on URL** casella di testo, digitare l'URL hello:`https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="b0d3a-158">In hello **Sign-on URL** textbox, type hello URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="b0d3a-159">b.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-159">b.</span></span> <span data-ttu-id="b0d3a-160">In hello **identificatore** casella di testo, digitare l'URL hello:`https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="b0d3a-160">In hello **Identifier** textbox, type hello URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="b0d3a-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="b0d3a-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b0d3a-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b0d3a-165">In un'altra finestra del browser sign-on tooyour Tableau Online delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-165">In a different browser window, sign-on tooyour Tableau Online application.</span></span> <span data-ttu-id="b0d3a-166">Andare troppo**impostazioni** e quindi **autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-166">Go too**Settings** and then **Authentication**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="b0d3a-168">tooenable SAML, in **tipi di autenticazione** sezione.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-168">tooenable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="b0d3a-169">Controllare hello **Single sign-on con SAML** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-169">Check hello **Single sign-on with SAML** checkbox.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="b0d3a-171">Scorrere verso il basso fino alla sezione **Import metadata file into Tableau Online** (Importa file di metadati in Tableau Online).</span><span class="sxs-lookup"><span data-stu-id="b0d3a-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="b0d3a-172">Fare clic su Sfoglia e importare il file di metadati hello che è stato scaricato da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-172">Click Browse and import hello metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="b0d3a-173">Fare quindi clic su **Apply**(Applica).</span><span class="sxs-lookup"><span data-stu-id="b0d3a-173">Then, click **Apply**.</span></span>
   
   ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="b0d3a-175">In hello **corrispondono asserzioni** sezione, inserire hello Provider di identità asserzione nome corrispondente **indirizzo di posta elettronica**, **nome**, e **cognome** .</span><span class="sxs-lookup"><span data-stu-id="b0d3a-175">In hello **Match assertions** section, insert hello corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="b0d3a-176">tooget queste informazioni da Azure AD:</span><span class="sxs-lookup"><span data-stu-id="b0d3a-176">tooget this information from Azure AD:</span></span> 
  
    <span data-ttu-id="b0d3a-177">a.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-177">a.</span></span> <span data-ttu-id="b0d3a-178">Nel portale di Azure hello, andare hello **Tableau Online** pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-178">In hello Azure portal, go on hello **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="b0d3a-179">b.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-179">b.</span></span> <span data-ttu-id="b0d3a-180">Nella sezione attributi hello selezionare hello **"consente di visualizzare e modificare tutti gli altri attributi utente"** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-180">In hello attributes section, Select hello **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="b0d3a-182">c.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-182">c.</span></span> <span data-ttu-id="b0d3a-183">Copiare il valore dello spazio dei nomi hello per questi attributi: givenname, posta elettronica e il cognome utilizzando hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b0d3a-183">Copy hello namespace value for these attributes: givenname, email and surname by using hello following steps:</span></span>

   ![Single Sign-On di Microsoft Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="b0d3a-185">d.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-185">d.</span></span> <span data-ttu-id="b0d3a-186">Fare clic sul valore **user.givenname**</span><span class="sxs-lookup"><span data-stu-id="b0d3a-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="b0d3a-187">e.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-187">e.</span></span> <span data-ttu-id="b0d3a-188">Copiare il valore di hello hello **dello spazio dei nomi** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-188">Copy hello value from hello **namespace** textbox.</span></span>

   ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="b0d3a-190">f.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-190">f.</span></span> <span data-ttu-id="b0d3a-191">i valori di spazio dei nomi di hello toocopy per posta elettronica hello e surname seguono hello passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-191">toocopy hello namesapce values for hello email and surname follow hello preceding steps.</span></span>

    <span data-ttu-id="b0d3a-192">g.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-192">g.</span></span> <span data-ttu-id="b0d3a-193">Passare toohello Tableau Online delle applicazioni, quindi impostare hello **Tableau Online attributi** sezione come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b0d3a-193">Switch toohello Tableau Online application, then set hello **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="b0d3a-194">Indirizzo di posta elettronica: **mail** o **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="b0d3a-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="b0d3a-195">Nome: **givenname**</span><span class="sxs-lookup"><span data-stu-id="b0d3a-195">First name: **givenname**</span></span>
     * <span data-ttu-id="b0d3a-196">Cognome: **surname**</span><span class="sxs-lookup"><span data-stu-id="b0d3a-196">Last name: **surname**</span></span>
   
   ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="b0d3a-198">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="b0d3a-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b0d3a-199">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b0d3a-200">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b0d3a-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b0d3a-201">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0d3a-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="b0d3a-202">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="b0d3a-204">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b0d3a-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0d3a-205">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b0d3a-207">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b0d3a-209">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b0d3a-211">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b0d3a-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b0d3a-213">a.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-213">a.</span></span> <span data-ttu-id="b0d3a-214">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b0d3a-215">b.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-215">b.</span></span> <span data-ttu-id="b0d3a-216">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b0d3a-217">c.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-217">c.</span></span> <span data-ttu-id="b0d3a-218">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b0d3a-219">d.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-219">d.</span></span> <span data-ttu-id="b0d3a-220">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="b0d3a-221">Creazione di un utente test di Tableau Online</span><span class="sxs-lookup"><span data-stu-id="b0d3a-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="b0d3a-222">In questa sezione viene creato un utente chiamato Britta Simon in Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="b0d3a-223">In **Tableau Online** fare clic su **Settings** (Impostazioni) e quindi sulla sezione **Authentication** (Autenticazione).</span><span class="sxs-lookup"><span data-stu-id="b0d3a-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="b0d3a-224">Scorrere verso il basso troppo**Seleziona utenti** sezione.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-224">Scroll down too**Select Users** section.</span></span> <span data-ttu-id="b0d3a-225">Fare clic su **Add Users** (Aggiungi utenti) e quindi su **Enter Email Addresses** (Immettere indirizzi di posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="b0d3a-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="b0d3a-227">Selezionare **Add users for single sign-on (SSO) authentication**(Aggiungi utenti per l'autenticazione Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="b0d3a-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="b0d3a-228">In hello **immettere indirizzi di posta elettronica** aggiungere casella di testobritta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="b0d3a-228">In hello **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="b0d3a-230">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-230">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b0d3a-231">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0d3a-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b0d3a-232">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooTableau Online.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Online.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b0d3a-234">**tooassign Britta Simon tooTableau Online, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b0d3a-234">**tooassign Britta Simon tooTableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0d3a-235">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b0d3a-237">Nell'elenco di applicazioni hello, selezionare **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-237">In hello applications list, select **Tableau Online**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="b0d3a-239">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b0d3a-241">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-241">Click **Add** button.</span></span> <span data-ttu-id="b0d3a-242">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b0d3a-244">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b0d3a-245">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0d3a-246">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b0d3a-247">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b0d3a-247">Testing single sign-on</span></span>

<span data-ttu-id="b0d3a-248">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="b0d3a-249">Quando si fa clic su riquadro Tableau Online di hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Tableau Online delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="b0d3a-249">When you click hello Tableau Online tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0d3a-250">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b0d3a-250">Additional resources</span></span>

* [<span data-ttu-id="b0d3a-251">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0d3a-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0d3a-252">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0d3a-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

