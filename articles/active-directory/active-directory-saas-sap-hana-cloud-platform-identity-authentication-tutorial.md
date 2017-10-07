---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP HANA Cloud Platform Identity Authentication |Microsoft Docs'
description: "Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SAP HANA Cloud Platform identità autenticazione."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="1781a-103">Esercitazione: Integrazione di Azure Active Directory con SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="1781a-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="1781a-104">In questa esercitazione, è illustrato come toointegrate SAP HANA Cloud Platform identità autenticazione con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1781a-104">In this tutorial, you learn how toointegrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="1781a-105">Autenticazione dell'identità di SAP HANA Cloud Platform viene utilizzato un proxy IdP tooaccess SAP come applicazioni che utilizzano Azure AD come hello IdP principale.</span><span class="sxs-lookup"><span data-stu-id="1781a-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP tooaccess SAP applications using Azure AD as hello main IdP.</span></span>

<span data-ttu-id="1781a-106">Integrazione di autenticazione dell'identità di SAP HANA Cloud Platform con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="1781a-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1781a-107">È possibile controllare in Azure AD che ha accesso tooSAP applicazione</span><span class="sxs-lookup"><span data-stu-id="1781a-107">You can control in Azure AD who has access tooSAP application</span></span>
- <span data-ttu-id="1781a-108">È possibile abilitare l'utenti tooautomatically get connesso tooSAP applicazioni single sign-on (SSO) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="1781a-108">You can enable your users tooautomatically get signed-on tooSAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="1781a-109">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="1781a-109">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="1781a-110">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1781a-110">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="1781a-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1781a-111">Prerequisites</span></span>

<span data-ttu-id="1781a-112">tooconfigure integrazione di Azure AD con l'autenticazione dell'identità di SAP HANA Cloud Platform, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1781a-112">tooconfigure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need hello following items:</span></span>

- <span data-ttu-id="1781a-113">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1781a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="1781a-114">Sottoscrizione di **SAP HANA Cloud Platform Identity Authentication** abilitata per l'accesso SSO</span><span class="sxs-lookup"><span data-stu-id="1781a-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="1781a-115">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1781a-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="1781a-116">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="1781a-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1781a-117">Non usare l'ambiente di produzione, a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="1781a-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1781a-118">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1781a-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1781a-119">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="1781a-119">Scenario description</span></span>
<span data-ttu-id="1781a-120">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1781a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="1781a-121">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="1781a-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1781a-122">Aggiunta di autenticazione dell'identità di SAP HANA Cloud Platform dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1781a-122">Adding SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
2. <span data-ttu-id="1781a-123">Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="1781a-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="1781a-124">Prima di leggere i dettagli tecnici di hello, è essenziale toounderstand concetti di hello in che eseguirai toolook.</span><span class="sxs-lookup"><span data-stu-id="1781a-124">Before diving into hello technical details, it is vital toounderstand hello concepts you're going toolook at.</span></span> <span data-ttu-id="1781a-125">Autenticazione dell'identità di SAP HANA Cloud Platform e Azure Active Directory federation Hello consente tooimplement SSO tra applicazioni o servizi protetti da Azure ad (come un provider di identità) con le applicazioni SAP e servizi protetti dall'identità di SAP HANA Cloud Platform Autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1781a-125">hello SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you tooimplement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="1781a-126">Attualmente, l'autenticazione identità di SAP HANA Cloud Platform funge da un Provider di identità Proxy tooSAP-applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1781a-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider tooSAP-applications.</span></span> <span data-ttu-id="1781a-127">Azure Active Directory è a sua volta agisce come hello iniziali di Provider di identità in questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="1781a-127">Azure Active Directory in turn acts as hello leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="1781a-128">Hello seguente diagramma viene illustrata questa situazione:</span><span class="sxs-lookup"><span data-stu-id="1781a-128">hello following diagram illustrates this:</span></span>    

![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="1781a-130">Con questa configurazione, il tenant di SAP HANA Cloud Platform Identity Authentication viene configurato come applicazione attendibile in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1781a-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="1781a-131">Tutte le applicazioni SAP e servizi da tooprotect tramite in questo modo vengono configurati successivamente nella console di gestione di autenticazione dell'identità di SAP HANA Cloud Platform hello!</span><span class="sxs-lookup"><span data-stu-id="1781a-131">All SAP applications and services you want tooprotect through this way are subsequently configured in hello SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="1781a-132">Questo significa che tale autorizzazione per la concessione dell'accesso tooSAP applicazioni e servizi sul posto tootake esigenze in SAP HANA Cloud Platform identità di autenticazione per una configurazione di questo tipo (come tooconfiguring anziché l'autorizzazione in Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1781a-132">This means that authorization for granting access tooSAP applications and services needs tootake place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed tooconfiguring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="1781a-133">Tramite la configurazione di autenticazione dell'identità di SAP HANA Cloud Platform come un'applicazione tramite Azure Active Directory Marketplace hello, non è necessario tootake cure attestazioni singole richieste di configurazione / asserzioni SAML e le trasformazioni necessarie tooproduce un token di autenticazione valido per le applicazioni SAP.</span><span class="sxs-lookup"><span data-stu-id="1781a-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through hello Azure Active Directory Marketplace, you don't need tootake care of configuring needed individual claims / SAML assertions and transformations needed tooproduce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="1781a-134">Attualmente solo Web SSO è stato testato da entrambe le parti.</span><span class="sxs-lookup"><span data-stu-id="1781a-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="1781a-135">I flussi necessari per la comunicazione da App a API o da API a API dovrebbero funzionare ma non sono ancora stati testati.</span><span class="sxs-lookup"><span data-stu-id="1781a-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="1781a-136">I test verranno eseguiti come parte delle attività successive.</span><span class="sxs-lookup"><span data-stu-id="1781a-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a><span data-ttu-id="1781a-137">Aggiungere l'autenticazione dell'identità di SAP HANA Cloud Platform dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="1781a-137">Add SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
<span data-ttu-id="1781a-138">integrazione hello tooconfigure di SAP HANA Cloud Platform identità autenticazione in Azure AD, è necessario tooadd autenticazione dell'identità di SAP HANA Cloud Platform dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="1781a-138">tooconfigure hello integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1781a-139">**Autenticazione identità dalla raccolta di hello, SAP HANA Cloud Platform tooadd eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1781a-139">**tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1781a-140">In hello [ **portale di gestione di Azure**](https://portal.azure.com)via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1781a-140">In hello [**Azure Management portal**](https://portal.azure.com), on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1781a-142">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="1781a-142">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1781a-143">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1781a-143">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="1781a-145">Fare clic su **Aggiungi** pulsante nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="1781a-145">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="1781a-147">Nella casella di ricerca hello, digitare **autenticazione dell'identità di SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="1781a-147">In hello search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="1781a-149">Nel riquadro dei risultati hello, selezionare **autenticazione dell'identità di SAP HANA Cloud Platform**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1781a-149">In hello results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1781a-151">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1781a-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1781a-152">In questa sezione viene configurato e testato l'accesso SSO di Azure AD con SAP HANA Cloud Platform Identity Authentication con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1781a-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1781a-153">Per toowork SSO, Azure AD deve tooknow quale utente controparte hello in SAP HANA Cloud Platform identità autenticazione è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1781a-153">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA Cloud Platform Identity Authentication is tooa user in Azure AD.</span></span> <span data-ttu-id="1781a-154">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello in SAP HANA Cloud Platform identità autenticazione richiede toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="1781a-154">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA Cloud Platform Identity Authentication needs toobe established.</span></span>

<span data-ttu-id="1781a-155">Questa relazione di collegamento viene stabilita tramite l'assegnazione valore hello di hello **nome utente** in Azure AD come valore hello hello **Username** nell'autenticazione dell'identità di SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="1781a-155">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="1781a-156">tooconfigure e test SSO AD Azure con l'autenticazione dell'identità di SAP HANA Cloud Platform, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="1781a-156">tooconfigure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1781a-157">**[Configurazione di Azure single sign-on AD](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="1781a-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1781a-158">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1781a-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1781a-159">**[Creazione di un utente di test di autenticazione dell'identità di SAP HANA Cloud Platform](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave un equivalente di Britta Simon in SAP HANA Cloud Platform autenticazione identità che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="1781a-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - toohave a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="1781a-160">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1781a-160">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1781a-161">**[Test di accesso single sign-on](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="1781a-161">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="1781a-162">Configurazione dell'accesso Single Sign-On (SSO) di Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="1781a-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="1781a-163">In questa sezione abilitare SSO AD Azure nel portale di gestione di Azure hello e configurare single sign-on nell'applicazione SAP HANA Cloud Platform identità autenticazione.</span><span class="sxs-lookup"><span data-stu-id="1781a-163">In this section, you enable Azure AD SSO in hello Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="1781a-164">Applicazione di autenticazione dell'identità di SAP HANA Cloud Platform prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="1781a-164">SAP HANA Cloud Platform Identity Authentication application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="1781a-165">È possibile gestire i valori hello di questi attributi da hello "**gli attributi utente**" sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1781a-165">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="1781a-166">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="1781a-166">hello following screenshot shows an example for this.</span></span>

![Configura accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="1781a-168">**tooconfigure SSO AD Azure con l'autenticazione identità di SAP HANA Cloud Platform, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1781a-168">**tooconfigure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="1781a-169">Nel portale di gestione di Azure hello in hello **autenticazione dell'identità di SAP HANA Cloud Platform** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1781a-169">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="1781a-171">In hello **Single sign-on** finestra di dialogo, come **modalità** selezionare **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1781a-171">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configura accesso Single Sign-On][5]

3. <span data-ttu-id="1781a-173">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, se l'applicazione SAP prevede un attributo, ad esempio "firstName".</span><span class="sxs-lookup"><span data-stu-id="1781a-173">In hello **User Attributes** section on hello **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="1781a-174">Nella finestra di dialogo di hello SAML degli attributi del token, aggiungere l'attributo "firstName" hello.</span><span class="sxs-lookup"><span data-stu-id="1781a-174">On hello SAML token attributes dialog, add hello "firstName" attribute.</span></span>
 1. <span data-ttu-id="1781a-175">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1781a-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
 
    ![Configura accesso Single Sign-On][6]

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="1781a-178">In hello **nome dell'attributo** casella di testo, nome dell'attributo di tipo hello "firstName".</span><span class="sxs-lookup"><span data-stu-id="1781a-178">In hello **Attribute Name** textbox, type hello attribute name "firstName".</span></span>
 3. <span data-ttu-id="1781a-179">Da hello **valore dell'attributo** elenco, il valore dell'attributo hello selezionare "user.givenname".</span><span class="sxs-lookup"><span data-stu-id="1781a-179">From hello **Attribute Value** list, select hello attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="1781a-180">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1781a-180">Click **Ok**.</span></span>

4. <span data-ttu-id="1781a-181">In hello **URL e il dominio di autenticazione identità SAP HANA Cloud Platform** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1781a-181">On hello **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="1781a-183">In hello **URL di accesso** casella di testo, digitare hello sign in URL per un'applicazione hello SAP.</span><span class="sxs-lookup"><span data-stu-id="1781a-183">In hello **Sign On URL** textbox, type hello sign on URL for hello SAP application.</span></span>
 2. <span data-ttu-id="1781a-184">In hello **identificatore** casella valore hello del tipo di modello:`<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="1781a-184">In hello **Identifier** textbox, type hello value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="1781a-185">Se non si conosce questo valore, seguire la documentazione di autenticazione dell'identità di SAP HANA Cloud Platform hello [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span><span class="sxs-lookup"><span data-stu-id="1781a-185">If you don't know this value, please follow hello SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="1781a-186">In hello **configurazione dell'autenticazione identità SAP HANA Cloud Platform** fare clic su **configurare SAP HANA Cloud Platform identità autenticazione** tooopen **configurasign-on** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1781a-186">On hello **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** tooopen **Configure sign-on** dialog.</span></span> <span data-ttu-id="1781a-187">Quindi, fare clic su **metadati XML SAML** e salvare il file hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1781a-187">Then, click on **SAML XML Metadata** and save hello file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="1781a-190">tooget SSO configurato per l'applicazione, andare tooSAP Console di amministrazione di identità autenticazione HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="1781a-190">tooget SSO configured for your application, go tooSAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="1781a-191">URL di Hello è hello seguente motivo:`https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="1781a-191">hello URL has hello following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="1781a-192">Quindi, seguire troppo documentazione hello in SAP HANA Cloud Platform identità autenticazione[configura Microsoft Azure AD come Provider di identità aziendale all'autenticazione dell'identità di SAP HANA Cloud Platform](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span><span class="sxs-lookup"><span data-stu-id="1781a-192">Then, follow hello documentation on SAP HANA Cloud Platform Identity Authentication too[Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="1781a-193">Nel portale di gestione di Azure hello, fare clic su **salvare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="1781a-193">In hello Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="1781a-194">Continuare seguendo i passaggi solo se si desidera tooadd e abilitare SSO per un'altra applicazione SAP hello.</span><span class="sxs-lookup"><span data-stu-id="1781a-194">Continue hello following steps only if you want tooadd and enable SSO for another SAP application.</span></span> <span data-ttu-id="1781a-195">Ripetere i passaggi in hello sezione "Aggiunta SAP HANA Cloud Platform autenticazione identità dalla raccolta hello" tooadd un'altra istanza di autenticazione dell'identità di SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="1781a-195">Repeat steps under hello section “Adding SAP HANA Cloud Platform Identity Authentication from hello gallery” tooadd another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="1781a-196">Nel portale di gestione di Azure hello in hello **autenticazione dell'identità di SAP HANA Cloud Platform** pagina di integrazione dell'applicazione, fare clic su **collegato Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1781a-196">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![Configurare l'accesso collegato](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="1781a-198">Quindi, salvare la configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="1781a-198">Then, save hello configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="1781a-199">nuova applicazione Hello sfruttano la configurazione di SSO hello per un'applicazione hello precedente SAP.</span><span class="sxs-lookup"><span data-stu-id="1781a-199">hello new application will leverage hello SSO configuration for hello previous SAP application.</span></span> <span data-ttu-id="1781a-200">Assicurarsi di utilizzare hello stesso provider di identità aziendale nella Console di amministrazione di SAP HANA Cloud Platform identità autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="1781a-200">Please make sure you use hello same Corporate Identity Providers in hello SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1781a-201">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1781a-201">Create an Azure AD test user</span></span>
<span data-ttu-id="1781a-202">obiettivo di Hello di questa sezione è toocreate un utente di test nel nuovo portale hello chiamato Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1781a-202">hello objective of this section is toocreate a test user in hello new portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="1781a-204">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1781a-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1781a-205">In hello **portale di gestione di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="1781a-205">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1781a-207">Andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti** elenco hello toodisplay degli utenti.</span><span class="sxs-lookup"><span data-stu-id="1781a-207">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1781a-209">Nella parte superiore di hello della finestra di dialogo hello fare clic su **Aggiungi** tooopen hello **utente** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="1781a-209">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1781a-211">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1781a-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="1781a-213">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1781a-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="1781a-214">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1781a-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="1781a-215">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="1781a-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>
  4. <span data-ttu-id="1781a-216">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1781a-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="1781a-217">Creare un utente test di SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="1781a-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="1781a-218">Non è necessario un utente nell'autenticazione dell'identità di SAP HANA Cloud Platform toocreate.</span><span class="sxs-lookup"><span data-stu-id="1781a-218">You don't need toocreate an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="1781a-219">Gli utenti che sono nell'archivio utente hello Azure AD possono usare funzionalità SSO hello.</span><span class="sxs-lookup"><span data-stu-id="1781a-219">Users who are in hello Azure AD user store can use hello SSO functionality.</span></span>

<span data-ttu-id="1781a-220">Autenticazione dell'identità di SAP HANA Cloud Platform supporta l'opzione di federazione delle identità di hello.</span><span class="sxs-lookup"><span data-stu-id="1781a-220">SAP HANA Cloud Platform Identity Authentication supports hello Identity Federation option.</span></span> <span data-ttu-id="1781a-221">Questa opzione consente toocheck applicazione hello in presenza di utenti hello autenticati dal provider di identità aziendale hello in hello archivio di SAP HANA Cloud Platform identità autenticazione utente.</span><span class="sxs-lookup"><span data-stu-id="1781a-221">This option allows hello application toocheck if hello users authenticated by hello corporate identity provider exist in hello user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="1781a-222">In impostazione hello, hello opzione federazione delle identità è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="1781a-222">In hello default setting, hello Identity Federation option is disabled.</span></span> <span data-ttu-id="1781a-223">Se è abilitata la federazione delle identità, solo gli utenti di hello che vengono importati nell'autenticazione dell'identità di SAP HANA Cloud Platform sono in grado di tooaccess un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1781a-223">If Identity Federation is enabled, only hello users that are imported in SAP HANA Cloud Platform Identity Authentication are able tooaccess hello application.</span></span> 

<span data-ttu-id="1781a-224">Per ulteriori informazioni su come tooenable o federazione delle identità con l'autenticazione identità di SAP HANA Cloud Platform, disabilitare la funzione vedere abilitare la federazione delle identità con l'autenticazione dell'identità in SAP HANA Cloud Platform [Configura federazione identità con hello archivio di SAP HANA Cloud Platform identità autenticazione utente. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span><span class="sxs-lookup"><span data-stu-id="1781a-224">For more information about how tooenable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with hello User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1781a-225">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1781a-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1781a-226">In questa sezione è abilitare Britta Simon toouse single sign-on Azure concedendo proprio tooSAP accesso autenticazione dell'identità di HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="1781a-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooSAP HANA Cloud Platform Identity Authentication.</span></span>

![Assegna utente][200] 

<span data-ttu-id="1781a-228">**tooassign Britta Simon tooSAP autenticazione dell'identità di HANA Cloud Platform, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="1781a-228">**tooassign Britta Simon tooSAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="1781a-229">Nel portale di gestione di Azure hello, aprire visualizzazione applicazioni hello, quindi selezionare la visualizzazione di directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="1781a-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="1781a-231">Nell'elenco di applicazioni hello, selezionare **autenticazione dell'identità di SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="1781a-231">In hello applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="1781a-233">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1781a-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="1781a-235">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1781a-235">Click **Add** button.</span></span> <span data-ttu-id="1781a-236">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1781a-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="1781a-238">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="1781a-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1781a-239">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="1781a-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1781a-240">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="1781a-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="1781a-241">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="1781a-241">Test single sign-on</span></span>

<span data-ttu-id="1781a-242">In questa sezione è verificare la configurazione di SSO AD Azure utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1781a-242">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="1781a-243">Quando si fa clic su riquadro di autenticazione dell'identità di SAP HANA Cloud Platform hello in hello Pannello di accesso, è necessario ottenere l'applicazione SAP HANA Cloud Platform identità autenticazione tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="1781a-243">When you click hello SAP HANA Cloud Platform Identity Authentication tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1781a-244">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="1781a-244">Additional resources</span></span>

* [<span data-ttu-id="1781a-245">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1781a-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1781a-246">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1781a-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png