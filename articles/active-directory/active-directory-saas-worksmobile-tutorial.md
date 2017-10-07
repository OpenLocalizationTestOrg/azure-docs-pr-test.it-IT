---
title: 'Esercitazione: Integrazione di Azure Active Directory con WORKS MOBILE | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e i dispositivi mobili funziona.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 80192218a2e99a921834bb53e708d5e4fab413f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="ba283-103">Esercitazione: Integrazione di Azure Active Directory con WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="ba283-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="ba283-104">In questa esercitazione, è illustrato il funzionamento toointegrate per dispositivi mobili con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ba283-104">In this tutorial, you learn how toointegrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ba283-105">Integrazione MOBILE funziona con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="ba283-105">Integrating WORKS MOBILE with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ba283-106">È possibile controllare in Azure AD che ha accesso tooWORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="ba283-106">You can control in Azure AD who has access tooWORKS MOBILE</span></span>
- <span data-ttu-id="ba283-107">È possibile abilitare l'utenti tooautomatically get connesso tooWORKS MOBILE (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba283-107">You can enable your users tooautomatically get signed-on tooWORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ba283-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ba283-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ba283-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ba283-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba283-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ba283-110">Prerequisites</span></span>

<span data-ttu-id="ba283-111">integrazione di Azure AD con WORKS MOBILE tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ba283-111">tooconfigure Azure AD integration with WORKS MOBILE, you need hello following items:</span></span>

- <span data-ttu-id="ba283-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba283-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ba283-113">Sottoscrizione di WORKS MOBILE abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ba283-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ba283-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ba283-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ba283-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="ba283-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ba283-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ba283-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ba283-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ba283-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ba283-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ba283-118">Scenario description</span></span>
<span data-ttu-id="ba283-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ba283-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ba283-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="ba283-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ba283-121">Aggiunta di dispositivi mobili funziona dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ba283-121">Adding WORKS MOBILE from hello gallery</span></span>
2. <span data-ttu-id="ba283-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba283-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-hello-gallery"></a><span data-ttu-id="ba283-123">Aggiunta di dispositivi mobili funziona dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ba283-123">Adding WORKS MOBILE from hello gallery</span></span>
<span data-ttu-id="ba283-124">integrazione hello tooconfigure di dispositivi mobili funziona in Azure AD, è necessario tooadd WORKS MOBILE dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ba283-124">tooconfigure hello integration of WORKS MOBILE into Azure AD, you need tooadd WORKS MOBILE from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ba283-125">**tooadd MOBILE WORKS dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ba283-125">**tooadd WORKS MOBILE from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba283-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ba283-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ba283-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ba283-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ba283-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ba283-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="ba283-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ba283-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="ba283-133">Nella casella di ricerca hello, digitare **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="ba283-133">In hello search box, type **WORKS MOBILE**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="ba283-135">Nel riquadro dei risultati hello, selezionare **WORKS MOBILE**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ba283-135">In hello results panel, select **WORKS MOBILE**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ba283-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba283-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ba283-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con WORKS MOBILE usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ba283-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ba283-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in WORKS MOBILE è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba283-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in WORKS MOBILE is tooa user in Azure AD.</span></span> <span data-ttu-id="ba283-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e utente correlato di hello in MOBILE WORKS deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="ba283-140">In other words, a link relationship between an Azure AD user and hello related user in WORKS MOBILE needs toobe established.</span></span>

<span data-ttu-id="ba283-141">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** in WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="ba283-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="ba283-142">tooconfigure e prova AD Azure single sign-on con dispositivi mobili funziona, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="ba283-142">tooconfigure and test Azure AD single sign-on with WORKS MOBILE, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ba283-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ba283-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ba283-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ba283-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ba283-145">**[Creazione di un utente test WORKS MOBILE](#creating-a-works-mobile-test-user)**  -toohave un equivalente di Britta Simon in WORKS MOBILE che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ba283-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - toohave a counterpart of Britta Simon in WORKS MOBILE that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ba283-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ba283-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ba283-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="ba283-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ba283-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba283-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ba283-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione MOBILE funziona.</span><span class="sxs-lookup"><span data-stu-id="ba283-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="ba283-150">**tooconfigure AD Azure single sign-on con dispositivi mobili funziona, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ba283-150">**tooconfigure Azure AD single sign-on with WORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba283-151">Nel portale di Azure su hello hello **WORKS MOBILE** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ba283-151">In hello Azure portal, on hello **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="ba283-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ba283-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="ba283-155">In hello **WORKS MOBILE dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ba283-155">On hello **WORKS MOBILE Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="ba283-157">a.</span><span class="sxs-lookup"><span data-stu-id="ba283-157">a.</span></span> <span data-ttu-id="ba283-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="ba283-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="ba283-159">b.</span><span class="sxs-lookup"><span data-stu-id="ba283-159">b.</span></span> <span data-ttu-id="ba283-160">In hello **identificatore** casella di testo, tipo di valore hello di`worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="ba283-160">In hello **Identifier** textbox, type hello value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ba283-161">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="ba283-161">This value is not real.</span></span> <span data-ttu-id="ba283-162">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="ba283-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ba283-163">Contatto [team di supporto Client di dispositivi mobili funziona](mailto:dl_ssoinfo@worksmobile.com) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="ba283-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="ba283-164">In hello **certificato di firma SAML** fare clic su **Certificate(Raw)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="ba283-164">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="ba283-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ba283-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ba283-168">In hello **configurazione per dispositivi mobili funziona** fare clic su **configurare MOBILE WORKS** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="ba283-168">On hello **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ba283-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="ba283-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="ba283-171">tooget SSO è configurato per l'applicazione, contattare [team di supporto di dispositivi mobili funziona](mailto:dl_ssoinfo@worksmobile.com) e fornire loro hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="ba283-171">tooget SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with hello following information:</span></span> 

    <span data-ttu-id="ba283-172">• hello scaricato **file di certificato**</span><span class="sxs-lookup"><span data-stu-id="ba283-172">• hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="ba283-173">• hello **SAML Single Sign-On Service URL**</span><span class="sxs-lookup"><span data-stu-id="ba283-173">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="ba283-174">• hello **ID entità SAML**</span><span class="sxs-lookup"><span data-stu-id="ba283-174">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="ba283-175">• hello **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="ba283-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="ba283-176">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="ba283-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ba283-177">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="ba283-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ba283-178">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ba283-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ba283-179">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba283-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="ba283-180">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ba283-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="ba283-182">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ba283-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba283-183">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ba283-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ba283-185">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ba283-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ba283-187">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="ba283-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ba283-189">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ba283-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ba283-191">a.</span><span class="sxs-lookup"><span data-stu-id="ba283-191">a.</span></span> <span data-ttu-id="ba283-192">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ba283-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ba283-193">b.</span><span class="sxs-lookup"><span data-stu-id="ba283-193">b.</span></span> <span data-ttu-id="ba283-194">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ba283-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ba283-195">c.</span><span class="sxs-lookup"><span data-stu-id="ba283-195">c.</span></span> <span data-ttu-id="ba283-196">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="ba283-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ba283-197">d.</span><span class="sxs-lookup"><span data-stu-id="ba283-197">d.</span></span> <span data-ttu-id="ba283-198">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ba283-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="ba283-199">Creazione di un utente test WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="ba283-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="ba283-200">In questa sezione viene creato un utente di nome Britta Simon in WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="ba283-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="ba283-201">Rivolgersi [team di supporto di dispositivi mobili funziona](mailto:dl_ssoinfo@worksmobile.com) utenti hello tooadd nella piattaforma MOBILE WORKS hello.</span><span class="sxs-lookup"><span data-stu-id="ba283-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) tooadd hello users in hello WORKS MOBILE platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ba283-202">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba283-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ba283-203">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooWORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="ba283-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWORKS MOBILE.</span></span>

![Assegna utente][200] 

<span data-ttu-id="ba283-205">**tooassign Britta Simon tooWORKS dispositivi mobili, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ba283-205">**tooassign Britta Simon tooWORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="ba283-206">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ba283-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ba283-208">Nell'elenco di applicazioni hello, selezionare **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="ba283-208">In hello applications list, select **WORKS MOBILE**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="ba283-210">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ba283-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="ba283-212">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ba283-212">Click **Add** button.</span></span> <span data-ttu-id="ba283-213">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ba283-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="ba283-215">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="ba283-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ba283-216">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ba283-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ba283-217">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ba283-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ba283-218">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ba283-218">Testing single sign-on</span></span>

<span data-ttu-id="ba283-219">In questa sezione è verificare la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ba283-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ba283-220">Quando si fa clic su riquadro MOBILE WORKS hello in hello Pannello di accesso, è necessario ottenere l'applicazione MOBILE WORKS tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="ba283-220">When you click hello WORKS MOBILE tile in hello Access Panel, you should get automatically signed-on tooyour WORKS MOBILE application.</span></span>
<span data-ttu-id="ba283-221">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ba283-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ba283-222">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ba283-222">Additional resources</span></span>

* [<span data-ttu-id="ba283-223">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba283-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ba283-224">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba283-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

