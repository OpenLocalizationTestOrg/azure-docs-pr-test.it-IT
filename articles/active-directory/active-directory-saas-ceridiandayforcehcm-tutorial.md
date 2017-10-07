---
title: 'Esercitazione: Integrazione di Azure Active Directory con Ceridian Dayforce HCM | Microsoft Docs'
description: Informazioni su come tooconfigure single sign-on tra Azure Active Directory e Ceridian Dayforce HCM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4d72f29b4e5e30ef8881806d789f6676fc541e2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="b5699-103">Esercitazione: Integrazione di Azure Active Directory con Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="b5699-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="b5699-104">In questa esercitazione, è illustrato come toointegrate Ceridian Dayforce HCM con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b5699-104">In this tutorial, you learn how toointegrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5699-105">Integrazione Ceridian Dayforce HCM con Azure AD fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="b5699-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b5699-106">È possibile controllare in Azure AD che ha accesso tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="b5699-106">You can control in Azure AD who has access tooCeridian Dayforce HCM.</span></span>
- <span data-ttu-id="b5699-107">È possibile abilitare l'utenti tooautomatically get connesso tooCeridian Dayforce HCM (Single Sign-On) con i propri account Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5699-107">You can enable your users tooautomatically get signed-on tooCeridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b5699-108">È possibile gestire gli account in un'unica posizione centrale - hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b5699-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b5699-109">Se si desiderano tooknow ulteriori informazioni sull'integrazione dell'applicazione SaaS con Azure AD, vedere [novità di accesso alle applicazioni e single sign-on con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b5699-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5699-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b5699-110">Prerequisites</span></span>

<span data-ttu-id="b5699-111">integrazione di Azure AD con HCM Dayforce Ceridian tooconfigure, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="b5699-111">tooconfigure Azure AD integration with Ceridian Dayforce HCM, you need hello following items:</span></span>

- <span data-ttu-id="b5699-112">Sottoscrizione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5699-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b5699-113">Sottoscrizione di Ceridian Dayforce HCM abilitata per l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b5699-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5699-114">hello tootest i passaggi in questa esercitazione, è consigliabile utilizzare un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="b5699-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b5699-115">passaggi di hello tootest in questa esercitazione, è necessario seguire questi suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="b5699-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b5699-116">Non usare l'ambiente di produzione a meno che non sia necessario.</span><span class="sxs-lookup"><span data-stu-id="b5699-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b5699-117">Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b5699-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b5699-118">Descrizione dello scenario</span><span class="sxs-lookup"><span data-stu-id="b5699-118">Scenario description</span></span>
<span data-ttu-id="b5699-119">In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="b5699-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5699-120">scenario di Hello descritto in questa esercitazione è composto da due componenti principali:</span><span class="sxs-lookup"><span data-stu-id="b5699-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5699-121">Aggiunta di Ceridian Dayforce HCM dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b5699-121">Adding Ceridian Dayforce HCM from hello gallery</span></span>
2. <span data-ttu-id="b5699-122">Configurazione e test dell'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5699-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-hello-gallery"></a><span data-ttu-id="b5699-123">Aggiunta di Ceridian Dayforce HCM dalla raccolta hello</span><span class="sxs-lookup"><span data-stu-id="b5699-123">Adding Ceridian Dayforce HCM from hello gallery</span></span>
<span data-ttu-id="b5699-124">integrazione hello tooconfigure di Ceridian Dayforce HCM in Azure AD, è necessario tooadd Ceridian Dayforce HCM dall'elenco di tooyour hello raccolta di App SaaS gestite.</span><span class="sxs-lookup"><span data-stu-id="b5699-124">tooconfigure hello integration of Ceridian Dayforce HCM into Azure AD, you need tooadd Ceridian Dayforce HCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b5699-125">**tooadd Ceridian Dayforce HCM dalla raccolta di hello, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b5699-125">**tooadd Ceridian Dayforce HCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5699-126">In hello  **[portale di Azure](https://portal.azure.com)**via hello del Pannello di navigazione a sinistra, fare clic su **Azure Active Directory** icona.</span><span class="sxs-lookup"><span data-stu-id="b5699-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![pulsante di Hello Azure Active Directory][1]

2. <span data-ttu-id="b5699-128">Passare troppo**applicazioni aziendali**.</span><span class="sxs-lookup"><span data-stu-id="b5699-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b5699-129">Quindi andare troppo**tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b5699-129">Then go too**All applications**.</span></span>

    ![Pannello di applicazioni Enterprise Hello][2]
    
3. <span data-ttu-id="b5699-131">tooadd nuova applicazione, fare clic su **nuova applicazione** pulsante nella parte superiore di hello della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="b5699-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nuovo pulsante dell'applicazione Hello][3]

4. <span data-ttu-id="b5699-133">Nella casella di ricerca hello, digitare **Ceridian Dayforce HCM**selezionare **Ceridian Dayforce HCM** dal pannello risultati quindi fare clic su **Aggiungi** pulsante applicazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b5699-133">In hello search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Ceridian Dayforce HCM nell'elenco risultati hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b5699-135">Configurare e testare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5699-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b5699-136">In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Ceridian Dayforce HCM usando un utente di test di nome "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b5699-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b5699-137">Per toowork di accesso singolo, Azure AD deve tooknow quale utente controparte hello in Ceridian Dayforce HCM è tooa utente in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5699-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ceridian Dayforce HCM is tooa user in Azure AD.</span></span> <span data-ttu-id="b5699-138">In altre parole, una relazione di collegamento tra un utente di Azure Active Directory e l'utente correlato di hello in Ceridian Dayforce HCM deve toobe stabilita.</span><span class="sxs-lookup"><span data-stu-id="b5699-138">In other words, a link relationship between an Azure AD user and hello related user in Ceridian Dayforce HCM needs toobe established.</span></span>

<span data-ttu-id="b5699-139">In Ceridian Dayforce HCM, assegnare il valore di hello di hello **nome utente** in Azure AD come valore hello hello **Username** tooestablish relazione di collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="b5699-139">In Ceridian Dayforce HCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b5699-140">tooconfigure e prova AD Azure single sign-on con Ceridian Dayforce HCM, è necessario hello toocomplete seguenti blocchi predefiniti:</span><span class="sxs-lookup"><span data-stu-id="b5699-140">tooconfigure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b5699-141">**[Configurare Azure Active Directory Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable il toouse utenti questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b5699-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b5699-142">**[Creare un utente prova AD Azure](#create-an-azure-ad-test-user)**  -tootest AD Azure single sign-on con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b5699-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5699-143">**[Creare un utente test HCM Dayforce Ceridian](#create-a-ceridian-dayforce-hcm-test-user)**  -toohave un equivalente di Britta Simon in Ceridian Dayforce HCM che è la rappresentazione toohello collegato Azure AD dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b5699-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - toohave a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b5699-144">**[Assegnare l'utente test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD accesso single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b5699-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5699-145">**[Testare single sign-on](#test-single-sign-on)**  -tooverify hello se funzionamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="b5699-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b5699-146">Configurare l'accesso Single Sign-On di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5699-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b5699-147">In questa sezione, si abilita Azure AD single sign-on in hello portale di Azure e configurare l'accesso single sign-on nell'applicazione HCM Dayforce Ceridian.</span><span class="sxs-lookup"><span data-stu-id="b5699-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="b5699-148">**tooconfigure AD Azure single sign-on con Ceridian Dayforce HCM, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b5699-148">**tooconfigure Azure AD single sign-on with Ceridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5699-149">Nel portale di Azure su hello hello **Ceridian Dayforce HCM** pagina di integrazione dell'applicazione, fare clic su **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b5699-149">In hello Azure portal, on hello **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![Collegamento per la configurazione dell'accesso Single Sign-On][4]

2. <span data-ttu-id="b5699-151">In hello **Single sign-on** finestra di dialogo Seleziona **modalità** come **basato su SAML Sign-on** tooenable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b5699-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Finestra di dialogo Single Sign-On](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="b5699-153">In hello **Ceridian Dayforce HCM dominio e gli URL** seguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b5699-153">On hello **Ceridian Dayforce HCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="b5699-155">a.</span><span class="sxs-lookup"><span data-stu-id="b5699-155">a.</span></span> <span data-ttu-id="b5699-156">In hello **URL di accesso** casella di testo, digitare l'URL hello usato da tooyour il toosign a utenti applicazione HCM Dayforce Ceridian.</span><span class="sxs-lookup"><span data-stu-id="b5699-156">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="b5699-157">Environment</span><span class="sxs-lookup"><span data-stu-id="b5699-157">Environment</span></span> | <span data-ttu-id="b5699-158">URL</span><span class="sxs-lookup"><span data-stu-id="b5699-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="b5699-159">Per la produzione</span><span class="sxs-lookup"><span data-stu-id="b5699-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="b5699-160">Per il test</span><span class="sxs-lookup"><span data-stu-id="b5699-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="b5699-161">b.</span><span class="sxs-lookup"><span data-stu-id="b5699-161">b.</span></span> <span data-ttu-id="b5699-162">In hello **identificatore** casella di testo, digitare un URL utilizzando hello seguente modello:</span><span class="sxs-lookup"><span data-stu-id="b5699-162">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    
    | <span data-ttu-id="b5699-163">Environment</span><span class="sxs-lookup"><span data-stu-id="b5699-163">Environment</span></span> | <span data-ttu-id="b5699-164">URL</span><span class="sxs-lookup"><span data-stu-id="b5699-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="b5699-165">Per la produzione</span><span class="sxs-lookup"><span data-stu-id="b5699-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="b5699-166">Per il test</span><span class="sxs-lookup"><span data-stu-id="b5699-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="b5699-167">c.</span><span class="sxs-lookup"><span data-stu-id="b5699-167">c.</span></span> <span data-ttu-id="b5699-168">In hello **URL di risposta** casella di testo, digitare l'URL hello usato dalla risposta hello toopost di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5699-168">In hello **Reply URL** textbox, type hello URL used by Azure AD toopost hello response.</span></span>
    
    | <span data-ttu-id="b5699-169">Environment</span><span class="sxs-lookup"><span data-stu-id="b5699-169">Environment</span></span> | <span data-ttu-id="b5699-170">URL</span><span class="sxs-lookup"><span data-stu-id="b5699-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="b5699-171">Per la produzione</span><span class="sxs-lookup"><span data-stu-id="b5699-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="b5699-172">Per il test</span><span class="sxs-lookup"><span data-stu-id="b5699-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="b5699-173">Poiché questi non sono i valori reali,</span><span class="sxs-lookup"><span data-stu-id="b5699-173">These values are not real.</span></span> <span data-ttu-id="b5699-174">Aggiornare questi valori con hello effettivo identificatore, l'URL di risposta e URL Sign-On.</span><span class="sxs-lookup"><span data-stu-id="b5699-174">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="b5699-175">Contatto [team di supporto Client di HCM Dayforce Ceridian](https://www.ceridian.com/contact-us/index.html) tooget questi valori.</span><span class="sxs-lookup"><span data-stu-id="b5699-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) tooget these values.</span></span>

4. <span data-ttu-id="b5699-176">In hello **certificato di firma SAML** fare clic su **Metadata XML** e quindi salvare il file di metadati hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="b5699-176">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![collegamento al download del certificato Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="b5699-178">L'applicazione Ceridian Dayforce HCM prevede asserzioni SAML hello in un formato specifico.</span><span class="sxs-lookup"><span data-stu-id="b5699-178">Your Ceridian Dayforce HCM application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="b5699-179">Lavorare con [team di supporto Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) primo tooidentify hello utente corretto l'identificatore.</span><span class="sxs-lookup"><span data-stu-id="b5699-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first tooidentify hello correct user identifier.</span></span> <span data-ttu-id="b5699-180">Microsoft consiglia di usare hello **"name"** attributo come identificatore utente.</span><span class="sxs-lookup"><span data-stu-id="b5699-180">Microsoft recommends using hello **"name"** attribute as user identifier.</span></span> <span data-ttu-id="b5699-181">È possibile gestire i valori hello di questi attributi da hello **gli attributi utente** sezione nella pagina di integrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b5699-181">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="b5699-182">Hello seguente schermata mostra un esempio per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="b5699-182">hello following screenshot shows an example for this.</span></span>  

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="b5699-184">In hello **gli attributi utente** sezione hello **Single sign-on** finestra di dialogo, configurare attributi token SAML, come illustrato nell'immagine di hello precedente ed eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b5699-184">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="b5699-185">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="b5699-185">Attribute Name</span></span>  | <span data-ttu-id="b5699-186">Valore attributo</span><span class="sxs-lookup"><span data-stu-id="b5699-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="b5699-187">name</span><span class="sxs-lookup"><span data-stu-id="b5699-187">name</span></span>  | <span data-ttu-id="b5699-188">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="b5699-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="b5699-189">a.</span><span class="sxs-lookup"><span data-stu-id="b5699-189">a.</span></span> <span data-ttu-id="b5699-190">Fare clic su **Aggiungi attributo** tooopen hello **Aggiungi attributo** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="b5699-190">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="b5699-193">b.</span><span class="sxs-lookup"><span data-stu-id="b5699-193">b.</span></span> <span data-ttu-id="b5699-194">In hello **nome** casella di testo, nome dell'attributo di tipo hello mostrato per la riga.</span><span class="sxs-lookup"><span data-stu-id="b5699-194">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="b5699-195">c.</span><span class="sxs-lookup"><span data-stu-id="b5699-195">c.</span></span> <span data-ttu-id="b5699-196">In hello **valore** elenco, l'attributo utente di selezionare hello da toouse per l'implementazione.</span><span class="sxs-lookup"><span data-stu-id="b5699-196">In hello **Value** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="b5699-197">Ad esempio, se si desidera toouse hello EmployeeID come identificatore utente univoco e archiviato il valore di attributo hello in hello ExtensionAttribute2, quindi selezionare **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="b5699-197">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="b5699-198">d.</span><span class="sxs-lookup"><span data-stu-id="b5699-198">d.</span></span> <span data-ttu-id="b5699-199">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5699-199">Click **Ok**.</span></span>

7. <span data-ttu-id="b5699-200">Fare clic sul pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="b5699-200">Click **Save** button.</span></span>

    ![Pulsante Salva di Configura accesso Single Sign-On](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="b5699-202">In hello **Ceridian Dayforce HCM configurazione** fare clic su **configurare Ceridian Dayforce HCM** tooopen **Configura sign-on** finestra.</span><span class="sxs-lookup"><span data-stu-id="b5699-202">On hello **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b5699-203">Hello copia **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** da hello **sezione di riferimento rapido.**</span><span class="sxs-lookup"><span data-stu-id="b5699-203">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurazione Ceridian Dayforce HCM](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="b5699-205">tooconfigure single sign-on sul **Ceridian Dayforce HCM** lato, è necessario hello toosend scaricato **Metadata XML** e **Sign-Out URL, l'ID entità SAML e SAML Single Sign-On Service URL** troppo[team di supporto HCM Dayforce Ceridian](https://www.ceridian.com/contact-us/index.html).</span><span class="sxs-lookup"><span data-stu-id="b5699-205">tooconfigure single sign-on on **Ceridian Dayforce HCM** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="b5699-206">È ora possibile leggere una versione di queste istruzioni all'interno di hello concisa [portale di Azure](https://portal.azure.com), mentre si stanno impostando app hello!</span><span class="sxs-lookup"><span data-stu-id="b5699-206">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b5699-207">Dopo l'aggiunta di questa app da hello **Active Directory > applicazioni aziendali** fare semplicemente clic su hello **Single Sign-On** scheda e l'accesso hello incorporato documentazione tramite hello  **Configurazione** sezione nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="b5699-207">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b5699-208">È possibile leggere altre informazioni sulla funzionalità di documentazione embedded hello qui: [AD Azure incorporato documentazione]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b5699-208">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b5699-209">Creare un utente test di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5699-209">Create an Azure AD test user</span></span>

<span data-ttu-id="b5699-210">obiettivo di Hello di questa sezione è un utente di test nel portale di Azure chiamato Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b5699-210">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creare un utente test di Azure AD][100]

<span data-ttu-id="b5699-212">**un utente di prova in Azure AD, toocreate eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b5699-212">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5699-213">Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su hello **Azure Active Directory** pulsante.</span><span class="sxs-lookup"><span data-stu-id="b5699-213">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![pulsante di Hello Azure Active Directory](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b5699-215">elenco di hello toodisplay di utenti, andare troppo**utenti e gruppi**, quindi fare clic su **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="b5699-215">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello "Utenti e gruppi" e i collegamenti di "Tutti gli utenti"](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b5699-217">hello tooopen **utente** la finestra di dialogo, fare clic su **Aggiungi** nella parte superiore di hello di hello **tutti gli utenti** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="b5699-217">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![pulsante Aggiungi Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b5699-219">In hello **utente** finestra di dialogo eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b5699-219">In hello **User** dialog box, perform hello following steps:</span></span>

    ![finestra di dialogo utente Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b5699-221">a.</span><span class="sxs-lookup"><span data-stu-id="b5699-221">a.</span></span> <span data-ttu-id="b5699-222">In hello **nome** digitare **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b5699-222">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b5699-223">b.</span><span class="sxs-lookup"><span data-stu-id="b5699-223">b.</span></span> <span data-ttu-id="b5699-224">In hello **nome utente** casella Tipo hello di indirizzo di posta elettronica dell'utente Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b5699-224">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b5699-225">c.</span><span class="sxs-lookup"><span data-stu-id="b5699-225">c.</span></span> <span data-ttu-id="b5699-226">Seleziona hello **Show Password** casella di controllo e quindi annotare i valori hello visualizzati in hello **Password** casella.</span><span class="sxs-lookup"><span data-stu-id="b5699-226">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b5699-227">d.</span><span class="sxs-lookup"><span data-stu-id="b5699-227">d.</span></span> <span data-ttu-id="b5699-228">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b5699-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="b5699-229">Creazione di un utente di test Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="b5699-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="b5699-230">obiettivo di Hello di questa sezione è un utente denominato Britta Simon in Ceridian Dayforce HCM toocreate.</span><span class="sxs-lookup"><span data-stu-id="b5699-230">hello objective of this section is toocreate a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="b5699-231">Lavorare con hello [team di supporto HCM Dayforce Ceridian](https://www.ceridian.com/contact-us/index.html) tooget utenti aggiunti in applicazione Ceridian Dayforce HCM hello.</span><span class="sxs-lookup"><span data-stu-id="b5699-231">Work with hello [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) tooget users added in hello Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b5699-232">Assegnazione utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5699-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b5699-233">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="b5699-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Assegna utente][200] 

<span data-ttu-id="b5699-235">**tooassign tooCeridian Britta Simon Dayforce HCM, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b5699-235">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5699-236">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b5699-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b5699-238">Nell'elenco di applicazioni hello, selezionare **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="b5699-238">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![Configura accesso Single Sign-On](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="b5699-240">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b5699-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Assegna utente][202] 

4. <span data-ttu-id="b5699-242">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b5699-242">Click **Add** button.</span></span> <span data-ttu-id="b5699-243">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b5699-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assegna utente][203]

5. <span data-ttu-id="b5699-245">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="b5699-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b5699-246">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b5699-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5699-247">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b5699-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b5699-248">Assegnare l'utente test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5699-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b5699-249">In questa sezione per abilitare Britta Simon toouse single sign-on Azure concessione dell'accesso tooCeridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="b5699-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCeridian Dayforce HCM.</span></span>

![Assegnazione del ruolo utente hello][200] 

<span data-ttu-id="b5699-251">**tooassign tooCeridian Britta Simon Dayforce HCM, eseguire hello alla procedura seguente:**</span><span class="sxs-lookup"><span data-stu-id="b5699-251">**tooassign Britta Simon tooCeridian Dayforce HCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="b5699-252">Nel portale di Azure hello, aprire la visualizzazione di applicazioni hello, quindi selezionare Visualizza directory toohello e andare troppo**applicazioni aziendali** quindi fare clic su **tutte le applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="b5699-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Assegna utente][201] 

2. <span data-ttu-id="b5699-254">Nell'elenco di applicazioni hello, selezionare **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="b5699-254">In hello applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![collegamento Ceridian Dayforce HCM Hello nell'elenco delle applicazioni hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="b5699-256">Dal menu hello hello sinistra, fare clic su **utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b5699-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![collegamento di "Utenti e gruppi" Hello][202]

4. <span data-ttu-id="b5699-258">Fare clic sul pulsante **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b5699-258">Click **Add** button.</span></span> <span data-ttu-id="b5699-259">Selezionare quindi **Utenti e gruppi** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b5699-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![riquadro assegnazione aggiungere Hello][203]

5. <span data-ttu-id="b5699-261">In **utenti e gruppi** finestra di dialogo Seleziona **Britta Simon** nell'elenco di utenti hello.</span><span class="sxs-lookup"><span data-stu-id="b5699-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b5699-262">Fare clic sul pulsante **Seleziona** nella finestra di dialogo **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="b5699-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5699-263">Fare clic sul pulsante **Assegna** nella finestra di dialogo **Aggiungi assegnazione**.</span><span class="sxs-lookup"><span data-stu-id="b5699-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b5699-264">Testare l'accesso Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="b5699-264">Test single sign-on</span></span>

<span data-ttu-id="b5699-265">obiettivo di Hello di questa sezione è tootest la configurazione di single sign-on di Azure AD mediante hello Pannello di accesso.</span><span class="sxs-lookup"><span data-stu-id="b5699-265">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="b5699-266">Quando si fa clic su riquadro Ceridian Dayforce HCM hello in hello Pannello di accesso, è necessario ottenere applicazione HCM Dayforce Ceridian tooyour automaticamente firmato-on.</span><span class="sxs-lookup"><span data-stu-id="b5699-266">When you click hello Ceridian Dayforce HCM tile in hello Access Panel, you should get automatically signed-on tooyour Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b5699-267">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="b5699-267">Additional resources</span></span>

* [<span data-ttu-id="b5699-268">Elenco di esercitazioni sulla tooIntegrate App SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5699-268">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5699-269">Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5699-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

