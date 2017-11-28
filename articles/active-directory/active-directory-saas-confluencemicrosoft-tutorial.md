---
title: 'Esercitazione: integrazione di Azure Active Directory con Confluence SAML SSO by Microsoft | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e confluenza SAML SSO da Microsoft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ace23800e3908c8125052b4a2edcaae71f19935d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a><span data-ttu-id="460e5-103">Esercitazione: Integrazione di Azure Active Directory con Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="460e5-103">Tutorial: Azure Active Directory integration with Confluence SAML SSO by Microsoft</span></span>

<span data-ttu-id="460e5-104">In questa esercitazione, è illustrato come toointegrate confluenza SAML SSO da Microsoft con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="460e5-104">In this tutorial, you learn how toointegrate Confluence SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="460e5-105">Integrazione confluenza SAML SSO da Microsoft Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="460e5-105">Integrating Confluence SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="460e5-106">È possibile controllare in Azure AD che ha accesso tooConfluence SAML SSO da Microsoft</span><span class="sxs-lookup"><span data-stu-id="460e5-106">You can control in Azure AD who has access tooConfluence SAML SSO by Microsoft</span></span>
- <span data-ttu-id="460e5-107">È possibile abilitare l'utenti tooautomatically get connesso tooConfluence SAML SSO da Microsoft (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="460e5-107">You can enable your users tooautomatically get signed-on tooConfluence SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="460e5-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="460e5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="460e5-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="460e5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="460e5-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="460e5-110">Prerequisites</span></span>

<span data-ttu-id="460e5-111">tooconfigure integrazione di Azure AD con confluenza SAML SSO da Microsoft, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="460e5-111">tooconfigure Azure AD integration with Confluence SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="460e5-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="460e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="460e5-113">Applicazione server confluenza installato in un server di Windows a 64 bit (in locale o nel cloud hello infrastruttura IaaS)</span><span class="sxs-lookup"><span data-stu-id="460e5-113">Confluence server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="460e5-114">Server Confluence abilitato per HTTPS</span><span class="sxs-lookup"><span data-stu-id="460e5-114">Confluence server is HTTPS enabled</span></span>
- <span data-ttu-id="460e5-115">Nota hello è supportato nelle versioni del plug-in confluenza indicate nella seguente sezione.</span><span class="sxs-lookup"><span data-stu-id="460e5-115">Note hello supported versions for Confluence Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="460e5-116">Confluenza server sia raggiungibile nella rete internet particolarmente tooAzure AD account di accesso di pagina per l'autenticazione e deve tooreceive in grado di hello token da Azure AD</span><span class="sxs-lookup"><span data-stu-id="460e5-116">Confluence server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="460e5-117">Credenziali di amministratore configurate in Confluence</span><span class="sxs-lookup"><span data-stu-id="460e5-117">Admin credentials are set up in Confluence</span></span>
- <span data-ttu-id="460e5-118">WebSudo disabilitato in Confluence</span><span class="sxs-lookup"><span data-stu-id="460e5-118">WebSudo is disabled in Confluence</span></span>
- <span data-ttu-id="460e5-119">Utente creato nel hello applicazione server confluenza di test</span><span class="sxs-lookup"><span data-stu-id="460e5-119">Test user created in hello Confluence server application</span></span>

> [!NOTE]
> <span data-ttu-id="460e5-120">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione di confluenza.</span><span class="sxs-lookup"><span data-stu-id="460e5-120">tootest hello steps in this tutorial, we do not recommend using a production environment of Confluence.</span></span> <span data-ttu-id="460e5-121">Prima di tutto testare integrazione hello nello sviluppo e gestione temporanea di ambiente dell'applicazione hello e quindi utilizzare hello ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="460e5-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="460e5-122">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="460e5-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="460e5-123">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="460e5-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="460e5-124">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="460e5-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-confluence"></a><span data-ttu-id="460e5-125">Versioni di Confluence supportate</span><span class="sxs-lookup"><span data-stu-id="460e5-125">Supported versions of Confluence</span></span> 

<span data-ttu-id="460e5-126">A tutt'oggi sono supportate le versioni seguenti di Confluence:</span><span class="sxs-lookup"><span data-stu-id="460e5-126">As of now, following versions of Confluence are supported:</span></span>

- <span data-ttu-id="460e5-127">Confluenza: too5.10 5.0</span><span class="sxs-lookup"><span data-stu-id="460e5-127">Confluence: 5.0 too5.10</span></span>

## <a name="scenario-description"></a><span data-ttu-id="460e5-128">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="460e5-128">Scenario description</span></span>
<span data-ttu-id="460e5-129">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="460e5-129">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="460e5-130">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="460e5-130">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="460e5-131">Aggiunta di confluenza SAML SSO da Microsoft dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="460e5-131">Adding Confluence SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="460e5-132">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="460e5-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-confluence-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="460e5-133">Aggiunta di confluenza SAML SSO da Microsoft dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="460e5-133">Adding Confluence SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="460e5-134">integrazione hello tooconfigure di confluenza SAML SSO da Microsoft in Azure AD, è necessario tooadd confluenza SAML SSO da Microsoft dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="460e5-134">tooconfigure hello integration of Confluence SAML SSO by Microsoft into Azure AD, you need tooadd Confluence SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="460e5-135">**tooadd confluenza SAML SSO da Microsoft dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="460e5-135">**tooadd Confluence SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="460e5-136">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="460e5-136">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="460e5-138">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="460e5-138">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="460e5-139">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="460e5-139">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="460e5-141">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="460e5-141">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="460e5-143">Nella casella di ricerca hello, digitare **confluenza SAML SSO da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="460e5-143">In hello search box, type **Confluence SAML SSO by Microsoft**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

5. <span data-ttu-id="460e5-145">Nel riquadro dei risultati hello, selezionare **confluenza SAML SSO da Microsoft**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="460e5-145">In hello results panel, select **Confluence SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="460e5-147">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="460e5-147">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="460e5-148">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Confluence SAML SSO by Microsoft mediante un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="460e5-148">In this section, you configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="460e5-149">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in confluenza SAML SSO da Microsoft è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="460e5-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Confluence SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="460e5-150">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in confluenza SAML SSO da Microsoft richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="460e5-150">In other words, a link relationship between an Azure AD user and hello related user in Confluence SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="460e5-151">In confluenza SAML SSO da Microsoft, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="460e5-151">In Confluence SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="460e5-152">tooconfigure e prova AD Azure single sign-on con confluenza SAML SSO da Microsoft, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="460e5-152">tooconfigure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="460e5-153">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="460e5-153">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="460e5-154">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="460e5-154">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="460e5-155">**[Creare una confluenza SAML SSO dall'utente di prova Microsoft](#creating-a-confluence-saml-sso-by-microsoft-test-user)**  -toohave un equivalente di Britta Simon confluenza SAML SSO da Microsoft che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="460e5-155">**[Creating a Confluence SAML SSO by Microsoft test user](#creating-a-confluence-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in Confluence SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="460e5-156">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="460e5-156">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="460e5-157">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="460e5-157">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="460e5-158">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="460e5-158">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="460e5-159">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare single sign-on nella confluenza SAML SSO dall'applicazione di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="460e5-159">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Confluence SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="460e5-160">**tooconfigure AD Azure single sign-on con confluenza SAML SSO da Microsoft, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="460e5-160">**tooconfigure Azure AD single sign-on with Confluence SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="460e5-161">Nel portale di Azure su hello hello **confluenza SAML SSO da Microsoft** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="460e5-161">In hello Azure portal, on hello **Confluence SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="460e5-163">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="460e5-163">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

3. <span data-ttu-id="460e5-165">In hello **confluenza SAML SSO URL e di Microsoft Domain** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="460e5-165">On hello **Confluence SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    <span data-ttu-id="460e5-167">a.</span><span class="sxs-lookup"><span data-stu-id="460e5-167">a.</span></span> <span data-ttu-id="460e5-168">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="460e5-168">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="460e5-169">b.</span><span class="sxs-lookup"><span data-stu-id="460e5-169">b.</span></span> <span data-ttu-id="460e5-170">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="460e5-170">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="460e5-171">c.</span><span class="sxs-lookup"><span data-stu-id="460e5-171">c.</span></span> <span data-ttu-id="460e5-172">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="460e5-172">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="460e5-173">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="460e5-173">These values are not real.</span></span> <span data-ttu-id="460e5-174">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="460e5-174">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="460e5-175">La porta è facoltativa nel caso di un URL denominato.</span><span class="sxs-lookup"><span data-stu-id="460e5-175">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="460e5-176">Questi valori vengono ricevuti durante la configurazione del plug-in confluenza, illustrato più avanti nell'esercitazione di hello hello.</span><span class="sxs-lookup"><span data-stu-id="460e5-176">These values are received during hello configuration of Confluence plugin, which is explained later in hello tutorial.</span></span>
 

4. <span data-ttu-id="460e5-177">hello toogenerate **metadati** url, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="460e5-177">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="460e5-178">a.</span><span class="sxs-lookup"><span data-stu-id="460e5-178">a.</span></span> <span data-ttu-id="460e5-179">Fare clic su **Registrazioni per l'app**.</span><span class="sxs-lookup"><span data-stu-id="460e5-179">Click **App registrations**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="460e5-181">b.</span><span class="sxs-lookup"><span data-stu-id="460e5-181">b.</span></span> <span data-ttu-id="460e5-182">Fare clic su **endpoint** tooopen **endpoint** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="460e5-182">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="460e5-184">c.</span><span class="sxs-lookup"><span data-stu-id="460e5-184">c.</span></span> <span data-ttu-id="460e5-185">Fare clic su hello copia pulsante toocopy **documento metadati federazione** url e incollarlo nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="460e5-185">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="460e5-187">d.</span><span class="sxs-lookup"><span data-stu-id="460e5-187">d.</span></span> <span data-ttu-id="460e5-188">Ora passare toohello pagina delle proprietà di **confluenza SAML SSO da Microsoft** e hello copia **Id applicazione** utilizzando **copia** pulsante e incollarlo nel blocco note.</span><span class="sxs-lookup"><span data-stu-id="460e5-188">Now go toohello property page of **Confluence SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/appid.png)

    <span data-ttu-id="460e5-190">e.</span><span class="sxs-lookup"><span data-stu-id="460e5-190">e.</span></span> <span data-ttu-id="460e5-191">Generare hello **URL dei metadati** utilizzando hello seguente motivo: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` e copiare il valore nel blocco note come viene utilizzato in un secondo momento per la configurazione di hello del plug-in hello.</span><span class="sxs-lookup"><span data-stu-id="460e5-191">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="460e5-192">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="460e5-192">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="460e5-194">Contatto [Microsoft](mailto:waadpartners@microsoft.com) con le seguenti informazioni per i plug-in di hello confluenza hello.</span><span class="sxs-lookup"><span data-stu-id="460e5-194">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello Confluence plugin.</span></span>
    
    *   <span data-ttu-id="460e5-195">Nome del cliente:</span><span class="sxs-lookup"><span data-stu-id="460e5-195">Customer Name:</span></span>
    *   <span data-ttu-id="460e5-196">Nome del dominio primario:</span><span class="sxs-lookup"><span data-stu-id="460e5-196">Primary domain name:</span></span>
    *   <span data-ttu-id="460e5-197">Azure AD Premium: Sì/No (plug-in è disponibile tooall hello cliente gratuito, Basic e SKU Premium)</span><span class="sxs-lookup"><span data-stu-id="460e5-197">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="460e5-198">Numero di utenti che useranno questa integrazione:</span><span class="sxs-lookup"><span data-stu-id="460e5-198">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="460e5-199">Versione Confluence:</span><span class="sxs-lookup"><span data-stu-id="460e5-199">Confluence Version:</span></span>
    *   <span data-ttu-id="460e5-200">Commenti:</span><span class="sxs-lookup"><span data-stu-id="460e5-200">Comments:</span></span>

7. <span data-ttu-id="460e5-201">In una finestra del web browser, accedere come amministratore nell'istanza confluenza tooyour.</span><span class="sxs-lookup"><span data-stu-id="460e5-201">In a different web browser window, log in tooyour Confluence instance as an administrator.</span></span>

8. <span data-ttu-id="460e5-202">Passare il mouse su ruota dentata e scegliere hello **componenti aggiuntivi**.</span><span class="sxs-lookup"><span data-stu-id="460e5-202">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="460e5-204">Nella sezione della scheda Add-ons (Componenti aggiuntivi) fare clic su **Manage add-ons** (Gestisci componenti aggiuntivi).</span><span class="sxs-lookup"><span data-stu-id="460e5-204">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon72.png)

10. <span data-ttu-id="460e5-206">Caricare manualmente i plug-in hello fornito da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="460e5-206">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="460e5-207">Una volta installato plug-in di hello, viene visualizzato **utente installato** sezione componenti aggiuntivi di **gestire componenti aggiuntivi** sezione.</span><span class="sxs-lookup"><span data-stu-id="460e5-207">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="460e5-208">Fare clic su **configura** tooconfigure hello nuovo plug-in.</span><span class="sxs-lookup"><span data-stu-id="460e5-208">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="460e5-209">Seguire questa procedura nella pagina di configurazione:</span><span class="sxs-lookup"><span data-stu-id="460e5-209">Perform following steps on configuration page:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="460e5-211">a.</span><span class="sxs-lookup"><span data-stu-id="460e5-211">a.</span></span> <span data-ttu-id="460e5-212">In **URL dei metadati** incollare hello **URL dei metadati** generato da Azure AD e fare clic su hello **risolvere** pulsante.</span><span class="sxs-lookup"><span data-stu-id="460e5-212">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="460e5-213">Legge l'URL dei metadati di hello IdP e inseriscono tutte le informazioni di campi di hello.</span><span class="sxs-lookup"><span data-stu-id="460e5-213">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="460e5-214">La posizione predefinita dell'ID utente SAML è nell'identificatore del nome.</span><span class="sxs-lookup"><span data-stu-id="460e5-214">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="460e5-215">È possibile modificare questa opzione attributo tooan e immettere il nome di attributo appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="460e5-215">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="460e5-216">Verificare che sia presente un solo certificato mappato a app hello in modo che non si verificano errori per la risoluzione dei metadati hello.</span><span class="sxs-lookup"><span data-stu-id="460e5-216">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="460e5-217">Se sono presenti più certificati, alla risoluzione dei metadati di hello, l'amministratore riceve un errore.</span><span class="sxs-lookup"><span data-stu-id="460e5-217">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="460e5-218">b.</span><span class="sxs-lookup"><span data-stu-id="460e5-218">b.</span></span> <span data-ttu-id="460e5-219">Hello copia **identificatore, l'URL di risposta e l'URL di accesso** valori e incollarli in **identificatore, l'URL di risposta e l'URL di accesso** in rispettivamente nelle caselle di testo **confluenza SAML SSO URL e di Microsoft Domain**  sezione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="460e5-219">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **Confluence SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="460e5-220">c.</span><span class="sxs-lookup"><span data-stu-id="460e5-220">c.</span></span> <span data-ttu-id="460e5-221">In **nome pulsante di accesso** nome hello del tipo di pulsante l'organizzazione vuole hello utenti toosee nella schermata di accesso.</span><span class="sxs-lookup"><span data-stu-id="460e5-221">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="460e5-222">d.</span><span class="sxs-lookup"><span data-stu-id="460e5-222">d.</span></span> <span data-ttu-id="460e5-223">In **percorsi di ID utente SAML** selezionare **è l'ID utente nell'elemento NameIdentifier hello di hello Subject statement** o **ID utente è in un elemento attributo**.</span><span class="sxs-lookup"><span data-stu-id="460e5-223">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="460e5-224">Questo ID è l'id utente confluenza di toobe hello. Se non trova corrispondenza id utente hello, sistema non consentirà toolog gli utenti in.</span><span class="sxs-lookup"><span data-stu-id="460e5-224">This ID has toobe hello Confluence user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="460e5-225">e.</span><span class="sxs-lookup"><span data-stu-id="460e5-225">e.</span></span> <span data-ttu-id="460e5-226">Se si seleziona **ID utente è in un elemento attributo** opzione, quindi nella **nome dell'attributo** nome hello di tipo casella di testo dell'attributo hello è previsto l'Id utente.</span><span class="sxs-lookup"><span data-stu-id="460e5-226">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="460e5-227">f.</span><span class="sxs-lookup"><span data-stu-id="460e5-227">f.</span></span> <span data-ttu-id="460e5-228">Se si utilizza dominio federato di hello (ad esempio, ecc. ad FS) con Azure AD, fare clic su hello **abilitare Home Realm Discovery** opzione e configurare hello **nome di dominio**.</span><span class="sxs-lookup"><span data-stu-id="460e5-228">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="460e5-229">g.</span><span class="sxs-lookup"><span data-stu-id="460e5-229">g.</span></span> <span data-ttu-id="460e5-230">In **nome di dominio** tipo hello nome di dominio qui in caso di accesso basato su ADFS hello.</span><span class="sxs-lookup"><span data-stu-id="460e5-230">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="460e5-231">h.</span><span class="sxs-lookup"><span data-stu-id="460e5-231">h.</span></span> <span data-ttu-id="460e5-232">Controllare **abilitare Single Sign-out** se si desidera toolog fuori da Azure AD quando un utente si disconnette da confluenza.</span><span class="sxs-lookup"><span data-stu-id="460e5-232">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from Confluence.</span></span> 

    <span data-ttu-id="460e5-233">i.</span><span class="sxs-lookup"><span data-stu-id="460e5-233">i.</span></span> <span data-ttu-id="460e5-234">Fare clic su **salvare** pulsante Impostazioni hello toosave.</span><span class="sxs-lookup"><span data-stu-id="460e5-234">Click **Save** button toosave hello settings.</span></span>


> [!TIP]
> <span data-ttu-id="460e5-235">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="460e5-235">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="460e5-236">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="460e5-236">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="460e5-237">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="460e5-237">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="460e5-238">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="460e5-238">Creating an Azure AD test user</span></span>
<span data-ttu-id="460e5-239">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="460e5-239">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="460e5-241">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="460e5-241">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="460e5-242">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="460e5-242">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="460e5-244">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="460e5-244">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="460e5-246">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="460e5-246">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="460e5-248">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="460e5-248">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="460e5-250">a.</span><span class="sxs-lookup"><span data-stu-id="460e5-250">a.</span></span> <span data-ttu-id="460e5-251">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="460e5-251">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="460e5-252">b.</span><span class="sxs-lookup"><span data-stu-id="460e5-252">b.</span></span> <span data-ttu-id="460e5-253">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="460e5-253">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="460e5-254">c.</span><span class="sxs-lookup"><span data-stu-id="460e5-254">c.</span></span> <span data-ttu-id="460e5-255">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="460e5-255">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="460e5-256">d.</span><span class="sxs-lookup"><span data-stu-id="460e5-256">d.</span></span> <span data-ttu-id="460e5-257">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="460e5-257">Click **Create**.</span></span>
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="460e5-258">Creazione di un utente di test di Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="460e5-258">Creating a Confluence SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="460e5-259">toolog agli utenti di Azure AD tooenable in tooConfluence nel server locale, è necessario eseguirne il provisioning in confluenza SAML SSO da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="460e5-259">tooenable Azure AD users toolog in tooConfluence on premise server, they must be provisioned into Confluence SAML SSO by Microsoft.</span></span> <span data-ttu-id="460e5-260">In Confluence SAML SSO by Microsoft il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="460e5-260">For Confluence SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="460e5-261">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="460e5-261">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="460e5-262">Accedere come amministratore tooyour confluenza nel server locale.</span><span class="sxs-lookup"><span data-stu-id="460e5-262">Log in tooyour Confluence on premise server as an administrator.</span></span>

2. <span data-ttu-id="460e5-263">Passare il mouse su ruota dentata e scegliere hello **Gestione utenti**.</span><span class="sxs-lookup"><span data-stu-id="460e5-263">Hover on cog and click hello **User management**.</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-confluencemicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="460e5-265">Nella sezione Users (Utenti) fare clic sula scheda **Add users** (Aggiungi utenti). In hello **"Aggiungi utente"** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="460e5-265">Under Users section, click **Add users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Aggiungere un dipendente](./media/active-directory-saas-confluencemicrosoft-tutorial/user2.png) 

    <span data-ttu-id="460e5-267">a.</span><span class="sxs-lookup"><span data-stu-id="460e5-267">a.</span></span> <span data-ttu-id="460e5-268">In hello **Username** casella di testo, posta elettronica hello tipo di utente come Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="460e5-268">In hello **Username** textbox, type hello email of user like Britta Simon.</span></span>

    <span data-ttu-id="460e5-269">b.</span><span class="sxs-lookup"><span data-stu-id="460e5-269">b.</span></span> <span data-ttu-id="460e5-270">In hello **nome completo** casella di testo, nome completo del tipo hello dell'utente come Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="460e5-270">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="460e5-271">c.</span><span class="sxs-lookup"><span data-stu-id="460e5-271">c.</span></span> <span data-ttu-id="460e5-272">In hello **posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="460e5-272">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="460e5-273">d.</span><span class="sxs-lookup"><span data-stu-id="460e5-273">d.</span></span> <span data-ttu-id="460e5-274">In hello **Password** casella di testo, digitare la password per Britta Simon hello.</span><span class="sxs-lookup"><span data-stu-id="460e5-274">In hello **Password** textbox, type hello password for Britta Simon.</span></span>

    <span data-ttu-id="460e5-275">e.</span><span class="sxs-lookup"><span data-stu-id="460e5-275">e.</span></span> <span data-ttu-id="460e5-276">Fare clic su **Conferma Password** digitare nuovamente la password di hello.</span><span class="sxs-lookup"><span data-stu-id="460e5-276">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="460e5-277">f.</span><span class="sxs-lookup"><span data-stu-id="460e5-277">f.</span></span> <span data-ttu-id="460e5-278">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="460e5-278">Click **Add** button.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="460e5-279">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="460e5-279">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="460e5-280">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooConfluence SAML SSO da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="460e5-280">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConfluence SAML SSO by Microsoft.</span></span>

![Assegna utente][200] 

<span data-ttu-id="460e5-282">**tooassign Britta Simon tooConfluence SAML SSO da Microsoft, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="460e5-282">**tooassign Britta Simon tooConfluence SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="460e5-283">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="460e5-283">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="460e5-285">Nell'elenco di applicazioni hello, selezionare **confluenza SAML SSO da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="460e5-285">In hello applications list, select **Confluence SAML SSO by Microsoft**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

3. <span data-ttu-id="460e5-287">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="460e5-287">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="460e5-289">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="460e5-289">Click **Add** button.</span></span> <span data-ttu-id="460e5-290">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="460e5-290">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="460e5-292">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="460e5-292">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="460e5-293">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="460e5-293">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="460e5-294">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="460e5-294">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="460e5-295">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="460e5-295">Testing single sign-on</span></span>

<span data-ttu-id="460e5-296">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="460e5-296">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="460e5-297">Quando si fa clic hello confluenza SAML SSO dal riquadro Microsoft nel Pannello di accesso hello, è necessario ottenere automaticamente firmato in tooyour confluenza SAML SSO dall'applicazione di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="460e5-297">When you click hello Confluence SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour Confluence SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="460e5-298">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="460e5-298">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="460e5-299">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="460e5-299">Additional resources</span></span>

* [<span data-ttu-id="460e5-300">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="460e5-300">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="460e5-301">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="460e5-301">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_203.png

