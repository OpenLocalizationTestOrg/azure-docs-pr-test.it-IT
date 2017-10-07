---
title: 'Esercitazione: Integrazione di Azure Active Directory con LearnUpon | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e LearnUpon.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="bb8ba-103">Esercitazione: Integrazione di Azure Active Directory con LearnUpon</span><span class="sxs-lookup"><span data-stu-id="bb8ba-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="bb8ba-104">In questa esercitazione, è illustrato come toointegrate LearnUpon con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bb8ba-104">In this tutorial, you learn how toointegrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bb8ba-105">Integrazione LearnUpon con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="bb8ba-105">Integrating LearnUpon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bb8ba-106">È possibile controllare in Azure AD che ha accesso tooLearnUpon</span><span class="sxs-lookup"><span data-stu-id="bb8ba-106">You can control in Azure AD who has access tooLearnUpon</span></span>
- <span data-ttu-id="bb8ba-107">È possibile abilitare l'utenti tooautomatically get connesso tooLearnUpon (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb8ba-107">You can enable your users tooautomatically get signed-on tooLearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bb8ba-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="bb8ba-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bb8ba-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bb8ba-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb8ba-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bb8ba-110">Prerequisites</span></span>

<span data-ttu-id="bb8ba-111">integrazione di Azure AD con LearnUpon tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="bb8ba-111">tooconfigure Azure AD integration with LearnUpon, you need hello following items:</span></span>

- <span data-ttu-id="bb8ba-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bb8ba-113">Sottoscrizione di LearnUpon abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bb8ba-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bb8ba-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bb8ba-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="bb8ba-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bb8ba-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bb8ba-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb8ba-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bb8ba-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="bb8ba-118">Scenario description</span></span>
<span data-ttu-id="bb8ba-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bb8ba-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="bb8ba-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bb8ba-121">Aggiunta di LearnUpon dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="bb8ba-121">Adding LearnUpon from hello gallery</span></span>
2. <span data-ttu-id="bb8ba-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb8ba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-hello-gallery"></a><span data-ttu-id="bb8ba-123">Aggiunta di LearnUpon dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="bb8ba-123">Adding LearnUpon from hello gallery</span></span>
<span data-ttu-id="bb8ba-124">integrazione hello tooconfigure di LearnUpon in Azure AD, è necessario tooadd LearnUpon dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-124">tooconfigure hello integration of LearnUpon into Azure AD, you need tooadd LearnUpon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bb8ba-125">**tooadd LearnUpon dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bb8ba-125">**tooadd LearnUpon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb8ba-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bb8ba-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bb8ba-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="bb8ba-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="bb8ba-133">Nella casella di ricerca hello, digitare **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-133">In hello search box, type **LearnUpon**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="bb8ba-135">Nel riquadro dei risultati hello, selezionare **LearnUpon**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-135">In hello results panel, select **LearnUpon**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bb8ba-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb8ba-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bb8ba-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LearnUpon in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bb8ba-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bb8ba-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in LearnUpon è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LearnUpon is tooa user in Azure AD.</span></span> <span data-ttu-id="bb8ba-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in LearnUpon deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-140">In other words, a link relationship between an Azure AD user and hello related user in LearnUpon needs toobe established.</span></span>

<span data-ttu-id="bb8ba-141">In LearnUpon, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-141">In LearnUpon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bb8ba-142">tooconfigure e prova AD Azure single sign-on con LearnUpon, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="bb8ba-142">tooconfigure and test Azure AD single sign-on with LearnUpon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bb8ba-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bb8ba-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bb8ba-145">**[Creazione di un utente test LearnUpon](#creating-a-learnupon-test-user)**  -toohave un equivalente di Britta Simon in LearnUpon che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - toohave a counterpart of Britta Simon in LearnUpon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bb8ba-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bb8ba-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bb8ba-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb8ba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bb8ba-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="bb8ba-150">**Azure AD tooconfigure single sign-on con LearnUpon, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bb8ba-150">**tooconfigure Azure AD single sign-on with LearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb8ba-151">Nel portale di Azure su hello hello **LearnUpon** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-151">In hello Azure portal, on hello **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="bb8ba-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="bb8ba-155">In hello **LearnUpon dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bb8ba-155">On hello **LearnUpon Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="bb8ba-157">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="bb8ba-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bb8ba-158">Si noti che questo non è il valore reale hello.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-158">Please note that this is not hello real value.</span></span> <span data-ttu-id="bb8ba-159">Hai tooupdate questo valore con l'URL di risposta effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-159">you have tooupdate this value with hello actual Reply URL.</span></span> <span data-ttu-id="bb8ba-160">Contattare questo valore tooget [team di supporto LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="bb8ba-160">tooget this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="bb8ba-161">In hello **certificato di firma SAML** fare clic su **certificato (Raw)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="bb8ba-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="bb8ba-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bb8ba-165">In hello **LearnUpon configurazione** fare clic su **configurare LearnUpon** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-165">On hello **LearnUpon Configuration** section, click **Configure LearnUpon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bb8ba-166">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="bb8ba-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="bb8ba-168">Aprire un'altra istanza del browser e accedere a LearnUpon con un account amministratore.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="bb8ba-169">Fare clic su hello **impostazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-169">Click hello **settings** tab.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="bb8ba-171">Fare clic su **Single Sign-On - SAML**, quindi fare clic su **impostazioni generali** tooconfigure SAML settings.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-171">Click **Single Sign On - SAML**, and then click **General Settings** tooconfigure SAML settings.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="bb8ba-173">In hello **impostazioni generali** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bb8ba-173">In hello **General Settings** section, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="bb8ba-175">a.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-175">a.</span></span> <span data-ttu-id="bb8ba-176">Selezionare **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-176">Select **Enabled**.</span></span>

    <span data-ttu-id="bb8ba-177">b.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-177">b.</span></span> <span data-ttu-id="bb8ba-178">Per **Version** selezionare **2.0**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="bb8ba-179">c.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-179">c.</span></span> <span data-ttu-id="bb8ba-180">Per **Skip conditions** (Ignorare le condizioni) selezionare **No**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="bb8ba-181">d.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-181">d.</span></span> <span data-ttu-id="bb8ba-182">In hello **Post Token SAML nome param** casella di testo Nome hello del tipo di richiesta post parametro toohello SAML consumer URL indicato in precedenza che contiene hello asserzione SAML toobe verificato e autenticato - ad esempio  **SAMLResponse**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-182">In hello **SAML Token Post param name** textbox, type hello name of request post parameter toohello SAML consumer URL indicated above that contains hello SAML Assertion toobe verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="bb8ba-183">e.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-183">e.</span></span> <span data-ttu-id="bb8ba-184">In hello **Name Identifier Format** casella di testo, valore che indica dove in agli utenti di asserzione SAML hello identificatore (indirizzo di posta elettronica) risiede - ad esempio hello del tipo **urn: oasis: nomi: tc: SAML: 1.1 NameID-formato: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-184">In hello **Name Identifier Format** textbox, type hello value that indicates where in your SAML Assertion hello users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="bb8ba-185">f.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-185">f.</span></span> <span data-ttu-id="bb8ba-186">In hello **identificare percorso del Provider** casella di testo, del tipo hello valore che indica dove hello tooif è vengono indirizzati gli utenti fanno clic sull'icona caricato da un'unica schermata di accesso al portale Azure.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-186">In hello **Identify Provider Location** textbox, type hello value that indicates where hello users are sent tooif they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="bb8ba-187">g.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-187">g.</span></span> <span data-ttu-id="bb8ba-188">In hello **Sign out URL** casella di testo, incollare hello **Sign-Out URL** che è stato copiato da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-188">In hello **Sign out URL** textbox, paste hello **Sign-Out URL** which you have copied from hello Azure portal.</span></span>
    
    <span data-ttu-id="bb8ba-189">h.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-189">h.</span></span> <span data-ttu-id="bb8ba-190">Fare clic su **Gestione stampa dito**, quindi caricare impronte digitali hello del certificato scaricato.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-190">Click **Manage finger prints**, and then upload hello finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="bb8ba-191">Fare clic su **impostazioni utente**e quindi eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bb8ba-191">Click **User Settings**, and then perform hello following steps:</span></span>
   
     ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="bb8ba-193">a.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-193">a.</span></span> <span data-ttu-id="bb8ba-194">In hello **formato identificatore nome** casella di testo, valore che indica dove in firstname di utenti hello l'asserzione SAML hello del tipo risiede - ad esempio: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-194">In hello **First Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="bb8ba-195">b.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-195">b.</span></span> <span data-ttu-id="bb8ba-196">In hello **ultimo Name Identifier Format** casella Tipo hello valore che indica dove è il cognome di asserzione SAML hello gli utenti in si trova - ad esempio: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-196">In hello **Last Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="bb8ba-197">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="bb8ba-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bb8ba-198">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bb8ba-199">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bb8ba-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bb8ba-200">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb8ba-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="bb8ba-201">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="bb8ba-203">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bb8ba-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb8ba-204">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bb8ba-206">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bb8ba-208">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bb8ba-210">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bb8ba-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bb8ba-212">a.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-212">a.</span></span> <span data-ttu-id="bb8ba-213">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bb8ba-214">b.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-214">b.</span></span> <span data-ttu-id="bb8ba-215">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bb8ba-216">c.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-216">c.</span></span> <span data-ttu-id="bb8ba-217">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bb8ba-218">d.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-218">d.</span></span> <span data-ttu-id="bb8ba-219">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="bb8ba-220">Creazione di un utente test LearnUpon</span><span class="sxs-lookup"><span data-stu-id="bb8ba-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="bb8ba-221">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in LearnUpon toocreate.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-221">hello objective of this section is toocreate a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="bb8ba-222">LearnUpon supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="bb8ba-223">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-223">There is no action item for you in this section.</span></span> <span data-ttu-id="bb8ba-224">Verrà creato un nuovo utente durante una tooaccess tentativo LearnUpon se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-224">A new user will be created during an attempt tooaccess LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="bb8ba-225">[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="bb8ba-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="bb8ba-226">Se è necessario un utente toocreate manualmente, è necessario toocontact [team di supporto LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="bb8ba-226">If you need toocreate an user manually, you need toocontact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bb8ba-227">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb8ba-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bb8ba-228">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLearnUpon.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearnUpon.</span></span>

![Assegna utente][200] 

<span data-ttu-id="bb8ba-230">**tooassign Britta Simon tooLearnUpon, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="bb8ba-230">**tooassign Britta Simon tooLearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb8ba-231">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="bb8ba-233">Nell'elenco di applicazioni hello, selezionare **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-233">In hello applications list, select **LearnUpon**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="bb8ba-235">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="bb8ba-237">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-237">Click **Add** button.</span></span> <span data-ttu-id="bb8ba-238">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="bb8ba-240">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bb8ba-241">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bb8ba-242">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bb8ba-243">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bb8ba-243">Testing single sign-on</span></span>

<span data-ttu-id="bb8ba-244">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bb8ba-245">Quando si fa clic su riquadro LearnUpon hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour LearnUpon applicazione.</span><span class="sxs-lookup"><span data-stu-id="bb8ba-245">When you click hello LearnUpon tile in hello Access Panel, you should get automatically signed-on tooyour LearnUpon application.</span></span>
<span data-ttu-id="bb8ba-246">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bb8ba-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb8ba-247">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="bb8ba-247">Additional resources</span></span>

* [<span data-ttu-id="bb8ba-248">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb8ba-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb8ba-249">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb8ba-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

