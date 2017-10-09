---
title: 'Esercitazione: Integrazione di Azure Active Directory con TOPdesk - Public |Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e TOPdesk - Public.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="5bb11-103">Esercitazione: Integrazione di Azure Active Directory con TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="5bb11-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="5bb11-104">In questa esercitazione, è illustrato come toointegrate TOPdesk - Public con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5bb11-104">In this tutorial, you learn how toointegrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5bb11-105">L'integrazione di TOPdesk - Public con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="5bb11-105">Integrating TOPdesk - Public with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5bb11-106">È possibile controllare in Azure AD che ha accesso tooTOPdesk - pubblico.</span><span class="sxs-lookup"><span data-stu-id="5bb11-106">You can control in Azure AD who has access tooTOPdesk - Public.</span></span>
- <span data-ttu-id="5bb11-107">È possibile abilitare l'utenti tooautomatically get connesso tooTOPdesk - Public (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bb11-107">You can enable your users tooautomatically get signed-on tooTOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5bb11-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5bb11-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="5bb11-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5bb11-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bb11-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5bb11-110">Prerequisites</span></span>

<span data-ttu-id="5bb11-111">tooconfigure integrazione di Azure Active Directory con TOPdesk - Public, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="5bb11-111">tooconfigure Azure AD integration with TOPdesk - Public, you need hello following items:</span></span>

- <span data-ttu-id="5bb11-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bb11-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5bb11-113">Sottoscrizione di TOPdesk - Public abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5bb11-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5bb11-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="5bb11-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5bb11-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="5bb11-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5bb11-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="5bb11-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5bb11-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5bb11-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5bb11-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="5bb11-118">Scenario description</span></span>
<span data-ttu-id="5bb11-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="5bb11-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5bb11-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="5bb11-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5bb11-121">Aggiunta di TOPdesk - Public dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5bb11-121">Adding TOPdesk - Public from hello gallery</span></span>
2. <span data-ttu-id="5bb11-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb11-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-hello-gallery"></a><span data-ttu-id="5bb11-123">Aggiunta di TOPdesk - Public dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="5bb11-123">Adding TOPdesk - Public from hello gallery</span></span>
<span data-ttu-id="5bb11-124">integrazione di hello tooconfigure di TOPdesk - Public in Azure AD, è necessario tooadd TOPdesk - Public dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="5bb11-124">tooconfigure hello integration of TOPdesk - Public into Azure AD, you need tooadd TOPdesk - Public from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5bb11-125">**tooadd TOPdesk - Public dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5bb11-125">**tooadd TOPdesk - Public from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bb11-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="5bb11-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="5bb11-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5bb11-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="5bb11-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5bb11-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="5bb11-133">Nella casella di ricerca hello, digitare **TOPdesk - Public**selezionare **TOPdesk - Public** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5bb11-133">In hello search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nell'elenco dei risultati di TOPdesk - Public in hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5bb11-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb11-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5bb11-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con TOPdesk - Public usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5bb11-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5bb11-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in TOPdesk - Public tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bb11-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TOPdesk - Public is tooa user in Azure AD.</span></span> <span data-ttu-id="5bb11-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in TOPdesk - Public richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="5bb11-138">In other words, a link relationship between an Azure AD user and hello related user in TOPdesk - Public needs toobe established.</span></span>

<span data-ttu-id="5bb11-139">In TOPdesk - Public, assegnare un valore di hello hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="5bb11-139">In TOPdesk - Public, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5bb11-140">tooconfigure e testare Azure AD single sign-on con TOPdesk - Public, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="5bb11-140">tooconfigure and test Azure AD single sign-on with TOPdesk - Public, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5bb11-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5bb11-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5bb11-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5bb11-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5bb11-143">**[Creare un TOPdesk - pubblico test utente](#create-a-topdesk---public-test-user)**  - toohave un equivalente di Britta Simon in TOPdesk - pubblico che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5bb11-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - toohave a counterpart of Britta Simon in TOPdesk - Public that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5bb11-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5bb11-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5bb11-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="5bb11-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5bb11-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb11-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5bb11-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on in TOPdesk - Public applicazione.</span><span class="sxs-lookup"><span data-stu-id="5bb11-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="5bb11-148">**tooconfigure AD Azure single sign-on con TOPdesk - Public, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5bb11-148">**tooconfigure Azure AD single sign-on with TOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bb11-149">Nel portale di Azure su hello hello **TOPdesk - Public** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-149">In hello Azure portal, on hello **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="5bb11-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5bb11-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="5bb11-153">In hello **TOPdesk - URL e dominio pubblico** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5bb11-153">On hello **TOPdesk - Public Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni sull'accesso Single Sign-On per URL e dominio di TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="5bb11-155">a.</span><span class="sxs-lookup"><span data-stu-id="5bb11-155">a.</span></span> <span data-ttu-id="5bb11-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="5bb11-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="5bb11-157">b.</span><span class="sxs-lookup"><span data-stu-id="5bb11-157">b.</span></span> <span data-ttu-id="5bb11-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="5bb11-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="5bb11-159">c.</span><span class="sxs-lookup"><span data-stu-id="5bb11-159">c.</span></span> <span data-ttu-id="5bb11-160">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="5bb11-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="5bb11-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="5bb11-161">These values are not real.</span></span> <span data-ttu-id="5bb11-162">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="5bb11-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="5bb11-163">L'URL di risposta è descritto più avanti nell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5bb11-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="5bb11-164">Contatto [TOPdesk - team di supporto Client pubblico](https://help.topdesk.com/saas/enterprise/user/) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="5bb11-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) tooget these values.</span></span>  

4. <span data-ttu-id="5bb11-165">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5bb11-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="5bb11-167">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="5bb11-167">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="5bb11-169">In hello **TOPdesk - Public configurazione** fare clic su **configurare TOPdesk - Public** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="5bb11-169">On hello **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5bb11-170">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="5bb11-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="5bb11-172">Accesso tooyour **TOPdesk - Public** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5bb11-172">Sign on tooyour **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="5bb11-173">In hello **TOPdesk** menu, fare clic su **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-173">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="5bb11-174">![Impostazioni](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Impostazioni")</span><span class="sxs-lookup"><span data-stu-id="5bb11-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="5bb11-175">Fare clic su **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="5bb11-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span><span class="sxs-lookup"><span data-stu-id="5bb11-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="5bb11-177">Espandere hello **impostazioni di accesso** menu e quindi fare clic su **generale**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-177">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="5bb11-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="5bb11-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="5bb11-179">In hello **pubblica** sezione di hello **SAML login** configurazione seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5bb11-179">In hello **Public** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5bb11-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span><span class="sxs-lookup"><span data-stu-id="5bb11-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="5bb11-181">a.</span><span class="sxs-lookup"><span data-stu-id="5bb11-181">a.</span></span> <span data-ttu-id="5bb11-182">Fare clic su **scaricare** toodownload hello file di metadati pubblici e quindi salvarlo in locale nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="5bb11-182">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="5bb11-183">b.</span><span class="sxs-lookup"><span data-stu-id="5bb11-183">b.</span></span> <span data-ttu-id="5bb11-184">Aprire il file di metadati scaricato hello e individuare hello **AssertionConsumerService** nodo.</span><span class="sxs-lookup"><span data-stu-id="5bb11-184">Open hello downloaded metadata file, and then locate hello **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="5bb11-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="5bb11-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="5bb11-186">c.</span><span class="sxs-lookup"><span data-stu-id="5bb11-186">c.</span></span> <span data-ttu-id="5bb11-187">Hello copia **AssertionConsumerService** valore, incollare il valore in hello **URL di risposta** nella casella di testo **TOPdesk - URL e dominio pubblico** sezione.</span><span class="sxs-lookup"><span data-stu-id="5bb11-187">Copy hello **AssertionConsumerService** value, paste this value in hello **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="5bb11-188">toocreate un file di certificato, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5bb11-188">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="5bb11-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span><span class="sxs-lookup"><span data-stu-id="5bb11-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="5bb11-190">a.</span><span class="sxs-lookup"><span data-stu-id="5bb11-190">a.</span></span> <span data-ttu-id="5bb11-191">Aprire hello scaricata file di metadati dal portale Azure.</span><span class="sxs-lookup"><span data-stu-id="5bb11-191">Open hello downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="5bb11-192">b.</span><span class="sxs-lookup"><span data-stu-id="5bb11-192">b.</span></span> <span data-ttu-id="5bb11-193">Espandere hello **RoleDescriptor** nodo che dispone di un **xsi: Type** di **fed: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-193">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="5bb11-194">c.</span><span class="sxs-lookup"><span data-stu-id="5bb11-194">c.</span></span> <span data-ttu-id="5bb11-195">Copiare il valore di hello di hello **X509Certificate** nodo.</span><span class="sxs-lookup"><span data-stu-id="5bb11-195">Copy hello value of hello **X509Certificate** node.</span></span>
    
    <span data-ttu-id="5bb11-196">d.</span><span class="sxs-lookup"><span data-stu-id="5bb11-196">d.</span></span> <span data-ttu-id="5bb11-197">Salva hello copiato **X509Certificate** valore in locale nel computer in un file.</span><span class="sxs-lookup"><span data-stu-id="5bb11-197">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="5bb11-198">In hello **pubblica** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-198">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="5bb11-199">![Login SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "Login SAML")</span><span class="sxs-lookup"><span data-stu-id="5bb11-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="5bb11-200">In hello **Assistente configurazione SAML** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5bb11-200">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="5bb11-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span><span class="sxs-lookup"><span data-stu-id="5bb11-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="5bb11-202">a.</span><span class="sxs-lookup"><span data-stu-id="5bb11-202">a.</span></span> <span data-ttu-id="5bb11-203">tooupload i metadati scaricati file dal portale di Azure in **i metadati della federazione**, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-203">tooupload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="5bb11-204">b.</span><span class="sxs-lookup"><span data-stu-id="5bb11-204">b.</span></span> <span data-ttu-id="5bb11-205">file del certificato, in tooupload **Certificate (RSA)**, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-205">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="5bb11-206">c.</span><span class="sxs-lookup"><span data-stu-id="5bb11-206">c.</span></span> <span data-ttu-id="5bb11-207">file del logo hello tooupload ottenuto dal team di supporto di TOPdesk hello, in **icona del Logo**, fare clic su **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-207">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="5bb11-208">d.</span><span class="sxs-lookup"><span data-stu-id="5bb11-208">d.</span></span> <span data-ttu-id="5bb11-209">In hello **attributo nome utente** casella tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="5bb11-209">In hello **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="5bb11-210">e.</span><span class="sxs-lookup"><span data-stu-id="5bb11-210">e.</span></span> <span data-ttu-id="5bb11-211">In hello **nome visualizzato** casella di testo, digitare un nome per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="5bb11-211">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="5bb11-212">f.</span><span class="sxs-lookup"><span data-stu-id="5bb11-212">f.</span></span> <span data-ttu-id="5bb11-213">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5bb11-214">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="5bb11-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5bb11-215">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="5bb11-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5bb11-216">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5bb11-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5bb11-217">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb11-217">Create an Azure AD test user</span></span>

<span data-ttu-id="5bb11-218">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="5bb11-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="5bb11-220">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5bb11-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bb11-221">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="5bb11-221">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5bb11-223">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-223">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5bb11-225">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5bb11-225">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5bb11-227">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5bb11-227">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5bb11-229">a.</span><span class="sxs-lookup"><span data-stu-id="5bb11-229">a.</span></span> <span data-ttu-id="5bb11-230">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-230">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5bb11-231">b.</span><span class="sxs-lookup"><span data-stu-id="5bb11-231">b.</span></span> <span data-ttu-id="5bb11-232">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5bb11-232">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="5bb11-233">c.</span><span class="sxs-lookup"><span data-stu-id="5bb11-233">c.</span></span> <span data-ttu-id="5bb11-234">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="5bb11-234">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="5bb11-235">d.</span><span class="sxs-lookup"><span data-stu-id="5bb11-235">d.</span></span> <span data-ttu-id="5bb11-236">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="5bb11-237">Creare un utente di test di TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="5bb11-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="5bb11-238">In ordine tooenable Azure AD utenti toolog TopDesk - Public, è necessario eseguirne il provisioning in TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="5bb11-238">In order tooenable Azure AD users toolog into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="5bb11-239">Nel caso di hello di TOPdesk - Public, il provisioning è un'attività manuale.</span><span class="sxs-lookup"><span data-stu-id="5bb11-239">In hello case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="5bb11-240">tooconfigure provisioning degli utenti, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5bb11-240">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="5bb11-241">Accesso tooyour **TOPdesk - Public** sito aziendale come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5bb11-241">Sign on tooyour **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="5bb11-242">Scegliere dal menu hello in primo piano hello **TOPdesk \> New \> i file di supporto \> persona**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-242">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="5bb11-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span><span class="sxs-lookup"><span data-stu-id="5bb11-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="5bb11-244">Nella finestra di dialogo nuova persona hello eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5bb11-244">On hello New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="5bb11-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span><span class="sxs-lookup"><span data-stu-id="5bb11-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="5bb11-246">a.</span><span class="sxs-lookup"><span data-stu-id="5bb11-246">a.</span></span> <span data-ttu-id="5bb11-247">Fare clic sulla scheda Generale hello.</span><span class="sxs-lookup"><span data-stu-id="5bb11-247">Click hello General tab.</span></span>

    <span data-ttu-id="5bb11-248">b.</span><span class="sxs-lookup"><span data-stu-id="5bb11-248">b.</span></span> <span data-ttu-id="5bb11-249">In hello **Surname** casella di testo, digitare il cognome dell'utente hello come Simon</span><span class="sxs-lookup"><span data-stu-id="5bb11-249">In hello **Surname** textbox, type Surname of hello user like Simon</span></span>
 
    <span data-ttu-id="5bb11-250">c.</span><span class="sxs-lookup"><span data-stu-id="5bb11-250">c.</span></span> <span data-ttu-id="5bb11-251">Selezionare un **sito** per conto di hello.</span><span class="sxs-lookup"><span data-stu-id="5bb11-251">Select a **Site** for hello account.</span></span>
 
    <span data-ttu-id="5bb11-252">d.</span><span class="sxs-lookup"><span data-stu-id="5bb11-252">d.</span></span> <span data-ttu-id="5bb11-253">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="5bb11-254">È possibile utilizzare qualsiasi altro TOPdesk - strumento di creazione di account utente pubblica o le API fornite da TOPdesk - pubblico tooprovision Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="5bb11-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5bb11-255">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb11-255">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5bb11-256">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooTOPdesk - pubblico.</span><span class="sxs-lookup"><span data-stu-id="5bb11-256">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTOPdesk - Public.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="5bb11-258">**tooassign tooTOPdesk Britta Simon - Public, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="5bb11-258">**tooassign Britta Simon tooTOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bb11-259">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-259">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="5bb11-261">Nell'elenco di applicazioni hello, selezionare **TOPdesk - Public**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-261">In hello applications list, select **TOPdesk - Public**.</span></span>

    ![Hello TOPdesk - Public collegamento nell'elenco delle applicazioni hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="5bb11-263">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-263">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="5bb11-265">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-265">Click **Add** button.</span></span> <span data-ttu-id="5bb11-266">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="5bb11-268">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="5bb11-268">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5bb11-269">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5bb11-270">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="5bb11-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5bb11-271">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="5bb11-271">Test single sign-on</span></span>

<span data-ttu-id="5bb11-272">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="5bb11-272">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5bb11-273">Quando si fa clic hello TOPdesk - Public riquadro in hello Pannello di accesso, è necessario ottenere automaticamente firmato in tooyour TOPdesk - pubblico dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5bb11-273">When you click hello TOPdesk - Public tile in hello Access Panel, you should get automatically signed-on tooyour TOPdesk - Public application.</span></span>
<span data-ttu-id="5bb11-274">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5bb11-274">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5bb11-275">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5bb11-275">Additional resources</span></span>

* [<span data-ttu-id="5bb11-276">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bb11-276">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5bb11-277">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bb11-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

