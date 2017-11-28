---
title: 'Esercitazione: Integrazione di Azure Active Directory con Mozy Enterprise | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Mozy Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: bab0df4f3621b784cd8edfda3c8e10fe5a7ced9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="92b2d-103">Esercitazione: Integrazione di Azure Active Directory con Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="92b2d-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="92b2d-104">In questa esercitazione, è illustrato come toointegrate Mozy Enterprise con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92b2d-104">In this tutorial, you learn how toointegrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92b2d-105">Integrazione di Mozy Enterprise con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="92b2d-105">Integrating Mozy Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="92b2d-106">È possibile controllare in Azure AD che ha accesso tooMozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="92b2d-106">You can control in Azure AD who has access tooMozy Enterprise</span></span>
- <span data-ttu-id="92b2d-107">È possibile abilitare l'utenti tooautomatically get connesso tooMozy Enterprise (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="92b2d-107">You can enable your users tooautomatically get signed-on tooMozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92b2d-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="92b2d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="92b2d-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92b2d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92b2d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="92b2d-110">Prerequisites</span></span>

<span data-ttu-id="92b2d-111">tooconfigure integrazione di Azure AD con Mozy Enterprise, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="92b2d-111">tooconfigure Azure AD integration with Mozy Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="92b2d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92b2d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92b2d-113">Sottoscrizione di Mozy Enterprise abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="92b2d-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92b2d-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="92b2d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92b2d-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="92b2d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92b2d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="92b2d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92b2d-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92b2d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92b2d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="92b2d-118">Scenario description</span></span>
<span data-ttu-id="92b2d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="92b2d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92b2d-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="92b2d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92b2d-121">Aggiunta di Mozy Enterprise dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="92b2d-121">Adding Mozy Enterprise from hello gallery</span></span>
2. <span data-ttu-id="92b2d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="92b2d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-hello-gallery"></a><span data-ttu-id="92b2d-123">Aggiunta di Mozy Enterprise dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="92b2d-123">Adding Mozy Enterprise from hello gallery</span></span>
<span data-ttu-id="92b2d-124">integrazione hello tooconfigure di Mozy Enterprise in Azure AD, è necessario tooadd Mozy Enterprise dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="92b2d-124">tooconfigure hello integration of Mozy Enterprise into Azure AD, you need tooadd Mozy Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="92b2d-125">**tooadd Mozy Enterprise dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="92b2d-125">**tooadd Mozy Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="92b2d-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="92b2d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="92b2d-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="92b2d-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="92b2d-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="92b2d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="92b2d-133">Nella casella di ricerca hello, digitare **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-133">In hello search box, type **Mozy Enterprise**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="92b2d-135">Nel riquadro dei risultati hello, selezionare **Mozy Enterprise**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="92b2d-135">In hello results panel, select **Mozy Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92b2d-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="92b2d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92b2d-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Mozy Enterprise usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="92b2d-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92b2d-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Mozy Enterprise è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92b2d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mozy Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="92b2d-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Mozy Enterprise richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="92b2d-140">In other words, a link relationship between an Azure AD user and hello related user in Mozy Enterprise needs toobe established.</span></span>

<span data-ttu-id="92b2d-141">In Mozy Enterprise, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="92b2d-141">In Mozy Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="92b2d-142">tooconfigure e test Azure single sign-on AD con Mozy Enterprise, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="92b2d-142">tooconfigure and test Azure AD single sign-on with Mozy Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="92b2d-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="92b2d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="92b2d-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92b2d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92b2d-145">**[Creazione di un utente test Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**  -toohave un equivalente di Britta Simon in Mozy Enterprise che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="92b2d-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - toohave a counterpart of Britta Simon in Mozy Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="92b2d-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="92b2d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92b2d-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="92b2d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92b2d-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="92b2d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92b2d-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="92b2d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="92b2d-150">**Azure AD tooconfigure single sign-on con Mozy Enterprise, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="92b2d-150">**tooconfigure Azure AD single sign-on with Mozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="92b2d-151">Nel portale di Azure su hello hello **Mozy Enterprise** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-151">In hello Azure portal, on hello **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="92b2d-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="92b2d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="92b2d-155">In hello **Mozy Enterprise dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="92b2d-155">On hello **Mozy Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="92b2d-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="92b2d-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92b2d-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="92b2d-158">This value is not real.</span></span> <span data-ttu-id="92b2d-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="92b2d-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="92b2d-160">Contatto [team di supporto di Mozy Enterprise Client](http://support.mozy.com/) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="92b2d-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) tooget this value.</span></span>

4. <span data-ttu-id="92b2d-161">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="92b2d-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="92b2d-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="92b2d-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="92b2d-165">In hello **Mozy Enterprise configurazione** fare clic su **configurare Mozy Enterprise** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="92b2d-165">On hello **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="92b2d-166">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="92b2d-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="92b2d-168">In un'altra finestra del Web browser accedere al sito aziendale di Mozy Enterprise come amministratore.</span><span class="sxs-lookup"><span data-stu-id="92b2d-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="92b2d-169">In hello **configurazione** fare clic su **criteri di autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-169">In hello **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="92b2d-170">![Criteri di autenticazione](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Criteri di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="92b2d-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="92b2d-171">In hello **criteri di autenticazione** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="92b2d-171">On hello **Authentication Policy** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="92b2d-172">![Criteri di autenticazione](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Criteri di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="92b2d-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="92b2d-173">a.</span><span class="sxs-lookup"><span data-stu-id="92b2d-173">a.</span></span> <span data-ttu-id="92b2d-174">Selezionare **Directory Service** come **Provider**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="92b2d-175">b.</span><span class="sxs-lookup"><span data-stu-id="92b2d-175">b.</span></span> <span data-ttu-id="92b2d-176">Selezionare **Use LDAP Push**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="92b2d-177">c.</span><span class="sxs-lookup"><span data-stu-id="92b2d-177">c.</span></span> <span data-ttu-id="92b2d-178">Fare clic su hello **SAML Authentication** scheda.</span><span class="sxs-lookup"><span data-stu-id="92b2d-178">Click hello **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="92b2d-179">d.</span><span class="sxs-lookup"><span data-stu-id="92b2d-179">d.</span></span> <span data-ttu-id="92b2d-180">Incolla **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure hello in hello **URL autenticazione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="92b2d-180">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="92b2d-181">e.</span><span class="sxs-lookup"><span data-stu-id="92b2d-181">e.</span></span> <span data-ttu-id="92b2d-182">Incolla **ID entità SAML**, che è stato copiato dal portale di Azure hello in hello **Endpoint SAML** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="92b2d-182">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="92b2d-183">f.</span><span class="sxs-lookup"><span data-stu-id="92b2d-183">f.</span></span> <span data-ttu-id="92b2d-184">Aprire il certificato con codificato base 64 scaricato nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollare hello intero certificato nella **SAML Certificate** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="92b2d-184">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="92b2d-185">g.</span><span class="sxs-lookup"><span data-stu-id="92b2d-185">g.</span></span> <span data-ttu-id="92b2d-186">Selezionare **Enable SSO for Admins toolog with their network credentials**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-186">Select **Enable SSO for Admins toolog in with their network credentials**.</span></span>
   
   <span data-ttu-id="92b2d-187">h.</span><span class="sxs-lookup"><span data-stu-id="92b2d-187">h.</span></span> <span data-ttu-id="92b2d-188">Fare clic su **Salva modifiche**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="92b2d-189">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="92b2d-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="92b2d-190">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="92b2d-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="92b2d-191">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92b2d-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92b2d-192">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="92b2d-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="92b2d-193">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="92b2d-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="92b2d-195">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="92b2d-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="92b2d-196">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="92b2d-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92b2d-198">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92b2d-200">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="92b2d-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92b2d-202">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="92b2d-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92b2d-204">a.</span><span class="sxs-lookup"><span data-stu-id="92b2d-204">a.</span></span> <span data-ttu-id="92b2d-205">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92b2d-206">b.</span><span class="sxs-lookup"><span data-stu-id="92b2d-206">b.</span></span> <span data-ttu-id="92b2d-207">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="92b2d-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92b2d-208">c.</span><span class="sxs-lookup"><span data-stu-id="92b2d-208">c.</span></span> <span data-ttu-id="92b2d-209">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="92b2d-210">d.</span><span class="sxs-lookup"><span data-stu-id="92b2d-210">d.</span></span> <span data-ttu-id="92b2d-211">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="92b2d-212">Creazione di un utente di test di Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="92b2d-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="92b2d-213">In ordine tooenable Azure AD utenti toolog a Mozy Enterprise, è necessario eseguirne il provisioning in Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="92b2d-213">In order tooenable Azure AD users toolog into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="92b2d-214">Nel caso di hello di Mozy Enterprise, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="92b2d-214">In hello case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="92b2d-215">È possibile usare qualsiasi altro Mozy Enterprise utente account strumento di creazione o qualsiasi API fornita da Mozy Enterprise tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="92b2d-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise tooprovision AAD user accounts.</span></span>

<span data-ttu-id="92b2d-216">**eseguire un account utente, tooprovision hello i passaggi seguenti:**</span><span class="sxs-lookup"><span data-stu-id="92b2d-216">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="92b2d-217">Accedi tooyour **Mozy Enterprise** tenant.</span><span class="sxs-lookup"><span data-stu-id="92b2d-217">Log in tooyour **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="92b2d-218">Fare clic su **Users** (Utenti) e quindi fare clic su **Add New User** (Aggiungi nuovo utente).</span><span class="sxs-lookup"><span data-stu-id="92b2d-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="92b2d-219">![Utenti](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="92b2d-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="92b2d-220">Hello **Add New User** opzione viene visualizzata solo se solo **Mozy** sia selezionato come provider di hello in **criteri di autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-220">hello **Add New User** option is only displayed only if **Mozy** is selected as hello provider under **Authentication policy**.</span></span> <span data-ttu-id="92b2d-221">Se è configurata l'autenticazione SAML, quindi hello utenti vengono aggiunti automaticamente al primo accesso tramite Single sign-in.</span><span class="sxs-lookup"><span data-stu-id="92b2d-221">If SAML Authentication is configured, then hello users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="92b2d-222">In hello nuova finestra di dialogo utente, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="92b2d-222">On hello new user dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="92b2d-223">![Aggiungere utenti](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Aggiungere utenti")</span><span class="sxs-lookup"><span data-stu-id="92b2d-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="92b2d-224">a.</span><span class="sxs-lookup"><span data-stu-id="92b2d-224">a.</span></span> <span data-ttu-id="92b2d-225">Da hello **scegliere un gruppo** elenco, selezionare un gruppo.</span><span class="sxs-lookup"><span data-stu-id="92b2d-225">From hello **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="92b2d-226">b.</span><span class="sxs-lookup"><span data-stu-id="92b2d-226">b.</span></span> <span data-ttu-id="92b2d-227">Da hello **il tipo di utente** selezionare un tipo.</span><span class="sxs-lookup"><span data-stu-id="92b2d-227">From hello **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="92b2d-228">c.</span><span class="sxs-lookup"><span data-stu-id="92b2d-228">c.</span></span> <span data-ttu-id="92b2d-229">In hello **Username** casella di testo Nome hello del tipo di utente hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92b2d-229">In hello **Username** textbox, type hello name of hello Azure AD user.</span></span>
   
   <span data-ttu-id="92b2d-230">d.</span><span class="sxs-lookup"><span data-stu-id="92b2d-230">d.</span></span> <span data-ttu-id="92b2d-231">In hello **posta elettronica** casella Tipo hello di indirizzo di posta elettronica dell'utente hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92b2d-231">In hello **Email** textbox, type hello email address of hello Azure AD user.</span></span>
   
   <span data-ttu-id="92b2d-232">e.</span><span class="sxs-lookup"><span data-stu-id="92b2d-232">e.</span></span> <span data-ttu-id="92b2d-233">Selezionare **Send user instruction email**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="92b2d-234">f.</span><span class="sxs-lookup"><span data-stu-id="92b2d-234">f.</span></span> <span data-ttu-id="92b2d-235">Fare clic su **Add User(s)**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="92b2d-236">Dopo aver creato l'utente hello, verrà inviato un messaggio di posta elettronica toohello utente di Azure AD che include un account di hello tooconfirm collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="92b2d-236">After creating hello user, an email will be sent toohello Azure AD user that includes a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="92b2d-237">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="92b2d-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="92b2d-238">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooMozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="92b2d-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMozy Enterprise.</span></span>

![Assegna utente][200] 

<span data-ttu-id="92b2d-240">**tooassign Britta Simon tooMozy Enterprise, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="92b2d-240">**tooassign Britta Simon tooMozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="92b2d-241">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="92b2d-243">Nell'elenco di applicazioni hello, selezionare **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-243">In hello applications list, select **Mozy Enterprise**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="92b2d-245">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="92b2d-247">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-247">Click **Add** button.</span></span> <span data-ttu-id="92b2d-248">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="92b2d-250">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="92b2d-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="92b2d-251">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92b2d-252">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="92b2d-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92b2d-253">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="92b2d-253">Testing single sign-on</span></span>

<span data-ttu-id="92b2d-254">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="92b2d-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="92b2d-255">Quando si fa clic hello Mozy Enterprise riquadro in hello Pannello di accesso, è necessario ottenere la pagina di accesso dell'applicazione di Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="92b2d-255">When you click hello Mozy Enterprise tile in hello Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="92b2d-256">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="92b2d-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92b2d-257">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="92b2d-257">Additional resources</span></span>

* [<span data-ttu-id="92b2d-258">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92b2d-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92b2d-259">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92b2d-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

