---
title: 'Esercitazione: Integrazione di Azure Active Directory con SumoLogic| Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SumoLogic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 2ef1bd329f5db8899f0b57744e4c0f6eed1c532f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="12d58-103">Esercitazione: Integrazione di Azure Active Directory con SumoLogic</span><span class="sxs-lookup"><span data-stu-id="12d58-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="12d58-104">In questa esercitazione, è illustrato come toointegrate SumoLogic con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="12d58-104">In this tutorial, you learn how toointegrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="12d58-105">Integrazione di SumoLogic con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="12d58-105">Integrating SumoLogic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="12d58-106">È possibile controllare in Azure AD che ha accesso tooSumoLogic</span><span class="sxs-lookup"><span data-stu-id="12d58-106">You can control in Azure AD who has access tooSumoLogic</span></span>
- <span data-ttu-id="12d58-107">È possibile abilitare l'utenti tooautomatically get connesso tooSumoLogic (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="12d58-107">You can enable your users tooautomatically get signed-on tooSumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="12d58-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="12d58-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="12d58-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="12d58-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12d58-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="12d58-110">Prerequisites</span></span>

<span data-ttu-id="12d58-111">integrazione di Azure AD con SumoLogic tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="12d58-111">tooconfigure Azure AD integration with SumoLogic, you need hello following items:</span></span>

- <span data-ttu-id="12d58-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12d58-112">An Azure AD subscription</span></span>
- <span data-ttu-id="12d58-113">Sottoscrizione di SumoLogic abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="12d58-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="12d58-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="12d58-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="12d58-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="12d58-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="12d58-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="12d58-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="12d58-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="12d58-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="12d58-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="12d58-118">Scenario description</span></span>
<span data-ttu-id="12d58-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="12d58-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="12d58-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="12d58-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="12d58-121">Aggiunta di SumoLogic dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="12d58-121">Adding SumoLogic from hello gallery</span></span>
2. <span data-ttu-id="12d58-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="12d58-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-hello-gallery"></a><span data-ttu-id="12d58-123">Aggiunta di SumoLogic dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="12d58-123">Adding SumoLogic from hello gallery</span></span>
<span data-ttu-id="12d58-124">integrazione hello tooconfigure di SumoLogic in Azure AD, è necessario tooadd SumoLogic dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="12d58-124">tooconfigure hello integration of SumoLogic into Azure AD, you need tooadd SumoLogic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="12d58-125">**tooadd SumoLogic dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="12d58-125">**tooadd SumoLogic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="12d58-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="12d58-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="12d58-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="12d58-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="12d58-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="12d58-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="12d58-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="12d58-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="12d58-133">Nella casella di ricerca hello, digitare **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="12d58-133">In hello search box, type **SumoLogic**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="12d58-135">Nel riquadro dei risultati hello, selezionare **SumoLogic**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="12d58-135">In hello results panel, select **SumoLogic**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="12d58-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="12d58-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="12d58-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SumoLogic usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="12d58-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="12d58-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in SumoLogic è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12d58-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SumoLogic is tooa user in Azure AD.</span></span> <span data-ttu-id="12d58-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in SumoLogic deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="12d58-140">In other words, a link relationship between an Azure AD user and hello related user in SumoLogic needs toobe established.</span></span>

<span data-ttu-id="12d58-141">In SumoLogic, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="12d58-141">In SumoLogic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="12d58-142">tooconfigure e test Azure single sign-on AD con SumoLogic, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="12d58-142">tooconfigure and test Azure AD single sign-on with SumoLogic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="12d58-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="12d58-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="12d58-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="12d58-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="12d58-145">**[Creazione di un utente test SumoLogic](#creating-a-sumologic-test-user)**  -toohave un equivalente di Britta Simon in SumoLogic che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="12d58-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - toohave a counterpart of Britta Simon in SumoLogic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="12d58-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="12d58-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="12d58-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="12d58-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="12d58-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="12d58-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="12d58-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="12d58-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="12d58-150">**Azure AD tooconfigure single sign-on con SumoLogic, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="12d58-150">**tooconfigure Azure AD single sign-on with SumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="12d58-151">Nel portale di Azure su hello hello **SumoLogic** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="12d58-151">In hello Azure portal, on hello **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="12d58-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="12d58-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="12d58-155">In hello **SumoLogic dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="12d58-155">On hello **SumoLogic Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="12d58-157">a.</span><span class="sxs-lookup"><span data-stu-id="12d58-157">a.</span></span> <span data-ttu-id="12d58-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="12d58-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="12d58-159">b.</span><span class="sxs-lookup"><span data-stu-id="12d58-159">b.</span></span> <span data-ttu-id="12d58-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="12d58-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="12d58-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="12d58-161">These values are not real.</span></span> <span data-ttu-id="12d58-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="12d58-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="12d58-163">Contatto [team di supporto Client di SumoLogic](https://www.sumologic.com/contact-us/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="12d58-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="12d58-164">In hello **certificato di firma SAML** fare clic su **certificato (Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="12d58-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="12d58-166">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="12d58-166">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="12d58-168">In hello **SumoLogic configurazione** fare clic su **configurare SumoLogic** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="12d58-168">On hello **SumoLogic Configuration** section, click **Configure SumoLogic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="12d58-169">Hello copia **ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="12d58-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="12d58-171">In una finestra del web browser, accedere come amministratore nel sito della società SumoLogic di tooyour.</span><span class="sxs-lookup"><span data-stu-id="12d58-171">In a different web browser window, log in tooyour SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="12d58-172">Andare troppo**Gestisci \> sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="12d58-172">Go too**Manage \> Security**.</span></span>
   
    <span data-ttu-id="12d58-173">![Gestione](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Gestione")</span><span class="sxs-lookup"><span data-stu-id="12d58-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="12d58-174">Fare clic su **SAML**.</span><span class="sxs-lookup"><span data-stu-id="12d58-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="12d58-175">![Impostazioni di sicurezza globale](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Impostazioni di sicurezza globale")</span><span class="sxs-lookup"><span data-stu-id="12d58-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="12d58-176">Da hello **selezionare una configurazione o crearne uno nuovo** selezionare **AD Azure**, quindi fare clic su **configura**.</span><span class="sxs-lookup"><span data-stu-id="12d58-176">From hello **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="12d58-177">![Configurare SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configurare SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="12d58-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="12d58-178">In hello **configurare SAML 2.0** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="12d58-178">On hello **Configure SAML 2.0** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="12d58-179">![Configurare SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configurare SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="12d58-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="12d58-180">a.</span><span class="sxs-lookup"><span data-stu-id="12d58-180">a.</span></span> <span data-ttu-id="12d58-181">In hello **nome configurazione** casella tipo **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="12d58-181">In hello **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="12d58-182">b.</span><span class="sxs-lookup"><span data-stu-id="12d58-182">b.</span></span> <span data-ttu-id="12d58-183">Selezionare **Debug Mode**.</span><span class="sxs-lookup"><span data-stu-id="12d58-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="12d58-184">c.</span><span class="sxs-lookup"><span data-stu-id="12d58-184">c.</span></span> <span data-ttu-id="12d58-185">In hello **dell'autorità di certificazione** casella di testo, hello Incolla valore **ID entità SAML**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="12d58-185">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="12d58-186">d.</span><span class="sxs-lookup"><span data-stu-id="12d58-186">d.</span></span> <span data-ttu-id="12d58-187">In hello **URL richiesta di autenticazione** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL**, che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="12d58-187">In hello **Authn Request URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="12d58-188">e.</span><span class="sxs-lookup"><span data-stu-id="12d58-188">e.</span></span> <span data-ttu-id="12d58-189">Aprire il certificato con codifica base 64 nel blocco note, hello copia del contenuto di esso negli Appunti e quindi incollare hello intero certificato nella **certificato x. 509** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="12d58-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="12d58-190">f.</span><span class="sxs-lookup"><span data-stu-id="12d58-190">f.</span></span> <span data-ttu-id="12d58-191">Per **Email Attribute** (Attributo e-mail), selezionare **Use SAML subject** (Usa oggetto SAML).</span><span class="sxs-lookup"><span data-stu-id="12d58-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="12d58-192">g.</span><span class="sxs-lookup"><span data-stu-id="12d58-192">g.</span></span> <span data-ttu-id="12d58-193">Selezionare **SP initiated Login Configuration**.</span><span class="sxs-lookup"><span data-stu-id="12d58-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="12d58-194">h.</span><span class="sxs-lookup"><span data-stu-id="12d58-194">h.</span></span> <span data-ttu-id="12d58-195">In hello **percorso di accesso** casella tipo **Azure** e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="12d58-195">In hello **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="12d58-196">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="12d58-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="12d58-197">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="12d58-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="12d58-198">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="12d58-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="12d58-199">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="12d58-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="12d58-200">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="12d58-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="12d58-202">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="12d58-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="12d58-203">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="12d58-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="12d58-205">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="12d58-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="12d58-207">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="12d58-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="12d58-209">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="12d58-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="12d58-211">a.</span><span class="sxs-lookup"><span data-stu-id="12d58-211">a.</span></span> <span data-ttu-id="12d58-212">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="12d58-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="12d58-213">b.</span><span class="sxs-lookup"><span data-stu-id="12d58-213">b.</span></span> <span data-ttu-id="12d58-214">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="12d58-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="12d58-215">c.</span><span class="sxs-lookup"><span data-stu-id="12d58-215">c.</span></span> <span data-ttu-id="12d58-216">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="12d58-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="12d58-217">d.</span><span class="sxs-lookup"><span data-stu-id="12d58-217">d.</span></span> <span data-ttu-id="12d58-218">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="12d58-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="12d58-219">Creazione di un utente di test di SumoLogic</span><span class="sxs-lookup"><span data-stu-id="12d58-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="12d58-220">In ordine tooenable Azure AD utenti toolog in tooSumoLogic, devono essere tooSumoLogic provisioning.</span><span class="sxs-lookup"><span data-stu-id="12d58-220">In order tooenable Azure AD users toolog in tooSumoLogic, they must be provisioned tooSumoLogic.</span></span>  

* <span data-ttu-id="12d58-221">Nel caso di hello di SumoLogic, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="12d58-221">In hello case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="12d58-222">**tooprovision un account utente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="12d58-222">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="12d58-223">Accedi tooyour **SumoLogic** tenant.</span><span class="sxs-lookup"><span data-stu-id="12d58-223">Log in tooyour **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="12d58-224">Andare troppo**Gestisci \> utenti**.</span><span class="sxs-lookup"><span data-stu-id="12d58-224">Go too**Manage \> Users**.</span></span>
   
    <span data-ttu-id="12d58-225">![Utenti](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="12d58-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="12d58-226">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="12d58-226">Click **Add**.</span></span>
   
    <span data-ttu-id="12d58-227">![Utenti](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Utenti")</span><span class="sxs-lookup"><span data-stu-id="12d58-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="12d58-228">In hello **nuovo utente** finestra di dialogo, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="12d58-228">On hello **New User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="12d58-229">![Nuovo utente](./media/active-directory-saas-sumologic-tutorial/ic778563.png "Nuovo utente")</span><span class="sxs-lookup"><span data-stu-id="12d58-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="12d58-230">a.</span><span class="sxs-lookup"><span data-stu-id="12d58-230">a.</span></span> <span data-ttu-id="12d58-231">Hello tipo informazioni dell'account hello Azure AD desiderati tooprovision hello **nome**, **cognome**, e **posta elettronica** nelle caselle di testo.</span><span class="sxs-lookup"><span data-stu-id="12d58-231">Type hello related information of hello Azure AD account you want tooprovision into hello **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="12d58-232">b.</span><span class="sxs-lookup"><span data-stu-id="12d58-232">b.</span></span> <span data-ttu-id="12d58-233">Selezionare un ruolo.</span><span class="sxs-lookup"><span data-stu-id="12d58-233">Select a role.</span></span>
  
    <span data-ttu-id="12d58-234">c.</span><span class="sxs-lookup"><span data-stu-id="12d58-234">c.</span></span> <span data-ttu-id="12d58-235">Per **Status** (Stato) selezionare **Active** (Attivo).</span><span class="sxs-lookup"><span data-stu-id="12d58-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="12d58-236">d.</span><span class="sxs-lookup"><span data-stu-id="12d58-236">d.</span></span> <span data-ttu-id="12d58-237">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="12d58-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="12d58-238">È possibile usare qualsiasi altro SumoLogic utente account strumento di creazione o le API fornite da SumoLogic tooprovision account utente di AAD.</span><span class="sxs-lookup"><span data-stu-id="12d58-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="12d58-239">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="12d58-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="12d58-240">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSumoLogic.</span><span class="sxs-lookup"><span data-stu-id="12d58-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSumoLogic.</span></span>

![Assegna utente][200] 

<span data-ttu-id="12d58-242">**tooassign Britta Simon tooSumoLogic, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="12d58-242">**tooassign Britta Simon tooSumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="12d58-243">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="12d58-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="12d58-245">Nell'elenco di applicazioni hello, selezionare **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="12d58-245">In hello applications list, select **SumoLogic**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="12d58-247">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="12d58-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="12d58-249">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="12d58-249">Click **Add** button.</span></span> <span data-ttu-id="12d58-250">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="12d58-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="12d58-252">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="12d58-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="12d58-253">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="12d58-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="12d58-254">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="12d58-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="12d58-255">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="12d58-255">Testing single sign-on</span></span>

<span data-ttu-id="12d58-256">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="12d58-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="12d58-257">Quando si fa clic su riquadro SumoLogic hello in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour SumoLogic applicazione.</span><span class="sxs-lookup"><span data-stu-id="12d58-257">When you click hello SumoLogic tile in hello Access Panel, you should get automatically signed-on tooyour SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="12d58-258">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="12d58-258">Additional resources</span></span>

* [<span data-ttu-id="12d58-259">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12d58-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="12d58-260">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12d58-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

