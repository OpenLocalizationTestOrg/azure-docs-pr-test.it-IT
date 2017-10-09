---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP Cloud for Customer | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e il Cloud di SAP per cliente.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="76aa7-103">Esercitazione: Integrazione di Azure Active Directory con SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="76aa7-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="76aa7-104">In questa esercitazione, è illustrato come toointegrate SAP Cloud per il cliente con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="76aa7-104">In this tutorial, you learn how toointegrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="76aa7-105">L'integrazione Cloud SAP per cliente con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="76aa7-105">Integrating SAP Cloud for Customer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="76aa7-106">È possibile controllare in Azure AD che ha accesso tooSAP Cloud per cliente</span><span class="sxs-lookup"><span data-stu-id="76aa7-106">You can control in Azure AD who has access tooSAP Cloud for Customer</span></span>
- <span data-ttu-id="76aa7-107">È possibile abilitare l'utenti tooautomatically get connesso tooSAP Cloud per cliente (Single Sign-On) con i propri account Azure AD</span><span class="sxs-lookup"><span data-stu-id="76aa7-107">You can enable your users tooautomatically get signed-on tooSAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="76aa7-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="76aa7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="76aa7-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="76aa7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76aa7-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="76aa7-110">Prerequisites</span></span>

<span data-ttu-id="76aa7-111">tooconfigure integrazione di Azure AD con SAP Cloud per cliente, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="76aa7-111">tooconfigure Azure AD integration with SAP Cloud for Customer, you need hello following items:</span></span>

- <span data-ttu-id="76aa7-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76aa7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="76aa7-113">Sottoscrizione di SAP Cloud for Customer abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="76aa7-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="76aa7-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="76aa7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="76aa7-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="76aa7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="76aa7-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="76aa7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="76aa7-117">Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese: [offerta prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76aa7-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="76aa7-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="76aa7-118">Scenario description</span></span>
<span data-ttu-id="76aa7-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="76aa7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="76aa7-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="76aa7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="76aa7-121">Aggiunta di Cloud di SAP per cliente dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="76aa7-121">Adding SAP Cloud for Customer from hello gallery</span></span>
2. <span data-ttu-id="76aa7-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="76aa7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a><span data-ttu-id="76aa7-123">Aggiunta di Cloud di SAP per cliente dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="76aa7-123">Adding SAP Cloud for Customer from hello gallery</span></span>
<span data-ttu-id="76aa7-124">integrazione hello tooconfigure di SAP Cloud per il cliente in Azure AD, è necessario tooadd Cloud SAP per cliente dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="76aa7-124">tooconfigure hello integration of SAP Cloud for Customer into Azure AD, you need tooadd SAP Cloud for Customer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="76aa7-125">**tooadd Cloud SAP per cliente dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="76aa7-125">**tooadd SAP Cloud for Customer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="76aa7-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="76aa7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="76aa7-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="76aa7-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-129">Then go too**All applications**.</span></span>

    ![Applicazioni][2]
    
3. <span data-ttu-id="76aa7-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="76aa7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applicazioni][3]

4. <span data-ttu-id="76aa7-133">Nella casella di ricerca hello, digitare **Cloud SAP per cliente**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-133">In hello search box, type **SAP Cloud for Customer**.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="76aa7-135">Nel riquadro dei risultati hello, selezionare **Cloud SAP per cliente**, quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="76aa7-135">In hello results panel, select **SAP Cloud for Customer**, and then click **Add** button tooadd hello application.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="76aa7-137">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="76aa7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="76aa7-138">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAP Cloud for Customer con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="76aa7-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="76aa7-139">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello nel Cloud di SAP per il cliente è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76aa7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Cloud for Customer is tooa user in Azure AD.</span></span> <span data-ttu-id="76aa7-140">In altre parole, una relazione di collegamento tra un utente di Azure AD e l'utente correlato di hello nel Cloud di SAP per il cliente deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="76aa7-140">In other words, a link relationship between an Azure AD user and hello related user in SAP Cloud for Customer needs toobe established.</span></span>

<span data-ttu-id="76aa7-141">Nel Cloud di SAP per cliente, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="76aa7-141">In SAP Cloud for Customer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="76aa7-142">tooconfigure e test con SAP Cloud AD Azure single sign-on per cliente, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="76aa7-142">tooconfigure and test Azure AD single sign-on with SAP Cloud for Customer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="76aa7-143">**[Configurazione di Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="76aa7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="76aa7-144">**[Creazione di un utente prova AD Azure](#creating-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="76aa7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="76aa7-145">**[Creazione di un Cloud di SAP per l'utente test cliente](#creating-a-sap-cloud-for-customer-test-user)**  -toohave un equivalente di Britta Simon nel Cloud di SAP per il cliente che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="76aa7-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - toohave a counterpart of Britta Simon in SAP Cloud for Customer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="76aa7-146">**[Assegnazione utente di prova hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="76aa7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="76aa7-147">**[Test di Single Sign-On](#testing-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="76aa7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="76aa7-148">Configurazione dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="76aa7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="76aa7-149">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nel Cloud per l'applicazione clienti SAP.</span><span class="sxs-lookup"><span data-stu-id="76aa7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="76aa7-150">**tooconfigure AD Azure single sign-on con il Cloud di SAP per cliente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="76aa7-150">**tooconfigure Azure AD single sign-on with SAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="76aa7-151">Nel portale di Azure su hello hello **Cloud SAP per cliente** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-151">In hello Azure portal, on hello **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Configura accesso Single Sign-On][4]

2. <span data-ttu-id="76aa7-153">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="76aa7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="76aa7-155">In hello **Cloud SAP per il dominio del cliente e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="76aa7-155">On hello **SAP Cloud for Customer Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="76aa7-157">a.</span><span class="sxs-lookup"><span data-stu-id="76aa7-157">a.</span></span> <span data-ttu-id="76aa7-158">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="76aa7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="76aa7-159">b.</span><span class="sxs-lookup"><span data-stu-id="76aa7-159">b.</span></span> <span data-ttu-id="76aa7-160">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="76aa7-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="76aa7-161">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="76aa7-161">These values are not real.</span></span> <span data-ttu-id="76aa7-162">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="76aa7-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="76aa7-163">Contatto [Cloud SAP per il team di supporto clienti Client](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="76aa7-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget these values.</span></span> 

4. <span data-ttu-id="76aa7-164">In hello **gli attributi utente** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="76aa7-164">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="76aa7-166">a.</span><span class="sxs-lookup"><span data-stu-id="76aa7-166">a.</span></span> <span data-ttu-id="76aa7-167">In **identificatore utente** elenco, seleziona hello **ExtractMailPrefix()** (funzione).</span><span class="sxs-lookup"><span data-stu-id="76aa7-167">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="76aa7-168">b.</span><span class="sxs-lookup"><span data-stu-id="76aa7-168">b.</span></span> <span data-ttu-id="76aa7-169">Da hello **posta** elenco, l'attributo utente di selezionare hello da toouse per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="76aa7-169">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="76aa7-170">Ad esempio, se si desidera toouse hello EmployeeID come identificatore utente univoco e archiviato il valore di attributo hello in hello ExtensionAttribute2, quindi selezionare user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="76aa7-170">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="76aa7-171">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="76aa7-171">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="76aa7-173">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="76aa7-173">Click **Save** button.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="76aa7-175">In hello **Cloud SAP per la configurazione personalizzata** fare clic su **configurare SAP Cloud per cliente** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="76aa7-175">On hello **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="76aa7-176">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="76aa7-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="76aa7-178">tooget SSO configurato, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="76aa7-178">tooget SSO configured, perform hello following steps:</span></span>
   
    <span data-ttu-id="76aa7-179">a.</span><span class="sxs-lookup"><span data-stu-id="76aa7-179">a.</span></span> <span data-ttu-id="76aa7-180">Accedere al portale di SAP Cloud for Customer con diritti di amministratore.</span><span class="sxs-lookup"><span data-stu-id="76aa7-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="76aa7-181">b.</span><span class="sxs-lookup"><span data-stu-id="76aa7-181">b.</span></span> <span data-ttu-id="76aa7-182">Passare toohello **attività comuni di gestione utente e di applicazione** e fare clic su hello **Provider di identità** scheda.</span><span class="sxs-lookup"><span data-stu-id="76aa7-182">Navigate toohello **Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="76aa7-183">c.</span><span class="sxs-lookup"><span data-stu-id="76aa7-183">c.</span></span> <span data-ttu-id="76aa7-184">Fare clic su **nuovo Provider di identità** e hello selezionare file XML di metadati scaricato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="76aa7-184">Click **New Identity Provider** and select hello metadata XML file you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="76aa7-185">Tramite l'importazione di metadati hello, sistema hello carica automaticamente il certificato di firma richiesta hello e certificato di crittografia.</span><span class="sxs-lookup"><span data-stu-id="76aa7-185">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="76aa7-187">d.</span><span class="sxs-lookup"><span data-stu-id="76aa7-187">d.</span></span> <span data-ttu-id="76aa7-188">Azure Active Directory richiede hello elemento URL del servizio Consumer di asserzione richiesta SAML hello, pertanto selezionare hello **URL del servizio Consumer di asserzione includono** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="76aa7-188">Azure Active Directory requires hello element Assertion Consumer Service URL in hello SAML request, so select hello **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="76aa7-189">e.</span><span class="sxs-lookup"><span data-stu-id="76aa7-189">e.</span></span> <span data-ttu-id="76aa7-190">Fare clic su **Activate Single Sign-On**(Attiva Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="76aa7-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="76aa7-191">f.</span><span class="sxs-lookup"><span data-stu-id="76aa7-191">f.</span></span> <span data-ttu-id="76aa7-192">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="76aa7-192">Save your changes.</span></span>
   
    <span data-ttu-id="76aa7-193">g.</span><span class="sxs-lookup"><span data-stu-id="76aa7-193">g.</span></span> <span data-ttu-id="76aa7-194">Fare clic su hello **risorse del sistema** scheda.</span><span class="sxs-lookup"><span data-stu-id="76aa7-194">Click hello **My System** tab.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="76aa7-196">h.</span><span class="sxs-lookup"><span data-stu-id="76aa7-196">h.</span></span> <span data-ttu-id="76aa7-197">Nella casella di testo **URL di accesso di Azure AD** incollare il valore dell'**URL del servizio Single Sign-On SAML** copiato dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="76aa7-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="76aa7-199">i.</span><span class="sxs-lookup"><span data-stu-id="76aa7-199">i.</span></span> <span data-ttu-id="76aa7-200">Specificare se il dipendente hello manualmente è possibile scegliere tra l'accesso con l'ID utente e password o SSO selezionando hello **selezione Provider di identità manuale**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-200">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting hello **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="76aa7-201">j.</span><span class="sxs-lookup"><span data-stu-id="76aa7-201">j.</span></span> <span data-ttu-id="76aa7-202">In hello **URL SSO** sezione specificare URL hello che deve essere utilizzata da toosign i dipendenti nel sistema toohello.</span><span class="sxs-lookup"><span data-stu-id="76aa7-202">In hello **SSO URL** section, specify hello URL that should be used by your employees toosign on toohello system.</span></span> 
    <span data-ttu-id="76aa7-203">In hello **tooEmployee URL inviato** elenco, è possibile scegliere tra hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="76aa7-203">In hello **URL Sent tooEmployee** list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="76aa7-204">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="76aa7-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="76aa7-205">sistema di Hello Invia solo hello normale sistema URL toohello dipendente.</span><span class="sxs-lookup"><span data-stu-id="76aa7-205">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="76aa7-206">dipendente Hello non è possibile accedere utilizzando SSO e deve utilizzare password o invece del certificato.</span><span class="sxs-lookup"><span data-stu-id="76aa7-206">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="76aa7-207">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="76aa7-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="76aa7-208">sistema di Hello Invia solo dipendente di toohello URL SSO hello.</span><span class="sxs-lookup"><span data-stu-id="76aa7-208">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="76aa7-209">utilizzo di SSO dipendente Hello può accedere.</span><span class="sxs-lookup"><span data-stu-id="76aa7-209">hello employee can log on using SSO.</span></span> <span data-ttu-id="76aa7-210">Richiesta di autenticazione viene reindirizzato tramite hello IdP.</span><span class="sxs-lookup"><span data-stu-id="76aa7-210">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="76aa7-211">**Automatic Selection**</span><span class="sxs-lookup"><span data-stu-id="76aa7-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="76aa7-212">Se SSO non è attivo, il sistema di hello invia dipendente toohello URL normale sistema di hello.</span><span class="sxs-lookup"><span data-stu-id="76aa7-212">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="76aa7-213">Se SSO è attiva, sistema di hello controlla se il dipendente hello dispone di una password.</span><span class="sxs-lookup"><span data-stu-id="76aa7-213">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="76aa7-214">Se è disponibile una password, sia URL SSO e SSO di Non vengono inviati toohello dipendente.</span><span class="sxs-lookup"><span data-stu-id="76aa7-214">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="76aa7-215">Tuttavia, se dipendente hello non dispone di password, solo hello URL SSO viene inviato toohello dipendente.</span><span class="sxs-lookup"><span data-stu-id="76aa7-215">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="76aa7-216">k.</span><span class="sxs-lookup"><span data-stu-id="76aa7-216">k.</span></span> <span data-ttu-id="76aa7-217">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="76aa7-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="76aa7-218">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="76aa7-218">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="76aa7-219">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="76aa7-219">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="76aa7-220">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="76aa7-220">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="76aa7-221">Creazione di un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="76aa7-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="76aa7-222">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="76aa7-222">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creare un utente di Azure AD][100]

<span data-ttu-id="76aa7-224">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="76aa7-224">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="76aa7-225">In hello **portale di Azure**via hello riquadro di spostamento a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="76aa7-225">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="76aa7-227">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi** e fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-227">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="76aa7-229">hello tooopen **utente** finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="76aa7-229">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="76aa7-231">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="76aa7-231">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="76aa7-233">a.</span><span class="sxs-lookup"><span data-stu-id="76aa7-233">a.</span></span> <span data-ttu-id="76aa7-234">In hello **nome** casella tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-234">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="76aa7-235">b.</span><span class="sxs-lookup"><span data-stu-id="76aa7-235">b.</span></span> <span data-ttu-id="76aa7-236">In hello **nome utente** casella di testo, hello tipo **indirizzo di posta elettronica** di BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="76aa7-236">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="76aa7-237">c.</span><span class="sxs-lookup"><span data-stu-id="76aa7-237">c.</span></span> <span data-ttu-id="76aa7-238">Selezionare **Show Password** e annotare il valore di hello di hello **Password**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-238">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="76aa7-239">d.</span><span class="sxs-lookup"><span data-stu-id="76aa7-239">d.</span></span> <span data-ttu-id="76aa7-240">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="76aa7-241">Creazione di un utente di test di SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="76aa7-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="76aa7-242">In questa sezione viene creato un utente di nome Britta Simon in SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="76aa7-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="76aa7-243">Rivolgersi [Cloud SAP per il team di supporto clienti](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) utenti hello tooadd hello Cloud SAP per la piattaforma di cliente.</span><span class="sxs-lookup"><span data-stu-id="76aa7-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd hello users in hello SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="76aa7-244">Assicurarsi che il valore NameID deve corrispondere con il campo username hello in hello Cloud SAP per la piattaforma di cliente.</span><span class="sxs-lookup"><span data-stu-id="76aa7-244">Please make sure that NameID value should match with hello username field in hello SAP Cloud for Customer platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="76aa7-245">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="76aa7-245">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="76aa7-246">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSAP Cloud per cliente.</span><span class="sxs-lookup"><span data-stu-id="76aa7-246">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Cloud for Customer.</span></span>

![Assegna utente][200] 

<span data-ttu-id="76aa7-248">**tooassign Britta Simon tooSAP Cloud per cliente, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="76aa7-248">**tooassign Britta Simon tooSAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="76aa7-249">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-249">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="76aa7-251">Nell'elenco di applicazioni hello, selezionare **Cloud SAP per cliente**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-251">In hello applications list, select **SAP Cloud for Customer**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="76aa7-253">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-253">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="76aa7-255">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-255">Click **Add** button.</span></span> <span data-ttu-id="76aa7-256">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="76aa7-258">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="76aa7-258">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="76aa7-259">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="76aa7-260">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="76aa7-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="76aa7-261">Test dell'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="76aa7-261">Testing single sign-on</span></span>

<span data-ttu-id="76aa7-262">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="76aa7-262">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="76aa7-263">Quando si fa clic hello SAP Cloud riquadro cliente in hello Pannello di accesso, è necessario ottenere tooyour automaticamente firmato nel Cloud di SAP per l'applicazione del cliente.</span><span class="sxs-lookup"><span data-stu-id="76aa7-263">When you click hello SAP Cloud for Customer tile in hello Access Panel, you should get automatically signed-on tooyour SAP Cloud for Customer application.</span></span>
<span data-ttu-id="76aa7-264">Per ulteriori informazioni su hello Pannello di accesso, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="76aa7-264">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="76aa7-265">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="76aa7-265">Additional resources</span></span>

* [<span data-ttu-id="76aa7-266">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76aa7-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="76aa7-267">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76aa7-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

