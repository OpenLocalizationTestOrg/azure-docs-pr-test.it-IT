---
title: 'Esercitazione: Integrazione di Azure Active Directory con Jobscience | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Jobscience.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="e7225-103">Esercitazione: Integrazione di Azure Active Directory con Jobscience</span><span class="sxs-lookup"><span data-stu-id="e7225-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="e7225-104">In questa esercitazione, è illustrato come toointegrate Jobscience con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7225-104">In this tutorial, you learn how toointegrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7225-105">Integrazione di Jobscience con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="e7225-105">Integrating Jobscience with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e7225-106">È possibile controllare in Azure AD che ha accesso tooJobscience</span><span class="sxs-lookup"><span data-stu-id="e7225-106">You can control in Azure AD who has access tooJobscience</span></span>
- <span data-ttu-id="e7225-107">È possibile abilitare l'utenti tooautomatically get connesso tooJobscience (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7225-107">You can enable your users tooautomatically get signed-on tooJobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7225-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e7225-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e7225-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7225-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7225-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e7225-110">Prerequisites</span></span>

<span data-ttu-id="e7225-111">integrazione di Azure AD con Jobscience tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="e7225-111">tooconfigure Azure AD integration with Jobscience, you need hello following items:</span></span>

- <span data-ttu-id="e7225-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7225-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7225-113">Sottoscrizione di Jobscience abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e7225-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7225-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="e7225-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7225-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="e7225-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7225-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="e7225-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7225-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7225-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7225-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="e7225-118">Scenario description</span></span>
<span data-ttu-id="e7225-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="e7225-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7225-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="e7225-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7225-121">Aggiunta di Jobscience dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e7225-121">Adding Jobscience from hello gallery</span></span>
2. <span data-ttu-id="e7225-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7225-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-hello-gallery"></a><span data-ttu-id="e7225-123">Aggiunta di Jobscience dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="e7225-123">Adding Jobscience from hello gallery</span></span>
<span data-ttu-id="e7225-124">integrazione hello tooconfigure di Jobscience in Azure AD, è necessario tooadd Jobscience dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="e7225-124">tooconfigure hello integration of Jobscience into Azure AD, you need tooadd Jobscience from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e7225-125">**tooadd Jobscience dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7225-125">**tooadd Jobscience from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7225-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="e7225-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e7225-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="e7225-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e7225-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e7225-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="e7225-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="e7225-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="e7225-133">Nella casella di ricerca hello, digitare **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="e7225-133">In hello search box, type **Jobscience**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="e7225-135">Nel riquadro dei risultati hello, selezionare **Jobscience**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e7225-135">In hello results panel, select **Jobscience**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7225-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7225-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7225-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Jobscience in base a un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e7225-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e7225-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Jobscience è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7225-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jobscience is tooa user in Azure AD.</span></span> <span data-ttu-id="e7225-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Jobscience richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="e7225-140">In other words, a link relationship between an Azure AD user and hello related user in Jobscience needs toobe established.</span></span>

<span data-ttu-id="e7225-141">In Jobscience, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="e7225-141">In Jobscience, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e7225-142">tooconfigure e test Azure single sign-on AD con Jobscience, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="e7225-142">tooconfigure and test Azure AD single sign-on with Jobscience, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e7225-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e7225-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e7225-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7225-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7225-145">**[Creazione di un utente test Jobscience](#creating-a-jobscience-test-user)**  -toohave un equivalente di Britta Simon in Jobscience che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e7225-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - toohave a counterpart of Britta Simon in Jobscience that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7225-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e7225-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7225-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="e7225-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7225-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7225-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7225-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Jobscience.</span><span class="sxs-lookup"><span data-stu-id="e7225-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="e7225-150">**Azure AD tooconfigure single sign-on con Jobscience, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7225-150">**tooconfigure Azure AD single sign-on with Jobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7225-151">Nel portale di Azure su hello hello **Jobscience** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e7225-151">In hello Azure portal, on hello **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="e7225-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e7225-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="e7225-155">In hello **Jobscience dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e7225-155">On hello **Jobscience Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="e7225-157">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="e7225-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="e7225-158">Poiché non è reale,</span><span class="sxs-lookup"><span data-stu-id="e7225-158">This value is not real.</span></span> <span data-ttu-id="e7225-159">Aggiorna il valore con hello URL effettivo Sign-On.</span><span class="sxs-lookup"><span data-stu-id="e7225-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="e7225-160">Ottenere questo valore per [team di supporto Client di Jobscience](https://www.jobscience.com/support) o dal profilo SSO hello si creeranno descritta più avanti nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="e7225-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from hello SSO profile you will create which is explained later in hello tutorial.</span></span> 
 
4. <span data-ttu-id="e7225-161">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="e7225-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="e7225-163">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="e7225-163">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e7225-165">In hello **Jobscience configurazione** fare clic su **configurare Jobscience** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="e7225-165">On hello **Jobscience Configuration** section, click **Configure Jobscience** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e7225-166">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="e7225-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="e7225-168">Accedi tooyour sito della società Jobscience come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e7225-168">Log in tooyour Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="e7225-169">Andare troppo**installazione**.</span><span class="sxs-lookup"><span data-stu-id="e7225-169">Go too**Setup**.</span></span>
   
   <span data-ttu-id="e7225-170">![Installazione](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="e7225-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="e7225-171">Nel riquadro di spostamento a sinistra, hello hello **Amministra** fare clic su **Gestione dominio** tooexpand hello sezione correlata e quindi fare clic su **My Domain** hello tooopen  **Il mio dominio** pagina.</span><span class="sxs-lookup"><span data-stu-id="e7225-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
   <span data-ttu-id="e7225-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="e7225-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="e7225-173">tooverify che il dominio è stato configurato correttamente, assicurarsi che sia in "**passaggio 4 distribuito tooUsers**" ed esaminare il "**impostazioni dominio personali**".</span><span class="sxs-lookup"><span data-stu-id="e7225-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="e7225-174">![Dominio distribuito tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser distribuite del dominio")</span><span class="sxs-lookup"><span data-stu-id="e7225-174">![Domain Deployed tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="e7225-175">Nel sito della società Jobscience hello scegliere **controlli di sicurezza**, quindi fare clic su **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="e7225-175">On hello Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="e7225-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="e7225-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="e7225-177">In hello **Single Sign-On Settings** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e7225-177">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="e7225-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="e7225-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="e7225-179">a.</span><span class="sxs-lookup"><span data-stu-id="e7225-179">a.</span></span> <span data-ttu-id="e7225-180">Selezionare **Abilitato SAML**.</span><span class="sxs-lookup"><span data-stu-id="e7225-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="e7225-181">b.</span><span class="sxs-lookup"><span data-stu-id="e7225-181">b.</span></span> <span data-ttu-id="e7225-182">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="e7225-182">Click **New**.</span></span>

13. <span data-ttu-id="e7225-183">In hello **SAML Single Sign-On Setting Edit** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e7225-183">On hello **SAML Single Sign-On Setting Edit** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="e7225-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span><span class="sxs-lookup"><span data-stu-id="e7225-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="e7225-185">a.</span><span class="sxs-lookup"><span data-stu-id="e7225-185">a.</span></span> <span data-ttu-id="e7225-186">In hello **nome** casella di testo, digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="e7225-186">In hello **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="e7225-187">b.</span><span class="sxs-lookup"><span data-stu-id="e7225-187">b.</span></span> <span data-ttu-id="e7225-188">In **dell'autorità di certificazione** casella di testo, hello Incolla valore **ID entità SAML**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7225-188">In **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e7225-189">c.</span><span class="sxs-lookup"><span data-stu-id="e7225-189">c.</span></span> <span data-ttu-id="e7225-190">In hello **Id entità** casella di testo, tipo`https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="e7225-190">In hello **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="e7225-191">d.</span><span class="sxs-lookup"><span data-stu-id="e7225-191">d.</span></span> <span data-ttu-id="e7225-192">Fare clic su **Sfoglia** tooupload il certificato di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7225-192">Click **Browse** tooupload your Azure AD certificate.</span></span>

    <span data-ttu-id="e7225-193">e.</span><span class="sxs-lookup"><span data-stu-id="e7225-193">e.</span></span> <span data-ttu-id="e7225-194">Come **tipo di identità SAML**selezionare **l'asserzione contiene l'ID di federazione di hello dall'oggetto utente hello**.</span><span class="sxs-lookup"><span data-stu-id="e7225-194">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>

    <span data-ttu-id="e7225-195">f.</span><span class="sxs-lookup"><span data-stu-id="e7225-195">f.</span></span> <span data-ttu-id="e7225-196">Come **SAML Identity Location**selezionare **identità si trova nell'elemento NameIdentfier hello di hello Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="e7225-196">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>

    <span data-ttu-id="e7225-197">g.</span><span class="sxs-lookup"><span data-stu-id="e7225-197">g.</span></span> <span data-ttu-id="e7225-198">In **Identity Provider Login URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7225-198">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e7225-199">h.</span><span class="sxs-lookup"><span data-stu-id="e7225-199">h.</span></span> <span data-ttu-id="e7225-200">In **Identity Provider Logout URL** casella di testo, hello Incolla valore **Sign-Out URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e7225-200">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e7225-201">i.</span><span class="sxs-lookup"><span data-stu-id="e7225-201">i.</span></span> <span data-ttu-id="e7225-202">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e7225-202">Click **Save**.</span></span>

14. <span data-ttu-id="e7225-203">Nel riquadro di spostamento a sinistra, hello hello **Amministra** fare clic su **Gestione dominio** tooexpand hello sezione correlata e quindi fare clic su **My Domain** hello tooopen  **Il mio dominio** pagina.</span><span class="sxs-lookup"><span data-stu-id="e7225-203">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="e7225-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span><span class="sxs-lookup"><span data-stu-id="e7225-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="e7225-205">In hello **My Domain** pagina hello **personalizzazione pagina di accesso** fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="e7225-205">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="e7225-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="e7225-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="e7225-207">In hello **personalizzazione pagina di accesso** pagina hello **servizio di autenticazione** sezione, il nome di hello del **SAML SSO Settings** viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="e7225-207">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="e7225-208">Selezionarlo e quindi fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="e7225-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="e7225-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span><span class="sxs-lookup"><span data-stu-id="e7225-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="e7225-210">hello tooget SP ha avviato l'accesso Single Sign, fare clic su URL di accesso su hello **impostazioni Single Sign-On** in hello **controlli di sicurezza** sezione del menu.</span><span class="sxs-lookup"><span data-stu-id="e7225-210">tooget hello SP initiated Single Sign on Login URL click on hello **Single Sign On settings** in hello **Security Controls** menu section.</span></span>

    <span data-ttu-id="e7225-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="e7225-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="e7225-212">Fare clic su profilo SSO hello creato nel passaggio hello precedente.</span><span class="sxs-lookup"><span data-stu-id="e7225-212">Click hello SSO profile you have created in hello step above.</span></span> <span data-ttu-id="e7225-213">Questa pagina vengono visualizzati hello Single Sign in URL per l'azienda (ad esempio, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span><span class="sxs-lookup"><span data-stu-id="e7225-213">This page shows hello Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="e7225-214">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="e7225-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e7225-215">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="e7225-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e7225-216">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7225-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7225-217">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7225-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7225-218">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="e7225-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="e7225-220">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7225-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7225-221">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="e7225-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7225-223">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="e7225-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7225-225">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="e7225-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7225-227">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e7225-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7225-229">a.</span><span class="sxs-lookup"><span data-stu-id="e7225-229">a.</span></span> <span data-ttu-id="e7225-230">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7225-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7225-231">b.</span><span class="sxs-lookup"><span data-stu-id="e7225-231">b.</span></span> <span data-ttu-id="e7225-232">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e7225-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7225-233">c.</span><span class="sxs-lookup"><span data-stu-id="e7225-233">c.</span></span> <span data-ttu-id="e7225-234">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="e7225-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e7225-235">d.</span><span class="sxs-lookup"><span data-stu-id="e7225-235">d.</span></span> <span data-ttu-id="e7225-236">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e7225-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="e7225-237">Creazione di un utente test di Jobscience</span><span class="sxs-lookup"><span data-stu-id="e7225-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="e7225-238">In ordine tooenable Azure AD utenti toolog in tooJobscience, è necessario eseguirne il provisioning in Jobscience.</span><span class="sxs-lookup"><span data-stu-id="e7225-238">In order tooenable Azure AD users toolog in tooJobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="e7225-239">Nel caso di hello di Jobscience, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="e7225-239">In hello case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="e7225-240">È possibile usare qualsiasi altro Jobscience utente account strumento di creazione o le API fornite da Jobscience tooprovision Azure Active Directory gli account utente.</span><span class="sxs-lookup"><span data-stu-id="e7225-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience tooprovision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="e7225-241">**tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7225-241">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7225-242">Accedi tooyour **Jobscience** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e7225-242">Log in tooyour **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="e7225-243">Passare tooSetup.</span><span class="sxs-lookup"><span data-stu-id="e7225-243">Go tooSetup.</span></span>
   
   <span data-ttu-id="e7225-244">![Installazione](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Installazione")</span><span class="sxs-lookup"><span data-stu-id="e7225-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="e7225-245">Andare troppo**Gestisci utenti \> utenti**.</span><span class="sxs-lookup"><span data-stu-id="e7225-245">Go too**Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="e7225-246">![Utenti](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="e7225-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="e7225-247">Fare clic su **Nuovo utente**.</span><span class="sxs-lookup"><span data-stu-id="e7225-247">Click **New User**.</span></span>
   
   <span data-ttu-id="e7225-248">![Tutti gli utenti](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Tutti gli utenti")</span><span class="sxs-lookup"><span data-stu-id="e7225-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="e7225-249">In hello **modifica utente** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e7225-249">On hello **Edit User** dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="e7225-250">![Modifica dell'utente](./media/active-directory-saas-jobscience-tutorial/ic784371.png "Modifica dell'utente")</span><span class="sxs-lookup"><span data-stu-id="e7225-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="e7225-251">a.</span><span class="sxs-lookup"><span data-stu-id="e7225-251">a.</span></span> <span data-ttu-id="e7225-252">In hello **nome** casella di testo, digitare un nome dell'utente hello come Laura.</span><span class="sxs-lookup"><span data-stu-id="e7225-252">In hello **First Name** textbox, type a first name of hello user like Britta.</span></span>
   
   <span data-ttu-id="e7225-253">b.</span><span class="sxs-lookup"><span data-stu-id="e7225-253">b.</span></span> <span data-ttu-id="e7225-254">In hello **cognome** casella di testo, specificare un cognome dell'utente hello come Simon.</span><span class="sxs-lookup"><span data-stu-id="e7225-254">In hello **Last Name** textbox, type a last name of hello user like Simon.</span></span>
   
   <span data-ttu-id="e7225-255">c.</span><span class="sxs-lookup"><span data-stu-id="e7225-255">c.</span></span> <span data-ttu-id="e7225-256">In hello **Alias** casella di testo, digitare un nome di alias dell'utente hello come brittas.</span><span class="sxs-lookup"><span data-stu-id="e7225-256">In hello **Alias** textbox, type an alias name of hello user like brittas.</span></span>

   <span data-ttu-id="e7225-257">d.</span><span class="sxs-lookup"><span data-stu-id="e7225-257">d.</span></span> <span data-ttu-id="e7225-258">In hello **posta elettronica** casella di testo, digitare hello di indirizzo di posta elettronica dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e7225-258">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="e7225-259">e.</span><span class="sxs-lookup"><span data-stu-id="e7225-259">e.</span></span> <span data-ttu-id="e7225-260">In hello **nome utente** , digitare un nome utente dell'utente come Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e7225-260">In hello **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="e7225-261">f.</span><span class="sxs-lookup"><span data-stu-id="e7225-261">f.</span></span> <span data-ttu-id="e7225-262">In hello **nome alternativo** casella di testo, digitare un nome alternativo dell'utente come Simon.</span><span class="sxs-lookup"><span data-stu-id="e7225-262">In hello **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="e7225-263">g.</span><span class="sxs-lookup"><span data-stu-id="e7225-263">g.</span></span> <span data-ttu-id="e7225-264">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e7225-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="e7225-265">titolare dell'account di Azure Active Directory Hello riceve un messaggio di posta elettronica e segue il proprio account tooconfirm un collegamento prima che diventi attivo.</span><span class="sxs-lookup"><span data-stu-id="e7225-265">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e7225-266">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7225-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e7225-267">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooJobscience.</span><span class="sxs-lookup"><span data-stu-id="e7225-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobscience.</span></span>

![Assegna utente][200] 

<span data-ttu-id="e7225-269">**tooassign Britta Simon tooJobscience, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="e7225-269">**tooassign Britta Simon tooJobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7225-270">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="e7225-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="e7225-272">Nell'elenco di applicazioni hello, selezionare **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="e7225-272">In hello applications list, select **Jobscience**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="e7225-274">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e7225-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="e7225-276">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e7225-276">Click **Add** button.</span></span> <span data-ttu-id="e7225-277">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e7225-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="e7225-279">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="e7225-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e7225-280">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="e7225-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7225-281">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="e7225-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7225-282">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e7225-282">Testing single sign-on</span></span>

<span data-ttu-id="e7225-283">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="e7225-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e7225-284">Quando si fa clic su riquadro Jobscience hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour Jobscience applicazione.</span><span class="sxs-lookup"><span data-stu-id="e7225-284">When you click hello Jobscience tile in hello Access Panel, you should get automatically signed-on tooyour Jobscience application.</span></span>
<span data-ttu-id="e7225-285">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e7225-285">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7225-286">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="e7225-286">Additional resources</span></span>

* [<span data-ttu-id="e7225-287">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7225-287">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7225-288">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7225-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

