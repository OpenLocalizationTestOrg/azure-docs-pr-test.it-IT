---
title: 'Esercitazione: Integrazione di Azure Active Directory con EverBridge | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed EverBridge.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a260298279407ed709bc2e685a104410f9836a74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="d0f35-103">Esercitazione: Integrazione di Azure Active Directory con EverBridge</span><span class="sxs-lookup"><span data-stu-id="d0f35-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="d0f35-104">In questa esercitazione, è illustrato come toointegrate EverBridge con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0f35-104">In this tutorial, you learn how toointegrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0f35-105">Integrazione EverBridge con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d0f35-105">Integrating EverBridge with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d0f35-106">È possibile controllare in Azure AD che ha accesso tooEverBridge</span><span class="sxs-lookup"><span data-stu-id="d0f35-106">You can control in Azure AD who has access tooEverBridge</span></span>
- <span data-ttu-id="d0f35-107">È possibile abilitare l'utenti tooautomatically get connesso tooEverBridge (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0f35-107">You can enable your users tooautomatically get signed-on tooEverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d0f35-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d0f35-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d0f35-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0f35-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0f35-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d0f35-110">Prerequisites</span></span>

<span data-ttu-id="d0f35-111">integrazione di Azure AD con EverBridge tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d0f35-111">tooconfigure Azure AD integration with EverBridge, you need hello following items:</span></span>

- <span data-ttu-id="d0f35-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0f35-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0f35-113">Sottoscrizione di EverBridge abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d0f35-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0f35-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d0f35-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0f35-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="d0f35-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0f35-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="d0f35-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0f35-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0f35-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0f35-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="d0f35-118">Scenario description</span></span>
<span data-ttu-id="d0f35-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="d0f35-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0f35-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="d0f35-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0f35-121">Aggiunta di EverBridge dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d0f35-121">Adding EverBridge from hello gallery</span></span>
2. <span data-ttu-id="d0f35-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0f35-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-hello-gallery"></a><span data-ttu-id="d0f35-123">Aggiunta di EverBridge dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="d0f35-123">Adding EverBridge from hello gallery</span></span>
<span data-ttu-id="d0f35-124">integrazione hello tooconfigure di EverBridge in Azure AD, è necessario tooadd EverBridge dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="d0f35-124">tooconfigure hello integration of EverBridge into Azure AD, you need tooadd EverBridge from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d0f35-125">**tooadd EverBridge dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d0f35-125">**tooadd EverBridge from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0f35-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d0f35-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d0f35-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d0f35-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="d0f35-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="d0f35-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="d0f35-133">Nella casella di ricerca hello, digitare **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-133">In hello search box, type **EverBridge**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. <span data-ttu-id="d0f35-135">Nel riquadro dei risultati hello, selezionare **EverBridge**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d0f35-135">In hello results panel, select **EverBridge**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d0f35-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0f35-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d0f35-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con EverBridge mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d0f35-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d0f35-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in EverBridge è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0f35-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EverBridge is tooa user in Azure AD.</span></span> <span data-ttu-id="d0f35-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in EverBridge deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="d0f35-140">In other words, a link relationship between an Azure AD user and hello related user in EverBridge needs toobe established.</span></span>

<span data-ttu-id="d0f35-141">In EverBridge, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="d0f35-141">In EverBridge, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d0f35-142">tooconfigure e prova AD Azure single sign-on con EverBridge, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="d0f35-142">tooconfigure and test Azure AD single sign-on with EverBridge, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d0f35-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d0f35-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d0f35-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0f35-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d0f35-145">**[Creazione di un utente test EverBridge](#creating-an-everbridge-test-user)**  -toohave un equivalente di Britta Simon in EverBridge che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d0f35-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - toohave a counterpart of Britta Simon in EverBridge that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d0f35-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d0f35-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d0f35-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="d0f35-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d0f35-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0f35-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d0f35-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione EverBridge.</span><span class="sxs-lookup"><span data-stu-id="d0f35-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="d0f35-150">**Azure AD tooconfigure single sign-on con EverBridge, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d0f35-150">**tooconfigure Azure AD single sign-on with EverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0f35-151">Nel portale di Azure su hello hello **EverBridge** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-151">In hello Azure portal, on hello **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="d0f35-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d0f35-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. <span data-ttu-id="d0f35-155">In hello **EverBridge dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d0f35-155">On hello **EverBridge Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="d0f35-157">a.</span><span class="sxs-lookup"><span data-stu-id="d0f35-157">a.</span></span> <span data-ttu-id="d0f35-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="d0f35-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="d0f35-159">b.</span><span class="sxs-lookup"><span data-stu-id="d0f35-159">b.</span></span> <span data-ttu-id="d0f35-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="d0f35-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d0f35-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="d0f35-161">These values are not real.</span></span> <span data-ttu-id="d0f35-162">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="d0f35-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="d0f35-163">Contatto [team di supporto EverBridge](mailto:support@everbridge.com) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="d0f35-163">Contact [EverBridge support team](mailto:support@everbridge.com) tooget these values.</span></span>
 
4. <span data-ttu-id="d0f35-164">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d0f35-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. <span data-ttu-id="d0f35-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d0f35-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d0f35-168">In hello **EverBridge configurazione** fare clic su **configurare EverBridge** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="d0f35-168">On hello **EverBridge Configuration** section, click **Configure EverBridge** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d0f35-169">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="d0f35-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. <span data-ttu-id="d0f35-171">tooget SSO configurato per l'applicazione, è necessario toosign-on tooyour Everbridge tenant come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d0f35-171">tooget SSO configured for your application, you need toosign-on tooyour Everbridge tenant as an administrator.</span></span>

7. <span data-ttu-id="d0f35-172">Scegliere hello hello menu in alto hello **impostazioni** e selezionare **Single Sign-On** in **sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="d0f35-174">a.</span><span class="sxs-lookup"><span data-stu-id="d0f35-174">a.</span></span> <span data-ttu-id="d0f35-175">In hello **nome** casella di testo, nome del Provider di identificatore di tipo hello (ad esempio: il nome della società).</span><span class="sxs-lookup"><span data-stu-id="d0f35-175">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="d0f35-176">b.</span><span class="sxs-lookup"><span data-stu-id="d0f35-176">b.</span></span> <span data-ttu-id="d0f35-177">In hello **nome API** casella di testo, il nome di tipo hello dell'API.</span><span class="sxs-lookup"><span data-stu-id="d0f35-177">In hello **API Name** textbox, type hello name of API.</span></span>
   
    <span data-ttu-id="d0f35-178">c.</span><span class="sxs-lookup"><span data-stu-id="d0f35-178">c.</span></span> <span data-ttu-id="d0f35-179">Fare clic su **Scegli File** pulsante tooupload hello metadati file scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d0f35-179">Click **Choose File** button tooupload hello metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="d0f35-180">d.</span><span class="sxs-lookup"><span data-stu-id="d0f35-180">d.</span></span> <span data-ttu-id="d0f35-181">In hello posizione identità SAML, selezionare **identità si trova nell'elemento NameIdentifier hello di hello Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-181">In hello SAML Identity Location, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
   
    <span data-ttu-id="d0f35-182">e.</span><span class="sxs-lookup"><span data-stu-id="d0f35-182">e.</span></span> <span data-ttu-id="d0f35-183">In hello **Identity Provider Login URL** casella di testo, incollare hello valore SAML SSO URL da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0f35-183">In hello **Identity Provider Login URL** textbox, paste hello value of SAML SSO URL from Azure AD.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="d0f35-185">f.</span><span class="sxs-lookup"><span data-stu-id="d0f35-185">f.</span></span> <span data-ttu-id="d0f35-186">In hello Service Provider Initiated Request Binding, selezionare **reindirizzamento HTTP**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-186">In hello Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="d0f35-187">g.</span><span class="sxs-lookup"><span data-stu-id="d0f35-187">g.</span></span> <span data-ttu-id="d0f35-188">Fare clic su **Save**</span><span class="sxs-lookup"><span data-stu-id="d0f35-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="d0f35-189">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="d0f35-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d0f35-190">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="d0f35-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d0f35-191">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d0f35-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d0f35-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0f35-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="d0f35-193">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d0f35-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="d0f35-195">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d0f35-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0f35-196">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="d0f35-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d0f35-198">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d0f35-200">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="d0f35-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d0f35-202">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d0f35-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d0f35-204">a.</span><span class="sxs-lookup"><span data-stu-id="d0f35-204">a.</span></span> <span data-ttu-id="d0f35-205">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0f35-206">b.</span><span class="sxs-lookup"><span data-stu-id="d0f35-206">b.</span></span> <span data-ttu-id="d0f35-207">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d0f35-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d0f35-208">c.</span><span class="sxs-lookup"><span data-stu-id="d0f35-208">c.</span></span> <span data-ttu-id="d0f35-209">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d0f35-210">d.</span><span class="sxs-lookup"><span data-stu-id="d0f35-210">d.</span></span> <span data-ttu-id="d0f35-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="d0f35-212">Creazione di un utente test di EverBridge</span><span class="sxs-lookup"><span data-stu-id="d0f35-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="d0f35-213">In questa sezione viene creato un utente chiamato Britta Simon in Everbridge.</span><span class="sxs-lookup"><span data-stu-id="d0f35-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="d0f35-214">Lavorare con [team di supporto EverBridge](mailto:support@everbridge.com) utenti hello tooadd nella piattaforma Everbridge hello.</span><span class="sxs-lookup"><span data-stu-id="d0f35-214">Work with [EverBridge support team](mailto:support@everbridge.com) tooadd hello users in hello Everbridge platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d0f35-215">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0f35-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d0f35-216">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooEverBridge.</span><span class="sxs-lookup"><span data-stu-id="d0f35-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEverBridge.</span></span>

![Assegna utente][200] 

<span data-ttu-id="d0f35-218">**tooassign Britta Simon tooEverBridge, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="d0f35-218">**tooassign Britta Simon tooEverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0f35-219">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="d0f35-221">Nell'elenco di applicazioni hello, selezionare **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-221">In hello applications list, select **EverBridge**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. <span data-ttu-id="d0f35-223">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="d0f35-225">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-225">Click **Add** button.</span></span> <span data-ttu-id="d0f35-226">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="d0f35-228">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="d0f35-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d0f35-229">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d0f35-230">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="d0f35-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d0f35-231">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="d0f35-231">Testing single sign-on</span></span>

<span data-ttu-id="d0f35-232">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="d0f35-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d0f35-233">Quando si fa clic su riquadro Everbridge hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Everbridge applicazione.</span><span class="sxs-lookup"><span data-stu-id="d0f35-233">When you click hello Everbridge tile in hello Access Panel, you should get automatically signed-on tooyour Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d0f35-234">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="d0f35-234">Additional resources</span></span>

* [<span data-ttu-id="d0f35-235">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0f35-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d0f35-236">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0f35-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

