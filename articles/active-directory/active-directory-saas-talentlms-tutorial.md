---
title: 'Esercitazione: Integrazione di Azure Active Directory con TalentLMS | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e TalentLMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 25538086602e58fbaab0fbf223f5b03908a74922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="65f0e-103">Esercitazione: Integrazione di Azure Active Directory con TalentLMS</span><span class="sxs-lookup"><span data-stu-id="65f0e-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="65f0e-104">In questa esercitazione, è illustrato come toointegrate TalentLMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65f0e-104">In this tutorial, you learn how toointegrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65f0e-105">Integrazione di TalentLMS con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="65f0e-105">Integrating TalentLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="65f0e-106">È possibile controllare in Azure AD che ha accesso tooTalentLMS</span><span class="sxs-lookup"><span data-stu-id="65f0e-106">You can control in Azure AD who has access tooTalentLMS</span></span>
- <span data-ttu-id="65f0e-107">È possibile abilitare l'utenti tooautomatically get connesso tooTalentLMS (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="65f0e-107">You can enable your users tooautomatically get signed-on tooTalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65f0e-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="65f0e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="65f0e-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="65f0e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65f0e-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="65f0e-110">Prerequisites</span></span>

<span data-ttu-id="65f0e-111">integrazione di Azure AD con TalentLMS tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="65f0e-111">tooconfigure Azure AD integration with TalentLMS, you need hello following items:</span></span>

- <span data-ttu-id="65f0e-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65f0e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65f0e-113">Sottoscrizione di TalentLMS abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="65f0e-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65f0e-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="65f0e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65f0e-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="65f0e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65f0e-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="65f0e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65f0e-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65f0e-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65f0e-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="65f0e-118">Scenario description</span></span>
<span data-ttu-id="65f0e-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="65f0e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65f0e-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="65f0e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65f0e-121">Aggiunta di TalentLMS dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="65f0e-121">Adding TalentLMS from hello gallery</span></span>
2. <span data-ttu-id="65f0e-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="65f0e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-hello-gallery"></a><span data-ttu-id="65f0e-123">Aggiunta di TalentLMS dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="65f0e-123">Adding TalentLMS from hello gallery</span></span>
<span data-ttu-id="65f0e-124">integrazione hello tooconfigure di TalentLMS in Azure AD, è necessario tooadd TalentLMS dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="65f0e-124">tooconfigure hello integration of TalentLMS into Azure AD, you need tooadd TalentLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="65f0e-125">**tooadd TalentLMS dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="65f0e-125">**tooadd TalentLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="65f0e-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="65f0e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65f0e-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="65f0e-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="65f0e-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="65f0e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="65f0e-133">Nella casella di ricerca hello, digitare **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-133">In hello search box, type **TalentLMS**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="65f0e-135">Nel riquadro dei risultati hello, selezionare **TalentLMS**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="65f0e-135">In hello results panel, select **TalentLMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65f0e-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="65f0e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65f0e-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TalentLMS usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="65f0e-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="65f0e-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in TalentLMS è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65f0e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TalentLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="65f0e-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in TalentLMS richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="65f0e-140">In other words, a link relationship between an Azure AD user and hello related user in TalentLMS needs toobe established.</span></span>

<span data-ttu-id="65f0e-141">In TalentLMS, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="65f0e-141">In TalentLMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="65f0e-142">tooconfigure e test Azure single sign-on AD con TalentLMS, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="65f0e-142">tooconfigure and test Azure AD single sign-on with TalentLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="65f0e-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="65f0e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="65f0e-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65f0e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65f0e-145">**[Creazione di un utente test TalentLMS](#creating-a-talentlms-test-user)**  -toohave un equivalente di Britta Simon in TalentLMS che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="65f0e-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - toohave a counterpart of Britta Simon in TalentLMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="65f0e-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="65f0e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65f0e-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="65f0e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65f0e-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="65f0e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65f0e-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="65f0e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="65f0e-150">**Azure AD tooconfigure single sign-on con TalentLMS, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="65f0e-150">**tooconfigure Azure AD single sign-on with TalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="65f0e-151">Nel portale di Azure su hello hello **TalentLMS** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-151">In hello Azure portal, on hello **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="65f0e-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="65f0e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="65f0e-155">In hello **TalentLMS dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="65f0e-155">On hello **TalentLMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="65f0e-157">a.</span><span class="sxs-lookup"><span data-stu-id="65f0e-157">a.</span></span> <span data-ttu-id="65f0e-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="65f0e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="65f0e-159">b.</span><span class="sxs-lookup"><span data-stu-id="65f0e-159">b.</span></span> <span data-ttu-id="65f0e-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="65f0e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="65f0e-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="65f0e-161">These values are not real.</span></span> <span data-ttu-id="65f0e-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="65f0e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="65f0e-163">Contatto [team di supporto Client di TalentLMS](https://www.talentlms.com/contact) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="65f0e-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="65f0e-164">In hello **certificato di firma SAML** sezione, hello copia **identificazione personale** valore dal certificato hello.</span><span class="sxs-lookup"><span data-stu-id="65f0e-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="65f0e-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="65f0e-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65f0e-168">In hello **TalentLMS configurazione** fare clic su **configurare TalentLMS** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="65f0e-168">On hello **TalentLMS Configuration** section, click **Configure TalentLMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="65f0e-169">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="65f0e-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="65f0e-171">In una finestra del web browser, accedere come amministratore nel sito aziendale TalentLMS di tooyour.</span><span class="sxs-lookup"><span data-stu-id="65f0e-171">In a different web browser window, log in tooyour TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="65f0e-172">In hello **Account e impostazioni** fare clic su hello **utenti** scheda.</span><span class="sxs-lookup"><span data-stu-id="65f0e-172">In hello **Account & Settings** section, click hello **Users** tab.</span></span>
   
    <span data-ttu-id="65f0e-173">![Impostazioni e account](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Impostazioni e account")</span><span class="sxs-lookup"><span data-stu-id="65f0e-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="65f0e-174">Fare clic su **Single Sign-On (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="65f0e-175">Nella sezione Single Sign-On hello, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="65f0e-175">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="65f0e-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="65f0e-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="65f0e-177">a.</span><span class="sxs-lookup"><span data-stu-id="65f0e-177">a.</span></span> <span data-ttu-id="65f0e-178">Da hello **il tipo di integrazione di SSO** elenco, selezionare **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-178">From hello **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="65f0e-179">b.</span><span class="sxs-lookup"><span data-stu-id="65f0e-179">b.</span></span> <span data-ttu-id="65f0e-180">In hello **il provider di identità (IDP)** casella di testo, hello Incolla valore **ID entità SAML**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="65f0e-180">In hello **Identity provider (IDP)** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="65f0e-181">c.</span><span class="sxs-lookup"><span data-stu-id="65f0e-181">c.</span></span> <span data-ttu-id="65f0e-182">Hello Incolla **identificazione personale** valore dal portale di Azure in hello **Certificate fingerprint** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="65f0e-182">Paste hello **Thumbprint** value from Azure portal into hello **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="65f0e-183">d.</span><span class="sxs-lookup"><span data-stu-id="65f0e-183">d.</span></span>  <span data-ttu-id="65f0e-184">In hello **URL di accesso remoto** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="65f0e-184">In hello **Remote sign-in URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="65f0e-185">e.</span><span class="sxs-lookup"><span data-stu-id="65f0e-185">e.</span></span> <span data-ttu-id="65f0e-186">In hello **URL disconnessione remota** casella di testo, hello Incolla valore **Sign-Out URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="65f0e-186">In hello **Remote sign-out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="65f0e-187">f.</span><span class="sxs-lookup"><span data-stu-id="65f0e-187">f.</span></span> <span data-ttu-id="65f0e-188">Compilare il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="65f0e-188">Fill in hello following:</span></span> 

    * <span data-ttu-id="65f0e-189">In hello **TargetedID** casella di testo, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="65f0e-189">In hello **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="65f0e-190">In hello **nome** casella di testo, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="65f0e-190">In hello **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="65f0e-191">In hello **cognome** casella di testo, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="65f0e-191">In hello **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="65f0e-192">In hello **posta elettronica** casella di testo, tipo`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="65f0e-192">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="65f0e-193">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="65f0e-194">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="65f0e-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="65f0e-195">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="65f0e-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="65f0e-196">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65f0e-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65f0e-197">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="65f0e-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="65f0e-198">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="65f0e-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="65f0e-200">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="65f0e-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="65f0e-201">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="65f0e-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65f0e-203">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65f0e-205">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="65f0e-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65f0e-207">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="65f0e-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65f0e-209">a.</span><span class="sxs-lookup"><span data-stu-id="65f0e-209">a.</span></span> <span data-ttu-id="65f0e-210">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65f0e-211">b.</span><span class="sxs-lookup"><span data-stu-id="65f0e-211">b.</span></span> <span data-ttu-id="65f0e-212">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="65f0e-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65f0e-213">c.</span><span class="sxs-lookup"><span data-stu-id="65f0e-213">c.</span></span> <span data-ttu-id="65f0e-214">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="65f0e-215">d.</span><span class="sxs-lookup"><span data-stu-id="65f0e-215">d.</span></span> <span data-ttu-id="65f0e-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="65f0e-217">Creazione di un utente test di TalentLMS</span><span class="sxs-lookup"><span data-stu-id="65f0e-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="65f0e-218">toolog agli utenti di Azure AD tooenable in tooTalentLMS, è necessario eseguirne il provisioning in TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="65f0e-218">tooenable Azure AD users toolog in tooTalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="65f0e-219">Nel caso di hello di TalentLMS, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="65f0e-219">In hello case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="65f0e-220">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="65f0e-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="65f0e-221">Accedi tooyour **TalentLMS** tenant.</span><span class="sxs-lookup"><span data-stu-id="65f0e-221">Log in tooyour **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="65f0e-222">Fare clic su **Users** (Utenti), quindi fare clic su **Add User** (Aggiungi utente).</span><span class="sxs-lookup"><span data-stu-id="65f0e-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="65f0e-223">In hello **Aggiungi utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="65f0e-223">On hello **Add user** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="65f0e-224">![Aggiungere un utente](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Aggiungere un utente")</span><span class="sxs-lookup"><span data-stu-id="65f0e-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="65f0e-225">a.</span><span class="sxs-lookup"><span data-stu-id="65f0e-225">a.</span></span> <span data-ttu-id="65f0e-226">In hello **nome** casella di testo, immettere nome hello dell'utente come **Laura**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-226">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="65f0e-227">b.</span><span class="sxs-lookup"><span data-stu-id="65f0e-227">b.</span></span> <span data-ttu-id="65f0e-228">In hello **cognome** casella di testo immettere hello cognome dell'utente come **Simon**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-228">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="65f0e-229">c.</span><span class="sxs-lookup"><span data-stu-id="65f0e-229">c.</span></span> <span data-ttu-id="65f0e-230">In hello **indirizzo di posta elettronica** casella di testo immettere hello email dell'utente come  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="65f0e-230">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="65f0e-231">d.</span><span class="sxs-lookup"><span data-stu-id="65f0e-231">d.</span></span> <span data-ttu-id="65f0e-232">Fare clic su **Aggiungi utente**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="65f0e-233">È possibile usare qualsiasi altro TalentLMS utente account strumento di creazione o le API fornite da TalentLMS tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="65f0e-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="65f0e-234">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="65f0e-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="65f0e-235">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooTalentLMS.</span><span class="sxs-lookup"><span data-stu-id="65f0e-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTalentLMS.</span></span>

![Assegna utente][200] 

<span data-ttu-id="65f0e-237">**tooassign Britta Simon tooTalentLMS, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="65f0e-237">**tooassign Britta Simon tooTalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="65f0e-238">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="65f0e-240">Nell'elenco di applicazioni hello, selezionare **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-240">In hello applications list, select **TalentLMS**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="65f0e-242">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="65f0e-244">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-244">Click **Add** button.</span></span> <span data-ttu-id="65f0e-245">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="65f0e-247">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="65f0e-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="65f0e-248">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65f0e-249">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="65f0e-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65f0e-250">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="65f0e-250">Testing single sign-on</span></span>

<span data-ttu-id="65f0e-251">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="65f0e-251">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="65f0e-252">Quando si fa clic hello TalentLMS riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour applicazione TalentLMS</span><span class="sxs-lookup"><span data-stu-id="65f0e-252">When you click hello TalentLMS tile in hello Access Panel, you should get automatically signed-on tooyour TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65f0e-253">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="65f0e-253">Additional resources</span></span>

* [<span data-ttu-id="65f0e-254">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65f0e-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65f0e-255">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65f0e-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

