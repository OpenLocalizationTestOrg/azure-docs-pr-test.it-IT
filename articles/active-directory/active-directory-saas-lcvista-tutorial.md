---
title: 'Esercitazione: integrazione di Azure Active Directory con LCVista | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e LCVista.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 5a4c7eb7d54b8b68c8241a97b9e516a3f6e55c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="1da52-103">Esercitazione: integrazione di Azure Active Directory con LCVista</span><span class="sxs-lookup"><span data-stu-id="1da52-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="1da52-104">In questa esercitazione, è illustrato come toointegrate LCVista con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1da52-104">In this tutorial, you learn how toointegrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1da52-105">Integrazione LCVista con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="1da52-105">Integrating LCVista with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1da52-106">È possibile controllare in Azure AD che ha accesso tooLCVista</span><span class="sxs-lookup"><span data-stu-id="1da52-106">You can control in Azure AD who has access tooLCVista</span></span>
- <span data-ttu-id="1da52-107">È possibile abilitare l'utenti tooautomatically get connesso tooLCVista (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1da52-107">You can enable your users tooautomatically get signed-on tooLCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1da52-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1da52-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1da52-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1da52-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1da52-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1da52-110">Prerequisites</span></span>

<span data-ttu-id="1da52-111">integrazione di Azure AD con LCVista tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1da52-111">tooconfigure Azure AD integration with LCVista, you need hello following items:</span></span>

- <span data-ttu-id="1da52-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1da52-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1da52-113">Sottoscrizione di LCVista abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1da52-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1da52-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1da52-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1da52-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="1da52-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1da52-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1da52-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1da52-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1da52-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1da52-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1da52-118">Scenario description</span></span>
<span data-ttu-id="1da52-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1da52-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1da52-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="1da52-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1da52-121">Aggiunta di LCVista dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1da52-121">Adding LCVista from hello gallery</span></span>
2. <span data-ttu-id="1da52-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1da52-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-hello-gallery"></a><span data-ttu-id="1da52-123">Aggiunta di LCVista dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1da52-123">Adding LCVista from hello gallery</span></span>
<span data-ttu-id="1da52-124">integrazione hello tooconfigure di LCVista in Azure AD, è necessario tooadd LCVista dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1da52-124">tooconfigure hello integration of LCVista into Azure AD, you need tooadd LCVista from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1da52-125">**tooadd LCVista dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1da52-125">**tooadd LCVista from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1da52-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1da52-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1da52-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1da52-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1da52-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1da52-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1da52-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1da52-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1da52-133">Nella casella di ricerca hello, digitare **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="1da52-133">In hello search box, type **LCVista**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="1da52-135">Nel riquadro dei risultati hello, selezionare **LCVista**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1da52-135">In hello results panel, select **LCVista**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1da52-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1da52-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1da52-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con LCVista in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1da52-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1da52-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in LCVista è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1da52-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LCVista is tooa user in Azure AD.</span></span> <span data-ttu-id="1da52-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in LCVista deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="1da52-140">In other words, a link relationship between an Azure AD user and hello related user in LCVista needs toobe established.</span></span>

<span data-ttu-id="1da52-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in LCVista.</span><span class="sxs-lookup"><span data-stu-id="1da52-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LCVista.</span></span>

<span data-ttu-id="1da52-142">tooconfigure e prova AD Azure single sign-on con LCVista, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1da52-142">tooconfigure and test Azure AD single sign-on with LCVista, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1da52-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1da52-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1da52-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1da52-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1da52-145">**[Creazione di un utente test LCVista](#creating-a-lcvista-test-user)**  -toohave un equivalente di Britta Simon in LCVista che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1da52-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - toohave a counterpart of Britta Simon in LCVista that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1da52-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1da52-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1da52-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1da52-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1da52-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1da52-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1da52-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione LCVista.</span><span class="sxs-lookup"><span data-stu-id="1da52-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="1da52-150">**Azure AD tooconfigure single sign-on con LCVista, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1da52-150">**tooconfigure Azure AD single sign-on with LCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="1da52-151">Nel portale di Azure su hello hello **LCVista** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1da52-151">In hello Azure portal, on hello **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1da52-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1da52-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="1da52-155">In hello **LCVista dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1da52-155">On hello **LCVista Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="1da52-157">a.</span><span class="sxs-lookup"><span data-stu-id="1da52-157">a.</span></span> <span data-ttu-id="1da52-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="1da52-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="1da52-159">b.</span><span class="sxs-lookup"><span data-stu-id="1da52-159">b.</span></span> <span data-ttu-id="1da52-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="1da52-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="1da52-161">Questi valori non sono hello reale.</span><span class="sxs-lookup"><span data-stu-id="1da52-161">These values are not hello real.</span></span> <span data-ttu-id="1da52-162">Aggiornare questi valori con hello effettivo identificatore e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1da52-162">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="1da52-163">Contatto [team di supporto LCVista Client](https://lcvista.com/contact) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="1da52-163">Contact [LCVista Client support team](https://lcvista.com/contact) tooget these values.</span></span> 

4. <span data-ttu-id="1da52-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1da52-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="1da52-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1da52-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="1da52-168">In hello **LCVista configurazione** fare clic su **configurare LCVista** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="1da52-168">On hello **LCVista Configuration** section, click **Configure LCVista** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1da52-169">Hello copia **ID entità SAML** e **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="1da52-169">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="1da52-171">Accesso tooyour LCVista applicazione come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1da52-171">Sign on tooyour LCVista application as an administrator.</span></span>

8. <span data-ttu-id="1da52-172">In hello **configurazione SAML** sezione, verificare hello **Abilita SAML login** e immettere i dettagli di hello, come indicato nella seguente immagine.</span><span class="sxs-lookup"><span data-stu-id="1da52-172">In hello **SAML Config** section, check hello **Enable SAML login** and enter hello details as mentioned in below image.</span></span> 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="1da52-174">a.</span><span class="sxs-lookup"><span data-stu-id="1da52-174">a.</span></span> <span data-ttu-id="1da52-175">Hello Incolla **URL autorità di certificazione** che è stato copiato da Azure AD in hello **ID entità** sezione.</span><span class="sxs-lookup"><span data-stu-id="1da52-175">Paste hello **Issuer URL** which you have copied from Azure AD in hello **Entity ID** section.</span></span> 

    <span data-ttu-id="1da52-176">b.</span><span class="sxs-lookup"><span data-stu-id="1da52-176">b.</span></span> <span data-ttu-id="1da52-177">Hello Incolla **URL servizio Single Sign-On** che è stato copiato da Azure AD in hello **URL** sezione.</span><span class="sxs-lookup"><span data-stu-id="1da52-177">Paste hello **Single Sign-On Service URL** which you have copied from Azure AD in hello **URL** section.</span></span>

    <span data-ttu-id="1da52-178">c.</span><span class="sxs-lookup"><span data-stu-id="1da52-178">c.</span></span> <span data-ttu-id="1da52-179">Da metadati (XML) che è stato scaricato dal portale di Azure, copiare il valore di hello **X509Certificate** e incollarlo in hello **certificato x509** sezione.</span><span class="sxs-lookup"><span data-stu-id="1da52-179">From Metadata (XML) which you have downloaded from Azure portal, copy hello value **X509Certificate** and paste it in hello **x509 Certificate** section.</span></span>

    <span data-ttu-id="1da52-180">d.</span><span class="sxs-lookup"><span data-stu-id="1da52-180">d.</span></span> <span data-ttu-id="1da52-181">In hello **nome attributo** casella di testo, il valore di hello Incolla `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="1da52-181">In hello **First name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="1da52-182">e.</span><span class="sxs-lookup"><span data-stu-id="1da52-182">e.</span></span> <span data-ttu-id="1da52-183">In hello **ultimo attributo nome** casella di testo, il valore di hello Incolla `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="1da52-183">In hello **Last name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="1da52-184">f.</span><span class="sxs-lookup"><span data-stu-id="1da52-184">f.</span></span> <span data-ttu-id="1da52-185">In hello **Email attribute** casella di testo, il valore di hello Incolla `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="1da52-185">In hello **Email attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="1da52-186">g.</span><span class="sxs-lookup"><span data-stu-id="1da52-186">g.</span></span> <span data-ttu-id="1da52-187">In hello **attributo Username** casella di testo, il valore di hello Incolla `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="1da52-187">In hello **Username attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="1da52-188">e.</span><span class="sxs-lookup"><span data-stu-id="1da52-188">e.</span></span> <span data-ttu-id="1da52-189">Fare clic su **salvare** impostazioni hello toosave.</span><span class="sxs-lookup"><span data-stu-id="1da52-189">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="1da52-190">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="1da52-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1da52-191">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="1da52-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1da52-192">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1da52-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1da52-193">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1da52-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="1da52-194">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1da52-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1da52-196">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1da52-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1da52-197">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1da52-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1da52-199">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1da52-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1da52-201">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="1da52-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1da52-203">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1da52-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1da52-205">a.</span><span class="sxs-lookup"><span data-stu-id="1da52-205">a.</span></span> <span data-ttu-id="1da52-206">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1da52-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1da52-207">b.</span><span class="sxs-lookup"><span data-stu-id="1da52-207">b.</span></span> <span data-ttu-id="1da52-208">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1da52-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1da52-209">c.</span><span class="sxs-lookup"><span data-stu-id="1da52-209">c.</span></span> <span data-ttu-id="1da52-210">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="1da52-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1da52-211">d.</span><span class="sxs-lookup"><span data-stu-id="1da52-211">d.</span></span> <span data-ttu-id="1da52-212">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1da52-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="1da52-213">Creazione di un utente test LCVista</span><span class="sxs-lookup"><span data-stu-id="1da52-213">Creating a LCVista test user</span></span>

<span data-ttu-id="1da52-214">In questa sezione viene creato un utente chiamato Britta Simon in LCVista.</span><span class="sxs-lookup"><span data-stu-id="1da52-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="1da52-215">È necessario toocontact [team di supporto LCVista Client](https://lcvista.com/contact) tooadd utenti hello hello LCVista applicazione.</span><span class="sxs-lookup"><span data-stu-id="1da52-215">You need toocontact [LCVista Client support team](https://lcvista.com/contact) tooadd hello users in hello LCVista application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1da52-216">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1da52-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1da52-217">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooLCVista.</span><span class="sxs-lookup"><span data-stu-id="1da52-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLCVista.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1da52-219">**tooassign Britta Simon tooLCVista, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1da52-219">**tooassign Britta Simon tooLCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="1da52-220">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1da52-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1da52-222">Nell'elenco di applicazioni hello, selezionare **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="1da52-222">In hello applications list, select **LCVista**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="1da52-224">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1da52-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1da52-226">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1da52-226">Click **Add** button.</span></span> <span data-ttu-id="1da52-227">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1da52-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1da52-229">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1da52-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1da52-230">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1da52-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1da52-231">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1da52-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1da52-232">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1da52-232">Testing single sign-on</span></span>

<span data-ttu-id="1da52-233">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1da52-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="1da52-234">Fare clic sul riquadro LCVista hello in hello Pannello di accesso, sarà reindirizzato tooOrganization della pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="1da52-234">Click hello LCVista tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="1da52-235">Dopo aver eseguito l'accesso, sarà connesso tooyour LCVista applicazione.</span><span class="sxs-lookup"><span data-stu-id="1da52-235">After successful login, you will be signed-on tooyour LCVista application.</span></span> <span data-ttu-id="1da52-236">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="1da52-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1da52-237">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1da52-237">Additional resources</span></span>

* [<span data-ttu-id="1da52-238">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1da52-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1da52-239">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1da52-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

