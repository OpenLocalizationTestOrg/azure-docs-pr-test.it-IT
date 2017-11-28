---
title: 'Esercitazione: Integrazione di Azure Active Directory con SAP Business ByDesign | Documentazione Microsoft'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e SAP Business ByDesign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="4501c-103">Esercitazione: Integrazione di Azure Active Directory con SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="4501c-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="4501c-104">In questa esercitazione, è illustrato come toointegrate SAP Business ByDesign con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4501c-104">In this tutorial, you learn how toointegrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4501c-105">Integrazione di SAP Business ByDesign con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="4501c-105">Integrating SAP Business ByDesign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4501c-106">È possibile controllare in Azure AD che ha accesso tooSAP ByDesign di Business.</span><span class="sxs-lookup"><span data-stu-id="4501c-106">You can control in Azure AD who has access tooSAP Business ByDesign.</span></span>
- <span data-ttu-id="4501c-107">È possibile abilitare l'utenti tooautomatically get connesso tooSAP ByDesign di Business (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4501c-107">You can enable your users tooautomatically get signed-on tooSAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4501c-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4501c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="4501c-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4501c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4501c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4501c-110">Prerequisites</span></span>

<span data-ttu-id="4501c-111">integrazione di Azure AD con SAP Business ByDesign tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="4501c-111">tooconfigure Azure AD integration with SAP Business ByDesign, you need hello following items:</span></span>

- <span data-ttu-id="4501c-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4501c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4501c-113">Sottoscrizione di SAP Business ByDesign abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4501c-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4501c-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="4501c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4501c-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="4501c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4501c-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="4501c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4501c-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4501c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4501c-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="4501c-118">Scenario description</span></span>
<span data-ttu-id="4501c-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="4501c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4501c-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="4501c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4501c-121">Aggiunta di SAP Business ByDesign dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4501c-121">Adding SAP Business ByDesign from hello gallery</span></span>
2. <span data-ttu-id="4501c-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4501c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a><span data-ttu-id="4501c-123">Aggiunta di SAP Business ByDesign dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="4501c-123">Adding SAP Business ByDesign from hello gallery</span></span>
<span data-ttu-id="4501c-124">integrazione hello tooconfigure di SAP Business ByDesign in Azure AD, è necessario tooadd SAP Business ByDesign dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="4501c-124">tooconfigure hello integration of SAP Business ByDesign into Azure AD, you need tooadd SAP Business ByDesign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4501c-125">**tooadd SAP Business ByDesign dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4501c-125">**tooadd SAP Business ByDesign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4501c-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="4501c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="4501c-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="4501c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4501c-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4501c-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="4501c-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4501c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="4501c-133">Nella casella di ricerca hello, digitare **SAP Business ByDesign**selezionare **SAP Business ByDesign** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4501c-133">In hello search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button tooadd hello application.</span></span>

    ![SAP Business ByDesign nell'elenco risultati hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4501c-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4501c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4501c-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con SAP Business ByDesign con un utente test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4501c-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4501c-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in SAP Business ByDesign è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4501c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Business ByDesign is tooa user in Azure AD.</span></span> <span data-ttu-id="4501c-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in SAP Business ByDesign deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="4501c-138">In other words, a link relationship between an Azure AD user and hello related user in SAP Business ByDesign needs toobe established.</span></span>

<span data-ttu-id="4501c-139">In SAP Business ByDesign, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="4501c-139">In SAP Business ByDesign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4501c-140">tooconfigure e prova AD Azure single sign-on con SAP Business ByDesign, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="4501c-140">tooconfigure and test Azure AD single sign-on with SAP Business ByDesign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4501c-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4501c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4501c-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4501c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4501c-143">**[Creare un utente test SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)**  -toohave un equivalente di Britta Simon in SAP Business ByDesign che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4501c-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - toohave a counterpart of Britta Simon in SAP Business ByDesign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4501c-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4501c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4501c-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="4501c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4501c-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4501c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4501c-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="4501c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="4501c-148">**tooconfigure AD Azure single sign-on con SAP Business ByDesign, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4501c-148">**tooconfigure Azure AD single sign-on with SAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="4501c-149">Nel portale di Azure su hello hello **SAP Business ByDesign** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4501c-149">In hello Azure portal, on hello **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="4501c-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4501c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="4501c-153">In hello **SAP Business ByDesign dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4501c-153">On hello **SAP Business ByDesign Domain and URLs** section, perform hello following steps:</span></span>

    ![Informazioni su URL e dominio per l'accesso Single Sign-On di SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="4501c-155">a.</span><span class="sxs-lookup"><span data-stu-id="4501c-155">a.</span></span> <span data-ttu-id="4501c-156">In hello **Sign-on URL** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="4501c-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="4501c-157">b.</span><span class="sxs-lookup"><span data-stu-id="4501c-157">b.</span></span> <span data-ttu-id="4501c-158">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="4501c-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4501c-159">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="4501c-159">These values are not real.</span></span> <span data-ttu-id="4501c-160">Aggiornare questi valori con hello effettivo URL di accesso e l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="4501c-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4501c-161">Contatto [team di supporto Client di SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="4501c-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooget these values.</span></span>

4. <span data-ttu-id="4501c-162">In hello **gli attributi utente** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4501c-162">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![Sezione degli attributi di SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="4501c-164">a.</span><span class="sxs-lookup"><span data-stu-id="4501c-164">a.</span></span> <span data-ttu-id="4501c-165">In **identificatore utente** elenco, seleziona hello **ExtractMailPrefix()** (funzione).</span><span class="sxs-lookup"><span data-stu-id="4501c-165">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="4501c-166">b.</span><span class="sxs-lookup"><span data-stu-id="4501c-166">b.</span></span> <span data-ttu-id="4501c-167">Da hello **posta** elenco, l'attributo utente di selezionare hello da toouse per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="4501c-167">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span> <span data-ttu-id="4501c-168">Ad esempio, se si desidera toouse hello EmployeeID come identificatore utente univoco e archiviato il valore di attributo hello in hello ExtensionAttribute2, quindi selezionare user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="4501c-168">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>   

5. <span data-ttu-id="4501c-169">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="4501c-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="4501c-171">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="4501c-171">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="4501c-173">In hello **SAP Business ByDesign configurazione** fare clic su **configurare SAP Business ByDesign** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="4501c-173">On hello **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4501c-174">Hello copia **SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="4501c-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione di SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="4501c-176">tooget SSO configurato per l'applicazione, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4501c-176">tooget SSO configured for your application, perform hello following steps:</span></span>
   
    <span data-ttu-id="4501c-177">a.</span><span class="sxs-lookup"><span data-stu-id="4501c-177">a.</span></span> <span data-ttu-id="4501c-178">Eseguire l'accesso nel portale di SAP Business ByDesign tooyour con diritti di amministratore.</span><span class="sxs-lookup"><span data-stu-id="4501c-178">Sign on tooyour SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="4501c-179">b.</span><span class="sxs-lookup"><span data-stu-id="4501c-179">b.</span></span> <span data-ttu-id="4501c-180">Passare troppo**attività comuni di gestione utente e di applicazione** e fare clic su hello **Provider di identità** scheda.</span><span class="sxs-lookup"><span data-stu-id="4501c-180">Navigate too**Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="4501c-181">c.</span><span class="sxs-lookup"><span data-stu-id="4501c-181">c.</span></span> <span data-ttu-id="4501c-182">Fare clic su **nuovo Provider di identità** hello selezionare file e metadati XML che è stato scaricato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4501c-182">Click **New Identity Provider** and select hello metadata XML file that you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="4501c-183">Tramite l'importazione di metadati hello, sistema hello carica automaticamente il certificato di firma richiesta hello e certificato di crittografia.</span><span class="sxs-lookup"><span data-stu-id="4501c-183">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="4501c-185">d.</span><span class="sxs-lookup"><span data-stu-id="4501c-185">d.</span></span> <span data-ttu-id="4501c-186">hello tooinclude **URL del servizio Consumer di asserzione** nella richiesta SAML hello, selezionare **URL del servizio Consumer di asserzione includono**.</span><span class="sxs-lookup"><span data-stu-id="4501c-186">tooinclude hello **Assertion Consumer Service URL** into hello SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="4501c-187">e.</span><span class="sxs-lookup"><span data-stu-id="4501c-187">e.</span></span> <span data-ttu-id="4501c-188">Fare clic su **Activate Single Sign-On**(Attiva Single Sign-On).</span><span class="sxs-lookup"><span data-stu-id="4501c-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="4501c-189">f.</span><span class="sxs-lookup"><span data-stu-id="4501c-189">f.</span></span> <span data-ttu-id="4501c-190">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="4501c-190">Save your changes.</span></span>
   
    <span data-ttu-id="4501c-191">g.</span><span class="sxs-lookup"><span data-stu-id="4501c-191">g.</span></span> <span data-ttu-id="4501c-192">Fare clic su hello **risorse del sistema** scheda.</span><span class="sxs-lookup"><span data-stu-id="4501c-192">Click hello **My System** tab.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="4501c-194">h.</span><span class="sxs-lookup"><span data-stu-id="4501c-194">h.</span></span> <span data-ttu-id="4501c-195">Incolla **SAML Single Sign-On Service URL**, che è stato copiato da hello portale di Azure in hello **URL di Azure AD accesso** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="4501c-195">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal it into hello **Azure AD Sign On URL** textbox.</span></span>
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="4501c-197">i.</span><span class="sxs-lookup"><span data-stu-id="4501c-197">i.</span></span> <span data-ttu-id="4501c-198">Specificare se il dipendente hello manualmente è possibile scegliere tra l'accesso con l'ID utente e password o SSO selezionando **selezione Provider di identità manuale**.</span><span class="sxs-lookup"><span data-stu-id="4501c-198">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="4501c-199">j.</span><span class="sxs-lookup"><span data-stu-id="4501c-199">j.</span></span> <span data-ttu-id="4501c-200">In hello **URL SSO** sezione specificare URL hello che deve essere usata dal sistema di hello dipendente toologon toohello.</span><span class="sxs-lookup"><span data-stu-id="4501c-200">In hello **SSO URL** section, specify hello URL that should be used by hello employee toologon toohello system.</span></span> 
    <span data-ttu-id="4501c-201">Elenco a discesa tooEmployee URL inviato hello è possibile scegliere tra hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4501c-201">In hello URL Sent tooEmployee dropdown list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="4501c-202">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="4501c-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="4501c-203">sistema di Hello Invia solo hello normale sistema URL toohello dipendente.</span><span class="sxs-lookup"><span data-stu-id="4501c-203">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="4501c-204">dipendente Hello non è possibile accedere utilizzando SSO e deve utilizzare password o invece del certificato.</span><span class="sxs-lookup"><span data-stu-id="4501c-204">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="4501c-205">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="4501c-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="4501c-206">sistema di Hello Invia solo dipendente di toohello URL SSO hello.</span><span class="sxs-lookup"><span data-stu-id="4501c-206">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="4501c-207">utilizzo di SSO dipendente Hello può accedere.</span><span class="sxs-lookup"><span data-stu-id="4501c-207">hello employee can log on using SSO.</span></span> <span data-ttu-id="4501c-208">Richiesta di autenticazione viene reindirizzato tramite hello IdP.</span><span class="sxs-lookup"><span data-stu-id="4501c-208">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="4501c-209">**Automatic Selection**</span><span class="sxs-lookup"><span data-stu-id="4501c-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="4501c-210">Se SSO non è attivo, il sistema di hello invia dipendente toohello URL normale sistema di hello.</span><span class="sxs-lookup"><span data-stu-id="4501c-210">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="4501c-211">Se SSO è attiva, sistema di hello controlla se il dipendente hello dispone di una password.</span><span class="sxs-lookup"><span data-stu-id="4501c-211">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="4501c-212">Se è disponibile una password, sia URL SSO e SSO di Non vengono inviati toohello dipendente.</span><span class="sxs-lookup"><span data-stu-id="4501c-212">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="4501c-213">Tuttavia, se dipendente hello non dispone di password, solo hello URL SSO viene inviato toohello dipendente.</span><span class="sxs-lookup"><span data-stu-id="4501c-213">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="4501c-214">k.</span><span class="sxs-lookup"><span data-stu-id="4501c-214">k.</span></span> <span data-ttu-id="4501c-215">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="4501c-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="4501c-216">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="4501c-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4501c-217">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="4501c-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4501c-218">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4501c-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4501c-219">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4501c-219">Create an Azure AD test user</span></span>

<span data-ttu-id="4501c-220">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4501c-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="4501c-222">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4501c-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4501c-223">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4501c-223">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4501c-225">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="4501c-225">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4501c-227">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="4501c-227">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4501c-229">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4501c-229">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4501c-231">a.</span><span class="sxs-lookup"><span data-stu-id="4501c-231">a.</span></span> <span data-ttu-id="4501c-232">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4501c-232">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4501c-233">b.</span><span class="sxs-lookup"><span data-stu-id="4501c-233">b.</span></span> <span data-ttu-id="4501c-234">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4501c-234">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="4501c-235">c.</span><span class="sxs-lookup"><span data-stu-id="4501c-235">c.</span></span> <span data-ttu-id="4501c-236">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="4501c-236">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="4501c-237">d.</span><span class="sxs-lookup"><span data-stu-id="4501c-237">d.</span></span> <span data-ttu-id="4501c-238">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="4501c-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="4501c-239">Creare un utente di test di SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="4501c-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="4501c-240">In questa sezione viene creato un utente di nome Britta Simon in SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="4501c-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="4501c-241">Rivolgersi [team di supporto SAP Business ByDesign Client](https://www.sap.com/products/cloud-analytics.support.html) utenti hello tooadd nella piattaforma SAP Business ByDesign hello.</span><span class="sxs-lookup"><span data-stu-id="4501c-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooadd hello users in hello SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="4501c-242">Assicurarsi che il valore NameID deve corrispondere a campo di nome utente hello nella piattaforma SAP Business ByDesign hello.</span><span class="sxs-lookup"><span data-stu-id="4501c-242">Please make sure that NameID value should match with hello username field in hello SAP Business ByDesign platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4501c-243">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4501c-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4501c-244">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooSAP ByDesign di Business.</span><span class="sxs-lookup"><span data-stu-id="4501c-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Business ByDesign.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="4501c-246">**tooassign tooSAP Britta Simon ByDesign Business, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="4501c-246">**tooassign Britta Simon tooSAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="4501c-247">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4501c-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="4501c-249">Nell'elenco di applicazioni hello, selezionare **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="4501c-249">In hello applications list, select **SAP Business ByDesign**.</span></span>

    ![collegamento di SAP Business ByDesign Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="4501c-251">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4501c-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="4501c-253">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4501c-253">Click **Add** button.</span></span> <span data-ttu-id="4501c-254">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4501c-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="4501c-256">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="4501c-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4501c-257">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="4501c-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4501c-258">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="4501c-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4501c-259">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="4501c-259">Test single sign-on</span></span>

<span data-ttu-id="4501c-260">In questa sezione si test configurazione di Azure AD single sign-on utilizzando hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="4501c-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4501c-261">Quando si fa clic su riquadro SAP Business ByDesign hello in hello Pannello di accesso, è necessario ottenere l'applicazione SAP Business ByDesign tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="4501c-261">When you click hello SAP Business ByDesign tile in hello Access Panel, you should get automatically signed-on tooyour SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4501c-262">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="4501c-262">Additional resources</span></span>

* [<span data-ttu-id="4501c-263">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4501c-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4501c-264">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4501c-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

