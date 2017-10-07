---
title: 'Esercitazione: Integrazione di Azure Active Directory con Pantheon | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Pantheon.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c3e54aef1f64dbab77d40a8c098172d609bfec8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="6a14d-103">Esercitazione: integrazione di Azure Active Directory con Pantheon</span><span class="sxs-lookup"><span data-stu-id="6a14d-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="6a14d-104">In questa esercitazione, è illustrato come toointegrate Pantheon con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6a14d-104">In this tutorial, you learn how toointegrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a14d-105">Integrazione Pantheon con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="6a14d-105">Integrating Pantheon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6a14d-106">È possibile controllare in Azure AD che ha accesso tooPantheon</span><span class="sxs-lookup"><span data-stu-id="6a14d-106">You can control in Azure AD who has access tooPantheon</span></span>
- <span data-ttu-id="6a14d-107">È possibile abilitare l'utenti tooautomatically get connesso tooPantheon (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a14d-107">You can enable your users tooautomatically get signed-on tooPantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6a14d-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6a14d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6a14d-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6a14d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a14d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6a14d-110">Prerequisites</span></span>

<span data-ttu-id="6a14d-111">integrazione di Azure AD con Pantheon tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="6a14d-111">tooconfigure Azure AD integration with Pantheon, you need hello following items:</span></span>

- <span data-ttu-id="6a14d-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a14d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a14d-113">Sottoscrizione di Pantheon abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6a14d-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a14d-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="6a14d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a14d-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="6a14d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a14d-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="6a14d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a14d-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a14d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a14d-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="6a14d-118">Scenario description</span></span>
<span data-ttu-id="6a14d-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="6a14d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a14d-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="6a14d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a14d-121">Aggiunta di Pantheon dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6a14d-121">Adding Pantheon from hello gallery</span></span>
2. <span data-ttu-id="6a14d-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a14d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-hello-gallery"></a><span data-ttu-id="6a14d-123">Aggiunta di Pantheon dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="6a14d-123">Adding Pantheon from hello gallery</span></span>
<span data-ttu-id="6a14d-124">integrazione hello tooconfigure di Pantheon in Azure AD, è necessario tooadd Pantheon dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="6a14d-124">tooconfigure hello integration of Pantheon into Azure AD, you need tooadd Pantheon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6a14d-125">**tooadd Pantheon dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6a14d-125">**tooadd Pantheon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a14d-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6a14d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6a14d-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6a14d-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="6a14d-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6a14d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="6a14d-133">Nella casella di ricerca hello, digitare **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-133">In hello search box, type **Pantheon**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="6a14d-135">Nel riquadro dei risultati hello, selezionare **Pantheon**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6a14d-135">In hello results panel, select **Pantheon**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6a14d-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a14d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6a14d-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Pantheon con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6a14d-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6a14d-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Pantheon è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a14d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pantheon is tooa user in Azure AD.</span></span> <span data-ttu-id="6a14d-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Pantheon deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="6a14d-140">In other words, a link relationship between an Azure AD user and hello related user in Pantheon needs toobe established.</span></span>

<span data-ttu-id="6a14d-141">In Pantheon, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="6a14d-141">In Pantheon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6a14d-142">tooconfigure e prova AD Azure single sign-on con Pantheon, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="6a14d-142">tooconfigure and test Azure AD single sign-on with Pantheon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6a14d-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6a14d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6a14d-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a14d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a14d-145">**[Creazione di un utente test Pantheon](#creating-a-pantheon-test-user)**  -toohave un equivalente di Britta Simon in Pantheon che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6a14d-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - toohave a counterpart of Britta Simon in Pantheon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a14d-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6a14d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a14d-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="6a14d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6a14d-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a14d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6a14d-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Pantheon.</span><span class="sxs-lookup"><span data-stu-id="6a14d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="6a14d-150">**Azure AD tooconfigure single sign-on con Pantheon, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6a14d-150">**tooconfigure Azure AD single sign-on with Pantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a14d-151">Nel portale di Azure su hello hello **Pantheon** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-151">In hello Azure portal, on hello **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="6a14d-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6a14d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="6a14d-155">In hello **Pantheon dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6a14d-155">On hello **Pantheon Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="6a14d-157">a.</span><span class="sxs-lookup"><span data-stu-id="6a14d-157">a.</span></span> <span data-ttu-id="6a14d-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="6a14d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="6a14d-159">b.</span><span class="sxs-lookup"><span data-stu-id="6a14d-159">b.</span></span> <span data-ttu-id="6a14d-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="6a14d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6a14d-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="6a14d-161">These values are not real.</span></span> <span data-ttu-id="6a14d-162">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="6a14d-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="6a14d-163">Contatto [team di supporto Pantheon](https://pantheon.io/docs/getting-support/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="6a14d-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) tooget these values.</span></span>

4. <span data-ttu-id="6a14d-164">Applicazione di pantheon prevede l'asserzione SAML hello in un formato specifico, che richiede di tooset hello idutente valore dell'attributo con l'indirizzo di posta elettronica dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="6a14d-164">Pantheon application expects hello SAML assertion in specific format, which requires you tooset hello UserIdentifier attribute value with hello user’s email address.</span></span> <span data-ttu-id="6a14d-165">Per impostazione predefinita AD Azure utilizza hello UserPrincipalName idutente attributo.</span><span class="sxs-lookup"><span data-stu-id="6a14d-165">By default Azure AD uses hello UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="6a14d-166">Ma per una corretta integrazione necessario tooadjust toomatch questo valore con l'indirizzo di posta elettronica dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6a14d-166">But for successful integration you need tooadjust this value toomatch with user’s email address.</span></span> <span data-ttu-id="6a14d-167">integrazione di Hello funziona solo dopo aver eseguito il mapping corretto hello.</span><span class="sxs-lookup"><span data-stu-id="6a14d-167">hello integration will only work after doing hello correct mapping.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="6a14d-169">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="6a14d-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="6a14d-171">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="6a14d-171">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6a14d-173">In hello **Pantheon configurazione** fare clic su **configurare Pantheon** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="6a14d-173">On hello **Pantheon Configuration** section, click **Configure Pantheon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6a14d-174">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="6a14d-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="6a14d-176">tooconfigure single sign-on sul **Pantheon** lato, è necessario hello toosend scaricato **certificato** e **SAML Single Sign-On Service URL** troppo[Pantheon team di supporto](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="6a14d-176">tooconfigure single sign-on on **Pantheon** side, you need toosend hello downloaded **Certificate** and **SAML Single Sign-On Service URL** too[Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="6a14d-177">È inoltre necessario tooprovide hello domini di posta elettronica e il tempo di Date quando si desidera tooenable questa connessione.</span><span class="sxs-lookup"><span data-stu-id="6a14d-177">You also need tooprovide hello Email Domain(s) information and Date Time when you want tooenable this connection.</span></span> <span data-ttu-id="6a14d-178">Per informazioni più dettagliate, vedere [qui](https://pantheon.io/docs/sso-organizations/).</span><span class="sxs-lookup"><span data-stu-id="6a14d-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="6a14d-179">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="6a14d-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6a14d-180">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="6a14d-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6a14d-181">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6a14d-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6a14d-182">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a14d-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="6a14d-183">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6a14d-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="6a14d-185">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6a14d-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a14d-186">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="6a14d-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6a14d-188">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6a14d-190">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="6a14d-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6a14d-192">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6a14d-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6a14d-194">a.</span><span class="sxs-lookup"><span data-stu-id="6a14d-194">a.</span></span> <span data-ttu-id="6a14d-195">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a14d-196">b.</span><span class="sxs-lookup"><span data-stu-id="6a14d-196">b.</span></span> <span data-ttu-id="6a14d-197">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6a14d-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6a14d-198">c.</span><span class="sxs-lookup"><span data-stu-id="6a14d-198">c.</span></span> <span data-ttu-id="6a14d-199">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6a14d-200">d.</span><span class="sxs-lookup"><span data-stu-id="6a14d-200">d.</span></span> <span data-ttu-id="6a14d-201">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="6a14d-202">Creazione di un utente di test di Pantheon</span><span class="sxs-lookup"><span data-stu-id="6a14d-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="6a14d-203">In questa sezione viene creato un utente di nome Britta Simon in Pantheon.</span><span class="sxs-lookup"><span data-stu-id="6a14d-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="6a14d-204">Seguire hello seguito passaggi tooadd hello utente Pantheon.</span><span class="sxs-lookup"><span data-stu-id="6a14d-204">Please follow hello below steps tooadd hello user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="6a14d-205">Per SSO toowork utente deve innanzitutto creato in Pantheon toobe.</span><span class="sxs-lookup"><span data-stu-id="6a14d-205">For SSO toowork user needs toobe created first in Pantheon.</span></span>

1. <span data-ttu-id="6a14d-206">TooPantheon di account di accesso con credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="6a14d-206">Login tooPantheon with admin credentials.</span></span>

2. <span data-ttu-id="6a14d-207">Passare troppo**organizzazione** pagina dashboard.</span><span class="sxs-lookup"><span data-stu-id="6a14d-207">Navigate too**Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="6a14d-208">Fare clic su **Persone**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-208">Click **People**.</span></span>

4. <span data-ttu-id="6a14d-209">Fare clic su **Add User**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-209">Click **Add user**.</span></span>

5. <span data-ttu-id="6a14d-210">Immettere l'indirizzo di posta elettronica dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="6a14d-210">Enter hello user's email address.</span></span>

6. <span data-ttu-id="6a14d-211">Scegliere hello del ruolo utente.</span><span class="sxs-lookup"><span data-stu-id="6a14d-211">Choose hello user's role.</span></span>

7. <span data-ttu-id="6a14d-212">Fare clic su **Add User**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-212">Click **Add user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6a14d-213">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a14d-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6a14d-214">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooPantheon.</span><span class="sxs-lookup"><span data-stu-id="6a14d-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPantheon.</span></span>

![Assegna utente][200] 

<span data-ttu-id="6a14d-216">**tooassign Britta Simon tooPantheon, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="6a14d-216">**tooassign Britta Simon tooPantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a14d-217">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="6a14d-219">Nell'elenco di applicazioni hello, selezionare **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-219">In hello applications list, select **Pantheon**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="6a14d-221">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="6a14d-223">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-223">Click **Add** button.</span></span> <span data-ttu-id="6a14d-224">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="6a14d-226">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="6a14d-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6a14d-227">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a14d-228">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="6a14d-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6a14d-229">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="6a14d-229">Testing single sign-on</span></span>

<span data-ttu-id="6a14d-230">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="6a14d-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6a14d-231">Quando si fa clic su riquadro Pantheon hello in hello Pannello di accesso, è necessario ottenere applicazione Pantheon tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="6a14d-231">When you click hello Pantheon tile in hello Access Panel, you should get automatically signed-on tooyour Pantheon application.</span></span>
<span data-ttu-id="6a14d-232">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6a14d-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6a14d-233">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="6a14d-233">Additional resources</span></span>

* [<span data-ttu-id="6a14d-234">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a14d-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a14d-235">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a14d-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

