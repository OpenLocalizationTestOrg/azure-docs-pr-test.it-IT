---
title: 'Esercitazione: Integrazione di Azure Active Directory con Novatus | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Novatus.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: jeedes
ms.openlocfilehash: 7ff13f56f0f47d0c2667c9ca555801a7a06a2fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="1d936-103">Esercitazione: Integrazione di Azure Active Directory con Novatus</span><span class="sxs-lookup"><span data-stu-id="1d936-103">Tutorial: Azure Active Directory integration with Novatus</span></span>

<span data-ttu-id="1d936-104">In questa esercitazione, è illustrato come toointegrate Novatus con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1d936-104">In this tutorial, you learn how toointegrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1d936-105">Integrazione Novatus con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="1d936-105">Integrating Novatus with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1d936-106">È possibile controllare in Azure AD che ha accesso tooNovatus</span><span class="sxs-lookup"><span data-stu-id="1d936-106">You can control in Azure AD who has access tooNovatus</span></span>
- <span data-ttu-id="1d936-107">È possibile abilitare l'utenti tooautomatically get connesso tooNovatus (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d936-107">You can enable your users tooautomatically get signed-on tooNovatus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1d936-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1d936-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1d936-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1d936-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d936-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1d936-110">Prerequisites</span></span>

<span data-ttu-id="1d936-111">integrazione di Azure AD con Novatus tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1d936-111">tooconfigure Azure AD integration with Novatus, you need hello following items:</span></span>

- <span data-ttu-id="1d936-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d936-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1d936-113">Sottoscrizione di Novatus abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1d936-113">A Novatus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1d936-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1d936-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1d936-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="1d936-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1d936-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1d936-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1d936-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1d936-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1d936-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1d936-118">Scenario description</span></span>
<span data-ttu-id="1d936-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1d936-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1d936-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="1d936-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1d936-121">Aggiunta di Novatus dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1d936-121">Adding Novatus from hello gallery</span></span>
2. <span data-ttu-id="1d936-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d936-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-novatus-from-hello-gallery"></a><span data-ttu-id="1d936-123">Aggiunta di Novatus dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1d936-123">Adding Novatus from hello gallery</span></span>
<span data-ttu-id="1d936-124">integrazione hello tooconfigure di Novatus in Azure AD, è necessario tooadd Novatus dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1d936-124">tooconfigure hello integration of Novatus into Azure AD, you need tooadd Novatus from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1d936-125">**tooadd Novatus dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1d936-125">**tooadd Novatus from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d936-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1d936-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1d936-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1d936-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1d936-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1d936-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1d936-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1d936-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1d936-133">Nella casella di ricerca hello, digitare **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="1d936-133">In hello search box, type **Novatus**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_search.png)

5. <span data-ttu-id="1d936-135">Nel riquadro dei risultati hello, selezionare **Novatus**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1d936-135">In hello results panel, select **Novatus**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1d936-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d936-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1d936-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Novatus usando un utente di prova di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1d936-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1d936-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Novatus è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d936-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Novatus is tooa user in Azure AD.</span></span> <span data-ttu-id="1d936-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Novatus deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="1d936-140">In other words, a link relationship between an Azure AD user and hello related user in Novatus needs toobe established.</span></span>

<span data-ttu-id="1d936-141">In Novatus, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="1d936-141">In Novatus, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1d936-142">tooconfigure e prova AD Azure single sign-on con Novatus, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1d936-142">tooconfigure and test Azure AD single sign-on with Novatus, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1d936-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1d936-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1d936-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1d936-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1d936-145">**[Creazione di un utente test Novatus](#creating-a-novatus-test-user)**  -toohave un equivalente di Britta Simon in Novatus che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1d936-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - toohave a counterpart of Britta Simon in Novatus that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1d936-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1d936-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1d936-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1d936-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1d936-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d936-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1d936-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Novatus.</span><span class="sxs-lookup"><span data-stu-id="1d936-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Novatus application.</span></span>

<span data-ttu-id="1d936-150">**Azure AD tooconfigure single sign-on con Novatus, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1d936-150">**tooconfigure Azure AD single sign-on with Novatus, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d936-151">Nel portale di Azure su hello hello **Novatus** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1d936-151">In hello Azure portal, on hello **Novatus** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1d936-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1d936-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_samlbase.png)

3. <span data-ttu-id="1d936-155">In hello **Novatus dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1d936-155">On hello **Novatus Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_url.png)

     <span data-ttu-id="1d936-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://sso.novatuscontracts.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="1d936-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.novatuscontracts.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1d936-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="1d936-158">This value is not real.</span></span> <span data-ttu-id="1d936-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1d936-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1d936-160">Contatto [team di supporto Novatus Client](mailto:jvinci@novatusinc.com) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="1d936-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) tooget this value.</span></span> 
 


4. <span data-ttu-id="1d936-161">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1d936-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_certificate.png) 

5. <span data-ttu-id="1d936-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="1d936-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-novatus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1d936-165">In hello **Novatus configurazione** fare clic su **configurare Novatus** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="1d936-165">On hello **Novatus Configuration** section, click **Configure Novatus** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1d936-166">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="1d936-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_configure.png) 

7. <span data-ttu-id="1d936-168">tooget SSO è configurato per l'applicazione, contattare il [Novatus team di supporto](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="1d936-168">tooget SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> <span data-ttu-id="1d936-169">Collegare hello **scaricato certificato** hello di posta elettronica e condivisione tooyour file **gli URL dei metadati** (**Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL**) con Tooset team Novatus di SSO sul relativo lato.</span><span class="sxs-lookup"><span data-stu-id="1d936-169">Attach hello **downloaded certificate** file tooyour mail and share hello **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team tooset up SSO on their side.</span></span>

> [!TIP]
> <span data-ttu-id="1d936-170">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="1d936-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1d936-171">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="1d936-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1d936-172">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1d936-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1d936-173">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d936-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="1d936-174">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1d936-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1d936-176">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1d936-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d936-177">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1d936-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1d936-179">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="1d936-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1d936-181">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="1d936-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1d936-183">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1d936-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1d936-185">a.</span><span class="sxs-lookup"><span data-stu-id="1d936-185">a.</span></span> <span data-ttu-id="1d936-186">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1d936-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1d936-187">b.</span><span class="sxs-lookup"><span data-stu-id="1d936-187">b.</span></span> <span data-ttu-id="1d936-188">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1d936-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1d936-189">c.</span><span class="sxs-lookup"><span data-stu-id="1d936-189">c.</span></span> <span data-ttu-id="1d936-190">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="1d936-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1d936-191">d.</span><span class="sxs-lookup"><span data-stu-id="1d936-191">d.</span></span> <span data-ttu-id="1d936-192">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1d936-192">Click **Create**.</span></span>
 
### <a name="creating-a-novatus-test-user"></a><span data-ttu-id="1d936-193">Creazione di un utente test per Novatus</span><span class="sxs-lookup"><span data-stu-id="1d936-193">Creating a Novatus test user</span></span>

<span data-ttu-id="1d936-194">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Novatus toocreate.</span><span class="sxs-lookup"><span data-stu-id="1d936-194">hello objective of this section is toocreate a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="1d936-195">Novatus supporta il provisioning just-in-time, che è abilitato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1d936-195">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1d936-196">Non è necessario alcun intervento dell'utente in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="1d936-196">There is no action item for you in this section.</span></span> <span data-ttu-id="1d936-197">Verrà creato un nuovo utente durante una tooaccess tentativo Novatus se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="1d936-197">A new user will be created during an attempt tooaccess Novatus if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="1d936-198">Se è necessario un utente toocreate manualmente, è necessario hello toocontact [Novatus team di supporto](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="1d936-198">If you need toocreate an user manually, you need toocontact hello [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1d936-199">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1d936-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1d936-200">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooNovatus.</span><span class="sxs-lookup"><span data-stu-id="1d936-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNovatus.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1d936-202">**tooassign Britta Simon tooNovatus, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1d936-202">**tooassign Britta Simon tooNovatus, perform hello following steps:**</span></span>

1. <span data-ttu-id="1d936-203">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1d936-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1d936-205">Nell'elenco di applicazioni hello, selezionare **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="1d936-205">In hello applications list, select **Novatus**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_app.png) 

3. <span data-ttu-id="1d936-207">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1d936-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1d936-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1d936-209">Click **Add** button.</span></span> <span data-ttu-id="1d936-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1d936-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1d936-212">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1d936-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1d936-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1d936-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1d936-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1d936-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1d936-215">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1d936-215">Testing single sign-on</span></span>

<span data-ttu-id="1d936-216">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1d936-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1d936-217">Quando si fa clic hello Novatus riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Novatus applicazione.</span><span class="sxs-lookup"><span data-stu-id="1d936-217">When you click hello Novatus tile in hello Access Panel, you should get automatically signed-on tooyour Novatus application.</span></span> <span data-ttu-id="1d936-218">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1d936-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1d936-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1d936-219">Additional resources</span></span>

* [<span data-ttu-id="1d936-220">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d936-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1d936-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d936-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_203.png

