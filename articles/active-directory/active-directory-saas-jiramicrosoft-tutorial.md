---
title: 'Esercitazione: integrazione di Azure Active Directory con JIRA SAML SSO by Microsoft | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e JIRA SAML SSO da Microsoft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="be50b-103">Esercitazione: integrazione di Azure Active Directory con JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="be50b-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="be50b-104">In questa esercitazione, è illustrato come toointegrate JIRA SAML SSO da Microsoft con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="be50b-104">In this tutorial, you learn how toointegrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="be50b-105">Integrazione JIRA SAML SSO da Microsoft Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="be50b-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="be50b-106">È possibile controllare in Azure AD che ha accesso tooJIRA SAML SSO da Microsoft</span><span class="sxs-lookup"><span data-stu-id="be50b-106">You can control in Azure AD who has access tooJIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="be50b-107">È possibile abilitare l'utenti tooautomatically get connesso tooJIRA SAML SSO da Microsoft (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="be50b-107">You can enable your users tooautomatically get signed-on tooJIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="be50b-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="be50b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="be50b-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="be50b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be50b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="be50b-110">Prerequisites</span></span>

<span data-ttu-id="be50b-111">tooconfigure integrazione di Azure AD con JIRA SAML SSO da Microsoft, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="be50b-111">tooconfigure Azure AD integration with JIRA SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="be50b-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be50b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="be50b-113">Applicazione server JIRA installato in un server di Windows a 64 bit (in locale o nel cloud hello infrastruttura IaaS)</span><span class="sxs-lookup"><span data-stu-id="be50b-113">JIRA server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="be50b-114">Server JIRA abilitato per HTTPS</span><span class="sxs-lookup"><span data-stu-id="be50b-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="be50b-115">Nota hello è supportato nelle versioni del plug-in JIRA indicate nella seguente sezione.</span><span class="sxs-lookup"><span data-stu-id="be50b-115">Note hello supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="be50b-116">JIRA server sia raggiungibile nella rete internet particolarmente tooAzure AD account di accesso di pagina per l'autenticazione e deve tooreceive in grado di hello token da Azure AD</span><span class="sxs-lookup"><span data-stu-id="be50b-116">JIRA server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="be50b-117">Credenziali di amministratore configurate in JIRA</span><span class="sxs-lookup"><span data-stu-id="be50b-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="be50b-118">WebSudo disabilitato in JIRA</span><span class="sxs-lookup"><span data-stu-id="be50b-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="be50b-119">Utente creato nell'applicazione server JIRA hello test</span><span class="sxs-lookup"><span data-stu-id="be50b-119">Test user created in hello JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="be50b-120">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione di JIRA.</span><span class="sxs-lookup"><span data-stu-id="be50b-120">tootest hello steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="be50b-121">Prima di tutto testare integrazione hello nello sviluppo e gestione temporanea di ambiente dell'applicazione hello e quindi utilizzare hello ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="be50b-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="be50b-122">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="be50b-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="be50b-123">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="be50b-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="be50b-124">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="be50b-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="be50b-125">Versioni di JIRA supportate</span><span class="sxs-lookup"><span data-stu-id="be50b-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="be50b-126">A tutt'oggi sono supportate le versioni seguenti di JIRA:</span><span class="sxs-lookup"><span data-stu-id="be50b-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="be50b-127">Software e Core JIRA: too7.2.0 6.0</span><span class="sxs-lookup"><span data-stu-id="be50b-127">JIRA Core and Software: 6.0 too7.2.0</span></span>
- <span data-ttu-id="be50b-128">JIRA Service Desk: too3.2 3.0</span><span class="sxs-lookup"><span data-stu-id="be50b-128">JIRA Service Desk: 3.0 too3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="be50b-129">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="be50b-129">Scenario description</span></span>
<span data-ttu-id="be50b-130">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="be50b-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="be50b-131">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="be50b-131">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="be50b-132">Aggiunta di JIRA SAML SSO da Microsoft dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="be50b-132">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="be50b-133">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="be50b-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="be50b-134">Aggiunta di JIRA SAML SSO da Microsoft dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="be50b-134">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="be50b-135">integrazione hello tooconfigure di JIRA SAML SSO da Microsoft in Azure AD, è necessario tooadd JIRA SAML SSO da Microsoft dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="be50b-135">tooconfigure hello integration of JIRA SAML SSO by Microsoft into Azure AD, you need tooadd JIRA SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="be50b-136">**tooadd JIRA SAML SSO da Microsoft dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="be50b-136">**tooadd JIRA SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="be50b-137">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="be50b-137">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="be50b-139">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="be50b-139">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="be50b-140">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="be50b-140">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="be50b-142">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="be50b-142">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="be50b-144">Nella casella di ricerca hello, digitare **JIRA SAML SSO da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="be50b-144">In hello search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="be50b-146">Nel riquadro dei risultati hello, selezionare **JIRA SAML SSO da Microsoft**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="be50b-146">In hello results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="be50b-148">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="be50b-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="be50b-149">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con JIRA SAML SSO by Microsoft mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="be50b-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="be50b-150">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in JIRA SAML SSO da Microsoft è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be50b-150">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in JIRA SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="be50b-151">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in JIRA SAML SSO da Microsoft richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="be50b-151">In other words, a link relationship between an Azure AD user and hello related user in JIRA SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="be50b-152">In JIRA SAML SSO da Microsoft, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="be50b-152">In JIRA SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="be50b-153">tooconfigure e prova AD Azure single sign-on con JIRA SAML SSO da Microsoft, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="be50b-153">tooconfigure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="be50b-154">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="be50b-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="be50b-155">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="be50b-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="be50b-156">**[Creazione di un JIRA SAML SSO dall'utente di prova Microsoft](#creating-a-jira-saml-sso-by-microsoft-test-user)**  -toohave un equivalente di Britta Simon JIRA SAML SSO da Microsoft che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="be50b-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="be50b-157">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="be50b-157">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="be50b-158">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="be50b-158">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="be50b-159">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="be50b-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="be50b-160">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nel SAML SSO JIRA dall'applicazione di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="be50b-160">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="be50b-161">**tooconfigure AD Azure single sign-on con JIRA SAML SSO da Microsoft, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="be50b-161">**tooconfigure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="be50b-162">Nel portale di Azure su hello hello **JIRA SAML SSO da Microsoft** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="be50b-162">In hello Azure portal, on hello **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="be50b-164">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="be50b-164">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="be50b-166">In hello **JIRA SAML SSO URL e di Microsoft Domain** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="be50b-166">On hello **JIRA SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="be50b-168">a.</span><span class="sxs-lookup"><span data-stu-id="be50b-168">a.</span></span> <span data-ttu-id="be50b-169">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="be50b-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="be50b-170">b.</span><span class="sxs-lookup"><span data-stu-id="be50b-170">b.</span></span> <span data-ttu-id="be50b-171">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="be50b-171">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="be50b-172">c.</span><span class="sxs-lookup"><span data-stu-id="be50b-172">c.</span></span> <span data-ttu-id="be50b-173">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="be50b-173">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="be50b-174">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="be50b-174">These values are not real.</span></span> <span data-ttu-id="be50b-175">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="be50b-175">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="be50b-176">La porta è facoltativa nel caso di un URL denominato.</span><span class="sxs-lookup"><span data-stu-id="be50b-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="be50b-177">Questi valori vengono ricevuti durante la configurazione del plug-in Jira, illustrato più avanti nell'esercitazione di hello hello.</span><span class="sxs-lookup"><span data-stu-id="be50b-177">These values are received during hello configuration of Jira plugin, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="be50b-178">hello toogenerate **metadati** url, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="be50b-178">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="be50b-179">a.</span><span class="sxs-lookup"><span data-stu-id="be50b-179">a.</span></span> <span data-ttu-id="be50b-180">Fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="be50b-180">Click **App registrations**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="be50b-182">b.</span><span class="sxs-lookup"><span data-stu-id="be50b-182">b.</span></span> <span data-ttu-id="be50b-183">Fare clic su **endpoint** tooopen **endpoint** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="be50b-183">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="be50b-185">c.</span><span class="sxs-lookup"><span data-stu-id="be50b-185">c.</span></span> <span data-ttu-id="be50b-186">Fare clic su hello copia pulsante toocopy **documento metadati federazione** url e incollarlo nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="be50b-186">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="be50b-188">d.</span><span class="sxs-lookup"><span data-stu-id="be50b-188">d.</span></span> <span data-ttu-id="be50b-189">Ora passare toohello pagina delle proprietà di **JIRA SAML SSO da Microsoft** e hello copia **Id applicazione** utilizzando **copia** pulsante e incollarlo nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="be50b-189">Now go toohello property page of **JIRA SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="be50b-191">e.</span><span class="sxs-lookup"><span data-stu-id="be50b-191">e.</span></span> <span data-ttu-id="be50b-192">Generare hello **URL dei metadati** utilizzando hello seguente motivo: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` e copiare il valore nel blocco note come viene utilizzato in un secondo momento per la configurazione di hello del plug-in hello.</span><span class="sxs-lookup"><span data-stu-id="be50b-192">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="be50b-193">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="be50b-193">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="be50b-195">Contatto [Microsoft](mailto:waadpartners@microsoft.com) con le seguenti informazioni per i plug-in di hello JIRA hello.</span><span class="sxs-lookup"><span data-stu-id="be50b-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello JIRA plugin.</span></span>
    
    *   <span data-ttu-id="be50b-196">Nome del cliente:</span><span class="sxs-lookup"><span data-stu-id="be50b-196">Customer Name:</span></span>
    *   <span data-ttu-id="be50b-197">Nome del dominio primario:</span><span class="sxs-lookup"><span data-stu-id="be50b-197">Primary domain name:</span></span>
    *   <span data-ttu-id="be50b-198">Azure AD Premium: Sì/No (plug-in è disponibile tooall hello cliente gratuito, Basic e SKU Premium)</span><span class="sxs-lookup"><span data-stu-id="be50b-198">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="be50b-199">Numero di utenti che useranno questa integrazione:</span><span class="sxs-lookup"><span data-stu-id="be50b-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="be50b-200">Versione di JIRA:</span><span class="sxs-lookup"><span data-stu-id="be50b-200">JIRA Version:</span></span>
    *   <span data-ttu-id="be50b-201">Commenti:</span><span class="sxs-lookup"><span data-stu-id="be50b-201">Comments:</span></span>

7. <span data-ttu-id="be50b-202">In una finestra del web browser, accedere come amministratore nell'istanza JIRA tooyour.</span><span class="sxs-lookup"><span data-stu-id="be50b-202">In a different web browser window, log in tooyour JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="be50b-203">Passare il mouse su ruota dentata e scegliere hello **componenti aggiuntivi**.</span><span class="sxs-lookup"><span data-stu-id="be50b-203">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="be50b-205">Nella sezione della scheda Add-ons (Componenti aggiuntivi) fare clic su **Manage add-ons** (Gestisci componenti aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="be50b-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="be50b-207">Caricare manualmente i plug-in hello fornito da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="be50b-207">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="be50b-208">Una volta installato plug-in di hello, viene visualizzato **utente installato** sezione componenti aggiuntivi di **gestire componenti aggiuntivi** sezione.</span><span class="sxs-lookup"><span data-stu-id="be50b-208">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="be50b-209">Fare clic su **configura** tooconfigure hello nuovo plug-in.</span><span class="sxs-lookup"><span data-stu-id="be50b-209">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="be50b-210">Seguire questa procedura nella pagina di configurazione:</span><span class="sxs-lookup"><span data-stu-id="be50b-210">Perform following steps on configuration page:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="be50b-212">a.</span><span class="sxs-lookup"><span data-stu-id="be50b-212">a.</span></span> <span data-ttu-id="be50b-213">In **URL dei metadati** incollare hello **URL dei metadati** generato da Azure AD e fare clic su hello **risolvere** pulsante.</span><span class="sxs-lookup"><span data-stu-id="be50b-213">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="be50b-214">Legge l'URL dei metadati di hello IdP e inseriscono tutte le informazioni di campi di hello.</span><span class="sxs-lookup"><span data-stu-id="be50b-214">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="be50b-215">La posizione predefinita dell'ID utente SAML è nell'identificatore del nome.</span><span class="sxs-lookup"><span data-stu-id="be50b-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="be50b-216">È possibile modificare questa opzione attributo tooan e immettere il nome di attributo appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="be50b-216">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="be50b-217">Verificare che sia presente un solo certificato mappato a app hello in modo che non si verificano errori per la risoluzione dei metadati hello.</span><span class="sxs-lookup"><span data-stu-id="be50b-217">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="be50b-218">Se sono presenti più certificati, alla risoluzione dei metadati di hello, l'amministratore riceve un errore.</span><span class="sxs-lookup"><span data-stu-id="be50b-218">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="be50b-219">b.</span><span class="sxs-lookup"><span data-stu-id="be50b-219">b.</span></span> <span data-ttu-id="be50b-220">Hello copia **identificatore, l'URL di risposta e l'URL di accesso** valori e incollarli in **identificatore, l'URL di risposta e l'URL di accesso** in rispettivamente nelle caselle di testo **JIRA SAML SSO URLediMicrosoftDomain** sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="be50b-220">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="be50b-221">c.</span><span class="sxs-lookup"><span data-stu-id="be50b-221">c.</span></span> <span data-ttu-id="be50b-222">In **nome pulsante di accesso** nome hello del tipo di pulsante l'organizzazione vuole hello utenti toosee nella schermata di accesso.</span><span class="sxs-lookup"><span data-stu-id="be50b-222">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="be50b-223">d.</span><span class="sxs-lookup"><span data-stu-id="be50b-223">d.</span></span> <span data-ttu-id="be50b-224">In **percorsi di ID utente SAML** selezionare **è l'ID utente nell'elemento NameIdentifier hello di hello Subject statement** o **ID utente è in un elemento attributo**.</span><span class="sxs-lookup"><span data-stu-id="be50b-224">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="be50b-225">Questo ID è l'id utente hello JIRA toobe. Se non trova corrispondenza id utente hello, sistema non consentirà toolog gli utenti in.</span><span class="sxs-lookup"><span data-stu-id="be50b-225">This ID has toobe hello JIRA user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="be50b-226">e.</span><span class="sxs-lookup"><span data-stu-id="be50b-226">e.</span></span> <span data-ttu-id="be50b-227">Se si seleziona **ID utente è in un elemento attributo** opzione, quindi nella **nome dell'attributo** nome hello di tipo casella di testo dell'attributo hello è previsto l'Id utente.</span><span class="sxs-lookup"><span data-stu-id="be50b-227">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="be50b-228">f.</span><span class="sxs-lookup"><span data-stu-id="be50b-228">f.</span></span> <span data-ttu-id="be50b-229">Se si utilizza dominio federato di hello (ad esempio, ecc. ad FS) con Azure AD, fare clic su hello **abilitare Home Realm Discovery** opzione e configurare hello **nome di dominio**.</span><span class="sxs-lookup"><span data-stu-id="be50b-229">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="be50b-230">g.</span><span class="sxs-lookup"><span data-stu-id="be50b-230">g.</span></span> <span data-ttu-id="be50b-231">In **nome di dominio** tipo hello nome di dominio qui in caso di accesso basato su ADFS hello.</span><span class="sxs-lookup"><span data-stu-id="be50b-231">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="be50b-232">h.</span><span class="sxs-lookup"><span data-stu-id="be50b-232">h.</span></span> <span data-ttu-id="be50b-233">Controllare **abilitare Single Sign-out** se si desidera toolog fuori da Azure AD quando un utente si disconnette da JIRA.</span><span class="sxs-lookup"><span data-stu-id="be50b-233">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="be50b-234">i.</span><span class="sxs-lookup"><span data-stu-id="be50b-234">i.</span></span> <span data-ttu-id="be50b-235">Fare clic su **salvare** pulsante Impostazioni hello toosave.</span><span class="sxs-lookup"><span data-stu-id="be50b-235">Click **Save** button toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="be50b-236">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="be50b-236">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="be50b-237">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="be50b-237">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="be50b-238">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="be50b-238">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="be50b-239">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="be50b-239">Creating an Azure AD test user</span></span>
<span data-ttu-id="be50b-240">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="be50b-240">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="be50b-242">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="be50b-242">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="be50b-243">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="be50b-243">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="be50b-245">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="be50b-245">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="be50b-247">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="be50b-247">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="be50b-249">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="be50b-249">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="be50b-251">a.</span><span class="sxs-lookup"><span data-stu-id="be50b-251">a.</span></span> <span data-ttu-id="be50b-252">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="be50b-252">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="be50b-253">b.</span><span class="sxs-lookup"><span data-stu-id="be50b-253">b.</span></span> <span data-ttu-id="be50b-254">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="be50b-254">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="be50b-255">c.</span><span class="sxs-lookup"><span data-stu-id="be50b-255">c.</span></span> <span data-ttu-id="be50b-256">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="be50b-256">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="be50b-257">d.</span><span class="sxs-lookup"><span data-stu-id="be50b-257">d.</span></span> <span data-ttu-id="be50b-258">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="be50b-258">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="be50b-259">Creazione di un utente test di JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="be50b-259">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="be50b-260">toolog agli utenti di Azure AD tooenable in tooJIRA server on-premise, è necessario eseguirne il provisioning in JIRA SAML SSO da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="be50b-260">tooenable Azure AD users toolog in tooJIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="be50b-261">In JIRA SAML SSO by Microsoft il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="be50b-261">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="be50b-262">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="be50b-262">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="be50b-263">Accedi tooyour server on-premise JIRA come amministratore.</span><span class="sxs-lookup"><span data-stu-id="be50b-263">Log in tooyour JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="be50b-264">Passare il mouse su ruota dentata e scegliere hello **Gestione utenti**.</span><span class="sxs-lookup"><span data-stu-id="be50b-264">Hover on cog and click hello **User management**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="be50b-266">Si è reindirizzato tooAdministrator accesso pagina tooenter **Password** e fare clic su **conferma** pulsante.</span><span class="sxs-lookup"><span data-stu-id="be50b-266">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="be50b-268">Nella sezione della scheda **User management** (Gestione utenti) fare clic su **Create user** (Crea utente).</span><span class="sxs-lookup"><span data-stu-id="be50b-268">Under **User management** tab section, click **create user**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="be50b-270">In hello **"Create new user"** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="be50b-270">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="be50b-272">a.</span><span class="sxs-lookup"><span data-stu-id="be50b-272">a.</span></span> <span data-ttu-id="be50b-273">In hello **indirizzo di posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="be50b-273">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="be50b-274">b.</span><span class="sxs-lookup"><span data-stu-id="be50b-274">b.</span></span> <span data-ttu-id="be50b-275">In hello **nome completo** casella di testo, nome completo del tipo di utente hello come Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="be50b-275">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="be50b-276">c.</span><span class="sxs-lookup"><span data-stu-id="be50b-276">c.</span></span> <span data-ttu-id="be50b-277">In hello **Username** casella Tipo hello email dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="be50b-277">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="be50b-278">d.</span><span class="sxs-lookup"><span data-stu-id="be50b-278">d.</span></span> <span data-ttu-id="be50b-279">In hello **Password** casella di testo, digitare la password dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="be50b-279">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="be50b-280">e.</span><span class="sxs-lookup"><span data-stu-id="be50b-280">e.</span></span> <span data-ttu-id="be50b-281">Fare clic su **Create User** (Crea utente).</span><span class="sxs-lookup"><span data-stu-id="be50b-281">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="be50b-282">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="be50b-282">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="be50b-283">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooJIRA SAML SSO da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="be50b-283">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJIRA SAML SSO by Microsoft.</span></span>

![Assegna utente][200] 

<span data-ttu-id="be50b-285">**tooassign Britta Simon tooJIRA SAML SSO da Microsoft, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="be50b-285">**tooassign Britta Simon tooJIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="be50b-286">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="be50b-286">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="be50b-288">Nell'elenco di applicazioni hello, selezionare **JIRA SAML SSO da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="be50b-288">In hello applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="be50b-290">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="be50b-290">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="be50b-292">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="be50b-292">Click **Add** button.</span></span> <span data-ttu-id="be50b-293">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="be50b-293">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="be50b-295">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="be50b-295">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="be50b-296">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="be50b-296">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="be50b-297">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="be50b-297">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="be50b-298">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="be50b-298">Testing single sign-on</span></span>

<span data-ttu-id="be50b-299">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="be50b-299">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="be50b-300">Quando si fa clic hello JIRA SAML SSO dal riquadro Microsoft nel Pannello di accesso hello, è necessario ottenere automaticamente firmato in tooyour JIRA SAML SSO dall'applicazione di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="be50b-300">When you click hello JIRA SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="be50b-301">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="be50b-301">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="be50b-302">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="be50b-302">Additional resources</span></span>

* [<span data-ttu-id="be50b-303">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be50b-303">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="be50b-304">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be50b-304">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

