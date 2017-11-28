---
title: 'Esercitazione: Integrazione di Azure Active Directory con eDigitalResearch | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory ed eDigitalResearch.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 6dd3cafb25ef8ede3a4c16902ed8da69cb7b715f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="0c12c-103">Esercitazione: Integrazione di Azure Active Directory con eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="0c12c-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="0c12c-104">In questa esercitazione, è illustrato come eDigitalResearch toointegrate con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0c12c-104">In this tutorial, you learn how toointegrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0c12c-105">Integrazione eDigitalResearch con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="0c12c-105">Integrating eDigitalResearch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0c12c-106">È possibile controllare in Azure AD che ha accesso tooeDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="0c12c-106">You can control in Azure AD who has access tooeDigitalResearch.</span></span>
- <span data-ttu-id="0c12c-107">È possibile abilitare l'utenti tooautomatically get connesso tooeDigitalResearch (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c12c-107">You can enable your users tooautomatically get signed-on tooeDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0c12c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c12c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="0c12c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0c12c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c12c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0c12c-110">Prerequisites</span></span>

<span data-ttu-id="0c12c-111">integrazione di Azure AD con eDigitalResearch tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="0c12c-111">tooconfigure Azure AD integration with eDigitalResearch, you need hello following items:</span></span>

- <span data-ttu-id="0c12c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c12c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0c12c-113">Sottoscrizione di eDigitalResearch abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0c12c-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0c12c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="0c12c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0c12c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="0c12c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0c12c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="0c12c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0c12c-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c12c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0c12c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="0c12c-118">Scenario description</span></span>
<span data-ttu-id="0c12c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="0c12c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0c12c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="0c12c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0c12c-121">Aggiunta di eDigitalResearch dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0c12c-121">Adding eDigitalResearch from hello gallery</span></span>
2. <span data-ttu-id="0c12c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c12c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-hello-gallery"></a><span data-ttu-id="0c12c-123">Aggiunta di eDigitalResearch dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="0c12c-123">Adding eDigitalResearch from hello gallery</span></span>
<span data-ttu-id="0c12c-124">integrazione hello tooconfigure di eDigitalResearch in Azure AD, è necessario eDigitalResearch tooadd dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="0c12c-124">tooconfigure hello integration of eDigitalResearch into Azure AD, you need tooadd eDigitalResearch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0c12c-125">**eDigitalResearch tooadd dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0c12c-125">**tooadd eDigitalResearch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c12c-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="0c12c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="0c12c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="0c12c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0c12c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0c12c-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="0c12c-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0c12c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="0c12c-133">Nella casella di ricerca hello, digitare **eDigitalResearch**selezionare **eDigitalResearch** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0c12c-133">In hello search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0c12c-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c12c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0c12c-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con eDigitalResearch usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0c12c-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0c12c-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in eDigitalResearch è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c12c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eDigitalResearch is tooa user in Azure AD.</span></span> <span data-ttu-id="0c12c-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in eDigitalResearch deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="0c12c-138">In other words, a link relationship between an Azure AD user and hello related user in eDigitalResearch needs toobe established.</span></span>

<span data-ttu-id="0c12c-139">In eDigitalResearch, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="0c12c-139">In eDigitalResearch, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0c12c-140">tooconfigure e prova AD Azure single sign-on con eDigitalResearch, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="0c12c-140">tooconfigure and test Azure AD single sign-on with eDigitalResearch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0c12c-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="0c12c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0c12c-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c12c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0c12c-143">**[Creare un utente test eDigitalResearch](#create-a-edigitalresearch-test-user)**  -toohave un equivalente di Britta Simon in eDigitalResearch che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0c12c-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - toohave a counterpart of Britta Simon in eDigitalResearch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0c12c-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0c12c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0c12c-145">**[Testare single sign-on](#test-single-sign-on)**  tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="0c12c-145">**[Test single sign-on](#test-single-sign-on)**  tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0c12c-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c12c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0c12c-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="0c12c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="0c12c-148">**Azure AD tooconfigure single sign-on con eDigitalResearch, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0c12c-148">**tooconfigure Azure AD single sign-on with eDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c12c-149">Nel portale di Azure su hello hello **eDigitalResearch** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0c12c-149">In hello Azure portal, on hello **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="0c12c-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0c12c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. <span data-ttu-id="0c12c-153">In hello **eDigitalResearch dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0c12c-153">On hello **eDigitalResearch Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni sul Single Sign-On di URL e dominio di eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="0c12c-155">a.</span><span class="sxs-lookup"><span data-stu-id="0c12c-155">a.</span></span> <span data-ttu-id="0c12c-156">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="0c12c-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="0c12c-157">b.</span><span class="sxs-lookup"><span data-stu-id="0c12c-157">b.</span></span> <span data-ttu-id="0c12c-158">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company-name>.edigitalresearch.com/login/consume`</span><span class="sxs-lookup"><span data-stu-id="0c12c-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0c12c-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="0c12c-159">These values are not real.</span></span> <span data-ttu-id="0c12c-160">Aggiornare questi valori con URL di risposta e identificatore effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="0c12c-160">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="0c12c-161">Contatto [team di supporto eDigitalResearch](http://www.maruedr.com/contact) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="0c12c-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) tooget these values.</span></span>
 


4. <span data-ttu-id="0c12c-162">In hello **certificato di firma SAML** fare clic su **Base(64) certificato** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="0c12c-162">On hello **SAML Signing Certificate** section, click **Certificate Base(64)** and then save hello certificate file on your computer.</span></span>

    <span data-ttu-id="0c12c-163">!</span><span class="sxs-lookup"><span data-stu-id="0c12c-163">!</span></span>![collegamento al download del certificato Hello](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. <span data-ttu-id="0c12c-165">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="0c12c-165">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0c12c-167">In hello **eDigitalResearch configurazione** fare clic su **configurare eDigitalResearch** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="0c12c-167">On hello **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0c12c-168">Hello copia **Sign-Out URL, ID entità SAML** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="0c12c-168">Copy hello **Sign-Out URL, SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurazione di eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. <span data-ttu-id="0c12c-170">tooconfigure single sign-on sul **eDigitalResearch** lato, è necessario hello toosend scaricato **File di certificato (Base64)**, **ID entità SAML**, e  **URL di disconnessione** troppo[team di supporto eDigitalResearch](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="0c12c-170">tooconfigure single sign-on on **eDigitalResearch** side, you need toosend hello downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** too[eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="0c12c-171">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="0c12c-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0c12c-172">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="0c12c-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0c12c-173">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="0c12c-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0c12c-174">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0c12c-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0c12c-175">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c12c-175">Create an Azure AD test user</span></span>

<span data-ttu-id="0c12c-176">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0c12c-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="0c12c-178">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0c12c-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c12c-179">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="0c12c-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0c12c-181">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="0c12c-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0c12c-183">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0c12c-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0c12c-185">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="0c12c-185">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0c12c-187">a.</span><span class="sxs-lookup"><span data-stu-id="0c12c-187">a.</span></span> <span data-ttu-id="0c12c-188">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0c12c-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0c12c-189">b.</span><span class="sxs-lookup"><span data-stu-id="0c12c-189">b.</span></span> <span data-ttu-id="0c12c-190">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c12c-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="0c12c-191">c.</span><span class="sxs-lookup"><span data-stu-id="0c12c-191">c.</span></span> <span data-ttu-id="0c12c-192">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="0c12c-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="0c12c-193">d.</span><span class="sxs-lookup"><span data-stu-id="0c12c-193">d.</span></span> <span data-ttu-id="0c12c-194">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0c12c-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="0c12c-195">Creare un utente test di eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="0c12c-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="0c12c-196">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in eDigitalResearch toocreate.</span><span class="sxs-lookup"><span data-stu-id="0c12c-196">hello objective of this section is toocreate a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="0c12c-197">Lavorare con hello [team di supporto eDigitalResearch](http://www.maruedr.com/contact) tooget utenti creati.</span><span class="sxs-lookup"><span data-stu-id="0c12c-197">Work with hello [eDigitalResearch support team](http://www.maruedr.com/contact) tooget users created.</span></span>       
    
 > [!NOTE]
 > <span data-ttu-id="0c12c-198">titolare dell'account di Azure Active Directory Hello riceve un messaggio di posta elettronica e segue il proprio account tooconfirm un collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="0c12c-198">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0c12c-199">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c12c-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0c12c-200">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooeDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="0c12c-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeDigitalResearch.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="0c12c-202">**tooassign Britta Simon tooeDigitalResearch, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="0c12c-202">**tooassign Britta Simon tooeDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c12c-203">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="0c12c-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="0c12c-205">Nell'elenco di applicazioni hello, selezionare **eDigitalResearch**.</span><span class="sxs-lookup"><span data-stu-id="0c12c-205">In hello applications list, select **eDigitalResearch**.</span></span>

    ![Hello eDigitalResearch collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. <span data-ttu-id="0c12c-207">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0c12c-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="0c12c-209">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0c12c-209">Click **Add** button.</span></span> <span data-ttu-id="0c12c-210">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0c12c-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="0c12c-212">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="0c12c-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0c12c-213">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="0c12c-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0c12c-214">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="0c12c-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0c12c-215">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="0c12c-215">Test single sign-on</span></span>

<span data-ttu-id="0c12c-216">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="0c12c-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0c12c-217">Quando si fa clic su riquadro eDigitalResearch hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour eDigitalResearch applicazione.</span><span class="sxs-lookup"><span data-stu-id="0c12c-217">When you click hello eDigitalResearch tile in hello Access Panel, you should get automatically signed-on tooyour eDigitalResearch application.</span></span>
<span data-ttu-id="0c12c-218">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0c12c-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0c12c-219">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="0c12c-219">Additional resources</span></span>

* [<span data-ttu-id="0c12c-220">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c12c-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0c12c-221">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c12c-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png

