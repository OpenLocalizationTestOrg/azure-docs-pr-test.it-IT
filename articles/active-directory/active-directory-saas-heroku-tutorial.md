---
title: 'Esercitazione: Integrazione di Azure Active Directory con Heroku | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Heroku.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee11db647fd385140f1dbcab2586dfafffe5d912
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="04b89-103">Esercitazione: Integrazione di Azure Active Directory con Heroku</span><span class="sxs-lookup"><span data-stu-id="04b89-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="04b89-104">In questa esercitazione, è illustrato come toointegrate Heroku con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="04b89-104">In this tutorial, you learn how toointegrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="04b89-105">Integrazione Heroku con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="04b89-105">Integrating Heroku with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="04b89-106">È possibile controllare in Azure AD che ha accesso tooHeroku</span><span class="sxs-lookup"><span data-stu-id="04b89-106">You can control in Azure AD who has access tooHeroku</span></span>
- <span data-ttu-id="04b89-107">È possibile abilitare l'utenti tooautomatically get connesso tooHeroku (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="04b89-107">You can enable your users tooautomatically get signed-on tooHeroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="04b89-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="04b89-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="04b89-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="04b89-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04b89-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="04b89-110">Prerequisites</span></span>

<span data-ttu-id="04b89-111">integrazione di Azure AD con Heroku tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="04b89-111">tooconfigure Azure AD integration with Heroku, you need hello following items:</span></span>

- <span data-ttu-id="04b89-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04b89-112">An Azure AD subscription</span></span>
- <span data-ttu-id="04b89-113">Sottoscrizione di Heroku abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="04b89-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="04b89-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="04b89-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="04b89-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="04b89-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="04b89-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="04b89-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="04b89-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="04b89-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="04b89-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="04b89-118">Scenario description</span></span>
<span data-ttu-id="04b89-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="04b89-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="04b89-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="04b89-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="04b89-121">Aggiunta di Heroku dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="04b89-121">Adding Heroku from hello gallery</span></span>
2. <span data-ttu-id="04b89-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="04b89-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-hello-gallery"></a><span data-ttu-id="04b89-123">Aggiunta di Heroku dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="04b89-123">Adding Heroku from hello gallery</span></span>
<span data-ttu-id="04b89-124">integrazione hello tooconfigure di Heroku in Azure AD, è necessario tooadd Heroku dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="04b89-124">tooconfigure hello integration of Heroku into Azure AD, you need tooadd Heroku from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="04b89-125">**tooadd Heroku dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="04b89-125">**tooadd Heroku from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="04b89-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="04b89-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="04b89-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="04b89-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="04b89-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="04b89-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="04b89-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="04b89-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="04b89-133">Nella casella di ricerca hello, digitare **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="04b89-133">In hello search box, type **Heroku**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="04b89-135">Nel riquadro dei risultati hello, selezionare **Heroku**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="04b89-135">In hello results panel, select **Heroku**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="04b89-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="04b89-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="04b89-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Heroku con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="04b89-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="04b89-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Heroku è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04b89-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Heroku is tooa user in Azure AD.</span></span> <span data-ttu-id="04b89-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Heroku deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="04b89-140">In other words, a link relationship between an Azure AD user and hello related user in Heroku needs toobe established.</span></span>

<span data-ttu-id="04b89-141">In Heroku, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="04b89-141">In Heroku, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="04b89-142">tooconfigure e prova AD Azure single sign-on con Heroku, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="04b89-142">tooconfigure and test Azure AD single sign-on with Heroku, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="04b89-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="04b89-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="04b89-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="04b89-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="04b89-145">**[Creazione di un utente test Heroku](#creating-a-heroku-test-user)**  -toohave un equivalente di Britta Simon in Heroku che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="04b89-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - toohave a counterpart of Britta Simon in Heroku that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="04b89-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="04b89-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="04b89-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="04b89-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="04b89-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="04b89-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="04b89-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Heroku.</span><span class="sxs-lookup"><span data-stu-id="04b89-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="04b89-150">**Azure AD tooconfigure single sign-on con Heroku, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="04b89-150">**tooconfigure Azure AD single sign-on with Heroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="04b89-151">Nel portale di Azure su hello hello **Heroku** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="04b89-151">In hello Azure portal, on hello **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="04b89-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="04b89-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="04b89-155">In hello **Heroku dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="04b89-155">On hello **Heroku Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="04b89-157">a.</span><span class="sxs-lookup"><span data-stu-id="04b89-157">a.</span></span> <span data-ttu-id="04b89-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="04b89-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="04b89-159">b.</span><span class="sxs-lookup"><span data-stu-id="04b89-159">b.</span></span> <span data-ttu-id="04b89-160">In hello **URL dell'identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="04b89-160">In hello **Identifier URL** textbox, type a URL using hello following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="04b89-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="04b89-161">These values are not real.</span></span> <span data-ttu-id="04b89-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="04b89-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="04b89-163">Questi valori vengono comunicati dal team di Heroku, come descritto nelle sezioni successive di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="04b89-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="04b89-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="04b89-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="04b89-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="04b89-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="04b89-168">tooenable SSO in Heroku, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="04b89-168">tooenable SSO in Heroku, perform hello following steps:</span></span>
   
    <span data-ttu-id="04b89-169">a.</span><span class="sxs-lookup"><span data-stu-id="04b89-169">a.</span></span> <span data-ttu-id="04b89-170">Accedi toohello Heroku account come amministratore.</span><span class="sxs-lookup"><span data-stu-id="04b89-170">Log in toohello Heroku account as an administrator.</span></span>

    <span data-ttu-id="04b89-171">b.</span><span class="sxs-lookup"><span data-stu-id="04b89-171">b.</span></span> <span data-ttu-id="04b89-172">Fare clic su hello **impostazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="04b89-172">Click hello **Settings** tab.</span></span>

    <span data-ttu-id="04b89-173">c.</span><span class="sxs-lookup"><span data-stu-id="04b89-173">c.</span></span> <span data-ttu-id="04b89-174">In hello **Single Sign in pagina**, fare clic su **Upload Metadata**.</span><span class="sxs-lookup"><span data-stu-id="04b89-174">On hello **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="04b89-175">d.</span><span class="sxs-lookup"><span data-stu-id="04b89-175">d.</span></span> <span data-ttu-id="04b89-176">Caricare file di metadati hello, che è stato scaricato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="04b89-176">Upload hello metadata file, which you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="04b89-177">e.</span><span class="sxs-lookup"><span data-stu-id="04b89-177">e.</span></span> <span data-ttu-id="04b89-178">Quando il programma di installazione di hello ha esito positivo, gli amministratori visualizzano una finestra di dialogo di conferma e viene visualizzato l'URL di hello di hello account di accesso SSO per gli utenti finali.</span><span class="sxs-lookup"><span data-stu-id="04b89-178">When hello setup is successful, administrators see a confirmation dialog and hello URL of hello SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="04b89-179">f.</span><span class="sxs-lookup"><span data-stu-id="04b89-179">f.</span></span> <span data-ttu-id="04b89-180">Hello copia **URL di accesso Heroku** e **ID entità Heroku** valori e si torna troppo**Heroku dominio e gli URL** sezione nel portale di Azure e incollare questi valori hello **Sign-On Url** e **identificatore** nelle caselle di testo rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="04b89-180">Copy hello **Heroku Login URL** and **Heroku Entity ID** values and go back too**Heroku Domain and URLs** section in Azure portal and paste these values into hello **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="04b89-182">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="04b89-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="04b89-183">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="04b89-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="04b89-184">Dopo l'aggiunta di questa app da hello **Active Directory Enterprise Applications** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="04b89-184">After adding this app from hello **Active Directory Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="04b89-185">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="04b89-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="04b89-186">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="04b89-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="04b89-187">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="04b89-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="04b89-189">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="04b89-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="04b89-190">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="04b89-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="04b89-192">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="04b89-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="04b89-194">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="04b89-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="04b89-196">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="04b89-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="04b89-198">a.</span><span class="sxs-lookup"><span data-stu-id="04b89-198">a.</span></span> <span data-ttu-id="04b89-199">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="04b89-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="04b89-200">b.</span><span class="sxs-lookup"><span data-stu-id="04b89-200">b.</span></span> <span data-ttu-id="04b89-201">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="04b89-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="04b89-202">c.</span><span class="sxs-lookup"><span data-stu-id="04b89-202">c.</span></span> <span data-ttu-id="04b89-203">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="04b89-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="04b89-204">d.</span><span class="sxs-lookup"><span data-stu-id="04b89-204">d.</span></span> <span data-ttu-id="04b89-205">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="04b89-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="04b89-206">Creazione di un utente test di Heroku</span><span class="sxs-lookup"><span data-stu-id="04b89-206">Creating a Heroku test user</span></span>

<span data-ttu-id="04b89-207">In questa sezione viene creato un utente chiamato Britta Simon in Heroku.</span><span class="sxs-lookup"><span data-stu-id="04b89-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="04b89-208">Heroku supporta il provisioning JIT (Just-In-Time) che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="04b89-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="04b89-209">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="04b89-209">There is no action item for you in this section.</span></span> <span data-ttu-id="04b89-210">Quando si accede a Heroku se utente hello non esiste ancora, viene creato un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="04b89-210">A new user is created when accessing Heroku if hello user doesn't exist yet.</span></span> <span data-ttu-id="04b89-211">Dopo il provisioning di account hello, hello utente riceve un messaggio di verifica e il collegamento di acknowledgement hello tooclick necessario.</span><span class="sxs-lookup"><span data-stu-id="04b89-211">After hello account is provisioned, hello end user receives a verification email and needs tooclick hello acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="04b89-212">Se è necessario un utente toocreate manualmente, è necessario hello toocontact [team di supporto Heroku Client](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="04b89-212">If you need toocreate a user manually, you need toocontact hello [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="04b89-213">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="04b89-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="04b89-214">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooHeroku.</span><span class="sxs-lookup"><span data-stu-id="04b89-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHeroku.</span></span>

![Assegna utente][200] 

<span data-ttu-id="04b89-216">**tooassign Britta Simon tooHeroku, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="04b89-216">**tooassign Britta Simon tooHeroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="04b89-217">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="04b89-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="04b89-219">Nell'elenco di applicazioni hello, selezionare **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="04b89-219">In hello applications list, select **Heroku**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="04b89-221">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="04b89-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="04b89-223">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="04b89-223">Click **Add** button.</span></span> <span data-ttu-id="04b89-224">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="04b89-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="04b89-226">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="04b89-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="04b89-227">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="04b89-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="04b89-228">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="04b89-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="04b89-229">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="04b89-229">Testing single sign-on</span></span>

<span data-ttu-id="04b89-230">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="04b89-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="04b89-231">Quando si fa clic su riquadro Heroku hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Heroku applicazione.</span><span class="sxs-lookup"><span data-stu-id="04b89-231">When you click hello Heroku tile in hello Access Panel, you should get automatically signed-on tooyour Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="04b89-232">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="04b89-232">Additional resources</span></span>

* [<span data-ttu-id="04b89-233">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04b89-233">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="04b89-234">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04b89-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
