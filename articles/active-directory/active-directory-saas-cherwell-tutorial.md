---
title: 'Esercitazione: Integrazione di Azure Active Directory con Cherwell | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Cherwell.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad891f99-179e-4487-834d-35f3bc01c1ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: jeedes
ms.openlocfilehash: a67b3d346a6f7b43a7e87fb4d9c533f9363f2e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cherwell"></a><span data-ttu-id="67480-103">Esercitazione: Integrazione di Azure Active Directory con Cherwell</span><span class="sxs-lookup"><span data-stu-id="67480-103">Tutorial: Azure Active Directory integration with Cherwell</span></span>

<span data-ttu-id="67480-104">In questa esercitazione, è illustrato come toointegrate Cherwell con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="67480-104">In this tutorial, you learn how toointegrate Cherwell with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="67480-105">Integrazione di Cherwell con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="67480-105">Integrating Cherwell with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="67480-106">È possibile controllare in Azure AD che ha accesso tooCherwell</span><span class="sxs-lookup"><span data-stu-id="67480-106">You can control in Azure AD who has access tooCherwell</span></span>
- <span data-ttu-id="67480-107">È possibile abilitare l'utenti tooautomatically get connesso tooCherwell (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="67480-107">You can enable your users tooautomatically get signed-on tooCherwell (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="67480-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="67480-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="67480-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="67480-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67480-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="67480-110">Prerequisites</span></span>

<span data-ttu-id="67480-111">integrazione di Azure AD con Cherwell tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="67480-111">tooconfigure Azure AD integration with Cherwell, you need hello following items:</span></span>

- <span data-ttu-id="67480-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67480-112">An Azure AD subscription</span></span>
- <span data-ttu-id="67480-113">Sottoscrizione di Cherwell abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="67480-113">A Cherwell single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="67480-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="67480-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="67480-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="67480-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="67480-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="67480-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="67480-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67480-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="67480-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="67480-118">Scenario description</span></span>
<span data-ttu-id="67480-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="67480-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="67480-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="67480-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="67480-121">Aggiunta di Cherwell dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="67480-121">Adding Cherwell from hello gallery</span></span>
2. <span data-ttu-id="67480-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67480-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cherwell-from-hello-gallery"></a><span data-ttu-id="67480-123">Aggiunta di Cherwell dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="67480-123">Adding Cherwell from hello gallery</span></span>
<span data-ttu-id="67480-124">integrazione hello tooconfigure di Cherwell in Azure AD, è necessario tooadd Cherwell dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="67480-124">tooconfigure hello integration of Cherwell into Azure AD, you need tooadd Cherwell from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="67480-125">**tooadd Cherwell dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="67480-125">**tooadd Cherwell from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="67480-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="67480-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="67480-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="67480-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="67480-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="67480-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="67480-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="67480-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="67480-133">Nella casella di ricerca hello, digitare **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="67480-133">In hello search box, type **Cherwell**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_search.png)

5. <span data-ttu-id="67480-135">Nel riquadro dei risultati hello, selezionare **Cherwell**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="67480-135">In hello results panel, select **Cherwell**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="67480-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67480-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="67480-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Cherwell usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="67480-138">In this section, you configure and test Azure AD single sign-on with Cherwell based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="67480-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Cherwell è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67480-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cherwell is tooa user in Azure AD.</span></span> <span data-ttu-id="67480-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Cherwell deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="67480-140">In other words, a link relationship between an Azure AD user and hello related user in Cherwell needs toobe established.</span></span>

<span data-ttu-id="67480-141">In Cherwell, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="67480-141">In Cherwell, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="67480-142">tooconfigure e prova AD Azure single sign-on con Cherwell, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="67480-142">tooconfigure and test Azure AD single sign-on with Cherwell, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="67480-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="67480-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="67480-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="67480-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="67480-145">**[Creazione di un utente test Cherwell](#creating-a-cherwell-test-user)**  -toohave un equivalente di Britta Simon in Cherwell che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="67480-145">**[Creating a Cherwell test user](#creating-a-cherwell-test-user)** - toohave a counterpart of Britta Simon in Cherwell that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="67480-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="67480-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="67480-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="67480-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="67480-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67480-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="67480-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Cherwell.</span><span class="sxs-lookup"><span data-stu-id="67480-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cherwell application.</span></span>

<span data-ttu-id="67480-150">**Azure AD tooconfigure single sign-on con Cherwell, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="67480-150">**tooconfigure Azure AD single sign-on with Cherwell, perform hello following steps:**</span></span>

1. <span data-ttu-id="67480-151">Nel portale di Azure su hello hello **Cherwell** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="67480-151">In hello Azure portal, on hello **Cherwell** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="67480-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="67480-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_samlbase.png)

3. <span data-ttu-id="67480-155">In hello **Cherwell dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="67480-155">On hello **Cherwell Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_url.png)

    <span data-ttu-id="67480-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.cherwellondemand.com/cherwellclient`</span><span class="sxs-lookup"><span data-stu-id="67480-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.cherwellondemand.com/cherwellclient`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="67480-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="67480-158">This value is not real.</span></span> <span data-ttu-id="67480-159">Aggiornare questo valore con URL hello effettivo Sign-on.</span><span class="sxs-lookup"><span data-stu-id="67480-159">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="67480-160">Contatto [team di supporto di Cherwell](https://csm.cherwell.com/contact) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="67480-160">Contact [Cherwell support team](https://csm.cherwell.com/contact) tooget this value.</span></span>
 
4. <span data-ttu-id="67480-161">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="67480-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_certificate.png) 

5. <span data-ttu-id="67480-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="67480-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cherwell-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="67480-165">In hello **Cherwell configurazione** fare clic su **configurare Cherwell** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="67480-165">On hello **Cherwell Configuration** section, click **Configure Cherwell** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="67480-166">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="67480-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_configure.png) 

7. <span data-ttu-id="67480-168">tooconfigure single sign-on sul **Cherwell** lato, è necessario hello toosend scaricato **certificato (Base64)**, **SAML Single Sign-On Service URL**, e  **ID entità SAML** troppo[team di supporto di Cherwell](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="67480-168">tooconfigure single sign-on on **Cherwell** side, you need toosend hello downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Cherwell support team](https://csm.cherwell.com/contact).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="67480-169">Il team di supporto di Cherwell con configurazione di SSO toodo hello effettivo.</span><span class="sxs-lookup"><span data-stu-id="67480-169">Your Cherwell support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="67480-170">Una volta completata l'abilitazione dell'accesso Single Sign-On per la sottoscrizione, si riceverà una notifica.</span><span class="sxs-lookup"><span data-stu-id="67480-170">You will get a notification when SSO has been enabled for your subscription.</span></span>
    > 
    
> [!TIP]
> <span data-ttu-id="67480-171">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="67480-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="67480-172">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="67480-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="67480-173">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="67480-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="67480-174">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="67480-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="67480-175">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="67480-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="67480-177">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="67480-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="67480-178">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="67480-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="67480-180">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="67480-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="67480-182">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="67480-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="67480-184">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="67480-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-cherwell-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="67480-186">a.</span><span class="sxs-lookup"><span data-stu-id="67480-186">a.</span></span> <span data-ttu-id="67480-187">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="67480-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="67480-188">b.</span><span class="sxs-lookup"><span data-stu-id="67480-188">b.</span></span> <span data-ttu-id="67480-189">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="67480-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="67480-190">c.</span><span class="sxs-lookup"><span data-stu-id="67480-190">c.</span></span> <span data-ttu-id="67480-191">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="67480-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="67480-192">d.</span><span class="sxs-lookup"><span data-stu-id="67480-192">d.</span></span> <span data-ttu-id="67480-193">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="67480-193">Click **Create**.</span></span>
 
### <a name="creating-a-cherwell-test-user"></a><span data-ttu-id="67480-194">Creazione di un utente di test di Cherwell</span><span class="sxs-lookup"><span data-stu-id="67480-194">Creating a Cherwell test user</span></span>

<span data-ttu-id="67480-195">toolog agli utenti di Azure AD tooenable in tooCherwell, è necessario eseguirne il provisioning in Cherwell.</span><span class="sxs-lookup"><span data-stu-id="67480-195">tooenable Azure AD users toolog in tooCherwell, they must be provisioned into Cherwell.</span></span>

<span data-ttu-id="67480-196">Nel caso di hello di Cherwell, gli account utente di hello necessitano toobe creati il [team di supporto di Cherwell](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="67480-196">In hello case of Cherwell, hello user accounts need toobe created by your [Cherwell support team](https://csm.cherwell.com/contact).</span></span>

>[!NOTE]
><span data-ttu-id="67480-197">È possibile usare qualsiasi altro Cherwell utente account strumento di creazione o le API fornite da Cherwell tooprovision Azure Active Directory gli account utente.</span><span class="sxs-lookup"><span data-stu-id="67480-197">You can use any other Cherwell user account creation tools or APIs provided by Cherwell tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="67480-198">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="67480-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="67480-199">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCherwell.</span><span class="sxs-lookup"><span data-stu-id="67480-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCherwell.</span></span>

![Assegna utente][200] 

<span data-ttu-id="67480-201">**tooassign Britta Simon tooCherwell, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="67480-201">**tooassign Britta Simon tooCherwell, perform hello following steps:**</span></span>

1. <span data-ttu-id="67480-202">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="67480-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="67480-204">Nell'elenco di applicazioni hello, selezionare **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="67480-204">In hello applications list, select **Cherwell**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_app.png) 

3. <span data-ttu-id="67480-206">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="67480-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="67480-208">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="67480-208">Click **Add** button.</span></span> <span data-ttu-id="67480-209">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="67480-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="67480-211">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="67480-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="67480-212">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="67480-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="67480-213">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="67480-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="67480-214">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="67480-214">Testing single sign-on</span></span>

<span data-ttu-id="67480-215">Se si desiderano tootest le impostazioni di single sign-on, aprire Pannello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="67480-215">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="67480-216">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="67480-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="67480-217">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="67480-217">Additional resources</span></span>

* [<span data-ttu-id="67480-218">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67480-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="67480-219">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67480-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_203.png

