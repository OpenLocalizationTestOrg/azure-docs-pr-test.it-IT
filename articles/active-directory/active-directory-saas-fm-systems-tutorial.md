---
title: 'Esercitazione: Integrazione di Azure Active Directory con FM:Systems | Microsoft Docs'
description: 'Informazioni su come tooconfigure single sign-on tra Azure Active Directory e FM: Systems.'
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 677ef74dac663a43835d65a4d4f4fd031a0078cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="53c2f-103">Esercitazione: Integrazione di Azure Active Directory con FM:Systems</span><span class="sxs-lookup"><span data-stu-id="53c2f-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>

<span data-ttu-id="53c2f-104">In questa esercitazione, è illustrato come toointegrate FM: Systems con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="53c2f-104">In this tutorial, you learn how toointegrate FM:Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="53c2f-105">Integrazione di FM: Systems con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="53c2f-105">Integrating FM:Systems with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="53c2f-106">È possibile controllare in Azure AD che ha accesso tooFM:Systems</span><span class="sxs-lookup"><span data-stu-id="53c2f-106">You can control in Azure AD who has access tooFM:Systems</span></span>
- <span data-ttu-id="53c2f-107">È possibile abilitare l'utenti tooautomatically get connesso tooFM:Systems (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="53c2f-107">You can enable your users tooautomatically get signed-on tooFM:Systems (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="53c2f-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="53c2f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="53c2f-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="53c2f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53c2f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="53c2f-110">Prerequisites</span></span>

<span data-ttu-id="53c2f-111">integrazione di Azure AD con FM: Systems tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="53c2f-111">tooconfigure Azure AD integration with FM:Systems, you need hello following items:</span></span>

- <span data-ttu-id="53c2f-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53c2f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="53c2f-113">Sottoscrizione di FM:Systems abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="53c2f-113">An FM:Systems single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="53c2f-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="53c2f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="53c2f-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="53c2f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="53c2f-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="53c2f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="53c2f-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="53c2f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="53c2f-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="53c2f-118">Scenario description</span></span>
<span data-ttu-id="53c2f-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="53c2f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="53c2f-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="53c2f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="53c2f-121">Aggiunta di FM: Systems dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="53c2f-121">Adding FM:Systems from hello gallery</span></span>
2. <span data-ttu-id="53c2f-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="53c2f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fmsystems-from-hello-gallery"></a><span data-ttu-id="53c2f-123">Aggiunta di FM: Systems dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="53c2f-123">Adding FM:Systems from hello gallery</span></span>
<span data-ttu-id="53c2f-124">integrazione hello tooconfigure di FM: Systems in Azure AD, è necessario tooadd FM: Systems dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="53c2f-124">tooconfigure hello integration of FM:Systems into Azure AD, you need tooadd FM:Systems from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="53c2f-125">**tooadd FM: Systems dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="53c2f-125">**tooadd FM:Systems from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="53c2f-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="53c2f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="53c2f-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="53c2f-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="53c2f-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="53c2f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="53c2f-133">Nella casella di ricerca hello, digitare **FM: Systems**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-133">In hello search box, type **FM:Systems**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_search.png)

5. <span data-ttu-id="53c2f-135">Nel riquadro dei risultati hello, selezionare **FM: Systems**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="53c2f-135">In hello results panel, select **FM:Systems**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="53c2f-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="53c2f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="53c2f-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con FM:Systems mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="53c2f-138">In this section, you configure and test Azure AD single sign-on with FM:Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="53c2f-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in FM: Systems è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53c2f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FM:Systems is tooa user in Azure AD.</span></span> <span data-ttu-id="53c2f-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in FM: Systems deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="53c2f-140">In other words, a link relationship between an Azure AD user and hello related user in FM:Systems needs toobe established.</span></span>

<span data-ttu-id="53c2f-141">In FM: Systems, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="53c2f-141">In FM:Systems, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="53c2f-142">tooconfigure e prova AD Azure single sign-on con FM: Systems, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="53c2f-142">tooconfigure and test Azure AD single sign-on with FM:Systems, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="53c2f-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="53c2f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="53c2f-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="53c2f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="53c2f-145">**[Creazione di un utente test FM: Systems](#creating-an-fmsystems-test-user)**  -toohave un equivalente di Britta Simon in FM: Systems che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="53c2f-145">**[Creating an FM:Systems test user](#creating-an-fmsystems-test-user)** - toohave a counterpart of Britta Simon in FM:Systems that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="53c2f-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="53c2f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="53c2f-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="53c2f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="53c2f-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="53c2f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="53c2f-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione FM: Systems.</span><span class="sxs-lookup"><span data-stu-id="53c2f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FM:Systems application.</span></span>

<span data-ttu-id="53c2f-150">**Azure AD tooconfigure single sign-on con FM: Systems, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="53c2f-150">**tooconfigure Azure AD single sign-on with FM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="53c2f-151">Nel portale di Azure su hello hello **FM: Systems** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-151">In hello Azure portal, on hello **FM:Systems** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="53c2f-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="53c2f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_samlbase.png)

3. <span data-ttu-id="53c2f-155">In hello **URL e il dominio di FM: Systems** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="53c2f-155">On hello **FM:Systems Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_url.png)

    <span data-ttu-id="53c2f-157">In hello **URL di risposta** casella di testo, digitare il FM: Systems **URL di risposta**, digitare l'URL hello utilizzando hello seguente motivo:`https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span><span class="sxs-lookup"><span data-stu-id="53c2f-157">In hello **Reply URL** textbox, type your FM:Systems **Reply URL**, type hello URL using hello following pattern: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="53c2f-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="53c2f-158">This value is not real.</span></span> <span data-ttu-id="53c2f-159">Aggiornare questo valore con l'URL di risposta effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="53c2f-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="53c2f-160">Contatto [team di supporto di FM: Systems](https://fmsystems.com/ask-us/) tooget questo valore.</span><span class="sxs-lookup"><span data-stu-id="53c2f-160">Contact [FM:Systems support team](https://fmsystems.com/ask-us/) tooget this value.</span></span>
 
4. <span data-ttu-id="53c2f-161">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="53c2f-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_certificate.png) 

5. <span data-ttu-id="53c2f-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="53c2f-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-fm-systems-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="53c2f-165">tooconfigure single sign-on sul **FM: Systems** lato, è necessario hello toosend scaricato **Metadata XML** troppo[team di supporto di FM: Systems](https://fmsystems.com/ask-us/).</span><span class="sxs-lookup"><span data-stu-id="53c2f-165">tooconfigure single sign-on on **FM:Systems** side, you need toosend hello downloaded **Metadata XML** too[FM:Systems support team](https://fmsystems.com/ask-us/).</span></span> <span data-ttu-id="53c2f-166">Impostano questo hello toohave impostazione connessione SAML SSO impostato correttamente su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="53c2f-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span> <span data-ttu-id="53c2f-167">Una volta completata l'abilitazione dell'accesso Single Sign-On per la sottoscrizione, si riceverà una notifica.</span><span class="sxs-lookup"><span data-stu-id="53c2f-167">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="53c2f-168">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="53c2f-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="53c2f-169">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="53c2f-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="53c2f-170">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="53c2f-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="53c2f-171">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="53c2f-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="53c2f-172">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="53c2f-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="53c2f-174">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="53c2f-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="53c2f-175">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="53c2f-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="53c2f-177">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="53c2f-179">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="53c2f-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="53c2f-181">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="53c2f-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="53c2f-183">a.</span><span class="sxs-lookup"><span data-stu-id="53c2f-183">a.</span></span> <span data-ttu-id="53c2f-184">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="53c2f-185">b.</span><span class="sxs-lookup"><span data-stu-id="53c2f-185">b.</span></span> <span data-ttu-id="53c2f-186">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="53c2f-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="53c2f-187">c.</span><span class="sxs-lookup"><span data-stu-id="53c2f-187">c.</span></span> <span data-ttu-id="53c2f-188">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="53c2f-189">d.</span><span class="sxs-lookup"><span data-stu-id="53c2f-189">d.</span></span> <span data-ttu-id="53c2f-190">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-190">Click **Create**.</span></span>
 
### <a name="creating-an-fmsystems-test-user"></a><span data-ttu-id="53c2f-191">Creazione di un utente test di FM:Systems</span><span class="sxs-lookup"><span data-stu-id="53c2f-191">Creating an FM:Systems test user</span></span>

1. <span data-ttu-id="53c2f-192">In una finestra del Web browser accedere al sito aziendale di FM:Systems come amministratore.</span><span class="sxs-lookup"><span data-stu-id="53c2f-192">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="53c2f-193">Andare troppo**Amministrazione sistema \> Gestisci sicurezza \> utenti \> elenco utenti**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-193">Go too**System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="53c2f-194">![Amministrazione del sistema](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "Amministrazione del sistema")</span><span class="sxs-lookup"><span data-stu-id="53c2f-194">![System Administration](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "System Administration")</span></span>

3. <span data-ttu-id="53c2f-195">Fare clic su **Crea nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-195">Click **Create new user**.</span></span>
   
    <span data-ttu-id="53c2f-196">![Creazione di un nuovo utente](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Creazione di un nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="53c2f-196">![Create New User](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Create New User")</span></span>

4. <span data-ttu-id="53c2f-197">In hello **Create User** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="53c2f-197">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="53c2f-198">![Crea utente](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Crea utente")</span><span class="sxs-lookup"><span data-stu-id="53c2f-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span></span>
   
    <span data-ttu-id="53c2f-199">a.</span><span class="sxs-lookup"><span data-stu-id="53c2f-199">a.</span></span> <span data-ttu-id="53c2f-200">Hello tipo **UserName**, hello **Password**, **Conferma Password**, **posta elettronica** e hello **ID dipendente**relative caselle di testo di un valido di Azure all'account di Active Directory desiderata tooprovision in hello.</span><span class="sxs-lookup"><span data-stu-id="53c2f-200">Type hello **UserName**, hello **Password**, **Confirm Password**, **E-mail** and hello **Employee ID** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="53c2f-201">b.</span><span class="sxs-lookup"><span data-stu-id="53c2f-201">b.</span></span> <span data-ttu-id="53c2f-202">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-202">Click **Next**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="53c2f-203">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="53c2f-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="53c2f-204">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooFM:Systems.</span><span class="sxs-lookup"><span data-stu-id="53c2f-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFM:Systems.</span></span>

![Assegna utente][200] 

<span data-ttu-id="53c2f-206">**tooassign Britta Simon tooFM:Systems, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="53c2f-206">**tooassign Britta Simon tooFM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="53c2f-207">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="53c2f-209">Nell'elenco di applicazioni hello, selezionare **FM: Systems**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-209">In hello applications list, select **FM:Systems**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_app.png) 

3. <span data-ttu-id="53c2f-211">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="53c2f-213">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-213">Click **Add** button.</span></span> <span data-ttu-id="53c2f-214">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="53c2f-216">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="53c2f-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="53c2f-217">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="53c2f-218">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="53c2f-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="53c2f-219">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="53c2f-219">Testing single sign-on</span></span>

<span data-ttu-id="53c2f-220">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="53c2f-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="53c2f-221">Quando si fa clic su riquadro FM: Systems hello in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in FM: Systems applicazione.</span><span class="sxs-lookup"><span data-stu-id="53c2f-221">When you click hello FM:Systems tile in hello Access Panel, you should get automatically signed-on tooyour FM:Systems application.</span></span>
<span data-ttu-id="53c2f-222">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="53c2f-222">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="53c2f-223">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="53c2f-223">Additional resources</span></span>

* [<span data-ttu-id="53c2f-224">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53c2f-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="53c2f-225">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53c2f-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_203.png

