---
title: 'Esercitazione: Integrazione di Azure Active Directory con Igloo Software | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Igloo Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="2f137-103">Esercitazione: Integrazione di Azure Active Directory con Igloo Software</span><span class="sxs-lookup"><span data-stu-id="2f137-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="2f137-104">In questa esercitazione, è illustrato come toointegrate Igloo Software con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f137-104">In this tutorial, you learn how toointegrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f137-105">Integrazione di Igloo Software con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="2f137-105">Integrating Igloo Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2f137-106">È possibile controllare in Azure AD che ha accesso tooIgloo Software</span><span class="sxs-lookup"><span data-stu-id="2f137-106">You can control in Azure AD who has access tooIgloo Software</span></span>
- <span data-ttu-id="2f137-107">È possibile abilitare l'utenti tooautomatically get connesso tooIgloo Software (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f137-107">You can enable your users tooautomatically get signed-on tooIgloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f137-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2f137-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2f137-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f137-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f137-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2f137-110">Prerequisites</span></span>

<span data-ttu-id="2f137-111">integrazione di Azure AD con Igloo Software tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="2f137-111">tooconfigure Azure AD integration with Igloo Software, you need hello following items:</span></span>

- <span data-ttu-id="2f137-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f137-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f137-113">Sottoscrizione di Igloo Software abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2f137-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f137-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="2f137-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f137-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="2f137-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f137-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="2f137-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f137-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f137-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f137-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="2f137-118">Scenario description</span></span>
<span data-ttu-id="2f137-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="2f137-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f137-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="2f137-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f137-121">Aggiunta di Igloo Software dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="2f137-121">Adding Igloo Software from hello gallery</span></span>
2. <span data-ttu-id="2f137-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f137-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-hello-gallery"></a><span data-ttu-id="2f137-123">Aggiunta di Igloo Software dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="2f137-123">Adding Igloo Software from hello gallery</span></span>
<span data-ttu-id="2f137-124">integrazione hello tooconfigure di Igloo Software in Azure AD, è necessario tooadd Igloo Software dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="2f137-124">tooconfigure hello integration of Igloo Software into Azure AD, you need tooadd Igloo Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2f137-125">**tooadd Igloo Software dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2f137-125">**tooadd Igloo Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f137-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="2f137-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f137-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="2f137-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2f137-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2f137-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="2f137-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2f137-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="2f137-133">Nella casella di ricerca hello, digitare **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="2f137-133">In hello search box, type **Igloo Software**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="2f137-135">Nel riquadro dei risultati hello, selezionare **Igloo Software**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2f137-135">In hello results panel, select **Igloo Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f137-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f137-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f137-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Igloo Software mediante un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2f137-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2f137-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Igloo Software è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f137-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Igloo Software is tooa user in Azure AD.</span></span> <span data-ttu-id="2f137-140">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Igloo Software richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="2f137-140">In other words, a link relationship between an Azure AD user and hello related user in Igloo Software needs toobe established.</span></span>

<span data-ttu-id="2f137-141">In Igloo Software, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="2f137-141">In Igloo Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2f137-142">tooconfigure e test Azure single sign-on AD con Igloo Software, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="2f137-142">tooconfigure and test Azure AD single sign-on with Igloo Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2f137-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2f137-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2f137-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f137-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f137-145">**[Creazione di un utente test Igloo Software](#creating-an-igloo-software-test-user)**  -toohave un equivalente di Britta Simon in Igloo Software che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2f137-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - toohave a counterpart of Britta Simon in Igloo Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2f137-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2f137-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f137-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="2f137-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f137-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f137-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f137-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="2f137-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="2f137-150">**Azure AD tooconfigure single sign-on con Igloo Software, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2f137-150">**tooconfigure Azure AD single sign-on with Igloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f137-151">Nel portale di Azure su hello hello **Igloo Software** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2f137-151">In hello Azure portal, on hello **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="2f137-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2f137-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="2f137-155">In hello **Igloo Software dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2f137-155">On hello **Igloo Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="2f137-157">a.</span><span class="sxs-lookup"><span data-stu-id="2f137-157">a.</span></span> <span data-ttu-id="2f137-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="2f137-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="2f137-159">b.</span><span class="sxs-lookup"><span data-stu-id="2f137-159">b.</span></span> <span data-ttu-id="2f137-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="2f137-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="2f137-161">c.</span><span class="sxs-lookup"><span data-stu-id="2f137-161">c.</span></span> <span data-ttu-id="2f137-162">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="2f137-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2f137-163">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="2f137-163">These values are not real.</span></span> <span data-ttu-id="2f137-164">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="2f137-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2f137-165">Contatto [team di supporto Igloo Software Client](https://www.igloosoftware.com/services/support) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="2f137-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="2f137-166">In hello **certificato di firma SAML** fare clic su **Certificate(Base64)** e quindi salvare il file di certificato hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="2f137-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="2f137-168">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="2f137-168">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="2f137-170">In hello **Igloo Software configurazione** fare clic su **Configura Igloo Software** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="2f137-170">On hello **Igloo Software Configuration** section, click **Configure Igloo Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2f137-171">Hello copia **Sign-Out URL e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="2f137-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="2f137-173">In una finestra del web browser, accedere come amministratore nel sito della società Igloo Software di tooyour.</span><span class="sxs-lookup"><span data-stu-id="2f137-173">In a different web browser window, log in tooyour Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="2f137-174">Passare toohello **Pannello di controllo**.</span><span class="sxs-lookup"><span data-stu-id="2f137-174">Go toohello **Control Panel**.</span></span>
   
     <span data-ttu-id="2f137-175">![Pannello di controllo](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Pannello di controllo")</span><span class="sxs-lookup"><span data-stu-id="2f137-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="2f137-176">In hello **appartenenza** scheda, fare clic su **Sign In Settings**.</span><span class="sxs-lookup"><span data-stu-id="2f137-176">In hello **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="2f137-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span><span class="sxs-lookup"><span data-stu-id="2f137-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="2f137-178">Nella sezione di configurazione SAML hello, fare clic su **Configure SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="2f137-178">In hello SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="2f137-179">![Configurazione SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "Configurazione SAML")</span><span class="sxs-lookup"><span data-stu-id="2f137-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="2f137-180">In hello **configurazione generale** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2f137-180">In hello **General Configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="2f137-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span><span class="sxs-lookup"><span data-stu-id="2f137-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="2f137-182">a.</span><span class="sxs-lookup"><span data-stu-id="2f137-182">a.</span></span> <span data-ttu-id="2f137-183">In hello **nome connessione** casella di testo, digitare un nome personalizzato per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="2f137-183">In hello **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="2f137-184">b.</span><span class="sxs-lookup"><span data-stu-id="2f137-184">b.</span></span> <span data-ttu-id="2f137-185">In hello **IdP Login URL** casella di testo, hello Incolla valore **SAML Single Sign-On Service URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f137-185">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="2f137-186">c.</span><span class="sxs-lookup"><span data-stu-id="2f137-186">c.</span></span> <span data-ttu-id="2f137-187">In hello **IdP Logout URL** casella di testo, hello Incolla valore **Sign-Out URL** che è stato copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f137-187">In hello **IdP Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="2f137-188">d.</span><span class="sxs-lookup"><span data-stu-id="2f137-188">d.</span></span> <span data-ttu-id="2f137-189">Selezionare **Logout Response and Request HTTP Type** (Risposta di disconnessione e tipo di richiesta HTTP) con l'impostazione **POST**.</span><span class="sxs-lookup"><span data-stu-id="2f137-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="2f137-190">e.</span><span class="sxs-lookup"><span data-stu-id="2f137-190">e.</span></span> <span data-ttu-id="2f137-191">Aprire il **base 64** codificato nel blocco note scaricato dal portale di Azure, hello copia del contenuto di esso negli Appunti, certificato e quindi incollarlo toohello **certificato pubblico** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="2f137-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="2f137-192">In hello **Response and Authentication Configuration**, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2f137-192">In hello **Response and Authentication Configuration**, perform hello following steps:</span></span>
    
    <span data-ttu-id="2f137-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span><span class="sxs-lookup"><span data-stu-id="2f137-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="2f137-194">a.</span><span class="sxs-lookup"><span data-stu-id="2f137-194">a.</span></span> <span data-ttu-id="2f137-195">In **Provider di identità** selezionare **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="2f137-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="2f137-196">b.</span><span class="sxs-lookup"><span data-stu-id="2f137-196">b.</span></span> <span data-ttu-id="2f137-197">In **Tipo di identificatore** selezionare **Indirizzo e-mail**.</span><span class="sxs-lookup"><span data-stu-id="2f137-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="2f137-198">c.</span><span class="sxs-lookup"><span data-stu-id="2f137-198">c.</span></span> <span data-ttu-id="2f137-199">In hello **Email Attribute** casella tipo **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="2f137-199">In hello **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="2f137-200">d.</span><span class="sxs-lookup"><span data-stu-id="2f137-200">d.</span></span> <span data-ttu-id="2f137-201">In hello **First Name Attribute** casella tipo **givenname**.</span><span class="sxs-lookup"><span data-stu-id="2f137-201">In hello **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="2f137-202">e.</span><span class="sxs-lookup"><span data-stu-id="2f137-202">e.</span></span> <span data-ttu-id="2f137-203">In hello **Last Name Attribute** casella tipo **surname**.</span><span class="sxs-lookup"><span data-stu-id="2f137-203">In hello **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="2f137-204">Eseguire hello seguente passaggi toocomplete hello configurazione:</span><span class="sxs-lookup"><span data-stu-id="2f137-204">Perform hello following steps toocomplete hello configuration:</span></span>
    
    <span data-ttu-id="2f137-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span><span class="sxs-lookup"><span data-stu-id="2f137-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="2f137-206">a.</span><span class="sxs-lookup"><span data-stu-id="2f137-206">a.</span></span> <span data-ttu-id="2f137-207">In **User creation on Sign in** (Creazione utente all'accesso) selezionare **Create a new user in your site when they sign in** (Creare un nuovo utente all'accesso).</span><span class="sxs-lookup"><span data-stu-id="2f137-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="2f137-208">b.</span><span class="sxs-lookup"><span data-stu-id="2f137-208">b.</span></span> <span data-ttu-id="2f137-209">In **Impostazioni di accesso** selezionare **Usa pulsante SAML nella schermata di accesso**.</span><span class="sxs-lookup"><span data-stu-id="2f137-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="2f137-210">c.</span><span class="sxs-lookup"><span data-stu-id="2f137-210">c.</span></span> <span data-ttu-id="2f137-211">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="2f137-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2f137-212">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="2f137-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2f137-213">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="2f137-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2f137-214">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f137-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f137-215">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f137-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f137-216">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="2f137-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="2f137-218">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2f137-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f137-219">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="2f137-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f137-221">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="2f137-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f137-223">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="2f137-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f137-225">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2f137-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f137-227">a.</span><span class="sxs-lookup"><span data-stu-id="2f137-227">a.</span></span> <span data-ttu-id="2f137-228">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f137-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f137-229">b.</span><span class="sxs-lookup"><span data-stu-id="2f137-229">b.</span></span> <span data-ttu-id="2f137-230">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2f137-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f137-231">c.</span><span class="sxs-lookup"><span data-stu-id="2f137-231">c.</span></span> <span data-ttu-id="2f137-232">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="2f137-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2f137-233">d.</span><span class="sxs-lookup"><span data-stu-id="2f137-233">d.</span></span> <span data-ttu-id="2f137-234">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2f137-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="2f137-235">Creazione di un utente test di Igloo Software</span><span class="sxs-lookup"><span data-stu-id="2f137-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="2f137-236">Non sono presenti elementi di azione per si tooconfigure di provisioning dell'utente tooIgloo Software.</span><span class="sxs-lookup"><span data-stu-id="2f137-236">There is no action item for you tooconfigure user provisioning tooIgloo Software.</span></span>  

<span data-ttu-id="2f137-237">Quando un utente assegnato tenta di toolog in tooIgloo Software hello Pannello di accesso, Igloo Software verifica l'esistenza di utente hello.</span><span class="sxs-lookup"><span data-stu-id="2f137-237">When an assigned user tries toolog in tooIgloo Software using hello access panel, Igloo Software checks whether hello user exists.</span></span>  <span data-ttu-id="2f137-238">Se l'account utente non è presente, Igloo Software lo crea automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2f137-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2f137-239">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f137-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2f137-240">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooIgloo Software.</span><span class="sxs-lookup"><span data-stu-id="2f137-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIgloo Software.</span></span>

![Assegna utente][200] 

<span data-ttu-id="2f137-242">**tooassign Britta Simon tooIgloo Software, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="2f137-242">**tooassign Britta Simon tooIgloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f137-243">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="2f137-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="2f137-245">Nell'elenco di applicazioni hello, selezionare **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="2f137-245">In hello applications list, select **Igloo Software**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="2f137-247">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2f137-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="2f137-249">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2f137-249">Click **Add** button.</span></span> <span data-ttu-id="2f137-250">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2f137-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="2f137-252">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="2f137-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2f137-253">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="2f137-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f137-254">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="2f137-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f137-255">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="2f137-255">Testing single sign-on</span></span>

<span data-ttu-id="2f137-256">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="2f137-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2f137-257">Quando si fa clic su riquadro Igloo Software hello in hello Pannello di accesso, è necessario ottenere applicazione Igloo Software tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="2f137-257">When you click hello Igloo Software tile in hello Access Panel, you should get automatically signed-on tooyour Igloo Software application.</span></span>
<span data-ttu-id="2f137-258">Per ulteriori informazioni sul pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2f137-258">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2f137-259">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2f137-259">Additional resources</span></span>

* [<span data-ttu-id="2f137-260">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f137-260">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f137-261">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f137-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

