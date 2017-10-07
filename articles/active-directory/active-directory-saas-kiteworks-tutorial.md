---
title: Esercitazione Integrazione di Azure Active Directory con Kiteworks | Microsoft Docs
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Kiteworks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 406417dd7f58cc3f1fa0d9e86b5cad0c1d7be750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="5bee0-103">Esercitazione Integrazione di Azure Active Directory con Kiteworks</span><span class="sxs-lookup"><span data-stu-id="5bee0-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="5bee0-104">In questa esercitazione, è illustrato come toointegrate Kiteworks con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5bee0-104">In this tutorial, you learn how toointegrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5bee0-105">Integrazione Kiteworks con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="5bee0-105">Integrating Kiteworks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5bee0-106">È possibile controllare in Azure AD che ha accesso tooKiteworks</span><span class="sxs-lookup"><span data-stu-id="5bee0-106">You can control in Azure AD who has access tooKiteworks</span></span>
- <span data-ttu-id="5bee0-107">È possibile abilitare l'utenti tooautomatically get connesso tooKiteworks (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bee0-107">You can enable your users tooautomatically get signed-on tooKiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5bee0-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5bee0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5bee0-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5bee0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bee0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5bee0-110">Prerequisites</span></span>

<span data-ttu-id="5bee0-111">integrazione di Azure AD con Kiteworks tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5bee0-111">tooconfigure Azure AD integration with Kiteworks, you need hello following items:</span></span>

- <span data-ttu-id="5bee0-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bee0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5bee0-113">Sottoscrizione di Kiteworks abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5bee0-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5bee0-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5bee0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5bee0-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="5bee0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5bee0-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5bee0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5bee0-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5bee0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5bee0-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5bee0-118">Scenario description</span></span>
<span data-ttu-id="5bee0-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5bee0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5bee0-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="5bee0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5bee0-121">Aggiunta di Kiteworks dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5bee0-121">Adding Kiteworks from hello gallery</span></span>
2. <span data-ttu-id="5bee0-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bee0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-hello-gallery"></a><span data-ttu-id="5bee0-123">Aggiunta di Kiteworks dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5bee0-123">Adding Kiteworks from hello gallery</span></span>
<span data-ttu-id="5bee0-124">integrazione hello tooconfigure di Kiteworks in Azure AD, è necessario tooadd Kiteworks dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5bee0-124">tooconfigure hello integration of Kiteworks into Azure AD, you need tooadd Kiteworks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5bee0-125">**tooadd Kiteworks dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5bee0-125">**tooadd Kiteworks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bee0-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5bee0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5bee0-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5bee0-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="5bee0-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5bee0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="5bee0-133">Nella casella di ricerca hello, digitare **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-133">In hello search box, type **Kiteworks**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="5bee0-135">Nel riquadro dei risultati hello, selezionare **Kiteworks**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5bee0-135">In hello results panel, select **Kiteworks**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5bee0-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bee0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5bee0-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Kiteworks mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5bee0-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5bee0-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Kiteworks è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bee0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kiteworks is tooa user in Azure AD.</span></span> <span data-ttu-id="5bee0-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Kiteworks deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="5bee0-140">In other words, a link relationship between an Azure AD user and hello related user in Kiteworks needs toobe established.</span></span>

<span data-ttu-id="5bee0-141">In Kiteworks, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="5bee0-141">In Kiteworks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5bee0-142">tooconfigure e prova AD Azure single sign-on con Kiteworks, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="5bee0-142">tooconfigure and test Azure AD single sign-on with Kiteworks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5bee0-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5bee0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5bee0-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5bee0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5bee0-145">**[Creazione di un utente test Kiteworks](#creating-a-kiteworks-test-user)**  -toohave un equivalente di Britta Simon in Kiteworks che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5bee0-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - toohave a counterpart of Britta Simon in Kiteworks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5bee0-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5bee0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5bee0-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="5bee0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5bee0-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bee0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5bee0-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="5bee0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="5bee0-150">**Azure AD tooconfigure single sign-on con Kiteworks, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5bee0-150">**tooconfigure Azure AD single sign-on with Kiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bee0-151">Nel portale di Azure su hello hello **Kiteworks** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-151">In hello Azure portal, on hello **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="5bee0-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5bee0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="5bee0-155">In hello **Kiteworks dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5bee0-155">On hello **Kiteworks Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="5bee0-157">a.</span><span class="sxs-lookup"><span data-stu-id="5bee0-157">a.</span></span> <span data-ttu-id="5bee0-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="5bee0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="5bee0-159">b.</span><span class="sxs-lookup"><span data-stu-id="5bee0-159">b.</span></span> <span data-ttu-id="5bee0-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="5bee0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5bee0-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="5bee0-161">These values are not real.</span></span> <span data-ttu-id="5bee0-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="5bee0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5bee0-163">Contatto [team di supporto Kiteworks Client](http://accellion.com/support) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="5bee0-163">Contact [Kiteworks Client support team](http://accellion.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="5bee0-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5bee0-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="5bee0-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5bee0-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5bee0-168">In hello **Kiteworks configurazione** fare clic su **configurare Kiteworks** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="5bee0-168">On hello **Kiteworks Configuration** section, click **Configure Kiteworks** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5bee0-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="5bee0-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="5bee0-171">Accesso tooyour sito della società Kiteworks come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5bee0-171">Sign on tooyour Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="5bee0-172">Nella barra degli strumenti hello in primo piano hello, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="5bee0-174">In hello **autenticazione e autorizzazione** fare clic su **il programma di installazione SSO**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-174">In hello **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="5bee0-176">Nella pagina di installazione SSO hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5bee0-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="5bee0-178">a.</span><span class="sxs-lookup"><span data-stu-id="5bee0-178">a.</span></span> <span data-ttu-id="5bee0-179">Selezionare **Autentica tramite Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="5bee0-180">b.</span><span class="sxs-lookup"><span data-stu-id="5bee0-180">b.</span></span> <span data-ttu-id="5bee0-181">Selezionare **Avvia richiesta autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="5bee0-182">c.</span><span class="sxs-lookup"><span data-stu-id="5bee0-182">c.</span></span> <span data-ttu-id="5bee0-183">In hello **IDP Entity ID** casella di testo, hello Incolla valore **ID entità SAML**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5bee0-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="5bee0-184">d.</span><span class="sxs-lookup"><span data-stu-id="5bee0-184">d.</span></span> <span data-ttu-id="5bee0-185">In hello **URL servizio Single Sign-On** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5bee0-185">In hello **Single Sign-On Service URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5bee0-186">e.</span><span class="sxs-lookup"><span data-stu-id="5bee0-186">e.</span></span> <span data-ttu-id="5bee0-187">In hello **Single Logout URL di servizio** casella di testo, hello Incolla valore **Sign-Out URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5bee0-187">In hello **Single Logout Service URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5bee0-188">f.</span><span class="sxs-lookup"><span data-stu-id="5bee0-188">f.</span></span> <span data-ttu-id="5bee0-189">Aprire il certificato scaricato nel blocco note, hello copia il contenuto e quindi incollarlo hello **certificato chiave pubblica RSA** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="5bee0-189">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="5bee0-190">g.</span><span class="sxs-lookup"><span data-stu-id="5bee0-190">g.</span></span> <span data-ttu-id="5bee0-191">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5bee0-192">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="5bee0-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5bee0-193">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="5bee0-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5bee0-194">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5bee0-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5bee0-195">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bee0-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="5bee0-196">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5bee0-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="5bee0-198">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5bee0-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bee0-199">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5bee0-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5bee0-201">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5bee0-203">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="5bee0-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5bee0-205">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5bee0-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5bee0-207">a.</span><span class="sxs-lookup"><span data-stu-id="5bee0-207">a.</span></span> <span data-ttu-id="5bee0-208">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5bee0-209">b.</span><span class="sxs-lookup"><span data-stu-id="5bee0-209">b.</span></span> <span data-ttu-id="5bee0-210">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5bee0-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5bee0-211">c.</span><span class="sxs-lookup"><span data-stu-id="5bee0-211">c.</span></span> <span data-ttu-id="5bee0-212">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5bee0-213">d.</span><span class="sxs-lookup"><span data-stu-id="5bee0-213">d.</span></span> <span data-ttu-id="5bee0-214">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="5bee0-215">Creazione di un utente test per Kiteworks</span><span class="sxs-lookup"><span data-stu-id="5bee0-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="5bee0-216">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Kiteworks toocreate.</span><span class="sxs-lookup"><span data-stu-id="5bee0-216">hello objective of this section is toocreate a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="5bee0-217">Kiteworks supporta il provisioning JIT (just-in-time), che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5bee0-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="5bee0-218">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="5bee0-218">There is no action item for you in this section.</span></span> <span data-ttu-id="5bee0-219">Se non esiste ancora, durante un tooaccess tentativo Kitewors viene creato un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="5bee0-219">A new user is created during an attempt tooaccess Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="5bee0-220">Se è necessario un utente toocreate manualmente, è necessario hello toocontact [Kiteworks team di supporto](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="5bee0-220">If you need toocreate a user manually, you need toocontact hello [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5bee0-221">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bee0-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5bee0-222">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooKiteworks.</span><span class="sxs-lookup"><span data-stu-id="5bee0-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKiteworks.</span></span>

![Assegna utente][200] 

<span data-ttu-id="5bee0-224">**tooassign Britta Simon tooKiteworks, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5bee0-224">**tooassign Britta Simon tooKiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bee0-225">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5bee0-227">Nell'elenco di applicazioni hello, selezionare **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-227">In hello applications list, select **Kiteworks**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="5bee0-229">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="5bee0-231">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-231">Click **Add** button.</span></span> <span data-ttu-id="5bee0-232">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="5bee0-234">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="5bee0-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5bee0-235">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5bee0-236">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5bee0-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5bee0-237">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5bee0-237">Testing single sign-on</span></span>

<span data-ttu-id="5bee0-238">obiettivo di Hello di questa sezione è tootest la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5bee0-238">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="5bee0-239">Quando si fa clic hello Kiteworks riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Kiteworks applicazione.</span><span class="sxs-lookup"><span data-stu-id="5bee0-239">When you click hello Kiteworks tile in hello Access Panel, you should get automatically signed-on tooyour Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5bee0-240">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5bee0-240">Additional resources</span></span>

* [<span data-ttu-id="5bee0-241">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bee0-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5bee0-242">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bee0-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

