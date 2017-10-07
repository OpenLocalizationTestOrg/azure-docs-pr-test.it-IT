---
title: 'Esercitazione: Integrazione di Azure Active Directory con Help Scout | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Scout Guida in linea.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="5ba52-103">Esercitazione: Integrazione di Azure Active Directory con Help Scout</span><span class="sxs-lookup"><span data-stu-id="5ba52-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="5ba52-104">In questa esercitazione illustrato come utilizzare toointegrate Guida con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5ba52-104">In this tutorial, you learn how toointegrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ba52-105">Si otterrà i seguenti vantaggi dagli Scout consentono l'integrazione con Azure AD hello:</span><span class="sxs-lookup"><span data-stu-id="5ba52-105">You get hello following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="5ba52-106">In Azure AD, è possibile controllare chi ha accesso tooHelp Scout.</span><span class="sxs-lookup"><span data-stu-id="5ba52-106">In Azure AD, you can control who has access tooHelp Scout.</span></span>
- <span data-ttu-id="5ba52-107">È possibile accedere automaticamente il tooHelp utenti Scout con accesso single sign-on e un account utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ba52-107">You can automatically sign in your users tooHelp Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="5ba52-108">È possibile gestire gli account in una posizione centrale, hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5ba52-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="5ba52-109">toolearn ulteriori informazioni su software come un servizio (SaaS) integrazione dell'applicazione con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5ba52-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ba52-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5ba52-110">Prerequisites</span></span>

<span data-ttu-id="5ba52-111">tooset l'integrazione di Azure AD con Scout della Guida, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5ba52-111">tooset up Azure AD integration with Help Scout, you need hello following items:</span></span>

- <span data-ttu-id="5ba52-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ba52-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5ba52-113">Sottoscrizione di Help Scout, con Single Sign-On attivato</span><span class="sxs-lookup"><span data-stu-id="5ba52-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="5ba52-114">Se si passi hello in questa esercitazione, si consiglia di non testare loro in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5ba52-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="5ba52-115">Indicazioni per il test passaggi hello in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="5ba52-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="5ba52-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5ba52-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="5ba52-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione gratuita di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ba52-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ba52-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5ba52-118">Scenario description</span></span>
<span data-ttu-id="5ba52-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5ba52-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="5ba52-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="5ba52-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ba52-121">Aggiungere Scout Guida dalla raccolta di hello.</span><span class="sxs-lookup"><span data-stu-id="5ba52-121">Add Help Scout from hello gallery.</span></span>
2. <span data-ttu-id="5ba52-122">Configurare e testare l'accesso Single Sign-On di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ba52-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-hello-gallery"></a><span data-ttu-id="5ba52-123">Aggiungere Scout Guida dalla raccolta di hello</span><span class="sxs-lookup"><span data-stu-id="5ba52-123">Add Help Scout from hello gallery</span></span>
<span data-ttu-id="5ba52-124">tooset l'integrazione di hello di Guida Scout con Azure AD, nella raccolta di hello, aggiungere l'elenco tooyour Scout Guida in linea di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5ba52-124">tooset up hello integration of Help Scout with Azure AD, in hello gallery, add Help Scout tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5ba52-125">tooadd Scout Guida dalla raccolta hello:</span><span class="sxs-lookup"><span data-stu-id="5ba52-125">tooadd Help Scout from hello gallery:</span></span>

1. <span data-ttu-id="5ba52-126">In hello [portale di Azure](https://portal.azure.com)in hello menu a sinistra, selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="5ba52-128">Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![pagina applicazioni di Enterprise Hello][2]
    
3. <span data-ttu-id="5ba52-130">Selezionare una nuova applicazione, tooadd **nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-130">tooadd a new application, select **New application**.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="5ba52-132">Nella casella di ricerca hello, immettere **Guida Scout**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-132">In hello search box, enter **Help Scout**.</span></span> <span data-ttu-id="5ba52-133">Nei risultati della ricerca hello, selezionare **Guida Scout**, quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-133">In hello search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Guida in linea Scout nell'elenco risultati hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5ba52-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ba52-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="5ba52-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Help Scout in base a un utente di test di nome *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="5ba52-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="5ba52-137">Per toowork di accesso singolo, Azure AD deve tooknow hello Azure controparte utente di Active Directory nella Guida in linea Scout.</span><span class="sxs-lookup"><span data-stu-id="5ba52-137">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="5ba52-138">È necessario stabilire una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Guida in linea Scout.</span><span class="sxs-lookup"><span data-stu-id="5ba52-138">A link relationship between an Azure AD user and hello related user in Help Scout must be established.</span></span>

<span data-ttu-id="5ba52-139">hello tooestablish relazione, in Guida in linea Scout, dei collegamenti per **Username**, assegnare il valore di hello di hello **nome utente** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ba52-139">tooestablish hello link relationship, in Help Scout, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="5ba52-140">tooconfigure e prova AD Azure single sign-on con Scout Guida in linea, hello completo seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="5ba52-140">tooconfigure and test Azure AD single sign-on with Help Scout, complete hello following tasks:</span></span>

1. <span data-ttu-id="5ba52-141">[Configurare l'accesso Single Sign-On di Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="5ba52-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="5ba52-142">Imposta un toouse utente questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5ba52-142">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="5ba52-143">[Creare un utente test di Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="5ba52-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="5ba52-144">Test AD Azure single sign-on con utente hello Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ba52-144">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="5ba52-145">[Creare un utente di test di Help Scout](#create-a-help-scout-test-user).</span><span class="sxs-lookup"><span data-stu-id="5ba52-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="5ba52-146">Crea un equivalente di Britta Simon Scout della Guida che è collegato toohello rappresentazione in forma di Azure AD dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="5ba52-146">Creates a counterpart of Britta Simon in Help Scout that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="5ba52-147">[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="5ba52-147">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="5ba52-148">Imposta Britta Simon toouse AD Azure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5ba52-148">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ba52-149">[Testare l'accesso Single Sign-On](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="5ba52-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="5ba52-150">Verifica che la configurazione di hello funziona.</span><span class="sxs-lookup"><span data-stu-id="5ba52-150">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="5ba52-151">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ba52-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="5ba52-152">In questa sezione, impostare di Azure AD single sign-on in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5ba52-152">In this section, you set up Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="5ba52-153">quindi si configura Single Sign-On nell'applicazione Help Scout.</span><span class="sxs-lookup"><span data-stu-id="5ba52-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="5ba52-154">tooset di Azure AD single sign-on con Scout Guida:</span><span class="sxs-lookup"><span data-stu-id="5ba52-154">tooset up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="5ba52-155">Nel portale di Azure su hello hello **Guida Scout** pagina di integrazione dell'applicazione, seleziona **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-155">In hello Azure portal, on hello **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Collegamento di configurazione di Single Sign-On][4]

2. <span data-ttu-id="5ba52-157">In hello **Single sign-on** pagina per **modalità**selezionare **basato su SAML Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-157">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="5ba52-159">In **Guida Scout dominio e gli URL**, se si desidera tooset di un'applicazione hello in modalità avviata da IDP hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5ba52-159">Under **Help Scout Domain and URLs**, if you want tooset up hello application in IDP-initiated mode, complete hello following steps:</span></span>

    1. <span data-ttu-id="5ba52-160">In hello **identificatore** , immettere un URL con hello seguente motivo:`urn:auth0:helpscout:<instancename>`</span><span class="sxs-lookup"><span data-stu-id="5ba52-160">In hello **Identifier** box, enter a URL that has hello following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="5ba52-161">In hello **URL di risposta** , immettere un URL con hello seguente motivo:`https://helpscout.auth0.com/login/callback?connection=<instancename>`</span><span class="sxs-lookup"><span data-stu-id="5ba52-161">In hello **Reply URL** box, enter a URL that has hello following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="5ba52-163">Se si desidera tooset di un'applicazione hello in modalità SP initiated, selezionare hello **Mostra URL impostazioni avanzate** casella di controllo e quindi hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="5ba52-163">If you want tooset up hello application in SP-initiated mode, select hello **Show advanced URL settings** check box, and then do hello following:</span></span>

    * <span data-ttu-id="5ba52-164">In hello **URL di accesso** , immettere un URL con hello seguente formato:`https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="5ba52-164">In hello **Sign on URL** box, enter a URL that has hello following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Informazioni su URL e dominio per Single Sign-On di Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="5ba52-166">i valori Hello in questi URL sono solo a scopo dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="5ba52-166">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="5ba52-167">Aggiornare i valori hello con URL effettivo identificatore hello e l'URL di risposta.</span><span class="sxs-lookup"><span data-stu-id="5ba52-167">Update hello values with hello actual identifier URL and reply URL.</span></span> <span data-ttu-id="5ba52-168">Questi valori, contattare il tooget [team di supporto della Guida Scout](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="5ba52-168">tooget these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="5ba52-169">In **certificato di firma SAML**selezionare **Metadata XML**e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5ba52-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="5ba52-171">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-171">Select **Save**.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="5ba52-173">tooset di single sign-on sul lato di Guida Scout hello, trasmissione hello scaricato metadati XML file toohello [team di supporto della Guida Scout](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="5ba52-173">tooset up single sign-on on hello Help Scout side, send hello downloaded metadata XML file toohello [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="5ba52-174">il team di supporto della Guida Scout Hello si applica questa impostazione in modo che sia impostata correttamente hello SAML single sign-on connessione su entrambi i lati.</span><span class="sxs-lookup"><span data-stu-id="5ba52-174">hello Help Scout support team applies this setting so that hello SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5ba52-175">È possibile leggere una versione di queste istruzioni in hello concisa [portale di Azure](https://portal.azure.com), mentre si configura l'app.</span><span class="sxs-lookup"><span data-stu-id="5ba52-175">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="5ba52-176">Dopo aver aggiunto l'applicazione hello selezionando **Active Directory** > **applicazioni aziendali**selezionare hello **Single Sign-On** scheda. È possibile accedere alla documentazione di hello incorporato in hello **configurazione** alla sezione, hello parte inferiore della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="5ba52-176">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="5ba52-177">Per altre informazioni, vedere la [documentazione incorporata su Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="5ba52-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5ba52-178">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ba52-178">Create an Azure AD test user</span></span>

<span data-ttu-id="5ba52-179">In questa sezione, nel portale di Azure hello si crea un utente di test denominato Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ba52-179">In this section, in hello Azure portal, you create a test user named Britta Simon.</span></span>

![Creare un utente test di Azure AD][100]

<span data-ttu-id="5ba52-181">toocreate un utente di prova in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="5ba52-181">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="5ba52-182">Nel portale di Azure, nel menu a sinistra di hello, hello selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-182">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5ba52-184">elenco di hello toodisplay di utenti, selezionare **utenti e gruppi**, quindi selezionare **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-184">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![Selezionare Utenti e gruppi e quindi selezionare Tutti gli utenti.](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5ba52-186">hello tooopen **utente** la finestra di dialogo, nella parte superiore di hello di hello **tutti gli utenti** selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-186">tooopen hello **User** dialog box, at hello top of hello **All Users** page, select **Add**.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5ba52-188">In hello **utente** della finestra di dialogo hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5ba52-188">In hello **User** dialog box, complete hello following steps:</span></span>

    1. <span data-ttu-id="5ba52-189">In hello **nome** immettere **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-189">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="5ba52-190">In hello **nome utente** , immettere l'indirizzo di posta elettronica hello di Britta Simon utente.</span><span class="sxs-lookup"><span data-stu-id="5ba52-190">In hello **User name** box, enter hello email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="5ba52-191">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="5ba52-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="5ba52-192">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-192">Select **Create**.</span></span>

        ![finestra di dialogo utente Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="5ba52-194">Creare un utente test di Help Scout</span><span class="sxs-lookup"><span data-stu-id="5ba52-194">Create a Help Scout test user</span></span>

<span data-ttu-id="5ba52-195">oggetto Hello di questa sezione è un utente denominato Britta Simon nella Guida in linea Scout toocreate.</span><span class="sxs-lookup"><span data-stu-id="5ba52-195">hello object of this section is toocreate a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="5ba52-196">Help Scout supporta il provisioning JIT, che è attivato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5ba52-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="5ba52-197">In questa sezione non è toocomplete alcuna azione o un'attività.</span><span class="sxs-lookup"><span data-stu-id="5ba52-197">In this section, there's no action or task toocomplete.</span></span> <span data-ttu-id="5ba52-198">Se un utente non esiste già nella Guida in linea Scout, viene creato uno nuovo quando si tenta di tooaccess Scout Guida in linea.</span><span class="sxs-lookup"><span data-stu-id="5ba52-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt tooaccess Help Scout.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5ba52-199">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ba52-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5ba52-200">In questa sezione utente hello Britta Simon toouse AD Azure single sign-on tramite la concessione di hello utente account accesso tooHelp Scout.</span><span class="sxs-lookup"><span data-stu-id="5ba52-200">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooHelp Scout.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="5ba52-202">tooassign Britta Simon tooHelp Scout:</span><span class="sxs-lookup"><span data-stu-id="5ba52-202">tooassign Britta Simon tooHelp Scout:</span></span>

1. <span data-ttu-id="5ba52-203">Nel portale di Azure hello, aprire visualizzazione applicazioni hello e fare clic sulla visualizzazione directory toohello.</span><span class="sxs-lookup"><span data-stu-id="5ba52-203">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="5ba52-204">Selezionare **Applicazioni aziendali** e quindi selezionare **Tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5ba52-206">Nell'elenco di applicazioni hello, selezionare **Guida Scout**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-206">In hello applications list, select **Help Scout**.</span></span>

    ![collegamento della Guida Scout Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="5ba52-208">Nel menu a sinistra di hello, selezionare **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-208">In hello left menu, select **Users and groups**.</span></span>

    ![Hello gli utenti e gruppi][202]

4. <span data-ttu-id="5ba52-210">Selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-210">Select **Add**.</span></span> <span data-ttu-id="5ba52-211">Quindi, nella hello **Aggiungi** selezionare **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-211">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="5ba52-213">In hello **utenti e gruppi** hello elenco di utenti, selezionare pagina **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-213">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="5ba52-214">In hello **utenti e gruppi** selezionare **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-214">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="5ba52-215">In hello **Aggiungi** selezionare **assegnare**.</span><span class="sxs-lookup"><span data-stu-id="5ba52-215">On hello **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5ba52-216">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5ba52-216">Test single sign-on</span></span>

<span data-ttu-id="5ba52-217">In questa sezione si test configurazione di Azure AD single sign-on utilizzando il pannello di accesso di hello.</span><span class="sxs-lookup"><span data-stu-id="5ba52-217">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="5ba52-218">Quando si seleziona riquadro Guida Scout hello nel Pannello di accesso hello, è necessario essere connessi automaticamente tooyour applicazione Scout Guida in linea.</span><span class="sxs-lookup"><span data-stu-id="5ba52-218">When you select hello Help Scout tile in hello access panel, you should be automatically signed in tooyour Help Scout application.</span></span>

<span data-ttu-id="5ba52-219">Per ulteriori informazioni sul pannello di accesso, vedere [Pannello di accesso di introduzione toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5ba52-219">For more information about the access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5ba52-220">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5ba52-220">Additional resources</span></span>

* [<span data-ttu-id="5ba52-221">Elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ba52-221">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ba52-222">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ba52-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

