---
title: 'Esercitazione: Integrazione di Azure Active Directory con ScreenSteps | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e ScreenSteps.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="7120c-103">Esercitazione: Integrazione di Azure Active Directory con ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="7120c-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="7120c-104">In questa esercitazione, è illustrato come toointegrate ScreenSteps con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7120c-104">In this tutorial, you learn how toointegrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7120c-105">Integrazione ScreenSteps con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="7120c-105">Integrating ScreenSteps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7120c-106">È possibile controllare in Azure AD che ha accesso tooScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="7120c-106">You can control in Azure AD who has access tooScreenSteps.</span></span>
- <span data-ttu-id="7120c-107">È possibile abilitare l'utenti tooautomatically get connesso tooScreenSteps (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7120c-107">You can enable your users tooautomatically get signed-on tooScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7120c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7120c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="7120c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7120c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7120c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7120c-110">Prerequisites</span></span>

<span data-ttu-id="7120c-111">integrazione di Azure AD con ScreenSteps tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="7120c-111">tooconfigure Azure AD integration with ScreenSteps, you need hello following items:</span></span>

- <span data-ttu-id="7120c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7120c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7120c-113">Sottoscrizione di ScreenSteps abilitata per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="7120c-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7120c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="7120c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7120c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="7120c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7120c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="7120c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7120c-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7120c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7120c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="7120c-118">Scenario description</span></span>
<span data-ttu-id="7120c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="7120c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7120c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="7120c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7120c-121">Aggiunta di ScreenSteps dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="7120c-121">Adding ScreenSteps from hello gallery</span></span>
2. <span data-ttu-id="7120c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7120c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-hello-gallery"></a><span data-ttu-id="7120c-123">Aggiunta di ScreenSteps dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="7120c-123">Adding ScreenSteps from hello gallery</span></span>
<span data-ttu-id="7120c-124">integrazione hello tooconfigure di ScreenSteps in Azure AD, è necessario tooadd ScreenSteps dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="7120c-124">tooconfigure hello integration of ScreenSteps into Azure AD, you need tooadd ScreenSteps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7120c-125">**tooadd ScreenSteps dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7120c-125">**tooadd ScreenSteps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7120c-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="7120c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="7120c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="7120c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7120c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7120c-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="7120c-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7120c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="7120c-133">Nella casella di ricerca hello, digitare **ScreenSteps**selezionare **ScreenSteps** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7120c-133">In hello search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco risultati hello ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7120c-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7120c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7120c-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con ScreenSteps usando un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7120c-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7120c-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in ScreenSteps è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7120c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScreenSteps is tooa user in Azure AD.</span></span> <span data-ttu-id="7120c-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in ScreenSteps deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="7120c-138">In other words, a link relationship between an Azure AD user and hello related user in ScreenSteps needs toobe established.</span></span>

<span data-ttu-id="7120c-139">In ScreenSteps, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="7120c-139">In ScreenSteps, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7120c-140">tooconfigure e test Azure single sign-on AD con ScreenSteps, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="7120c-140">tooconfigure and test Azure AD single sign-on with ScreenSteps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7120c-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7120c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7120c-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7120c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7120c-143">**[Creare un utente test ScreenSteps](#create-a-screensteps-test-user)**  -toohave un equivalente di Britta Simon in ScreenSteps che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="7120c-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - toohave a counterpart of Britta Simon in ScreenSteps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7120c-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7120c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7120c-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="7120c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7120c-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7120c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7120c-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="7120c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="7120c-148">**Azure AD tooconfigure single sign-on con ScreenSteps, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7120c-148">**tooconfigure Azure AD single sign-on with ScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="7120c-149">Nel portale di Azure su hello hello **ScreenSteps** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7120c-149">In hello Azure portal, on hello **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="7120c-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7120c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="7120c-153">In hello **ScreenSteps dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7120c-153">On hello **ScreenSteps Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni sull'accesso Single Sign-On per URL e dominio di ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="7120c-155">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="7120c-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7120c-156">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="7120c-156">This value is not real.</span></span> <span data-ttu-id="7120c-157">Aggiorna il valore con hello Sign-On URL effettivo, illustrato più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7120c-157">Update this value with hello actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="7120c-158">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="7120c-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="7120c-160">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="7120c-160">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7120c-162">In hello **ScreenSteps configurazione** fare clic su **configurare ScreenSteps** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="7120c-162">On hello **ScreenSteps Configuration** section, click **Configure ScreenSteps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7120c-163">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="7120c-163">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="7120c-165">In un'altra finestra del Web browser accedere al sito aziendale di ScreenSteps come amministratore.</span><span class="sxs-lookup"><span data-stu-id="7120c-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="7120c-166">Click **Account Settings** (Impostazioni account).</span><span class="sxs-lookup"><span data-stu-id="7120c-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="7120c-167">![Gestione degli account](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Gestione degli account")</span><span class="sxs-lookup"><span data-stu-id="7120c-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="7120c-168">Fare clic su **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="7120c-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="7120c-169">![Autenticazione remota](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Autenticazione remota")</span><span class="sxs-lookup"><span data-stu-id="7120c-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="7120c-170">Fare clic su **Create Single Sign-on Endpoint** (Crea endpoint Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="7120c-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="7120c-171">![Autenticazione remota](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Autenticazione remota")</span><span class="sxs-lookup"><span data-stu-id="7120c-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="7120c-172">In hello **creare Single Sign-on Endpoint** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7120c-172">In hello **Create Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="7120c-173">![Creare un endpoint di autenticazione](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Creare un endpoint di autenticazione")</span><span class="sxs-lookup"><span data-stu-id="7120c-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="7120c-174">a.</span><span class="sxs-lookup"><span data-stu-id="7120c-174">a.</span></span> <span data-ttu-id="7120c-175">In hello **titolo** casella di testo, digitare un titolo.</span><span class="sxs-lookup"><span data-stu-id="7120c-175">In hello **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="7120c-176">b.</span><span class="sxs-lookup"><span data-stu-id="7120c-176">b.</span></span> <span data-ttu-id="7120c-177">Da hello **modalità** elenco, selezionare **SAML**.</span><span class="sxs-lookup"><span data-stu-id="7120c-177">From hello **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="7120c-178">c.</span><span class="sxs-lookup"><span data-stu-id="7120c-178">c.</span></span> <span data-ttu-id="7120c-179">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7120c-179">Click **Create**.</span></span>

12. <span data-ttu-id="7120c-180">**Modifica** hello nuovo endpoint.</span><span class="sxs-lookup"><span data-stu-id="7120c-180">**Edit** hello new endpoint.</span></span>

    <span data-ttu-id="7120c-181">![Modifica endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Modifica endpoint")</span><span class="sxs-lookup"><span data-stu-id="7120c-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="7120c-182">In hello **modifica Single Sign-on Endpoint** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7120c-182">In hello **Edit Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="7120c-183">![Endpoint di autenticazione remota](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Endpoint di autenticazione remota")</span><span class="sxs-lookup"><span data-stu-id="7120c-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="7120c-184">a.</span><span class="sxs-lookup"><span data-stu-id="7120c-184">a.</span></span> <span data-ttu-id="7120c-185">Fare clic su **Carica nuovo file di certificato di SAML**e quindi caricare hello certificato, che è stato scaricato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7120c-185">Click **Upload new SAML Certificate file**, and then upload hello certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="7120c-186">b.</span><span class="sxs-lookup"><span data-stu-id="7120c-186">b.</span></span> <span data-ttu-id="7120c-187">Incolla **SAML Single Sign-On Service URL** valore, che è stato copiato dal portale di Azure hello in hello **URL accesso remoto** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="7120c-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="7120c-188">c.</span><span class="sxs-lookup"><span data-stu-id="7120c-188">c.</span></span> <span data-ttu-id="7120c-189">Incolla **Sign-Out URL** valore, che è stato copiato dal portale di Azure hello in hello **URL disconnessione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="7120c-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="7120c-190">d.</span><span class="sxs-lookup"><span data-stu-id="7120c-190">d.</span></span> <span data-ttu-id="7120c-191">Selezionare un **gruppo** tooassign utenti toowhen l'esecuzione del provisioning.</span><span class="sxs-lookup"><span data-stu-id="7120c-191">Select a **Group** tooassign users toowhen they are provisioned.</span></span>
    
    <span data-ttu-id="7120c-192">e.</span><span class="sxs-lookup"><span data-stu-id="7120c-192">e.</span></span> <span data-ttu-id="7120c-193">Fare clic su **Update**.</span><span class="sxs-lookup"><span data-stu-id="7120c-193">Click **Update**.</span></span>

    <span data-ttu-id="7120c-194">f.</span><span class="sxs-lookup"><span data-stu-id="7120c-194">f.</span></span> <span data-ttu-id="7120c-195">Hello copia **SAML Consumer URL** toohello Appunti e incollare in toohello **Sign-on URL** nella casella di testo **ScreenSteps dominio e gli URL** sezione.</span><span class="sxs-lookup"><span data-stu-id="7120c-195">Copy hello **SAML Consumer URL** toohello clipboard and paste in toohello **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="7120c-196">g.</span><span class="sxs-lookup"><span data-stu-id="7120c-196">g.</span></span> <span data-ttu-id="7120c-197">Restituire toohello **modifica Single Sign-on Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="7120c-197">Return toohello **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="7120c-198">h.</span><span class="sxs-lookup"><span data-stu-id="7120c-198">h.</span></span> <span data-ttu-id="7120c-199">Fare clic su hello **impostare come predefinito per l'account** pulsante toouse questo endpoint per tutti gli utenti che effettuano l'accesso in ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="7120c-199">Click hello **Make default for account** button toouse this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="7120c-200">In alternativa è possibile fare clic su hello **aggiungere tooSite** pulsante toouse questo endpoint per specifici siti Web in **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="7120c-200">Alternatively you can click hello **Add tooSite** button toouse this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="7120c-201">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="7120c-201">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7120c-202">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="7120c-202">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7120c-203">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7120c-203">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7120c-204">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7120c-204">Create an Azure AD test user</span></span>

<span data-ttu-id="7120c-205">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="7120c-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="7120c-207">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7120c-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7120c-208">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7120c-208">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7120c-210">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="7120c-210">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7120c-212">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="7120c-212">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7120c-214">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="7120c-214">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7120c-216">a.</span><span class="sxs-lookup"><span data-stu-id="7120c-216">a.</span></span> <span data-ttu-id="7120c-217">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7120c-217">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7120c-218">b.</span><span class="sxs-lookup"><span data-stu-id="7120c-218">b.</span></span> <span data-ttu-id="7120c-219">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7120c-219">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7120c-220">c.</span><span class="sxs-lookup"><span data-stu-id="7120c-220">c.</span></span> <span data-ttu-id="7120c-221">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="7120c-221">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7120c-222">d.</span><span class="sxs-lookup"><span data-stu-id="7120c-222">d.</span></span> <span data-ttu-id="7120c-223">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="7120c-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="7120c-224">Creare un utente test di ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="7120c-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="7120c-225">In questa sezione viene creato un utente di nome Britta Simon in ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="7120c-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="7120c-226">Lavorare con [team di supporto ScreenSteps Client](https://www.screensteps.com/contact) per aggiungere gli utenti di hello nella piattaforma ScreenSteps hello.</span><span class="sxs-lookup"><span data-stu-id="7120c-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add hello users in hello ScreenSteps platform.</span></span> <span data-ttu-id="7120c-227">Gli utenti devono essere creati e attivati prima di usare l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="7120c-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7120c-228">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7120c-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7120c-229">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="7120c-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooScreenSteps.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="7120c-231">**tooassign Britta Simon tooScreenSteps, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="7120c-231">**tooassign Britta Simon tooScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="7120c-232">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="7120c-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="7120c-234">Nell'elenco di applicazioni hello, selezionare **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="7120c-234">In hello applications list, select **ScreenSteps**.</span></span>

    ![collegamento ScreenSteps Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="7120c-236">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7120c-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="7120c-238">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7120c-238">Click **Add** button.</span></span> <span data-ttu-id="7120c-239">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7120c-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="7120c-241">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="7120c-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7120c-242">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="7120c-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7120c-243">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="7120c-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7120c-244">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="7120c-244">Test single sign-on</span></span>

<span data-ttu-id="7120c-245">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="7120c-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7120c-246">Quando si fa clic hello ScreenSteps riquadro in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato in ScreenSteps applicazione.</span><span class="sxs-lookup"><span data-stu-id="7120c-246">When you click hello ScreenSteps tile in hello Access Panel, you should get automatically signed-on tooyour ScreenSteps application.</span></span>
<span data-ttu-id="7120c-247">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7120c-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7120c-248">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="7120c-248">Additional resources</span></span>

* [<span data-ttu-id="7120c-249">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7120c-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7120c-250">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7120c-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

