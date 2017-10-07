---
title: 'Esercitazione: Integrazione di Azure Active Directory con Bonusly | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Bonusly.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="ad4de-103">Esercitazione: Integrazione di Azure Active Directory con Bonusly</span><span class="sxs-lookup"><span data-stu-id="ad4de-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="ad4de-104">In questa esercitazione, è illustrato come toointegrate Bonusly con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad4de-104">In this tutorial, you learn how toointegrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad4de-105">Integrazione Bonusly con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="ad4de-105">Integrating Bonusly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ad4de-106">È possibile controllare in Azure AD che ha accesso tooBonusly</span><span class="sxs-lookup"><span data-stu-id="ad4de-106">You can control in Azure AD who has access tooBonusly</span></span>
- <span data-ttu-id="ad4de-107">È possibile abilitare l'utenti tooautomatically get connesso tooBonusly (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad4de-107">You can enable your users tooautomatically get signed-on tooBonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ad4de-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ad4de-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ad4de-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad4de-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad4de-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ad4de-110">Prerequisites</span></span>

<span data-ttu-id="ad4de-111">integrazione di Azure AD con Bonusly tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="ad4de-111">tooconfigure Azure AD integration with Bonusly, you need hello following items:</span></span>

- <span data-ttu-id="ad4de-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad4de-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad4de-113">Sottoscrizione di Bonusly abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ad4de-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad4de-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="ad4de-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad4de-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="ad4de-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad4de-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="ad4de-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ad4de-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad4de-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad4de-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="ad4de-118">Scenario description</span></span>
<span data-ttu-id="ad4de-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="ad4de-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad4de-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="ad4de-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad4de-121">Aggiunta di Bonusly dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ad4de-121">Adding Bonusly from hello gallery</span></span>
2. <span data-ttu-id="ad4de-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad4de-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-hello-gallery"></a><span data-ttu-id="ad4de-123">Aggiunta di Bonusly dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="ad4de-123">Adding Bonusly from hello gallery</span></span>
<span data-ttu-id="ad4de-124">integrazione hello tooconfigure di Bonusly in Azure AD, è necessario tooadd Bonusly dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="ad4de-124">tooconfigure hello integration of Bonusly into Azure AD, you need tooadd Bonusly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ad4de-125">**tooadd Bonusly dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ad4de-125">**tooadd Bonusly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad4de-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ad4de-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="ad4de-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ad4de-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="ad4de-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ad4de-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="ad4de-133">Nella casella di ricerca hello, digitare **Bonusly**selezionare **Bonusly** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ad4de-133">In hello search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ad4de-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad4de-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ad4de-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Bonusly usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ad4de-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ad4de-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Bonusly è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad4de-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bonusly is tooa user in Azure AD.</span></span> <span data-ttu-id="ad4de-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Bonusly deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="ad4de-138">In other words, a link relationship between an Azure AD user and hello related user in Bonusly needs toobe established.</span></span>

<span data-ttu-id="ad4de-139">In Bonusly, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="ad4de-139">In Bonusly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ad4de-140">tooconfigure e prova AD Azure single sign-on con Bonusly, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="ad4de-140">tooconfigure and test Azure AD single sign-on with Bonusly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ad4de-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ad4de-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ad4de-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad4de-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad4de-143">**[Creare un utente test Bonusly](#create-a-bonusly-test-user)**  -toohave un equivalente di Britta Simon in Bonusly che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ad4de-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - toohave a counterpart of Britta Simon in Bonusly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ad4de-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ad4de-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad4de-145">**[Testare Single Sign-On](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="ad4de-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ad4de-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad4de-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ad4de-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Bonusly.</span><span class="sxs-lookup"><span data-stu-id="ad4de-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="ad4de-148">**Azure AD tooconfigure single sign-on con Bonusly, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ad4de-148">**tooconfigure Azure AD single sign-on with Bonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad4de-149">Nel portale di Azure su hello hello **Bonusly** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-149">In hello Azure portal, on hello **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="ad4de-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ad4de-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="ad4de-153">In hello **Bonusly dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ad4de-153">On hello **Bonusly Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="ad4de-155">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="ad4de-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ad4de-156">il valore di Hello non è di tipo real.</span><span class="sxs-lookup"><span data-stu-id="ad4de-156">hello value is not real.</span></span> <span data-ttu-id="ad4de-157">Il valore di hello aggiornamento con hello URL di risposta effettivo.</span><span class="sxs-lookup"><span data-stu-id="ad4de-157">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="ad4de-158">Contatto [team di supporto Bonusly](https://Bonusly/contact) valore hello tooget.</span><span class="sxs-lookup"><span data-stu-id="ad4de-158">Contact [Bonusly support team](https://Bonusly/contact) tooget hello value.</span></span>
 
4. <span data-ttu-id="ad4de-159">In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore dal certificato hello.</span><span class="sxs-lookup"><span data-stu-id="ad4de-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="ad4de-161">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ad4de-161">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ad4de-163">In hello **configurazione Bonusly** fare clic su **configurare Bonusly** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="ad4de-163">On hello **Bonusly Configuration** section, click **Configure Bonusly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ad4de-164">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="ad4de-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="ad4de-166">In un'altra finestra del browser, accedere tooyour **Bonusly** tenant.</span><span class="sxs-lookup"><span data-stu-id="ad4de-166">In a different browser window, log in tooyour **Bonusly** tenant.</span></span>

8. <span data-ttu-id="ad4de-167">Nella barra degli strumenti hello in primo piano hello, fare clic su **impostazioni**, quindi selezionare **integrazioni e app**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-167">In hello toolbar on hello top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="ad4de-168">![Sezione Bonusly Social](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="ad4de-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="ad4de-169">In **Single Sign-On** selezionare **SAML**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="ad4de-170">In hello **SAML** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ad4de-170">On hello **SAML** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="ad4de-171">![Finestra di dialogo SAML per Bonusly](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="ad4de-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="ad4de-172">a.</span><span class="sxs-lookup"><span data-stu-id="ad4de-172">a.</span></span> <span data-ttu-id="ad4de-173">In hello **IdP SSO target URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad4de-173">In hello **IdP SSO target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="ad4de-174">b.</span><span class="sxs-lookup"><span data-stu-id="ad4de-174">b.</span></span> <span data-ttu-id="ad4de-175">In hello **IdP Issuer** casella di testo, hello Incolla valore **ID entità SAML**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad4de-175">In hello **IdP Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="ad4de-176">c.</span><span class="sxs-lookup"><span data-stu-id="ad4de-176">c.</span></span> <span data-ttu-id="ad4de-177">In hello **IdP Login URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad4de-177">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ad4de-178">d.</span><span class="sxs-lookup"><span data-stu-id="ad4de-178">d.</span></span> <span data-ttu-id="ad4de-179">Incolla il **identificazione personale** valore copiato dal portale di Azure in hello **Cert Fingerprint** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ad4de-179">Paste the **Thumbprint** value copied from Azure portal into hello **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="ad4de-180">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ad4de-181">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="ad4de-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ad4de-182">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="ad4de-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ad4de-183">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ad4de-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ad4de-184">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad4de-184">Create an Azure AD test user</span></span>
<span data-ttu-id="ad4de-185">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ad4de-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="ad4de-187">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ad4de-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad4de-188">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="ad4de-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ad4de-190">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ad4de-192">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="ad4de-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![pulsante Aggiungi Hello](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ad4de-194">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ad4de-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![finestra di dialogo utente Hello](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad4de-196">a.</span><span class="sxs-lookup"><span data-stu-id="ad4de-196">a.</span></span> <span data-ttu-id="ad4de-197">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad4de-198">b.</span><span class="sxs-lookup"><span data-stu-id="ad4de-198">b.</span></span> <span data-ttu-id="ad4de-199">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ad4de-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad4de-200">c.</span><span class="sxs-lookup"><span data-stu-id="ad4de-200">c.</span></span> <span data-ttu-id="ad4de-201">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ad4de-202">d.</span><span class="sxs-lookup"><span data-stu-id="ad4de-202">d.</span></span> <span data-ttu-id="ad4de-203">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="ad4de-204">Creare un utente di test di Bonusly</span><span class="sxs-lookup"><span data-stu-id="ad4de-204">Create a Bonusly test user</span></span>

<span data-ttu-id="ad4de-205">In ordine tooenable Azure AD utenti toolog in tooBonusly, è necessario eseguirne il provisioning in Bonusly.</span><span class="sxs-lookup"><span data-stu-id="ad4de-205">In order tooenable Azure AD users toolog in tooBonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="ad4de-206">Nel caso di hello di Bonusly, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="ad4de-206">In hello case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="ad4de-207">È possibile usare qualsiasi altro strumento di creazione utente Bonusly account o le API fornite da tooprovision Bonusly AAD gli account utente.</span><span class="sxs-lookup"><span data-stu-id="ad4de-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly tooprovision AAD user accounts.</span></span>
>  

<span data-ttu-id="ad4de-208">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ad4de-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad4de-209">In una finestra del web browser accedere tooyour Bonusly tenant.</span><span class="sxs-lookup"><span data-stu-id="ad4de-209">In a web browser window, log in tooyour Bonusly tenant.</span></span>

2. <span data-ttu-id="ad4de-210">Fare clic su **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="ad4de-211">![Impostazioni](./media/active-directory-saas-bonus-tutorial/ic781041.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="ad4de-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="ad4de-212">Fare clic su hello **utenti e bonus** scheda.</span><span class="sxs-lookup"><span data-stu-id="ad4de-212">Click hello **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="ad4de-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span><span class="sxs-lookup"><span data-stu-id="ad4de-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="ad4de-214">Fare clic su **Gestisci utenti**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="ad4de-215">![Gestione utenti](./media/active-directory-saas-bonus-tutorial/ic781043.png "Gestione utenti")</span><span class="sxs-lookup"><span data-stu-id="ad4de-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="ad4de-216">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="ad4de-217">![Aggiungere un utente](./media/active-directory-saas-bonus-tutorial/ic781044.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="ad4de-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="ad4de-218">In hello **Aggiungi utente** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ad4de-218">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="ad4de-219">![Aggiungere un utente](./media/active-directory-saas-bonus-tutorial/ic781045.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="ad4de-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="ad4de-220">a.</span><span class="sxs-lookup"><span data-stu-id="ad4de-220">a.</span></span> <span data-ttu-id="ad4de-221">In hello **nome** casella di testo, immettere nome hello dell'utente come **Laura**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-221">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="ad4de-222">b.</span><span class="sxs-lookup"><span data-stu-id="ad4de-222">b.</span></span> <span data-ttu-id="ad4de-223">In hello **cognome** casella di testo immettere hello cognome dell'utente come **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-223">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="ad4de-224">c.</span><span class="sxs-lookup"><span data-stu-id="ad4de-224">c.</span></span> <span data-ttu-id="ad4de-225">In hello **posta elettronica** casella di testo immettere hello email dell'utente come  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ad4de-225">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="ad4de-226">d.</span><span class="sxs-lookup"><span data-stu-id="ad4de-226">d.</span></span> <span data-ttu-id="ad4de-227">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="ad4de-228">titolare dell'account di Azure AD Hello riceve un messaggio di posta elettronica che include un account di hello tooconfirm collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="ad4de-228">hello Azure AD account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span>
     >  

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ad4de-229">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad4de-229">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ad4de-230">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooBonusly.</span><span class="sxs-lookup"><span data-stu-id="ad4de-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBonusly.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="ad4de-232">**tooassign Britta Simon tooBonusly, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="ad4de-232">**tooassign Britta Simon tooBonusly, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad4de-233">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="ad4de-235">Nell'elenco di applicazioni hello, selezionare **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-235">In hello applications list, select **Bonusly**.</span></span>

    ![Hello Bonusly collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="ad4de-237">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202] 

4. <span data-ttu-id="ad4de-239">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-239">Click **Add** button.</span></span> <span data-ttu-id="ad4de-240">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="ad4de-242">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="ad4de-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ad4de-243">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad4de-244">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="ad4de-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ad4de-245">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ad4de-245">Test single sign-on</span></span>

<span data-ttu-id="ad4de-246">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="ad4de-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ad4de-247">Quando si fa clic sul riquadro Bonusly hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Bonusly applicazione.</span><span class="sxs-lookup"><span data-stu-id="ad4de-247">When you click hello Bonusly tile in hello Access Panel, you should get automatically signed-on tooyour Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad4de-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="ad4de-248">Additional resources</span></span>

* [<span data-ttu-id="ad4de-249">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad4de-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad4de-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad4de-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

