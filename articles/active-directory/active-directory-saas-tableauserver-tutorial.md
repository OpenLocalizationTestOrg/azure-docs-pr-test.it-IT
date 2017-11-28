---
title: 'Esercitazione: Integrazione di Azure Active Directory con Tableau Server | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Tableau Server.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="4ed87-103">Esercitazione: Integrazione di Azure Active Directory con Tableau Server</span><span class="sxs-lookup"><span data-stu-id="4ed87-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="4ed87-104">In questa esercitazione, è illustrato come toointegrate Tableau Server con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4ed87-104">In this tutorial, you learn how toointegrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4ed87-105">Integrazione di Server Tableau con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4ed87-105">Integrating Tableau Server with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4ed87-106">È possibile controllare in Azure AD che ha accesso tooTableau Server</span><span class="sxs-lookup"><span data-stu-id="4ed87-106">You can control in Azure AD who has access tooTableau Server</span></span>
- <span data-ttu-id="4ed87-107">È possibile abilitare l'utenti tooautomatically get connesso tooTableau Server (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ed87-107">You can enable your users tooautomatically get signed-on tooTableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4ed87-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4ed87-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4ed87-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4ed87-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ed87-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4ed87-110">Prerequisites</span></span>

<span data-ttu-id="4ed87-111">integrazione di Azure AD con Server Tableau tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4ed87-111">tooconfigure Azure AD integration with Tableau Server, you need hello following items:</span></span>

- <span data-ttu-id="4ed87-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ed87-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4ed87-113">Sottoscrizione di Tableau Server abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4ed87-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4ed87-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4ed87-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4ed87-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4ed87-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4ed87-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4ed87-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4ed87-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ed87-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4ed87-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4ed87-118">Scenario description</span></span>
<span data-ttu-id="4ed87-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4ed87-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4ed87-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4ed87-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4ed87-121">Aggiunta di Server Tableau dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4ed87-121">Adding Tableau Server from hello gallery</span></span>
2. <span data-ttu-id="4ed87-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ed87-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-hello-gallery"></a><span data-ttu-id="4ed87-123">Aggiunta di Server Tableau dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4ed87-123">Adding Tableau Server from hello gallery</span></span>
<span data-ttu-id="4ed87-124">integrazione hello tooconfigure di Tableau Server in Azure AD, è necessario tooadd Tableau Server dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4ed87-124">tooconfigure hello integration of Tableau Server into Azure AD, you need tooadd Tableau Server from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4ed87-125">**tooadd Tableau Server dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4ed87-125">**tooadd Tableau Server from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ed87-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4ed87-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4ed87-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4ed87-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="4ed87-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4ed87-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="4ed87-133">Nella casella di ricerca hello, digitare **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-133">In hello search box, type **Tableau Server**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="4ed87-135">Nel riquadro dei risultati hello, selezionare **Tableau Server**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4ed87-135">In hello results panel, select **Tableau Server**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4ed87-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ed87-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4ed87-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Tableau Server usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4ed87-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4ed87-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Server Tableau è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ed87-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Server is tooa user in Azure AD.</span></span> <span data-ttu-id="4ed87-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in Server Tableau deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="4ed87-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Server needs toobe established.</span></span>

<span data-ttu-id="4ed87-141">Nel Server Tableau, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="4ed87-141">In Tableau Server, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4ed87-142">tooconfigure e prova AD Azure single sign-on con Server Tableau, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4ed87-142">tooconfigure and test Azure AD single sign-on with Tableau Server, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4ed87-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4ed87-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4ed87-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4ed87-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4ed87-145">**[Creazione di un utente test Tableau Server](#creating-a-tableau-server-test-user)**  -toohave un equivalente di Britta Simon Tableau server che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4ed87-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - toohave a counterpart of Britta Simon in Tableau Server that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4ed87-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4ed87-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4ed87-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4ed87-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4ed87-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ed87-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4ed87-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione Server Tableau.</span><span class="sxs-lookup"><span data-stu-id="4ed87-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="4ed87-150">**Azure AD tooconfigure single sign-on con Server Tableau, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4ed87-150">**tooconfigure Azure AD single sign-on with Tableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ed87-151">Nel portale di Azure su hello hello **Tableau Server** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-151">In hello Azure portal, on hello **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="4ed87-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4ed87-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="4ed87-155">In hello **Tableau dominio del Server e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4ed87-155">On hello **Tableau Server Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="4ed87-157">a.</span><span class="sxs-lookup"><span data-stu-id="4ed87-157">a.</span></span> <span data-ttu-id="4ed87-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="4ed87-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="4ed87-159">b.</span><span class="sxs-lookup"><span data-stu-id="4ed87-159">b.</span></span> <span data-ttu-id="4ed87-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="4ed87-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="4ed87-161">c.</span><span class="sxs-lookup"><span data-stu-id="4ed87-161">c.</span></span> <span data-ttu-id="4ed87-162">In hello **URL di risposta** casella di testo, digitare un URL utilizzando hello seguente modello:`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="4ed87-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="4ed87-163">Hello valori precedenti non sono valori reali.</span><span class="sxs-lookup"><span data-stu-id="4ed87-163">hello preceding values are not real values.</span></span> <span data-ttu-id="4ed87-164">In un secondo momento, aggiornare i valori hello con URL effettivo hello e l'identificatore dalla pagina di configurazione Server Tableau hello.</span><span class="sxs-lookup"><span data-stu-id="4ed87-164">Later, you update hello values with hello actual URL and identifier from hello Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="4ed87-165">Applicazione Server tableau prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="4ed87-165">Tableau Server application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="4ed87-166">Configurare hello seguendo le attestazioni per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ed87-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="4ed87-167">È possibile gestire i valori hello di questi attributi da hello **"Attributi utente"** sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ed87-167">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="4ed87-168">Hello schermata riportata di seguito viene illustrato un esempio di hello stesso.</span><span class="sxs-lookup"><span data-stu-id="4ed87-168">hello following screenshot shows an example for hello same.</span></span>
    
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="4ed87-170">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine di hello precedente ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4ed87-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="4ed87-171">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="4ed87-171">Attribute Name</span></span> | <span data-ttu-id="4ed87-172">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="4ed87-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="4ed87-173">username</span><span class="sxs-lookup"><span data-stu-id="4ed87-173">username</span></span> | <span data-ttu-id="4ed87-174">*user.displayname*</span><span class="sxs-lookup"><span data-stu-id="4ed87-174">*user.displayname*</span></span> |

    <span data-ttu-id="4ed87-175">a.</span><span class="sxs-lookup"><span data-stu-id="4ed87-175">a.</span></span> <span data-ttu-id="4ed87-176">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4ed87-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="4ed87-179">b.</span><span class="sxs-lookup"><span data-stu-id="4ed87-179">b.</span></span> <span data-ttu-id="4ed87-180">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="4ed87-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="4ed87-181">c.</span><span class="sxs-lookup"><span data-stu-id="4ed87-181">c.</span></span> <span data-ttu-id="4ed87-182">Da hello **valore** elencare, valore dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="4ed87-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4ed87-183">d.</span><span class="sxs-lookup"><span data-stu-id="4ed87-183">d.</span></span> <span data-ttu-id="4ed87-184">Fare clic su **Ok**</span><span class="sxs-lookup"><span data-stu-id="4ed87-184">Click **Ok**</span></span>


6. <span data-ttu-id="4ed87-185">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4ed87-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="4ed87-187">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4ed87-187">Click **Save** button.</span></span>

    <span data-ttu-id="4ed87-188">![Configurare l'accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="4ed87-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="4ed87-189">tooget SSO configurato per l'applicazione, è necessario tooyour toosign-nel tenant di Tableau Server come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4ed87-189">tooget SSO configured for your application, you need toosign-on tooyour Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="4ed87-190">a.</span><span class="sxs-lookup"><span data-stu-id="4ed87-190">a.</span></span> <span data-ttu-id="4ed87-191">In configurazione Server Tableau hello, fare clic su hello **SAML** scheda.</span><span class="sxs-lookup"><span data-stu-id="4ed87-191">In hello Tableau Server configuration, click hello **SAML** tab.</span></span>
  
    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="4ed87-193">b.</span><span class="sxs-lookup"><span data-stu-id="4ed87-193">b.</span></span> <span data-ttu-id="4ed87-194">Selezionare una casella di controllo hello **Use SAML single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-194">Select hello checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="4ed87-195">c.</span><span class="sxs-lookup"><span data-stu-id="4ed87-195">c.</span></span> <span data-ttu-id="4ed87-196">URL restituito tableau Server: URL del Server Tableau gli utenti accedono, ad esempio http://tableau_server hello.</span><span class="sxs-lookup"><span data-stu-id="4ed87-196">Tableau Server return URL—hello URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="4ed87-197">Non è consigliabile utilizzare http://localhost.</span><span class="sxs-lookup"><span data-stu-id="4ed87-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="4ed87-198">Gli URL con barra finale (ad esempio http://tableau_server/) non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="4ed87-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="4ed87-199">Copia **URL restituito Server Tableau** e incollarlo tooAzure AD **URL di accesso** nella casella di testo **Tableau dominio del Server e gli URL** sezione.</span><span class="sxs-lookup"><span data-stu-id="4ed87-199">Copy **Tableau Server return URL** and paste it tooAzure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="4ed87-200">d.</span><span class="sxs-lookup"><span data-stu-id="4ed87-200">d.</span></span> <span data-ttu-id="4ed87-201">ID entità SAML: hello entity ID che identifica in modo univoco il toohello di installazione Server Tableau IdP.</span><span class="sxs-lookup"><span data-stu-id="4ed87-201">SAML entity ID—hello entity ID uniquely identifies your Tableau Server installation toohello IdP.</span></span> <span data-ttu-id="4ed87-202">È possibile immettere l'URL del Server Tableau nuovamente in questo caso, se si desidera, ma non è toobe l'URL del Server Tableau.</span><span class="sxs-lookup"><span data-stu-id="4ed87-202">You can enter your Tableau Server URL again here, if you like, but it does not have toobe your Tableau Server URL.</span></span> <span data-ttu-id="4ed87-203">Copia **ID entità SAML** e incollarlo tooAzure AD **identificatore** nella casella di testo **Tableau dominio del Server e gli URL** sezione.</span><span class="sxs-lookup"><span data-stu-id="4ed87-203">Copy **SAML entity ID** and paste it tooAzure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="4ed87-204">e.</span><span class="sxs-lookup"><span data-stu-id="4ed87-204">e.</span></span> <span data-ttu-id="4ed87-205">Fare clic su hello **Esporta File di metadati** e aprirlo in un'applicazione hello testo dell'editor.</span><span class="sxs-lookup"><span data-stu-id="4ed87-205">Click hello **Export Metadata File** and open it in hello text editor application.</span></span> <span data-ttu-id="4ed87-206">Individuare l'URL di servizio Consumer di asserzione con Http Post e indice 0 e copia hello URL.</span><span class="sxs-lookup"><span data-stu-id="4ed87-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy hello URL.</span></span> <span data-ttu-id="4ed87-207">Ora incollarlo tooAzure AD **URL di risposta** nella casella di testo **Tableau dominio del Server e gli URL** sezione.</span><span class="sxs-lookup"><span data-stu-id="4ed87-207">Now paste it tooAzure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="4ed87-208">f.</span><span class="sxs-lookup"><span data-stu-id="4ed87-208">f.</span></span> <span data-ttu-id="4ed87-209">Individuare il file di metadati di federazione scaricato dal portale di Azure e quindi caricarlo in hello **file di metadati del provider di identità SAML**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in hello **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="4ed87-210">g.</span><span class="sxs-lookup"><span data-stu-id="4ed87-210">g.</span></span> <span data-ttu-id="4ed87-211">Fare clic su hello **OK** nella pagina Configurazione Server Tableau hello.</span><span class="sxs-lookup"><span data-stu-id="4ed87-211">Click hello **OK** button in hello Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="4ed87-212">Cliente tooupload qualsiasi certificato nella configurazione di hello Tableau Server SAML SSO e si verrà ottenere ignorato in hello flusso SSO.</span><span class="sxs-lookup"><span data-stu-id="4ed87-212">Customer have tooupload any certificate in hello Tableau Server SAML SSO configuration and it will get ignored in hello SSO flow.</span></span>
    ><span data-ttu-id="4ed87-213">Se si devono consentire la configurazione SAML nel Server Tableau, vedere l'articolo toothis [configurare SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="4ed87-213">If you need help configuring SAML on Tableau Server then please refer toothis article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="4ed87-214">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="4ed87-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4ed87-215">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="4ed87-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4ed87-216">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4ed87-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4ed87-217">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ed87-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="4ed87-218">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4ed87-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="4ed87-220">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4ed87-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ed87-221">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4ed87-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4ed87-223">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4ed87-225">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="4ed87-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4ed87-227">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4ed87-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4ed87-229">a.</span><span class="sxs-lookup"><span data-stu-id="4ed87-229">a.</span></span> <span data-ttu-id="4ed87-230">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4ed87-231">b.</span><span class="sxs-lookup"><span data-stu-id="4ed87-231">b.</span></span> <span data-ttu-id="4ed87-232">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4ed87-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4ed87-233">c.</span><span class="sxs-lookup"><span data-stu-id="4ed87-233">c.</span></span> <span data-ttu-id="4ed87-234">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4ed87-235">d.</span><span class="sxs-lookup"><span data-stu-id="4ed87-235">d.</span></span> <span data-ttu-id="4ed87-236">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="4ed87-237">Creazione di un utente test di Tableau Server</span><span class="sxs-lookup"><span data-stu-id="4ed87-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="4ed87-238">obiettivo di Hello di questa sezione è un utente denominato Britta Simon Tableau server toocreate.</span><span class="sxs-lookup"><span data-stu-id="4ed87-238">hello objective of this section is toocreate a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="4ed87-239">È necessario tooprovision tutti gli utenti di hello server Tableau hello.</span><span class="sxs-lookup"><span data-stu-id="4ed87-239">You need tooprovision all hello users in hello Tableau server.</span></span> 

<span data-ttu-id="4ed87-240">Nome utente dell'utente hello deve corrispondere il valore hello che è stato configurato nell'attributo personalizzato di hello Azure AD di **username**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-240">That username of hello user should match hello value which you have configured in hello Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="4ed87-241">Con hello corretto mapping integrazione hello dovrebbe funzionare [configurazione Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="4ed87-241">With hello correct mapping hello integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="4ed87-242">Se è necessario un utente toocreate manualmente, è necessario toocontact messaggio Tableau Server per l'amministratore dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="4ed87-242">If you need toocreate a user manually, you need toocontact hello Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4ed87-243">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ed87-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4ed87-244">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooTableau Server.</span><span class="sxs-lookup"><span data-stu-id="4ed87-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Server.</span></span>

![Assegna utente][200] 

<span data-ttu-id="4ed87-246">**tooassign Britta Simon tooTableau Server, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4ed87-246">**tooassign Britta Simon tooTableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="4ed87-247">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4ed87-249">Nell'elenco di applicazioni hello, selezionare **Tableau Server**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-249">In hello applications list, select **Tableau Server**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="4ed87-251">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="4ed87-253">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-253">Click **Add** button.</span></span> <span data-ttu-id="4ed87-254">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="4ed87-256">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="4ed87-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4ed87-257">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4ed87-258">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4ed87-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4ed87-259">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4ed87-259">Testing single sign-on</span></span>

<span data-ttu-id="4ed87-260">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4ed87-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4ed87-261">Quando si fa clic su riquadro Server Tableau hello in hello Pannello di accesso, è necessario ottenere l'applicazione Server Tableau tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="4ed87-261">When you click hello Tableau Server tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Server application.</span></span>
<span data-ttu-id="4ed87-262">Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="4ed87-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4ed87-263">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4ed87-263">Additional resources</span></span>

* [<span data-ttu-id="4ed87-264">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ed87-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4ed87-265">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ed87-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

